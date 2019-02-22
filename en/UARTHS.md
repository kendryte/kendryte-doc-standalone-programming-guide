# 高速通用异步收发传输器 (UARTHS)

## Summary

嵌入式应用通常要求一个简单的并且占用系统资源少的方法来传输数据。高速通用异步收发传输器 (UARTHS) 即可以满足这些要求，它能够灵活地与外部设备进行全双工数据交换。
目前系统使用该串口做为调试串口，printf时会调用该串口输出。

## Features

UARTHS 模块具有以下功能：

- 配置 UARTHS Parameter

- 自动收取数据到缓冲区

## API

对应的头文件 `uarths.h`

为用户提供以下接口

- uarths\_init

- uarths\_config

- uarths\_receive\_data

- uarths\_send\_data

- uarths\_set\_irq

- uarths\_get\_interrupt\_mode

- uarths\_set\_interrupt\_cnt

### uarths\_init

#### Description

初始化UARTHS，系统默认波特率为115200 8bit 1位停止位 无检验位。因为uarths时钟源为PLL0，在设置PLL0后需要重新调用该函数设置波特率，否则会打印乱码。

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

设置UARTHS的参数。默认8bit数据，无校验位。

#### Function prototype

```c
void uarths_config(uint32_t baud_rate, uarths_stopbit_t stopbit)
```

### Parameter

| Parameter name    |   Description       |  Input or output  |
| ---------- | ------------ | --------- |
| baud\_rate | 波特率        | 输入      |
| stopbit    | 停止位        | 输入      |

#### Return value

None.

### uarths\_receive\_data

#### Description

通过UARTHS读取数据。

#### Function prototype

```c
size_t uarths_receive_data(uint8_t *buf, size_t buf_len)
```

#### Parameter

| Parameter name    |   Description           |  Input or output  |
| ---------- | ---------------  | --------- |
| buf        | 接收数据         | 输出       |
| buf\_len   | 接收数据的长度    | 输入       |

#### Return value

已接收到的数据长度。

### uarths\_send\_data

#### Description

通过UART发送数据。

#### Function prototype

```c
size_t uarths_send_data(const uint8_t *buf, size_t buf_len)
```

#### Parameter

| Parameter name    |   Description           |  Input or output  |
| ---------- | ---------------  | --------- |
| buf        | 待发送数据        | 输入      |
| buf\_len   | 待发送数据的长度  | 输入       |

#### Return value

已发送数据的长度。

### uarths\_set\_irq

#### Description

设置UARTHS中断回调函数。

#### Function prototype

```c
void uarths_set_irq(uarths_interrupt_mode_t interrupt_mode, plic_irq_callback_t uarths_callback, void *ctx, uint32_t priority)
```

#### Parameter

| Parameter name                       |   Description           |  Input or output  |
| ----------------------------- | ---------------  | --------- |
| interrupt\_mode               | 中断类型          | 输入       |
| uarths\_callback              | 中断回调函数      | 输入      |
| ctx                           | 回调函数的参数    | 输入       |
| priority                      | 中断优先级        | 输入       |

#### Return value

None.

### uarths\_get\_interrupt\_mode

#### Description

获取UARTHS的中断类型。接收、发送或接收发送同时中断。

#### Function prototype

```c
uarths_interrupt_mode_t uarths_get_interrupt_mode(void)
```

#### Parameter

无

#### Return value

当前中断的类型。

### uarths\_set\_interrupt\_cnt

#### Description

设置UARTHS中断时的FIFO深度。
当中断类型为UARTHS\_SEND\_RECEIVE，发送接收FIFO中断深度均为cnt;

#### Function prototype

```c
void uarths_set_interrupt_cnt(uarths_interrupt_mode_t interrupt_mode, uint8_t cnt)
```

#### Parameter

| Parameter name                       |   Description           |  Input or output  |
| ----------------------------- | ---------------  | --------- |
| interrupt\_mode               | 中断类型         | 输入       |
| cnt                           | FIFO深度         | 输入      |

#### Return value

None.

### Example

```c
/* 设置接收中断 中断FIFO深度为0，即接收到数据立即中断并读取接收到的数据。*/
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

相关数据类型、数据结构定义如下：

- uarths\_interrupt\_mode\_t：中断类型。
- uarths\_stopbit\_t：停止位。

### uarths\_interrupt\_mode\_t

### Description

UARTHS中断类型。

#### Type definition

```c
typedef enum _uarths_interrupt_mode
{
    UARTHS_SEND = 1,
    UARTHS_RECEIVE = 2,
    UARTHS_SEND_RECEIVE = 3,
} uarths_interrupt_mode_t;
```

#### 成员

| 成员名称              | Description         |
| -------------------- | ------------ |
| UARTHS_SEND          | 发送中断      |
| UARTHS_RECEIVE       | 接收中断      |
| UARTHS\_SEND\_RECEIVE  | 发送接收中断  |

### uarths\_stopbit\_t

#### Description：

UARTHS停止位。

#### Type definition

```c
typedef enum _uarths_stopbit
{
    UART_STOP_1,
    UART_STOP_2
} uarths_stopbit_t;
```

#### 成员

| 成员名称              | Description         |
| -------------------- | ------------ |
| UART\_STOP\_1        | 1位停止位     |
| UART\_STOP\_2        | 2位停止位     |