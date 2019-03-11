# 脈衝寬度調製器(PWM)

## 概述

PWM 用於控制脈衝輸出的占空比。其本質是一個定時器，所以註意設置PWM號與通道時不要與TIMER定時器衝突。

## 功能描述

PWM 模組具有以下功能：

- 配置 PWM 輸出頻率
- 配置 PWM 每個腳位的輸出占空比

## API參考

對應頭文件 `pwm.h`  

為用戶提供以下介面

- pwm\_init

- pwm\_set\_frequency

- pwm\_set\_enable

### pwm\_init

#### 描述

初始化PWM。

#### 函數原型

```c
void pwm_init(pwm_device_number_t pwm_number)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| pwm_number | pwm號 | 輸入 |

#### 返回值

無。

### pwm\_set\_frequency

#### 描述

設置頻率及占空比。

#### 函數原型

```c
double pwm_set_frequency(pwm_device_number_t pwm_number, pwm_channel_number_t channel, double frequency, double duty)
```

#### 參數

| 參數名稱     | 描述                             |  輸入輸出  |
| :---------- | :------------------------------- | :-------- |
| pwm_number  | PWM號                            | 輸入       |
| channel     | PWM通道號                        | 輸入       |
| frequency   | PWM輸出頻率                       | 輸入       |
| duty        | 占空比                            | 輸入      |

#### 返回值

實際輸出頻率。

### pwm_set_enable

#### 描述

啟動禁用PWM。

#### 函數原型

```c
void pwm_set_enable(pwm_device_number_t pwm_number, uint32_t channel, int enable)
```

#### 參數

| 參數名稱     |   描述                          |  輸入輸出  |
| :---------- | :------------------------------ | :-------- |
| pwm_number  | PWM號                           | 輸入       |
| channel     | PWM通道號                        | 輸入      |
| enable      | 啟動禁用PWM<br>0：禁用  1：啟動   | 輸入      |

#### 返回值

無。

### 舉例

```c
/* pwm0 channel 1 輸出 200KHZ占空比為0.5的方波 */
/* 設置IO13作為PWM的輸出腳位 */
fpioa_set_function(13, FUNC_TIMER0_TOGGLE1);
pwm_init(PWM_DEVICE_0);
pwm_set_frequency(PWM_DEVICE_0, PWM_CHANNEL_1, 200000, 0.5);
pwm_set_enable(PWM_DEVICE_0, PWM_CHANNEL_1, 1);
```

## 資料類型

- pwm\_device\_number\_t：pwm號。

- pwm\_channel\_number\_t：pwm通道號。

### pwm\_device\_number\_t

#### 描述

pwm號。

#### 定義

```c
typedef enum _pwm_device_number
{
    PWM_DEVICE_0,
    PWM_DEVICE_1,
    PWM_DEVICE_2,
    PWM_DEVICE_MAX,
} pwm_device_number_t;
```

#### 成員

| 成員名稱        | 描述 |
| :------------- | :--- |
| PWM\_DEVICE\_0 | PWM0 |
| PWM\_DEVICE\_1 | PWM1 |
| PWM\_DEVICE\_2 | PWM2 |

### pwm\_channel\_number\_t

#### 描述

pwm通道號。

#### 定義

```c
typedef enum _pwm_channel_number
{
    PWM_CHANNEL_0,
    PWM_CHANNEL_1,
    PWM_CHANNEL_2,
    PWM_CHANNEL_3,
    PWM_CHANNEL_MAX,
} pwm_channel_number_t;
```

#### 成員

| 成員名稱         | 描述     |
| :-------------- | :------- |
| PWM\_CHANNEL\_0 | PWM通道0 |
| PWM\_CHANNEL\_1 | PWM通道1 |
| PWM\_CHANNEL\_2 | PWM通道2 |
| PWM\_CHANNEL\_3 | PWM通道3 |