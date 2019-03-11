# 神經網路處理器 (KPU)

## 概述

KPU 是通用的神經網路處理器，它可以在低功耗的情況下實現捲積神經網路計算，實時獲取被檢測目標的大小、坐標和種類，對人臉或者物體進行檢測和分類。
使用kpu時，必須結合model compiler。

## 功能描述

KPU 具備以下幾個特點：

- 支持主流訓練框架按照特定限制規則訓練出來的定點化模型

- 對網路層數無直接限制，支持每層捲積神經網路參數單獨配置，包括輸入輸出通道數目、輸入輸出行寬列高

- 支持兩種捲積內核 1x1 和 3x3

- 支持任意形式的激活函數

- 實時工作時最大支持神經網路參數大小為 5.5MiB 到 5.9MiB

- 非實時工作時最大支持網路參數大小為（Flash 容量-軟體體積）

## API 參考

對應的頭文件 `kpu.h`

為用戶提供以下介面

- kpu\_task\_init (0.6.0以後不再支持，請使用kpu\_single\_task\_init)

- kpu\_run (0.6.0以後不再支持，請使用kpu\_start)

- kpu\_get\_output\_buf (0.6.0以後不再支持)

- kpu\_release\_output\_buf (0.6.0以後不再支持)

- kpu\_start

- kpu\_single\_task\_init

- kpu\_single\_task\_deinit

- kpu\_model\_load\_from\_buffer

### kpu\_task\_init

#### 描述

初始化kpu任務句柄，該函數具體實現在model compiler生成的gencode_output.c中。

#### 函數定義

```c
kpu_task_t* kpu_task_init(kpu_task_t* task)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任務句柄             | 輸入      |

#### 返回值

KPU任務句柄。

### kpu\_run

#### 描述

啟動KPU，進行AI運算。

#### 函數原型

```c
int kpu_run(kpu_task_t* v_task, dmac_channel_number_t dma_ch, const void *src, void* dest, plic_irq_callback_t callback)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任務句柄             | 輸入      |
| dma\_ch                         | DMA通道                 | 輸入      |
| src                             | 輸入圖像資料             | 輸入      |
| dest                            | 運算輸出結果             | 輸出      |
| callback                        | 運算完成回調函數         | 輸入      |

#### 返回值

| 返回值  | 描述         |
| :----  | :------------|
| 0      | 成功         |
| 非0    | KPU忙，失敗   |

### kpu\_get\_output\_buf

#### 描述

獲取KPU輸出結果的緩存。

#### 函數原型

```c
uint8_t *kpu_get_output_buf(kpu_task_t* task)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任務句柄             | 輸入      |

#### 返回值

KPU輸出結果的緩存的指針。

### kpu\_release\_output\_buf

#### 描述

釋放KPU輸出結果緩存。

#### 函數原型

```c
void kpu_release_output_buf(uint8_t *output_buf)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| output\_buf                     | KPU輸出結果緩存         | 輸入      |

#### 返回值

無

### kpu\_start

#### 描述

啟動KPU，進行AI運算。

#### 函數原型

```c
int kpu_start(kpu_task_t *task)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任務句柄             | 輸入      |

#### 返回值

| 返回值  | 描述         |
| :----  | :------------|
| 0      | 成功         |
| 非0    | KPU忙，失敗   |

### kpu\_single\_task\_init

#### 描述

初始化kpu任務句柄。

#### 函數原型

```c
int kpu_single_task_init(kpu_task_t *task)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任務句柄             | 輸入      |

#### 返回值

| 返回值  | 描述         |
| :----  | :------------|
| 0      | 成功         |
| 非0    | 失敗         |

### kpu\_single\_task\_deinit

#### 描述

註銷kpu任務。

#### 函數原型

```c
int kpu_single_task_deinit(kpu_task_t *task)
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任務句柄             | 輸入      |

#### 返回值

| 返回值  | 描述         |
| :----  | :------------|
| 0      | 成功         |
| 非0    | 失敗         |

### kpu\_model\_load\_from\_buffer

#### 描述

解析kmodel並初始化kpu句柄。

#### 函數原型

```c
int kpu_model_load_from_buffer(kpu_task_t *task, uint8_t *buffer, kpu_model_layer_metadata_t **meta);
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任務句柄             | 輸入      |
| buffer                          | kmodel資料             | 輸入      |
| meta                            | 內部測試資料，用戶設置為NULL | 輸出      |

#### 返回值

| 返回值  | 描述         |
| :----  | :------------|
| 0      | 成功         |
| 非0    | 失敗         |

### 舉例

```c
/* 通過MC生成kpu_task_gencode_output_init，設置源資料為g_ai_buf，使用DMA5，kpu完成後調用ai_done函數 */
kpu_task_t task;
volatile uint8_t g_ai_done_flag;
static int ai_done(void *ctx)
{
    g_ai_done_flag = 1;
    return 0;
}

/* 初始化kpu */
kpu_task_gencode_output_init(&task); /* MC生成的函數 */
task.src = g_ai_buf;
task.dma_ch = 5;
task.callback = ai_done;
kpu_single_task_init(&task);

/* 啟動kpu */
kpu_start(&task);
```

## 資料類型

相關資料類型、資料結構定義如下：

- kpu\_task\_t：kpu任務結構體。

### kpu\_task\_t

#### 描述

kpu任務結構體。

#### 定義

```c
typedef struct
{
    kpu_layer_argument_t *layers;
    kpu_layer_argument_t *remain_layers;
    plic_irq_callback_t callback;
    void *ctx;
    uint64_t *src;
    uint64_t *dst;
    uint32_t src_length;
    uint32_t dst_length;
    uint32_t layers_length;
    uint32_t remain_layers_length;
    dmac_channel_number_t dma_ch;
    uint32_t eight_bit_mode;
    float output_scale;
    float output_bias;
    float input_scale;
    float input_bias;
} kpu_task_t;
```

#### 成員

| 成員名稱                | 描述                                       |
| ---------------------- | ------------------------------------------ |
| layers                 | KPU參數指針(MC初始化，用戶不必關心)           |
| remain\_layers         | KPU參數指針（運算過程中使用，用戶不必關心）    |
| callback               | 運算完成回調函數（需要用戶設置）               |
| ctx                    | 回調函數的參數（非空需要用戶設置）             |
| src                    | 運算源資料（需要用戶設置）                    |
| dst                    | 運算結果輸出指針（KPU初始化賦值，用戶不必關心） |
| src\_length            | 源資料長度(MC初始化，用戶不必關心)             |
| dst\_length            | 運算結果長度(MC初始化，用戶不必關心)           |
| layers\_length         | 層數(MC初始化，用戶不必關心)                  |
| remain\_layers\_length | 剩餘層數（運算過程中使用，用戶不必關心）        |
| dma\_ch                | 使用的DMA通道號（需要用戶設置）                |
| eight\_bit\_mode       | 是否是8比特模式(MC初始化，用戶不必關心)         |
| output\_scale          | 輸出scale值(MC初始化，用戶不必關心)            |
| output\_bias           | 輸出bias值(MC初始化，用戶不必關心)             |
| input\_scale           | 輸入scale值(MC初始化，用戶不必關心)            |
| input\_bias            | 輸入bias值(MC初始化，用戶不必關心)             |
