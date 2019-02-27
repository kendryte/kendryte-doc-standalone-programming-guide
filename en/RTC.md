# 实时时钟(RTC)

## Overview

The Real Time Clock (RTC) is a unit for timing and has a timing function after
the set time.

**Note** The RTC module is only used when PLL0 is enabled and the CPU frequency is greater than 30MHz.

## Features

RTC 模块具有以下功能：

- 获取当前日期时刻
- 设置当前日期时刻

## API

Corresponding header file `rtc.h`

Provide the following interfaces

- rtc\_init

- rtc\_timer\_set

- rtc\_timer\_get

### rtc\_init

#### Description

初始化RTC。

#### Function prototype

```c
int rtc_init(void)
```

#### Parameter

None.

#### Return value

| Return value | Description |
| :----  | :----|
| 0      | Success |
| 非0    | Fail |

### rtc\_timer\_set

#### Description

设置日期时间。

#### Function prototype

```c
int rtc_timer_set(int year, int month, int day, int hour, int minute, int second)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :--------- | :-------- |
| year        | 年         | Input       |
| month       | 月         | Input       |
| day         | 日         | Input       |
| hour        | 时         | Input       |
| minute      | 分         | Input       |
| second      | 秒         | Input       |

#### Return value

无

### rtc\_timer\_get

#### Description

获取日期时间。

#### Function prototype

```c
int rtc_timer_get(int *year, int *month, int *day, int *hour, int *minute, int *second)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :--------- | :-------- |
| year        | 年         | Output       |
| month       | 月         | Output       |
| day         | 日         | Output       |
| hour        | 时         | Output       |
| minute      | 分         | Output       |
| second      | 秒         | Output       |

#### Return value

| Return value | Description |
| :----  | :----|
| 0      | Success |
| 非0    | Fail |

### Example

```c
rtc_init();
rtc_timer_set(2018, 9, 12, 23, 30, 29);
int year;
int month;
int day;
int hour;
int minute;
int second;
rtc_timer_get(&year, &month, &day, &hour, &minute, &second);
printf("%4d-%d-%d %d:%d:%d\n", year, month, day, hour, minute, second);
```