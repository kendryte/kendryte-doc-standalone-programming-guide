# 通用输入/Output (GPIO)

## Overview

芯片有8个通用GPIO。

## Features

GPIO 模块具有以下功能：

- 可配置上下拉驱动模式

## API

Corresponding header file `gpio.h`

Provide the following interfaces

- gpio\_init

- gpio\_set\_drive\_mode

- gpio\_set\_pin

- gpio\_get\_pin

### gpio\_init

#### Description

初始化GPIO。

#### Function prototype

```c
int gpio_init(void)
```

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | Success |
| 非0   | Fail |

### gpio\_set\_drive\_mode

#### Description

设置GPIO驱动模式。

#### Function prototype

```c
void gpio_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
```

#### Parameter

| Parameter name       | Description           | Input or output   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | Input      |
| mode          | GPIO驱动模式    | Input      |

#### Return value

None.

### gpio\_set\_pin

#### Description

设置GPIO管脚值。

#### Function prototype

```c
void gpio_set_pin(uint8_t pin, gpio_pin_value_t value)
```

#### Parameter

| Parameter name       | Description           | Input or output   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | Input      |
| value         | GPIO值         | Input      |

#### Return value

None.

### gpio\_get\_pin

#### Description

获取GPIO管脚值。

#### Function prototype

```c
gpio_pin_value_t gpio_get_pin(uint8_t pin)
```

#### Parameter

| Parameter name       | Description           | Input or output   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | Input      |

#### Return value

获取的GPIO管脚值。

### Example

```c
/* 设置IO13为Output并置为高 */
gpio_init();
fpioa_set_function(13, FUNC_GPIO3);
gpio_set_drive_mode(3, GPIO_DM_OUTPUT);
gpio_set_pin(3, GPIO_PV_High);
```

## Data type

The relevant data types and data structures are defined as follows:

- gpio\_drive\_mode\_t：GPIO驱动模式。

- gpio\_pin\_value\_t：GPIO值。

### gpio\_drive\_mode\_t

#### Description

GPIO驱动模式。

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

| Element name                     | Description        |
| --------------------------- | ----------- |
| GPIO\_DM\_INPUT             | Input        |
| GPIO\_DM\_INPUT\_PULL\_DOWN | Input下拉     |
| GPIO\_DM\_INPUT\_PULL\_UP   | Input上拉     |
| GPIO\_DM\_OUTPUT            | Output        |

### gpio\_pin\_value\_t

#### Description

GPIO 值。

#### Type definition

```c
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| GPIO\_PV\_LOW      | 低          |
| GPIO\_PV\_HIGH     | 高          |