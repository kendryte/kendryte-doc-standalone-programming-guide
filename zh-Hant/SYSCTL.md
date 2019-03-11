# 系統控制

## 概述

系統控制模組提供對操作系統的配置功能。

## 功能描述

系統控制模組具有以下功能：

- 設置 PLL CPU 時脈頻率。

- 設置各個模組時脈的分頻值。

- 獲取各個模組的時脈頻率。

- 啟動、禁用、複位各個模組。

- 設置DMA請求源。

- 啟動禁用系統中斷。

## API 參考

對應的頭文件 `sysctl.h`

為用戶提供以下介面

- sysctl\_cpu\_set\_freq
- sysctl\_pll\_set\_freq
- sysctl\_pll\_get\_freq
- sysctl\_pll\_enable
- sysctl\_pll\_disable
- sysctl\_clock\_set\_threshold
- sysctl\_clock\_get\_threshold
- sysctl\_clock\_set\_clock\_select
- sysctl\_clock\_get\_clock\_select
- sysctl\_clock\_get\_freq
- sysctl\_clock\_enable
- sysctl\_clock\_disable
- sysctl\_reset
- sysctl\_dma\_select
- sysctl\_set\_power\_mode
- sysctl\_enable\_irq
- sysctl\_disable\_irq
- sysctl\_get\_time\_us
- sysctl\_get\_reset\_status

### sysctl\_cpu\_set\_freq

#### 描述

設置CPU工作頻率。是通過修改PLL0的頻率實現的。

#### 函數原型

```c
uint32_t sysctl_cpu_set_freq(uint32_t freq)
```

#### 參數

| 參數名稱     |   描述           |  輸入輸出  |
| ----------- | ---------------- | --------- |
| freq        | 要設置的頻率（Hz） | 輸入      |

#### 返回值

設置後的實際頻率（Hz）。

### sysctl\_set\_pll\_frequency

#### 描述

設置PLL頻率。

#### 函數原型

```c
uint32_t sysctl_pll_set_freq(sysctl_pll_t pll, uint32_t pll_freq)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| pll             | PLL編號          | 輸入       |
| pll\_freq        | 要設置的頻率（Hz）| 輸入       |

#### 返回值

設置後的實際頻率（Hz）。

#### 函數原型

```c
uint32_t sysctl_pll_get_freq(sysctl_pll_t pll)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| pll             | PLL編號          | 輸入       |

#### 返回值

對應PLL的頻率（Hz）。

### sysctl\_pll\_enable

#### 描述

啟動對應的PLL。

#### 函數原型

```c
int sysctl_pll_enable(sysctl_pll_t pll)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| pll             | PLL編號          | 輸入       |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### sysctl\_pll\_disable

#### 描述

禁用對應PLL。

#### 函數原型

```c
int sysctl_pll_disable(sysctl_pll_t pll)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| pll             | PLL編號          | 輸入       |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### sysctl\_clock\_set\_threshold

#### 描述

設置對應時脈的分頻值。

#### 函數原型

```c
void sysctl_clock_set_threshold(sysctl_threshold_t which, int threshold)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| which           | 設置的時脈        | 輸入       |
| threshold       | 分頻值            | 輸入       |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### sysctl\_clock\_get\_threshold

#### 描述

獲取對應時脈的分頻值。

#### 函數原型

```c
int sysctl_clock_get_threshold(sysctl_threshold_t which)
```

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| which           | 時脈             | 輸入       |

#### 返回值

對應時脈的分頻值。

### sysctl\_clock\_set\_clock\_select

#### 描述

設置時脈源。

#### 函數原型

```c
int sysctl_clock_set_clock_select(sysctl_clock_select_t which, int select)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| which           | 時脈             | 輸入       |
| select          | 時脈源           | 輸入       |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### sysctl\_clock\_get\_clock\_select

#### 描述

獲取時脈對應的時脈源。

#### 函數原型

```c
int sysctl_clock_get_clock_select(sysctl_clock_select_t which)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| which           | 時脈             | 輸入       |

#### 返回值

時脈對應的時脈源。

### sysctl\_clock\_get\_freq

#### 描述

獲取時脈的頻率。

#### 函數原型

```c
uint32_t sysctl_clock_get_freq(sysctl_clock_t clock)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| clock           | 時脈             | 輸入       |

#### 返回值

時脈的頻率（Hz）

### sysctl\_clock\_enable

#### 描述

啟動時脈。PLL要使用sysctl\_pll\_enable。

#### 函數原型

```c
int sysctl_clock_enable(sysctl_clock_t clock)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| clock           | 時脈             | 輸入       |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### sysctl\_clock\_disable

#### 描述

禁用時脈，PLL使用sysctl\_pll\_disable。

#### 函數原型

```c
int sysctl_clock_disable(sysctl_clock_t clock)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| clock           | 時脈             | 輸入       |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### sysctl\_reset

#### 描述

複位各個模組。

#### 函數原型

```c
void sysctl_reset(sysctl_reset_t reset)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| reset           | 預複位模組        | 輸入       |

#### 返回值

無。

### sysctl\_dma\_select

#### 描述

設置DMA請求源。與DMAC的API配合使用。

#### 函數原型

```c
int sysctl_dma_select(sysctl_dma_channel_t channel, sysctl_dma_select_t select)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------- | --------- |
| channel         | DMA通道號        | 輸入       |
| select          | DMA請求源        | 輸入       |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### sysctl\_set\_power\_mode

#### 描述

設置FPIOA的對應電源域的電壓。

#### 原型

```c
void sysctl_set_power_mode(sysctl_power_bank_t power_bank, sysctl_io_power_mode_t io_power_mode)
```

#### 參數

| 參數名稱         |   描述               |  輸入輸出  |
| --------------- | -------------------- | --------- |
| power\_bank     | IO電源域編號          | 輸入       |
| io\_power\_mode | 設置的電壓值1.8V或3.3V| 輸入       |

#### 返回值

無。

### sysctl\_enable\_irq

#### 描述

啟動系統中斷，如果使用中斷一定要開啟系統中斷。

#### 函數原型

```c
void sysctl_enable_irq(void)
```

#### 參數

無。

#### 返回值

無。

### sysctl\_disable\_irq

#### 描述

禁用系統中斷。

#### 函數原型

```c
void sysctl_disable_irq(void)
```

#### 參數

無。

#### 返回值

無。

### sysctl\_get\_time\_us

#### 描述

開機至今的時間（微秒）。

#### 函數原型

```c
uint64_t sysctl_get_time_us(void)
```

#### 參數

無。

#### 返回值

開機至今的時間（微秒）。

### sysctl\_get\_reset\_status

#### 描述

獲取複位狀態。參見sysctl_reset_enum_status_t說明。

#### 函數原型

```c
sysctl_reset_enum_status_t sysctl_get_reset_status(void)
```

#### 參數

無。

#### 返回值

複位狀態。

## 資料類型

相關資料類型、資料結構定義如下：

- sysctl\_pll\_t：PLL編號。

- sysctl\_threshold\_t：設置分頻值時各模組編號。

- sysctl\_clock\_select\_t：設置時脈源時各模組編號。

- sysctl\_clock\_t：各個模組的編號。

- sysctl\_reset\_t：複位時各個模組的編號。

- sysctl\_dma\_channel\_t：DMA通道號。

- sysctl\_dma\_select\_t：DMA請求源編號。

- sysctl\_power\_bank\_t：電源域編號。

- sysctl\_io\_power\_mode\_t：IO輸出電壓值。

- sysctl\_reset\_enum\_status\_t：複位狀態。

### sysctl\_pll_t

#### 描述

PLL編號。

#### 定義

```c
typedef enum _sysctl_pll_t
{
    SYSCTL_PLL0,
    SYSCTL_PLL1,
    SYSCTL_PLL2,
    SYSCTL_PLL_MAX
} sysctl_pll_t;
```

#### 成員

| 成員名稱             |      描述             |
| :------------------ | :-------------------- |
|SYSCTL\_PLL0         | PLL0                  |
|SYSCTL\_PLL1         | PLL1                  |
|SYSCTL\_PLL2         | PLL2                  |

### sysctl\_threshold\_t

#### 描述

設置分頻值各模組編號。

#### 定義

```c
typedef enum _sysctl_threshold_t
{
    SYSCTL_THRESHOLD_ACLK,
    SYSCTL_THRESHOLD_APB0,
    SYSCTL_THRESHOLD_APB1,
    SYSCTL_THRESHOLD_APB2,
    SYSCTL_THRESHOLD_SRAM0,
    SYSCTL_THRESHOLD_SRAM1,
    SYSCTL_THRESHOLD_AI,
    SYSCTL_THRESHOLD_DVP,
    SYSCTL_THRESHOLD_ROM,
    SYSCTL_THRESHOLD_SPI0,
    SYSCTL_THRESHOLD_SPI1,
    SYSCTL_THRESHOLD_SPI2,
    SYSCTL_THRESHOLD_SPI3,
    SYSCTL_THRESHOLD_TIMER0,
    SYSCTL_THRESHOLD_TIMER1,
    SYSCTL_THRESHOLD_TIMER2,
    SYSCTL_THRESHOLD_I2S0,
    SYSCTL_THRESHOLD_I2S1,
    SYSCTL_THRESHOLD_I2S2,
    SYSCTL_THRESHOLD_I2S0_M,
    SYSCTL_THRESHOLD_I2S1_M,
    SYSCTL_THRESHOLD_I2S2_M,
    SYSCTL_THRESHOLD_I2C0,
    SYSCTL_THRESHOLD_I2C1,
    SYSCTL_THRESHOLD_I2C2,
    SYSCTL_THRESHOLD_WDT0,
    SYSCTL_THRESHOLD_WDT1,
    SYSCTL_THRESHOLD_MAX = 28
} sysctl_threshold_t;
```

#### 成員

| 成員名稱                       |      描述             |
| :---------------------------- | :-------------------- |
|SYSCTL\_THRESHOLD\_ACLK        | ACLK                  |
|SYSCTL\_THRESHOLD\_APB0        | APB0                  |
|SYSCTL\_THRESHOLD\_APB1        | APB1                  |
|SYSCTL\_THRESHOLD\_APB2        | ACLK                  |
|SYSCTL\_THRESHOLD\_SRAM0       | SRAM0                 |
|SYSCTL\_THRESHOLD\_SRAM1       | SRAM1                 |
|SYSCTL\_THRESHOLD\_AI          | AI                    |
|SYSCTL\_THRESHOLD\_DVP         | DVP                   |
|SYSCTL\_THRESHOLD\_ROM         | ROM                   |
|SYSCTL\_THRESHOLD\_SPI0        | SPI0                  |
|SYSCTL\_THRESHOLD\_SPI1        | SPI1                  |
|SYSCTL\_THRESHOLD\_SPI2        | SPI2                  |
|SYSCTL\_THRESHOLD\_SPI3        | SPI3                  |
|SYSCTL\_THRESHOLD\_TIMER0      | TIMER0                |
|SYSCTL\_THRESHOLD\_TIMER1      | TIMER1                |
|SYSCTL\_THRESHOLD\_TIMER2      | TIMER2                |
|SYSCTL\_THRESHOLD\_I2S0        | I2S0                  |
|SYSCTL\_THRESHOLD\_I2S1        | I2S1                  |
|SYSCTL\_THRESHOLD\_I2S2        | I2S2                  |
|SYSCTL\_THRESHOLD\_I2S0\_M     | I2S0 MCLK             |
|SYSCTL\_THRESHOLD\_I2S1\_M     | I2S1 MCLK             |
|SYSCTL\_THRESHOLD\_I2S2\_M     | I2S2 MCLK             |
|SYSCTL\_THRESHOLD\_I2C0        | I2C0                  |
|SYSCTL\_THRESHOLD\_I2C1        | I2C1                  |
|SYSCTL\_THRESHOLD\_I2C2        | I2C2                  |
|SYSCTL\_THRESHOLD\_WDT0        | WDT0                  |
|SYSCTL\_THRESHOLD\_WDT1        | WDT1                  |

### sysctl\_clock\_select\_t

#### 描述

設置時脈源時各模組編號。

#### 定義

```c
typedef enum _sysctl_clock_select_t
{
    SYSCTL_CLOCK_SELECT_PLL0_BYPASS,
    SYSCTL_CLOCK_SELECT_PLL1_BYPASS,
    SYSCTL_CLOCK_SELECT_PLL2_BYPASS,
    SYSCTL_CLOCK_SELECT_PLL2,
    SYSCTL_CLOCK_SELECT_ACLK,
    SYSCTL_CLOCK_SELECT_SPI3,
    SYSCTL_CLOCK_SELECT_TIMER0,
    SYSCTL_CLOCK_SELECT_TIMER1,
    SYSCTL_CLOCK_SELECT_TIMER2,
    SYSCTL_CLOCK_SELECT_SPI3_SAMPLE,
    SYSCTL_CLOCK_SELECT_MAX = 11
} sysctl_clock_select_t;
```

#### 成員

| 成員名稱                                  |      描述             |
| :--------------------------------------- | :-------------------- |
|SYSCTL\_CLOCK\_SELECT\_PLL0\_BYPASS       | PLL0\_BYPASS           |
|SYSCTL\_CLOCK\_SELECT\_PLL1\_BYPASS       | PLL1\_BYPASS           |
|SYSCTL\_CLOCK\_SELECT\_PLL2\_BYPASS       | PLL2\_BYPASS           |
|SYSCTL\_CLOCK\_SELECT\_PLL2               | PLL2                  |
|SYSCTL\_CLOCK\_SELECT\_ACLK               | ACLK                  |
|SYSCTL\_CLOCK\_SELECT\_SPI3               | SPI3                  |
|SYSCTL\_CLOCK\_SELECT\_TIMER0             | TIMER0                |
|SYSCTL\_CLOCK\_SELECT\_TIMER1             | TIMER1                |
|SYSCTL\_CLOCK\_SELECT\_TIMER2             | TIMER2                |
|SYSCTL\_CLOCK\_SELECT\_SPI3\_SAMPLE       | SPI3資料採樣時脈沿選擇  |

### sysctl\_clock\_t

#### 描述

各個模組的編號。

#### 定義

```c
typedef enum _sysctl_clock_t
{
    SYSCTL_CLOCK_PLL0,
    SYSCTL_CLOCK_PLL1,
    SYSCTL_CLOCK_PLL2,
    SYSCTL_CLOCK_CPU,
    SYSCTL_CLOCK_SRAM0,
    SYSCTL_CLOCK_SRAM1,
    SYSCTL_CLOCK_APB0,
    SYSCTL_CLOCK_APB1,
    SYSCTL_CLOCK_APB2,
    SYSCTL_CLOCK_ROM,
    SYSCTL_CLOCK_DMA,
    SYSCTL_CLOCK_AI,
    SYSCTL_CLOCK_DVP,
    SYSCTL_CLOCK_FFT,
    SYSCTL_CLOCK_GPIO,
    SYSCTL_CLOCK_SPI0,
    SYSCTL_CLOCK_SPI1,
    SYSCTL_CLOCK_SPI2,
    SYSCTL_CLOCK_SPI3,
    SYSCTL_CLOCK_I2S0,
    SYSCTL_CLOCK_I2S1,
    SYSCTL_CLOCK_I2S2,
    SYSCTL_CLOCK_I2C0,
    SYSCTL_CLOCK_I2C1,
    SYSCTL_CLOCK_I2C2,
    SYSCTL_CLOCK_UART1,
    SYSCTL_CLOCK_UART2,
    SYSCTL_CLOCK_UART3,
    SYSCTL_CLOCK_AES,
    SYSCTL_CLOCK_FPIOA,
    SYSCTL_CLOCK_TIMER0,
    SYSCTL_CLOCK_TIMER1,
    SYSCTL_CLOCK_TIMER2,
    SYSCTL_CLOCK_WDT0,
    SYSCTL_CLOCK_WDT1,
    SYSCTL_CLOCK_SHA,
    SYSCTL_CLOCK_OTP,
    SYSCTL_CLOCK_RTC,
    SYSCTL_CLOCK_ACLK = 40,
    SYSCTL_CLOCK_HCLK,
    SYSCTL_CLOCK_IN0,
    SYSCTL_CLOCK_MAX
} sysctl_clock_t;
```

#### 成員

| 成員名稱                                |      描述        |
| :------------------------------------- | :--------------- |
|SYSCTL\_CLOCK\_PLL0                     | PLL0             |
|SYSCTL\_CLOCK\_PLL1                     | PLL1             |
|SYSCTL\_CLOCK\_PLL2                     | PLL2             |
|SYSCTL\_CLOCK\_CPU                      | CPU              |
|SYSCTL\_CLOCK\_SRAM0                    | SRAM0            |
|SYSCTL\_CLOCK\_SRAM1                    | SRAM1            |
|SYSCTL\_CLOCK\_APB0                     | APB0             |
|SYSCTL\_CLOCK\_APB1                     | APB1             |
|SYSCTL\_CLOCK\_APB2                     | APB2             |
|SYSCTL\_CLOCK\_ROM                      | ROM              |
|SYSCTL\_CLOCK\_DMA                      | DMA              |
|SYSCTL\_CLOCK\_AI                       | AI               |
|SYSCTL\_CLOCK\_DVP                      | DVP              |
|SYSCTL\_CLOCK\_FFT                      | FFT              |
|SYSCTL\_CLOCK\_GPIO                     | GPIO             |
|SYSCTL\_CLOCK\_SPI0                     | SPI0             |
|SYSCTL\_CLOCK\_SPI1                     | SPI1             |
|SYSCTL\_CLOCK\_SPI2                     | SPI2             |
|SYSCTL\_CLOCK\_SPI3                     | SPI3             |
|SYSCTL\_CLOCK\_I2S0                     | I2S0             |
|SYSCTL\_CLOCK\_I2S1                     | I2S1             |
|SYSCTL\_CLOCK\_I2S2                     | I2S2             |
|SYSCTL\_CLOCK\_I2C0                     | I2C0             |
|SYSCTL\_CLOCK\_I2C1                     | I2C1             |
|SYSCTL\_CLOCK\_I2C2                     | I2C2             |
|SYSCTL\_CLOCK\_UART1                    | UART1            |
|SYSCTL\_CLOCK\_UART2                    | UART2            |
|SYSCTL\_CLOCK\_UART3                    | UART3            |
|SYSCTL\_CLOCK\_AES                      | AES              |
|SYSCTL\_CLOCK\_FPIOA                    | FPIOA            |
|SYSCTL\_CLOCK\_TIMER0                   | TIMER0           |
|SYSCTL\_CLOCK\_TIMER1                   | TIMER1           |
|SYSCTL\_CLOCK\_TIMER2                   | TIMER2           |
|SYSCTL\_CLOCK\_WDT0                     | WDT0             |
|SYSCTL\_CLOCK\_WDT1                     | WDT1             |
|SYSCTL\_CLOCK\_SHA                      | SHA              |
|SYSCTL\_CLOCK\_OTP                      | OTP              |
|SYSCTL\_CLOCK\_RTC                      | RTC              |
|SYSCTL\_CLOCK\_ACLK                     | ACLK             |
|SYSCTL\_CLOCK\_HCLK                     | HCLK             |
|SYSCTL\_CLOCK\_IN0                      | 外部輸入時脈IN0   |

### sysctl\_reset\_t

#### 描述

複位時各個模組的編號。

#### 定義

```c
typedef enum _sysctl_reset_t
{
    SYSCTL_RESET_SOC,
    SYSCTL_RESET_ROM,
    SYSCTL_RESET_DMA,
    SYSCTL_RESET_AI,
    SYSCTL_RESET_DVP,
    SYSCTL_RESET_FFT,
    SYSCTL_RESET_GPIO,
    SYSCTL_RESET_SPI0,
    SYSCTL_RESET_SPI1,
    SYSCTL_RESET_SPI2,
    SYSCTL_RESET_SPI3,
    SYSCTL_RESET_I2S0,
    SYSCTL_RESET_I2S1,
    SYSCTL_RESET_I2S2,
    SYSCTL_RESET_I2C0,
    SYSCTL_RESET_I2C1,
    SYSCTL_RESET_I2C2,
    SYSCTL_RESET_UART1,
    SYSCTL_RESET_UART2,
    SYSCTL_RESET_UART3,
    SYSCTL_RESET_AES,
    SYSCTL_RESET_FPIOA,
    SYSCTL_RESET_TIMER0,
    SYSCTL_RESET_TIMER1,
    SYSCTL_RESET_TIMER2,
    SYSCTL_RESET_WDT0,
    SYSCTL_RESET_WDT1,
    SYSCTL_RESET_SHA,
    SYSCTL_RESET_RTC,
    SYSCTL_RESET_MAX = 31
} sysctl_reset_t;
```

#### 成員

| 成員名稱                              |      描述         |
| :----------------------------------- | :---------------- |
|SYSCTL\_RESET\_SOC                    | 晶片複位           |
|SYSCTL\_RESET\_ROM                    | ROM               |
|SYSCTL\_RESET\_DMA                    | DMA               |
|SYSCTL\_RESET\_AI                     | AI                |
|SYSCTL\_RESET\_DVP                    | DVP               |
|SYSCTL\_RESET\_FFT                    | FFT               |
|SYSCTL\_RESET\_GPIO                   | GPIO              |
|SYSCTL\_RESET\_SPI0                   | SPI0              |
|SYSCTL\_RESET\_SPI1                   | SPI1              |
|SYSCTL\_RESET\_SPI2                   | SPI2              |
|SYSCTL\_RESET\_SPI3                   | SPI3              |
|SYSCTL\_RESET\_I2S0                   | I2S0              |
|SYSCTL\_RESET\_I2S1                   | I2S1              |
|SYSCTL\_RESET\_I2S2                   | I2S2              |
|SYSCTL\_RESET\_I2C0                   | I2C0              |
|SYSCTL\_RESET\_I2C1                   | I2C1              |
|SYSCTL\_RESET\_I2C2                   | I2C2              |
|SYSCTL\_RESET\_UART1                  | UART1             |
|SYSCTL\_RESET\_UART2                  | UART2             |
|SYSCTL\_RESET\_UART3                  | UART3             |
|SYSCTL\_RESET\_AES                    | AES               |
|SYSCTL\_RESET\_FPIOA                  | FPIOA             |
|SYSCTL\_RESET\_TIMER0                 | TIMER0            |
|SYSCTL\_RESET\_TIMER1                 | TIMER1            |
|SYSCTL\_RESET\_TIMER2                 | TIMER2            |
|SYSCTL\_RESET\_WDT0                   | WDT0              |
|SYSCTL\_RESET\_WDT1                   | WDT1              |
|SYSCTL\_RESET\_SHA                    | SHA               |
|SYSCTL\_RESET\_RTC                    | RTC               |

### sysctl\_dma\_channel\_t

#### 描述

DMA通道號。

#### 定義

```c
typedef enum _sysctl_dma_channel_t
{
    SYSCTL_DMA_CHANNEL_0,
    SYSCTL_DMA_CHANNEL_1,
    SYSCTL_DMA_CHANNEL_2,
    SYSCTL_DMA_CHANNEL_3,
    SYSCTL_DMA_CHANNEL_4,
    SYSCTL_DMA_CHANNEL_5,
    SYSCTL_DMA_CHANNEL_MAX
} sysctl_dma_channel_t;
```

#### 成員

| 成員名稱                               |      描述         |
| :------------------------------------ | :---------------- |
|SYSCTL\_DMA\_CHANNEL\_0                | DMA通道0           |
|SYSCTL\_DMA\_CHANNEL\_1                | DMA通道1           |
|SYSCTL\_DMA\_CHANNEL\_2                | DMA通道2           |
|SYSCTL\_DMA\_CHANNEL\_3                | DMA通道3           |
|SYSCTL\_DMA\_CHANNEL\_4                | DMA通道4           |
|SYSCTL\_DMA\_CHANNEL\_5                | DMA通道5           |

### sysctl\_dma\_select\_t

#### 描述

DMA請求源編號。

#### 定義

```c
typedef enum _sysctl_dma_select_t
{
    SYSCTL_DMA_SELECT_SSI0_RX_REQ,
    SYSCTL_DMA_SELECT_SSI0_TX_REQ,
    SYSCTL_DMA_SELECT_SSI1_RX_REQ,
    SYSCTL_DMA_SELECT_SSI1_TX_REQ,
    SYSCTL_DMA_SELECT_SSI2_RX_REQ,
    SYSCTL_DMA_SELECT_SSI2_TX_REQ,
    SYSCTL_DMA_SELECT_SSI3_RX_REQ,
    SYSCTL_DMA_SELECT_SSI3_TX_REQ,
    SYSCTL_DMA_SELECT_I2C0_RX_REQ,
    SYSCTL_DMA_SELECT_I2C0_TX_REQ,
    SYSCTL_DMA_SELECT_I2C1_RX_REQ,
    SYSCTL_DMA_SELECT_I2C1_TX_REQ,
    SYSCTL_DMA_SELECT_I2C2_RX_REQ,
    SYSCTL_DMA_SELECT_I2C2_TX_REQ,
    SYSCTL_DMA_SELECT_UART1_RX_REQ,
    SYSCTL_DMA_SELECT_UART1_TX_REQ,
    SYSCTL_DMA_SELECT_UART2_RX_REQ,
    SYSCTL_DMA_SELECT_UART2_TX_REQ,
    SYSCTL_DMA_SELECT_UART3_RX_REQ,
    SYSCTL_DMA_SELECT_UART3_TX_REQ,
    SYSCTL_DMA_SELECT_AES_REQ,
    SYSCTL_DMA_SELECT_SHA_RX_REQ,
    SYSCTL_DMA_SELECT_AI_RX_REQ,
    SYSCTL_DMA_SELECT_FFT_RX_REQ,
    SYSCTL_DMA_SELECT_FFT_TX_REQ,
    SYSCTL_DMA_SELECT_I2S0_TX_REQ,
    SYSCTL_DMA_SELECT_I2S0_RX_REQ,
    SYSCTL_DMA_SELECT_I2S1_TX_REQ,
    SYSCTL_DMA_SELECT_I2S1_RX_REQ,
    SYSCTL_DMA_SELECT_I2S2_TX_REQ,
    SYSCTL_DMA_SELECT_I2S2_RX_REQ,
    SYSCTL_DMA_SELECT_MAX
} sysctl_dma_select_t;
```

#### 成員

| 成員名稱                                          |      描述         |
| :------------------------------------------------ | :---------------- |
|SYSCTL\_DMA\_SELECT\_SSI0\_RX\_REQ                 | SPI0接收          |
|SYSCTL\_DMA\_SELECT\_SSI0\_TX\_REQ                 | SPI0發送          |
|SYSCTL\_DMA\_SELECT\_SSI1\_RX\_REQ                 | SPI1接收          |
|SYSCTL\_DMA\_SELECT\_SSI1\_TX\_REQ                 | SPI1發送          |
|SYSCTL\_DMA\_SELECT\_SSI2\_RX\_REQ                 | SPI2接收          |
|SYSCTL\_DMA\_SELECT\_SSI2\_TX\_REQ                 | SPI2發送          |
|SYSCTL\_DMA\_SELECT\_SSI3\_RX\_REQ                 | SPI3接收          |
|SYSCTL\_DMA\_SELECT\_SSI3\_TX\_REQ                 | SPI3發送          |
|SYSCTL\_DMA\_SELECT\_I2C0\_RX\_REQ                 | I2C0接收          |
|SYSCTL\_DMA\_SELECT\_I2C0\_TX\_REQ                 | I2C0發送          |
|SYSCTL\_DMA\_SELECT\_I2C1\_RX\_REQ                 | I2C1接收          |
|SYSCTL\_DMA\_SELECT\_I2C1\_TX\_REQ                 | I2C1發送          |
|SYSCTL\_DMA\_SELECT\_I2C2\_RX\_REQ                 | I2C2接收          |
|SYSCTL\_DMA\_SELECT\_I2C2\_TX\_REQ                 | I2C2發送          |
|SYSCTL\_DMA\_SELECT\_UART1\_RX\_REQ                | UART1接收         |
|SYSCTL\_DMA\_SELECT\_UART1\_TX\_REQ                | UART1發送         |
|SYSCTL\_DMA\_SELECT\_UART2\_RX\_REQ                | UART2接收         |
|SYSCTL\_DMA\_SELECT\_UART2\_TX\_REQ                | UART2發送         |
|SYSCTL\_DMA\_SELECT\_UART3\_RX\_REQ                | UART3接收         |
|SYSCTL\_DMA\_SELECT\_UART3\_TX\_REQ                | UART3發送         |
|SYSCTL\_DMA\_SELECT\_AES\_REQ                      | AES               |
|SYSCTL\_DMA\_SELECT\_SHA\_RX\_REQ                  | SHA接收           |
|SYSCTL\_DMA\_SELECT\_AI\_RX\_REQ                   | AI接收            |
|SYSCTL\_DMA\_SELECT\_FFT\_RX\_REQ                  | FFT接收           |
|SYSCTL\_DMA\_SELECT\_FFT\_TX\_REQ                  | FFT發送           |
|SYSCTL\_DMA\_SELECT\_I2S0\_TX\_REQ                 | I2S0發送          |
|SYSCTL\_DMA\_SELECT\_I2S0\_RX\_REQ                 | I2S0接收          |
|SYSCTL\_DMA\_SELECT\_I2S1\_TX\_REQ                 | I2S1發送          |
|SYSCTL\_DMA\_SELECT\_I2S1\_RX\_REQ                 | I2S1接收          |
|SYSCTL\_DMA\_SELECT\_I2S2\_TX\_REQ                 | I2S2發送          |
|SYSCTL\_DMA\_SELECT\_I2S2\_RX\_REQ                 | I2S2接收          |

### sysctl\_power\_bank\_t

#### 描述

電源域編號。

#### 定義

```c
typedef enum _sysctl_power_bank
{
    SYSCTL_POWER_BANK0,
    SYSCTL_POWER_BANK1,
    SYSCTL_POWER_BANK2,
    SYSCTL_POWER_BANK3,
    SYSCTL_POWER_BANK4,
    SYSCTL_POWER_BANK5,
    SYSCTL_POWER_BANK6,
    SYSCTL_POWER_BANK7,
    SYSCTL_POWER_BANK_MAX,
} sysctl_power_bank_t;
```

#### 成員

| 成員名稱                              |      描述             |
| :----------------------------------- | :-------------------- |
|SYSCTL\_POWER\_BANK0                  | 電源域0，控制IO0-IO5   |
|SYSCTL\_POWER\_BANK1                  | 電源域1，控制IO6-IO11  |
|SYSCTL\_POWER\_BANK2                  | 電源域2，控制IO12-IO17 |
|SYSCTL\_POWER\_BANK3                  | 電源域3，控制IO18-IO23 |
|SYSCTL\_POWER\_BANK4                  | 電源域4，控制IO24-IO29 |
|SYSCTL\_POWER\_BANK5                  | 電源域5，控制IO30-IO35 |
|SYSCTL\_POWER\_BANK6                  | 電源域6，控制IO36-IO41 |
|SYSCTL\_POWER\_BANK7                  | 電源域7，控制IO42-IO47 |

### sysctl\_io\_power\_mode\_t

#### 描述

IO輸出電壓值。

#### 定義

```c
typedef enum _sysctl_io_power_mode
{
    SYSCTL_POWER_V33,
    SYSCTL_POWER_V18
} sysctl_io_power_mode_t;
```

#### 成員

| 成員名稱                            |      描述             |
| :--------------------------------- | :-------------------- |
|SYSCTL\_POWER\_V33                  | 設置為3.3V             |
|SYSCTL\_POWER\_V18                  | 設置為1.8V             |

### sysctl\_reset\_enum\_status\_t

#### 描述

複位狀態。

#### 定義

```c
typedef enum _sysctl_reset_enum_status
{
    SYSCTL_RESET_STATUS_HARD,
    SYSCTL_RESET_STATUS_SOFT,
    SYSCTL_RESET_STATUS_WDT0,
    SYSCTL_RESET_STATUS_WDT1,
    SYSCTL_RESET_STATUS_MAX,
} sysctl_reset_enum_status_t;
```

#### 成員

| 成員名稱                                     |      描述             |
| :------------------------------------------ | :-------------------- |
|SYSCTL\_RESET\_STATUS\_HARD                  | 硬體複位，重新上電或觸發reset腳位 |
|SYSCTL\_RESET\_STATUS\_SOFT                  | 軟體複位               |
|SYSCTL\_RESET\_STATUS\_WDT0                  | 看門狗0複位            |
|SYSCTL\_RESET\_STATUS\_WDT1                  | 看門狗1複位            |
