# 定时器 (TIMER)

## Overview

芯片有3个定时器，每个定时器有4路通道。可以配置为PWM，详见PWM说明。

## Features

TIMER 模块具有以下功能: 

- 启用或禁用定时器
- 配置定时器触发间隔
- 配置定时器触发处理程序

## API

Corresponding header file `timer.h`

Provide the following interfaces

- timer\_init

- timer\_set\_interval

- timer\_set\_irq (deprecated)

- timer\_set\_enable

- timer\_irq\_register

- timer\_irq\_deregister

### timer\_init

#### Description

Initialize 定时器.

#### Function prototype

```c
void timer_init(timer_device_number_t timer_number)
```

#### Parameter

| Parameter name         | Description        | Input or output  |
| :-------------- | :----------| :-------- |
| timer\_number   | 定时器号    | Input      |

#### Return value

None.

### timer\_set\_interval

#### Description

设置定时间隔。

#### Function prototype

```c
size_t timer_set_interval(timer_device_number_t timer_number, timer_channel_number_t channel, size_t nanoseconds)
```

#### Parameter

| Parameter name      | Description           | Input or output   |
| :----------- | :------------- | :-------- |
| timer\_number| 定时器号        | Input      |
| channel      | 定时器通道号    | Input      |
| nanoseconds  | 时间间隔（纳秒） | Input      |

#### Return value

实际的触发间隔（纳秒）。

### timer\_set\_irq

#### Description

设置定时器触发中断回调函数，该函数已废弃，替代函数为timer\_irq\_register。

#### Function prototype

```c
void timer_set_irq(timer_device_number_t timer_number, timer_channel_number_t channel, void(*func)(),  uint32_t priority)
```

#### Parameter

| Parameter name       | Description           | Input or output   |
| :------------ | :------------- | :-------- |
| timer\_number | 定时器号        | Input     |
| channel       | 定时器通道号    | Input      |
| func          | 回调函数        | Input      |
| priority      | 中断优先级      | Input      |

#### Return value

None.

### timer\_set\_enable

#### Description

使能禁用定时器。

#### Function prototype

```c
void timer_set_enable(timer_device_number_t timer_number, timer_channel_number_t channel, uint32_t enable)
```

#### Parameter

| Parameter name       | Description           | Input or output   |
| :------------ | :------------- | :-------- |
| timer\_number | 定时器号        | Input      |
| channel       | 定时器通道号    | Input      |
| enable        | 使能禁用定时器<br>0: 禁用 1: 使能  | Input      |

#### Return value

None.

### timer\_irq\_register

#### Description

注册定时器触发中断回调函数。

#### Function prototype

```c
int timer_irq_register(timer_device_number_t device, timer_channel_number_t channel, int is_single_shot, uint32_t priority, timer_callback_t callback, void *ctx);
```

#### Parameter

| Parameter name          | Description           | Input or output   |
| :--------------- | :------------- | :-------- |
| device           | 定时器号        | Input      |
| channel          | 定时器通道号    | Input      |
| is\_single\_shot | 是否单次中断    | Input      |
| priority         | 中断优先级      | Input      |
| callback         | 中断回调函数    | Input      |
| ctx              | 回调函数参数    | Input      |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | Success |
| Others   | Fail |

### timer\_irq\_deregister

#### Description

注销定时器中断函数。

#### Function prototype

```c
int timer_irq_deregister(timer_device_number_t device, timer_channel_number_t channel)
```

#### Parameter

| Parameter name          | Description           | Input or output   |
| :--------------- | :------------- | :-------- |
| device           | 定时器号        | Input      |
| channel          | 定时器通道号    | Input      |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | Success |
| Others   | Fail |

### Example

```c
/* 定时器0 通道0 定时1秒打印Time OK! */
void irq_time(void)
{
    printf("Time OK!\n");
}
plic_init();
timer_init(TIMER_DEVICE_0);
timer_set_interval(TIMER_DEVICE_0, TIMER_CHANNEL_0, 1e9);
timer_set_irq(TIMER_CHANNEL_0, TIMER_CHANNEL_0, irq_time, 1);
timer_set_enable(TIMER_CHANNEL_0, TIMER_CHANNEL_0, 1);
sysctl_enable_irq();
```

## Data type

The relevant data types and data structures are defined as follows:

- timer\_device\_number_t: 定时器编号。

- timer\_channel\_number_t: 定时器通道号。

- timer\_callback\_t: 定时器回调函数。

### timer\_device\_number_t

#### Description

定时器编号

#### Type definition

```c
typedef enum _timer_deivce_number
{
    TIMER_DEVICE_0,
    TIMER_DEVICE_1,
    TIMER_DEVICE_2,
    TIMER_DEVICE_MAX,
} timer_device_number_t;
```

#### Enumeration element

| Element name           | Description          |
| ----------------- | ------------- |
| TIMER\_DEVICE\_0  | 定时器 0      |
| TIMER\_DEVICE\_1  | 定时器 1      |
| TIMER\_DEVICE\_2  | 定时器 2      |

### timer\_channel\_number_t

#### Description

定时器通道号。

#### Type definition

```c
typedef enum _timer_channel_number
{
    TIMER_CHANNEL_0,
    TIMER_CHANNEL_1,
    TIMER_CHANNEL_2,
    TIMER_CHANNEL_3,
    TIMER_CHANNEL_MAX,
} timer_channel_number_t;
```

#### Enumeration element

| Element name            | Description             |
| -----------------  | ---------------- |
| TIMER\_CHANNEL\_0  | 定时器通道 0      |
| TIMER\_CHANNEL\_1  | 定时器通道 1      |
| TIMER\_CHANNEL\_2  | 定时器通道 2      |
| TIMER\_CHANNEL\_3  | 定时器通道 3      |

### timer\_callback\_t

#### Description

定时器回调函数。

#### Type definition

```c
typedef int (*timer_callback_t)(void *ctx);
```