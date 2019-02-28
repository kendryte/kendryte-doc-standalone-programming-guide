# I2S

## Overview

The Integrated Inter-IC Sound Bus (I2S) is a serial bus interface standard used for connecting digital audio devices together.

The I2S bus defines three types of signals: the clock signal BCK, the channel selection signal WS, and the serial data signal SD. A basic I2S bus has one master and one slave. The roles of the master and slave remain unchanged during the communication process. The I2S unit includes separate transmit and receive channels for excellent communication performance.

## Features

The I2S module has the following features:

- Automatically configure the device according to the audio format (supports 16, 24, 32 bit depth, 44100 sample rate, 1 - 4 channels)
- Configurable for playback or recording mode
- Automatic management of audio buffers

## API

Corresponding header file `i2s.h`

Provide the following interfaces

- i2s\_init
- i2s\_send\_data\_dma
- i2s\_recv\_data\_dma
- i2s\_rx\_channel\_config
- i2s\_tx\_channel\_config
- i2s\_play
- i2s\_set\_sample\_rate: I2S set the sampling rate.
- i2s\_set\_dma\_divide\_16: Set dma_divide_16, set dma_divide_16 for 16-bit data, and automatically divide 32-bit INT32 data into two 16-bit left and right channel data during DMA transfer.
- i2s\_get\_dma\_divide\_16: Get the dma_divide_16 value. Used to determine if dma_divide_16 needs to be set.

### i2s\_init

#### Description

Initialize I2S.

#### Function prototype

```c
void i2s_init(i2s_device_number_t device_num, i2s_transmit_t rxtx_mode, uint32_t channel_mask)
```

#### Parameter

| Element name  |       Description        | Input or output |
| ------------- | ------------------------ | --------------- |
| device\_num   | I2S number               | Input           |
| rxtx\_mode    | Receive or transmit mode | Input           |
| channel\_mask | Channel mask             | Input           |

#### Return value

None.

### i2s\_send\_data\_dma

#### Description

I2S sends data over DMA.

#### Function prototype

```c
void i2s_send_data_dma(i2s_device_number_t device_num, const void *buf, size_t buf_len, dmac_channel_number_t channel_num)
```

#### Parameter

| Element name |    Description     | Input or output |
| ------------ | ------------------ | --------------- |
| device\_num  | I2S number         | Input           |
| buf          | Send data address  | Input           |
| buf\_len     | Data length        | Input           |
| channel\_num | DMA channel number | Input           |

#### Return value

None.

### i2s\_recv\_data\_dma

#### Description

I2S receives data.

#### Function prototype

```c
void i2s_recv_data_dma(i2s_device_number_t device_num, uint32_t *buf, size_t buf_len, dmac_channel_number_t channel_num)
```

#### Parameter

| Element name |     Description      | Input or output |
| ------------ | -------------------- | --------------- |
| device\_num  | I2S number           | Input           |
| buf          | Receive data address | Output          |
| buf\_len     | Data length          | Input           |
| channel\_num | DMA channel number   | Input           |

#### Return value

None.

### i2s\_rx\_channel\_config

#### Description

Set the receive channel parameters.

#### Function prototype

```c
void i2s_rx_channel_config(i2s_device_number_t device_num, i2s_channel_num_t channel_num, i2s_word_length_t word_length, i2s_word_select_cycles_t word_select_size, i2s_fifo_threshold_t trigger_level, i2s_work_mode_t word_mode)
```

#### Parameter

|    Element name    |           Description            | Input or output |
| ------------------ | -------------------------------- | --------------- |
| device\_num        | I2S number                       | Input           |
| channel\_num       | Channel number                   | Input           |
| word\_length       | Word length (bits)               | Output          |
| word\_select\_size | Word select size                 | Input           |
| trigger\_level     | FIFO depth when DMA is triggered | Input           |
| word\_mode         | Word mode                        | Input           |

#### Return value

None.

### i2s\_tx\_channel\_config

#### Description

Set the send channel parameters.

#### Function prototype

```c
void i2s_tx_channel_config(i2s_device_number_t device_num, i2s_channel_num_t channel_num, i2s_word_length_t word_length, i2s_word_select_cycles_t word_select_size, i2s_fifo_threshold_t trigger_level, i2s_work_mode_t word_mode)
```

#### Parameter

|    Element name    |           Description            | Input or output |
| ------------------ | -------------------------------- | --------------- |
| device\_num        | I2S number                       | Input           |
| channel\_num       | Channel number                   | Input           |
| word\_length       | Word length (bits)               | Output          |
| word\_select\_size | Word select size                 | Input           |
| trigger\_level     | FIFO depth when DMA is triggered | Input           |
| word\_mode         | Word mode                        | Input           |

#### Return value

None.

### i2s\_play

#### Description

Send PCM data, such as playing music

#### Function prototype

```c
void i2s_play(i2s_device_number_t device_num, dmac_channel_number_t channel_num,
              const uint8_t *buf, size_t buf_len, size_t frame, size_t bits_per_sample, uint8_t track_num)
```

#### Parameter

|   Element name    |        Description        | Input or output |
| ----------------- | ------------------------- | --------------- |
| device\_num       | I2S number                | Input           |
| channel\_num      | Channel number            | Input           |
| buf               | PCM data                  | Input           |
| buf\_len          | PCM data length           | Input           |
| frame             | Single send quantity      | Input           |
| bits\_per\_sample | Single sampling bit width | Input           |
| track_num         | Number of channels        | Input           |

#### Return value

None.

### i2s\_set\_sample\_rate

#### Description

Set the sampling rate.

#### Function prototype

```c
uint32_t i2s_set_sample_rate(i2s_device_number_t device_num, uint32_t sample_rate)
```

#### Parameter

| Element name |  Description  | Input or output |
| ------------ | ------------- | --------------- |
| device\_num  | I2S number    | Input           |
| sample\_rate | Sampling Rate | Input           |

#### Return value

Actual sampling rate.

### i2s\_set\_dma\_divide\_16

#### Description

Set dma\_divide\_16, set dma\_divide\_16 for 16-bit data, and automatically split 32-bit INT32 data into two 16-bit left and right channel data during DMA transfer.

#### Function prototype

```c
int i2s_set_dma_divide_16(i2s_device_number_t device_num, uint32_t enable)
```

#### Parameter

| Element name |     Description      | Input or output |
| ------------ | -------------------- | --------------- |
| device\_num  | I2S number           | Input           |
| enable       | 0: Disable 1: Enable | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### i2s\_get\_dma\_divide\_16

#### Description

Get the dma\_divide\_16 value. Used to determine if you need to set dma\_divide\_16.

#### Function prototype

```c
int i2s_get_dma_divide_16(i2s_device_number_t device_num)
```

#### Parameter

| Element name | Description | Input or output |
| ------------ | ----------- | --------------- |
| device\_num  | I2S number  | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 1            | Enable      |
| 0            | Disable     |
| <0           | Fail        |

### Example

```c
/*
 * I2S0 Channel 0 is set to receive channel, receive 16-bit data, 32 clocks in a
 * single transmission, FIFO depth is 4, standard mode. Receive 8 sets of data.
 * I2S2 Channel 1 is set to transmit channel, transmitting 16-bit data, 32
 * clocks in a single transmission, FIFO depth is 4, right-aligned mode. Send 8
 * sets of data
 */
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

- i2s\_device\_number\_t: I2S device number.

- i2s\_channel\_num\_t: I2S channel number.

- i2s\_transmit\_t: I2S transmission mode.

- i2s\_work_mode\_t: I2S working mode.

- i2s\_word_select\_cycles\_t: The number of I2S single transmission clocks.

- i2s\_word_length\_t: The number of data bits transmitted by I2S.

- i2s\_fifo\_threshold\_t: I2S FIFO depth.

### i2s\_device\_number\_t

#### Description

I2S device number.

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

|  Element name  | Description |
| -------------- | ----------- |
| I2S\_DEVICE\_0 | I2S 0       |
| I2S\_DEVICE\_1 | I2S 1       |
| I2S\_DEVICE\_2 | I2S 2       |

### i2s\_channel\_num\_t

#### Description

I2S channel number.

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

|  Element name   |  Description  |
| --------------- | ------------- |
| I2S\_CHANNEL\_0 | I2S channel 0 |
| I2S\_CHANNEL\_1 | I2S channel 1 |
| I2S\_CHANNEL\_2 | I2S channel 2 |
| I2S\_CHANNEL\_3 | I2S channel 3 |

### i2s\_transmit\_t

#### Description

I2S transmission mode.

#### Type definition

```c
typedef enum _i2s_transmit
{
    I2S_TRANSMITTER = 0,
    I2S_RECEIVER = 1
} i2s_transmit_t;
```

#### Enumeration element

|   Element name   | Description  |
| ---------------- | ------------ |
| I2S\_TRANSMITTER | Send mode    |
| I2S\_RECEIVER    | Receive mode |

### i2s\_work_mode\_t

#### Description

I2S working mode.

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

|      Element name       |     Description      |
| ----------------------- | -------------------- |
| STANDARD_MODE           | Standard mode        |
| RIGHT\_JUSTIFYING\_MODE | Right justified mode |
| LEFT\_JUSTIFYING\_MODE  | Left justified mode  |

### i2s\_word_select\_cycles\_t

#### Description

The number of I2S single transmission clocks.

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

|   Element name   |   Description   |
| ---------------- | --------------- |
| SCLK\_CYCLES\_16 | 16 clock cycles |
| SCLK\_CYCLES\_24 | 24 clock cycles |
| SCLK\_CYCLES\_32 | 32 clock cycles |

### i2s\_word_length\_t

#### Description

The number of data bits transmitted by I2S.

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

|     Element name     |    Description     |
| -------------------- | ------------------ |
| IGNORE\_WORD\_LENGTH | Ignore word length |
| RESOLUTION\_12\_BIT  | 12 bit data length |
| RESOLUTION\_16\_BIT  | 16 bit data length |
| RESOLUTION\_20\_BIT  | 20 bit data length |
| RESOLUTION\_24\_BIT  | 24 bit data length |
| RESOLUTION\_32\_BIT  | 32 bit data length |

### i2s\_fifo\_threshold\_t

#### Description

I2S FIFO depth.

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

|    Element name    |    Description     |
| ------------------ | ------------------ |
| TRIGGER\_LEVEL\_1  | 1 Byte FIFO depth  |
| TRIGGER\_LEVEL\_2  | 2 Byte FIFO depth  |
| TRIGGER\_LEVEL\_3  | 3 Byte FIFO depth  |
| TRIGGER\_LEVEL\_4  | 4 Byte FIFO depth  |
| TRIGGER\_LEVEL\_5  | 5 Byte FIFO depth  |
| TRIGGER\_LEVEL\_6  | 6 Byte FIFO depth  |
| TRIGGER\_LEVEL\_7  | 7 Byte FIFO depth  |
| TRIGGER\_LEVEL\_8  | 8 Byte FIFO depth  |
| TRIGGER\_LEVEL\_9  | 9 Byte FIFO depth  |
| TRIGGER\_LEVEL\_10 | 10 Byte FIFO depth |
| TRIGGER\_LEVEL\_11 | 11 Byte FIFO depth |
| TRIGGER\_LEVEL\_12 | 12 Byte FIFO depth |
| TRIGGER\_LEVEL\_13 | 13 Byte FIFO depth |
| TRIGGER\_LEVEL\_14 | 14 Byte FIFO depth |
| TRIGGER\_LEVEL\_15 | 15 Byte FIFO depth |
| TRIGGER\_LEVEL\_16 | 16 Byte FIFO depth |