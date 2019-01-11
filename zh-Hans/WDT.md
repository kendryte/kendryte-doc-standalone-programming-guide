# 看门狗定时器 (WDT)

## 概述

WDT 提供系统出错或无响应时的恢复功能。

## 功能描述

WDT 模块具有以下功能：

- 配置超时时间

- 手动重启计时

## API 参考

对应的头文件 `wdt.h`

为用户提供以下接口

- wdt\_init

- wdt\_start(0.6.0后不再支持，请使用wdt\_init)

- wdt\_stop

- wdt\_feed

- wdt\_clear\_interrupt

### wdt\_init

#### 描述

配置参数，启动看门狗。不使用中断的话，将on_irq设置为NULL。

#### 函数原型

```c
uint32_t wdt_init(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq, void *ctx)
```

#### 参数

| 参数名称         |   描述           |  输入输出  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | 输入       |
| time\_out\_ms   | 超时时间（毫秒）   | 输入      |
| on\_irq         | 中断回调函数      | 输入       |
| ctx             | 回调函数参数      | 输入       |

#### 返回值

看门狗超时重启的实际时间（毫秒）。与time\_out\_ms有差异，一般情况会大于这个时间。在外部晶振26M的情况下，最大超时时间为330毫秒。

### wdt\_start

#### 描述

启动看门狗。

#### 函数原型

```c
void wdt_start(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq)
```

#### 参数

| 参数名称         |   描述           |  输入输出  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | 输入       |
| time\_out\_ms   | 超时时间（毫秒）   | 输入      |
| on\_irq          | 中断回调函数     | 输入       |

#### 返回值

无

### wdt\_stop

#### 描述

关闭看门狗。

#### 函数原型

```c
void wdt_stop(wdt_device_number_t id)
```

#### 参数

| 参数名称         |   描述           |  输入输出  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | 输入       |

#### 返回值

无。

### wdt\_feed

#### 描述

喂狗。

#### 函数原型

```c
void wdt_feed(wdt_device_number_t id)
```

#### 参数

| 参数名称         |   描述           |  输入输出  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | 输入       |

#### 返回值

无。

### wdt\_clear\_interrupt

#### 描述

清除中断。如果在中断函数中清除中断，则看门狗不会重启。

#### 函数原型

```c
void wdt_clear_interrupt(wdt_device_number_t id)
```

#### 参数

| 参数名称         |   描述           |  输入输出  |
| --------------- | ---------------  | --------- |
| id              | 看门狗编号        | 输入       |

#### 返回值

无。

### 举例

```c
/* 2秒后进入看门狗中断函数打印Hello_world，再过2s复位 */
int wdt0_irq(void *ctx)
{
    printf("Hello_world\n");
    return 0;
}
plic_init();
sysctl_enable_irq();
wdt_init(WDT_DEVICE_0, 2000, wdt0_irq, NULL);
```

## 数据类型

相关数据类型、数据结构定义如下：

- wdt\_device\_number\_t

### wdt\_device\_number\_t

#### 描述

看门狗编号。

#### 定义

```c
typedef enum _wdt_device_number
{
    WDT_DEVICE_0,
    WDT_DEVICE_1,
    WDT_DEVICE_MAX,
} wdt_device_number_t;
```

#### 成员

| 成员名称         | 描述         |
| --------------- | ------------ |
| WDT\_DEVICE\_0  | 看门狗 0      |
| WDT\_DEVICE\_1  | 看门狗 1      |