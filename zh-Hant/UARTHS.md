# 高速通用非同步收發傳輸器 (UARTHS)

## 概述

嵌入式應用通常要求一個簡單的並且占用系統資源少的方法來傳輸資料。高速通用非同步收發傳輸器 (UARTHS) 即可以滿足這些要求，它能夠靈活地與外部裝置進行全雙工資料交換。
目前系統使用該串口做為調試串口，printf時會調用該串口輸出。

## 功能描述

UARTHS 模組具有以下功能：

- 配置 UARTHS 參數

- 自動收取資料到緩衝區

## API 參考

對應的頭文件 `uarths.h`

為用戶提供以下介面

- uarths\_init

- uarths\_config

- uarths\_receive\_data

- uarths\_send\_data

- uarths\_set\_irq

- uarths\_get\_interrupt\_mode

- uarths\_set\_interrupt\_cnt

### uarths\_init

#### 描述

初始化UARTHS，系統默認波特率為115200 8bit 1位停止位 無檢驗位。因為uarths時脈源為PLL0，在設置PLL0後需要重新調用該函數設置波特率，否則會列印亂碼。

#### 函數原型

```c
void uarths_init(void)
```

#### 參數

無。

#### 返回值

無。

### uarths\_config

#### 描述

設置UARTHS的參數。默認8bit資料，無校驗位。

#### 函數原型

```c
void uarths_config(uint32_t baud_rate, uarths_stopbit_t stopbit)
```

### 參數

| 參數名稱    |   描述       |  輸入輸出  |
| ---------- | ------------ | --------- |
| baud\_rate | 波特率        | 輸入      |
| stopbit    | 停止位        | 輸入      |

#### 返回值

無。

### uarths\_receive\_data

#### 描述

通過UARTHS讀取資料。

#### 函數原型

```c
size_t uarths_receive_data(uint8_t *buf, size_t buf_len)
```

#### 參數

| 參數名稱    |   描述           |  輸入輸出  |
| ---------- | ---------------  | --------- |
| buf        | 接收資料         | 輸出       |
| buf\_len   | 接收資料的長度    | 輸入       |

#### 返回值

已接收到的資料長度。

### uarths\_send\_data

#### 描述

通過UART發送資料。

#### 函數原型

```c
size_t uarths_send_data(const uint8_t *buf, size_t buf_len)
```

#### 參數

| 參數名稱    |   描述           |  輸入輸出  |
| ---------- | ---------------  | --------- |
| buf        | 待發送資料        | 輸入      |
| buf\_len   | 待發送資料的長度  | 輸入       |

#### 返回值

已發送資料的長度。

### uarths\_set\_irq

#### 描述

設置UARTHS中斷回調函數。

#### 函數原型

```c
void uarths_set_irq(uarths_interrupt_mode_t interrupt_mode, plic_irq_callback_t uarths_callback, void *ctx, uint32_t priority)
```

#### 參數

| 參數名稱                       |   描述           |  輸入輸出  |
| ----------------------------- | ---------------  | --------- |
| interrupt\_mode               | 中斷類型          | 輸入       |
| uarths\_callback              | 中斷回調函數      | 輸入      |
| ctx                           | 回調函數的參數    | 輸入       |
| priority                      | 中斷優先順序        | 輸入       |

#### 返回值

無。

### uarths\_get\_interrupt\_mode

#### 描述

獲取UARTHS的中斷類型。接收、發送或接收發送同時中斷。

#### 函數原型

```c
uarths_interrupt_mode_t uarths_get_interrupt_mode(void)
```

#### 參數

無

#### 返回值

當前中斷的類型。

### uarths\_set\_interrupt\_cnt

#### 描述

設置UARTHS中斷時的FIFO深度。
當中斷類型為UARTHS\_SEND\_RECEIVE，發送接收FIFO中斷深度均為cnt;

#### 函數原型

```c
void uarths_set_interrupt_cnt(uarths_interrupt_mode_t interrupt_mode, uint8_t cnt)
```

#### 參數

| 參數名稱                       |   描述           |  輸入輸出  |
| ----------------------------- | ---------------  | --------- |
| interrupt\_mode               | 中斷類型         | 輸入       |
| cnt                           | FIFO深度         | 輸入      |

#### 返回值

無。

### 舉例

```c
/* 設置接收中斷 中斷FIFO深度為0，即接收到資料立即中斷並讀取接收到的資料。*/
    int uarths_irq(void *ctx)
    {
        if(!uarths_receive_data((uint8_t *)&receive_char, 1))
            printf("Uarths receive ERR!\n");
        return 0;
    }

    plic_init();
    uarths_set_interrupt_cnt(UARTHS_RECEIVE , 0);
    uarths_set_irq(UARTHS_RECEIVE ,uarths_irq, NULL, 4);
    sysctl_enable_irq();
```

## 資料類型

相關資料類型、資料結構定義如下：

- uarths\_interrupt\_mode\_t：中斷類型。
- uarths\_stopbit\_t：停止位。

### uarths\_interrupt\_mode\_t

### 描述

UARTHS中斷類型。

#### 定義

```c
typedef enum _uarths_interrupt_mode
{
    UARTHS_SEND = 1,
    UARTHS_RECEIVE = 2,
    UARTHS_SEND_RECEIVE = 3,
} uarths_interrupt_mode_t;
```

#### 成員

| 成員名稱              | 描述         |
| -------------------- | ------------ |
| UARTHS_SEND          | 發送中斷      |
| UARTHS_RECEIVE       | 接收中斷      |
| UARTHS\_SEND\_RECEIVE  | 發送接收中斷  |

### uarths\_stopbit\_t

#### 描述：

UARTHS停止位。

#### 定義

```c
typedef enum _uarths_stopbit
{
    UART_STOP_1,
    UART_STOP_2
} uarths_stopbit_t;
```

#### 成員

| 成員名稱              | 描述         |
| -------------------- | ------------ |
| UART\_STOP\_1        | 1位停止位     |
| UART\_STOP\_2        | 2位停止位     |