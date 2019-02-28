# PWM

## Overview

A pulse width modulator (PWM) is used to control the duty cycle of the pulse output.
It is essentially a timer, so be careful not to conflict with the timer when setting the PWM number and channel.

## Features

The PWM module has the following features:

- Configure the PWM output frequency
- Configure the output duty cycle of each pin of the PWM

## API

Corresponding header file `pwm.h`

Provide the following interfaces

- pwm\_init

- pwm\_set\_frequency

- pwm\_set\_enable

### pwm\_init

#### Description

Initialize PWM.

#### Function prototype

```c
void pwm_init(pwm_device_number_t pwm_number)
```

#### Parameter

| Parameter name | Description | Input or output |
| :------------- | :---------- | :-------------: |
| pwm_number     | PWM number  |      Input      |

#### Return value

None.

### pwm\_set\_frequency

#### Description

Set the frequency and duty cycle.

#### Function prototype

```c
double pwm_set_frequency(pwm_device_number_t pwm_number, pwm_channel_number_t channel, double frequency, double duty)
```

#### Parameter

| Parameter name |     Description      | Input or output |
| :------------- | :------------------- | :-------------- |
| pwm_number     | PWM number           | Input           |
| channel        | PWM channel number   | Input           |
| frequency      | PWM output frequency | Input           |
| duty           | Duty cycle           | Input           |

#### Return value

Actual output frequency.

### pwm_set_enable

#### Description

Enable or disable the PWM.

#### Function prototype

```c
void pwm_set_enable(pwm_device_number_t pwm_number, uint32_t channel, int enable)
```

#### Parameter

| Parameter name |               Description               | Input or output |
| :------------- | :-------------------------------------- | :-------------- |
| pwm_number     | PWM number                              | Input           |
| channel        | PWM channel number                      | Input           |
| enable         | Whether to enable, 0: Disable 1: Enable | Input           |

#### Return value

None.

### Example

```c
/* pwm0 pin0 output 200KHz square wave with duty cycle of 0.5 */
/* Set IO13 as the output pin of PWM */
fpioa_set_function(13, FUNC_TIMER0_TOGGLE1);
pwm_init(PWM_DEVICE_0);
pwm_set_frequency(PWM_DEVICE_0, PWM_CHANNEL_1, 200000, 0.5);
pwm_set_enable(PWM_DEVICE_0, PWM_CHANNEL_1, 1);
```

## Data type

- pwm\_device\_number\_t: PWM device number.

- pwm\_channel\_number\_t: PWM channel number.

### pwm\_device\_number\_t

#### Description

PWM device number.

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

#### Enumeration element

|  Element name  | Description |
| :------------- | :---------- |
| PWM\_DEVICE\_0 | PWM0        |
| PWM\_DEVICE\_1 | PWM1        |
| PWM\_DEVICE\_2 | PWM2        |

### pwm\_channel\_number\_t

#### Description

PWM channel number.

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

#### Enumeration element

|  Element name   |  Description  |
| :-------------- | :------------ |
| PWM\_CHANNEL\_0 | PWM channel 0 |
| PWM\_CHANNEL\_1 | PWM channel 1 |
| PWM\_CHANNEL\_2 | PWM channel 2 |
| PWM\_CHANNEL\_3 | PWM channel 3 |
