# 高級加密加速器(AES)

## 功能描述

  K210內置AES(高級加密加速器)，相對於軟體可以極大的提高AES運算速度。AES加速器支持多種加密/解密模式(ECB,CBC,GCM), 多種長度的KEY(128,192,256)的運算。

## API參考

對應的頭文件 `aes.h`

為用戶提供以下介面

- aes\_ecb128\_hard\_encrypt

- aes\_ecb128\_hard\_decrypt

- aes\_ecb192\_hard\_encrypt

- aes\_ecb192\_hard\_decrypt

- aes\_ecb256\_hard\_encrypt

- aes\_ecb256\_hard\_decrypt

- aes\_cbc128\_hard\_encrypt

- aes\_cbc128\_hard\_decrypt

- aes\_cbc192\_hard\_encrypt

- aes\_cbc192\_hard\_decrypt

- aes\_cbc256\_hard\_encrypt

- aes\_cbc256\_hard\_decrypt

- aes\_gcm128\_hard\_encrypt

- aes\_gcm128\_hard\_decrypt

- aes\_gcm192\_hard\_encrypt

- aes\_gcm192\_hard\_decrypt

- aes\_gcm256\_hard\_encrypt

- aes\_gcm256\_hard\_decrypt

- aes\_ecb128\_hard\_encrypt\_dma

- aes\_ecb128\_hard\_decrypt\_dma

- aes\_ecb192\_hard\_encrypt\_dma

- aes\_ecb192\_hard\_decrypt\_dma

- aes\_ecb256\_hard\_encrypt\_dma

- aes\_ecb256\_hard\_decrypt\_dma

- aes\_cbc128\_hard\_encrypt\_dma

- aes\_cbc128\_hard\_decrypt\_dma

- aes\_cbc192\_hard\_encrypt\_dma

- aes\_cbc192\_hard\_decrypt\_dma

- aes\_cbc256\_hard\_encrypt\_dma

- aes\_cbc256\_hard\_decrypt\_dma

- aes\_gcm128\_hard\_encrypt\_dma

- aes\_gcm128\_hard\_decrypt\_dma

- aes\_gcm192\_hard\_encrypt\_dma

- aes\_gcm192\_hard\_decrypt\_dma

- aes\_gcm256\_hard\_encrypt\_dma

- aes\_gcm256\_hard\_decrypt\_dma

- aes\_init

- aes\_process

- gcm\_get\_tag

### aes\_ecb128\_hard\_encrypt

#### 描述

AES-ECB-128加密運算。輸入輸出資料都使用cpu傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb128_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-128加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-128待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-128待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-128加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。|輸出 |

#### 返回值

無。

### aes\_ecb128\_hard\_decrypt

#### 描述

AES-ECB-128解密運算。輸入輸出資料都使用cpu傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb128_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-128解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-128待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-128待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-128解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_ecb192\_hard\_encrypt

#### 描述

AES-ECB-192加密運算。輸入輸出資料都使用cpu傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb192_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-192加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-192待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-192待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-192加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_ecb192\_hard\_decrypt

#### 描述

AES-ECB-192解密運算。輸入輸出資料都使用cpu傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb192_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-192解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-192待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-192待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-192解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_ecb256\_hard\_encrypt

#### 描述

AES-ECB-256加密運算。輸入輸出資料都使用cpu傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb256_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-256加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-256待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-256待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-256加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_ecb256\_hard\_decrypt

#### 描述

AES-ECB-256解密運算。輸入輸出資料都使用cpu傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-256解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-256待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-256待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-256解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc128\_hard\_encrypt

#### 描述

AES-CBC-128加密運算。輸入輸出資料都使用cpu傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc128_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-128加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-128待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-128待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-128加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc128\_hard\_decrypt

#### 描述

AES-CBC-128解密運算。輸入輸出資料都使用cpu傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc128_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context    |AES-CBC-128解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-128待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-128待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-128解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc192\_hard\_encrypt

#### 描述

AES-CBC-192加密運算。輸入輸出資料都使用cpu傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc192_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-192加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-192待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-192待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-192加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc192\_hard\_decrypt

#### 描述

AES-CBC-192解密運算。輸入輸出資料都使用cpu傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc192_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-192解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-192待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-192待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-192解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc256\_hard\_encrypt

#### 描述

AES-CBC-256加密運算。輸入輸出資料都使用cpu傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc256_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-256加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-256待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-256待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-256加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc256\_hard\_decrypt

#### 描述

AES-CBC-256解密運算。輸入輸出資料都使用cpu傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-256解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-256待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-256待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-256解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_gcm128\_hard\_encrypt

#### 描述

AES-GCM-128加密運算。輸入輸出資料都使用cpu傳輸。

#### 函數原型

```c
void aes_gcm128_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-GCM-128加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-128待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-128待加密明文資料的長度        | 輸入 |
|output\_data  |AES-GCM-128加密運算後的結果存放在這個buffer| 輸出 |
|gcm\_tag  |AES-GCM-128加密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm128\_hard\_decrypt

#### 描述

AES-GCM-128解密運算。輸入輸出資料都使用cpu傳輸。

#### 函數原型

```c
void aes_gcm128_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context    |AES-GCM-128解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-128待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-128待解密密文資料的長度        | 輸入 |
|output\_data  |AES-GCM-128解密運算後的結果存放在這個buffer| 輸出 |
|gcm\_tag  |AES-GCM-128解密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm192\_hard\_encrypt

#### 描述

AES-GCM-192加密運算。輸入輸出資料都使用cpu傳輸。

#### 函數原型

```c
void aes_gcm192_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-GCM-192加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-192待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-192待加密明文資料的長度        | 輸入 |
|output\_data  |AES-GCM-192加密運算後的結果存放在這個buffer| 輸出 |
|gcm\_tag  |AES-GCM-192加密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm192\_hard\_decrypt

#### 描述

AES-GCM-192解密運算。輸入輸出資料都使用cpu傳輸。

#### 函數原型

```c
void aes_gcm192_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-GCM-192解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-192待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-192待解密密文資料的長度        | 輸入 |
|output\_data  |AES-GCM-192解密運算後的結果存放在這個buffer| 輸出 |
|gcm\_tag  |AES-GCM-192解密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm256\_hard\_encrypt

#### 描述

AES-GCM-256加密運算。輸入輸出資料都使用cpu傳輸。

#### 函數原型

```c
void aes_gcm256_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|context      |AES-GCM-256加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-256待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-256待加密明文資料的長度        | 輸入 |
|output\_data  |AES-GCM-256加密運算後的結果存放在這個buffer| 輸出 |
|gcm\_tag  |AES-GCM-256加密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm256\_hard\_decrypt

#### 描述

AES-GCM-256解密運算。輸入輸出資料都使用cpu傳輸。

#### 函數原型

```c
void aes_gcm256_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱    |  描述                          |輸入輸出|
| :------:  |:-----                         | :----: |
|context |AES-GCM-256解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-256待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-256待解密密文資料的長度        | 輸入 |
|output\_data  |AES-GCM-256解密運算後的結果存放在這個buffer| 輸出 |
|gcm\_tag  |AES-GCM-256解密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_ecb128\_hard\_encrypt\_dma

#### 描述

AES-ECB-128加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|input\_key    |AES-ECB-128加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-128待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-128待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-128加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。|輸出 |

#### 返回值

無。

### aes\_ecb128\_hard\_decrypt\_dma

#### 描述

AES-ECB-128解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|input\_key    |AES-ECB-128解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-128待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-128待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-128解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_ecb192\_hard\_encrypt\_dma

#### 描述

AES-ECB-192加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|input\_key    |AES-ECB-192加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-192待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-192待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-192加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_ecb192\_hard\_decrypt\_dma

#### 描述

AES-ECB-192解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|input\_key    |AES-ECB-192解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-192待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-192待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-192解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_ecb256\_hard\_encrypt\_dma

#### 描述

AES-ECB-256加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|input\_key    |AES-ECB-256加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-256待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-256待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-256加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_ecb256\_hard\_decrypt\_dma

#### 描述

AES-ECB-256解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。ECB加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。ECB模式沒有用到向量。

#### 函數原型

```c
void aes_ecb256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|input\_key    |AES-ECB-256解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-256待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-256待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-256解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc128\_hard\_encrypt\_dma

#### 描述

AES-CBC-128加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-CBC-128加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-128待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-128待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-128加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc128\_hard\_decrypt\_dma

#### 描述

AES-CBC-128解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context    |AES-CBC-128解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-128待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-128待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-128解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc192\_hard\_encrypt\_dma

#### 描述

AES-CBC-192加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-CBC-192加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-192待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-192待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-192加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc192\_hard\_decrypt\_dma

#### 描述

AES-CBC-192解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-CBC-192解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-192待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-192待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-192解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc256\_hard\_encrypt\_dma

#### 描述

AES-CBC-256加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-CBC-256加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-256待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-256待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-256加密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_cbc256\_hard\_decrypt\_dma

#### 描述

AES-CBC-256解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。CBC加密將明文按照固定大小16bytes的塊進行加密的，塊大小不足則進行填充。

#### 函數原型

```c
void aes_cbc256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-CBC-256解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-256待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-256待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-256解密運算後的結果存放在這個buffer。<br/>這個buffer的大小需要保證16bytes對齊。| 輸出 |

#### 返回值

無。

### aes\_gcm128\_hard\_encrypt\_dma

#### 描述

AES-GCM-128加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。

#### 函數原型

```c
void aes_gcm128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-GCM-128加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-128待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-128待加密明文資料的長度。| 輸入 |
|output\_data  |AES-GCM-128加密運算後的結果存放在這個buffer。。<br/>由於DMA搬運資料的最小粒度為4bytes，<br/>所以需要保證這個buffer大小至少為4bytes的整數倍。| 輸出 |
|gcm\_tag  |AES-GCM-128加密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm128\_hard\_decrypt\_dma

#### 描述

AES-GCM-128解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。

#### 函數原型

```c
void aes_gcm128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context    |AES-GCM-128解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-128待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-128待解密密文資料的長度。| 輸入 |
|output\_data  |AES-GCM-128解密運算後的結果存放在這個buffer。<br/>由於DMA搬運資料的最小粒度為4bytes，<br/>所以需要保證這個buffer大小至少為4bytes的整數倍。| 輸出 |
|gcm\_tag  |AES-GCM-128解密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm192\_hard\_encrypt\_dma

#### 描述

AES-GCM-192加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。

#### 函數原型

```c
void aes_gcm192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-GCM-192加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-192待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-192待加密明文資料的長度。| 輸入 |
|output\_data  |AES-GCM-192加密運算後的結果存放在這個buffer。<br/>由於DMA搬運資料的最小粒度為4bytes，<br/>所以需要保證這個buffer大小至少為4bytes的整數倍。| 輸出 |
|gcm\_tag  |AES-GCM-192加密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm192\_hard\_decrypt\_dma

#### 描述

AES-GCM-192解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。

#### 函數原型

```c
void aes_gcm192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-GCM-192解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-192待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-192待解密密文資料的長度。| 輸入 |
|output\_data  |AES-GCM-192解密運算後的結果存放在這個buffer。<br/>由於DMA搬運資料的最小粒度為4bytes，<br/>所以需要保證這個buffer大小至少為4bytes的整數倍。| 輸出 |
|gcm\_tag  |AES-GCM-192解密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm256\_hard\_encrypt\_dma

#### 描述

AES-GCM-256加密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。

#### 函數原型

```c
void aes_gcm256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context      |AES-GCM-256加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-256待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-256待加密明文資料的長度。| 輸入 |
|output\_data  |AES-GCM-256加密運算後的結果存放在這個buffer。<br/>由於DMA搬運資料的最小粒度為4bytes，<br/>所以需要保證這個buffer大小至少為4bytes的整數倍。| 輸出 |
|gcm\_tag  |AES-GCM-256加密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm256\_hard\_decrypt\_dma

#### 描述

AES-GCM-256解密運算。輸入資料使用cpu傳輸，輸出資料都使用dma傳輸。

#### 函數原型

```c
void aes_gcm256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱    |  描述                          |輸入輸出|
| :------:  |:-----                         | :----: |
|dma\_receive\_channel\_num|AES輸出資料的DMA通道號  | 輸入 |
|context |AES-GCM-256解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-256待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-256待解密密文資料的長度。| 輸入 |
|output\_data  |AES-GCM-256解密運算後的結果存放在這個buffer。<br/>由於DMA搬運資料的最小粒度為4bytes，<br/>所以需要保證這個buffer大小至少為4bytes的整數倍。| 輸出 |
|gcm\_tag  |AES-GCM-256解密運算後的tag存放在這個buffer。<br/>這個buffer大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_init

#### 描述

AES硬體模組的初始化

#### 函數原型

```c
void aes_init(uint8_t *input_key, size_t input_key_len, uint8_t *iv,size_t iv_len, uint8_t *gcm_aad,aes_cipher_mode_t cipher_mode, aes_encrypt_sel_t encrypt_sel, size_t gcm_aad_len, size_t input_data_len)
```

#### 參數

| 參數名稱    |  描述                          |輸入輸出|
| :------:  |:-----                         | :----: |
|input\_key  |待加密/解密的密鑰                | 輸入 |
|input\_key_len|待加密/解密密鑰的長度          | 輸入 |
|iv       |AES加密解密用到的iv資料            | 輸入 |
|iv\_len  |AES加密解密用到的iv資料的長度，CBC固定為16bytes，GCM固定為12bytes| 輸出 |
|gcm\_aad  |AES-GCM加密解密用到的aad資料       | 輸出 |
|cipher\_mode|AES硬體模組執行的加密解密類型，支持AES\_CBC/AES\_ECB/AES\_GCM| 輸入 |
|encrypt\_sel  |AES硬體模組執行的模式：加密或解密| 輸入 |
|gcm\_aad\_len |AES-GCM加密解密用到的aad資料的長度| 輸入 |
|input\_data\_len |待加密/解密的資料長度          | 輸入 |

#### 返回值

無。

### aes\_process

#### 描述

AES硬體模組執行加密解密操作

#### 函數原型

```c
void aes_process(uint8_t *input_data, uint8_t *output_data, size_t input_data_len, aes_cipher_mode_t cipher_mode)
```

#### 參數

| 參數名稱    |  描述                          |輸入輸出|
| :------:   |:-----                          | :----: |
|input\_data |這個buffer存放待加密/解密的資料   | 輸入 |
|output\_data|這個buffer存放加密/解密的輸出結果 | 輸出 |
|input\_data\_len|待加密/解密的資料的長度        | 輸入 |
|cipher\_mode |AES硬體模組執行的加密解密類型，支持AES\_CBC/AES\_ECB/AES\_GCM| 輸入 |

#### 返回值

無。

### gcm\_get\_tag

#### 描述

獲取AES-GCM計算結束後的tag

#### 函數原型

```c
void gcm_get_tag(uint8_t *gcm_tag)
```

#### 參數

| 參數名稱    |  描述                          |輸入輸出|
| :------:  |:-----                         | :----: |
|gcm\_tag |這個buffer存放AES-GCM加密/解密後的tag，固定為16bytes的大小| 輸出|

#### 返回值

無。

### 舉例

```c
cbc_context_t cbc_context;
cbc_context.input_key = cbc_key;
cbc_context.iv = cbc_iv;
aes_cbc128_hard_encrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
memcpy(aes_input_data, aes_output_data, 16L);
aes_cbc128_hard_decrypt(&cbc_context, aes_input_data, 16L, aes_output_data);

```

## 資料類型

相關資料類型、資料結構定義如下：

- `aes_cipher_mode_t`：AES加密/解密的方式。

### aes\_cipher\_mode\_t

#### 描述

AES加密/解密的方式。

#### 定義

```c
typedef enum _aes_cipher_mode
{
    AES_ECB = 0,
    AES_CBC = 1,
    AES_GCM = 2,
    AES_CIPHER_MAX
} aes_cipher_mode_t;
```

- `gcm_context_t`：AES-GCM加密/解密時參數用到的結構體

### gcm\_context\_t

#### 描述

AES-GCM參數用到的結構體，包括密鑰、偏移向量、aad資料、aad資料長度。

#### 定義

```c
typedef struct _gcm_context
{
    uint8_t *input_key;
    uint8_t *iv;
    uint8_t *gcm_aad;
    size_t gcm_aad_len;
} gcm_context_t;
```

- `cbc_context_t`：AES-CBC加密/解密時參數用到的結構體

### cbc\_context\_t

#### 描述

AES-CBC參數用到的結構體，包括密鑰、偏移向量。

#### 定義

```c
typedef struct _cbc_context
{
    uint8_t *input_key;
    uint8_t *iv;
} cbc_context_t;
```

#### 成員

| 成員名稱 | 描述 |
| :----- | :--- |
| AES\_ECB | ECB加密/解密 |
| AES\_CBC | CBC加密/解密 |
| AES\_GCM | GCM加密/解密 |