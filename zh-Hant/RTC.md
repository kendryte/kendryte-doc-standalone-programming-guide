# 實時時脈(RTC)

## 概述

RTC是用來計時的單元，在設置時間後具備計時功能。  
**註意** RTC模組僅當 PLL0 啟動,並且 CPU 頻率大於 30MHz 時使用

## 功能描述

RTC 模組具有以下功能：

- 獲取當前日期時刻
- 設置當前日期時刻

## API參考

對應的頭文件 `rtc.h`

為用戶提供以下介面

- rtc\_init

- rtc\_timer\_set

- rtc\_timer\_get

### rtc\_init

#### 描述

初始化RTC。

#### 函數原型

```c
int rtc_init(void)
```

#### 參數

無。

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失敗 |

### rtc\_timer\_set

#### 描述

設置日期時間。

#### 函數原型

```c
int rtc_timer_set(int year, int month, int day, int hour, int minute, int second)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :--------- | :-------- |
| year        | 年         | 輸入       |
| month       | 月         | 輸入       |
| day         | 日         | 輸入       |
| hour        | 時         | 輸入       |
| minute      | 分         | 輸入       |
| second      | 秒         | 輸入       |

#### 返回值

無

### rtc\_timer\_get

#### 描述

獲取日期時間。

#### 函數原型

```c
int rtc_timer_get(int *year, int *month, int *day, int *hour, int *minute, int *second)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :--------- | :-------- |
| year        | 年         | 輸出       |
| month       | 月         | 輸出       |
| day         | 日         | 輸出       |
| hour        | 時         | 輸出       |
| minute      | 分         | 輸出       |
| second      | 秒         | 輸出       |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失敗 |

### 舉例

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