# 系统控制

## Summary

系统控制模块提供对操作系统的配置功能。

## Features

系统控制模块具有以下功能：

- 设置 PLL CPU 时钟频率。

- 设置各个模块时钟的分频值。

- 获取各个模块的时钟频率。

- 使能、禁用、复位各个模块。

- 设置DMA请求源。

- 使能禁用系统中断。

## API

Corresponding header file `sysctl.h`

Provide the following interfaces

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

### sysctl\_cpu\_set\_freq

#### Description

设置CPU工作频率。是通过修改PLL0的频率实现的。

#### Function prototype

```c
uint32_t sysctl_cpu_set_freq(uint32_t freq)
```

#### Parameter

| Parameter name     |   Description           |  Input or output  |
| ----------- | ---------------- | --------- |
| freq        | 要设置的频率（Hz） | Input      |

#### Return value

设置后的实际频率（Hz）。

### sysctl\_set\_pll\_frequency

#### Description

设置PLL频率。

#### Function prototype

```c
uint32_t sysctl_pll_set_freq(sysctl_pll_t pll, uint32_t pll_freq)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| pll             | PLL编号          | Input       |
| pll\_freq        | 要设置的频率（Hz）| Input       |

#### Return value

设置后的实际频率（Hz）。

#### Function prototype

```c
uint32_t sysctl_pll_get_freq(sysctl_pll_t pll)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| pll             | PLL编号          | Input       |

#### Return value

对应PLL的频率（Hz）。

### sysctl\_pll\_enable

#### Description

使能对应的PLL。

#### Function prototype

```c
int sysctl_pll_enable(sysctl_pll_t pll)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| pll             | PLL编号          | Input       |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### sysctl\_pll\_disable

#### Description

禁用对应PLL。

#### Function prototype

```c
int sysctl_pll_disable(sysctl_pll_t pll)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| pll             | PLL编号          | Input       |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### sysctl\_clock\_set\_threshold

#### Description

设置对应时钟的分频值。

#### Function prototype

```c
void sysctl_clock_set_threshold(sysctl_threshold_t which, int threshold)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| which           | 设置的时钟        | Input       |
| threshold       | 分频值            | Input       |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### sysctl\_clock\_get\_threshold

#### Description

获取对应时钟的分频值。

#### Function prototype

```c
int sysctl_clock_get_threshold(sysctl_threshold_t which)
```

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| which           | 时钟             | Input       |

#### Return value

对应时钟的分频值。

### sysctl\_clock\_set\_clock\_select

#### Description

设置时钟源。

#### Function prototype

```c
int sysctl_clock_set_clock_select(sysctl_clock_select_t which, int select)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| which           | 时钟             | Input       |
| select          | 时钟源           | Input       |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### sysctl\_clock\_get\_clock\_select

#### Description

获取时钟对应的时钟源。

#### Function prototype

```c
int sysctl_clock_get_clock_select(sysctl_clock_select_t which)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| which           | 时钟             | Input       |

#### Return value

时钟对应的时钟源。

### sysctl\_clock\_get\_freq

#### Description

获取时钟的频率。

#### Function prototype

```c
uint32_t sysctl_clock_get_freq(sysctl_clock_t clock)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| clock           | 时钟             | Input       |

#### Return value

时钟的频率（Hz）

### sysctl\_clock\_enable

#### Description

使能时钟。PLL要使用sysctl\_pll\_enable。

#### Function prototype

```c
int sysctl_clock_enable(sysctl_clock_t clock)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| clock           | 时钟             | Input       |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### sysctl\_clock\_disable

#### Description

禁用时钟，PLL使用sysctl\_pll\_disable。

#### Function prototype

```c
int sysctl_clock_disable(sysctl_clock_t clock)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| clock           | 时钟             | Input       |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### sysctl\_reset

#### Description

复位各个模块。

#### Function prototype

```c
void sysctl_reset(sysctl_reset_t reset)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| reset           | 预复位模块        | Input       |

#### Return value

None.

### sysctl\_dma\_select

#### Description

设置DMA请求源。与DMAC的API配合使用。

#### Function prototype

```c
int sysctl_dma_select(sysctl_dma_channel_t channel, sysctl_dma_select_t select)
```

#### Parameter

| Parameter name         |   Description           |  Input or output  |
| --------------- | ---------------- | --------- |
| channel         | DMA通道号        | Input       |
| select          | DMA请求源        | Input       |

#### Return value

| Return value | Description |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失败 |

### sysctl\_set\_power\_mode

#### Description

设置FPIOA的对应电源域的电压。

#### 原型

```c
void sysctl_set_power_mode(sysctl_power_bank_t power_bank, sysctl_io_power_mode_t io_power_mode)
```

#### Parameter

| Parameter name         |   Description               |  Input or output  |
| --------------- | -------------------- | --------- |
| power\_bank     | IO电源域编号          | Input       |
| io\_power\_mode | 设置的电压值1.8V或3.3V| Input       |

#### Return value

None.

### sysctl\_enable\_irq

#### Description

使能系统中断，如果使用中断一定要开启系统中断。

#### Function prototype

```c
void sysctl_enable_irq(void)
```

#### Parameter

None.

#### Return value

None.

### sysctl\_disable\_irq

#### Description

禁用系统中断。

#### Function prototype

```c
void sysctl_disable_irq(void)
```

#### Parameter

None.

#### Return value

None.

## Data type

The relevant data types and data structures are defined as follows:

- sysctl\_pll\_t：PLL编号。

- sysctl\_threshold\_t：设置分频值时各模块编号。

- sysctl\_clock\_select\_t：设置时钟源时各模块编号。

- sysctl\_clock\_t：各个模块的编号。

- sysctl\_reset\_t：复位时各个模块的编号。

- sysctl\_dma\_channel\_t：DMA通道号。

- sysctl\_dma\_select\_t：DMA请求源编号。

- sysctl\_power\_bank\_t：电源域编号。

- sysctl\_io\_power\_mode\_t：IO输出电压值。

### sysctl\_pll_t

#### Description

PLL编号。

#### Type definition

```c
typedef enum _sysctl_pll_t
{
    SYSCTL_PLL0,
    SYSCTL_PLL1,
    SYSCTL_PLL2,
    SYSCTL_PLL_MAX
} sysctl_pll_t;
```

#### Enumeration element

| Element name             |      Description             |
| :------------------ | :-------------------- |
|SYSCTL\_PLL0         | PLL0                  |
|SYSCTL\_PLL1         | PLL1                  |
|SYSCTL\_PLL2         | PLL2                  |

### sysctl\_threshold\_t

#### Description

设置分频值各模块编号。

#### Type definition

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

#### Enumeration element

| Element name                       |      Description             |
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

#### Description

设置时钟源时各模块编号。

#### Type definition

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

#### Enumeration element

| Element name                                  |      Description             |
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
|SYSCTL\_CLOCK\_SELECT\_SPI3\_SAMPLE       | SPI3数据采样时钟沿选择  |

### sysctl\_clock\_t

#### Description

各个模块的编号。

#### Type definition

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

#### Enumeration element

| Element name                                |      Description        |
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
|SYSCTL\_CLOCK\_IN0                      | 外部Input时钟IN0   |

### sysctl\_reset\_t

#### Description

复位时各个模块的编号。

#### Type definition

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

#### Enumeration element

| Element name                              |      Description         |
| :----------------------------------- | :---------------- |
|SYSCTL\_RESET\_SOC                    | 芯片复位           |
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

#### Description

DMA通道号。

#### Type definition

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

#### Enumeration element

| Element name                               |      Description         |
| :------------------------------------ | :---------------- |
|SYSCTL\_DMA\_CHANNEL\_0                | DMA通道0           |
|SYSCTL\_DMA\_CHANNEL\_1                | DMA通道1           |
|SYSCTL\_DMA\_CHANNEL\_2                | DMA通道2           |
|SYSCTL\_DMA\_CHANNEL\_3                | DMA通道3           |
|SYSCTL\_DMA\_CHANNEL\_4                | DMA通道4           |
|SYSCTL\_DMA\_CHANNEL\_5                | DMA通道5           |

### sysctl\_dma\_select\_t

#### Description

DMA请求源编号。

#### Type definition

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

#### Enumeration element

| Element name                                          |      Description         |
| :------------------------------------------------ | :---------------- |
|SYSCTL\_DMA\_SELECT\_SSI0\_RX\_REQ                 | SPI0接收          |
|SYSCTL\_DMA\_SELECT\_SSI0\_TX\_REQ                 | SPI0发送          |
|SYSCTL\_DMA\_SELECT\_SSI1\_RX\_REQ                 | SPI1接收          |
|SYSCTL\_DMA\_SELECT\_SSI1\_TX\_REQ                 | SPI1发送          |
|SYSCTL\_DMA\_SELECT\_SSI2\_RX\_REQ                 | SPI2接收          |
|SYSCTL\_DMA\_SELECT\_SSI2\_TX\_REQ                 | SPI2发送          |
|SYSCTL\_DMA\_SELECT\_SSI3\_RX\_REQ                 | SPI3接收          |
|SYSCTL\_DMA\_SELECT\_SSI3\_TX\_REQ                 | SPI3发送          |
|SYSCTL\_DMA\_SELECT\_I2C0\_RX\_REQ                 | I2C0接收          |
|SYSCTL\_DMA\_SELECT\_I2C0\_TX\_REQ                 | I2C0发送          |
|SYSCTL\_DMA\_SELECT\_I2C1\_RX\_REQ                 | I2C1接收          |
|SYSCTL\_DMA\_SELECT\_I2C1\_TX\_REQ                 | I2C1发送          |
|SYSCTL\_DMA\_SELECT\_I2C2\_RX\_REQ                 | I2C2接收          |
|SYSCTL\_DMA\_SELECT\_I2C2\_TX\_REQ                 | I2C2发送          |
|SYSCTL\_DMA\_SELECT\_UART1\_RX\_REQ                | UART1接收         |
|SYSCTL\_DMA\_SELECT\_UART1\_TX\_REQ                | UART1发送         |
|SYSCTL\_DMA\_SELECT\_UART2\_RX\_REQ                | UART2接收         |
|SYSCTL\_DMA\_SELECT\_UART2\_TX\_REQ                | UART2发送         |
|SYSCTL\_DMA\_SELECT\_UART3\_RX\_REQ                | UART3接收         |
|SYSCTL\_DMA\_SELECT\_UART3\_TX\_REQ                | UART3发送         |
|SYSCTL\_DMA\_SELECT\_AES\_REQ                      | AES               |
|SYSCTL\_DMA\_SELECT\_SHA\_RX\_REQ                  | SHA接收           |
|SYSCTL\_DMA\_SELECT\_AI\_RX\_REQ                   | AI接收            |
|SYSCTL\_DMA\_SELECT\_FFT\_RX\_REQ                  | FFT接收           |
|SYSCTL\_DMA\_SELECT\_FFT\_TX\_REQ                  | FFT发送           |
|SYSCTL\_DMA\_SELECT\_I2S0\_TX\_REQ                 | I2S0发送          |
|SYSCTL\_DMA\_SELECT\_I2S0\_RX\_REQ                 | I2S0接收          |
|SYSCTL\_DMA\_SELECT\_I2S1\_TX\_REQ                 | I2S1发送          |
|SYSCTL\_DMA\_SELECT\_I2S1\_RX\_REQ                 | I2S1接收          |
|SYSCTL\_DMA\_SELECT\_I2S2\_TX\_REQ                 | I2S2发送          |
|SYSCTL\_DMA\_SELECT\_I2S2\_RX\_REQ                 | I2S2接收          |

### sysctl\_power\_bank\_t

#### Description

电源域编号。

#### Type definition

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

#### Enumeration element

| Element name                              |      Description             |
| :----------------------------------- | :-------------------- |
|SYSCTL\_POWER\_BANK0                  | 电源域0，控制IO0-IO5   |
|SYSCTL\_POWER\_BANK1                  | 电源域1，控制IO6-IO11  |
|SYSCTL\_POWER\_BANK2                  | 电源域2，控制IO12-IO17 |
|SYSCTL\_POWER\_BANK3                  | 电源域3，控制IO18-IO23 |
|SYSCTL\_POWER\_BANK4                  | 电源域4，控制IO24-IO29 |
|SYSCTL\_POWER\_BANK5                  | 电源域5，控制IO30-IO35 |
|SYSCTL\_POWER\_BANK6                  | 电源域6，控制IO36-IO41 |
|SYSCTL\_POWER\_BANK7                  | 电源域7，控制IO42-IO47 |

### sysctl\_io\_power\_mode\_t

#### Description

IOOutput电压值。

#### Type definition

```c
typedef enum _sysctl_io_power_mode
{
    SYSCTL_POWER_V33,
    SYSCTL_POWER_V18
} sysctl_io_power_mode_t;
```

#### Enumeration element

| Element name                            |      Description             |
| :--------------------------------- | :-------------------- |
|SYSCTL\_POWER\_V33                  | 设置为3.3V             |
|SYSCTL\_POWER\_V18                  | 设置为1.8V             |