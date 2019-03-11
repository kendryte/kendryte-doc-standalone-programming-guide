# 中斷PLIC

## 概述

可以將任一外部中斷源單獨分配到每個 CPU 的外部中斷上。這提供了強大的靈活性，能適應不同的應用需求。

## 功能描述

PLIC 模組具有以下功能：

- 啟用或禁用中斷
- 設置中斷處理程序
- 配置中斷優先順序

## API參考

對應頭文件 `plic.h`  

為用戶提供以下介面

- plic\_init

- plic\_irq\_enable

- plic\_irq\_disable

- plic\_set\_priority

- plic\_get\_priority

- plic\_irq\_register

- plic\_irq\_deregister

### plic\_init

#### 描述

PLIC初始化外部中斷。

#### 函數原型

```c
void plic_init(void)
```

#### 參數

無。

#### 返回值

無。

### plic\_irq\_enable

#### 描述

啟動外部中斷。

#### 函數原型

```c
int plic_irq_enable(plic_irq_t irq_number)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------:   | :-----     | :----:     |
| irq\_number | 中斷號 | 輸入 |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失敗 |

### plic\_irq\_disable

#### 描述

禁用外部中斷。

#### 函數原型

```c
int plic_irq_disable(plic_irq_t irq_number)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------:   | :-----     | :----:     |
| irq\_number | 中斷號 | 輸入 |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失敗 |

### plic\_set\_priority

#### 描述

設置中斷優先順序。

#### 函數原型

```c
int plic_set_priority(plic_irq_t irq_number, uint32_t priority)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| irq\_number | 中斷號 | 輸入 |
| priority | 中斷優先順序 | 輸入 |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失敗 |

### plic\_get\_priority

#### 描述

獲取中斷優先順序。

#### 函數原型

```c
uint32_t plic_get_priority(plic_irq_t irq_number)
```

#### 參數

| 參數名稱      |   描述     |  輸入輸出  |
| :------------| :----------| :-------- |
| irq\_number  | 中斷號     | 輸入      |

#### 返回值

irq_number中斷的優先順序。

### plic\_irq\_register

#### 描述

註冊外部中斷函數。

#### 函數原型

```c
int plic_irq_register(plic_irq_t irq, plic_irq_callback_t callback, void* ctx)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------:   | :-----     | :----:     |
| irq | 中斷號 | 輸入 |
| callback | 中斷回調函數 | 輸入 |
| ctx | 回調函數的參數 | 輸入 |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失敗 |

### plic\_irq\_deregister

#### 描述

註銷外部中斷函數。

#### 函數原型

```c
int plic_irq_deregister(plic_irq_t irq)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------:   | :-----     | :----:     |
| irq | 中斷號 | 輸入 |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失敗 |

### 舉例

```c
/* 設置GPIOHS0的觸發中斷 */
int count = 0;
int gpiohs_pin_onchange_isr(void *ctx)
{
    int *userdata = (int *)ctx;
    *userdata++;
}
plic_init();
plic_set_priority(IRQN_GPIOHS0_INTERRUPT, 1);
plic_irq_register(IRQN_GPIOHS0_INTERRUPT, gpiohs_pin_onchange_isr, &count);
plic_irq_enable(IRQN_GPIOHS0_INTERRUPT);
sysctl_enable_irq();
```

## 資料類型

相關資料類型、資料結構定義如下：

- plic\_irq\_t：外部中斷號。

- plic\_irq\_callback\_t：外部中斷回調函數。

### plic\_irq\_t

#### 描述

外部中斷號。

#### 定義

```c
typedef enum _plic_irq
{
    IRQN_NO_INTERRUPT        = 0, /*!< The non-existent interrupt */
    IRQN_SPI0_INTERRUPT      = 1, /*!< SPI0 interrupt */
    IRQN_SPI1_INTERRUPT      = 2, /*!< SPI1 interrupt */
    IRQN_SPI_SLAVE_INTERRUPT = 3, /*!< SPI_SLAVE interrupt */
    IRQN_SPI3_INTERRUPT      = 4, /*!< SPI3 interrupt */
    IRQN_I2S0_INTERRUPT      = 5, /*!< I2S0 interrupt */
    IRQN_I2S1_INTERRUPT      = 6, /*!< I2S1 interrupt */
    IRQN_I2S2_INTERRUPT      = 7, /*!< I2S2 interrupt */
    IRQN_I2C0_INTERRUPT      = 8, /*!< I2C0 interrupt */
    IRQN_I2C1_INTERRUPT      = 9, /*!< I2C1 interrupt */
    IRQN_I2C2_INTERRUPT      = 10, /*!< I2C2 interrupt */
    IRQN_UART1_INTERRUPT     = 11, /*!< UART1 interrupt */
    IRQN_UART2_INTERRUPT     = 12, /*!< UART2 interrupt */
    IRQN_UART3_INTERRUPT     = 13, /*!< UART3 interrupt */
    IRQN_TIMER0A_INTERRUPT   = 14, /*!< TIMER0 channel 0 or 1 interrupt */
    IRQN_TIMER0B_INTERRUPT   = 15, /*!< TIMER0 channel 2 or 3 interrupt */
    IRQN_TIMER1A_INTERRUPT   = 16, /*!< TIMER1 channel 0 or 1 interrupt */
    IRQN_TIMER1B_INTERRUPT   = 17, /*!< TIMER1 channel 2 or 3 interrupt */
    IRQN_TIMER2A_INTERRUPT   = 18, /*!< TIMER2 channel 0 or 1 interrupt */
    IRQN_TIMER2B_INTERRUPT   = 19, /*!< TIMER2 channel 2 or 3 interrupt */
    IRQN_RTC_INTERRUPT       = 20, /*!< RTC tick and alarm interrupt */
    IRQN_WDT0_INTERRUPT      = 21, /*!< Watching dog timer0 interrupt */
    IRQN_WDT1_INTERRUPT      = 22, /*!< Watching dog timer1 interrupt */
    IRQN_APB_GPIO_INTERRUPT  = 23, /*!< APB GPIO interrupt */
    IRQN_DVP_INTERRUPT       = 24, /*!< Digital video port interrupt */
    IRQN_AI_INTERRUPT        = 25, /*!< AI accelerator interrupt */
    IRQN_FFT_INTERRUPT       = 26, /*!< FFT accelerator interrupt */
    IRQN_DMA0_INTERRUPT      = 27, /*!< DMA channel0 interrupt */
    IRQN_DMA1_INTERRUPT      = 28, /*!< DMA channel1 interrupt */
    IRQN_DMA2_INTERRUPT      = 29, /*!< DMA channel2 interrupt */
    IRQN_DMA3_INTERRUPT      = 30, /*!< DMA channel3 interrupt */
    IRQN_DMA4_INTERRUPT      = 31, /*!< DMA channel4 interrupt */
    IRQN_DMA5_INTERRUPT      = 32, /*!< DMA channel5 interrupt */
    IRQN_UARTHS_INTERRUPT    = 33, /*!< Hi-speed UART0 interrupt */
    IRQN_GPIOHS0_INTERRUPT   = 34, /*!< Hi-speed GPIO0 interrupt */
    IRQN_GPIOHS1_INTERRUPT   = 35, /*!< Hi-speed GPIO1 interrupt */
    IRQN_GPIOHS2_INTERRUPT   = 36, /*!< Hi-speed GPIO2 interrupt */
    IRQN_GPIOHS3_INTERRUPT   = 37, /*!< Hi-speed GPIO3 interrupt */
    IRQN_GPIOHS4_INTERRUPT   = 38, /*!< Hi-speed GPIO4 interrupt */
    IRQN_GPIOHS5_INTERRUPT   = 39, /*!< Hi-speed GPIO5 interrupt */
    IRQN_GPIOHS6_INTERRUPT   = 40, /*!< Hi-speed GPIO6 interrupt */
    IRQN_GPIOHS7_INTERRUPT   = 41, /*!< Hi-speed GPIO7 interrupt */
    IRQN_GPIOHS8_INTERRUPT   = 42, /*!< Hi-speed GPIO8 interrupt */
    IRQN_GPIOHS9_INTERRUPT   = 43, /*!< Hi-speed GPIO9 interrupt */
    IRQN_GPIOHS10_INTERRUPT  = 44, /*!< Hi-speed GPIO10 interrupt */
    IRQN_GPIOHS11_INTERRUPT  = 45, /*!< Hi-speed GPIO11 interrupt */
    IRQN_GPIOHS12_INTERRUPT  = 46, /*!< Hi-speed GPIO12 interrupt */
    IRQN_GPIOHS13_INTERRUPT  = 47, /*!< Hi-speed GPIO13 interrupt */
    IRQN_GPIOHS14_INTERRUPT  = 48, /*!< Hi-speed GPIO14 interrupt */
    IRQN_GPIOHS15_INTERRUPT  = 49, /*!< Hi-speed GPIO15 interrupt */
    IRQN_GPIOHS16_INTERRUPT  = 50, /*!< Hi-speed GPIO16 interrupt */
    IRQN_GPIOHS17_INTERRUPT  = 51, /*!< Hi-speed GPIO17 interrupt */
    IRQN_GPIOHS18_INTERRUPT  = 52, /*!< Hi-speed GPIO18 interrupt */
    IRQN_GPIOHS19_INTERRUPT  = 53, /*!< Hi-speed GPIO19 interrupt */
    IRQN_GPIOHS20_INTERRUPT  = 54, /*!< Hi-speed GPIO20 interrupt */
    IRQN_GPIOHS21_INTERRUPT  = 55, /*!< Hi-speed GPIO21 interrupt */
    IRQN_GPIOHS22_INTERRUPT  = 56, /*!< Hi-speed GPIO22 interrupt */
    IRQN_GPIOHS23_INTERRUPT  = 57, /*!< Hi-speed GPIO23 interrupt */
    IRQN_GPIOHS24_INTERRUPT  = 58, /*!< Hi-speed GPIO24 interrupt */
    IRQN_GPIOHS25_INTERRUPT  = 59, /*!< Hi-speed GPIO25 interrupt */
    IRQN_GPIOHS26_INTERRUPT  = 60, /*!< Hi-speed GPIO26 interrupt */
    IRQN_GPIOHS27_INTERRUPT  = 61, /*!< Hi-speed GPIO27 interrupt */
    IRQN_GPIOHS28_INTERRUPT  = 62, /*!< Hi-speed GPIO28 interrupt */
    IRQN_GPIOHS29_INTERRUPT  = 63, /*!< Hi-speed GPIO29 interrupt */
    IRQN_GPIOHS30_INTERRUPT  = 64, /*!< Hi-speed GPIO30 interrupt */
    IRQN_GPIOHS31_INTERRUPT  = 65, /*!< Hi-speed GPIO31 interrupt */
    IRQN_MAX
} plic_irq_t;
```

#### 成員

| 成員名稱      | 描述  |
| ------------ | ------------ |
|IRQN\_NO\_INTERRUPT|不存在                 |
|IRQN\_SPI0\_INTERRUPT|SPI0中斷             |
|IRQN\_SPI1\_INTERRUPT|SPI1中斷             |
|IRQN\_SPI\_SLAVE\_INTERRUPT|從SPI中斷      |
|IRQN\_SPI3\_INTERRUPT|SPI3中斷             |
|IRQN\_I2S0\_INTERRUPT|I2S0 中斷            |
|IRQN\_I2S1\_INTERRUPT|I2S1 中斷            |
|IRQN\_I2S2\_INTERRUPT|I2S2 中斷            |
|IRQN\_I2C0\_INTERRUPT|I2C0 中斷            |
|IRQN\_I2C1\_INTERRUPT|I2C1 中斷            |
|IRQN\_I2C2\_INTERRUPT|I2C2 中斷            |
|IRQN\_UART1\_INTERRUPT|UART1中斷           |
|IRQN\_UART2\_INTERRUPT|UART2中斷           |
|IRQN\_UART3\_INTERRUPT|UART3中斷           |
|IRQN\_TIMER0A\_INTERRUPT|TIMER0通道0和1中斷|
|IRQN\_TIMER0B\_INTERRUPT|TIMER0通道2和3中斷|
|IRQN\_TIMER1A\_INTERRUPT|TIMER1通道0和1中斷|
|IRQN\_TIMER1B\_INTERRUPT|TIMER1通道2和3中斷|
|IRQN\_TIMER2A\_INTERRUPT|TIMER2通道0和1中斷|
|IRQN\_TIMER2B\_INTERRUPT|TIMER2通道2和3中斷|
|IRQN\_RTC\_INTERRUPT|RTC 滴答中斷和報警中斷|
|IRQN\_WDT0\_INTERRUPT|看門狗0中斷          |
|IRQN\_WDT1\_INTERRUPT|看門狗1中斷          |
|IRQN\_APB\_GPIO\_INTERRUPT|普通GPIO中斷    |
|IRQN\_DVP\_INTERRUPT|數位攝像頭（DVP）中斷 |
|IRQN\_AI\_INTERRUPT|AI 加速器中斷          |
|IRQN\_FFT\_INTERRUPTFFT |傅立葉加速器中斷  |
|IRQN\_DMA0\_INTERRUPT|DMA 通道0中斷        |
|IRQN\_DMA1\_INTERRUPT|DMA 通道1中斷        |
|IRQN\_DMA2\_INTERRUPT|DMA 通道2中斷        |
|IRQN\_DMA3\_INTERRUPT|DMA 通道3中斷        |
|IRQN\_DMA4\_INTERRUPT|DMA 通道4中斷        |
|IRQN\_DMA5\_INTERRUPT|DMA 通道5中斷        |
|IRQN\_UARTHS\_INTERRUPT|高速UART中斷       |
|IRQN\_GPIOHS0\_INTERRUPT|高速GPIO0中斷     |
|IRQN\_GPIOHS1\_INTERRUPT|高速GPIO1中斷     |
|IRQN\_GPIOHS2\_INTERRUPT|高速GPIO2中斷     |
|IRQN\_GPIOHS3\_INTERRUPT|高速GPIO3中斷     |
|IRQN\_GPIOHS4\_INTERRUPT|高速GPIO4中斷     |
|IRQN\_GPIOHS5\_INTERRUPT|高速GPIO5中斷     |
|IRQN\_GPIOHS6\_INTERRUPT|高速GPIO6中斷     |
|IRQN\_GPIOHS7\_INTERRUPT|高速GPIO7中斷     |
|IRQN\_GPIOHS8\_INTERRUPT|高速GPIO8中斷     |
|IRQN\_GPIOHS9\_INTERRUPT|高速GPIO9中斷     |
|IRQN\_GPIOHS10\_INTERRUPT|高速GPIO10中斷   |
|IRQN\_GPIOHS11\_INTERRUPT|高速GPIO11中斷   |
|IRQN\_GPIOHS12\_INTERRUPT|高速GPIO12中斷   |
|IRQN\_GPIOHS13\_INTERRUPT|高速GPIO13中斷   |
|IRQN\_GPIOHS14\_INTERRUPT|高速GPIO14中斷   |
|IRQN\_GPIOHS15\_INTERRUPT|高速GPIO15中斷   |
|IRQN\_GPIOHS16\_INTERRUPT|高速GPIO16中斷   |
|IRQN\_GPIOHS17\_INTERRUPT|高速GPIO17中斷   |
|IRQN\_GPIOHS18\_INTERRUPT|高速GPIO18中斷   |
|IRQN\_GPIOHS19\_INTERRUPT|高速GPIO19中斷   |
|IRQN\_GPIOHS20\_INTERRUPT|高速GPIO20中斷   |
|IRQN\_GPIOHS21\_INTERRUPT|高速GPIO21中斷   |
|IRQN\_GPIOHS22\_INTERRUPT|高速GPIO22中斷   |
|IRQN\_GPIOHS23\_INTERRUPT|高速GPIO23中斷   |
|IRQN\_GPIOHS24\_INTERRUPT|高速GPIO24中斷   |
|IRQN\_GPIOHS25\_INTERRUPT|高速GPIO25中斷   |
|IRQN\_GPIOHS26\_INTERRUPT|高速GPIO26中斷   |
|IRQN\_GPIOHS27\_INTERRUPT|高速GPIO27中斷   |
|IRQN\_GPIOHS28\_INTERRUPT|高速GPIO28中斷   |
|IRQN\_GPIOHS29\_INTERRUPT|高速GPIO29中斷   |
|IRQN\_GPIOHS30\_INTERRUPT|高速GPIO30中斷   |
|IRQN\_GPIOHS31\_INTERRUPT|高速GPIO31中斷   |

### plic\_irq\_callback\_t

#### 描述

外部中斷回調函數。

#### 定義

```c
typedef int (*plic_irq_callback_t)(void *ctx);
```