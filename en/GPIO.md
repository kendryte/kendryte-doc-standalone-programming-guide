# GPIO

## Overview

GPIO stands for General Purpose Input Output.
The chip has 8 general purpose GPIOs.

## Features

The GPIO unit has the following features:

- Configurable up and down drive mode

## API

Corresponding header file `gpio.h`

Provide the following interfaces

- gpio\_init

- gpio\_set\_drive\_mode

- gpio\_set\_pin

- gpio\_get\_pin

### gpio\_init

#### Description

Initialize GPIO.

#### Function prototype

```c
int gpio_init(void)
```

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### gpio\_set\_drive\_mode

#### Description

Set GPIO drive mode.

#### Function prototype

```c
void gpio_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
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
void gpio_set_pin(uint8_t pin, gpio_pin_value_t value)
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
gpio_pin_value_t gpio_get_pin(uint8_t pin)
```

#### Parameter

| Parameter name | Description | Input or output |
| :------------- | :---------- | :-------------- |
| pin            | GPIO pin    | Input           |

#### Return value

The result of GPIO pin value.

### Example

```c
/* Set IO13 to Output and set it high */
gpio_init();
fpioa_set_function(13, FUNC_GPIO3);
gpio_set_drive_mode(3, GPIO_DM_OUTPUT);
gpio_set_pin(3, GPIO_PV_High);
```

## Data type

The relevant data types and data structures are defined as follows:

- gpio\_drive\_mode\_t: GPIO drive mode.

- gpio\_pin\_value\_t: GPIO value.

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