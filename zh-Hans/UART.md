# 通用异步收发传输器 (UART)

## 概述

嵌入式应用通常要求一个简单的并且占用系统资源少的方法来传输数据。通用异步收发传输器 (UART) 即可以满足这些要求，它能够灵活地与外部设备进行全双工数据交换。

## 功能描述

UART 模块具有以下功能：

- 配置 UART 参数

- 自动收取数据到缓冲区

## API 参考

对应的头文件 `uart.h`

为用户提供以下接口

- uart\_init

- uart\_config  (0.6.0后不再支持，请使用uart\_configure)

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

#### 描述

初始化uart。

#### 函数原型

```c
void uart_init(uart_device_number_t channel)
```

#### 参数

| 参数名称     | 描述       | 输入输出   |
| :-----------| :----------| :-------- |
| channel     | UART号     | 输入       |

#### 返回值

无。

### uart\_configure

#### 描述

设置UART相关参数。该函数已废弃，替代函数为uart_configure。

### uart\_configure

#### 描述

设置UART相关参数。

#### 函数原型

```c
void uart_configure(uart_device_number_t channel, uint32_t baud_rate, uart_bitwidth_t data_width, uart_stopbit_t stopbit, uart_parity_t parity)
```

#### 参数

| 参数名称    |   描述       |  输入输出  |
| ---------- | ------------ | --------- |
| channel    | UART 编号     | 输入      |
| baud\_rate | 波特率        | 输入      |
| data_width | 数据位 (5-8)  | 输入      |
| stopbit   | 停止位        | 输入      |
| parity     | 校验位        | 输入      |

#### 返回值

无。

### uart\_send\_data

#### 描述

通过UART发送数据。

#### 函数原型

```c
int uart_send_data(uart_device_number_t channel, const char *buffer, size_t buf_len)
```

#### 参数

| 参数名称    |   描述           |  输入输出  |
| ---------- | ---------------  | --------- |
| channel    | UART 编号        | 输入       |
| buffer     | 待发送数据        | 输入      |
| buf\_len    | 待发送数据的长度  | 输入       |

#### 返回值

已发送数据的长度。

### uart\_send\_data\_dma

#### 描述

UART通过DMA发送数据。数据全部发送完毕后返回。

#### 函数原型

```c
void uart_send_data_dma(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, const uint8_t *buffer, size_t buf_len)
```

#### 参数

| 参数名称          |   描述           |  输入输出  |
| ---------------- | ---------------  | --------- |
| uart\_channel    | UART 编号        | 输入       |
| dmac\_channel    | DMA通道          | 输入       |
| buffer           | 待发送数据        | 输入       |
| buf\_len         | 待发送数据的长度  | 输入       |

#### 返回值

无。

### uart\_send\_data\_dma\_irq

#### 描述

UART通过DMA发送数据，并设置DMA发送完成中断函数，仅单次中断。

#### 函数原型

```c
void uart_send_data_dma_irq(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel,
                            const uint8_t *buffer, size_t buf_len, plic_irq_callback_t uart_callback,
                            void *ctx, uint32_t priority)
```

#### 参数

| 参数名称          |   描述           |  输入输出  |
| ---------------- | ---------------  | --------- |
| uart\_channel    | UART 编号        | 输入       |
| dmac\_channel    | DMA通道          | 输入       |
| buffer           | 待发送数据        | 输入       |
| buf\_len         | 待发送数据的长度  | 输入       |
| uart\_callback   | DMA中断回调      | 输入       |
| ctx              | 中断函数参数      | 输入       |
| priority         | 中断优先级        | 输入       |

#### 返回值

无。

### uart\_receive\_data

#### 描述

通过UART读取数据。

#### 函数原型

```c
int uart_receive_data(uart_device_number_t channel, char *buffer, size_t buf_len);
```

#### 参数

| 参数名称    |   描述           |  输入输出  |
| ---------- | ---------------  | --------- |
| channel    | UART 编号        | 输入       |
| buffer     | 接收数据         | 输出       |
| buf\_len    | 接收数据的长度    | 输入       |

#### 返回值

已接收到的数据长度。

### uart\_receive\_data\_dma

#### 描述

UART通过DMA接收数据。

#### 函数原型

```c
void uart_receive_data_dma(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, uint8_t *buffer, size_t buf_len)
```

#### 参数

| 参数名称          |   描述           |  输入输出  |
| ---------------- | ---------------  | --------- |
| uart\_channel    | UART 编号        | 输入       |
| dmac\_channel    | DMA通道          | 输入       |
| buffer           | 接收数据         | 输出       |
| buf\_len         | 接收数据的长度    | 输入       |

#### 返回值

无。

### uart\_receive\_data\_dma\_irq

#### 描述

UART通过DMA接收数据，并注册DMA接收完成中断函数，仅单次中断。

#### 函数原型

```c
void uart_receive_data_dma_irq(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel,
                                     uint8_t *buffer, size_t buf_len, plic_irq_callback_t uart_callback,
                                     void *ctx, uint32_t priority)
```

#### 参数

| 参数名称          |   描述           |  输入输出  |
| ---------------- | ---------------  | --------- |
| uart\_channel    | UART 编号        | 输入       |
| dmac\_channel    | DMA通道          | 输入       |
| buffer           | 接收数据         | 输出       |
| buf\_len         | 接收数据的长度    | 输入       |
| uart\_callback   | DMA中断回调      | 输入       |
| ctx              | 中断函数参数      | 输入       |
| priority         | 中断优先级        | 输入       |

#### 返回值

无。

### uart\_irq\_register

#### 描述

注册UART中断函数。

#### 函数原型

```c
void uart_irq_register(uart_device_number_t channel, uart_interrupt_mode_t interrupt_mode, plic_irq_callback_t uart_callback, void *ctx, uint32_t priority)
```

#### 参数

| 参数名称          |   描述           |  输入输出  |
| ---------------- | ---------------  | --------- |
| channel          | UART 编号        | 输入       |
| interrupt\_mode  | 中断类型          | 输入       |
| uart\_callback   | 中断回调          | 输入       |
| ctx              | 中断函数参数      | 输入       |
| priority         | 中断优先级        | 输入       |

#### 返回值

无。

### uart\_irq\_deregister

#### 描述

注销UART中断函数。

#### 函数原型

```c
void uart_irq_deregister(uart_device_number_t channel, uart_interrupt_mode_t interrupt_mode)
```

#### 参数

| 参数名称          |   描述           |  输入输出  |
| ---------------- | ---------------  | --------- |
| channel          | UART 编号        | 输入       |
| interrupt\_mode  | 中断类型          | 输入       |

#### 返回值

无。

### 举例

```c
/* UART1 波特率115200, 8位数据， 1位停止位，无校验位 */
uart_init(UART_DEVICE_1);
uart_config(UART_DEVICE_1, 115200, UART_BITWIDTH_8BIT, UART_STOP_1, UART_PARITY_NONE);
char *v_hel = {"hello world!\n"};
/* 发送 hello world! */
uart_send_data(UART_DEVICE_1, hel, strlen(v_hel));
/* 接收数据 */
while(uart_receive_data(UART_DEVICE_1, &recv, 1))
{
    printf("%c ", recv);
}
```

## 数据类型

相关数据类型、数据结构定义如下：

- uart\_device\_number\_t：UART 编号。
- uart\_bitwidth\_t：UART 数据位宽。
- uart\_stopbits\_t：UART 停止位。
- uart\_parity\_t：UART 校验位。
- uart\_interrupt\_mode\_t：UART中断类型，接收或发送。
- uart\_send\_trigger\_t：发送中断或DMA触发FIFO深度。
- uart\_receive\_trigger\_t：接收中断或DMA触发FIFO深度。

### uart\_device\_number\_t

#### 描述

UART编号。

#### 定义

```c
typedef enum _uart_device_number
{
    UART_DEVICE_1,
    UART_DEVICE_2,
    UART_DEVICE_3,
    UART_DEVICE_MAX,
} uart_device_number_t;
```

#### 成员

| 成员名称          | 描述        |
| ---------------- | ----------- |
| UART\_DEVICE\_1  | UART 1      |
| UART\_DEVICE\_2  | UART 2      |
| UART\_DEVICE\_3  | UART 3      |

### uart\_bitwidth\_t

#### 描述

UART数据位宽。

#### 定义

```c
typedef enum _uart_bitwidth
{
    UART_BITWIDTH_5BIT = 0,
    UART_BITWIDTH_6BIT,
    UART_BITWIDTH_7BIT,
    UART_BITWIDTH_8BIT,
} uart_bitwidth_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| UART_BITWIDTH_5BIT | 5比特        |
| UART_BITWIDTH_6BIT | 6比特        |
| UART_BITWIDTH_7BIT | 7比特        |
| UART_BITWIDTH_8BIT | 8比特        |

### uart\_stopbits\_t

#### 描述

UART 停止位。

#### 定义

```c
typedef enum _uart_stopbits
{
    UART_STOP_1,
    UART_STOP_1_5,
    UART_STOP_2
} uart_stopbits_t;  
```

#### 成员

| 成员名称          | 描述        |
| ---------------- | ----------- |
| UART\_STOP\_1    | 1 个停止位   |
| UART\_STOP\_1\_5 | 1.5 个停止位 |
| UART\_STOP\_2    | 2 个停止位   |

### uart\_parity\_t

#### 描述

UART 校验位。

#### 定义

```c
typedef enum _uart_parity
{
    UART_PARITY_NONE,
    UART_PARITY_ODD,
    UART_PARITY_EVEN
} uart_parity_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| UART\_PARITY\_NONE | 无校验位    |
| UART\_PARITY\_ODD  | 奇校验      |
| UART\_PARITY\_EVEN | 偶校验      |

### uart\_interrupt\_mode\_t

#### 描述

UART中断类型，接收或发送。

#### 定义

```c
typedef enum _uart_interrupt_mode
{
    UART_SEND = 1,
    UART_RECEIVE = 2,
} uart_interrupt_mode_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| UART\_SEND          | UART 发送   |
| UART\_RECEIVE       | UART 接收   |

### uart\_send\_trigger\_t

#### 描述

发送中断或DMA触发FIFO深度。当FIFO中的数据小于等于该值时触发中断或DMA传输。FIFO的深度为16字节。

#### 定义

```c
typedef enum _uart_send_trigger
{
    UART_SEND_FIFO_0,
    UART_SEND_FIFO_2,
    UART_SEND_FIFO_4,
    UART_SEND_FIFO_8,
} uart_send_trigger_t;
```

#### 成员

| 成员名称               | 描述          |
| --------------------- | ------------- |
| UART\_SEND\_FIFO\_0   | FIFO为空      |
| UART\_SEND\_FIFO\_2   | FIFO剩余2字节  |
| UART\_SEND\_FIFO\_4   | FIFO剩余4字节  |
| UART\_SEND\_FIFO\_8   | FIFO剩余8字节  |

### uart\_receive\_trigger\_t

#### 描述

接收中断或DMA触发FIFO深度。当FIFO中的数据大于等于该值时触发中断或DMA传输。FIFO的深度为16字节。

#### 定义

```c
typedef enum _uart_receive_trigger
{
    UART_RECEIVE_FIFO_1,
    UART_RECEIVE_FIFO_4,
    UART_RECEIVE_FIFO_8,
    UART_RECEIVE_FIFO_14,
} uart_receive_trigger_t;
```

#### 成员

| 成员名称                  | 描述          |
| ------------------------ | ------------- |
| UART\_RECEIVE\_FIFO\_1   | FIFO剩余1字节  |
| UART\_RECEIVE\_FIFO\_4   | FIFO剩余2字节  |
| UART\_RECEIVE\_FIFO\_8   | FIFO剩余4字节  |
| UART\_RECEIVE\_FIFO\_14  | FIFO剩余8字节  |
