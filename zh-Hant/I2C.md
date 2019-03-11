# 集成電路內置匯流排(I²C)

## 概述

I2C 匯流排用於和多個外部裝置進行通信。多個外部裝置可以共用一個 I2C 匯流排。

## 功能描述

I2C 模組具有以下功能：

- 獨立的 I2C 裝置封裝外部裝置相關參數
- 自動處理多裝置匯流排爭用

## API參考

對應的頭文件 `i2c.h`

為用戶提供以下介面

- i2c\_init

- i2c\_init\_as\_slave

- i2c\_send\_data

- i2c\_send\_data\_dma

- i2c\_recv\_data

- i2c\_recv\_data\_dma

### i2c\_init

#### 描述

配置 I²C 器件從地址、寄存器位寬度和 I²C 速率。

#### 函數原型

```c
void i2c_init(i2c_device_number_t i2c_num, uint32_t slave_address, uint32_t address_width, uint32_t i2c_clk)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| i2c\_num | I²C號 | 輸入 |
| slave\_address | I²C 器件從地址 | 輸入|
| address\_width | I²C 器件寄存器寬度(7或10) | 輸入
| i2c\_clk | I²C 速率 (Hz) | 輸入 |

#### 返回值

無。

### i2c\_init\_as\_slave

#### 描述

配置 I²C 為從模式。

#### 函數原型

```c
void i2c_init_as_slave(i2c_device_number_t i2c_num, uint32_t slave_address, uint32_t address_width, const i2c_slave_handler_t *handler)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------   | :-----     | :----:     |
| i2c\_num | I²C號 | 輸入 |
| slave\_address | I²C 從模式的地址 | 輸入|
| address\_width | I²C 器件寄存器寬度(7或10) | 輸入
| handler | I²C 從模式的中斷處理函數 | 輸入 |

#### 返回值

無。

### i2c\_send\_data

#### 描述

寫資料。

#### 函數原型

```c
int i2c_send_data(i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len)
```

#### 參數

| 參數名稱     |   描述     |  輸入輸出  |
| :--------:   | :-----     | :----:     |
| i2c\_num | I²C號 | 輸入 |
| send\_buf | 待傳輸資料 | 輸入 |
| send\_buf\_len | 待傳輸資料長度 | 輸入 |

#### 返回值

| 返回值 | 描述 |
| :----  | :----|
| 0      | 成功 |
| 非0    | 失敗 |

### i2c\_send\_data\_dma

#### 描述

通過DMA寫資料。

#### 函數原型

```c
void i2c_send_data_dma(dmac_channel_number_t dma_channel_num, i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len)
```

#### 參數

| 參數名稱         |   描述         |  輸入輸出  |
| :-------------- | :------------- | :-------- |
| dma\_channel\_num | 使用的dma通道號 | 輸入       |
| i2c\_num        | I²C號          | 輸入       |
| send\_buf       | 待傳輸資料      | 輸入       |
| send\_buf\_len  | 待傳輸資料長度  | 輸入       |

#### 返回值

無

### i2c\_recv\_data

#### 描述

通過CPU讀資料。

#### 函數原型

```c
int i2c_recv_data(i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len, uint8_t *receive_buf, size_t receive_buf_len)
```

#### 參數

| 參數名稱               |   描述       |  輸入輸出  |
| :-------------------- | :----------- | :-------- |
| i2c\_num              | I²C 匯流排號    | 輸入      |
| send\_buf             | 待傳輸資料，一般情況是i2c外部裝置的寄存器，如果沒有設置為NULL | 輸入 |
| send\_buf\_len        | 待傳輸資料長度，如果沒有則寫0 | 輸入 |
| receive\_buf          | 接收資料內部儲存   | 輸出      |
| receive\_buf\_len     | 接收資料的長度 | 輸入      |

#### 返回值

| 返回值 | 描述 |
| :---- | :----|
| 0     | 成功 |
| 非0   | 失敗 |

### i2c\_recv\_data\_dma

#### 描述

通過dma讀資料。

#### 函數原型

```c
void i2c_recv_data_dma(dmac_channel_number_t dma_send_channel_num, dmac_channel_number_t dma_receive_channel_num,
    i2c_device_number_t i2c_num, const uint8_t *send_buf, size_t send_buf_len, uint8_t *receive_buf, size_t receive_buf_len)
```

#### 參數

| 參數名稱                 |   描述              | 輸入輸出  |
| :---------------------- | :------------------ | :------- |
| dma\_send\_channel\_num    | 發送資料使用的dma通道 | 輸入     |
| dma\_receive\_channel\_num | 接收資料使用的dma通道 | 輸入     |
| i2c\_num                | I²C 匯流排號           | 輸入     |
| send\_buf               | 待傳輸資料，一般情況是i2c外部裝置的寄存器，如果沒有設置為NULL | 輸入 |
| send\_buf\_len          | 待傳輸資料長度，如果沒有則寫0 | 輸入 |
| receive\_buf            | 接收資料內部儲存         | 輸出     |
| receive\_buf\_len       | 接收資料的長度       | 輸入      |

#### 返回值

無

### 舉例

```c
/* i2c外部裝置地址是0x32, 7位地址，速率200K */
i2c_init(I2C_DEVICE_0, 0x32, 7, 200000);
uint8_t reg = 0;
uint8_t data_buf[2] = {0x00,0x01}
data_buf[0] = reg;
/* 向0寄存器寫0x01 */
i2c_send_data(I2C_DEVICE_0, data_buf, 2);
i2c_send_data_dma(DMAC_CHANNEL0, I2C_DEVICE_0, data_buf, 4);
/* 從0寄存器讀取1位元組資料 */
i2c_receive_data(I2C_DEVICE_0, &reg, 1, data_buf, 1);
i2c_receive_data_dma(DMAC_CHANNEL0, DMAC_CHANNEL1, I2C_DEVICE_0,&reg, 1, data_buf, 1);
```

## 資料類型

相關資料類型、資料結構定義如下：

- i2c\_device\_number\_t：i2c號。

- i2c\_slave\_handler\_t：i2c從模式的中斷處理函數句柄

### i2c\_device\_number_t

#### 描述

i2c編號。

#### 定義

```c
typedef enum _i2c_device_number
{
    I2C_DEVICE_0,
    I2C_DEVICE_1,
    I2C_DEVICE_2,
    I2C_DEVICE_MAX,
} i2c_device_number_t;
```

### i2c\_slave\_handler\_t

#### 描述

i2c從模式的中斷處理函數句柄。根據不同的中斷狀態執行相應的函數操作。

#### 定義

```c
typedef struct _i2c_slave_handler
{
    void(*on_receive)(uint32_t data);
    uint32_t(*on_transmit)();
    void(*on_event)(i2c_event_t event);
} i2c_slave_handler_t;
```

#### 成員

| 成員名稱 | 描述 |
| :----- | :--- |
| I2C\_DEVICE\_0 | I2C 0 |
| I2C\_DEVICE\_1 | I2C 1 |
| I2C\_DEVICE\_2 | I2C 2 |
