# 通用輸入/輸出 (GPIO)

## 概述

晶片有8個通用GPIO。

## 功能描述

GPIO 模組具有以下功能：

- 可配置上下拉驅動模式

## API 參考

對應的頭文件 `gpio.h`

為用戶提供以下介面

- gpio\_init

- gpio\_set\_drive\_mode

- gpio\_set\_pin

- gpio\_get\_pin

### gpio\_init

#### 描述

初始化GPIO。

#### 函數原型

```c
int gpio_init(void)
```

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### gpio\_set\_drive\_mode

#### 描述

設置GPIO驅動模式。

#### 函數原型

```c
void gpio_set_drive_mode(uint8_t pin, gpio_drive_mode_t mode)
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
void gpio_set_pin(uint8_t pin, gpio_pin_value_t value)
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
gpio_pin_value_t gpio_get_pin(uint8_t pin)
```

#### 參數

| 參數名稱       | 描述           | 輸入輸出   |
| :------------ | :------------- | :-------- |
| pin           | GPIO腳位       | 輸入      |

#### 返回值

獲取的GPIO腳位值。

### 舉例

```c
/* 設置IO13為輸出並置為高 */
gpio_init();
fpioa_set_function(13, FUNC_GPIO3);
gpio_set_drive_mode(3, GPIO_DM_OUTPUT);
gpio_set_pin(3, GPIO_PV_High);
```

## 資料類型

相關資料類型、資料結構定義如下：

- gpio\_drive\_mode\_t：GPIO驅動模式。

- gpio\_pin\_value\_t：GPIO值。

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