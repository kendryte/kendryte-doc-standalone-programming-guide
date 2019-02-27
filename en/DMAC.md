# DMA

## Overview

Direct Memory Access (DMA) controller is used to provide high-speed data transfer between peripherals and memory and between memory and memory.
This improves CPU efficiency by quickly moving data through DMA without any CPU operation.

## Features

The DMA controller has the following features:

- Automatically select an idle DMA channel for transmission
- Automatic selection of software or hardware handshake protocol based on source and destination addresses
- Supports 1, 2, 4, and 8 byte element sizes, source and target sizes do not have to be consistent
- Asynchronous or synchronous transfer function
- Loop transmission function, often used to refresh scenes such as screen or audio recording and playback

## API

Corresponding header file `dmac.h`

Provide the following interfaces

- dmac\_init

- dmac\_set\_single\_mode

- dmac\_is\_done

- dmac\_wait\_done

- dmac\_set\_irq

- dmac\_set\_src\_dest\_length

- dmac\_is\_idle

- dmac\_wait\_idle

### dmac\_init

#### Description

Initialize the DMA.

#### Function prototype

```c
void dmac_init(void)
```

#### Parameter

None.

#### Return value

None.

### dmac\_set\_single\_mode

#### Description

Set a single channel DMA parameter.

#### Function prototype

```c
void dmac_set_single_mode(dmac_channel_number_t channel_num, const void *src, void *dest, dmac_address_increment_t src_inc, dmac_address_increment_t dest_inc, dmac_burst_trans_length_t dmac_burst_size, dmac_transfer_width_t dmac_trans_width, size_t block_size)
```

#### Parameter

|   Parameter name   |                  Description                  | Input or output |
| ------------------ | --------------------------------------------- | --------------- |
| channel_num        | DMA channel number                            | Input           |
| src                | Source address                                | Input           |
| dest               | Destination address                           | Output          |
| src\_inc           | Whether the source address is increasing      | Input           |
| dest\_inc          | Whether the destination address is increasing | Input           |
| dmac\_burst\_size  | Burst transfer size                           | Input           |
| dmac\_trans\_width | Single transfer data bit width                | Input           |
| block\_size        | The size of the transmitted data              | Input           |

#### Return value

None.

### dmac\_is\_done

#### Description

It is used to determine whether the transmission is completed after the DMAC
starts the transmission. It can only be used after the DMAC starts transmitting.
If you use it before the DMAC starts transmitting, you will get an incorrect result.

#### Function prototype

```c
int dmac_is_done(dmac_channel_number_t channel_num)
```

#### Parameter

| Parameter name |    Description     | Input or output |
| -------------- | ------------------ | --------------- |
| channel\_num   | DMA channel number | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Undone      |
| 1            | Done        |

### dmac\_wait\_done

#### Description

Wait for the DMA to finish working.

#### Function prototype

```c
void dmac_wait_done(dmac_channel_number_t channel_num)
```

#### Parameter

| Parameter name |    Description     | Input or output |
| -------------- | ------------------ | --------------- |
| channel\_num   | DMA channel number | Input           |

#### Return value

None.

### dmac\_set\_irq

#### Description

Set the callback function of the DMAC interrupt.

#### Function prototype

```c
void dmac_set_irq(dmac_channel_number_t channel_num , plic_irq_callback_t dmac_callback, void *ctx, uint32_t priority)
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| channel\_num   | DMA channel number           | Input           |
| dmac\_callback | Interrupt callback function  | Input           |
| ctx            | Callback function parameters | Input           |
| priority       | Interrupt priority           | Input           |

#### Return value

None.

### dmac\_set\_src\_dest\_length

#### Description

Set the source address, destination address, and length of the DMAC, and then
start DMA transfer. If src is NULL, the source address is not set. If dest is
NULL, the destination address is not set. If len<=0, the length is not set.

This function is typically used in DMAC interrupts to allow the DMA to continue
transferring data without having to set all the parameters of the DMAC again to
save time.

#### Function prototype

```c
void dmac_set_src_dest_length(dmac_channel_number_t channel_num, const void *src, void *dest, size_t len)
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| channel\_num   | DMA channel number           | Input           |
| src            | Interrupt callback function  | Input           |
| dest           | Callback function parameters | Input           |
| len            | Transmission length          | Input           |

#### Return value

None.

### dmac\_is\_idle

#### Description

Determine whether the current channel of the DMAC is idle.
This function can be used to determine the DMAC status before and after transmission.

#### Function prototype

```c
int dmac_is_idle(dmac_channel_number_t channel_num)
```

#### Parameter

| Parameter name |    Description     | Input or output |
| -------------- | ------------------ | --------------- |
| channel\_num   | DMA channel number | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Busy        |
| 1            | Idle        |

### dmac\_wait\_idle

#### Description

Wait for the DMAC to enter the idle state.

#### Parameter

| Parameter name |    Description     | Input or output |
| -------------- | ------------------ | --------------- |
| channel_num    | DMA channel number | Input           |

#### Return value

None.

### Example

```c
/* I2C sends 128 int data via DMA */
uint32_t buf[128];
dmac_wait_idle(SYSCTL_DMA_CHANNEL_0);
sysctl_dma_select(SYSCTL_DMA_CHANNEL_0, SYSCTL_DMA_SELECT_I2C0_TX_REQ);
dmac_set_single_mode(SYSCTL_DMA_CHANNEL_0, buf, (void*)(&i2c_adapter->data_cmd), DMAC_ADDR_INCREMENT, DMAC_ADDR_NOCHANGE, DMAC_MSIZE_4, DMAC_TRANS_WIDTH_32, 128);
dmac_wait_done(SYSCTL_DMA_CHANNEL_0);
```

## Data type

The relevant data types and data structures are defined as follows:

- dmac\_channel\_number\_t：DMA channel number.

- dmac\_address\_increment\_t：Address self-increasing behavior.

- dmac\_burst\_trans\_length\_t：Burst transfer size.

- dmac\_transfer\_width\_t：The bit width of a single transfer of data.

### dmac\_channel\_number\_t

#### Description

DMA channel number.

#### Type definition

```c
typedef enum _dmac_channel_number
{
    DMAC_CHANNEL0 = 0,
    DMAC_CHANNEL1 = 1,
    DMAC_CHANNEL2 = 2,
    DMAC_CHANNEL3 = 3,
    DMAC_CHANNEL4 = 4,
    DMAC_CHANNEL5 = 5,
    DMAC_CHANNEL_MAX
} dmac_channel_number_t;
```

#### Enumeration element

|  Element name  |  Description  |
| -------------- | ------------- |
| DMAC\_CHANNEL0 | DMA channel 0 |
| DMAC\_CHANNEL1 | DMA channel 1 |
| DMAC\_CHANNEL2 | DMA channel 2 |
| DMAC\_CHANNEL3 | DMA channel 3 |
| DMAC\_CHANNEL4 | DMA channel 4 |
| DMAC\_CHANNEL5 | DMA channel 5 |

### dmac\_address\_increment\_t

#### Description

Address self-increasing behavior.

#### Type definition

```c
typedef enum _dmac_address_increment
{
    DMAC_ADDR_INCREMENT = 0x0,
    DMAC_ADDR_NOCHANGE  = 0x1
} dmac_address_increment_t;
```

#### Enumeration element

|     Element name      |        Description         |
| --------------------- | -------------------------- |
| DMAC\_ADDR\_INCREMENT | Automatic address increase |
| DMAC\_ADDR\_NOCHANGE  | Fixed address              |

### dmac\_burst\_trans\_length\_t

#### Description

Burst transfer size.

#### Type definition

```c
typedef enum _dmac_burst_trans_length
{
    DMAC_MSIZE_1   = 0x0,
    DMAC_MSIZE_4   = 0x1,
    DMAC_MSIZE_8   = 0x2,
    DMAC_MSIZE_16  = 0x3,
    DMAC_MSIZE_32  = 0x4,
    DMAC_MSIZE_64  = 0x5,
    DMAC_MSIZE_128 = 0x6,
    DMAC_MSIZE_256 = 0x7
} dmac_burst_trans_length_t;
```

#### Enumeration element

|   Element name   |                 Description                  |
| ---------------- | -------------------------------------------- |
| DMAC\_MSIZE\_1   | Single transmission number multiplied by 1   |
| DMAC\_MSIZE\_4   | Single transmission number multiplied by 4   |
| DMAC\_MSIZE\_8   | Single transmission number multiplied by 8   |
| DMAC\_MSIZE\_16  | Single transmission number multiplied by 16  |
| DMAC\_MSIZE\_32  | Single transmission number multiplied by 32  |
| DMAC\_MSIZE\_64  | Single transmission number multiplied by 64  |
| DMAC\_MSIZE\_128 | Single transmission number multiplied by 128 |
| DMAC\_MSIZE\_256 | Single transmission number multiplied by 256 |

### dmac\_transfer\_width\_t

#### Description

The bit width of a single transfer of data.

#### Type definition

```c
typedef enum _dmac_transfer_width
{
    DMAC_TRANS_WIDTH_8   = 0x0,
    DMAC_TRANS_WIDTH_16  = 0x1,
    DMAC_TRANS_WIDTH_32  = 0x2,
    DMAC_TRANS_WIDTH_64  = 0x3,
    DMAC_TRANS_WIDTH_128 = 0x4,
    DMAC_TRANS_WIDTH_256 = 0x5
} dmac_transfer_width_t;
```

#### Enumeration element

|      Element name       |           Description           |
| ----------------------- | ------------------------------- |
| DMAC\_TRANS\_WIDTH\_8   | Single transmission of 8 bits   |
| DMAC\_TRANS\_WIDTH\_16  | Single transmission of 16 bits  |
| DMAC\_TRANS\_WIDTH\_32  | Single transmission of 32 bits  |
| DMAC\_TRANS\_WIDTH\_64  | Single transmission of 64 bits  |
| DMAC\_TRANS\_WIDTH\_128 | Single transmission of 128 bits |
| DMAC\_TRANS\_WIDTH\_256 | Single transmission of 256 bits |