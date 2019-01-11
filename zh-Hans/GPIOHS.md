# 通用高速输入/输出 (GPIOHS)

## 概述

芯片有32个高速GPIO。与普通GPIO相似，管脚反转能力更强。

## 功能描述

GPIOHS模块具有以下功能：

- 可配置上下拉驱动模式
- 支持上升沿、下降沿和双沿触发

## API 参考

对应的头文件 `gpiohs.h`

为用户提供以下接口

- gpiohs\_set\_drive\_mode

- gpiohs\_set\_pin

- gpiohs\_get\_pin

- gpiohs\_set\_pin\_edge

- gpiohs\_set\_irq  (0.6.0后不再支持，请使用gpiohs\_irq\_register)

- gpiohs\_irq\_register

- gpiohs\_irq\_unregister

### gpiohs\_set\_drive\_mode

#### 描述

设置GPIO驱动模式。

#### 函数原型

```c
void gpiohs_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
```

#### 参数

| 参数名称       | 描述           | 输入输出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | 输入      |
| mode          | GPIO驱动模式    | 输入      |

#### 返回值

无。

### gpio\_set\_pin

#### 描述

设置GPIO管脚值。

#### 函数原型

```c
void gpiohs_set_pin(uint8_t pin, gpio_pin_value_t value)
```

#### 参数

| 参数名称       | 描述           | 输入输出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | 输入      |
| value         | GPIO值         | 输入      |

#### 返回值

无。

### gpio\_get\_pin

#### 描述

获取GPIO管脚值。

#### 函数原型

```c
gpio_pin_value_t gpiohs_get_pin(uint8_t pin)
```

#### 参数

| 参数名称       | 描述           | 输入输出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | 输入       |

#### 返回值

获取的GPIO管脚值。

### gpiohs\_set\_pin\_edge

#### 描述

设置高速GPIO中断触发模式。

#### 函数原型

```c
void gpiohs_set_pin_edge(uint8_t pin, gpio_pin_edge_t edge)
```

#### 参数

| 参数名称       | 描述           | 输入输出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | 输入       |
| edge          | 中断触发方式    | 输入      |

#### 返回值

无。

### gpiohs\_set\_irq

#### 描述

设置高速GPIO的中断回调函数。

#### 函数原型

```c
void gpiohs_set_irq(uint8_t pin, uint32_t priority, void(*func)());
```

#### 参数

| 参数名称       | 描述           | 输入输出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO管脚       | 输入       |
| priority      | 中断优先级      | 输入      |
| func          | 中断回调函数    | 输入       |

#### 返回值

无。

### gpiohs\_irq\_register

#### 描述

设置高速GPIO的中断回调函数。

#### 函数原型

```c
void gpiohs_irq_register(uint8_t pin, uint32_t priority, plic_irq_callback_t callback, void *ctx)
```

#### 参数

| 参数名称                  | 描述           | 输入输出   |
| :----------------------- | :------------- | :-------- |
| pin                      | GPIO管脚       | 输入       |
| priority                 | 中断优先级      | 输入       |
| plic\_irq\_callback\_t   | 中断回调函数    | 输入       |
| ctx                      | 回调函数参数    | 输入       |

#### 返回值

无。

### gpiohs\_irq\_unregister

#### 描述

注销GPIOHS中断。

### 函数原型

```c
void gpiohs_irq_unregister(uint8_t pin)
```

#### 参数

| 参数名称                  | 描述           | 输入输出   |
| :----------------------- | :------------- | :-------- |
| pin                      | GPIO管脚       | 输入       |

#### 返回值

无。

### 举例

```c
void irq_gpiohs2(void *ctx)
{
    printf("Hello world\n");
}
/* 设置IO13为高速GPIO，输出模式并置为高 */
fpioa_set_function(13, FUNC_GPIOHS3);
gpiohs_set_drive_mode(3, GPIO_DM_OUTPUT);
gpiohs_set_pin(3, GPIO_PV_High);
/* 设置IO14为高速GPIO 输入模式 双沿触发中断时打印Hello world */
plic_init();
fpioa_set_function(14, FUNC_GPIOHS2);
gpiohs_set_drive_mode(2, GPIO_DM_INPUT);
gpiohs_set_pin_edge(2, GPIO_PE_BOTH);
gpiohs_irq_register(2, 1, irq_gpiohs2, NULL);
sysctl_enable_irq();
```

## 数据类型

相关数据类型、数据结构定义如下：

- gpio\_drive\_mode\_t：GPIO驱动模式。

- gpio\_pin\_value\_t：GPIO值。

- gpio\_pin\_edge\_t：GPIO边沿触发模式。

### gpio\_drive\_mode\_t

#### 描述

GPIO驱动模式。

#### 定义

```c
typedef enum _gpio_drive_mode
{
    GPIO_DM_INPUT,
    GPIO_DM_INPUT_PULL_DOWN,
    GPIO_DM_INPUT_PULL_UP,
    GPIO_DM_OUTPUT,
} gpio_drive_mode_t;
```

#### 成员

| 成员名称                     | 描述        |
| --------------------------- | ----------- |
| GPIO\_DM\_INPUT             | 输入        |
| GPIO\_DM\_INPUT\_PULL\_DOWN | 输入下拉     |
| GPIO\_DM\_INPUT\_PULL\_UP   | 输入上拉     |
| GPIO\_DM\_OUTPUT            | 输出        |

### gpio\_pin\_value\_t

#### 描述

GPIO 值。

#### 定义

```c
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| GPIO\_PV\_LOW      | 低          |
| GPIO\_PV\_HIGH     | 高          |

### gpio\_pin\_edge\_t

#### 描述

高速GPIO边沿触发模式。

#### 定义

```c
typedef enum _gpio_pin_edge
{
    GPIO_PE_NONE,
    GPIO_PE_FALLING,
    GPIO_PE_RISING,
    GPIO_PE_BOTH,
    GPIO_PE_LOW,
    GPIO_PE_HIGH = 8,
} gpio_pin_edge_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| GPIO\_PE\_NONE     | 不触发      |
| GPIO\_PE\_FALLING  | 下降沿触发  |
| GPIO\_PE\_RISING   | 上升沿触发  |
| GPIO\_PE\_BOTH     | 双沿触发    |
| GPIO\_PE\_LOW      | 低电平触发  |
| GPIO\_PE\_HIGH     | 高电平触发  |
