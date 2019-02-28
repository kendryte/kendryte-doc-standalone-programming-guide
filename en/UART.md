# UART

## Overview

Universal Asynchronous Receiver/Transmitter (UART).

Embedded applications typically require a simple method that consumes less system resources to transfer data. The Universal Asynchronous Receiver/Transmitter (UART) meets these requirements with the flexibility to perform full-duplex data exchange with external devices.

## Features

The UART module has the following features:

- Configuring UART parameters
- Automatically charge data to the buffer
- 8-N-1 and 8-N-2 formats: 8 data bits, no parity bit, 1 start bit, 1 or 2 stop bits

## API

Corresponding header file `uart.h`

Provide the following interfaces

- uart\_init

- uart\_config  (deprecated)

- uart\_configure

- uart\_send\_data

- uart\_send\_data\_dma

- uart\_send\_data\_dma\_irq

- uart\_receive\_data

- uart\_receive\_data\_dma

- uart\_receive\_data\_dma\_irq

- uart\_irq\_register

- uart\_irq\_deregister

### uart\_init

#### Description

Initialize uart.

#### Function prototype

```c
void uart_init(uart_device_number_t channel)
```

#### Parameter

| Parameter name | Description | Input or output |
| :------------- | :---------- | :-------------- |
| channel        | UART number | Input           |

#### Return value

None.

### uart\_configure

#### Description

Set the UART related parameters. This function is deprecated and the recommended replacement function is uart_configure.

### uart\_configure

#### Description

Set the UART related parameters.

#### Function prototype

```c
void uart_configure(uart_device_number_t channel, uint32_t baud_rate, uart_bitwidth_t data_width, uart_stopbit_t stopbit, uart_parity_t parity)
```

#### Parameter

| Parameter name |   Description   | Input or output |
| -------------- | --------------- | --------------- |
| channel        | UART number     | Input           |
| baud\_rate     | Baud rate       | Input           |
| data_width     | Data bits (5-8) | Input           |
| stopbit        | Stop bit        | Input           |
| parity         | Parity bit      | Input           |

#### Return value

None.

### uart\_send\_data

#### Description

Send data through the UART.

#### Function prototype

```c
int uart_send_data(uart_device_number_t channel, const char *buffer, size_t buf_len)
```

#### Parameter

| Parameter name |        Description        | Input or output |
| -------------- | ------------------------- | --------------- |
| channel        | UART number               | Input           |
| buffer         | Data to be sent           | Input           |
| buf\_len       | Length of data to be sent | Input           |

#### Return value

The length of the data that has been sent.

### uart\_send\_data\_dma

#### Description

The UART sends data via DMA. After all the data has been sent, return.

#### Function prototype

```c
void uart_send_data_dma(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, const uint8_t *buffer, size_t buf_len)
```

#### Parameter

| Parameter name |        Description        | Input or output |
| -------------- | ------------------------- | --------------- |
| uart\_channel  | UART number               | Input           |
| dmac\_channel  | DMA channel               | Input           |
| buffer         | Data to be sent           | Input           |
| buf\_len       | Length of data to be sent | Input           |

#### Return value

None.

### uart\_send\_data\_dma\_irq

#### Description

The UART sends data through DMA and sets the DMA transmission completion interrupt function, which is only a single interrupt.

#### Function prototype

```c
void uart_send_data_dma_irq(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel,
                            const uint8_t *buffer, size_t buf_len, plic_irq_callback_t uart_callback,
                            void *ctx, uint32_t priority)
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| uart\_channel  | UART number                  | Input           |
| dmac\_channel  | DMA channel                  | Input           |
| buffer         | Data to be sent              | Input           |
| buf\_len       | Length of data to be sent    | Input           |
| uart\_callback | DMA interrupt callback       | Input           |
| ctx            | Interrupt function parameter | Input           |
| priority       | Interrupt priority           | Input           |

#### Return value

None.

### uart\_receive\_data

#### Description

Read data through the UART.

#### Function prototype

```c
int uart_receive_data(uart_device_number_t channel, char *buffer, size_t buf_len);
```

#### Parameter

| Parameter name |       Description       | Input or output |
| -------------- | ----------------------- | --------------- |
| channel        | UART number             | Input           |
| buffer         | Receive data            | Output          |
| buf\_len       | Length of received data | Input           |

#### Return value

The length of the data that has been received.

### uart\_receive\_data\_dma

#### Description

The UART receives data via DMA.

#### Function prototype

```c
void uart_receive_data_dma(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, uint8_t *buffer, size_t buf_len)
```

#### Parameter

| Parameter name |       Description       | Input or output |
| -------------- | ----------------------- | --------------- |
| uart\_channel  | UART number             | Input           |
| dmac\_channel  | DMA channel             | Input           |
| buffer         | Receive data            | Output          |
| buf\_len       | Length of received data | Input           |

#### Return value

None.

### uart\_receive\_data\_dma\_irq

#### Description

The UART receives data via DMA and registers the DMA receive completion interrupt function with a single interrupt.

#### Function prototype

```c
void uart_receive_data_dma_irq(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel,
                                     uint8_t *buffer, size_t buf_len, plic_irq_callback_t uart_callback,
                                     void *ctx, uint32_t priority)
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| uart\_channel  | UART number                  | Input           |
| dmac\_channel  | DMA channel                  | Input           |
| buffer         | Receive data                 | Output          |
| buf\_len       | Length of received data      | Input           |
| uart\_callback | DMA interrupt callback       | Input           |
| ctx            | Interrupt function parameter | Input           |
| priority       | Interrupt priority           | Input           |

#### Return value

None.

### uart\_irq\_register

#### Description

Register the UART interrupt function.

#### Function prototype

```c
void uart_irq_register(uart_device_number_t channel, uart_interrupt_mode_t interrupt_mode, plic_irq_callback_t uart_callback, void *ctx, uint32_t priority)
```

#### Parameter

| Parameter name  |         Description          | Input or output |
| --------------- | ---------------------------- | --------------- |
| channel         | UART number                  | Input           |
| interrupt\_mode | Interrupt type               | Input           |
| uart\_callback  | Interrupt callback           | Input           |
| ctx             | Interrupt function parameter | Input           |
| priority        | Interrupt priority           | Input           |

#### Return value

None.

### uart\_irq\_deregister

#### Description

Deregister the UART interrupt function.

#### Function prototype

```c
void uart_irq_deregister(uart_device_number_t channel, uart_interrupt_mode_t interrupt_mode)
```

#### Parameter

| Parameter name  |  Description   | Input or output |
| --------------- | -------------- | --------------- |
| channel         | UART number    | Input           |
| interrupt\_mode | Interrupt type | Input           |

#### Return value

None.

### Example

```c
/* UART1 with baud rate 115200, 8 data bits, 1 stop bit, no parity bit */
uart_init(UART_DEVICE_1);
uart_config(UART_DEVICE_1, 115200, UART_BITWIDTH_8BIT, UART_STOP_1, UART_PARITY_NONE);
char *v_hel = {"hello world!\n"};
/* Send data "hello world!" */
uart_send_data(UART_DEVICE_1, hel, strlen(v_hel));
/* Receive data */
while(uart_receive_data(UART_DEVICE_1, &recv, 1))
{
    printf("%c ", recv);
}
```

## Data type

The relevant data types and data structures are defined as follows:

- uart\_device\_number\_t: UART number.
- uart\_bitwidth\_t: UART data bit width.
- uart\_stopbits\_t: UART stop bit.
- uart\_parity\_t: UART parity bit.
- uart\_interrupt\_mode\_t: UART interrupt type，send or receive.
- uart\_send\_trigger\_t: Send interrupt or DMA trigger FIFO depth.
- uart\_receive\_trigger\_t: Receive interrupt or DMA trigger FIFO depth.

### uart\_device\_number\_t

#### Description

UART number.

#### Type definition

```c
typedef enum _uart_device_number
{
    UART_DEVICE_1,
    UART_DEVICE_2,
    UART_DEVICE_3,
    UART_DEVICE_MAX,
} uart_device_number_t;
```

#### Enumeration element

|  Element name   | Description |
| --------------- | ----------- |
| UART\_DEVICE\_1 | UART 1      |
| UART\_DEVICE\_2 | UART 2      |
| UART\_DEVICE\_3 | UART 3      |

### uart\_bitwidth\_t

#### Description

UART data bit width.

#### Type definition

```c
typedef enum _uart_bitwidth
{
    UART_BITWIDTH_5BIT = 0,
    UART_BITWIDTH_6BIT,
    UART_BITWIDTH_7BIT,
    UART_BITWIDTH_8BIT,
} uart_bitwidth_t;
```

#### Enumeration element

|    Element name    | Description |
| ------------------ | ----------- |
| UART_BITWIDTH_5BIT | 5 bits      |
| UART_BITWIDTH_6BIT | 6 bits      |
| UART_BITWIDTH_7BIT | 7 bits      |
| UART_BITWIDTH_8BIT | 8 bits      |

### uart\_stopbits\_t

#### Description

UART stop bit.

#### Type definition

```c
typedef enum _uart_stopbits
{
    UART_STOP_1,
    UART_STOP_1_5,
    UART_STOP_2
} uart_stopbits_t;
```

#### Enumeration element

|   Element name   |  Description  |
| ---------------- | ------------- |
| UART\_STOP\_1    | 1 stop bit    |
| UART\_STOP\_1\_5 | 1.5 stop bits |
| UART\_STOP\_2    | 2 stop bits   |

### uart\_parity\_t

#### Description

UART parity bit.

#### Type definition

```c
typedef enum _uart_parity
{
    UART_PARITY_NONE,
    UART_PARITY_ODD,
    UART_PARITY_EVEN
} uart_parity_t;
```

#### Enumeration element

|    Element name    |  Description  |
| ------------------ | ------------- |
| UART\_PARITY\_NONE | No parity bit |
| UART\_PARITY\_ODD  | Odd parity    |
| UART\_PARITY\_EVEN | Even parity   |

### uart\_interrupt\_mode\_t

#### Description

UART interrupt type，send or receive.

#### Type definition

```c
typedef enum _uart_interrupt_mode
{
    UART_SEND = 1,
    UART_RECEIVE = 2,
} uart_interrupt_mode_t;
```

#### Enumeration element

| Element name  | Description  |
| ------------- | ------------ |
| UART\_SEND    | UART send    |
| UART\_RECEIVE | UART receive |

### uart\_send\_trigger\_t

#### Description

Transmit interrupt or DMA trigger FIFO depth.
An interrupt or DMA transfer is triggered when the data in the FIFO is less than or equal to this value. The depth of the FIFO is 16 bytes.

#### Type definition

```c
typedef enum _uart_send_trigger
{
    UART_SEND_FIFO_0,
    UART_SEND_FIFO_2,
    UART_SEND_FIFO_4,
    UART_SEND_FIFO_8,
} uart_send_trigger_t;
```

#### Enumeration element

|    Element name     |      Description       |
| ------------------- | ---------------------- |
| UART\_SEND\_FIFO\_0 | FIFO is empty          |
| UART\_SEND\_FIFO\_2 | FIFO remaining 2 Bytes |
| UART\_SEND\_FIFO\_4 | FIFO remaining 4 Bytes |
| UART\_SEND\_FIFO\_8 | FIFO remaining 8 Bytes |

### uart\_receive\_trigger\_t

#### Description

Receive interrupt or DMA trigger FIFO depth.
An interrupt or DMA transfer is triggered when the data in the FIFO is greater than or equal to this value. The depth of the FIFO is 16 bytes.

#### Type definition

```c
typedef enum _uart_receive_trigger
{
    UART_RECEIVE_FIFO_1,
    UART_RECEIVE_FIFO_4,
    UART_RECEIVE_FIFO_8,
    UART_RECEIVE_FIFO_14,
} uart_receive_trigger_t;
```

#### Enumeration element

|      Element name       |      Description       |
| ----------------------- | ---------------------- |
| UART\_RECEIVE\_FIFO\_1  | FIFO remaining 1 Bytes |
| UART\_RECEIVE\_FIFO\_4  | FIFO remaining 2 Bytes |
| UART\_RECEIVE\_FIFO\_8  | FIFO remaining 4 Bytes |
| UART\_RECEIVE\_FIFO\_14 | FIFO remaining 8 Bytes |
