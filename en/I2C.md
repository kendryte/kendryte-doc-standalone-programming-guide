# I²C

## Overview

The I²C (Inter-Integrated Circuit) bus is used to communicate with multiple
external I²C devices. Multiple external I²C devices can share an I²C bus.

## Features

The I²C unit has the following features:

- Independent I²C controller
- Automatic processing of multi-device bus contention
- Support slave mode

## API

Corresponding header file `i2c.h`

Provide the following interfaces

- i2c\_init

- i2c\_init\_as\_slave

- i2c\_send\_data

- i2c\_send\_data\_dma

- i2c\_recv\_data

- i2c\_recv\_data\_dma

### i2c\_init

#### Description

Configure the I²C device slave address, register bit width, and I²C rate.

#### Function prototype

```c
void i2c_init(i2c_device_number_t i2c_num, uint32_t slave_address, uint32_t address_width, uint32_t i2c_clk)
```

#### Parameter

| Parameter name |             Description             | Input or output |
| :------------- | :---------------------------------- | :-------------: |
| i2c\_num       | I²C number                          |      Input      |
| slave\_address | I²C device slave address            |      Input      |
| address\_width | I²C device register width (7 or 10) |      Input      |
| i2c\_clk       | I²C clock rate (Hz)                 |      Input      |

#### Return value

None.

### i2c\_init\_as\_slave

#### Description

Configure the I²C controller to be in slave mode.

#### Function prototype

```c
void i2c_init_as_slave(i2c_device_number_t i2c_num, uint32_t slave_address, uint32_t address_width, const i2c_slave_handler_t *handler)
```

#### Parameter

| Parameter name |             Description             | Input or output |
| :------------- | :---------------------------------- | :-------------: |
| i2c\_num       | I²C number                          |      Input      |
| slave\_address | I²C slave address                   |      Input      |
| address\_width | I²C device register width (7 or 10) |      Input      |
| handler        | I²C slave interrupt handler         |      Input      |

#### Return value

None.

### i2c\_send\_data

#### Description

Write data.

#### Function prototype

```c
int i2c_send_data(i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len)
```

#### Parameter

| Parameter name |           Description            | Input or output |
| :------------: | :------------------------------- | :-------------: |
|    i2c\_num    | I²C number                       |      Input      |
|   send\_buf    | Data to be transmitted           |      Input      |
| send\_buf\_len | Length of data to be transmitted |      Input      |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### i2c\_send\_data\_dma

#### Description

Write data through the DMA.

#### Function prototype

```c
void i2c_send_data_dma(dmac_channel_number_t dma_channel_num, i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len)
```

#### Parameter

|  Parameter name   |           Description            | Input or output |
| :---------------- | :------------------------------- | :-------------- |
| dma\_channel\_num | DMA channel number used          | Input           |
| i2c\_num          | I²C number                       | Input           |
| send\_buf         | Data to be transmitted           | Input           |
| send\_buf\_len    | Length of data to be transmitted | Input           |

#### Return value

None.

### i2c\_recv\_data

#### Description

Read data through the CPU.

#### Function prototype

```c
int i2c_recv_data(i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len, uint8_t *receive_buf, size_t receive_buf_len)
```

#### Parameter

|  Parameter name   |                      Description                      | Input or output |
| :---------------- | :---------------------------------------------------- | :-------------- |
| i2c\_num          | I²C number                                            | Input           |
| send\_buf         | Data to be transmitted[^device_register]              | Input           |
| send\_buf\_len    | Length of data to be transmitted. If not use, write 0 | Input           |
| receive\_buf      | Receive data buffer                                   | Output          |
| receive\_buf\_len | Length of received data                               | Input           |

[^device_register]: The general case corresponds to the register of the I²C peripheral, if it is not set to NULL.

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### i2c\_recv\_data\_dma

#### Description

Read data through the DMA.

#### Function prototype

```c
void i2c_recv_data_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num,
    i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len, uint8_t *receive_buf, size_t receive_buf_len)
```

#### Parameter

|       Parameter name       |                      Description                      | Input or output |
| :------------------------- | :---------------------------------------------------- | :-------------- |
| dma\_send\_channel\_num    | Dma channel used to send data                         | Input           |
| dma\_receive\_channel\_num | Dma channel for receiving data                        | Input           |
| i2c\_num                   | I²C number                                            | Input           |
| send\_buf                  | Data to be transmitted[^device_register]              | Input           |
| send\_buf\_len             | Length of data to be transmitted. If not use, write 0 | Input           |
| receive\_buf               | Receive data buffer                                   | Output          |
| receive\_buf\_len          | Length of received data                               | Input           |

#### Return value

None.

### Example

```c
/* The i2c peripheral address is 0x32, 7-bit address, rate 200K */
i2c_init(I2C_DEVICE_0, 0x32, 7, 200000);
uint8_t reg = 0;
uint8_t data_buf[2] = {0x00,0x01}
data_buf[0] = reg;
/* Write 0x01 to the 0 register */
i2c_send_data(I2C_DEVICE_0, data_buf, 2);
i2c_send_data_dma(DMAC_CHANNEL0, I2C_DEVICE_0, data_buf, 4);
/* Read 1 byte data from 0 registe */
i2c_receive_data(I2C_DEVICE_0, &reg, 1, data_buf, 1);
i2c_receive_data_dma(DMAC_CHANNEL0, DMAC_CHANNEL1, I2C_DEVICE_0,&reg, 1, data_buf, 1);
```

## Data type

The relevant data types and data structures are defined as follows:

- i2c\_device\_number\_t: I²C device number.

- i2c\_slave\_handler\_t: I²C slave mode interrupt handler function handle.

### i2c\_device\_number_t

#### Description

I²C device number.

#### Type definition

```c
typedef enum _i2c_device_number
{
    I2C_DEVICE_0,
    I2C_DEVICE_1,
    I2C_DEVICE_2,
    I2C_DEVICE_MAX,
} i2c_device_number_t;
```

### i2c\_slave\_handler\_t

#### Description

I²C slave mode interrupt handler function handle.
The corresponding function operations are performed according to different interrupt states.

#### Type definition

```c
typedef struct _i2c_slave_handler
{
    void(*on_receive)(uint32_t data);
    uint32_t(*on_transmit)();
    void(*on_event)(i2c_event_t event);
} i2c_slave_handler_t;
```

#### Enumeration element

|  Element name  | Description |
| :------------- | :---------- |
| I2C\_DEVICE\_0 | I²C 0       |
| I2C\_DEVICE\_1 | I²C 1       |
| I2C\_DEVICE\_2 | I²C 2       |
