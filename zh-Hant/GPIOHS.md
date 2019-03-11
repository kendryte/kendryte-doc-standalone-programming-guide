# 通用高速輸入/輸出 (GPIOHS)

## 概述

晶片有32個高速GPIO。與普通GPIO相似，腳位反轉能力更強。

## 功能描述

GPIOHS模組具有以下功能：

- 可配置上下拉驅動模式
- 支持正緣、負緣和雙緣觸發

## API 參考

對應的頭文件 `gpiohs.h`

為用戶提供以下介面

- gpiohs\_set\_drive\_mode

- gpiohs\_set\_pin

- gpiohs\_get\_pin

- gpiohs\_set\_pin\_edge

- gpiohs\_set\_irq  (0.6.0後不再支持，請使用gpiohs\_irq\_register)

- gpiohs\_irq\_register

- gpiohs\_irq\_unregister

### gpiohs\_set\_drive\_mode

#### 描述

設置GPIO驅動模式。

#### 函數原型

```c
void gpiohs_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
```

#### 參數

| 參數名稱       | 描述           | 輸入輸出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO腳位       | 輸入      |
| mode          | GPIO驅動模式    | 輸入      |

#### 返回值

無。

### gpio\_set\_pin

#### 描述

設置GPIO腳位值。

#### 函數原型

```c
void gpiohs_set_pin(uint8_t pin, gpio_pin_value_t value)
```

#### 參數

| 參數名稱       | 描述           | 輸入輸出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO腳位       | 輸入      |
| value         | GPIO值         | 輸入      |

#### 返回值

無。

### gpio\_get\_pin

#### 描述

獲取GPIO腳位值。

#### 函數原型

```c
gpio_pin_value_t gpiohs_get_pin(uint8_t pin)
```

#### 參數

| 參數名稱       | 描述           | 輸入輸出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO腳位       | 輸入       |

#### 返回值

獲取的GPIO腳位值。

### gpiohs\_set\_pin\_edge

#### 描述

設置高速GPIO中斷觸發模式。

#### 函數原型

```c
void gpiohs_set_pin_edge(uint8_t pin, gpio_pin_edge_t edge)
```

#### 參數

| 參數名稱       | 描述           | 輸入輸出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO腳位       | 輸入       |
| edge          | 中斷觸發方式    | 輸入      |

#### 返回值

無。

### gpiohs\_set\_irq

#### 描述

設置高速GPIO的中斷回調函數。

#### 函數原型

```c
void gpiohs_set_irq(uint8_t pin, uint32_t priority, void(*func)());
```

#### 參數

| 參數名稱       | 描述           | 輸入輸出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO腳位       | 輸入       |
| priority      | 中斷優先順序      | 輸入      |
| func          | 中斷回調函數    | 輸入       |

#### 返回值

無。

### gpiohs\_irq\_register

#### 描述

設置高速GPIO的中斷回調函數。

#### 函數原型

```c
void gpiohs_irq_register(uint8_t pin, uint32_t priority, plic_irq_callback_t callback, void *ctx)
```

#### 參數

| 參數名稱                  | 描述           | 輸入輸出   |
| :----------------------- | :------------- | :-------- |
| pin                      | GPIO腳位       | 輸入       |
| priority                 | 中斷優先順序      | 輸入       |
| plic\_irq\_callback\_t   | 中斷回調函數    | 輸入       |
| ctx                      | 回調函數參數    | 輸入       |

#### 返回值

無。

### gpiohs\_irq\_unregister

#### 描述

註銷GPIOHS中斷。

### 函數原型

```c
void gpiohs_irq_unregister(uint8_t pin)
```

#### 參數

| 參數名稱                  | 描述           | 輸入輸出   |
| :----------------------- | :------------- | :-------- |
| pin                      | GPIO腳位       | 輸入       |

#### 返回值

無。

### 舉例

```c
void irq_gpiohs2(void *ctx)
{
    printf("Hello world\n");
}
/* 設置IO13為高速GPIO，輸出模式並置為高 */
fpioa_set_function(13, FUNC_GPIOHS3);
gpiohs_set_drive_mode(3, GPIO_DM_OUTPUT);
gpiohs_set_pin(3, GPIO_PV_High);
/* 設置IO14為高速GPIO 輸入模式 雙緣觸發中斷時列印Hello world */
plic_init();
fpioa_set_function(14, FUNC_GPIOHS2);
gpiohs_set_drive_mode(2, GPIO_DM_INPUT);
gpiohs_set_pin_edge(2, GPIO_PE_BOTH);
gpiohs_irq_register(2, 1, irq_gpiohs2, NULL);
sysctl_enable_irq();
```

## 資料類型

相關資料類型、資料結構定義如下：

- gpio\_drive\_mode\_t：GPIO驅動模式。

- gpio\_pin\_value\_t：GPIO值。

- gpio\_pin\_edge\_t：GPIO邊緣觸發模式。

### gpio\_drive\_mode\_t

#### 描述

GPIO驅動模式。

#### 定義

```c
typedef enum _gpio_drive_mode
{
    GPIO_DM_INPUT,
    GPIO_DM_INPUT_PULL_DOWN,
    GPIO_DM_INPUT_PULL_UP,
    GPIO_DM_OUTPUT,
} gpio_drive_mode_t;
```

#### 成員

| 成員名稱                     | 描述        |
| --------------------------- | ----------- |
| GPIO\_DM\_INPUT             | 輸入        |
| GPIO\_DM\_INPUT\_PULL\_DOWN | 輸入下拉     |
| GPIO\_DM\_INPUT\_PULL\_UP   | 輸入上拉     |
| GPIO\_DM\_OUTPUT            | 輸出        |

### gpio\_pin\_value\_t

#### 描述

GPIO 值。

#### 定義

```c
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| GPIO\_PV\_LOW      | 低          |
| GPIO\_PV\_HIGH     | 高          |

### gpio\_pin\_edge\_t

#### 描述

高速GPIO邊緣觸發模式。

#### 定義

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

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| GPIO\_PE\_NONE     | 不觸發      |
| GPIO\_PE\_FALLING  | 負緣觸發  |
| GPIO\_PE\_RISING   | 正緣觸發  |
| GPIO\_PE\_BOTH     | 雙緣觸發    |
| GPIO\_PE\_LOW      | 低電平觸發  |
| GPIO\_PE\_HIGH     | 高電平觸發  |
