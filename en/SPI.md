# 串行外设接口(SPI)

## Summary

SPI 是一种高速的，全双工，同步的通信总线。

## Features

SPI 模块具有以下功能：

- 独立的 SPI 设备封装外设相关参数
- 自动处理多设备总线争用
- 支持标准、双线、四线、八线模式
- 支持先写后读和全双工读写
- 支持发送一串相同的数据帧，常用于清屏、填充存储扇区等场景

## API

对应的头文件 `spi.h`

为用户提供以下接口

- spi\_init

- spi\_init\_non\_standard

- spi\_send\_data\_standard

- spi\_send\_data\_standard\_dma

- spi\_receive\_data\_standard

- spi\_receive\_data\_standard\_dma

- spi\_send\_data\_multiple

- spi\_send\_data\_multiple\_dma

- spi\_receive\_data\_multiple

- spi\_receive\_data\_multiple\_dma

- spi\_fill\_data\_dma

- spi\_send\_data\_normal\_dma

- spi\_set\_clk\_rate

### spi\_init

#### Description

设置SPI工作模式、多线模式和位宽。

#### Function prototype

```c
void spi_init(spi_device_num_t spi_num, spi_work_mode_t work_mode, spi_frame_format_t frame_format, size_t data_bit_length, uint32_t endian)
```

#### Parameter

| Parameter name            |   Description             |  Input or output  |
| :----------------- | :----------------- | :-------- |
| spi\_num           | SPI号              | 输入       |
| work\_mode         | 极性相位的四种模式   | 输入      |
| frame\_format      | 多线模式            | 输入      |
| data\_bit\_length  | 单次传输的数据的位宽 | 输入      |
| endian             | 大小端<br>0：小端<br>1：大端 | 输入 |

#### Return value

None.

### spi\_config\_non\_standard

#### Description

多线模式下设置指令长度、地址长度、等待时钟数、指令地址传输模式。

#### Function prototype

```c
void spi_init_non_standard(spi_device_num_t spi_num, uint32_t instruction_length, uint32_t address_length, uint32_t wait_cycles, spi_instruction_address_trans_mode_t instruction_address_trans_mode)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI号 | 输入 |
| instruction\_length | 发送指令的位数 | 输入 |
| address\_length | 发送地址的位数 | 输入 |
| wait\_cycles | 等待时钟个数 | 输入 |
| instruction\_address\_trans\_mode | 指令地址传输的方式 | 输入 |

#### Return value

无

### spi\_send\_data\_standard

#### Description

SPI标准模式传输数据。

#### Function prototype

```c
void spi_send_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| tx\_buff | 发送的数据 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### Return value

无

### spi\_send\_data\_standard\_dma

#### Description

SPI标准模式下使用DMA传输数据。

#### Function prototype

```c
void spi_send_data_standard_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| channel\_num | DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| tx\_buff | 发送的数据 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### Return value

无

### spi\_receive\_data\_standard

#### Description

标准模式下接收数据。

#### Function prototype

```c
void spi_receive_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| rx\_buff | 接收的数据 | 输出 |
| rx\_len | 接收数据的长度 | 输入 |

#### Return value

无

### spi\_receive\_data\_standard\_dma

#### Description

标准模式下通过DMA接收数据。

#### Function prototype

```c
void spi_receive_data_standard_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| dma\_send\_channel\_num | 发送指令地址使用的DMA通道号 | 输入 |
| dma\_receive\_channel\_num | 接收数据使用的DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| rx\_buff | 接收的数据 | 输出 |
| rx\_len | 接收数据的长度 | 输入 |

#### Return value

无

### spi\_send\_data\_multiple

#### Description

多线模式发送数据。

#### Function prototype

```c
void spi_send_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, uint8_t *tx_buff, size_t tx_len)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| tx\_buff | 发送的数据 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### Return value

无

### spi\_send\_data\_multiple\_dma

#### Description

多线模式使用DMA发送数据。

#### Function prototype

```c
void spi_send_data_multiple_dma(dmac_channel_number_t channel_num,spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| channel\_num | DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| tx\_buff | 发送的数据 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### Return value

无

### spi\_receive\_data\_multiple

#### Description

多线模式接收数据。

#### Function prototype

```c
void spi_receive_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| rx\_buff | 接收的数据 | 输出 |
| rx\_len | 接收数据的长度 | 输入 |

#### Return value

无

### spi\_receive\_data\_multiple\_dma

#### Description

多线模式通过DMA接收。

#### Function prototype

```c
void spi_receive_data_multiple_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, uint32_t const *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len);
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| dma\_send\_channel\_num | 发送指令地址使用的DMA通道号 | 输入 |
| dma\_receive\_channel\_num | 接收数据使用的DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| cmd\_buff | 外设指令地址数据，没有则设为NULL | 输入 |
| cmd\_len | 外设指令地址数据长度，没有则设为0 | 输入 |
| rx\_buff | 接收的数据 | 输出 |
| rx\_len | 接收数据的长度 | 输入 |

#### Return value

无

### spi\_fill\_data\_dma

#### Description

通过DMA始终发送同一个数据，可以用于刷新数据。

#### Function prototype

```c
void spi_fill_data_dma(dmac_channel_number_t channel_num,spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *tx_buff, size_t tx_len);
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| channel\_num | DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| tx\_buff | 发送的数据,仅发送tx_buff这一个数据，不会自动增加 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |

#### Return value

无

### spi\_send\_data\_normal\_dma

#### Description

通过DMA发送数据。不用设置指令地址。

#### Function prototype

```c
void spi_send_data_normal_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const void *tx_buff, size_t tx_len, spi_transfer_width_t spi_transfer_width)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| channel\_num | DMA通道号 | 输入 |
| spi\_num | SPI号 | 输入 |
| chip\_select | 片选信号 | 输入 |
| tx\_buff | 发送的数据,仅发送tx_buff这一个数据，不会自动增加 | 输入 |
| tx\_len | 发送数据的长度 | 输入 |
| spi\_transfer\_width | 发送数据的位宽 | 输入 |

#### Return value

无

### Example

```c
/* SPI0 工作在MODE0模式 标准SPI模式 单次发送8位数据 */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_0, SPI_FF_STANDARD, 8, 0);
uint8_t cmd[4];
cmd[0] = 0x06;
cmd[1] = 0x01;
cmd[2] = 0x02;
cmd[3] = 0x04;
uint8_t data_buf[4] = {0,1,2,3};
/* SPI0 使用片选0 发送指令0x06 向地址0x010204 发送0，1，2，3 四个字节数据 */
spi_send_data_standard(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 4, data_buf, 4);
/* SPI0 使用片选0 发送指令0x06 地址0x010204 接收4个字节的数据 */
spi_receive_data_standard(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 4, data_buf, 4);

/* SPI0 工作在MODE0模式 四线SPI模式 单次发送8位数据 */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_0, SPI_FF_QUAD, 8, 0);
/* 8位指令长度 32位地址长度 发送指令地址后等待4个clk，指令通过标准SPI方式发送，地址通过四线方式发送 */
spi_init_non_standard(SPI_DEVICE_0, 8, 32, 4, SPI_AITM_ADDR_STANDARD);
uint32 cmd[2];
cmd[0] = 0x06;
cmd[1] = 0x010204;
uint8_t data_buf[4] = {0,1,2,3};
/* SPI0 使用片选0 发送指令0x06 向地址0x010204 发送0，1，2，3 四个字节数据 */
spi_send_data_multiple(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 2, data_buf, 4);
/* SPI0 使用片选0 发送指令0x06 地址0x010204 接收4个字节的数据 */
spi_receive_data_multiple(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 2, data_buf, 4);

/* SPI0 工作在MODE2模式 八线SPI模式 单次发送32位数据 */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_2, SPI_FF_OCTAL, 32, 0);
/* 无指令 32位地址长度 发送指令地址后等待0个clk，指令地址通过8线发送 */
spi_init_non_standard(SPI_DEVICE_0, 0, 32, 0, SPI_AITM_AS_FRAME_FORMAT);
uint32_t data_buf[256] = {0};
/* 使用DMA通道0 片选0 发送256个int数据*/
spi_send_data_normal_dma(DMAC_CHANNEL0, SPI_DEVICE_0, SPI_CHIP_SELECT_0, data_buf, 256, SPI_TRANS_INT);
uint32_t data = 0x55AA55AA;
/* 使用DMA通道0 片选0 连续发送256个 0x55AA55AA*/
spi_fill_data_dma(DMAC_CHANNEL0, SPI_DEVICE_0, SPI_CHIP_SELECT_0,&data, 256);
```

### spi\_set\_clk\_rate

#### Description

设置 SPI 的时钟频率

#### Function prototype

```c
uint32_t spi_set_clk_rate(spi_device_num_t spi_num, uint32_t spi_clk)
```

#### Parameter

| Parameter name     |   Description     |  Input or output  |
| :--------   | :-----     | :----:     |
| spi\_num| SPI号 | 输入 |
| spi\_clk | 目标SPI设备的时钟频率 | 输入 |

#### Return value

设置完后的SPI设备的时钟频率

## Data type

相关数据类型、数据结构定义如下：

- spi\_device\_num\_t：SPI编号。
- spi\_mode\_t：SPI 模式。
- spi\_frame\_format\_t：SPI 帧格式。
- spi\_instruction\_address\_trans\_mode\_t：SPI 指令和地址的传输模式。

### spi\_device\_num\_t

#### Description

SPI编号。

#### Type definition

```c
typedef enum _spi_device_num
{
    SPI_DEVICE_0,
    SPI_DEVICE_1,
    SPI_DEVICE_2,
    SPI_DEVICE_3,
    SPI_DEVICE_MAX,
} spi_device_num_t;
```

#### 成员

| 成员名称      | Description           |
| :----------- | :------------- |
| SPI_DEVICE_0 | SPI 0 做为主设备|
| SPI_DEVICE_1 | SPI 1 做为主设备|
| SPI_DEVICE_2 | SPI 2 做为从设备|
| SPI_DEVICE_3 | SPI 3 做为主设备|

### spi\_mode\_t

#### Description

SPI 模式。

#### Type definition

```c
typedef enum _spi_mode
{
    SPI_WORK_MODE_0,
    SPI_WORK_MODE_1,
    SPI_WORK_MODE_2,
    SPI_WORK_MODE_3,
} spi_mode_t;
```

#### 成员

| 成员名称             | Description        |
| ------------------- | ----------- |
| SPI\_WORK\_MODE\_0  | SPI 模式 0  |
| SPI\_WORK\_MODE\_1  | SPI 模式 1  |
| SPI\_WORK\_MODE\_2  | SPI 模式 2  |
| SPI\_WORK\_MODE\_3  | SPI 模式 3  |

### spi\_frame\_format\_t

#### Description

SPI 帧格式。

#### Type definition

```c
typedef enum _spi_frame_format
{
    SPI_FF_STANDARD,
    SPI_FF_DUAL,
    SPI_FF_QUAD,
    SPI_FF_OCTAL
} spi_frame_format_t;
```

#### 成员

| 成员名称            | Description                      |
| ------------------ | ------------------------- |
| SPI\_FF\_STANDARD  | 标准                      |
| SPI\_FF\_DUAL      | 双线                      |
| SPI\_FF\_QUAD      | 四线                      |
| SPI\_FF\_OCTAL     | 八线（SPI3 不支持）        |

### spi\_instruction\_address\_trans\_mode\_t

#### Description

SPI 指令和地址的传输模式。

#### Type definition

```c
typedef enum _spi_instruction_address_trans_mode
{
    SPI_AITM_STANDARD,
    SPI_AITM_ADDR_STANDARD,
    SPI_AITM_AS_FRAME_FORMAT
} spi_instruction_address_trans_mode_t;
```

#### 成员

| 成员名称                      | Description               |
| ---------------------------- | ------------------ |
| SPI\_AITM\_STANDARD          | 均使用标准帧格式     |
| SPI\_AITM\_ADDR\_STANDARD    | 指令使用配置的值，地址使用标准帧格式 |
| SPI\_AITM\_AS\_FRAME\_FORMAT | 均使用配置的值     |