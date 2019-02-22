# 快速傅里叶变换加速器(FFT)

## Summary

FFT模块是用硬件的方式来实现FFT的基2时分运算加速。

## Features

目前该模块可以支持64点、128点、256点以及512点的FFT以及IFFT。在FFT内部有两块大小为512*32bit的SRAM，在配置完成后FFT会向DMA发送TX请求，将DMA送来的送据放到其中的一块SRAM中去，直到满足当前FFT运算所需要的数据量并开始FFT运算，蝶形运算单元从包含有有效数据的SRAM中读出数据，运算结束后将数据写到另外一块SRAM中去，下次蝶形运算再从刚写入的SRAM中读出数据，运算结束后并写入另外一块SRAM，如此反复交替进行直到完成整个FFT运算。

## API

Corresponding header file `fft.h`

Provide the following interfaces

- [fft\_complex\_uint16\_dma](#fft\_complex\_uint16\_dma)

### fft\_complex\_uint16\_dma

#### Description

FFT运算。

#### Function prototype

```c
void fft_complex_uint16_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, uint16_t shift, fft_direction_t direction, const uint64_t *input, size_t point_num, uint64_t *output);
```

#### Parameter

| Parameter name                                  |   Description                     |  Input or output  |
| :--------------------------------------- | :------------------------- | :-------- |
| dma\_send\_channel\_num                  | 发送数据使用的DMA通道号      | Input       |
| dma\_receive\_channel\_num               | 接收数据使用的DMA通道号      | Input       |
| shift    | FFT模块16位寄存器导致数据溢出(-32768~32767)，FFT变换有9层，shift决定哪一层需要移位操作(如0x1ff表示9层都做移位操作；0x03表示第第一层与第二层做移位操作)，防止溢出。如果移位了，则变换后的幅值不是正常FFT变换的幅值，对应关系可以参考fft_test测试demo程序。包含了求解频率点、相位、幅值的示例| Input |
| direction                                | FFT正变换或是逆变换          | Input       |
| input                                    | Input的数据序列，格式为RIRI..,实部与虚部的精度都为16bit| Input|
| point\_num                               | 待运算的数据点数，只能为512/256/128/64 | Input |
| output                                   | 运算后结果。格式为RIRI..,实部与虚部的精度都为16bit | Output |

#### Return value

None.

### Example

```c
#define FFT_N               512U
#define FFT_FORWARD_SHIFT   0x0U
#define FFT_BACKWARD_SHIFT  0x1ffU
#define PI                  3.14159265358979323846
complex_hard_t data_hard[FFT_N] = {0};
for (i = 0; i < FFT_N; i++)
{
    tempf1[0] = 0.3 * cosf(2 * PI * i / FFT_N + PI / 3) * 256;
    tempf1[1] = 0.1 * cosf(16 * 2 * PI * i / FFT_N - PI / 9) * 256;
    tempf1[2] = 0.5 * cosf((19 * 2 * PI * i / FFT_N) + PI / 6) * 256;
    data_hard[i].real = (int16_t)(tempf1[0] + tempf1[1] + tempf1[2] + 10);
    data_hard[i].imag = (int16_t)0;
}
for (int i = 0; i < FFT_N / 2; ++i)
{
    input_data = (fft_data_t *)&buffer_input[i];
    input_data->R1 = data_hard[2 * i].real;
    input_data->I1 = data_hard[2 * i].imag;
    input_data->R2 = data_hard[2 * i + 1].real;
    input_data->I2 = data_hard[2 * i + 1].imag;
}
fft_complex_uint16_dma(DMAC_CHANNEL0, DMAC_CHANNEL1, FFT_FORWARD_SHIFT, FFT_DIR_FORWARD, buffer_input, FFT_N, buffer_output);
for (i = 0; i < FFT_N / 2; i++)
{
    output_data = (fft_data_t*)&buffer_output[i];
    data_hard[2 * i].imag = output_data->I1 ;
    data_hard[2 * i].real = output_data->R1 ;
    data_hard[2 * i + 1].imag = output_data->I2 ;
    data_hard[2 * i + 1].real = output_data->R2 ;
}
for (int i = 0; i < FFT_N / 2; ++i)
{
    input_data = (fft_data_t *)&buffer_input[i];
    input_data->R1 = data_hard[2 * i].real;
    input_data->I1 = data_hard[2 * i].imag;
    input_data->R2 = data_hard[2 * i + 1].real;
    input_data->I2 = data_hard[2 * i + 1].imag;
}
fft_complex_uint16_dma(DMAC_CHANNEL0, DMAC_CHANNEL1, FFT_BACKWARD_SHIFT, FFT_DIR_BACKWARD, buffer_input, FFT_N, buffer_output);
for (i = 0; i < FFT_N / 2; i++)
{
    output_data = (fft_data_t*)&buffer_output[i];
    data_hard[2 * i].imag = output_data->I1 ;
    data_hard[2 * i].real = output_data->R1 ;
    data_hard[2 * i + 1].imag = output_data->I2 ;
    data_hard[2 * i + 1].real = output_data->R2 ;
}
```

## Data type

相关数据类型、数据结构定义如下：

- fft\_data\_t：FFT运算传入的数据格式。
- fft\_direction\_t：FFT变换模式。

### fft\_data\_t

#### Description

FFT运算传入的数据格式。

#### Type definition

```c
typedef struct tag_fft_data
{
    int16_t I1;
    int16_t R1;
    int16_t I2;
    int16_t R2;
} fft_data_t;
```

#### 成员

| 成员名称 | Description |
| :----- | :--- |
| I1 | 第一个数据的虚部  |
| R1 | 第一个数据的实部  |
| I2 | 第二个数据的虚部  |
| R2 | 第二个数据的实部  |

### fft\_direction\_t

#### Description

FFT变换模式

#### Type definition

```c
typedef enum _fft_direction
{
    FFT_DIR_BACKWARD,
    FFT_DIR_FORWARD,
    FFT_DIR_MAX,
} fft_direction_t;
```

#### 成员

| 成员名称 | Description |
| :----- | :--- |
| FFT\_DIR\_BACKWARD | FFT逆变换 |
| FFT\_DIR\_FORWARD  | FFT正变换 |