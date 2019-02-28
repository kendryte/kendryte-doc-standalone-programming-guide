# UARTHS

## Overview

High Speed Universal Asynchronous Receiver/Transmitter (UART).

Embedded applications typically require a simple method that consumes less system resources to transfer data. The Universal Asynchronous Receiver/Transmitter (UART) meets these requirements with the flexibility to perform full-duplex data exchange with external devices.

At present, the system uses this high speed serial port as the debugging serial port, and the serial port output is called when using printf.

## Features

The UART peripheral has the following features:

- Configuring UART parameters
- Automatically charge data to the buffer
- 8-N-1 and 8-N-2 formats: 8 data bits, no parity bit, 1 start
  bit, 1 or 2 stop bits
- 8-entry transmit and receive FIFO buffers with programmable
  watermark interrupts
- 16× Rx oversampling with 2/3 majority voting per bit
  The UART peripheral does not support hardware flow control or
  other modem control signals, or synchronous serial data
  tranfesrs.

## API

Corresponding header file `uarths.h`

Provide the following interfaces

- uarths\_init

- uarths\_config

- uarths\_receive\_data

- uarths\_send\_data

- uarths\_set\_irq

- uarths\_get\_interrupt\_mode

- uarths\_set\_interrupt\_cnt

### uarths\_init

#### Description

Initialize UARTHS, the system default baud rate is 115200 and 8-N-1 formats (8 data bits, no parity bit, 1 start bit, 1 stop bits). Because the clock source of the uarths is PLL0, you need to call this function to set the baud rate after setting PLL0, otherwise it will print garbled characters.

#### Function prototype

```c
void uarths_init(void)
```

#### Parameter

None.

#### Return value

None.

### uarths\_config

#### Description

Set the parameters of the UARTHS. Default is 8-N-1 formats (8 data bits, no parity bit, 1 start bit, 1 stop bits).

#### Function prototype

```c
void uarths_config(uint32_t baud_rate, uarths_stopbit_t stopbit)
```

### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| baud\_rate     | Baud rate   | Input           |
| stopbit        | Stop bit    | Input           |

#### Return value

None.

### uarths\_receive\_data

#### Description

Read data through UARTHS.

#### Function prototype

```c
size_t uarths_receive_data(uint8_t *buf, size_t buf_len)
```

#### Parameter

| Parameter name |       Description       | Input or output |
| -------------- | ----------------------- | --------------- |
| buf            | Receive data            | Output          |
| buf\_len       | Length of received data | Input           |

#### Return value

The length of the data that has been received.

### uarths\_send\_data

#### Description

Send data through the UART.

#### Function prototype

```c
size_t uarths_send_data(const uint8_t *buf, size_t buf_len)
```

#### Parameter

| Parameter name |        Description        | Input or output |
| -------------- | ------------------------- | --------------- |
| buf            | Data to be sent           | Input           |
| buf\_len       | Length of data to be sent | Input           |

#### Return value

The length of the data that has been sent.

### uarths\_set\_irq

#### Description

Set the UARTHS interrupt callback function.

#### Function prototype

```c
void uarths_set_irq(uarths_interrupt_mode_t interrupt_mode, plic_irq_callback_t uarths_callback, void *ctx, uint32_t priority)
```

#### Parameter

|  Parameter name  |         Description          | Input or output |
| ---------------- | ---------------------------- | --------------- |
| interrupt\_mode  | Interrupt type               | Input           |
| uarths\_callback | Interrupt callback function  | Input           |
| ctx              | Callback function parameters | Input           |
| priority         | Interrupt priority           | Input           |

#### Return value

None.

### uarths\_get\_interrupt\_mode

#### Description

Get the interrupt type of UARTHS. The same interrupt is used by received, sent, or received.

#### Function prototype

```c
uarths_interrupt_mode_t uarths_get_interrupt_mode(void)
```

#### Parameter

None.

#### Return value

The type of current interrupt.

### uarths\_set\_interrupt\_cnt

#### Description

Set the FIFO depth when the UARTHS interrupt is generated.
When the interrupt type is UARTHS\_SEND\_RECEIVE, the transmit and receive FIFO interrupt depths are both cnt.

#### Function prototype

```c
void uarths_set_interrupt_cnt(uarths_interrupt_mode_t interrupt_mode, uint8_t cnt)
```

#### Parameter

| Parameter name  |  Description   | Input or output |
| --------------- | -------------- | --------------- |
| interrupt\_mode | Interrupt type | Input           |
| cnt             | FIFO depth     | Input           |

#### Return value

None.

### Example

```c
/*
 * Set the receive interrupt. The interrupt FIFO depth is 0, that is, the
 * received data is immediately interrupted and the received data is read.
 */
    int uarths_irq(void *ctx)
    {
        if(!uarths_receive_data((uint8_t *)&receive_char, 1))
            printf("Uarths receive ERR!\n");
        return 0;
    }

    plic_init();
    uarths_set_interrupt_cnt(UARTHS_RECEIVE , 0);
    uarths_set_irq(UARTHS_RECEIVE ,uarths_irq, NULL, 4);
    sysctl_enable_irq();
```

## Data type

The relevant data types and data structures are defined as follows:

- uarths\_interrupt\_mode\_t: UARTHS interrupt type.
- uarths\_stopbit\_t: UARTHS stop bit.

### uarths\_interrupt\_mode\_t

### Description

UARTHS interrupt type.

#### Type definition

```c
typedef enum _uarths_interrupt_mode
{
    UARTHS_SEND = 1,
    UARTHS_RECEIVE = 2,
    UARTHS_SEND_RECEIVE = 3,
} uarths_interrupt_mode_t;
```

#### Enumeration element

|     Element name      |        Description        |
| --------------------- | ------------------------- |
| UARTHS_SEND           | Send interrupt            |
| UARTHS_RECEIVE        | Receive interrupt         |
| UARTHS\_SEND\_RECEIVE | Send or Receive interrupt |

### uarths\_stopbit\_t

#### Description

UARTHS stop bit.

#### Type definition

```c
typedef enum _uarths_stopbit
{
    UART_STOP_1,
    UART_STOP_2
} uarths_stopbit_t;
```

#### Enumeration element

| Element name  | Description |
| ------------- | ----------- |
| UART\_STOP\_1 | 1 Stop bit  |
| UART\_STOP\_2 | 2 Stop bits |
