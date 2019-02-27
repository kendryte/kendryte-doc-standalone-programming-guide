# FFT

## Overview

Fast Fourier Transform (FFT) Accelerator.

The FFT accelerator implements the radix-2 decimation-in-time (DIT)
Cooley–Tukey FFT algorithm[^cooley_tukey] acceleration in hardware.

[^cooley_tukey]: https://en.wikipedia.org/wiki/Cooley%E2%80%93Tukey_FFT_algorithm

## Features

The FFT accelerator currently supports 64-point, 128-point, 256-point,
and 512-point FFTs and IFFTs. Inside the FFT accelerator, there are two SRAMs
with a size of 512 * 32 bits. After the configuration is completed, the FFT
sends a TX request to the DMA, and the data sent by the DMA is placed in one of
the SRAMs until the data volume satisfies the current FFT operation needs, and
the FFT operation begins at this point.
The butterfly operation unit reads data from the SRAM which containing the valid
data, and writes the data to another SRAM after the end of the operation.
The next butterfly operation reads the data from the SRAM just written, when the
operation ends write to another SRAM.
This process alternates this way until the entire FFT operation is completed.

## API

Corresponding header file `fft.h`

Provide the following interfaces

- [fft\_complex\_uint16\_dma](#fft\_complex\_uint16\_dma)

### fft\_complex\_uint16\_dma

#### Description

FFT operation.

#### Function prototype

```c
void fft_complex_uint16_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, uint16_t shift, fft_direction_t direction, const uint64_t *input, size_t point_num, uint64_t *output);
```

#### Parameter

|       Parameter name       |                              Description                              | Input or output |
| :------------------------- | :-------------------------------------------------------------------- | :-------------- |
| dma\_send\_channel\_num    | DMA channel number used to send data                                  | Input           |
| dma\_receive\_channel\_num | DMA channel number used to receive data                               | Input           |
| shift                      | Data shift setting[^fft_shift]                                        | Input           |
| direction                  | FFT or IFFT                                                           | Input           |
| input                      | Input data sequence, format is RIRI...[^precision]                    | Input           |
| point\_num                 | The number of data points to be calculated can only be 512/256/128/64 | Input           |
| output                     | The result after the operation. The format is RIRI...[^precision]     | Output          |

[^fft_shift]: The 16-bit register (-32768~32767) of the FFT accelerator may
overflow during the operation, and the FFT transform has 9 layers. Shift setting
determines which layer needs to be shifted to prevent overflow, such as 0x1ff
means that 9 layers are all shifted; 0x03 means The first layer and the second
layer are shifted. If it is shifted, the transformed amplitude is not the
amplitude of the normal FFT transform. For the corresponding relationship, refer
to the fft_test test demo program, they contain examples of solving frequency
points, phases, and amplitudes.

[^precision]: The precision of both the real part and the imaginary part is 16 bit.

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

The relevant data types and data structures are defined as follows:

- fft\_data\_t：The data format passed in by the FFT operation.
- fft\_direction\_t：FFT transform mode.

### fft\_data\_t

#### Description

The data format passed in by the FFT operation.

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

#### Enumeration element

| Element name |              Description              |
| :----------- | :------------------------------------ |
| I1           | The imaginary part of the first data  |
| R1           | The real part of the first data       |
| I2           | The imaginary part of the second data |
| R2           | The real part of the second data      |

### fft\_direction\_t

#### Description

FFT transform mode.

#### Type definition

```c
typedef enum _fft_direction
{
    FFT_DIR_BACKWARD,
    FFT_DIR_FORWARD,
    FFT_DIR_MAX,
} fft_direction_t;
```

#### Enumeration element

|    Element name    |          Description          |
| :----------------- | :---------------------------- |
| FFT\_DIR\_BACKWARD | FFT inverse transform (FFT)   |
| FFT\_DIR\_FORWARD  | FFT positive transform (IFFT) |