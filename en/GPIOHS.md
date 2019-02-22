# 通用高速输入/Output (GPIOHS)

## Summary

芯片有32个高速GPIO。与普通GPIO相似，管脚反转能力更强。

## Features

GPIOHS模块具有以下功能：

- 可配置上下拉驱动模式
- 支持上升沿、下降沿和双沿触发

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

设置GPIO驱动模式。

#### Function prototype

```c
void gpiohs_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
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
void gpiohs_set_pin(uint8_t pin, gpio_pin_value_t value)
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
gpio_pin_value_t gpiohs_get_pin(uint8_t pin)
```

#### Parameter

| Parameter name       | Description           | Input or output   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | Input       |

#### Return value

获取的GPIO管脚值。

### gpiohs\_set\_pin\_edge

#### Description

设置高速GPIO中断触发模式。

#### Function prototype

```c
void gpiohs_set_pin_edge(uint8_t pin, gpio_pin_edge_t edge)
```

#### Parameter

| Parameter name       | Description           | Input or output   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | Input       |
| edge          | 中断触发方式    | Input      |

#### Return value

None.

### gpiohs\_set\_irq

#### Description

设置高速GPIO的中断回调函数。

#### Function prototype

```c
void gpiohs_set_irq(uint8_t pin, uint32_t priority, void(*func)());
```

#### Parameter

| Parameter name       | Description           | Input or output   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | Input       |
| priority      | 中断优先级      | Input      |
| func          | 中断回调函数    | Input       |

#### Return value

None.

### Example

```c
void irq_gpiohs2(void)
{
    printf("Hello world\n");
}
/* 设置IO13为高速GPIO，Output模式并置为高 */
fpioa_set_function(13, FUNC_GPIOHS3);
gpiohs_set_drive_mode(3, GPIO_DM_OUTPUT);
gpiohs_set_pin(3, GPIO_PV_High);
/* 设置IO14为高速GPIO Input模式 双沿触发中断时打印Hello world */
plic_init();
fpioa_set_function(14, FUNC_GPIOHS2);
gpiohs_set_drive_mode(2, GPIO_DM_INPUT);
gpiohs_set_pin_edge(2, GPIO_PE_BOTH);
gpiohs_set_irq(2, 1, irq_gpiohs2);
sysctl_enable_irq();
```

## Data type

相关数据类型、数据结构定义如下：

- gpio\_drive\_mode\_t：GPIO驱动模式。

- gpio\_pin\_value\_t：GPIO值。

- gpio\_pin\_edge\_t：GPIO边沿触发模式。

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

### gpio\_pin\_edge\_t

#### Description

高速GPIO边沿触发模式。

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

| Element name            | Description        |
| ------------------ | ----------- |
| GPIO\_PE\_NONE     | 不触发      |
| GPIO\_PE\_FALLING  | 下降沿触发  |
| GPIO\_PE\_RISING   | 上升沿触发  |
| GPIO\_PE\_BOTH     | 双沿触发    |
