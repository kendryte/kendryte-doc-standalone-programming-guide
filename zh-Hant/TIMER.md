# 定時器 (TIMER)

## 概述

晶片有3個定時器，每個定時器有4路通道。可以配置為PWM，詳見PWM說明。

## 功能描述

TIMER 模組具有以下功能：

- 啟用或禁用定時器
- 配置定時器觸發間隔
- 配置定時器觸發處理程序

## API 參考

對應的頭文件 `timer.h`

為用戶提供以下介面

- timer\_init

- timer\_set\_interval

- timer\_set\_irq (0.6.0後不再支持，請使用timer\_irq\_register)

- timer\_set\_enable

- timer\_irq\_register

- timer\_irq\_deregister

### timer\_init

#### 描述

初始化定時器。

#### 函數原型

```c
void timer_init(timer_device_number_t timer_number)
```

#### 參數

| 參數名稱         | 描述        | 輸入輸出  |
| :-------------- | :----------| :-------- |
| timer\_number   | 定時器號    | 輸入      |

#### 返回值

無。

### timer\_set\_interval

#### 描述

設置定時間隔。

#### 函數原型

```c
size_t timer_set_interval(timer_device_number_t timer_number, timer_channel_number_t channel, size_t nanoseconds)
```

#### 參數

| 參數名稱      | 描述           | 輸入輸出   |
| :----------- | :------------- | :-------- |
| timer\_number| 定時器號        | 輸入      |
| channel      | 定時器通道號    | 輸入      |
| nanoseconds  | 時間間隔（納秒） | 輸入      |

#### 返回值

實際的觸發間隔（納秒）。

### timer\_set\_irq

#### 描述

設置定時器觸發中斷回調函數，該函數已廢棄，替代函數為timer\_irq\_register。

#### 函數原型

```c
void timer_set_irq(timer_device_number_t timer_number, timer_channel_number_t channel, void(*func)(),  uint32_t priority)
```

#### 參數

| 參數名稱       | 描述           | 輸入輸出   |
| :------------ | :------------- | :-------- |
| timer\_number | 定時器號        | 輸入     |
| channel       | 定時器通道號    | 輸入      |
| func          | 回調函數        | 輸入      |
| priority      | 中斷優先順序      | 輸入      |

#### 返回值

無。

### timer\_set\_enable

#### 描述

啟動禁用定時器。

#### 函數原型

```c
void timer_set_enable(timer_device_number_t timer_number, timer_channel_number_t channel, uint32_t enable)
```

#### 參數

| 參數名稱       | 描述           | 輸入輸出   |
| :------------ | :------------- | :-------- |
| timer\_number | 定時器號        | 輸入      |
| channel       | 定時器通道號    | 輸入      |
| enable        | 啟動禁用定時器<br>0：禁用 1：啟動  | 輸入      |

#### 返回值

無。

### timer\_irq\_register

#### 描述

註冊定時器觸發中斷回調函數。

#### 函數原型

```c
int timer_irq_register(timer_device_number_t device, timer_channel_number_t channel, int is_single_shot, uint32_t priority, timer_callback_t callback, void *ctx);
```

#### 參數

| 參數名稱          | 描述           | 輸入輸出   |
| :--------------- | :------------- | :-------- |
| device           | 定時器號        | 輸入      |
| channel          | 定時器通道號    | 輸入      |
| is\_single\_shot | 是否單次中斷    | 輸入      |
| priority         | 中斷優先順序      | 輸入      |
| callback         | 中斷回調函數    | 輸入      |
| ctx              | 回調函數參數    | 輸入      |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### timer\_irq\_deregister

#### 描述

註銷定時器中斷函數。

#### 函數原型

```c
int timer_irq_deregister(timer_device_number_t device, timer_channel_number_t channel)
```

#### 參數

| 參數名稱          | 描述           | 輸入輸出   |
| :--------------- | :------------- | :-------- |
| device           | 定時器號        | 輸入      |
| channel          | 定時器通道號    | 輸入      |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### 舉例

```c
/* 定時器0 通道0 定時1秒列印Time OK! */
void irq_time(void)
{
    printf("Time OK!\n");
}
plic_init();
timer_init(TIMER_DEVICE_0);
timer_set_interval(TIMER_DEVICE_0, TIMER_CHANNEL_0, 1e9);
timer_set_irq(TIMER_DEVICE_0, TIMER_CHANNEL_0, irq_time, 1);
timer_set_enable(TIMER_DEVICE_0, TIMER_CHANNEL_0, 1);
sysctl_enable_irq();
```

## 資料類型

相關資料類型、資料結構定義如下：

- timer\_device\_number_t：定時器編號。

- timer\_channel\_number_t：定時器通道號。

- timer\_callback\_t：定時器回調函數。

### timer\_device\_number_t

#### 描述

定時器編號

#### 定義

```c
typedef enum _timer_deivce_number
{
    TIMER_DEVICE_0,
    TIMER_DEVICE_1,
    TIMER_DEVICE_2,
    TIMER_DEVICE_MAX,
} timer_device_number_t;
```

#### 成員

| 成員名稱           | 描述          |
| ----------------- | ------------- |
| TIMER\_DEVICE\_0  | 定時器 0      |
| TIMER\_DEVICE\_1  | 定時器 1      |
| TIMER\_DEVICE\_2  | 定時器 2      |

### timer\_channel\_number_t

#### 描述

定時器通道號。

#### 定義

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

#### 成員

| 成員名稱            | 描述             |
| -----------------  | ---------------- |
| TIMER\_CHANNEL\_0  | 定時器通道 0      |
| TIMER\_CHANNEL\_1  | 定時器通道 1      |
| TIMER\_CHANNEL\_2  | 定時器通道 2      |
| TIMER\_CHANNEL\_3  | 定時器通道 3      |

### timer\_callback\_t

#### 描述

定時器回調函數。

#### 定義

```c
typedef int (*timer_callback_t)(void *ctx);
```
