# PLIC

## Overview

Platform-Level Interrupt Controller (PLIC).

Any external interrupt source can be individually assigned to an external interrupt on each CPU. This provides great flexibility to adapt to different application needs.

## Features

The PLIC module has the following features:

- Enable or disable interrupts
- Set the interrupt handler
- Configure interrupt priority

## API

Corresponding header file `plic.h`

Provide the following interfaces

- plic\_init

- plic\_irq\_enable

- plic\_irq\_disable

- plic\_set\_priority

- plic\_get\_priority

- plic\_irq\_register

- plic\_irq\_deregister

### plic\_init

#### Description

Initializes PLIC external interrupt.

#### Function prototype

```c
void plic_init(void)
```

#### Parameter

None.

#### Return value

None.

### plic\_irq\_enable

#### Description

Enable external interrupts.

#### Function prototype

```c
int plic_irq_enable(plic_irq_t irq_number)
```

#### Parameter

| Parameter name |   Description    | Input or output |
| :------------: | :--------------- | :-------------: |
|  irq\_number   | Interrupt number |      Input      |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### plic\_irq\_disable

#### Description

Disable external interrupts.

#### Function prototype

```c
int plic_irq_disable(plic_irq_t irq_number)
```

#### Parameter

| Parameter name |   Description    | Input or output |
| :------------: | :--------------- | :-------------: |
|  irq\_number   | Interrupt number |      Input      |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### plic\_set\_priority

#### Description

Set the interrupt priority.

#### Function prototype

```c
int plic_set_priority(plic_irq_t irq_number, uint32_t priority)
```

#### Parameter

| Parameter name |    Description     | Input or output |
| :------------- | :----------------- | :-------------: |
| irq\_number    | Interrupt number   |      Input      |
| priority       | Interrupt priority |      Input      |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### plic\_get\_priority

#### Description

Get the interrupt priority.

#### Function prototype

```c
uint32_t plic_get_priority(plic_irq_t irq_number)
```

#### Parameter

| Parameter name |   Description    | Input or output |
| :------------- | :--------------- | :-------------- |
| irq\_number    | Interrupt number | Input           |

#### Return value

The priority of the interrupt whose interrupt number is irq_number.

### plic\_irq\_register

#### Description

Register an external interrupt function.

#### Function prototype

```c
int plic_irq_register(plic_irq_t irq, plic_irq_callback_t callback, void* ctx)
```

#### Parameter

| Parameter name |          Description           | Input or output |
| :------------: | :----------------------------- | :-------------: |
|      irq       | Interrupt number               |      Input      |
|    callback    | Interrupt callback function    |      Input      |
|      ctx       | Parameter of callback function |      Input      |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### plic\_irq\_deregister

#### Description

Deregister the external interrupt function.

#### Function prototype

```c
int plic_irq_deregister(plic_irq_t irq)
```

#### Parameter

| Parameter name |   Description    | Input or output |
| :------------: | :--------------- | :-------------: |
|      irq       | Interrupt number |      Input      |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | Success     |
| Others       | Fail        |

### Example

```c
/* Set the trigger interrupt of GPIOHS0 */
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

## Data type

The relevant data types and data structures are defined as follows:

- plic\_irq\_t: External interrupt number.

- plic\_irq\_callback\_t: External interrupt callback function.

### plic\_irq\_t

#### Description

External interrupt number.

#### Type definition

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

#### Enumeration element

|        Element name         |           Description           |
| --------------------------- | ------------------------------- |
| IRQN\_NO\_INTERRUPT         | The non-existent interrupt      |
| IRQN\_SPI0\_INTERRUPT       | SPI0 interrupt                  |
| IRQN\_SPI1\_INTERRUPT       | SPI1 interrupt                  |
| IRQN\_SPI\_SLAVE\_INTERRUPT | SPI_SLAVE interrupt             |
| IRQN\_SPI3\_INTERRUPT       | SPI3 interrupt                  |
| IRQN\_I2S0\_INTERRUPT       | I2S0 interrupt                  |
| IRQN\_I2S1\_INTERRUPT       | I2S1 interrupt                  |
| IRQN\_I2S2\_INTERRUPT       | I2S2 interrupt                  |
| IRQN\_I2C0\_INTERRUPT       | I2C0 interrupt                  |
| IRQN\_I2C1\_INTERRUPT       | I2C1 interrupt                  |
| IRQN\_I2C2\_INTERRUPT       | I2C2 interrupt                  |
| IRQN\_UART1\_INTERRUPT      | UART1 interrupt                 |
| IRQN\_UART2\_INTERRUPT      | UART2 interrupt                 |
| IRQN\_UART3\_INTERRUPT      | UART3 interrupt                 |
| IRQN\_TIMER0A\_INTERRUPT    | TIMER0 channel 0 or 1 interrupt |
| IRQN\_TIMER0B\_INTERRUPT    | TIMER0 channel 2 or 3 interrupt |
| IRQN\_TIMER1A\_INTERRUPT    | TIMER1 channel 0 or 1 interrupt |
| IRQN\_TIMER1B\_INTERRUPT    | TIMER1 channel 2 or 3 interrupt |
| IRQN\_TIMER2A\_INTERRUPT    | TIMER2 channel 0 or 1 interrupt |
| IRQN\_TIMER2B\_INTERRUPT    | TIMER2 channel 2 or 3 interrupt |
| IRQN\_RTC\_INTERRUPT        | RTC tick and alarm interrupt    |
| IRQN\_WDT0\_INTERRUPT       | Watching dog timer0 interrupt   |
| IRQN\_WDT1\_INTERRUPT       | Watching dog timer1 interrupt   |
| IRQN\_APB\_GPIO\_INTERRUPT  | APB GPIO interrupt              |
| IRQN\_DVP\_INTERRUPT        | Digital video port interrupt    |
| IRQN\_AI\_INTERRUPT         | AI accelerator interrupt        |
| IRQN\_FFT\_INTERRUPTFFT     | FFT accelerator interrupt       |
| IRQN\_DMA0\_INTERRUPT       | DMA channel0 interrupt          |
| IRQN\_DMA1\_INTERRUPT       | DMA channel1 interrupt          |
| IRQN\_DMA2\_INTERRUPT       | DMA channel2 interrupt          |
| IRQN\_DMA3\_INTERRUPT       | DMA channel3 interrupt          |
| IRQN\_DMA4\_INTERRUPT       | DMA channel4 interrupt          |
| IRQN\_DMA5\_INTERRUPT       | DMA channel5 interrupt          |
| IRQN\_UARTHS\_INTERRUPT     | Hi-speed UART0 interrupt        |
| IRQN\_GPIOHS0\_INTERRUPT    | Hi-speed GPIO0 interrupt        |
| IRQN\_GPIOHS1\_INTERRUPT    | Hi-speed GPIO1 interrupt        |
| IRQN\_GPIOHS2\_INTERRUPT    | Hi-speed GPIO2 interrupt        |
| IRQN\_GPIOHS3\_INTERRUPT    | Hi-speed GPIO3 interrupt        |
| IRQN\_GPIOHS4\_INTERRUPT    | Hi-speed GPIO4 interrupt        |
| IRQN\_GPIOHS5\_INTERRUPT    | Hi-speed GPIO5 interrupt        |
| IRQN\_GPIOHS6\_INTERRUPT    | Hi-speed GPIO6 interrupt        |
| IRQN\_GPIOHS7\_INTERRUPT    | Hi-speed GPIO7 interrupt        |
| IRQN\_GPIOHS8\_INTERRUPT    | Hi-speed GPIO8 interrupt        |
| IRQN\_GPIOHS9\_INTERRUPT    | Hi-speed GPIO9 interrupt        |
| IRQN\_GPIOHS10\_INTERRUPT   | Hi-speed GPIO10 interrupt       |
| IRQN\_GPIOHS11\_INTERRUPT   | Hi-speed GPIO11 interrupt       |
| IRQN\_GPIOHS12\_INTERRUPT   | Hi-speed GPIO12 interrupt       |
| IRQN\_GPIOHS13\_INTERRUPT   | Hi-speed GPIO13 interrupt       |
| IRQN\_GPIOHS14\_INTERRUPT   | Hi-speed GPIO14 interrupt       |
| IRQN\_GPIOHS15\_INTERRUPT   | Hi-speed GPIO15 interrupt       |
| IRQN\_GPIOHS16\_INTERRUPT   | Hi-speed GPIO16 interrupt       |
| IRQN\_GPIOHS17\_INTERRUPT   | Hi-speed GPIO17 interrupt       |
| IRQN\_GPIOHS18\_INTERRUPT   | Hi-speed GPIO18 interrupt       |
| IRQN\_GPIOHS19\_INTERRUPT   | Hi-speed GPIO19 interrupt       |
| IRQN\_GPIOHS20\_INTERRUPT   | Hi-speed GPIO20 interrupt       |
| IRQN\_GPIOHS21\_INTERRUPT   | Hi-speed GPIO21 interrupt       |
| IRQN\_GPIOHS22\_INTERRUPT   | Hi-speed GPIO22 interrupt       |
| IRQN\_GPIOHS23\_INTERRUPT   | Hi-speed GPIO23 interrupt       |
| IRQN\_GPIOHS24\_INTERRUPT   | Hi-speed GPIO24 interrupt       |
| IRQN\_GPIOHS25\_INTERRUPT   | Hi-speed GPIO25 interrupt       |
| IRQN\_GPIOHS26\_INTERRUPT   | Hi-speed GPIO26 interrupt       |
| IRQN\_GPIOHS27\_INTERRUPT   | Hi-speed GPIO27 interrupt       |
| IRQN\_GPIOHS28\_INTERRUPT   | Hi-speed GPIO28 interrupt       |
| IRQN\_GPIOHS29\_INTERRUPT   | Hi-speed GPIO29 interrupt       |
| IRQN\_GPIOHS30\_INTERRUPT   | Hi-speed GPIO30 interrupt       |
| IRQN\_GPIOHS31\_INTERRUPT   | Hi-speed GPIO31 interrupt       |

### plic\_irq\_callback\_t

#### Description

External interrupt callback function.

#### Type definition

```c
typedef int (*plic_irq_callback_t)(void *ctx);
```