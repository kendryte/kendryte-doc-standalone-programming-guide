# 数字摄像头接口 (DVP)

## 概述

DVP 是摄像头接口模块，支持把摄像头输入图像数据转发给 AI 模块或者内存。

## 功能描述

DVP 模块具有以下功能：

- 支持RGB565、RGB422与单通道Y灰度输入模式
- 支持设置帧中断
- 支持设置传输地址
- 支持同时向两个地址写数据（输出格式分别是RGB888与RGB565）
- 支持丢弃不需要处理的帧

## API 参考

对应的头文件 `dvp.h`

为用户提供以下接口

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

#### 函数原型

```c
void dvp_init(uint8_t reg_len)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| reg\_len                         | sccb寄存器长度          | 输入      |

#### 返回值

无

### dvp\_set\_output\_enable

#### 描述

设置输出模式使能或禁用。

#### 函数原型

```c
void dvp_set_output_enable(dvp_output_mode_t index, int enable)
```

#### 参数

| 参数名称         |   描述                 |  输入输出  |
| --------------- | ---------------------- | --------- |
| index           | 图像输出至内存或AI      | 输入      |
| enable          | 0：禁用 1：使能         | 输入      |

#### 返回值

无。

### dvp\_set\_image\_format

#### 描述

设置图像接收模式，RGB或YUV。

#### 函数原型

```c
void dvp_set_image_format(uint32_t format)
```

#### 参数

| 参数名称     |   描述                 |  输入输出  |
| ----------- | ---------------------- | --------- |
| format      | 图像模式<br>DVP\_CFG\_RGB\_FORMAT RGB模式<br>DVP\_CFG\_YUV\_FORMAT YUV模式| 输入      |

#### 返回值

无

### dvp\_set\_image\_size

#### 描述

设置DVP图像采集尺寸。

#### 函数原型

```c
void dvp_set_image_size(uint32_t width, uint32_t height)
```

#### 参数

| 参数名称     |   描述                 |  输入输出  |
| ----------- | ---------------------- | --------- |
| width       | 图像宽度                | 输入      |
| height      | 图像高度                | 输入      |

#### 返回值

无

### dvp\_set\_ai\_addr

#### 描述

设置AI存放图像的地址，供AI模块进行算法处理。

#### 函数原型

```c
void dvp_set_ai_addr(uint32_t r_addr, uint32_t g_addr, uint32_t b_addr)
```

#### 参数

| 参数名称     |   描述                 |  输入输出  |
| ----------- | ---------------------- | --------- |
| r\_addr      | 红色分量地址            | 输入      |
| g\_addr      | 绿色分量地址            | 输入      |
| b\_addr      | 蓝色分量地址            | 输入      |

#### 返回值

无

### dvp\_set\_display\_addr

#### 描述

设置采集图像在内存中的存放地址，可以用来显示。

#### 函数原型

```c
void dvp_set_display_addr(uint32_t addr)
```

#### 参数

| 参数名称     |   描述                 |  输入输出  |
| ----------- | ---------------------- | --------- |
| addr        | 存放图像的内存地址       | 输入      |

#### 返回值

无

### dvp\_config\_interrupt

配置DVP中断类型。

#### 函数原型

```c
void dvp_config_interrupt(uint32_t interrupt, uint8_t enable)
```

#### 描述

设置图像开始和结束中断状态，使能或禁用。

#### 参数

| 参数名称     |   描述                 |  输入输出  |
| ----------- | ---------------------- | --------- |
| interrupt   | 中断类型<br>DVP\_CFG\_START\_INT\_ENABLE 图像开始采集中断<br>DVP\_CFG\_FINISH\_INT\_ENABLE 图像结束采集中断     | 输入      |
| enable      | 0：禁止 1：使能         | 输入      |

#### 返回值

无。

### dvp\_get\_interrupt

#### 描述

判断是否是输入的中断类型。

#### 函数原型

```c
int dvp_get_interrupt(uint32_t interrupt)
```

#### 参数

| 参数名称     |   描述                 |  输入输出  |
| ----------- | ---------------------- | --------- |
| interrupt   | 中断类型<br>DVP\_CFG\_START\_INT\_ENABLE 图像开始采集中断<br>DVP\_CFG\_FINISH\_INT\_ENABLE 图像结束采集中断     | 输入      |

#### 返回值

| 返回值  | 描述  |
| :----  | :----|
| 0      | 否   |
| 非0    | 是   |

### dvp\_clear\_interrupt

#### 描述

清除中断。

#### 函数原型

```c
void dvp_clear_interrupt(uint32_t interrupt)
```

#### 参数

| 参数名称     |   描述                 |  输入输出  |
| ----------- | ---------------------- | --------- |
| interrupt   | 中断类型<br>DVP\_CFG\_START\_INT\_ENABLE 图像开始采集中断<br>DVP\_CFG\_FINISH\_INT\_ENABLE 图像结束采集中断     | 输入      |

#### 返回值

无。

### dvp\_start\_convert

#### 描述

开始采集图像，在确定图像采集开始中断后调用。

#### 函数原型

```c
void dvp_start_convert(void)
```

#### 参数

无。

#### 返回值

无。

### dvp\_enable\_burst

#### 描述

使能突发传输模式。

#### 函数原型

```c
void dvp_enable_burst(void)
```

#### 参数

无。

#### 返回值

无。

### dvp\_disable\_burst

#### 描述

禁用突发传输模式。

#### 函数原型

```c
void dvp_disable_burst(void)
```

#### 参数

无。

#### 返回值

无。

### dvp\_enable\_auto

#### 描述

使能自动接收图像模式。

#### 函数原型

```c
void dvp_enable_auto(void)
```

#### 参数

无。

#### 返回值

无。

### dvp\_disable\_auto

#### 描述

禁用自动接收图像模式。

#### 函数原型

```c
void dvp_disable_auto(void)
```

#### 参数

无。

#### 返回值

无。

### dvp\_sccb\_send\_data

#### 描述

通过sccb发送数据。

#### 函数原型

```c
void dvp_sccb_send_data(uint8_t dev_addr, uint16_t reg_addr, uint8_t reg_data)
```

#### 参数

| 参数名称         |   描述                     |  输入输出  |
| --------------- | -------------------------- | --------- |
| dev\_addr        | 外设图像传感器SCCB地址       | 输入      |
| reg\_addr        | 外设图像传感器寄存器         | 输入      |
| reg\_data        | 发送的数据                  | 输入      |

#### 返回值

无

### dvp\_sccb\_receive\_data

#### 描述

通过SCCB接收数据。

#### 函数原型

```c
uint8_t dvp_sccb_receive_data(uint8_t dev_addr, uint16_t reg_addr)
```

#### 参数

| 参数名称         |   描述                     |  输入输出  |
| --------------- | -------------------------- | --------- |
| dev\_addr        | 外设图像传感器SCCB地址       | 输入      |
| reg\_addr        | 外设图像传感器寄存器         | 输入      |

#### 返回值

读取寄存器的数据。

### dvp\_set\_xclk\_rate

#### 描述

设置xclk的速率。

#### 函数原型

```c
uint32_t dvp_set_xclk_rate(uint32_t xclk_rate)
```

#### 参数

| 参数名称         |   描述                     |  输入输出  |
| --------------- | -------------------------- | --------- |
| xclk\_rate      | xclk的速率                  | 输入      |

#### 返回值

xclk的实际速率。

### dvp\_sccb\_set\_clk\_rate

#### 描述

设置sccb的速率。

#### 函数原型

```c
uint32_t dvp_sccb_set_clk_rate(uint32_t clk_rate)
```

#### 参数

| 参数名称         |   描述                     |  输入输出  |
| --------------- | -------------------------- | --------- |
| clk\_rate       | sccb的速率                  | 输入      |

#### 返回值

| 返回值                   | 描述                |
| :---------------------- | :------------------ |
| 0                       | 失败，设置的速率太低无法满足，请使用I2C |
| 非0                     | 实际的sccb速率       |

### 举例

```c
/* 采集320 * 240的RGB图像数据传输至lcd_gram0, 及0x40600000 0x40612C00 0x40625800 地址处 */
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
/* 通过SCCB向地址0x60的外设0xFF寄存器发送0x01,从寄存器0x1D读取数据 */
dvp_sccb_send_data(0x60, 0xFF, 0x01);
dvp_sccb_receive_data(0x60, 0x1D)
```

## 数据类型

相关数据类型、数据结构定义如下：

- dvp\_output\_mode\_t：DVP输出图像的模式。

### dvp\_output\_mode\_t

#### 描述

DVP输入图像的模式。

#### 定义

```c
typedef enum _dvp_output_mode
{
    DVP_OUTPUT_AI,
    DVP_OUTPUT_DISPLAY,
} dvp_output_mode_t;
```

#### 成员

| 成员名称                | 描述              |
| ---------------------- | ----------------- |
| DVP\_OUTPUT\_AI        | AI输出             |
| DVP\_OUTPUT\_DISPLAY   | 向内存输出用于显示  |