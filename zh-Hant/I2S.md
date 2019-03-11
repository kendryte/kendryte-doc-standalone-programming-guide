# 集成電路內置音頻匯流排 (I2S)

## 概述

I2S 標準匯流排定義了三種信號：時脈信號 BCK、聲道選擇信號 WS 和串列資料信號 SD。一個基本的I2S 資料匯流排有一個主機和一個從機。主機和從機的角色在通信過程中保持不變。I2S 模組包含獨立的發送和接收聲道，能夠保證優良的通信性能。

## 功能描述

I2S 模組具有以下功能：

- 根據音頻格式自動配置裝置（支持 16、24、32 位深，44100 採樣率，1 - 4 聲道）
- 可配置為播放或錄音模式
- 自動管理音頻緩衝區

## API 參考

對應的頭文件 `i2s.h`

為用戶提供以下介面

- i2s\_init
- i2s\_send\_data\_dma
- i2s\_recv\_data\_dma
- i2s\_rx\_channel\_config
- i2s\_tx\_channel\_config
- i2s\_play
- i2s\_set\_sample\_rate：I2S 設置採樣率。
- i2s\_set\_dma\_divide\_16：設置dma_divide_16，16位資料時設置dma_divide_16，DMA傳輸時自動將32比特INT32資料分成兩個16比特的左右聲道資料。
- i2s\_get\_dma\_divide\_16：獲取dma_divide_16值。用於判斷是否需要設置dma_divide_16。

### i2s\_init

#### 描述

初始化I2S。

#### 函數原型

```c
void i2s_init(i2s_device_number_t device_num, i2s_transmit_t rxtx_mode, uint32_t channel_mask)
```

#### 參數

| 成員名稱            | 描述         |  輸入輸出  |
| ------------------ | ------------ | --------- |
| device\_num         | I2S號        | 輸入      |
| rxtx\_mode          | 接收或發送模式| 輸入      |
| channel\_mask       | 通道掩碼      | 輸入      |

#### 返回值

無。

### i2s\_send\_data\_dma

#### 描述

I2S發送資料。

#### 函數原型

```c
void i2s_send_data_dma(i2s_device_number_t device_num, const void *buf, size_t buf_len, dmac_channel_number_t channel_num)
```

#### 參數

| 成員名稱            | 描述         |  輸入輸出  |
| ------------------ | ------------ | --------- |
| device\_num         | I2S號        | 輸入      |
| buf                | 發送資料地址  | 輸入      |
| buf\_len            | 資料長度      | 輸入      |
| channel\_num        | DMA通道號     | 輸入      |

#### 返回值

無。

### i2s\_recv\_data\_dma

#### 描述

I2S接收資料。

#### 函數原型

```c
void i2s_recv_data_dma(i2s_device_number_t device_num, uint32_t *buf, size_t buf_len, dmac_channel_number_t channel_num)
```

#### 參數

| 成員名稱            | 描述         |  輸入輸出  |
| ------------------  | ------------ | --------- |
| device\_num         | I2S號        | 輸入      |
| buf                 | 接收資料地址  | 輸出      |
| buf\_len            | 資料長度      | 輸入      |
| channel\_num        | DMA通道號     | 輸入      |

#### 返回值

無

### i2s\_rx\_channel\_config

#### 描述

設置接收通道參數。

#### 函數原型

```c
void i2s_rx_channel_config(i2s_device_number_t device_num, i2s_channel_num_t channel_num, i2s_word_length_t word_length, i2s_word_select_cycles_t word_select_size, i2s_fifo_threshold_t trigger_level, i2s_work_mode_t word_mode)
```

#### 參數

| 成員名稱            | 描述              |  輸入輸出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S號             | 輸入      |
| channel\_num        | 通道號             | 輸入     |
| word\_length        | 接收資料位數       | 輸出      |
| word\_select\_size   | 單個資料時脈數     | 輸入      |
| trigger\_level      | DMA觸發時FIFO深度  | 輸入      |
| word\_mode          | 工作模式           | 輸入      |

#### 返回值

無。

### i2s\_tx\_channel\_config

#### 描述

設置發送通道參數。

#### 函數原型

```c
void i2s_tx_channel_config(i2s_device_number_t device_num, i2s_channel_num_t channel_num, i2s_word_length_t word_length, i2s_word_select_cycles_t word_select_size, i2s_fifo_threshold_t trigger_level, i2s_work_mode_t word_mode)
```

#### 參數

| 成員名稱            | 描述              |  輸入輸出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S號             | 輸入      |
| channel\_num        | 通道號             | 輸入     |
| word\_length        | 接收資料位數       | 輸出      |
| word\_select\_size   | 單個資料時脈數     | 輸入      |
| trigger\_level      | DMA觸發時FIFO深度  | 輸入      |
| word\_mode          | 工作模式           | 輸入      |

#### 返回值

無。

### i2s\_play

#### 描述

發送PCM資料, 比如播放音樂

#### 函數原型

```c
void i2s_play(i2s_device_number_t device_num, dmac_channel_number_t channel_num,
              const uint8_t *buf, size_t buf_len, size_t frame, size_t bits_per_sample, uint8_t track_num)
```

#### 參數

| 成員名稱            | 描述              |  輸入輸出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S號             | 輸入      |
| channel\_num        | 通道號             | 輸入     |
| buf                 | PCM 資料           | 輸入      |
| buf\_len             | PCM資料長度        | 輸入      |
| frame               | 單次發送數量        | 輸入      |
| bits\_per\_sample     | 單次採樣位寬        | 輸入      |
| track_num           | 聲道數            | 輸入      |

#### 返回值

無。

### i2s\_set\_sample\_rate

#### 描述

設置採樣率。

#### 函數原型

```c
uint32_t i2s_set_sample_rate(i2s_device_number_t device_num, uint32_t sample_rate)
```

#### 參數

| 成員名稱            | 描述              |  輸入輸出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S號             | 輸入      |
| sample\_rate        | 採樣率            | 輸入     |

#### 返回值

實際的採樣率。

### i2s\_set\_dma\_divide\_16

#### 描述

設置dma\_divide\_16，16位資料時設置dma\_divide\_16，DMA傳輸時自動將32比特INT32資料分成兩個16比特的左右聲道資料。

#### 函數原型

```c
int i2s_set_dma_divide_16(i2s_device_number_t device_num, uint32_t enable)
```

#### 參數

| 成員名稱            | 描述              |  輸入輸出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S號             | 輸入      |
| enable              | 0:禁用 1：啟動    | 輸入     |

#### 返回值

| 返回值              | 描述       |
| :------------------ | :-------- |
| 0                   | 成功      |
| 非0                 | 失敗       |

### i2s\_get\_dma\_divide\_16

#### 描述

獲取dma\_divide\_16值。用於判斷是否需要設置dma\_divide\_16。

#### 函數原型

```c
int i2s_get_dma_divide_16(i2s_device_number_t device_num)
```

#### 參數

| 成員名稱            | 描述              |  輸入輸出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S號             | 輸入      |

#### 返回值

| 返回值              | 描述       |
| :------------------ | :-------- |
| 1                   | 啟動      |
| 0                   | 禁用      |
| <0                 | 失敗       |

### 舉例

```c
/* I2S0 通道0 設置為接收通道，接收16位資料，單次傳輸32個時脈，FIFO深度為4，標準模式。接收8組資料*/
/* I2S2 通道1 設置為發送通道，發送16位資料，單次傳輸32個時脈，FIFO深度為4，右對齊模式。發送8組資料*/
uint32_t buf[8];
i2s_init(I2S_DEVICE_0, I2S_RECEIVER, 0x3);
i2s_init(I2S_DEVICE_2, I2S_TRANSMITTER, 0xC);
i2s_rx_channel_config(I2S_DEVICE_0, I2S_CHANNEL_0, RESOLUTION_16_BIT, SCLK_CYCLES_32, TRIGGER_LEVEL_4, STANDARD_MODE);
i2s_tx_channel_config(I2S_DEVICE_2, I2S_CHANNEL_1, RESOLUTION_16_BIT, SCLK_CYCLES_32, TRIGGER_LEVEL_4, RIGHT_JUSTIFYING_MODE);
i2s_recv_data_dma(I2S_DEVICE_0, rx_buf, 8, DMAC_CHANNEL1);
i2s_send_data_dma(I2S_DEVICE_2, buf, 8, DMAC_CHANNEL0);
```

## 資料類型

相關資料類型、資料結構定義如下：

- i2s\_device\_number\_t：I2S編號。

- i2s\_channel\_num\_t：I2S通道號。

- i2s\_transmit\_t：I2S傳輸模式。

- i2s\_work_mode\_t：I2S工作模式。

- i2s\_word_select\_cycles\_t：I2S單次傳輸時脈數。

- i2s\_word_length\_t：I2S傳輸資料位數。

- i2s\_fifo\_threshold\_t：I2S FIFO深度。

### i2s\_device\_number\_t

#### 描述

I2S編號。

#### 定義

```c
typedef enum _i2s_device_number
{
    I2S_DEVICE_0 = 0,
    I2S_DEVICE_1 = 1,
    I2S_DEVICE_2 = 2,
    I2S_DEVICE_MAX
} i2s_device_number_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| I2S\_DEVICE\_0     | I2S 0       |
| I2S\_DEVICE\_1     | I2S 1       |
| I2S\_DEVICE\_2     | I2S 2       |

### i2s\_channel\_num\_t

#### 描述

I2S通道號。

#### 定義

```c
typedef enum _i2s_channel_num
{
    I2S_CHANNEL_0 = 0,
    I2S_CHANNEL_1 = 1,
    I2S_CHANNEL_2 = 2,
    I2S_CHANNEL_3 = 3
} i2s_channel_num_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| I2S\_CHANNEL\_0    | I2S通道0    |
| I2S\_CHANNEL\_1    | I2S通道1    |
| I2S\_CHANNEL\_2    | I2S通道2    |
| I2S\_CHANNEL\_3    | I2S通道3    |

### i2s\_transmit\_t

#### 描述

I2S傳輸模式。

#### 定義

```c
typedef enum _i2s_transmit
{
    I2S_TRANSMITTER = 0,
    I2S_RECEIVER = 1
} i2s_transmit_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| I2S\_TRANSMITTER   | 發送模式    |
| I2S\_RECEIVER      | 接收模式    |

### i2s\_work_mode\_t

#### 描述

I2S工作模式。

#### 定義

```c
typedef enum _i2s_work_mode
{
    STANDARD_MODE = 1,
    RIGHT_JUSTIFYING_MODE = 2,
    LEFT_JUSTIFYING_MODE = 4
} i2s_work_mode_t;
```

#### 成員

| 成員名稱                  | 描述        |
| ------------------------ | ----------- |
| STANDARD_MODE            | 標準模式    |
| RIGHT\_JUSTIFYING\_MODE    | 右對齊模式   |
| LEFT\_JUSTIFYING\_MODE     | 左對齊模式   |

### i2s\_word_select\_cycles\_t

#### 描述

I2S單次傳輸時脈數。

#### 定義

```c
typedef enum _word_select_cycles
{
    SCLK_CYCLES_16 = 0x0,
    SCLK_CYCLES_24 = 0x1,
    SCLK_CYCLES_32 = 0x2
} i2s_word_select_cycles_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| SCLK\_CYCLES\_16   | 16個時脈    |
| SCLK\_CYCLES\_24   | 24個時脈    |
| SCLK\_CYCLES\_32   | 32個時脈    |

### i2s\_word_length\_t

#### 描述

I2S傳輸資料位數。

#### 定義

```c
typedef enum _word_length
{
    IGNORE_WORD_LENGTH = 0x0,
    RESOLUTION_12_BIT = 0x1,
    RESOLUTION_16_BIT = 0x2,
    RESOLUTION_20_BIT = 0x3,
    RESOLUTION_24_BIT = 0x4,
    RESOLUTION_32_BIT = 0x5
} i2s_word_length_t;
```

#### 成員

| 成員名稱              | 描述        |
| -------------------- | ----------- |
| IGNORE\_WORD\_LENGTH | 忽略長度     |
| RESOLUTION\_12\_BIT  | 12位資料長度 |
| RESOLUTION\_16\_BIT  | 16位資料長度 |
| RESOLUTION\_20\_BIT  | 20位資料長度 |
| RESOLUTION\_24\_BIT  | 24位資料長度 |
| RESOLUTION\_32\_BIT  | 32位資料長度 |

### i2s\_fifo\_threshold\_t

#### 描述

I2S FIFO深度。

#### 定義

```c
typedef enum _fifo_threshold
{
    /* Interrupt trigger when FIFO level is 1 */
    TRIGGER_LEVEL_1 = 0x0,
    /* Interrupt trigger when FIFO level is 2 */
    TRIGGER_LEVEL_2 = 0x1,
    /* Interrupt trigger when FIFO level is 3 */
    TRIGGER_LEVEL_3 = 0x2,
    /* Interrupt trigger when FIFO level is 4 */
    TRIGGER_LEVEL_4 = 0x3,
    /* Interrupt trigger when FIFO level is 5 */
    TRIGGER_LEVEL_5 = 0x4,
    /* Interrupt trigger when FIFO level is 6 */
    TRIGGER_LEVEL_6 = 0x5,
    /* Interrupt trigger when FIFO level is 7 */
    TRIGGER_LEVEL_7 = 0x6,
    /* Interrupt trigger when FIFO level is 8 */
    TRIGGER_LEVEL_8 = 0x7,
    /* Interrupt trigger when FIFO level is 9 */
    TRIGGER_LEVEL_9 = 0x8,
    /* Interrupt trigger when FIFO level is 10 */
    TRIGGER_LEVEL_10 = 0x9,
    /* Interrupt trigger when FIFO level is 11 */
    TRIGGER_LEVEL_11 = 0xa,
    /* Interrupt trigger when FIFO level is 12 */
    TRIGGER_LEVEL_12 = 0xb,
    /* Interrupt trigger when FIFO level is 13 */
    TRIGGER_LEVEL_13 = 0xc,
    /* Interrupt trigger when FIFO level is 14 */
    TRIGGER_LEVEL_14 = 0xd,
    /* Interrupt trigger when FIFO level is 15 */
    TRIGGER_LEVEL_15 = 0xe,
    /* Interrupt trigger when FIFO level is 16 */
    TRIGGER_LEVEL_16 = 0xf
} i2s_fifo_threshold_t;
```

#### 成員

| 成員名稱              | 描述         |
| -------------------- | ------------ |
| TRIGGER\_LEVEL\_1    | 1位元組FIFO深度 |
| TRIGGER\_LEVEL\_2    | 2位元組FIFO深度 |
| TRIGGER\_LEVEL\_3    | 3位元組FIFO深度 |
| TRIGGER\_LEVEL\_4    | 4位元組FIFO深度 |
| TRIGGER\_LEVEL\_5    | 5位元組FIFO深度 |
| TRIGGER\_LEVEL\_6    | 6位元組FIFO深度 |
| TRIGGER\_LEVEL\_7    | 7位元組FIFO深度 |
| TRIGGER\_LEVEL\_8    | 8位元組FIFO深度 |
| TRIGGER\_LEVEL\_9    | 9位元組FIFO深度 |
| TRIGGER\_LEVEL\_10   | 10位元組FIFO深度|
| TRIGGER\_LEVEL\_11   | 11位元組FIFO深度|
| TRIGGER\_LEVEL\_12   | 12位元組FIFO深度|
| TRIGGER\_LEVEL\_13   | 13位元組FIFO深度|
| TRIGGER\_LEVEL\_14   | 14位元組FIFO深度|
| TRIGGER\_LEVEL\_15   | 15位元組FIFO深度|
| TRIGGER\_LEVEL\_16   | 16位元組FIFO深度|