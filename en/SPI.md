# SPI

## Overview

The Serial Peripheral Interface (SPI) is a synchronous serial communication interface.
It is a high speed, full duplex, synchronous communication interface.

## Features

The SPI module has the following features:

- Independent SPI device interface with peripheral related parameters
- Automatic processing of multi-device bus contention
- Support standard, two-wire, four-wire, eight-wire mode
- Supports write-before-read and full-duplex read and write
- Supports sending a series of identical data frames, often used for clearing screens, filling storage sectors, etc.

## API

Corresponding header file `spi.h`

Provide the following interfaces

- spi\_init

- spi\_init\_non\_standard

- spi\_send\_data\_standard

- spi\_send\_data\_standard\_dma

- spi\_receive\_data\_standard

- spi\_receive\_data\_standard\_dma

- spi\_send\_data\_multiple

- spi\_send\_data\_multiple\_dma

- spi\_receive\_data\_multiple

- spi\_receive\_data\_multiple\_dma

- spi\_fill\_data\_dma

- spi\_send\_data\_normal\_dma

- spi\_set\_clk\_rate

### spi\_init

#### Description

Set the SPI mode of operation, multi-line mode, and transfer bit width.

#### Function prototype

```c
void spi_init(spi_device_num_t spi_num, spi_work_mode_t work_mode, spi_frame_format_t frame_format, size_t data_bit_length, uint32_t endian)
```

#### Parameter

|  Parameter name   |              Description               | Input or output |
| :---------------- | :------------------------------------- | :-------------- |
| spi\_num          | SPI number                             | Input           |
| work\_mode        | Four working modes                     | Input           |
| frame\_format     | Frame format                           | Input           |
| data\_bit\_length | Data bit length                        | Input           |
| endian            | Endian. 0: Little endian 1: Big endian | Input           |

#### Return value

None.

### spi\_config\_non\_standard

#### Description

Used to set the instruction length, address length, wait clock count, and instructio/ address transfer mode in multi-wire mode.

#### Function prototype

```c
void spi_init_non_standard(spi_device_num_t spi_num, uint32_t instruction_length, uint32_t address_length, uint32_t wait_cycles, spi_instruction_address_trans_mode_t instruction_address_trans_mode)
```

#### Parameter

|          Parameter name           |            Description            | Input or output |
| :-------------------------------- | :-------------------------------- | :-------------: |
| spi\_num                          | SPI number                        |      Input      |
| instruction\_length               | Instruction length                |      Input      |
| address\_length                   | Address length                    |      Input      |
| wait\_cycles                      | Number of waiting cycles          |      Input      |
| instruction\_address\_trans\_mode | Instruction/address transfer mode |      Input      |

#### Return value

None.

### spi\_send\_data\_standard

#### Description

The SPI transfers data in standard mode.

#### Function prototype

```c
void spi_send_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### Parameter

| Parameter name |                           Description                            | Input or output |
| :------------- | :--------------------------------------------------------------- | :-------------: |
| spi\_num       | SPI number                                                       |      Input      |
| chip\_select   | Chip select                                                      |      Input      |
| cmd\_buff      | Peripheral instruction/address data, set to NULL if not used     |      Input      |
| cmd\_len       | Peripheral instruction/address data length, set to 0 if not used |      Input      |
| tx\_buff       | Sent data buffer                                                 |      Input      |
| tx\_len        | Length of data sent                                              |      Input      |

#### Return value

None.

### spi\_send\_data\_standard\_dma

#### Description

Data is transferred via DMA using SPI standard mode.

#### Function prototype

```c
void spi_send_data_standard_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### Parameter

| Parameter name |                           Description                            | Input or output |
| :------------- | :--------------------------------------------------------------- | :-------------: |
| channel\_num   | DMA channel number                                               |      Input      |
| spi\_num       | SPI number                                                       |      Input      |
| chip\_select   | Chip select                                                      |      Input      |
| cmd\_buff      | Peripheral instruction/address data, set to NULL if not used     |      Input      |
| cmd\_len       | Peripheral instruction/address data length, set to 0 if not used |      Input      |
| tx\_buff       | Sent data buffer                                                 |      Input      |
| tx\_len        | Length of data sent                                              |      Input      |

#### Return value

None.

### spi\_receive\_data\_standard

#### Description

Receive data using standard mode.

#### Function prototype

```c
void spi_receive_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### Parameter

| Parameter name |                           Description                            | Input or output |
| :------------- | :--------------------------------------------------------------- | :-------------: |
| spi\_num       | SPI number                                                       |      Input      |
| chip\_select   | Chip select                                                      |      Input      |
| cmd\_buff      | Peripheral instruction/address data, set to NULL if not used     |      Input      |
| cmd\_len       | Peripheral instruction/address data length, set to 0 if not used |      Input      |
| rx\_buff       | Received data buffer                                             |     Output      |
| rx\_len        | Length of received data                                          |      Input      |

#### Return value

None.

### spi\_receive\_data\_standard\_dma

#### Description

Data is received via DMA using standard mode.

#### Function prototype

```c
void spi_receive_data_standard_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### Parameter

|       Parameter name       |                           Description                            | Input or output |
| :------------------------- | :--------------------------------------------------------------- | :-------------: |
| dma\_send\_channel\_num    | The DMA channel number used to send the instructio/ address      |      Input      |
| dma\_receive\_channel\_num | DMA channel number used to receive data                          |      Input      |
| spi\_num                   | SPI number                                                       |      Input      |
| chip\_select               | Chip select                                                      |      Input      |
| cmd\_buff                  | Peripheral instruction/address data, set to NULL if not used     |      Input      |
| cmd\_len                   | Peripheral instruction/address data length, set to 0 if not used |      Input      |
| rx\_buff                   | Received data buffer                                             |     Output      |
| rx\_len                    | Length of received data                                          |      Input      |

#### Return value

None.

### spi\_send\_data\_multiple

#### Description

Send data using multi-wire mode.

#### Function prototype

```c
void spi_send_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, uint8_t *tx_buff, size_t tx_len)
```

#### Parameter

| Parameter name |                           Description                            | Input or output |
| :------------- | :--------------------------------------------------------------- | :-------------: |
| spi\_num       | SPI number                                                       |      Input      |
| chip\_select   | Chip select                                                      |      Input      |
| cmd\_buff      | Peripheral instruction/address data, set to NULL if not used     |      Input      |
| cmd\_len       | Peripheral instruction/address data length, set to 0 if not used |      Input      |
| tx\_buff       | Sent data buffer                                                 |      Input      |
| tx\_len        | Length of data sent                                              |      Input      |

#### Return value

None.

### spi\_send\_data\_multiple\_dma

#### Description

Data is sent by DMA using multi-line mode.

#### Function prototype

```c
void spi_send_data_multiple_dma(dmac_channel_number_t channel_num,spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### Parameter

| Parameter name |                           Description                            | Input or output |
| :------------- | :--------------------------------------------------------------- | :-------------: |
| channel\_num   | DMA channel number                                               |      Input      |
| spi\_num       | SPI number                                                       |      Input      |
| chip\_select   | Chip select                                                      |      Input      |
| cmd\_buff      | Peripheral instruction/address data, set to NULL if not used     |      Input      |
| cmd\_len       | Peripheral instruction/address data length, set to 0 if not used |      Input      |
| tx\_buff       | Sent data buffer                                                 |      Input      |
| tx\_len        | Length of data sent                                              |      Input      |

#### Return value

None.

### spi\_receive\_data\_multiple

#### Description

Receive data using multi-wire mode.

#### Function prototype

```c
void spi_receive_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### Parameter

| Parameter name |                           Description                            | Input or output |
| :------------- | :--------------------------------------------------------------- | :-------------: |
| spi\_num       | SPI number                                                       |      Input      |
| chip\_select   | Chip select                                                      |      Input      |
| cmd\_buff      | Peripheral instruction/address data, set to NULL if not used     |      Input      |
| cmd\_len       | Peripheral instruction/address data length, set to 0 if not used |      Input      |
| rx\_buff       | Received data buffer                                             |     Output      |
| rx\_len        | Length of received data                                          |      Input      |

#### Return value

None.

### spi\_receive\_data\_multiple\_dma

#### Description

Receive data via DMA using multi-wire mode.

#### Function prototype

```c
void spi_receive_data_multiple_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, uint32_t const *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len);
```

#### Parameter

|       Parameter name       |                           Description                            | Input or output |
| :------------------------- | :--------------------------------------------------------------- | :-------------: |
| dma\_send\_channel\_num    | The DMA channel number used to send the instructio/ address      |      Input      |
| dma\_receive\_channel\_num | DMA channel number used to receive data                          |      Input      |
| spi\_num                   | SPI number                                                       |      Input      |
| chip\_select               | Chip select                                                      |      Input      |
| cmd\_buff                  | Peripheral instruction/address data, set to NULL if not used     |      Input      |
| cmd\_len                   | Peripheral instruction/address data length, set to 0 if not used |      Input      |
| rx\_buff                   | Received data buffer                                             |     Output      |
| rx\_len                    | Length of received data                                          |      Input      |

#### Return value

None.

### spi\_fill\_data\_dma

#### Description

Always send the same data through DMA, can be used to refresh data.

#### Function prototype

```c
void spi_fill_data_dma(dmac_channel_number_t channel_num,spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *tx_buff, size_t tx_len);
```

#### Parameter

| Parameter name |                                    Description                                    | Input or output |
| :------------- | :-------------------------------------------------------------------------------- | :-------------: |
| channel\_num   | DMA channel number                                                                |      Input      |
| spi\_num       | SPI number                                                                        |      Input      |
| chip\_select   | Chip select                                                                       |      Input      |
| tx\_buff       | Sent data buffer, send only tx_buff this data, it will not increase automatically |      Input      |
| tx\_len        | Length of data sent                                                               |      Input      |

#### Return value

None.

### spi\_send\_data\_normal\_dma

#### Description

Send data by DMA. There is no need to set the instruction/address.

#### Function prototype

```c
void spi_send_data_normal_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const void *tx_buff, size_t tx_len, spi_transfer_width_t spi_transfer_width)
```

#### Parameter

|    Parameter name    |                                    Description                                    | Input or output |
| :------------------- | :-------------------------------------------------------------------------------- | :-------------: |
| channel\_num         | DMA channel number                                                                |      Input      |
| spi\_num             | SPI number                                                                        |      Input      |
| chip\_select         | Chip select                                                                       |      Input      |
| tx\_buff             | Sent data buffer, send only tx_buff this data, it will not increase automatically |      Input      |
| tx\_len              | Length of data sent                                                               |      Input      |
| spi\_transfer\_width | The bit width of the transmitted data                                             |      Input      |

#### Return value

None.

### Example

```c
/* SPI0 operates in MODE0 (standard SPI mode) for single transmission of 8-bit data */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_0, SPI_FF_STANDARD, 8, 0);
uint8_t cmd[4];
cmd[0] = 0x06;
cmd[1] = 0x01;
cmd[2] = 0x02;
cmd[3] = 0x04;
uint8_t data_buf[4] = {0,1,2,3};
/* SPI0 sends the instruction 0x06 using chip select 0, and sends 0, 1, 2, 3 four bytes of data to address 0x010204. */
spi_send_data_standard(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 4, data_buf, 4);
/* SPI0 sends a 0x06 instruction using chip select 0 and then receives 4 bytes of data from Address 0x010204. */
spi_receive_data_standard(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 4, data_buf, 4);

/* SPI0 operates in MODE0 (4-wire SPI mode) single-transmission of 8-bit data */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_0, SPI_FF_QUAD, 8, 0);
/* 8-bit instruction length 32-bit address length wait for 4 clk after sending the instruction/address, the instruction is sent by standard SPI mode, and the address is sent by four-wire mode. */
spi_init_non_standard(SPI_DEVICE_0, 8, 32, 4, SPI_AITM_ADDR_STANDARD);
uint32 cmd[2];
cmd[0] = 0x06;
cmd[1] = 0x010204;
uint8_t data_buf[4] = {0,1,2,3};
/* SPI0 sends the instruction 0x06 using chip select 0, and sends 0, 1, 2, 3 four bytes of data to address 0x010204. */
spi_send_data_multiple(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 2, data_buf, 4);
/* SPI0 sends a 0x06 instruction using chip select 0 and then receives 4 bytes of data from Address 0x010204. */
spi_receive_data_multiple(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 2, data_buf, 4);

/* SPI0 works in MODE2 (8-wire SPI mode) single-transmission 32-bit data */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_2, SPI_FF_OCTAL, 32, 0);
/* No instruction 32-bit address length Wait for 0 clk after sending the instruction/address, the instruction/address is sent through 8-wires */
spi_init_non_standard(SPI_DEVICE_0, 0, 32, 0, SPI_AITM_AS_FRAME_FORMAT);
uint32_t data_buf[256] = {0};
/* Send 256 int data using DMA channel 0 and chip select 0 */
spi_send_data_normal_dma(DMAC_CHANNEL0, SPI_DEVICE_0, SPI_CHIP_SELECT_0, data_buf, 256, SPI_TRANS_INT);
uint32_t data = 0x55AA55AA;
/* Use DMA channel 0 and chip select 0 to send 256 consecutively 0x55AA55AA */
spi_fill_data_dma(DMAC_CHANNEL0, SPI_DEVICE_0, SPI_CHIP_SELECT_0,&data, 256);
```

### spi\_set\_clk\_rate

#### Description

Set the clock frequency of the SPI

#### Function prototype

```c
uint32_t spi_set_clk_rate(spi_device_num_t spi_num, uint32_t spi_clk)
```

#### Parameter

| Parameter name |            Description            | Input or output |
| :------------- | :-------------------------------- | :-------------: |
| spi\_num       | SPI number                        |      Input      |
| spi\_clk       | Target SPI device clock frequency |      Input      |

#### Return value

The actual clock frequency of the SPI device after setup

## Data type

The relevant data types and data structures are defined as follows:

- spi\_device\_num\_t: SPI number.
- spi\_mode\_t: SPI mode.
- spi\_frame\_format\_t: SPI frame format.
- spi\_instruction\_address\_trans\_mode\_t: The transfer mode of the SPI instruction and address.

### spi\_device\_num\_t

#### Description

SPI number.

#### Type definition

```c
typedef enum _spi_device_num
{
    SPI_DEVICE_0,
    SPI_DEVICE_1,
    SPI_DEVICE_2,
    SPI_DEVICE_3,
    SPI_DEVICE_MAX,
} spi_device_num_t;
```

#### Enumeration element

| Element name |        Description         |
| :----------- | :------------------------- |
| SPI_DEVICE_0 | SPI 0 as the master device |
| SPI_DEVICE_1 | SPI 1 as the master device |
| SPI_DEVICE_2 | SPI 2 as the slave device  |
| SPI_DEVICE_3 | SPI 3 as the master device |

### spi\_mode\_t

#### Description

SPI mode.

#### Type definition

```c
typedef enum _spi_mode
{
    SPI_WORK_MODE_0,
    SPI_WORK_MODE_1,
    SPI_WORK_MODE_2,
    SPI_WORK_MODE_3,
} spi_mode_t;
```

#### Enumeration element

|    Element name    | Description |
| ------------------ | ----------- |
| SPI\_WORK\_MODE\_0 | SPI mode 0  |
| SPI\_WORK\_MODE\_1 | SPI mode 1  |
| SPI\_WORK\_MODE\_2 | SPI mode 2  |
| SPI\_WORK\_MODE\_3 | SPI mode 3  |

### spi\_frame\_format\_t

#### Description

SPI frame format.

#### Type definition

```c
typedef enum _spi_frame_format
{
    SPI_FF_STANDARD,
    SPI_FF_DUAL,
    SPI_FF_QUAD,
    SPI_FF_OCTAL
} spi_frame_format_t;
```

#### Enumeration element

|   Element name    |                 Description                 |
| ----------------- | ------------------------------------------- |
| SPI\_FF\_STANDARD | Standard                                    |
| SPI\_FF\_DUAL     | Dual wire (2 wires)                         |
| SPI\_FF\_QUAD     | Duad wire (4 wires)                         |
| SPI\_FF\_OCTAL    | Octal wire (8 wires, SPI3 is not supported) |

### spi\_instruction\_address\_trans\_mode\_t

#### Description

The transfer mode of the SPI instruction and address.

#### Type definition

```c
typedef enum _spi_instruction_address_trans_mode
{
    SPI_AITM_STANDARD,
    SPI_AITM_ADDR_STANDARD,
    SPI_AITM_AS_FRAME_FORMAT
} spi_instruction_address_trans_mode_t;
```

#### Enumeration element

|         Element name         |                                       Description                                        |
| ---------------------------- | ---------------------------------------------------------------------------------------- |
| SPI\_AITM\_STANDARD          | All use the standard frame format                                                        |
| SPI\_AITM\_ADDR\_STANDARD    | The instruction uses the configured value and the address uses the standard frame format |
| SPI\_AITM\_AS\_FRAME\_FORMAT | All use the configured values                                                            |