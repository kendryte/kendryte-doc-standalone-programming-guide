# 通用非同步收發傳輸器 (UART)

## 概述

嵌入式應用通常要求一個簡單的並且占用系統資源少的方法來傳輸資料。通用非同步收發傳輸器 (UART) 即可以滿足這些要求，它能夠靈活地與外部裝置進行全雙工資料交換。

## 功能描述

UART 模組具有以下功能：

- 配置 UART 參數

- 自動收取資料到緩衝區

## API 參考

對應的頭文件 `uart.h`

為用戶提供以下介面

- uart\_init

- uart\_config  (0.6.0後不再支持，請使用uart\_configure)

- uart\_configure

- uart\_send\_data

- uart\_send\_data\_dma

- uart\_send\_data\_dma\_irq

- uart\_receive\_data

- uart\_receive\_data\_dma

- uart\_receive\_data\_dma\_irq

- uart\_irq\_register

- uart\_irq\_deregister

### uart\_init

#### 描述

初始化uart。

#### 函數原型

```c
void uart_init(uart_device_number_t channel)
```

#### 參數

| 參數名稱     | 描述       | 輸入輸出   |
| :-----------| :----------| :-------- |
| channel     | UART號     | 輸入       |

#### 返回值

無。

### uart\_configure

#### 描述

設置UART相關參數。該函數已廢棄，替代函數為uart_configure。

### uart\_configure

#### 描述

設置UART相關參數。

#### 函數原型

```c
void uart_configure(uart_device_number_t channel, uint32_t baud_rate, uart_bitwidth_t data_width, uart_stopbit_t stopbit, uart_parity_t parity)
```

#### 參數

| 參數名稱    |   描述       |  輸入輸出  |
| ---------- | ------------ | --------- |
| channel    | UART 編號     | 輸入      |
| baud\_rate | 波特率        | 輸入      |
| data_width | 資料位 (5-8)  | 輸入      |
| stopbit   | 停止位        | 輸入      |
| parity     | 校驗位        | 輸入      |

#### 返回值

無。

### uart\_send\_data

#### 描述

通過UART發送資料。

#### 函數原型

```c
int uart_send_data(uart_device_number_t channel, const char *buffer, size_t buf_len)
```

#### 參數

| 參數名稱    |   描述           |  輸入輸出  |
| ---------- | ---------------  | --------- |
| channel    | UART 編號        | 輸入       |
| buffer     | 待發送資料        | 輸入      |
| buf\_len    | 待發送資料的長度  | 輸入       |

#### 返回值

已發送資料的長度。

### uart\_send\_data\_dma

#### 描述

UART通過DMA發送資料。資料全部發送完畢後返回。

#### 函數原型

```c
void uart_send_data_dma(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, const uint8_t *buffer, size_t buf_len)
```

#### 參數

| 參數名稱          |   描述           |  輸入輸出  |
| ---------------- | ---------------  | --------- |
| uart\_channel    | UART 編號        | 輸入       |
| dmac\_channel    | DMA通道          | 輸入       |
| buffer           | 待發送資料        | 輸入       |
| buf\_len         | 待發送資料的長度  | 輸入       |

#### 返回值

無。

### uart\_send\_data\_dma\_irq

#### 描述

UART通過DMA發送資料，並設置DMA發送完成中斷函數，僅單次中斷。

#### 函數原型

```c
void uart_send_data_dma_irq(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel,
                            const uint8_t *buffer, size_t buf_len, plic_irq_callback_t uart_callback,
                            void *ctx, uint32_t priority)
```

#### 參數

| 參數名稱          |   描述           |  輸入輸出  |
| ---------------- | ---------------  | --------- |
| uart\_channel    | UART 編號        | 輸入       |
| dmac\_channel    | DMA通道          | 輸入       |
| buffer           | 待發送資料        | 輸入       |
| buf\_len         | 待發送資料的長度  | 輸入       |
| uart\_callback   | DMA中斷回調      | 輸入       |
| ctx              | 中斷函數參數      | 輸入       |
| priority         | 中斷優先順序        | 輸入       |

#### 返回值

無。

### uart\_receive\_data

#### 描述

通過UART讀取資料。

#### 函數原型

```c
int uart_receive_data(uart_device_number_t channel, char *buffer, size_t buf_len);
```

#### 參數

| 參數名稱    |   描述           |  輸入輸出  |
| ---------- | ---------------  | --------- |
| channel    | UART 編號        | 輸入       |
| buffer     | 接收資料         | 輸出       |
| buf\_len    | 接收資料的長度    | 輸入       |

#### 返回值

已接收到的資料長度。

### uart\_receive\_data\_dma

#### 描述

UART通過DMA接收資料。

#### 函數原型

```c
void uart_receive_data_dma(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel, uint8_t *buffer, size_t buf_len)
```

#### 參數

| 參數名稱          |   描述           |  輸入輸出  |
| ---------------- | ---------------  | --------- |
| uart\_channel    | UART 編號        | 輸入       |
| dmac\_channel    | DMA通道          | 輸入       |
| buffer           | 接收資料         | 輸出       |
| buf\_len         | 接收資料的長度    | 輸入       |

#### 返回值

無。

### uart\_receive\_data\_dma\_irq

#### 描述

UART通過DMA接收資料，並註冊DMA接收完成中斷函數，僅單次中斷。

#### 函數原型

```c
void uart_receive_data_dma_irq(uart_device_number_t uart_channel, dmac_channel_number_t dmac_channel,
                                     uint8_t *buffer, size_t buf_len, plic_irq_callback_t uart_callback,
                                     void *ctx, uint32_t priority)
```

#### 參數

| 參數名稱          |   描述           |  輸入輸出  |
| ---------------- | ---------------  | --------- |
| uart\_channel    | UART 編號        | 輸入       |
| dmac\_channel    | DMA通道          | 輸入       |
| buffer           | 接收資料         | 輸出       |
| buf\_len         | 接收資料的長度    | 輸入       |
| uart\_callback   | DMA中斷回調      | 輸入       |
| ctx              | 中斷函數參數      | 輸入       |
| priority         | 中斷優先順序        | 輸入       |

#### 返回值

無。

### uart\_irq\_register

#### 描述

註冊UART中斷函數。

#### 函數原型

```c
void uart_irq_register(uart_device_number_t channel, uart_interrupt_mode_t interrupt_mode, plic_irq_callback_t uart_callback, void *ctx, uint32_t priority)
```

#### 參數

| 參數名稱          |   描述           |  輸入輸出  |
| ---------------- | ---------------  | --------- |
| channel          | UART 編號        | 輸入       |
| interrupt\_mode  | 中斷類型          | 輸入       |
| uart\_callback   | 中斷回調          | 輸入       |
| ctx              | 中斷函數參數      | 輸入       |
| priority         | 中斷優先順序        | 輸入       |

#### 返回值

無。

### uart\_irq\_deregister

#### 描述

註銷UART中斷函數。

#### 函數原型

```c
void uart_irq_deregister(uart_device_number_t channel, uart_interrupt_mode_t interrupt_mode)
```

#### 參數

| 參數名稱          |   描述           |  輸入輸出  |
| ---------------- | ---------------  | --------- |
| channel          | UART 編號        | 輸入       |
| interrupt\_mode  | 中斷類型          | 輸入       |

#### 返回值

無。

### 舉例

```c
/* UART1 波特率115200, 8位資料， 1位停止位，無校驗位 */
uart_init(UART_DEVICE_1);
uart_config(UART_DEVICE_1, 115200, UART_BITWIDTH_8BIT, UART_STOP_1, UART_PARITY_NONE);
char *v_hel = {"hello world!\n"};
/* 發送 hello world! */
uart_send_data(UART_DEVICE_1, hel, strlen(v_hel));
/* 接收資料 */
while(uart_receive_data(UART_DEVICE_1, &recv, 1))
{
    printf("%c ", recv);
}
```

## 資料類型

相關資料類型、資料結構定義如下：

- uart\_device\_number\_t：UART 編號。
- uart\_bitwidth\_t：UART 資料位寬。
- uart\_stopbits\_t：UART 停止位。
- uart\_parity\_t：UART 校驗位。
- uart\_interrupt\_mode\_t：UART中斷類型，接收或發送。
- uart\_send\_trigger\_t：發送中斷或DMA觸發FIFO深度。
- uart\_receive\_trigger\_t：接收中斷或DMA觸發FIFO深度。

### uart\_device\_number\_t

#### 描述

UART編號。

#### 定義

```c
typedef enum _uart_device_number
{
    UART_DEVICE_1,
    UART_DEVICE_2,
    UART_DEVICE_3,
    UART_DEVICE_MAX,
} uart_device_number_t;
```

#### 成員

| 成員名稱          | 描述        |
| ---------------- | ----------- |
| UART\_DEVICE\_1  | UART 1      |
| UART\_DEVICE\_2  | UART 2      |
| UART\_DEVICE\_3  | UART 3      |

### uart\_bitwidth\_t

#### 描述

UART資料位寬。

#### 定義

```c
typedef enum _uart_bitwidth
{
    UART_BITWIDTH_5BIT = 0,
    UART_BITWIDTH_6BIT,
    UART_BITWIDTH_7BIT,
    UART_BITWIDTH_8BIT,
} uart_bitwidth_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| UART_BITWIDTH_5BIT | 5比特        |
| UART_BITWIDTH_6BIT | 6比特        |
| UART_BITWIDTH_7BIT | 7比特        |
| UART_BITWIDTH_8BIT | 8比特        |

### uart\_stopbits\_t

#### 描述

UART 停止位。

#### 定義

```c
typedef enum _uart_stopbits
{
    UART_STOP_1,
    UART_STOP_1_5,
    UART_STOP_2
} uart_stopbits_t;  
```

#### 成員

| 成員名稱          | 描述        |
| ---------------- | ----------- |
| UART\_STOP\_1    | 1 個停止位   |
| UART\_STOP\_1\_5 | 1.5 個停止位 |
| UART\_STOP\_2    | 2 個停止位   |

### uart\_parity\_t

#### 描述

UART 校驗位。

#### 定義

```c
typedef enum _uart_parity
{
    UART_PARITY_NONE,
    UART_PARITY_ODD,
    UART_PARITY_EVEN
} uart_parity_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| UART\_PARITY\_NONE | 無校驗位    |
| UART\_PARITY\_ODD  | 奇校驗      |
| UART\_PARITY\_EVEN | 偶校驗      |

### uart\_interrupt\_mode\_t

#### 描述

UART中斷類型，接收或發送。

#### 定義

```c
typedef enum _uart_interrupt_mode
{
    UART_SEND = 1,
    UART_RECEIVE = 2,
} uart_interrupt_mode_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| UART\_SEND          | UART 發送   |
| UART\_RECEIVE       | UART 接收   |

### uart\_send\_trigger\_t

#### 描述

發送中斷或DMA觸發FIFO深度。當FIFO中的資料小於等於該值時觸發中斷或DMA傳輸。FIFO的深度為16位元組。

#### 定義

```c
typedef enum _uart_send_trigger
{
    UART_SEND_FIFO_0,
    UART_SEND_FIFO_2,
    UART_SEND_FIFO_4,
    UART_SEND_FIFO_8,
} uart_send_trigger_t;
```

#### 成員

| 成員名稱               | 描述          |
| --------------------- | ------------- |
| UART\_SEND\_FIFO\_0   | FIFO為空      |
| UART\_SEND\_FIFO\_2   | FIFO剩餘2位元組  |
| UART\_SEND\_FIFO\_4   | FIFO剩餘4位元組  |
| UART\_SEND\_FIFO\_8   | FIFO剩餘8位元組  |

### uart\_receive\_trigger\_t

#### 描述

接收中斷或DMA觸發FIFO深度。當FIFO中的資料大於等於該值時觸發中斷或DMA傳輸。FIFO的深度為16位元組。

#### 定義

```c
typedef enum _uart_receive_trigger
{
    UART_RECEIVE_FIFO_1,
    UART_RECEIVE_FIFO_4,
    UART_RECEIVE_FIFO_8,
    UART_RECEIVE_FIFO_14,
} uart_receive_trigger_t;
```

#### 成員

| 成員名稱                  | 描述          |
| ------------------------ | ------------- |
| UART\_RECEIVE\_FIFO\_1   | FIFO剩餘1位元組  |
| UART\_RECEIVE\_FIFO\_4   | FIFO剩餘2位元組  |
| UART\_RECEIVE\_FIFO\_8   | FIFO剩餘4位元組  |
| UART\_RECEIVE\_FIFO\_14  | FIFO剩餘8位元組  |
