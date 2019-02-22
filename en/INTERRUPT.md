# 中断PLIC

## Summary

可以将任一外部中断源单独分配到每个 CPU 的外部中断上。这提供了强大的灵活性，能适应不同的应用需求。

## Features

PLIC 模块具有以下功能：

- 启用或禁用中断
- 设置中断处理程序
- 配置中断优先级

## API

对应头文件 `plic.h`  

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

PLIC初始化外部中断。

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

使能外部中断。

#### Function prototype

```c
int plic_irq_enable(plic_irq_t irq_number)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------:   | :-----     | :----:     |
| irq\_number | 中断号 | 输入 |

#### Return value

| Return value | Description |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### plic\_irq\_disable

#### Description

禁用外部中断。

#### Function prototype

```c
int plic_irq_disable(plic_irq_t irq_number)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------:   | :-----     | :----:     |
| irq\_number | 中断号 | 输入 |

#### Return value

| Return value | Description |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### plic\_set\_priority

#### Description

设置中断优先级。

#### Function prototype

```c
int plic_set_priority(plic_irq_t irq_number, uint32_t priority)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| irq\_number | 中断号 | 输入 |
| priority | 中断优先级 | 输入 |

#### Return value

| Return value | Description |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### plic\_get\_priority

#### Description

获取中断优先级。

#### Function prototype

```c
uint32_t plic_get_priority(plic_irq_t irq_number)
```

#### Parameter

| Parameter name      |   Description     |  Input or output  |
| :------------| :----------| :-------- |
| irq\_number  | 中断号     | 输入      |

#### Return value

irq_number中断的优先级。

### plic\_irq\_register

#### Description

注册外部中断函数。

#### Function prototype

```c
int plic_irq_register(plic_irq_t irq, plic_irq_callback_t callback, void* ctx)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------:   | :-----     | :----:     |
| irq | 中断号 | 输入 |
| callback | 中断回调函数 | 输入 |
| ctx | 回调函数的参数 | 输入 |

#### Return value

| Return value | Description |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### plic\_irq\_deregister

#### Description

注销外部中断函数。

#### Function prototype

```c
int plic_irq_deregister(plic_irq_t irq)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------:   | :-----     | :----:     |
| irq | 中断号 | 输入 |

#### Return value

| Return value | Description |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失败 |

### Example

```c
/* 设置GPIOHS0的触发中断 */
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

相关数据类型、数据结构定义如下：

- plic\_irq\_t：外部中断号。

- plic\_irq\_callback\_t：外部中断回调函数。

### plic\_irq\_t

#### Description

外部中断号。

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

#### 成员

| 成员名称      | Description  |
| ------------ | ------------ |
|IRQN\_NO\_INTERRUPT|不存在                 |
|IRQN\_SPI0\_INTERRUPT|SPI0中断             |
|IRQN\_SPI1\_INTERRUPT|SPI1中断             |
|IRQN\_SPI\_SLAVE\_INTERRUPT|从SPI中断      |
|IRQN\_SPI3\_INTERRUPT|SPI3中断             |
|IRQN\_I2S0\_INTERRUPT|I2S0 中断            |
|IRQN\_I2S1\_INTERRUPT|I2S1 中断            |
|IRQN\_I2S2\_INTERRUPT|I2S2 中断            |
|IRQN\_I2C0\_INTERRUPT|I2C0 中断            |
|IRQN\_I2C1\_INTERRUPT|I2C1 中断            |
|IRQN\_I2C2\_INTERRUPT|I2C2 中断            |
|IRQN\_UART1\_INTERRUPT|UART1中断           |
|IRQN\_UART2\_INTERRUPT|UART2中断           |
|IRQN\_UART3\_INTERRUPT|UART3中断           |
|IRQN\_TIMER0A\_INTERRUPT|TIMER0通道0和1中断|
|IRQN\_TIMER0B\_INTERRUPT|TIMER0通道2和3中断|
|IRQN\_TIMER1A\_INTERRUPT|TIMER1通道0和1中断|
|IRQN\_TIMER1B\_INTERRUPT|TIMER1通道2和3中断|
|IRQN\_TIMER2A\_INTERRUPT|TIMER2通道0和1中断|
|IRQN\_TIMER2B\_INTERRUPT|TIMER2通道2和3中断|
|IRQN\_RTC\_INTERRUPT|RTC 滴答中断和报警中断|
|IRQN\_WDT0\_INTERRUPT|看门狗0中断          |
|IRQN\_WDT1\_INTERRUPT|看门狗1中断          |
|IRQN\_APB\_GPIO\_INTERRUPT|普通GPIO中断    |
|IRQN\_DVP\_INTERRUPT|数字摄像头（DVP）中断 |
|IRQN\_AI\_INTERRUPT|AI 加速器中断          |
|IRQN\_FFT\_INTERRUPTFFT |傅里叶加速器中断  |
|IRQN\_DMA0\_INTERRUPT|DMA 通道0中断        |
|IRQN\_DMA1\_INTERRUPT|DMA 通道1中断        |
|IRQN\_DMA2\_INTERRUPT|DMA 通道2中断        |
|IRQN\_DMA3\_INTERRUPT|DMA 通道3中断        |
|IRQN\_DMA4\_INTERRUPT|DMA 通道4中断        |
|IRQN\_DMA5\_INTERRUPT|DMA 通道5中断        |
|IRQN\_UARTHS\_INTERRUPT|高速UART中断       |
|IRQN\_GPIOHS0\_INTERRUPT|高速GPIO0中断     |
|IRQN\_GPIOHS1\_INTERRUPT|高速GPIO1中断     |
|IRQN\_GPIOHS2\_INTERRUPT|高速GPIO2中断     |
|IRQN\_GPIOHS3\_INTERRUPT|高速GPIO3中断     |
|IRQN\_GPIOHS4\_INTERRUPT|高速GPIO4中断     |
|IRQN\_GPIOHS5\_INTERRUPT|高速GPIO5中断     |
|IRQN\_GPIOHS6\_INTERRUPT|高速GPIO6中断     |
|IRQN\_GPIOHS7\_INTERRUPT|高速GPIO7中断     |
|IRQN\_GPIOHS8\_INTERRUPT|高速GPIO8中断     |
|IRQN\_GPIOHS9\_INTERRUPT|高速GPIO9中断     |
|IRQN\_GPIOHS10\_INTERRUPT|高速GPIO10中断   |
|IRQN\_GPIOHS11\_INTERRUPT|高速GPIO11中断   |
|IRQN\_GPIOHS12\_INTERRUPT|高速GPIO12中断   |
|IRQN\_GPIOHS13\_INTERRUPT|高速GPIO13中断   |
|IRQN\_GPIOHS14\_INTERRUPT|高速GPIO14中断   |
|IRQN\_GPIOHS15\_INTERRUPT|高速GPIO15中断   |
|IRQN\_GPIOHS16\_INTERRUPT|高速GPIO16中断   |
|IRQN\_GPIOHS17\_INTERRUPT|高速GPIO17中断   |
|IRQN\_GPIOHS18\_INTERRUPT|高速GPIO18中断   |
|IRQN\_GPIOHS19\_INTERRUPT|高速GPIO19中断   |
|IRQN\_GPIOHS20\_INTERRUPT|高速GPIO20中断   |
|IRQN\_GPIOHS21\_INTERRUPT|高速GPIO21中断   |
|IRQN\_GPIOHS22\_INTERRUPT|高速GPIO22中断   |
|IRQN\_GPIOHS23\_INTERRUPT|高速GPIO23中断   |
|IRQN\_GPIOHS24\_INTERRUPT|高速GPIO24中断   |
|IRQN\_GPIOHS25\_INTERRUPT|高速GPIO25中断   |
|IRQN\_GPIOHS26\_INTERRUPT|高速GPIO26中断   |
|IRQN\_GPIOHS27\_INTERRUPT|高速GPIO27中断   |
|IRQN\_GPIOHS28\_INTERRUPT|高速GPIO28中断   |
|IRQN\_GPIOHS29\_INTERRUPT|高速GPIO29中断   |
|IRQN\_GPIOHS30\_INTERRUPT|高速GPIO30中断   |
|IRQN\_GPIOHS31\_INTERRUPT|高速GPIO31中断   |

### plic\_irq\_callback\_t

#### Description

外部中断回调函数。

#### Type definition

```c
typedef int (*plic_irq_callback_t)(void *ctx);
```