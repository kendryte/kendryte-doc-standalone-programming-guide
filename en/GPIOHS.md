# GPIOHS

## Overview

GPIO stands for General Purpose Input Output.
HS stands for high speed.
The chip has 32 high speed GPIOs. Similar to normal GPIO, but faster.

## Features

The GPIO unit has the following features:

- Configurable up and down drive mode
- Support for rising edge, falling edge and double edge trigger

## API

Corresponding header file `gpiohs.h`

Provide the following interfaces

- gpiohs\_set\_drive\_mode

- gpiohs\_set\_pin

- gpiohs\_get\_pin

- gpiohs\_set\_pin\_edge

- gpiohs\_set\_irq

### gpiohs\_set\_drive\_mode

#### Description

Set GPIO drive mode.

#### Function prototype

```c
void gpiohs_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
```

#### Parameter

| Parameter name |   Description    | Input or output |
| :------------- | :--------------- | :-------------- |
| pin            | GPIO pin         | Input           |
| mode           | GPIO driver mode | Input           |

#### Return value

None.

### gpio\_set\_pin

#### Description

Set GPIO pin value.

#### Function prototype

```c
void gpiohs_set_pin(uint8_t pin, gpio_pin_value_t value)
```

#### Parameter

| Parameter name | Description | Input or output |
| :------------- | :---------- | :-------------- |
| pin            | GPIO pin    | Input           |
| value          | GPIO value  | Input           |

#### Return value

None.

### gpio\_get\_pin

#### Description

Get GPIO pin value.

#### Function prototype

```c
gpio_pin_value_t gpiohs_get_pin(uint8_t pin)
```

#### Parameter

| Parameter name | Description | Input or output |
| :------------- | :---------- | :-------------- |
| pin            | GPIO pin    | Input           |

#### Return value

The result of GPIO pin value.

### gpiohs\_set\_pin\_edge

#### Description

Set the high speed GPIO interrupt trigger mode.

#### Function prototype

```c
void gpiohs_set_pin_edge(uint8_t pin, gpio_pin_edge_t edge)
```

#### Parameter

| Parameter name |      Description       | Input or output |
| :------------- | :--------------------- | :-------------- |
| pin            | GPIO pin               | Input           |
| edge           | Interrupt trigger mode | Input           |

#### Return value

None.

### gpiohs\_set\_irq

#### Description

Set the interrupt callback function for high speed GPIO.

#### Function prototype

```c
void gpiohs_set_irq(uint8_t pin, uint32_t priority, void(*func)());
```

#### Parameter

| Parameter name |         Description         | Input or output |
| :------------- | :-------------------------- | :-------------- |
| pin            | GPIO pin                    | Input           |
| priority       | Interrupt priority          | Input           |
| func           | Interrupt callback function | Input           |

#### Return value

None.

### Example

```c
void irq_gpiohs2(void)
{
    printf("Hello world\n");
}
/* Set IO13 to high speed GPIO and set the output mode to high. */
fpioa_set_function(13, FUNC_GPIOHS3);
gpiohs_set_drive_mode(3, GPIO_DM_OUTPUT);
gpiohs_set_pin(3, GPIO_PV_High);
/* Set IO14 to high speed GPIO Input mode. Print Hello world when double edge triggers interrupt. */
plic_init();
fpioa_set_function(14, FUNC_GPIOHS2);
gpiohs_set_drive_mode(2, GPIO_DM_INPUT);
gpiohs_set_pin_edge(2, GPIO_PE_BOTH);
gpiohs_set_irq(2, 1, irq_gpiohs2);
sysctl_enable_irq();
```

## Data type

The relevant data types and data structures are defined as follows:

- gpio\_drive\_mode\_t: GPIO drive mode.

- gpio\_pin\_value\_t: GPIO value.

- gpio\_pin\_edge\_t: GPIO edge trigger mode.

### gpio\_drive\_mode\_t

#### Description

GPIO drive mode.

#### Type definition

```c
typedef enum _gpio_drive_mode
{
    GPIO_DM_INPUT,
    GPIO_DM_INPUT_PULL_DOWN,
    GPIO_DM_INPUT_PULL_UP,
    GPIO_DM_OUTPUT,
} gpio_drive_mode_t;
```

#### Enumeration element

|        Element name         |   Description   |
| --------------------------- | --------------- |
| GPIO\_DM\_INPUT             | Input           |
| GPIO\_DM\_INPUT\_PULL\_DOWN | Input pull down |
| GPIO\_DM\_INPUT\_PULL\_UP   | Input pull up   |
| GPIO\_DM\_OUTPUT            | Output          |

### gpio\_pin\_value\_t

#### Description

GPIO value.

#### Type definition

```c
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### Enumeration element

|  Element name  | Description |
| -------------- | ----------- |
| GPIO\_PV\_LOW  | Low         |
| GPIO\_PV\_HIGH | High        |

### gpio\_pin\_edge\_t

#### Description

GPIO edge trigger mode.

#### Type definition

```c
typedef enum _gpio_pin_edge
{
    GPIO_PE_NONE,
    GPIO_PE_FALLING,
    GPIO_PE_RISING,
    GPIO_PE_BOTH
} gpio_pin_edge_t;
```

#### Enumeration element

|   Element name    |     Description      |
| ----------------- | -------------------- |
| GPIO\_PE\_NONE    | Do not trigger       |
| GPIO\_PE\_FALLING | Falling edge trigger |
| GPIO\_PE\_RISING  | Rising edge trigger  |
| GPIO\_PE\_BOTH    | Double edge trigger  |
