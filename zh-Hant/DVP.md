# 數位攝像頭介面 (DVP)

## 概述

DVP 是攝像頭介面模組，支持把攝像頭輸入圖像資料轉發給 AI 模組或者內部儲存。

## 功能描述

DVP 模組具有以下功能：

- 支持RGB565、RGB422與單通道Y灰度輸入模式
- 支持設置幀中斷
- 支持設置傳輸地址
- 支持同時向兩個地址寫資料（輸出格式分別是RGB888與RGB565）
- 支持丟棄不需要處理的幀

## API 參考

對應的頭文件 `dvp.h`

為用戶提供以下介面

- dvp\_init

- dvp\_set\_output\_enable

- dvp\_set\_image\_format

- dvp\_set\_image\_size

- dvp\_set\_ai\_addr

- dvp\_set\_display\_addr

- dvp\_config\_interrupt

- dvp\_get\_interrupt

- dvp\_clear\_interrupt

- dvp\_start\_convert

- dvp\_enable\_burst

- dvp\_disable\_burst

- dvp\_enable\_auto

- dvp\_disable\_auto

- dvp\_sccb\_send\_data

- dvp\_sccb\_receive\_data

- dvp\_sccb\_set\_clk\_rate

- dvp\_set\_xclk\_rate

### dvp\_init

#### 描述

初始化DVP。

#### 函數原型

```c
void dvp_init(uint8_t reg_len)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| reg\_len                         | sccb寄存器長度          | 輸入      |

#### 返回值

無

### dvp\_set\_output\_enable

#### 描述

設置輸出模式啟動或禁用。

#### 函數原型

```c
void dvp_set_output_enable(dvp_output_mode_t index, int enable)
```

#### 參數

| 參數名稱         |   描述                 |  輸入輸出  |
| --------------- | ---------------------- | --------- |
| index           | 圖像輸出至內部儲存或AI      | 輸入      |
| enable          | 0：禁用 1：啟動         | 輸入      |

#### 返回值

無。

### dvp\_set\_image\_format

#### 描述

設置圖像接收模式，RGB或YUV。

#### 函數原型

```c
void dvp_set_image_format(uint32_t format)
```

#### 參數

| 參數名稱     |   描述                 |  輸入輸出  |
| ----------- | ---------------------- | --------- |
| format      | 圖像模式<br>DVP\_CFG\_RGB\_FORMAT RGB模式<br>DVP\_CFG\_YUV\_FORMAT YUV模式| 輸入      |

#### 返回值

無

### dvp\_set\_image\_size

#### 描述

設置DVP圖像採集尺寸。

#### 函數原型

```c
void dvp_set_image_size(uint32_t width, uint32_t height)
```

#### 參數

| 參數名稱     |   描述                 |  輸入輸出  |
| ----------- | ---------------------- | --------- |
| width       | 圖像寬度                | 輸入      |
| height      | 圖像高度                | 輸入      |

#### 返回值

無

### dvp\_set\_ai\_addr

#### 描述

設置AI存放圖像的地址，供AI模組進行演算法處理。

#### 函數原型

```c
void dvp_set_ai_addr(uint32_t r_addr, uint32_t g_addr, uint32_t b_addr)
```

#### 參數

| 參數名稱     |   描述                 |  輸入輸出  |
| ----------- | ---------------------- | --------- |
| r\_addr      | 紅色分量地址            | 輸入      |
| g\_addr      | 綠色分量地址            | 輸入      |
| b\_addr      | 藍色分量地址            | 輸入      |

#### 返回值

無

### dvp\_set\_display\_addr

#### 描述

設置採集圖像在內部儲存中的存放地址，可以用來顯示。

#### 函數原型

```c
void dvp_set_display_addr(uint32_t addr)
```

#### 參數

| 參數名稱     |   描述                 |  輸入輸出  |
| ----------- | ---------------------- | --------- |
| addr        | 存放圖像的內部儲存地址       | 輸入      |

#### 返回值

無

### dvp\_config\_interrupt

配置DVP中斷類型。

#### 函數原型

```c
void dvp_config_interrupt(uint32_t interrupt, uint8_t enable)
```

#### 描述

設置圖像開始和結束中斷狀態，啟動或禁用。

#### 參數

| 參數名稱     |   描述                 |  輸入輸出  |
| ----------- | ---------------------- | --------- |
| interrupt   | 中斷類型<br>DVP\_CFG\_START\_INT\_ENABLE 圖像開始採集中斷<br>DVP\_CFG\_FINISH\_INT\_ENABLE 圖像結束採集中斷     | 輸入      |
| enable      | 0：禁止 1：啟動         | 輸入      |

#### 返回值

無。

### dvp\_get\_interrupt

#### 描述

判斷是否是輸入的中斷類型。

#### 函數原型

```c
int dvp_get_interrupt(uint32_t interrupt)
```

#### 參數

| 參數名稱     |   描述                 |  輸入輸出  |
| ----------- | ---------------------- | --------- |
| interrupt   | 中斷類型<br>DVP\_CFG\_START\_INT\_ENABLE 圖像開始採集中斷<br>DVP\_CFG\_FINISH\_INT\_ENABLE 圖像結束採集中斷     | 輸入      |

#### 返回值

| 返回值  | 描述  |
| :----  | :----|
| 0      | 否   |
| 非0    | 是   |

### dvp\_clear\_interrupt

#### 描述

清除中斷。

#### 函數原型

```c
void dvp_clear_interrupt(uint32_t interrupt)
```

#### 參數

| 參數名稱     |   描述                 |  輸入輸出  |
| ----------- | ---------------------- | --------- |
| interrupt   | 中斷類型<br>DVP\_CFG\_START\_INT\_ENABLE 圖像開始採集中斷<br>DVP\_CFG\_FINISH\_INT\_ENABLE 圖像結束採集中斷     | 輸入      |

#### 返回值

無。

### dvp\_start\_convert

#### 描述

開始採集圖像，在確定圖像採集開始中斷後調用。

#### 函數原型

```c
void dvp_start_convert(void)
```

#### 參數

無。

#### 返回值

無。

### dvp\_enable\_burst

#### 描述

啟動突發傳輸模式。

#### 函數原型

```c
void dvp_enable_burst(void)
```

#### 參數

無。

#### 返回值

無。

### dvp\_disable\_burst

#### 描述

禁用突發傳輸模式。

#### 函數原型

```c
void dvp_disable_burst(void)
```

#### 參數

無。

#### 返回值

無。

### dvp\_enable\_auto

#### 描述

啟動自動接收圖像模式。

#### 函數原型

```c
void dvp_enable_auto(void)
```

#### 參數

無。

#### 返回值

無。

### dvp\_disable\_auto

#### 描述

禁用自動接收圖像模式。

#### 函數原型

```c
void dvp_disable_auto(void)
```

#### 參數

無。

#### 返回值

無。

### dvp\_sccb\_send\_data

#### 描述

通過sccb發送資料。

#### 函數原型

```c
void dvp_sccb_send_data(uint8_t dev_addr, uint16_t reg_addr, uint8_t reg_data)
```

#### 參數

| 參數名稱         |   描述                     |  輸入輸出  |
| --------------- | -------------------------- | --------- |
| dev\_addr        | 外部裝置圖像感測器SCCB地址       | 輸入      |
| reg\_addr        | 外部裝置圖像感測器寄存器         | 輸入      |
| reg\_data        | 發送的資料                  | 輸入      |

#### 返回值

無

### dvp\_sccb\_receive\_data

#### 描述

通過SCCB接收資料。

#### 函數原型

```c
uint8_t dvp_sccb_receive_data(uint8_t dev_addr, uint16_t reg_addr)
```

#### 參數

| 參數名稱         |   描述                     |  輸入輸出  |
| --------------- | -------------------------- | --------- |
| dev\_addr        | 外部裝置圖像感測器SCCB地址       | 輸入      |
| reg\_addr        | 外部裝置圖像感測器寄存器         | 輸入      |

#### 返回值

讀取寄存器的資料。

### dvp\_set\_xclk\_rate

#### 描述

設置xclk的速率。

#### 函數原型

```c
uint32_t dvp_set_xclk_rate(uint32_t xclk_rate)
```

#### 參數

| 參數名稱         |   描述                     |  輸入輸出  |
| --------------- | -------------------------- | --------- |
| xclk\_rate      | xclk的速率                  | 輸入      |

#### 返回值

xclk的實際速率。

### dvp\_sccb\_set\_clk\_rate

#### 描述

設置sccb的速率。

#### 函數原型

```c
uint32_t dvp_sccb_set_clk_rate(uint32_t clk_rate)
```

#### 參數

| 參數名稱         |   描述                     |  輸入輸出  |
| --------------- | -------------------------- | --------- |
| clk\_rate       | sccb的速率                  | 輸入      |

#### 返回值

| 返回值                   | 描述                |
| :---------------------- | :------------------ |
| 0                       | 失敗，設置的速率太低無法滿足，請使用I2C |
| 非0                     | 實際的sccb速率       |

### 舉例

```c
/* 採集320 * 240的RGB圖像資料傳輸至lcd_gram0, 及0x40600000 0x40612C00 0x40625800 地址處 */
uint32_t lcd_gram0[38400] __attribute__((aligned(64)));

int on_irq_dvp(void* ctx)
{
    if (dvp_get_interrupt(DVP_STS_FRAME_FINISH))
    {
        dvp_clear_interrupt(DVP_STS_FRAME_FINISH);
    }
    else
    {
        dvp_start_convert();
        dvp_clear_interrupt(DVP_STS_FRAME_START);
    }
    return 0;
}
plic_init();
dvp_init(8);
dvp_set_xclk_rate(12000000);
dvp_enable_burst();
dvp_set_output_enable(DVP_OUTPUT_AI, 1);
dvp_set_output_enable(DVP_OUTPUT_DISPLAY, 1);
dvp_set_image_format(DVP_CFG_RGB_FORMAT);
dvp_set_image_size(320, 240);
dvp_set_ai_addr((uint32_t)0x40600000, (uint32_t)0x40612C00, (uint32_t)0x40625800);
dvp_set_display_addr(lcd_gram0);
dvp_config_interrupt(DVP_CFG_START_INT_ENABLE | DVP_CFG_FINISH_INT_ENABLE, 0);
dvp_disable_auto();
plic_set_priority(IRQN_DVP_INTERRUPT, 1);
plic_irq_register(IRQN_DVP_INTERRUPT, on_irq_dvp, NULL);
plic_irq_enable(IRQN_DVP_INTERRUPT);
dvp_clear_interrupt(DVP_STS_FRAME_START | DVP_STS_FRAME_FINISH);
dvp_config_interrupt(DVP_CFG_START_INT_ENABLE | DVP_CFG_FINISH_INT_ENABLE, 1);
sysctl_enable_irq();
/* 通過SCCB向地址0x60的外部裝置0xFF寄存器發送0x01,從寄存器0x1D讀取資料 */
dvp_sccb_send_data(0x60, 0xFF, 0x01);
dvp_sccb_receive_data(0x60, 0x1D)
```

## 資料類型

相關資料類型、資料結構定義如下：

- dvp\_output\_mode\_t：DVP輸出圖像的模式。

### dvp\_output\_mode\_t

#### 描述

DVP輸入圖像的模式。

#### 定義

```c
typedef enum _dvp_output_mode
{
    DVP_OUTPUT_AI,
    DVP_OUTPUT_DISPLAY,
} dvp_output_mode_t;
```

#### 成員

| 成員名稱                | 描述              |
| ---------------------- | ----------------- |
| DVP\_OUTPUT\_AI        | AI輸出             |
| DVP\_OUTPUT\_DISPLAY   | 向內部儲存輸出用於顯示  |