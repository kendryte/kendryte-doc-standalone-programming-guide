# 脉冲宽度调制器(PWM)

## Summary

PWM 用于控制脉冲输出的占空比。其本质是一个定时器，所以注意设置PWM号与通道时不要与TIMER定时器冲突。

## Features

PWM 模块具有以下功能：

- 配置 PWM 输出频率
- 配置 PWM 每个管脚的输出占空比

## API

对应头文件 `pwm.h`

Provide the following interfaces

- pwm\_init

- pwm\_set\_frequency

- pwm\_set\_enable

### pwm\_init

#### Description

初始化PWM。

#### Function prototype

```c
void pwm_init(pwm_device_number_t pwm_number)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| pwm_number | pwm号 | 输入 |

#### Return value

None.

### pwm\_set\_frequency

#### Description

设置频率及占空比。

#### Function prototype

```c
double pwm_set_frequency(pwm_device_number_t pwm_number, pwm_channel_number_t channel, double frequency, double duty)
```

#### Parameter

| Parameter name     | Description                             |  Input or output  |
| :---------- | :------------------------------- | :-------- |
| pwm_number  | PWM号                            | 输入       |
| channel     | PWM通道号                        | 输入       |
| frequency   | PWM输出频率                       | 输入       |
| duty        | 占空比                            | 输入      |

#### Return value

实际输出频率。

### pwm_set_enable

#### Description

使能禁用PWM。

#### Function prototype

```c
void pwm_set_enable(pwm_device_number_t pwm_number, uint32_t channel, int enable)
```

#### Parameter

| Parameter name     |   Description                          |  Input or output  |
| :---------- | :------------------------------ | :-------- |
| pwm_number  | PWM号                           | 输入       |
| channel     | PWM通道号                        | 输入      |
| enable      | 使能禁用PWM<br>0：禁用  1：使能   | 输入      |

#### Return value

None.

### Example

```c
/* pwm0 channel 1 输出 200KHZ占空比为0.5的方波 */
/* 设置IO13作为PWM的输出管脚 */
fpioa_set_function(13, FUNC_TIMER0_TOGGLE1);
pwm_init(PWM_DEVICE_0);
pwm_set_frequency(PWM_DEVICE_0, PWM_CHANNEL_1, 200000, 0.5);
pwm_set_enable(PWM_DEVICE_0, PWM_CHANNEL_1, 1);
```

## Data type

- pwm\_device\_number\_t：pwm号。

- pwm\_channel\_number\_t：pwm通道号。

### pwm\_device\_number\_t

#### Description

pwm号。

#### Type definition

```c
typedef enum _pwm_device_number
{
    PWM_DEVICE_0,
    PWM_DEVICE_1,
    PWM_DEVICE_2,
    PWM_DEVICE_MAX,
} pwm_device_number_t;
```

#### 成员

| 成员名称        | Description |
| :------------- | :--- |
| PWM\_DEVICE\_0 | PWM0 |
| PWM\_DEVICE\_1 | PWM1 |
| PWM\_DEVICE\_2 | PWM2 |

### pwm\_channel\_number\_t

#### Description

pwm通道号。

#### Type definition

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

#### 成员

| 成员名称         | Description     |
| :-------------- | :------- |
| PWM\_CHANNEL\_0 | PWM通道0 |
| PWM\_CHANNEL\_1 | PWM通道1 |
| PWM\_CHANNEL\_2 | PWM通道2 |
| PWM\_CHANNEL\_3 | PWM通道3 |