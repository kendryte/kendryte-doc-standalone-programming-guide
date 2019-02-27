# 集成电路内置音频总线 (I2S)

## Overview

I2S 标准总线定义了三种信号: 时钟信号 BCK、声道选择信号 WS 和串行数据信号 SD。一个基本的I2S 数据总线有一个主机和一个从机。主机和从机的角色在通信过程中保持不变。I2S 模块包含独立的发送和接收声道，能够保证优良的通信性能。

## Features

I2S 模块具有以下功能:

- 根据音频格式自动配置设备（支持 16、24、32 位深，44100 采样率，1 - 4 声道）
- 可配置为播放或录音模式
- 自动管理音频缓冲区

## API

Corresponding header file `i2s.h`

Provide the following interfaces

- i2s\_init
- i2s\_send\_data\_dma
- i2s\_recv\_data\_dma
- i2s\_rx\_channel\_config
- i2s\_tx\_channel\_config
- i2s\_play
- i2s\_set\_sample\_rate: I2S 设置采样率。
- i2s\_set\_dma\_divide\_16: 设置dma_divide_16，16位数据时设置dma_divide_16，DMA传输时自动将32比特INT32数据分成两个16比特的左右声道数据。
- i2s\_get\_dma\_divide\_16: 获取dma_divide_16值。用于判断是否需要设置dma_divide_16。

### i2s\_init

#### Description

Initialize I2S.

#### Function prototype

```c
void i2s_init(i2s_device_number_t device_num, i2s_transmit_t rxtx_mode, uint32_t channel_mask)
```

#### Parameter

| Element name            | Description         |  Input or output  |
| ------------------ | ------------ | --------- |
| device\_num         | I2S号        | Input      |
| rxtx\_mode          | 接收或发送模式| Input      |
| channel\_mask       | 通道掩码      | Input      |

#### Return value

None.

### i2s\_send\_data\_dma

#### Description

I2S发送数据。

#### Function prototype

```c
void i2s_send_data_dma(i2s_device_number_t device_num, const void *buf, size_t buf_len, dmac_channel_number_t channel_num)
```

#### Parameter

| Element name            | Description         |  Input or output  |
| ------------------ | ------------ | --------- |
| device\_num         | I2S号        | Input      |
| buf                | 发送数据地址  | Input      |
| buf\_len            | 数据长度      | Input      |
| channel\_num        | DMA通道号     | Input      |

#### Return value

None.

### i2s\_recv\_data\_dma

#### Description

I2S接收数据。

#### Function prototype

```c
void i2s_recv_data_dma(i2s_device_number_t device_num, uint32_t *buf, size_t buf_len, dmac_channel_number_t channel_num)
```

#### Parameter

| Element name            | Description         |  Input or output  |
| ------------------  | ------------ | --------- |
| device\_num         | I2S号        | Input      |
| buf                 | 接收数据地址  | Output      |
| buf\_len            | 数据长度      | Input      |
| channel\_num        | DMA通道号     | Input      |

#### Return value

None.

### i2s\_rx\_channel\_config

#### Description

设置接收通道参数。

#### Function prototype

```c
void i2s_rx_channel_config(i2s_device_number_t device_num, i2s_channel_num_t channel_num, i2s_word_length_t word_length, i2s_word_select_cycles_t word_select_size, i2s_fifo_threshold_t trigger_level, i2s_work_mode_t word_mode)
```

#### Parameter

| Element name            | Description              |  Input or output  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | Input      |
| channel\_num        | 通道号             | Input     |
| word\_length        | 接收数据位数       | Output      |
| word\_select\_size   | 单个数据时钟数     | Input      |
| trigger\_level      | DMA触发时FIFO深度  | Input      |
| word\_mode          | 工作模式           | Input      |

#### Return value

None.

### i2s\_tx\_channel\_config

#### Description

设置发送通道参数。

#### Function prototype

```c
void i2s_tx_channel_config(i2s_device_number_t device_num, i2s_channel_num_t channel_num, i2s_word_length_t word_length, i2s_word_select_cycles_t word_select_size, i2s_fifo_threshold_t trigger_level, i2s_work_mode_t word_mode)
```

#### Parameter

| Element name            | Description              |  Input or output  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | Input      |
| channel\_num        | 通道号             | Input     |
| word\_length        | 接收数据位数       | Output      |
| word\_select\_size   | 单个数据时钟数     | Input      |
| trigger\_level      | DMA触发时FIFO深度  | Input      |
| word\_mode          | 工作模式           | Input      |

#### Return value

None.

### i2s\_play

#### Description

发送PCM数据, 比如播放音乐

#### Function prototype

```c
void i2s_play(i2s_device_number_t device_num, dmac_channel_number_t channel_num,
              const uint8_t *buf, size_t buf_len, size_t frame, size_t bits_per_sample, uint8_t track_num)
```

#### Parameter

| Element name            | Description              |  Input or output  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | Input      |
| channel\_num        | 通道号             | Input     |
| buf                 | PCM 数据           | Input      |
| buf\_len             | PCM数据长度        | Input      |
| frame               | 单次发送数量        | Input      |
| bits\_per\_sample     | 单次采样位宽        | Input      |
| track_num           | 声道数            | Input      |

#### Return value

None.

### i2s\_set\_sample\_rate

#### Description

设置采样率。

#### Function prototype

```c
uint32_t i2s_set_sample_rate(i2s_device_number_t device_num, uint32_t sample_rate)
```

#### Parameter

| Element name            | Description              |  Input or output  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | Input      |
| sample\_rate        | 采样率            | Input     |

#### Return value

实际的采样率。

### i2s\_set\_dma\_divide\_16

#### Description

设置dma\_divide\_16，16位数据时设置dma\_divide\_16，DMA传输时自动将32比特INT32数据分成两个16比特的左右声道数据。

#### Function prototype

```c
int i2s_set_dma_divide_16(i2s_device_number_t device_num, uint32_t enable)
```

#### Parameter

| Element name            | Description              |  Input or output  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | Input      |
| enable              | 0:禁用 1: 使能    | Input     |

#### Return value

| Return value              | Description       |
| :------------------ | :-------- |
| 0                   | Success      |
| Others                 | Fail       |

### i2s\_get\_dma\_divide\_16

#### Description

获取dma\_divide\_16值。用于判断是否需要设置dma\_divide\_16。

#### Function prototype

```c
int i2s_get_dma_divide_16(i2s_device_number_t device_num)
```

#### Parameter

| Element name            | Description              |  Input or output  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | Input      |

#### Return value

| Return value              | Description       |
| :------------------ | :-------- |
| 1                   | 使能      |
| 0                   | 禁用      |
| <0                 | Fail       |

### Example

```c
/* I2S0 通道0 设置为接收通道，接收16位数据，单次传输32个时钟，FIFO深度为4，标准模式。接收8组数据*/
/* I2S2 通道1 设置为发送通道，发送16位数据，单次传输32个时钟，FIFO深度为4，右对齐模式。发送8组数据*/
uint32_t buf[8];
i2s_init(I2S_DEVICE_0, I2S_RECEIVER, 0x3);
i2s_init(I2S_DEVICE_2, I2S_TRANSMITTER, 0xC);
i2s_rx_channel_config(I2S_DEVICE_0, I2S_CHANNEL_0, RESOLUTION_16_BIT, SCLK_CYCLES_32, TRIGGER_LEVEL_4, STANDARD_MODE);
i2s_tx_channel_config(I2S_DEVICE_2, I2S_CHANNEL_1, RESOLUTION_16_BIT, SCLK_CYCLES_32, TRIGGER_LEVEL_4, RIGHT_JUSTIFYING_MODE);
i2s_recv_data_dma(I2S_DEVICE_0, rx_buf, 8, DMAC_CHANNEL1);
i2s_send_data_dma(I2S_DEVICE_2, buf, 8, DMAC_CHANNEL0);
```

## Data type

The relevant data types and data structures are defined as follows:

- i2s\_device\_number\_t: I2S编号。

- i2s\_channel\_num\_t: I2S通道号。

- i2s\_transmit\_t: I2S传输模式。

- i2s\_work_mode\_t: I2S工作模式。

- i2s\_word_select\_cycles\_t: I2S单次传输时钟数。

- i2s\_word_length\_t: I2S传输数据位数。

- i2s\_fifo\_threshold\_t: I2S FIFO深度。

### i2s\_device\_number\_t

#### Description

I2S编号。

#### Type definition

```c
typedef enum _i2s_device_number
{
    I2S_DEVICE_0 = 0,
    I2S_DEVICE_1 = 1,
    I2S_DEVICE_2 = 2,
    I2S_DEVICE_MAX
} i2s_device_number_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| I2S\_DEVICE\_0     | I2S 0       |
| I2S\_DEVICE\_1     | I2S 1       |
| I2S\_DEVICE\_2     | I2S 2       |

### i2s\_channel\_num\_t

#### Description

I2S通道号。

#### Type definition

```c
typedef enum _i2s_channel_num
{
    I2S_CHANNEL_0 = 0,
    I2S_CHANNEL_1 = 1,
    I2S_CHANNEL_2 = 2,
    I2S_CHANNEL_3 = 3
} i2s_channel_num_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| I2S\_CHANNEL\_0    | I2S通道0    |
| I2S\_CHANNEL\_1    | I2S通道1    |
| I2S\_CHANNEL\_2    | I2S通道2    |
| I2S\_CHANNEL\_3    | I2S通道3    |

### i2s\_transmit\_t

#### Description

I2S传输模式。

#### Type definition

```c
typedef enum _i2s_transmit
{
    I2S_TRANSMITTER = 0,
    I2S_RECEIVER = 1
} i2s_transmit_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| I2S\_TRANSMITTER   | 发送模式    |
| I2S\_RECEIVER      | 接收模式    |

### i2s\_work_mode\_t

#### Description

I2S工作模式。

#### Type definition

```c
typedef enum _i2s_work_mode
{
    STANDARD_MODE = 1,
    RIGHT_JUSTIFYING_MODE = 2,
    LEFT_JUSTIFYING_MODE = 4
} i2s_work_mode_t;
```

#### Enumeration element

| Element name                  | Description        |
| ------------------------ | ----------- |
| STANDARD_MODE            | 标准模式    |
| RIGHT\_JUSTIFYING\_MODE    | 右对齐模式   |
| LEFT\_JUSTIFYING\_MODE     | 左对齐模式   |

### i2s\_word_select\_cycles\_t

#### Description

I2S单次传输时钟数。

#### Type definition

```c
typedef enum _word_select_cycles
{
    SCLK_CYCLES_16 = 0x0,
    SCLK_CYCLES_24 = 0x1,
    SCLK_CYCLES_32 = 0x2
} i2s_word_select_cycles_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| SCLK\_CYCLES\_16   | 16个时钟    |
| SCLK\_CYCLES\_24   | 24个时钟    |
| SCLK\_CYCLES\_32   | 32个时钟    |

### i2s\_word_length\_t

#### Description

I2S传输数据位数。

#### Type definition

```c
typedef enum _word_length
{
    IGNORE_WORD_LENGTH = 0x0,
    RESOLUTION_12_BIT = 0x1,
    RESOLUTION_16_BIT = 0x2,
    RESOLUTION_20_BIT = 0x3,
    RESOLUTION_24_BIT = 0x4,
    RESOLUTION_32_BIT = 0x5
} i2s_word_length_t;
```

#### Enumeration element

| Element name              | Description        |
| -------------------- | ----------- |
| IGNORE\_WORD\_LENGTH | 忽略长度     |
| RESOLUTION\_12\_BIT  | 12位数据长度 |
| RESOLUTION\_16\_BIT  | 16位数据长度 |
| RESOLUTION\_20\_BIT  | 20位数据长度 |
| RESOLUTION\_24\_BIT  | 24位数据长度 |
| RESOLUTION\_32\_BIT  | 32位数据长度 |

### i2s\_fifo\_threshold\_t

#### Description

I2S FIFO深度。

#### Type definition

```c
typedef enum _fifo_threshold
{
    /* Interrupt trigger when FIFO level is 1 */
    TRIGGER_LEVEL_1 = 0x0,
    /* Interrupt trigger when FIFO level is 2 */
    TRIGGER_LEVEL_2 = 0x1,
    /* Interrupt trigger when FIFO level is 3 */
    TRIGGER_LEVEL_3 = 0x2,
    /* Interrupt trigger when FIFO level is 4 */
    TRIGGER_LEVEL_4 = 0x3,
    /* Interrupt trigger when FIFO level is 5 */
    TRIGGER_LEVEL_5 = 0x4,
    /* Interrupt trigger when FIFO level is 6 */
    TRIGGER_LEVEL_6 = 0x5,
    /* Interrupt trigger when FIFO level is 7 */
    TRIGGER_LEVEL_7 = 0x6,
    /* Interrupt trigger when FIFO level is 8 */
    TRIGGER_LEVEL_8 = 0x7,
    /* Interrupt trigger when FIFO level is 9 */
    TRIGGER_LEVEL_9 = 0x8,
    /* Interrupt trigger when FIFO level is 10 */
    TRIGGER_LEVEL_10 = 0x9,
    /* Interrupt trigger when FIFO level is 11 */
    TRIGGER_LEVEL_11 = 0xa,
    /* Interrupt trigger when FIFO level is 12 */
    TRIGGER_LEVEL_12 = 0xb,
    /* Interrupt trigger when FIFO level is 13 */
    TRIGGER_LEVEL_13 = 0xc,
    /* Interrupt trigger when FIFO level is 14 */
    TRIGGER_LEVEL_14 = 0xd,
    /* Interrupt trigger when FIFO level is 15 */
    TRIGGER_LEVEL_15 = 0xe,
    /* Interrupt trigger when FIFO level is 16 */
    TRIGGER_LEVEL_16 = 0xf
} i2s_fifo_threshold_t;
```

#### Enumeration element

| Element name              | Description         |
| -------------------- | ------------ |
| TRIGGER\_LEVEL\_1    | 1字节FIFO深度 |
| TRIGGER\_LEVEL\_2    | 2字节FIFO深度 |
| TRIGGER\_LEVEL\_3    | 3字节FIFO深度 |
| TRIGGER\_LEVEL\_4    | 4字节FIFO深度 |
| TRIGGER\_LEVEL\_5    | 5字节FIFO深度 |
| TRIGGER\_LEVEL\_6    | 6字节FIFO深度 |
| TRIGGER\_LEVEL\_7    | 7字节FIFO深度 |
| TRIGGER\_LEVEL\_8    | 8字节FIFO深度 |
| TRIGGER\_LEVEL\_9    | 9字节FIFO深度 |
| TRIGGER\_LEVEL\_10   | 10字节FIFO深度|
| TRIGGER\_LEVEL\_11   | 11字节FIFO深度|
| TRIGGER\_LEVEL\_12   | 12字节FIFO深度|
| TRIGGER\_LEVEL\_13   | 13字节FIFO深度|
| TRIGGER\_LEVEL\_14   | 14字节FIFO深度|
| TRIGGER\_LEVEL\_15   | 15字节FIFO深度|
| TRIGGER\_LEVEL\_16   | 16字节FIFO深度|