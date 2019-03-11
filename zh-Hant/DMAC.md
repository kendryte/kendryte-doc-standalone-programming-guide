# 直接內部儲存存取控制器(DMAC)

## 概述

直接存儲訪問 (Direct Memory Access, DMA) 用於在外部裝置與記憶體之間以及記憶體與記憶體之間提供高速資料傳輸。可以在無需任何 CPU 操作的情況下通過 DMA 快速移動資料，從而提高了CPU 的效率。

## 功能描述

DMA 模組具有以下功能：

- 自動選擇一路空閑的 DMA 通道用於傳輸
- 根據源地址和目標地址自動選擇軟體或硬體握手協議
- 支持 1、2、4、8 位元組的元素大小，源和目標大小不必一致
- 非同步或同步傳輸功能
- 循環傳輸功能，常用於刷新屏幕或音頻錄放等場景

## API 參考

對應的頭文件 `dmac.h`

為用戶提供以下介面

- dmac\_init

- dmac\_set\_single\_mode

- dmac\_is\_done

- dmac\_wait\_done

- dmac\_set\_irq

- dmac\_set\_src\_dest\_length

- dmac\_is\_idle

- dmac\_wait\_idle

### dmac\_init

#### 描述

初始化DMA。

#### 函數原型

```c
void dmac_init(void)
```

#### 參數

無。

#### 返回值

無。

### dmac\_set\_single\_mode

#### 描述

設置單路DMA參數。

#### 函數原型

```c
void dmac_set_single_mode(dmac_channel_number_t channel_num, const void *src, void *dest, dmac_address_increment_t src_inc, dmac_address_increment_t dest_inc, dmac_burst_trans_length_t dmac_burst_size, dmac_transfer_width_t dmac_trans_width, size_t block_size)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| channel_num                     | DMA 通道號              | 輸入      |
| src                             | 源地址                  | 輸入      |
| dest                            | 目標地址                | 輸出      |
| src\_inc                        | 源地址是否自增          | 輸入      |
| dest\_inc                       | 目標地址是否自增        | 輸入      |
| dmac\_burst\_size               | 突發傳輸數量            | 輸入      |
| dmac\_trans\_width              | 單次傳輸資料位寬         | 輸入      |
| block\_size                       | 傳輸資料的個數           | 輸入      |

#### 返回值

無。

### dmac\_is\_done

#### 描述

用於DMAC啟動後判斷是否完成傳輸。用於DMAC啟動傳輸後，如果在啟動前判斷會不准確。

#### 函數原型

```c
int dmac_is_done(dmac_channel_number_t channel_num)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| channel\_num                     | DMA 通道號              | 輸入      |

#### 返回值

| 返回值  | 描述     |
| :----  | :--------|
| 0      | 未完成    |
| 1      | 已完成    |

### dmac\_wait\_done

#### 描述

等待DMA完成工作。

#### 函數原型

```c
void dmac_wait_done(dmac_channel_number_t channel_num)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| channel\_num                     | DMA 通道號              | 輸入      |

#### 返回值

無。

### dmac\_set\_irq

#### 描述

設置DMAC中斷的回調函數

#### 函數原型

```c
void dmac_set_irq(dmac_channel_number_t channel_num , plic_irq_callback_t dmac_callback, void *ctx, uint32_t priority)
```

#### 參數

| 參數名稱                       |   描述           |  輸入輸出  |
| ----------------------------- | ---------------  | --------- |
| channel\_num                  | DMA 通道號        | 輸入      |
| dmac\_callback                | 中斷回調函數      | 輸入      |
| ctx                           | 回調函數的參數    | 輸入       |
| priority                      | 中斷優先順序        | 輸入       |

#### 返回值

無。

### dmac\_set\_src\_dest\_length

#### 描述

設置DMAC的源地址、目的地址和長度，然後啟動DMAC傳輸。如果src為NULL則不設置源地址，dest為NULL則不設置目的地址，len<=0則不設置長度。

該函數一般用於DMAC中斷中，使DMA繼續傳輸資料，而不必再次設置DMAC的所有參數以節省時間。

#### 函數原型

```c
void dmac_set_src_dest_length(dmac_channel_number_t channel_num, const void *src, void *dest, size_t len)
```

#### 參數

| 參數名稱                       |   描述           |  輸入輸出  |
| ----------------------------- | ---------------  | --------- |
| channel\_num                  | DMA 通道號        | 輸入      |
| src                           | 中斷回調函數      | 輸入      |
| dest                          | 回調函數的參數    | 輸入       |
| len                           | 傳輸長度        | 輸入       |

#### 返回值

無。

### dmac\_is\_idle

#### 描述

判斷DMAC當前通道是否空閑，該函數在傳輸前和傳輸後都可以用來判斷DMAC狀態。

#### 函數原型

```c
int dmac_is_idle(dmac_channel_number_t channel_num)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| channel\_num                     | DMA 通道號              | 輸入      |

#### 返回值

| 返回值  | 描述     |
| :----  | :--------|
| 0      | 忙       |
| 1      | 空閑     |

### dmac\_wait\_idle

#### 描述

等待DMAC進入空閑狀態。

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| channel_num                     | DMA 通道號              | 輸入      |

#### 返回值

無。

### 舉例

```c
/* I2C通過DMA發送128個int資料 */
uint32_t buf[128];
dmac_wait_idle(SYSCTL_DMA_CHANNEL_0);
sysctl_dma_select(SYSCTL_DMA_CHANNEL_0, SYSCTL_DMA_SELECT_I2C0_TX_REQ);
dmac_set_single_mode(SYSCTL_DMA_CHANNEL_0, buf, (void*)(&i2c_adapter->data_cmd), DMAC_ADDR_INCREMENT, DMAC_ADDR_NOCHANGE, DMAC_MSIZE_4, DMAC_TRANS_WIDTH_32, 128);
dmac_wait_done(SYSCTL_DMA_CHANNEL_0);
```

## 資料類型

相關資料類型、資料結構定義如下：

- dmac\_channel\_number\_t：DMA通道編號。

- dmac\_address\_increment\_t：地址增長方式。

- dmac\_burst\_trans\_length\_t：突發傳輸數量。

- dmac\_transfer\_width\_t：單次傳輸資料位數。

### dmac\_channel\_number\_t

#### 描述

DMA通道編號。

#### 定義

```c
typedef enum _dmac_channel_number
{
    DMAC_CHANNEL0 = 0,
    DMAC_CHANNEL1 = 1,
    DMAC_CHANNEL2 = 2,
    DMAC_CHANNEL3 = 3,
    DMAC_CHANNEL4 = 4,
    DMAC_CHANNEL5 = 5,
    DMAC_CHANNEL_MAX
} dmac_channel_number_t;
```

#### 成員

| 成員名稱         | 描述         |
| --------------- | ------------ |
| DMAC\_CHANNEL0  | DMA通道 0     |
| DMAC\_CHANNEL1  | DMA通道 1     |
| DMAC\_CHANNEL2  | DMA通道 2     |
| DMAC\_CHANNEL3  | DMA通道 3     |
| DMAC\_CHANNEL4  | DMA通道 4     |
| DMAC\_CHANNEL5  | DMA通道 5     |

### dmac\_address\_increment\_t

#### 描述

地址增長方式。

#### 定義

```c
typedef enum _dmac_address_increment
{
    DMAC_ADDR_INCREMENT = 0x0,
    DMAC_ADDR_NOCHANGE  = 0x1
} dmac_address_increment_t;
```

#### 成員

| 成員名稱                | 描述         |
| ---------------------- | ------------ |
| DMAC\_ADDR\_INCREMENT  | 地址自動增長  |
| DMAC\_ADDR\_NOCHANGE   | 地址不變      |

### dmac\_burst\_trans\_length\_t

#### 描述

突發傳輸數量。

#### 定義

```c
typedef enum _dmac_burst_trans_length
{
    DMAC_MSIZE_1   = 0x0,
    DMAC_MSIZE_4   = 0x1,
    DMAC_MSIZE_8   = 0x2,
    DMAC_MSIZE_16  = 0x3,
    DMAC_MSIZE_32  = 0x4,
    DMAC_MSIZE_64  = 0x5,
    DMAC_MSIZE_128 = 0x6,
    DMAC_MSIZE_256 = 0x7
} dmac_burst_trans_length_t;
```

#### 成員

| 成員名稱           | 描述              |
| ----------------- | ----------------- |
| DMAC\_MSIZE\_1    | 單次傳輸數量乘1    |
| DMAC\_MSIZE\_4    | 單次傳輸數量乘4    |
| DMAC\_MSIZE\_8    | 單次傳輸數量乘8    |
| DMAC\_MSIZE\_16   | 單次傳輸數量乘16   |
| DMAC\_MSIZE\_32   | 單次傳輸數量乘32   |
| DMAC\_MSIZE\_64   | 單次傳輸數量乘64   |
| DMAC\_MSIZE\_128  | 單次傳輸數量乘128  |
| DMAC\_MSIZE\_256  | 單次傳輸數量乘256  |

### dmac\_transfer\_width\_t

#### 描述

單次傳輸資料位數。

#### 定義

```c
typedef enum _dmac_transfer_width
{
    DMAC_TRANS_WIDTH_8   = 0x0,
    DMAC_TRANS_WIDTH_16  = 0x1,
    DMAC_TRANS_WIDTH_32  = 0x2,
    DMAC_TRANS_WIDTH_64  = 0x3,
    DMAC_TRANS_WIDTH_128 = 0x4,
    DMAC_TRANS_WIDTH_256 = 0x5
} dmac_transfer_width_t;
```

#### 成員

| 成員名稱                 | 描述              |
| ----------------------- | ----------------- |
| DMAC\_TRANS\_WIDTH\_8   | 單次傳輸8位        |
| DMAC\_TRANS\_WIDTH\_16  | 單次傳輸16位       |
| DMAC\_TRANS\_WIDTH\_32  | 單次傳輸32位       |
| DMAC\_TRANS\_WIDTH\_64  | 單次傳輸64位       |
| DMAC\_TRANS\_WIDTH\_128 | 單次傳輸128位      |
| DMAC\_TRANS\_WIDTH\_256 | 單次傳輸256位      |