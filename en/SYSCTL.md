# SYSCTL

## Overview

The system control (SYSCTL) unit can provide configuration functions for the SoC (system on chip).

## Features

The system control module has the following features:

- Set the PLL CPU clock frequency.
- Set the division value of each module clock.
- Get the clock frequency of each module.
- Enable, disable, reset each module.
- Set the DMA request source.
- Enable or disable system interrupts.

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

Set the CPU operating frequency. It is achieved by modifying the frequency of PLL0.

#### Function prototype

```c
uint32_t sysctl_cpu_set_freq(uint32_t freq)
```

#### Parameter

| Parameter name |       Description        | Input or output |
| -------------- | ------------------------ | --------------- |
| freq           | Frequency to be set (Hz) | Input           |

#### Return value

The actual frequency (Hz) after setting.

### sysctl\_set\_pll\_frequency

#### Description

Set the PLL frequency.

#### Function prototype

```c
uint32_t sysctl_pll_set_freq(sysctl_pll_t pll, uint32_t pll_freq)
```

#### Parameter

| Parameter name |       Description        | Input or output |
| -------------- | ------------------------ | --------------- |
| pll            | PLL number               | Input           |
| pll\_freq      | Frequency to be set (Hz) | Input           |

#### Return value

The actual frequency (Hz) after setting.

#### Function prototype

```c
uint32_t sysctl_pll_get_freq(sysctl_pll_t pll)
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| pll            | PLL number  | Input           |

#### Return value

The frequency of the PLL (Hz).

### sysctl\_pll\_enable

#### Description

Enable the PLL.

#### Function prototype

```c
int sysctl_pll_enable(sysctl_pll_t pll)
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| pll            | PLL number  | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### sysctl\_pll\_disable

#### Description

Disable the PLL.

#### Function prototype

```c
int sysctl_pll_disable(sysctl_pll_t pll)
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| pll            | PLL number  | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### sysctl\_clock\_set\_threshold

#### Description

Set the division value of the clock.

#### Function prototype

```c
void sysctl_clock_set_threshold(sysctl_threshold_t which, int threshold)
```

#### Parameter

| Parameter name |       Description        | Input or output |
| -------------- | ------------------------ | --------------- |
| which          | The clock to be select   | Input           |
| threshold      | Frequency division value | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### sysctl\_clock\_get\_threshold

#### Description

Get the division value of the clock.

#### Function prototype

```c
int sysctl_clock_get_threshold(sysctl_threshold_t which)
```

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| which          | The clock to be select | Input           |

#### Return value

The division value of the clock.

### sysctl\_clock\_set\_clock\_select

#### Description

Set the clock source.

#### Function prototype

```c
int sysctl_clock_set_clock_select(sysctl_clock_select_t which, int select)
```

#### Parameter

| Parameter name |          Description          | Input or output |
| -------------- | ----------------------------- | --------------- |
| which          | The clock to be select        | Input           |
| select         | The clock source to be select | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### sysctl\_clock\_get\_clock\_select

#### Description

Get the clock source corresponding to the clock.

#### Function prototype

```c
int sysctl_clock_get_clock_select(sysctl_clock_select_t which)
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| which          | The clock to be select | Input           |

#### Return value

The clock source corresponding to the clock.

### sysctl\_clock\_get\_freq

#### Description

Get the frequency of the clock.

#### Function prototype

```c
uint32_t sysctl_clock_get_freq(sysctl_clock_t clock)
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| clock          | The clock to be select | Input           |

#### Return value

Clock frequency (Hz)

### sysctl\_clock\_enable

#### Description

Enable the clock. If you enable the PLL you need to use sysctl\_pll\_enable.

#### Function prototype

```c
int sysctl_clock_enable(sysctl_clock_t clock)
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| clock          | The clock to be select | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### sysctl\_clock\_disable

#### Description

Disable the clock. If you disable the PLL you need to use sysctl\_pll\_disable.

#### Function prototype

```c
int sysctl_clock_disable(sysctl_clock_t clock)
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| clock          | The clock to be select | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### sysctl\_reset

#### Description

Reset a peripheral.

#### Function prototype

```c
void sysctl_reset(sysctl_reset_t reset)
```

#### Parameter

| Parameter name |        Description         | Input or output |
| -------------- | -------------------------- | --------------- |
| reset          | The peripheral to be reset | Input           |

#### Return value

None.

### sysctl\_dma\_select

#### Description

Set the DMA request source. Used in conjunction with the DMAC API.

#### Function prototype

```c
int sysctl_dma_select(sysctl_dma_channel_t channel, sysctl_dma_select_t select)
```

#### Parameter

| Parameter name |    Description     | Input or output |
| -------------- | ------------------ | --------------- |
| channel        | DMA channel number | Input           |
| select         | DMA request source | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### sysctl\_set\_power\_mode

#### Description

Select the voltage of the corresponding power domain of the FPIOA.

#### Function prototype

```c
void sysctl_set_power_mode(sysctl_power_bank_t power_bank, sysctl_io_power_mode_t io_power_mode)
```

#### Parameter

| Parameter name  |             Description              | Input or output |
| --------------- | ------------------------------------ | --------------- |
| power\_bank     | IO power domain number               | Input           |
| io\_power\_mode | Select the voltage. 0: 3.3V, 1: 1.8V | Input           |

#### Return value

None.

### sysctl\_enable\_irq

#### Description

Enable system interrupts, if you use interrupts, you must turn on system interrupts.

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

Disable system interrupts.

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

- sysctl\_pll\_t: PLL number.

- sysctl\_threshold\_t: The peripheral number when setting the divider value.

- sysctl\_clock\_select\_t: The peripheral number when setting the clock source.

- sysctl\_clock\_t: The peripheral number when setting the clock.

- sysctl\_reset\_t: The peripheral number when reset.

- sysctl\_dma\_channel\_t: DMA channel number.

- sysctl\_dma\_select\_t: DMA request source number.

- sysctl\_power\_bank\_t: Power domain number.

- sysctl\_io\_power\_mode\_t: IO power domain voltage selection.

### sysctl\_pll_t

#### Description

PLL number.

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

| Element name | Description |
| :----------- | :---------- |
| SYSCTL\_PLL0 | PLL0        |
| SYSCTL\_PLL1 | PLL1        |
| SYSCTL\_PLL2 | PLL2        |

### sysctl\_threshold\_t

#### Description

The peripheral number when setting the divider value.

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

|        Element name        | Description |
| :------------------------- | :---------- |
| SYSCTL\_THRESHOLD\_ACLK    | ACLK        |
| SYSCTL\_THRESHOLD\_APB0    | APB0        |
| SYSCTL\_THRESHOLD\_APB1    | APB1        |
| SYSCTL\_THRESHOLD\_APB2    | ACLK        |
| SYSCTL\_THRESHOLD\_SRAM0   | SRAM0       |
| SYSCTL\_THRESHOLD\_SRAM1   | SRAM1       |
| SYSCTL\_THRESHOLD\_AI      | AI          |
| SYSCTL\_THRESHOLD\_DVP     | DVP         |
| SYSCTL\_THRESHOLD\_ROM     | ROM         |
| SYSCTL\_THRESHOLD\_SPI0    | SPI0        |
| SYSCTL\_THRESHOLD\_SPI1    | SPI1        |
| SYSCTL\_THRESHOLD\_SPI2    | SPI2        |
| SYSCTL\_THRESHOLD\_SPI3    | SPI3        |
| SYSCTL\_THRESHOLD\_TIMER0  | TIMER0      |
| SYSCTL\_THRESHOLD\_TIMER1  | TIMER1      |
| SYSCTL\_THRESHOLD\_TIMER2  | TIMER2      |
| SYSCTL\_THRESHOLD\_I2S0    | I2S0        |
| SYSCTL\_THRESHOLD\_I2S1    | I2S1        |
| SYSCTL\_THRESHOLD\_I2S2    | I2S2        |
| SYSCTL\_THRESHOLD\_I2S0\_M | I2S0 MCLK   |
| SYSCTL\_THRESHOLD\_I2S1\_M | I2S1 MCLK   |
| SYSCTL\_THRESHOLD\_I2S2\_M | I2S2 MCLK   |
| SYSCTL\_THRESHOLD\_I2C0    | I2C0        |
| SYSCTL\_THRESHOLD\_I2C1    | I2C1        |
| SYSCTL\_THRESHOLD\_I2C2    | I2C2        |
| SYSCTL\_THRESHOLD\_WDT0    | WDT0        |
| SYSCTL\_THRESHOLD\_WDT1    | WDT1        |

### sysctl\_clock\_select\_t

#### Description

The peripheral number when setting the clock source.

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

|            Element name             |               Description               |
| :---------------------------------- | :-------------------------------------- |
| SYSCTL\_CLOCK\_SELECT\_PLL0\_BYPASS | PLL0\_BYPASS                            |
| SYSCTL\_CLOCK\_SELECT\_PLL1\_BYPASS | PLL1\_BYPASS                            |
| SYSCTL\_CLOCK\_SELECT\_PLL2\_BYPASS | PLL2\_BYPASS                            |
| SYSCTL\_CLOCK\_SELECT\_PLL2         | PLL2                                    |
| SYSCTL\_CLOCK\_SELECT\_ACLK         | ACLK                                    |
| SYSCTL\_CLOCK\_SELECT\_SPI3         | SPI3                                    |
| SYSCTL\_CLOCK\_SELECT\_TIMER0       | TIMER0                                  |
| SYSCTL\_CLOCK\_SELECT\_TIMER1       | TIMER1                                  |
| SYSCTL\_CLOCK\_SELECT\_TIMER2       | TIMER2                                  |
| SYSCTL\_CLOCK\_SELECT\_SPI3\_SAMPLE | SPI3 data sampling clock edge selection |

### sysctl\_clock\_t

#### Description

The peripheral number when setting the clock.

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

|     Element name      |       Description        |
| :-------------------- | :----------------------- |
| SYSCTL\_CLOCK\_PLL0   | PLL0                     |
| SYSCTL\_CLOCK\_PLL1   | PLL1                     |
| SYSCTL\_CLOCK\_PLL2   | PLL2                     |
| SYSCTL\_CLOCK\_CPU    | CPU                      |
| SYSCTL\_CLOCK\_SRAM0  | SRAM0                    |
| SYSCTL\_CLOCK\_SRAM1  | SRAM1                    |
| SYSCTL\_CLOCK\_APB0   | APB0                     |
| SYSCTL\_CLOCK\_APB1   | APB1                     |
| SYSCTL\_CLOCK\_APB2   | APB2                     |
| SYSCTL\_CLOCK\_ROM    | ROM                      |
| SYSCTL\_CLOCK\_DMA    | DMA                      |
| SYSCTL\_CLOCK\_AI     | AI                       |
| SYSCTL\_CLOCK\_DVP    | DVP                      |
| SYSCTL\_CLOCK\_FFT    | FFT                      |
| SYSCTL\_CLOCK\_GPIO   | GPIO                     |
| SYSCTL\_CLOCK\_SPI0   | SPI0                     |
| SYSCTL\_CLOCK\_SPI1   | SPI1                     |
| SYSCTL\_CLOCK\_SPI2   | SPI2                     |
| SYSCTL\_CLOCK\_SPI3   | SPI3                     |
| SYSCTL\_CLOCK\_I2S0   | I2S0                     |
| SYSCTL\_CLOCK\_I2S1   | I2S1                     |
| SYSCTL\_CLOCK\_I2S2   | I2S2                     |
| SYSCTL\_CLOCK\_I2C0   | I2C0                     |
| SYSCTL\_CLOCK\_I2C1   | I2C1                     |
| SYSCTL\_CLOCK\_I2C2   | I2C2                     |
| SYSCTL\_CLOCK\_UART1  | UART1                    |
| SYSCTL\_CLOCK\_UART2  | UART2                    |
| SYSCTL\_CLOCK\_UART3  | UART3                    |
| SYSCTL\_CLOCK\_AES    | AES                      |
| SYSCTL\_CLOCK\_FPIOA  | FPIOA                    |
| SYSCTL\_CLOCK\_TIMER0 | TIMER0                   |
| SYSCTL\_CLOCK\_TIMER1 | TIMER1                   |
| SYSCTL\_CLOCK\_TIMER2 | TIMER2                   |
| SYSCTL\_CLOCK\_WDT0   | WDT0                     |
| SYSCTL\_CLOCK\_WDT1   | WDT1                     |
| SYSCTL\_CLOCK\_SHA    | SHA                      |
| SYSCTL\_CLOCK\_OTP    | OTP                      |
| SYSCTL\_CLOCK\_RTC    | RTC                      |
| SYSCTL\_CLOCK\_ACLK   | ACLK                     |
| SYSCTL\_CLOCK\_HCLK   | HCLK                     |
| SYSCTL\_CLOCK\_IN0    | External input clock IN0 |

### sysctl\_reset\_t

#### Description

The peripheral number when reset.

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

|     Element name      | Description |
| :-------------------- | :---------- |
| SYSCTL\_RESET\_SOC    | SoC         |
| SYSCTL\_RESET\_ROM    | ROM         |
| SYSCTL\_RESET\_DMA    | DMA         |
| SYSCTL\_RESET\_AI     | AI          |
| SYSCTL\_RESET\_DVP    | DVP         |
| SYSCTL\_RESET\_FFT    | FFT         |
| SYSCTL\_RESET\_GPIO   | GPIO        |
| SYSCTL\_RESET\_SPI0   | SPI0        |
| SYSCTL\_RESET\_SPI1   | SPI1        |
| SYSCTL\_RESET\_SPI2   | SPI2        |
| SYSCTL\_RESET\_SPI3   | SPI3        |
| SYSCTL\_RESET\_I2S0   | I2S0        |
| SYSCTL\_RESET\_I2S1   | I2S1        |
| SYSCTL\_RESET\_I2S2   | I2S2        |
| SYSCTL\_RESET\_I2C0   | I2C0        |
| SYSCTL\_RESET\_I2C1   | I2C1        |
| SYSCTL\_RESET\_I2C2   | I2C2        |
| SYSCTL\_RESET\_UART1  | UART1       |
| SYSCTL\_RESET\_UART2  | UART2       |
| SYSCTL\_RESET\_UART3  | UART3       |
| SYSCTL\_RESET\_AES    | AES         |
| SYSCTL\_RESET\_FPIOA  | FPIOA       |
| SYSCTL\_RESET\_TIMER0 | TIMER0      |
| SYSCTL\_RESET\_TIMER1 | TIMER1      |
| SYSCTL\_RESET\_TIMER2 | TIMER2      |
| SYSCTL\_RESET\_WDT0   | WDT0        |
| SYSCTL\_RESET\_WDT1   | WDT1        |
| SYSCTL\_RESET\_SHA    | SHA         |
| SYSCTL\_RESET\_RTC    | RTC         |

### sysctl\_dma\_channel\_t

#### Description

DMA channel number.

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

|      Element name       |  Description  |
| :---------------------- | :------------ |
| SYSCTL\_DMA\_CHANNEL\_0 | DMA channel 0 |
| SYSCTL\_DMA\_CHANNEL\_1 | DMA channel 1 |
| SYSCTL\_DMA\_CHANNEL\_2 | DMA channel 2 |
| SYSCTL\_DMA\_CHANNEL\_3 | DMA channel 3 |
| SYSCTL\_DMA\_CHANNEL\_4 | DMA channel 4 |
| SYSCTL\_DMA\_CHANNEL\_5 | DMA channel 5 |

### sysctl\_dma\_select\_t

#### Description

DMA request source number.

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

|            Element name             |  Description   |
| :---------------------------------- | :------------- |
| SYSCTL\_DMA\_SELECT\_SSI0\_RX\_REQ  | SPI0 receive   |
| SYSCTL\_DMA\_SELECT\_SSI0\_TX\_REQ  | SPI0 transmit  |
| SYSCTL\_DMA\_SELECT\_SSI1\_RX\_REQ  | SPI1 receive   |
| SYSCTL\_DMA\_SELECT\_SSI1\_TX\_REQ  | SPI1 transmit  |
| SYSCTL\_DMA\_SELECT\_SSI2\_RX\_REQ  | SPI2 receive   |
| SYSCTL\_DMA\_SELECT\_SSI2\_TX\_REQ  | SPI2 transmit  |
| SYSCTL\_DMA\_SELECT\_SSI3\_RX\_REQ  | SPI3 receive   |
| SYSCTL\_DMA\_SELECT\_SSI3\_TX\_REQ  | SPI3 transmit  |
| SYSCTL\_DMA\_SELECT\_I2C0\_RX\_REQ  | I2C0 receive   |
| SYSCTL\_DMA\_SELECT\_I2C0\_TX\_REQ  | I2C0 transmit  |
| SYSCTL\_DMA\_SELECT\_I2C1\_RX\_REQ  | I2C1 receive   |
| SYSCTL\_DMA\_SELECT\_I2C1\_TX\_REQ  | I2C1 transmit  |
| SYSCTL\_DMA\_SELECT\_I2C2\_RX\_REQ  | I2C2 receive   |
| SYSCTL\_DMA\_SELECT\_I2C2\_TX\_REQ  | I2C2 transmit  |
| SYSCTL\_DMA\_SELECT\_UART1\_RX\_REQ | UART1 receive  |
| SYSCTL\_DMA\_SELECT\_UART1\_TX\_REQ | UART1 transmit |
| SYSCTL\_DMA\_SELECT\_UART2\_RX\_REQ | UART2 receive  |
| SYSCTL\_DMA\_SELECT\_UART2\_TX\_REQ | UART2 transmit |
| SYSCTL\_DMA\_SELECT\_UART3\_RX\_REQ | UART3 receive  |
| SYSCTL\_DMA\_SELECT\_UART3\_TX\_REQ | UART3 transmit |
| SYSCTL\_DMA\_SELECT\_AES\_REQ       | AES            |
| SYSCTL\_DMA\_SELECT\_SHA\_RX\_REQ   | SHA receive    |
| SYSCTL\_DMA\_SELECT\_AI\_RX\_REQ    | AI receive     |
| SYSCTL\_DMA\_SELECT\_FFT\_RX\_REQ   | FFT receive    |
| SYSCTL\_DMA\_SELECT\_FFT\_TX\_REQ   | FFT transmit   |
| SYSCTL\_DMA\_SELECT\_I2S0\_TX\_REQ  | I2S0 transmit  |
| SYSCTL\_DMA\_SELECT\_I2S0\_RX\_REQ  | I2S0 receive   |
| SYSCTL\_DMA\_SELECT\_I2S1\_TX\_REQ  | I2S1 transmit  |
| SYSCTL\_DMA\_SELECT\_I2S1\_RX\_REQ  | I2S1 receive   |
| SYSCTL\_DMA\_SELECT\_I2S2\_TX\_REQ  | I2S2 transmit  |
| SYSCTL\_DMA\_SELECT\_I2S2\_RX\_REQ  | I2S2 receive   |

### sysctl\_power\_bank\_t

#### Description

Power domain number.

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

|     Element name     |            Description            |
| :------------------- | :-------------------------------- |
| SYSCTL\_POWER\_BANK0 | Power domain 0，contain IO0-IO5   |
| SYSCTL\_POWER\_BANK1 | Power domain 1，contain IO6-IO11  |
| SYSCTL\_POWER\_BANK2 | Power domain 2，contain IO12-IO17 |
| SYSCTL\_POWER\_BANK3 | Power domain 3，contain IO18-IO23 |
| SYSCTL\_POWER\_BANK4 | Power domain 4，contain IO24-IO29 |
| SYSCTL\_POWER\_BANK5 | Power domain 5，contain IO30-IO35 |
| SYSCTL\_POWER\_BANK6 | Power domain 6，contain IO36-IO41 |
| SYSCTL\_POWER\_BANK7 | Power domain 7，contain IO42-IO47 |

### sysctl\_io\_power\_mode\_t

#### Description

IO power domain voltage selection.

#### Type definition

```c
typedef enum _sysctl_io_power_mode
{
    SYSCTL_POWER_V33,
    SYSCTL_POWER_V18
} sysctl_io_power_mode_t;
```

#### Enumeration element

|    Element name    | Description |
| :----------------- | :---------- |
| SYSCTL\_POWER\_V33 | Set to 3.3V |
| SYSCTL\_POWER\_V18 | Set to 1.8V |