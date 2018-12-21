# 直接内存存取控制器(DMAC)

## 概述

直接存储访问 (Direct Memory Access, DMA) 用于在外设与存储器之间以及存储器与存储器之间提供高速数据传输。可以在无需任何 CPU 操作的情况下通过 DMA 快速移动数据，从而提高了CPU 的效率。

## 功能描述

DMA 模块具有以下功能：

- 自动选择一路空闲的 DMA 通道用于传输
- 根据源地址和目标地址自动选择软件或硬件握手协议
- 支持 1、2、4、8 字节的元素大小，源和目标大小不必一致
- 异步或同步传输功能
- 循环传输功能，常用于刷新屏幕或音频录放等场景

## API 参考

对应的头文件 `dmac.h`

为用户提供以下接口

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

#### 函数原型

```c
void dmac_init(void)
```

#### 参数

无。

#### 返回值

无。

### dmac\_set\_single\_mode

#### 描述

设置单路DMA参数。

#### 函数原型

```c
void dmac_set_single_mode(dmac_channel_number_t channel_num, const void *src, void *dest, dmac_address_increment_t src_inc, dmac_address_increment_t dest_inc, dmac_burst_trans_length_t dmac_burst_size, dmac_transfer_width_t dmac_trans_width, size_t block_size)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| channel_num                     | DMA 通道号              | 输入      |
| src                             | 源地址                  | 输入      |
| dest                            | 目标地址                | 输出      |
| src\_inc                        | 源地址是否自增          | 输入      |
| dest\_inc                       | 目标地址是否自增        | 输入      |
| dmac\_burst\_size               | 突发传输数量            | 输入      |
| dmac\_trans\_width              | 单次传输数据位宽         | 输入      |
| block\_size                       | 传输数据的个数           | 输入      |

#### 返回值

无。

### dmac\_is\_done

#### 描述

用于DMAC启动后判断是否完成传输。用于DMAC启动传输后，如果在启动前判断会不准确。

#### 函数原型

```c
int dmac_is_done(dmac_channel_number_t channel_num)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| channel\_num                     | DMA 通道号              | 输入      |

#### 返回值

| 返回值  | 描述     |
| :----  | :--------|
| 0      | 未完成    |
| 1      | 已完成    |

### dmac\_wait\_done

#### 描述

等待DMA完成工作。

#### 函数原型

```c
void dmac_wait_done(dmac_channel_number_t channel_num)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| channel\_num                     | DMA 通道号              | 输入      |

#### 返回值

无。

### dmac\_set\_irq

#### 描述

设置DMAC中断的回调函数

#### 函数原型

```c
void dmac_set_irq(dmac_channel_number_t channel_num , plic_irq_callback_t dmac_callback, void *ctx, uint32_t priority)
```

#### 参数

| 参数名称                       |   描述           |  输入输出  |
| ----------------------------- | ---------------  | --------- |
| channel\_num                  | DMA 通道号        | 输入      |
| dmac\_callback                | 中断回调函数      | 输入      |
| ctx                           | 回调函数的参数    | 输入       |
| priority                      | 中断优先级        | 输入       |

#### 返回值

无。

### dmac\_set\_src\_dest\_length

#### 描述

设置DMAC的源地址、目的地址和长度，然后启动DMAC传输。如果src为NULL则不设置源地址，dest为NULL则不设置目的地址，len<=0则不设置长度。

该函数一般用于DMAC中断中，使DMA继续传输数据，而不必再次设置DMAC的所有参数以节省时间。

#### 函数原型

```c
void dmac_set_src_dest_length(dmac_channel_number_t channel_num, const void *src, void *dest, size_t len)
```

#### 参数

| 参数名称                       |   描述           |  输入输出  |
| ----------------------------- | ---------------  | --------- |
| channel\_num                  | DMA 通道号        | 输入      |
| src                           | 中断回调函数      | 输入      |
| dest                          | 回调函数的参数    | 输入       |
| len                           | 中断优先级        | 输入       |

#### 返回值

无。

### dmac\_is\_idle

#### 描述

判断DMAC当前通道是否空闲，该函数在传输前和传输后都可以用来判断DMAC状态。

#### 函数原型

```c
int dmac_is_idle(dmac_channel_number_t channel_num)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| channel\_num                     | DMA 通道号              | 输入      |

#### 返回值

| 返回值  | 描述     |
| :----  | :--------|
| 0      | 忙       |
| 1      | 空闲     |

### dmac\_wait\_idle

#### 描述

等待DMAC进入空闲状态。

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| channel_num                     | DMA 通道号              | 输入      |

#### 返回值

无。

### 举例

```c
/* I2C通过DMA发送128个int数据 */
uint32_t buf[128];
dmac_wait_idle(SYSCTL_DMA_CHANNEL_0);
sysctl_dma_select(SYSCTL_DMA_CHANNEL_0, SYSCTL_DMA_SELECT_I2C0_TX_REQ);
dmac_set_single_mode(SYSCTL_DMA_CHANNEL_0, buf, (void*)(&i2c_adapter->data_cmd), DMAC_ADDR_INCREMENT, DMAC_ADDR_NOCHANGE, DMAC_MSIZE_4, DMAC_TRANS_WIDTH_32, 128);
dmac_wait_done(SYSCTL_DMA_CHANNEL_0);
```

## 数据类型

相关数据类型、数据结构定义如下：

- dmac\_channel\_number\_t：DMA通道编号。

- dmac\_address\_increment\_t：地址增长方式。

- dmac\_burst\_trans\_length\_t：突发传输数量。

- dmac\_transfer\_width\_t：单次传输数据位数。

### dmac\_channel\_number\_t

#### 描述

DMA通道编号。

#### 定义

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

#### 成员

| 成员名称         | 描述         |
| --------------- | ------------ |
| DMAC\_CHANNEL0  | DMA通道 0     |
| DMAC\_CHANNEL1  | DMA通道 1     |
| DMAC\_CHANNEL2  | DMA通道 2     |
| DMAC\_CHANNEL3  | DMA通道 3     |
| DMAC\_CHANNEL4  | DMA通道 4     |
| DMAC\_CHANNEL5  | DMA通道 5     |

### dmac\_address\_increment\_t

#### 描述

地址增长方式。

#### 定义

```c
typedef enum _dmac_address_increment
{
    DMAC_ADDR_INCREMENT = 0x0,
    DMAC_ADDR_NOCHANGE  = 0x1
} dmac_address_increment_t;
```

#### 成员

| 成员名称                | 描述         |
| ---------------------- | ------------ |
| DMAC\_ADDR\_INCREMENT  | 地址自动增长  |
| DMAC\_ADDR\_NOCHANGE   | 地址不变      |

### dmac\_burst\_trans\_length\_t

#### 描述

突发传输数量。

#### 定义

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

#### 成员

| 成员名称           | 描述              |
| ----------------- | ----------------- |
| DMAC\_MSIZE\_1    | 单次传输数量乘1    |
| DMAC\_MSIZE\_4    | 单次传输数量乘4    |
| DMAC\_MSIZE\_8    | 单次传输数量乘8    |
| DMAC\_MSIZE\_16   | 单次传输数量乘16   |
| DMAC\_MSIZE\_32   | 单次传输数量乘32   |
| DMAC\_MSIZE\_64   | 单次传输数量乘64   |
| DMAC\_MSIZE\_128  | 单次传输数量乘128  |
| DMAC\_MSIZE\_256  | 单次传输数量乘256  |

### dmac\_transfer\_width\_t

#### 描述

单次传输数据位数。

#### 定义

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

#### 成员

| 成员名称                 | 描述              |
| ----------------------- | ----------------- |
| DMAC\_TRANS\_WIDTH\_8   | 单次传输8位        |
| DMAC\_TRANS\_WIDTH\_16  | 单次传输16位       |
| DMAC\_TRANS\_WIDTH\_32  | 单次传输32位       |
| DMAC\_TRANS\_WIDTH\_64  | 单次传输64位       |
| DMAC\_TRANS\_WIDTH\_128 | 单次传输128位      |
| DMAC\_TRANS\_WIDTH\_256 | 单次传输256位      |