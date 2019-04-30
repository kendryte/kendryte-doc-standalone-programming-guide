# TIMER

## Overview

The timer peripheral provides high-precision timing.
The chip has 3 timers, each with 4 channels. Can be configured as PWM, see PWM description for details.

## Features

The TIMER module has the following features:

- Enable or disable the timer
- Configure timer trigger interval
- Configure timer trigger handler

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

Initialize timer.

#### Function prototype

```c
void timer_init(timer_device_number_t timer_number)
```

#### Parameter

| Parameter name | Description  | Input or output |
| :------------- | :----------- | :-------------- |
| timer\_number  | Timer number | Input           |

#### Return value

None.

### timer\_set\_interval

#### Description

Set the timer trigger interval.

#### Function prototype

```c
size_t timer_set_interval(timer_device_number_t timer_number, timer_channel_number_t channel, size_t nanoseconds)
```

#### Parameter

| Parameter name |      Description       | Input or output |
| :------------- | :--------------------- | :-------------- |
| timer\_number  | Timer number           | Input           |
| channel        | Timer channel number   | Input           |
| nanoseconds    | Interval (nanoseconds) | Input           |

#### Return value

Actual trigger interval (nanoseconds).

### timer\_set\_irq

#### Description

Set the timer to trigger the interrupt callback function. This function is deprecated. The recommended replacement function is timer\_irq\_register.

#### Function prototype

```c
void timer_set_irq(timer_device_number_t timer_number, timer_channel_number_t channel, void(*func)(),  uint32_t priority)
```

#### Parameter

| Parameter name |     Description      | Input or output |
| :------------- | :------------------- | :-------------- |
| timer\_number  | Timer number         | Input           |
| channel        | Timer channel number | Input           |
| func           | Callback             | Input           |
| priority       | Interrupt priority   | Input           |

#### Return value

None.

### timer\_set\_enable

#### Description

Enable or disable the timer.

#### Function prototype

```c
void timer_set_enable(timer_device_number_t timer_number, timer_channel_number_t channel, uint32_t enable)
```

#### Parameter

| Parameter name |                 Description                 | Input or output |
| :------------- | :------------------------------------------ | :-------------- |
| timer\_number  | Timer number                                | Input           |
| channel        | Timer channel number                        | Input           |
| enable         | Whether it is enabled, 0: disable 1: enable | Input           |

#### Return value

None.

### timer\_irq\_register

#### Description

Register the timer interrupt callback function.

#### Function prototype

```c
int timer_irq_register(timer_device_number_t device, timer_channel_number_t channel, int is_single_shot, uint32_t priority, timer_callback_t callback, void *ctx);
```

#### Parameter

|  Parameter name  |               Description                | Input or output |
| :--------------- | :--------------------------------------- | :-------------- |
| device           | Timer number                             | Input           |
| channel          | Timer channel number                     | Input           |
| is\_single\_shot | Whether it is a single shot interruption | Input           |
| priority         | Interrupt priority                       | Input           |
| callback         | Interrupt callback function              | Input           |
| ctx              | Callback function parameter              | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### timer\_irq\_deregister

#### Description

Deregister the timer interrupt callback function.

#### Function prototype

```c
int timer_irq_deregister(timer_device_number_t device, timer_channel_number_t channel)
```

#### Parameter

| Parameter name |     Description      | Input or output |
| :------------- | :------------------- | :-------------- |
| device         | Timer number         | Input           |
| channel        | Timer channel number | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### Example

```c
/* Timer 0 Channel 0 timed 1 second print "Time OK!" */
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

## Data type

The relevant data types and data structures are defined as follows:

- timer\_device\_number_t: Timer number.

- timer\_channel\_number_t: Timer channel number.

- timer\_callback\_t: Timer callback function.

### timer\_device\_number_t

#### Description

Timer number.

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

|   Element name   | Description |
| ---------------- | ----------- |
| TIMER\_DEVICE\_0 | Timer 0     |
| TIMER\_DEVICE\_1 | Timer 1     |
| TIMER\_DEVICE\_2 | Timer 2     |

### timer\_channel\_number_t

#### Description

Timer channel number.

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

|   Element name    |   Description   |
| ----------------- | --------------- |
| TIMER\_CHANNEL\_0 | Timer channel 0 |
| TIMER\_CHANNEL\_1 | Timer channel 1 |
| TIMER\_CHANNEL\_2 | Timer channel 2 |
| TIMER\_CHANNEL\_3 | Timer channel 3 |

### timer\_callback\_t

#### Description

Timer callback function.

#### Type definition

```c
typedef int (*timer_callback_t)(void *ctx);
```