# 集成电路内置音频总线 (I2S)

## 概述

I2S 标准总线定义了三种信号：时钟信号 BCK、声道选择信号 WS 和串行数据信号 SD。一个基本的I2S 数据总线有一个主机和一个从机。主机和从机的角色在通信过程中保持不变。I2S 模块包含独立的发送和接收声道，能够保证优良的通信性能。

## 功能描述

I2S 模块具有以下功能：

- 根据音频格式自动配置设备（支持 16、24、32 位深，44100 采样率，1 - 4 声道）
- 可配置为播放或录音模式
- 自动管理音频缓冲区

## API 参考

对应的头文件 `i2s.h`

为用户提供以下接口

- i2s\_init
- i2s\_send\_data\_dma
- i2s\_recv\_data\_dma
- i2s\_rx\_channel\_config
- i2s\_tx\_channel\_config
- i2s\_play
- i2s\_set\_sample\_rate
- i2s\_set\_dma\_divide\_16
- i2s\_get\_dma\_divide\_16
- i2s\_handle\_data\_dma

### i2s\_init

#### 描述

初始化I2S。

#### 函数原型

```c
void i2s_init(i2s_device_number_t device_num, i2s_transmit_t rxtx_mode, uint32_t channel_mask)
```

#### 参数

| 成员名称            | 描述         |  输入输出  |
| ------------------ | ------------ | --------- |
| device\_num         | I2S号        | 输入      |
| rxtx\_mode          | 接收或发送模式| 输入      |
| channel\_mask       | 通道掩码      | 输入      |

#### 返回值

无。

### i2s\_send\_data\_dma

#### 描述

I2S发送数据。

#### 函数原型

```c
void i2s_send_data_dma(i2s_device_number_t device_num, const void *buf, size_t buf_len, dmac_channel_number_t channel_num)
```

#### 参数

| 成员名称            | 描述         |  输入输出  |
| ------------------ | ------------ | --------- |
| device\_num         | I2S号        | 输入      |
| buf                | 发送数据地址  | 输入      |
| buf\_len            | 数据长度      | 输入      |
| channel\_num        | DMA通道号     | 输入      |

#### 返回值

无。

### i2s\_recv\_data\_dma

#### 描述

I2S接收数据。

#### 函数原型

```c
void i2s_recv_data_dma(i2s_device_number_t device_num, uint32_t *buf, size_t buf_len, dmac_channel_number_t channel_num)
```

#### 参数

| 成员名称            | 描述         |  输入输出  |
| ------------------  | ------------ | --------- |
| device\_num         | I2S号        | 输入      |
| buf                 | 接收数据地址  | 输出      |
| buf\_len            | 数据长度      | 输入      |
| channel\_num        | DMA通道号     | 输入      |

#### 返回值

无

### i2s\_rx\_channel\_config

#### 描述

设置接收通道参数。

#### 函数原型

```c
void i2s_rx_channel_config(i2s_device_number_t device_num, i2s_channel_num_t channel_num, i2s_word_length_t word_length, i2s_word_select_cycles_t word_select_size, i2s_fifo_threshold_t trigger_level, i2s_work_mode_t word_mode)
```

#### 参数

| 成员名称            | 描述              |  输入输出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | 输入      |
| channel\_num        | 通道号             | 输入     |
| word\_length        | 接收数据位数       | 输出      |
| word\_select\_size   | 单个数据时钟数     | 输入      |
| trigger\_level      | DMA触发时FIFO深度  | 输入      |
| word\_mode          | 工作模式           | 输入      |

#### 返回值

无。

### i2s\_tx\_channel\_config

#### 描述

设置发送通道参数。

#### 函数原型

```c
void i2s_tx_channel_config(i2s_device_number_t device_num, i2s_channel_num_t channel_num, i2s_word_length_t word_length, i2s_word_select_cycles_t word_select_size, i2s_fifo_threshold_t trigger_level, i2s_work_mode_t word_mode)
```

#### 参数

| 成员名称            | 描述              |  输入输出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | 输入      |
| channel\_num        | 通道号             | 输入     |
| word\_length        | 接收数据位数       | 输出      |
| word\_select\_size   | 单个数据时钟数     | 输入      |
| trigger\_level      | DMA触发时FIFO深度  | 输入      |
| word\_mode          | 工作模式           | 输入      |

#### 返回值

无。

### i2s\_play

#### 描述

发送PCM数据, 比如播放音乐

#### 函数原型

```c
void i2s_play(i2s_device_number_t device_num, dmac_channel_number_t channel_num,
              const uint8_t *buf, size_t buf_len, size_t frame, size_t bits_per_sample, uint8_t track_num)
```

#### 参数

| 成员名称            | 描述              |  输入输出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | 输入      |
| channel\_num        | 通道号             | 输入     |
| buf                 | PCM 数据           | 输入      |
| buf\_len             | PCM数据长度        | 输入      |
| frame               | 单次发送数量        | 输入      |
| bits\_per\_sample     | 单次采样位宽        | 输入      |
| track_num           | 声道数            | 输入      |

#### 返回值

无。

### i2s\_set\_sample\_rate

#### 描述

设置采样率。

#### 函数原型

```c
uint32_t i2s_set_sample_rate(i2s_device_number_t device_num, uint32_t sample_rate)
```

#### 参数

| 成员名称            | 描述              |  输入输出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | 输入      |
| sample\_rate        | 采样率            | 输入     |

#### 返回值

实际的采样率。

### i2s\_set\_dma\_divide\_16

#### 描述

设置dma\_divide\_16，16位数据时设置dma\_divide\_16，DMA传输时自动将32比特INT32数据分成两个16比特的左右声道数据。

#### 函数原型

```c
int i2s_set_dma_divide_16(i2s_device_number_t device_num, uint32_t enable)
```

#### 参数

| 成员名称            | 描述              |  输入输出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | 输入      |
| enable              | 0:禁用 1：使能    | 输入     |

#### 返回值

| 返回值              | 描述       |
| :------------------ | :-------- |
| 0                   | 成功      |
| 非0                 | 失败       |

### i2s\_get\_dma\_divide\_16

#### 描述

获取dma\_divide\_16值。用于判断是否需要设置dma\_divide\_16。

#### 函数原型

```c
int i2s_get_dma_divide_16(i2s_device_number_t device_num)
```

#### 参数

| 成员名称            | 描述              |  输入输出  |
| ------------------ | ----------------- | --------- |
| device\_num         | I2S号             | 输入      |

#### 返回值

| 返回值              | 描述       |
| :------------------ | :-------- |
| 1                   | 使能      |
| 0                   | 禁用      |
| <0                 | 失败       |

### i2s\_handle\_data\_dma

#### 描述

I2S通过DMA传输数据。

#### 函数原型

```c
void i2s_handle_data_dma(i2s_device_number_t device_num, i2s_data_t data, plic_interrupt_t *cb);
```

#### 参数

| 参数名称                 |   描述              | 输入输出  |
| :---------------------- | :------------------ | :------- |
| device\_num             | I2S号               | 输入      |
| data                    | I2S数据相关的参数，详见i2s_data_t说明 | 输入 |
| cb                      | dma中断回调函数，如果设置为NULL则为阻塞模式，直至传输完毕后退出函数      | 输入 |

#### 返回值

无

### 举例

```c
/* I2S0 通道0 设置为接收通道，接收16位数据，单次传输32个时钟，FIFO深度为4，标准模式。接收8组数据*/
/* I2S2 通道1 设置为发送通道，发送16位数据，单次传输32个时钟，FIFO深度为4，右对齐模式。发送8组数据*/
uint32_t buf[8];
i2s_init(I2S_DEVICE_0, I2S_RECEIVER, 0x3);
i2s_init(I2S_DEVICE_2, I2S_TRANSMITTER, 0xC);
i2s_rx_channel_config(I2S_DEVICE_0, I2S_CHANNEL_0, RESOLUTION_16_BIT, SCLK_CYCLES_32, TRIGGER_LEVEL_4, STANDARD_MODE);
i2s_tx_channel_config(I2S_DEVICE_2, I2S_CHANNEL_1, RESOLUTION_16_BIT, SCLK_CYCLES_32, TRIGGER_LEVEL_4, RIGHT_JUSTIFYING_MODE);
i2s_recv_data_dma(I2S_DEVICE_0, rx_buf, 8, DMAC_CHANNEL1);
i2s_send_data_dma(I2S_DEVICE_2, buf, 8, DMAC_CHANNEL0);
```

## 数据类型

相关数据类型、数据结构定义如下：

- i2s\_device\_number\_t：I2S编号。

- i2s\_channel\_num\_t：I2S通道号。

- i2s\_transmit\_t：I2S传输模式。

- i2s\_work_mode\_t：I2S工作模式。

- i2s\_word_select\_cycles\_t：I2S单次传输时钟数。

- i2s\_word_length\_t：I2S传输数据位数。

- i2s\_fifo\_threshold\_t：I2S FIFO深度。

- i2s\_data\_t：通过DMA传输时数据相关的参数。

- i2s\_transfer\_mode\_t：I2S传输方式。

### i2s\_device\_number\_t

#### 描述

I2S编号。

#### 定义

```c
typedef enum _i2s_device_number
{
    I2S_DEVICE_0 = 0,
    I2S_DEVICE_1 = 1,
    I2S_DEVICE_2 = 2,
    I2S_DEVICE_MAX
} i2s_device_number_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| I2S\_DEVICE\_0     | I2S 0       |
| I2S\_DEVICE\_1     | I2S 1       |
| I2S\_DEVICE\_2     | I2S 2       |

### i2s\_channel\_num\_t

#### 描述

I2S通道号。

#### 定义

```c
typedef enum _i2s_channel_num
{
    I2S_CHANNEL_0 = 0,
    I2S_CHANNEL_1 = 1,
    I2S_CHANNEL_2 = 2,
    I2S_CHANNEL_3 = 3
} i2s_channel_num_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| I2S\_CHANNEL\_0    | I2S通道0    |
| I2S\_CHANNEL\_1    | I2S通道1    |
| I2S\_CHANNEL\_2    | I2S通道2    |
| I2S\_CHANNEL\_3    | I2S通道3    |

### i2s\_transmit\_t

#### 描述

I2S传输模式。

#### 定义

```c
typedef enum _i2s_transmit
{
    I2S_TRANSMITTER = 0,
    I2S_RECEIVER = 1
} i2s_transmit_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| I2S\_TRANSMITTER   | 发送模式    |
| I2S\_RECEIVER      | 接收模式    |

### i2s\_work_mode\_t

#### 描述

I2S工作模式。

#### 定义

```c
typedef enum _i2s_work_mode
{
    STANDARD_MODE = 1,
    RIGHT_JUSTIFYING_MODE = 2,
    LEFT_JUSTIFYING_MODE = 4
} i2s_work_mode_t;
```

#### 成员

| 成员名称                  | 描述        |
| ------------------------ | ----------- |
| STANDARD_MODE            | 标准模式    |
| RIGHT\_JUSTIFYING\_MODE    | 右对齐模式   |
| LEFT\_JUSTIFYING\_MODE     | 左对齐模式   |

### i2s\_word_select\_cycles\_t

#### 描述

I2S单次传输时钟数。

#### 定义

```c
typedef enum _word_select_cycles
{
    SCLK_CYCLES_16 = 0x0,
    SCLK_CYCLES_24 = 0x1,
    SCLK_CYCLES_32 = 0x2
} i2s_word_select_cycles_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| SCLK\_CYCLES\_16   | 16个时钟    |
| SCLK\_CYCLES\_24   | 24个时钟    |
| SCLK\_CYCLES\_32   | 32个时钟    |

### i2s\_word_length\_t

#### 描述

I2S传输数据位数。

#### 定义

```c
typedef enum _word_length
{
    IGNORE_WORD_LENGTH = 0x0,
    RESOLUTION_12_BIT = 0x1,
    RESOLUTION_16_BIT = 0x2,
    RESOLUTION_20_BIT = 0x3,
    RESOLUTION_24_BIT = 0x4,
    RESOLUTION_32_BIT = 0x5
} i2s_word_length_t;
```

#### 成员

| 成员名称              | 描述        |
| -------------------- | ----------- |
| IGNORE\_WORD\_LENGTH | 忽略长度     |
| RESOLUTION\_12\_BIT  | 12位数据长度 |
| RESOLUTION\_16\_BIT  | 16位数据长度 |
| RESOLUTION\_20\_BIT  | 20位数据长度 |
| RESOLUTION\_24\_BIT  | 24位数据长度 |
| RESOLUTION\_32\_BIT  | 32位数据长度 |

### i2s\_fifo\_threshold\_t

#### 描述

I2S FIFO深度。

#### 定义

```c
typedef enum _fifo_threshold
{
    /* Interrupt trigger when FIFO level is 1 */
    TRIGGER_LEVEL_1 = 0x0,
    /* Interrupt trigger when FIFO level is 2 */
    TRIGGER_LEVEL_2 = 0x1,
    /* Interrupt trigger when FIFO level is 3 */
    TRIGGER_LEVEL_3 = 0x2,
    /* Interrupt trigger when FIFO level is 4 */
    TRIGGER_LEVEL_4 = 0x3,
    /* Interrupt trigger when FIFO level is 5 */
    TRIGGER_LEVEL_5 = 0x4,
    /* Interrupt trigger when FIFO level is 6 */
    TRIGGER_LEVEL_6 = 0x5,
    /* Interrupt trigger when FIFO level is 7 */
    TRIGGER_LEVEL_7 = 0x6,
    /* Interrupt trigger when FIFO level is 8 */
    TRIGGER_LEVEL_8 = 0x7,
    /* Interrupt trigger when FIFO level is 9 */
    TRIGGER_LEVEL_9 = 0x8,
    /* Interrupt trigger when FIFO level is 10 */
    TRIGGER_LEVEL_10 = 0x9,
    /* Interrupt trigger when FIFO level is 11 */
    TRIGGER_LEVEL_11 = 0xa,
    /* Interrupt trigger when FIFO level is 12 */
    TRIGGER_LEVEL_12 = 0xb,
    /* Interrupt trigger when FIFO level is 13 */
    TRIGGER_LEVEL_13 = 0xc,
    /* Interrupt trigger when FIFO level is 14 */
    TRIGGER_LEVEL_14 = 0xd,
    /* Interrupt trigger when FIFO level is 15 */
    TRIGGER_LEVEL_15 = 0xe,
    /* Interrupt trigger when FIFO level is 16 */
    TRIGGER_LEVEL_16 = 0xf
} i2s_fifo_threshold_t;
```

#### 成员

| 成员名称              | 描述         |
| -------------------- | ------------ |
| TRIGGER\_LEVEL\_1    | 1字节FIFO深度 |
| TRIGGER\_LEVEL\_2    | 2字节FIFO深度 |
| TRIGGER\_LEVEL\_3    | 3字节FIFO深度 |
| TRIGGER\_LEVEL\_4    | 4字节FIFO深度 |
| TRIGGER\_LEVEL\_5    | 5字节FIFO深度 |
| TRIGGER\_LEVEL\_6    | 6字节FIFO深度 |
| TRIGGER\_LEVEL\_7    | 7字节FIFO深度 |
| TRIGGER\_LEVEL\_8    | 8字节FIFO深度 |
| TRIGGER\_LEVEL\_9    | 9字节FIFO深度 |
| TRIGGER\_LEVEL\_10   | 10字节FIFO深度|
| TRIGGER\_LEVEL\_11   | 11字节FIFO深度|
| TRIGGER\_LEVEL\_12   | 12字节FIFO深度|
| TRIGGER\_LEVEL\_13   | 13字节FIFO深度|
| TRIGGER\_LEVEL\_14   | 14字节FIFO深度|
| TRIGGER\_LEVEL\_15   | 15字节FIFO深度|
| TRIGGER\_LEVEL\_16   | 16字节FIFO深度|

### i2s\_data\_t

#### 描述

通过DMA传输时数据相关的参数。

#### 定义

```c
typedef struct _i2s_data_t
{
    dmac_channel_number_t tx_channel;
    dmac_channel_number_t rx_channel;
    uint32_t *tx_buf;
    size_t tx_len;
    uint32_t *rx_buf;
    size_t rx_len;
    i2s_transfer_mode_t transfer_mode;
    bool nowait_dma_idle;
    bool wait_dma_done;
} i2s_data_t;
```

#### 成员

| 成员名称                              | 描述                                        |
| :----------------------------------- | :------------------------------------------ |
| tx\_channel                           | 发送时使用的DMA通道号                         |
| rx\_channel                           | 发送时使用的DMA通道号                         |
| tx\_buf                               | 发送的数据                                    |
| tx\_len                               | 发送数据的长度                                |
| rx\_buf                               | 接收的数据                                    |
| rx\_len                               | 接收数据长度                                  |
| transfer\_mode                        | 传输模式，发送或接收                           |
| nowait\_dma\_idle                     | DMA传输前是否等待DMA通道空闲                   |
| wait\_dma\_done                       | DMA传输后是否等待传输完成，如果cb不为空则这个函数无效 |

### i2s\_transfer\_mode\_t

#### 描述

I2S传输方式。

#### 定义

```c
typedef enum _i2s_transfer_mode
{
    I2S_SEND,
    I2S_RECEIVE,
} i2s_transfer_mode_t;
```

#### 成员

| 成员名称                              | 描述                                        |
| :------------------------------------ | :------------------------------------------ |
| I2S\_SEND                             | 发送                                        |
| I2S\_RECEIVE                          | 软件                                        |