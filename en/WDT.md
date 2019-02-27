# 看门狗定时器 (WDT)

## Overview

WDT 提供系统出错或无响应时的恢复功能。

## Features

WDT 模块具有以下功能：

- 配置超时时间

- 手动重启计时

## API

Corresponding header file `wdt.h`

Provide the following interfaces

- wdt\_start

- wdt\_stop

- wdt\_feed

- wdt\_clear\_interrupt

### wdt\_start

#### Description

启动看门狗。

#### Function prototype

```c
void wdt_start(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | Input       |
| time\_out\_ms   | 超时时间（毫秒）   | Input      |
| on\_irq          | 中断回调函数     | Input       |

#### Return value

无

### wdt\_stop

#### Description

关闭看门狗。

#### Function prototype

```c
void wdt_stop(wdt_device_number_t id)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | Input       |

#### Return value

None.

### wdt\_feed

#### Description

喂狗。

#### Function prototype

```c
void wdt_feed(wdt_device_number_t id)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | Input       |

#### Return value

None.

### wdt\_clear\_interrupt

#### Description

清除中断。如果在中断函数中清除中断，则看门狗不会重启。

#### Function prototype

```c
void wdt_clear_interrupt(wdt_device_number_t id)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | Input       |

#### Return value

None.

### Example

```c
/* 2秒后进入看门狗中断函数打印Hello_world，再过2s复位 */
int wdt0_irq(void)
{
    printf("Hello_world\n");
    return 0;
}
plic_init();
sysctl_enable_irq();
wdt_start(WDT_DEVICE_0, 2000, wdt0_irq);
```

## Data type

The relevant data types and data structures are defined as follows:

- wdt\_device\_number\_t

### wdt\_device\_number\_t

#### Description

看门狗编号。

#### Type definition

```c
typedef enum _wdt_device_number
{
    WDT_DEVICE_0,
    WDT_DEVICE_1,
    WDT_DEVICE_MAX,
} wdt_device_number_t;
```

#### Enumeration element

| Element name         | Description         |
| --------------- | ------------ |
| WDT\_DEVICE\_0  | 看门狗 0      |
| WDT\_DEVICE\_1  | 看门狗 1      |