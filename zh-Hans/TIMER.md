# 定时器 (TIMER)

## 概述

芯片有3个定时器，每个定时器有4路通道。可以配置为PWM，详见PWM说明。

## 功能描述

TIMER 模块具有以下功能：

- 启用或禁用定时器
- 配置定时器触发间隔
- 配置定时器触发处理程序

## API 参考

对应的头文件 `timer.h`

为用户提供以下接口

- timer\_init

- timer\_set\_interval

- timer\_set\_irq (0.6.0后不再支持，请使用timer\_irq\_register)

- timer\_set\_enable

- timer\_irq\_register

- timer\_irq\_deregister

### timer\_init

#### 描述

初始化定时器。

#### 函数原型

```c
void timer_init(timer_device_number_t timer_number)
```

#### 参数

| 参数名称         | 描述        | 输入输出  |
| :-------------- | :----------| :-------- |
| timer\_number   | 定时器号    | 输入      |

#### 返回值

无。

### timer\_set\_interval

#### 描述

设置定时间隔。

#### 函数原型

```c
size_t timer_set_interval(timer_device_number_t timer_number, timer_channel_number_t channel, size_t nanoseconds)
```

#### 参数

| 参数名称      | 描述           | 输入输出   |
| :----------- | :------------- | :-------- |
| timer\_number| 定时器号        | 输入      |
| channel      | 定时器通道号    | 输入      |
| nanoseconds  | 时间间隔（纳秒） | 输入      |

#### 返回值

实际的触发间隔（纳秒）。

### timer\_set\_irq

#### 描述

设置定时器触发中断回调函数，该函数已废弃，替代函数为timer\_irq\_register。

#### 函数原型

```c
void timer_set_irq(timer_device_number_t timer_number, timer_channel_number_t channel, void(*func)(),  uint32_t priority)
```

#### 参数

| 参数名称       | 描述           | 输入输出   |
| :------------ | :------------- | :-------- |
| timer\_number | 定时器号        | 输入     |
| channel       | 定时器通道号    | 输入      |
| func          | 回调函数        | 输入      |
| priority      | 中断优先级      | 输入      |

#### 返回值

无。

### timer\_set\_enable

#### 描述

使能禁用定时器。

#### 函数原型

```c
void timer_set_enable(timer_device_number_t timer_number, timer_channel_number_t channel, uint32_t enable)
```

#### 参数

| 参数名称       | 描述           | 输入输出   |
| :------------ | :------------- | :-------- |
| timer\_number | 定时器号        | 输入      |
| channel       | 定时器通道号    | 输入      |
| enable        | 使能禁用定时器<br>0：禁用 1：使能  | 输入      |

#### 返回值

无。

### timer\_irq\_register

#### 描述

注册定时器触发中断回调函数。

#### 函数原型

```c
int timer_irq_register(timer_device_number_t device, timer_channel_number_t channel, int is_single_shot, uint32_t priority, timer_callback_t callback, void *ctx);
```

#### 参数

| 参数名称          | 描述           | 输入输出   |
| :--------------- | :------------- | :-------- |
| device           | 定时器号        | 输入      |
| channel          | 定时器通道号    | 输入      |
| is\_single\_shot | 是否单次中断    | 输入      |
| priority         | 中断优先级      | 输入      |
| callback         | 中断回调函数    | 输入      |
| ctx              | 回调函数参数    | 输入      |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### timer\_irq\_deregister

#### 描述

注销定时器中断函数。

#### 函数原型

```c
int timer_irq_deregister(timer_device_number_t device, timer_channel_number_t channel)
```

#### 参数

| 参数名称          | 描述           | 输入输出   |
| :--------------- | :------------- | :-------- |
| device           | 定时器号        | 输入      |
| channel          | 定时器通道号    | 输入      |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### 举例

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

## 数据类型

相关数据类型、数据结构定义如下：

- timer\_device\_number_t：定时器编号。

- timer\_channel\_number_t：定时器通道号。

- timer\_callback\_t：定时器回调函数。

### timer\_device\_number_t

#### 描述

定时器编号

#### 定义

```c
typedef enum _timer_deivce_number
{
    TIMER_DEVICE_0,
    TIMER_DEVICE_1,
    TIMER_DEVICE_2,
    TIMER_DEVICE_MAX,
} timer_device_number_t;
```

#### 成员

| 成员名称           | 描述          |
| ----------------- | ------------- |
| TIMER\_DEVICE\_0  | 定时器 0      |
| TIMER\_DEVICE\_1  | 定时器 1      |
| TIMER\_DEVICE\_2  | 定时器 2      |

### timer\_channel\_number_t

#### 描述

定时器通道号。

#### 定义

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

#### 成员

| 成员名称            | 描述             |
| -----------------  | ---------------- |
| TIMER\_CHANNEL\_0  | 定时器通道 0      |
| TIMER\_CHANNEL\_1  | 定时器通道 1      |
| TIMER\_CHANNEL\_2  | 定时器通道 2      |
| TIMER\_CHANNEL\_3  | 定时器通道 3      |

### timer\_callback\_t

#### 描述

定时器回调函数。

#### 定义

```c
typedef int (*timer_callback_t)(void *ctx);
```