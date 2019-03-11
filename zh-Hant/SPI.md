# 串列外部裝置介面(SPI)

## 概述

SPI 是一種高速的，全雙工，同步的通信匯流排。

## 功能描述

SPI 模組具有以下功能：

- 獨立的 SPI 裝置封裝外部裝置相關參數
- 自動處理多裝置匯流排爭用
- 支持標準、雙線、四線、八線模式
- 支持先寫後讀和全雙工讀寫
- 支持發送一串相同的資料幀，常用於清屏、填充存儲扇區等場景

## API參考

對應的頭文件 `spi.h`

為用戶提供以下介面

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

#### 描述

設置SPI工作模式、多線模式和位寬。

#### 函數原型

```c
void spi_init(spi_device_num_t spi_num, spi_work_mode_t work_mode, spi_frame_format_t frame_format, size_t data_bit_length, uint32_t endian)
```

#### 參數

| 參數名稱            |   描述             |  輸入輸出  |
| :----------------- | :----------------- | :-------- |
| spi\_num           | SPI號              | 輸入       |
| work\_mode         | 極性相位的四種模式   | 輸入      |
| frame\_format      | 多線模式            | 輸入      |
| data\_bit\_length  | 單次傳輸的資料的位寬 | 輸入      |
| endian             | 大小端<br>0：小端<br>1：大端 | 輸入 |

#### 返回值

無。

### spi\_config\_non\_standard

#### 描述

多線模式下設置指令長度、地址長度、等待時脈數、指令地址傳輸模式。

#### 函數原型

```c
void spi_init_non_standard(spi_device_num_t spi_num, uint32_t instruction_length, uint32_t address_length, uint32_t wait_cycles, spi_instruction_address_trans_mode_t instruction_address_trans_mode)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI號 | 輸入 |
| instruction\_length | 發送指令的位數 | 輸入 |
| address\_length | 發送地址的位數 | 輸入 |
| wait\_cycles | 等待時脈個數 | 輸入 |
| instruction\_address\_trans\_mode | 指令地址傳輸的方式 | 輸入 |

#### 返回值

無

### spi\_send\_data\_standard

#### 描述

SPI標準模式傳輸資料。

#### 函數原型

```c
void spi_send_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| cmd\_buff | 外部裝置指令地址資料，沒有則設為NULL | 輸入 |
| cmd\_len | 外部裝置指令地址資料長度，沒有則設為0 | 輸入 |
| tx\_buff | 發送的資料 | 輸入 |
| tx\_len | 發送資料的長度 | 輸入 |

#### 返回值

無

### spi\_send\_data\_standard\_dma

#### 描述

SPI標準模式下使用DMA傳輸資料。

#### 函數原型

```c
void spi_send_data_standard_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| channel\_num | DMA通道號 | 輸入 |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| cmd\_buff | 外部裝置指令地址資料，沒有則設為NULL | 輸入 |
| cmd\_len | 外部裝置指令地址資料長度，沒有則設為0 | 輸入 |
| tx\_buff | 發送的資料 | 輸入 |
| tx\_len | 發送資料的長度 | 輸入 |

#### 返回值

無

### spi\_receive\_data\_standard

#### 描述

標準模式下接收資料。

#### 函數原型

```c
void spi_receive_data_standard(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| cmd\_buff | 外部裝置指令地址資料，沒有則設為NULL | 輸入 |
| cmd\_len | 外部裝置指令地址資料長度，沒有則設為0 | 輸入 |
| rx\_buff | 接收的資料 | 輸出 |
| rx\_len | 接收資料的長度 | 輸入 |

#### 返回值

無

### spi\_receive\_data\_standard\_dma

#### 描述

標準模式下通過DMA接收資料。

#### 函數原型

```c
void spi_receive_data_standard_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint8_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| dma\_send\_channel\_num | 發送指令地址使用的DMA通道號 | 輸入 |
| dma\_receive\_channel\_num | 接收資料使用的DMA通道號 | 輸入 |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| cmd\_buff | 外部裝置指令地址資料，沒有則設為NULL | 輸入 |
| cmd\_len | 外部裝置指令地址資料長度，沒有則設為0 | 輸入 |
| rx\_buff | 接收的資料 | 輸出 |
| rx\_len | 接收資料的長度 | 輸入 |

#### 返回值

無

### spi\_send\_data\_multiple

#### 描述

多線模式發送資料。

#### 函數原型

```c
void spi_send_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, uint8_t *tx_buff, size_t tx_len)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| cmd\_buff | 外部裝置指令地址資料，沒有則設為NULL | 輸入 |
| cmd\_len | 外部裝置指令地址資料長度，沒有則設為0 | 輸入 |
| tx\_buff | 發送的資料 | 輸入 |
| tx\_len | 發送資料的長度 | 輸入 |

#### 返回值

無

### spi\_send\_data\_multiple\_dma

#### 描述

多線模式使用DMA發送資料。

#### 函數原型

```c
void spi_send_data_multiple_dma(dmac_channel_number_t channel_num,spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, const uint8_t *tx_buff, size_t tx_len)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| channel\_num | DMA通道號 | 輸入 |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| cmd\_buff | 外部裝置指令地址資料，沒有則設為NULL | 輸入 |
| cmd\_len | 外部裝置指令地址資料長度，沒有則設為0 | 輸入 |
| tx\_buff | 發送的資料 | 輸入 |
| tx\_len | 發送資料的長度 | 輸入 |

#### 返回值

無

### spi\_receive\_data\_multiple

#### 描述

多線模式接收資料。

#### 函數原型

```c
void spi_receive_data_multiple(spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| cmd\_buff | 外部裝置指令地址資料，沒有則設為NULL | 輸入 |
| cmd\_len | 外部裝置指令地址資料長度，沒有則設為0 | 輸入 |
| rx\_buff | 接收的資料 | 輸出 |
| rx\_len | 接收資料的長度 | 輸入 |

#### 返回值

無

### spi\_receive\_data\_multiple\_dma

#### 描述

多線模式通過DMA接收。

#### 函數原型

```c
void spi_receive_data_multiple_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, uint32_t const *cmd_buff, size_t cmd_len, uint8_t *rx_buff, size_t rx_len);
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| dma\_send\_channel\_num | 發送指令地址使用的DMA通道號 | 輸入 |
| dma\_receive\_channel\_num | 接收資料使用的DMA通道號 | 輸入 |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| cmd\_buff | 外部裝置指令地址資料，沒有則設為NULL | 輸入 |
| cmd\_len | 外部裝置指令地址資料長度，沒有則設為0 | 輸入 |
| rx\_buff | 接收的資料 | 輸出 |
| rx\_len | 接收資料的長度 | 輸入 |

#### 返回值

無

### spi\_fill\_data\_dma

#### 描述

通過DMA始終發送同一個資料，可以用於刷新資料。

#### 函數原型

```c
void spi_fill_data_dma(dmac_channel_number_t channel_num,spi_device_num_t spi_num, spi_chip_select_t chip_select, const uint32_t *tx_buff, size_t tx_len);
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| channel\_num | DMA通道號 | 輸入 |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| tx\_buff | 發送的資料,僅發送tx_buff這一個資料，不會自動增加 | 輸入 |
| tx\_len | 發送資料的長度 | 輸入 |

#### 返回值

無

### spi\_send\_data\_normal\_dma

#### 描述

通過DMA發送資料。不用設置指令地址。

#### 函數原型

```c
void spi_send_data_normal_dma(dmac_channel_number_t channel_num, spi_device_num_t spi_num, spi_chip_select_t chip_select, const void *tx_buff, size_t tx_len, spi_transfer_width_t spi_transfer_width)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| channel\_num | DMA通道號 | 輸入 |
| spi\_num | SPI號 | 輸入 |
| chip\_select | 片選信號 | 輸入 |
| tx\_buff | 發送的資料,僅發送tx_buff這一個資料，不會自動增加 | 輸入 |
| tx\_len | 發送資料的長度 | 輸入 |
| spi\_transfer\_width | 發送資料的位寬 | 輸入 |

#### 返回值

無

### 舉例

```c
/* SPI0 工作在MODE0模式 標準SPI模式 單次發送8位資料 */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_0, SPI_FF_STANDARD, 8, 0);
uint8_t cmd[4];
cmd[0] = 0x06;
cmd[1] = 0x01;
cmd[2] = 0x02;
cmd[3] = 0x04;
uint8_t data_buf[4] = {0,1,2,3};
/* SPI0 使用片選0 發送指令0x06 向地址0x010204 發送0，1，2，3 四個位元組資料 */
spi_send_data_standard(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 4, data_buf, 4);
/* SPI0 使用片選0 發送指令0x06 地址0x010204 接收4個位元組的資料 */
spi_receive_data_standard(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 4, data_buf, 4);

/* SPI0 工作在MODE0模式 四線SPI模式 單次發送8位資料 */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_0, SPI_FF_QUAD, 8, 0);
/* 8位指令長度 32位地址長度 發送指令地址後等待4個clk，指令通過標準SPI方式發送，地址通過四線方式發送 */
spi_init_non_standard(SPI_DEVICE_0, 8, 32, 4, SPI_AITM_ADDR_STANDARD);
uint32 cmd[2];
cmd[0] = 0x06;
cmd[1] = 0x010204;
uint8_t data_buf[4] = {0,1,2,3};
/* SPI0 使用片選0 發送指令0x06 向地址0x010204 發送0，1，2，3 四個位元組資料 */
spi_send_data_multiple(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 2, data_buf, 4);
/* SPI0 使用片選0 發送指令0x06 地址0x010204 接收4個位元組的資料 */
spi_receive_data_multiple(SPI_DEVICE_0, SPI_CHIP_SELECT_0, cmd, 2, data_buf, 4);

/* SPI0 工作在MODE2模式 八線SPI模式 單次發送32位資料 */
spi_init(SPI_DEVICE_0, SPI_WORK_MODE_2, SPI_FF_OCTAL, 32, 0);
/* 無指令 32位地址長度 發送指令地址後等待0個clk，指令地址通過8線發送 */
spi_init_non_standard(SPI_DEVICE_0, 0, 32, 0, SPI_AITM_AS_FRAME_FORMAT);
uint32_t data_buf[256] = {0};
/* 使用DMA通道0 片選0 發送256個int資料*/
spi_send_data_normal_dma(DMAC_CHANNEL0, SPI_DEVICE_0, SPI_CHIP_SELECT_0, data_buf, 256, SPI_TRANS_INT);
uint32_t data = 0x55AA55AA;
/* 使用DMA通道0 片選0 連續發送256個 0x55AA55AA*/
spi_fill_data_dma(DMAC_CHANNEL0, SPI_DEVICE_0, SPI_CHIP_SELECT_0,&data, 256);
```

### spi\_set\_clk\_rate

#### 描述

設置 SPI 的時脈頻率

#### 函數原型

```c
uint32_t spi_set_clk_rate(spi_device_num_t spi_num, uint32_t spi_clk)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| spi\_num| SPI號 | 輸入 |
| spi\_clk | 目標SPI裝置的時脈頻率 | 輸入 |

#### 返回值

設置完後的SPI裝置的時脈頻率

## 資料類型

相關資料類型、資料結構定義如下：

- spi\_device\_num\_t：SPI編號。
- spi\_mode\_t：SPI 模式。
- spi\_frame\_format\_t：SPI 幀格式。
- spi\_instruction\_address\_trans\_mode\_t：SPI 指令和地址的傳輸模式。

### spi\_device\_num\_t

#### 描述

SPI編號。

#### 定義

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

#### 成員

| 成員名稱      | 描述           |
| :----------- | :------------- |
| SPI_DEVICE_0 | SPI 0 做為主裝置|
| SPI_DEVICE_1 | SPI 1 做為主裝置|
| SPI_DEVICE_2 | SPI 2 做為從裝置|
| SPI_DEVICE_3 | SPI 3 做為主裝置|

### spi\_mode\_t

#### 描述

SPI 模式。

#### 定義

```c
typedef enum _spi_mode
{
    SPI_WORK_MODE_0,
    SPI_WORK_MODE_1,
    SPI_WORK_MODE_2,
    SPI_WORK_MODE_3,
} spi_mode_t;
```

#### 成員

| 成員名稱             | 描述        |
| ------------------- | ----------- |
| SPI\_WORK\_MODE\_0  | SPI 模式 0  |
| SPI\_WORK\_MODE\_1  | SPI 模式 1  |
| SPI\_WORK\_MODE\_2  | SPI 模式 2  |
| SPI\_WORK\_MODE\_3  | SPI 模式 3  |

### spi\_frame\_format\_t

#### 描述

SPI 幀格式。

#### 定義

```c
typedef enum _spi_frame_format
{
    SPI_FF_STANDARD,
    SPI_FF_DUAL,
    SPI_FF_QUAD,
    SPI_FF_OCTAL
} spi_frame_format_t;
```

#### 成員

| 成員名稱            | 描述                      |
| ------------------ | ------------------------- |
| SPI\_FF\_STANDARD  | 標準                      |
| SPI\_FF\_DUAL      | 雙線                      |
| SPI\_FF\_QUAD      | 四線                      |
| SPI\_FF\_OCTAL     | 八線（SPI3 不支持）        |

### spi\_instruction\_address\_trans\_mode\_t

#### 描述

SPI 指令和地址的傳輸模式。

#### 定義

```c
typedef enum _spi_instruction_address_trans_mode
{
    SPI_AITM_STANDARD,
    SPI_AITM_ADDR_STANDARD,
    SPI_AITM_AS_FRAME_FORMAT
} spi_instruction_address_trans_mode_t;
```

#### 成員

| 成員名稱                      | 描述               |
| ---------------------------- | ------------------ |
| SPI\_AITM\_STANDARD          | 均使用標準幀格式     |
| SPI\_AITM\_ADDR\_STANDARD    | 指令使用配置的值，地址使用標準幀格式 |
| SPI\_AITM\_AS\_FRAME\_FORMAT | 均使用配置的值     |