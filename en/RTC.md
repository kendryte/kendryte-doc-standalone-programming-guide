# RTC

## Overview

The Real Time Clock (RTC) is a unit for timing and has a timing function after
the set time.

**Note** The RTC unit is only used when PLL0 is enabled and the CPU frequency is greater than 30MHz.

## Features

The RTC unit has the following features:

- Get current date and time
- Set the current date and time
- Set timing interrupt
- Set alarm interrupt

## API

Corresponding header file `rtc.h`

Provide the following interfaces

- rtc\_init

- rtc\_timer\_set

- rtc\_timer\_get

### rtc\_init

#### Description

Initialize the RTC.

#### Function prototype

```c
int rtc_init(void)
```

#### Parameter

None.

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| 非0          | Fail        |

### rtc\_timer\_set

#### Description

Set the RTC date and time.

#### Function prototype

```c
int rtc_timer_set(int year, int month, int day, int hour, int minute, int second)
```

#### Parameter

| Parameter name | Description | Input or output |
| :------------- | :---------- | :-------------- |
| year           | Year        | Input           |
| month          | Month       | Input           |
| day            | Day         | Input           |
| hour           | Hour        | Input           |
| minute         | Minute      | Input           |
| second         | Second      | Input           |

#### Return value

None.

### rtc\_timer\_get

#### Description

Get the RTC date and time.

#### Function prototype

```c
int rtc_timer_get(int *year, int *month, int *day, int *hour, int *minute, int *second)
```

#### Parameter

| Parameter name | Description | Input or output |
| :------------- | :---------- | :-------------- |
| year           | Year        | Output          |
| month          | Month       | Output          |
| day            | Day         | Output          |
| hour           | Hour        | Output          |
| minute         | Minute      | Output          |
| second         | Second      | Output          |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| 非0          | Fail        |

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