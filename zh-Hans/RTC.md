# 实时时钟(RTC)

## 概述

RTC是用来计时的单元，在设置时间后具备计时功能。  
**注意** RTC模块仅当 PLL0 使能,并且 CPU 频率大于 30MHz 时使用

## 功能描述

RTC 模块具有以下功能：

- 获取当前日期时刻
- 设置当前日期时刻

## API参考

对应的头文件 `rtc.h`

为用户提供以下接口

- rtc\_init

- rtc\_timer\_set

- rtc\_timer\_get

- rtc\_alarm\_set

- rtc\_alarm\_get

- rtc\_tick\_irq\_register

- rtc\_tick\_irq\_unregister

- rtc\_alarm\_irq\_register

- rtc\_alarm\_irq\_unregister

### rtc\_init

#### 描述

初始化RTC。

#### 函数原型

```c
int rtc_init(void)
```

#### 参数

无。

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### rtc\_timer\_set

#### 描述

设置日期时间。

#### 函数原型

```c
int rtc_timer_set(int year, int month, int day, int hour, int minute, int second)
```

#### 参数

| 参数名称     |   描述     |  输入输出  |
| :--------   | :--------- | :-------- |
| year        | 年         | 输入       |
| month       | 月         | 输入       |
| day         | 日         | 输入       |
| hour        | 时         | 输入       |
| minute      | 分         | 输入       |
| second      | 秒         | 输入       |

#### 返回值

无

### rtc\_timer\_get

#### 描述

获取日期时间。

#### 函数原型

```c
int rtc_timer_get(int *year, int *month, int *day, int *hour, int *minute, int *second)
```

#### 参数

| 参数名称     |   描述     |  输入输出  |
| :--------   | :--------- | :-------- |
| year        | 年         | 输出       |
| month       | 月         | 输出       |
| day         | 日         | 输出       |
| hour        | 时         | 输出       |
| minute      | 分         | 输出       |
| second      | 秒         | 输出       |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### rtc\_alarm\_set

#### 描述

设置日期时间。

#### 函数原型

```c
int rtc_alarmr_set(int year, int month, int day, int hour, int minute, int second)
```

#### 参数

| 参数名称     |   描述     |  输入输出  |
| :--------   | :--------- | :-------- |
| year        | 年         | 输入       |
| month       | 月         | 输入       |
| day         | 日         | 输入       |
| hour        | 时         | 输入       |
| minute      | 分         | 输入       |
| second      | 秒         | 输入       |

#### 返回值

无

### rtc\_alarm\_get

#### 描述

获取日期时间。

#### 函数原型

```c
int rtc_alarm_get(int *year, int *month, int *day, int *hour, int *minute, int *second)
```

#### 参数

| 参数名称     |   描述     |  输入输出  |
| :--------   | :--------- | :-------- |
| year        | 年         | 输出       |
| month       | 月         | 输出       |
| day         | 日         | 输出       |
| hour        | 时         | 输出       |
| minute      | 分         | 输出       |
| second      | 秒         | 输出       |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### rtc\_tick\_irq\_register

#### 描述

设置RTC tick中断，可以设置整秒、整分、整时、整天中断。

#### 函数原型

```c
int rtc_tick_irq_register(bool is_single_shot, rtc_tick_interrupt_mode_t mode, plic_irq_callback_t callback, void *ctx, uint8_t priority)
```

#### 参数

| 参数名称                             |   描述                                       |  输入输出  |
| :--------------------------------   | :------------------------------------------- | :-------- |
| is_single_shot                      | 是否单次触发                                  | 输入       |
| mode                                | 中断触发模式                                  | 输入       |
| callback                            | 回调函数                                      | 输入       |
| ctx                                 | 回调函数参数                                  | 输入       |
| priority                            | 优先级                                        | 输入       |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### rtc\_tick\_irq\_unregister

#### 描述

注销tick中断。

#### 函数原型

```c
void rtc_tick_irq_unregister(void);
```

#### 参数

无。

#### 返回值

无。

### rtc\_alarm\_irq\_register

#### 描述

注册alarm中断。

#### 函数原型

```c
int rtc_alarm_irq_register(bool is_single_shot, rtc_mask_t mask, plic_irq_callback_t callback, void *ctx, uint8_t priority)
```

#### 参数

| 参数名称                             |   描述                                       |  输入输出  |
| :--------------------------------   | :------------------------------------------- | :-------- |
| is_single_shot                      | 是否单次触发                                  | 输入       |
| mask                                | alarm中断掩码，用于灵活配置中断触发方式         | 输入       |
| callback                            | 回调函数                                      | 输入       |
| ctx                                 | 回调函数参数                                  | 输入       |
| priority                            | 优先级                                        | 输入       |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### rtc\_alarm\_irq\_unregister

#### 描述

注销alarm中断。

#### 函数原型

```c
void rtc_alarm_irq_unregister(void)
```

#### 参数

无。

#### 返回值

无。

### 举例

```c

int tick_irq(void *ctx)
{
    printk("%s\n", __func__);
    return 0;
}

int alarm_irq(void *ctx)
{
    printk("%s\n", __func__);
    return 0;
}


rtc_init();
rtc_timer_set(2019, 5, 7, 15, 4, 55);
rtc_tick_irq_register(true, RTC_INT_MINUTE, tick_irq, NULL, 1);

rtc_alarm_set(2019, 5, 7, 15, 5, 5);
rtc_mask_t mask = (rtc_mask_t)
{
    .second = 0,
    .minute = 1,
    .hour = 1,
    .day = 1,
    .month = 1,
    .year = 1,
};
rtc_alarm_irq_register(true, mask, alarm_irq, NULL, 1);
int year;
int month;
int day;
int hour;
int minute;
int second;
rtc_timer_get(&year, &month, &day, &hour, &minute, &second);
printf("%4d-%d-%d %d:%d:%d\n", year, month, day, hour, minute, second);
```