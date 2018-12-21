# 高级加密加速器(AES)

## 功能描述

  K210内置AES(高级加密加速器)，相对于软件可以极大的提高AES运算速度。AES加速器支持多种加密/解密模式(ECB,CBC,GCM), 多种长度的KEY(128,192,256)的运算。

## API参考

对应的头文件 `aes.h`

为用户提供以下接口

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

AES-ECB-128加密运算。输入输出数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb128_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-128加密的密钥                | 输入 |
|input\_data   |AES-ECB-128待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-128待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-128加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。|输出 |

#### 返回值

无。

### aes\_ecb128\_hard\_decrypt

#### 描述

AES-ECB-128解密运算。输入输出数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb128_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-128解密的密钥                | 输入 |
|input\_data   |AES-ECB-128待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-128待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-128解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_ecb192\_hard\_encrypt

#### 描述

AES-ECB-192加密运算。输入输出数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb192_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-192加密的密钥                | 输入 |
|input\_data   |AES-ECB-192待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-192待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-192加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_ecb192\_hard\_decrypt

#### 描述

AES-ECB-192解密运算。输入输出数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb192_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-192解密的密钥                | 输入 |
|input\_data   |AES-ECB-192待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-192待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-192解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_ecb256\_hard\_encrypt

#### 描述

AES-ECB-256加密运算。输入输出数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb256_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-256加密的密钥                | 输入 |
|input\_data   |AES-ECB-256待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-256待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-256加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_ecb256\_hard\_decrypt

#### 描述

AES-ECB-256解密运算。输入输出数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|input\_key    |AES-ECB-256解密的密钥                | 输入 |
|input\_data   |AES-ECB-256待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-256待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-256解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc128\_hard\_encrypt

#### 描述

AES-CBC-128加密运算。输入输出数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc128_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-128加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-128待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-128待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-128加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc128\_hard\_decrypt

#### 描述

AES-CBC-128解密运算。输入输出数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc128_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context    |AES-CBC-128解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-128待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-128待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-128解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc192\_hard\_encrypt

#### 描述

AES-CBC-192加密运算。输入输出数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc192_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-192加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-192待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-192待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-192加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc192\_hard\_decrypt

#### 描述

AES-CBC-192解密运算。输入输出数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc192_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-192解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-192待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-192待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-192解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc256\_hard\_encrypt

#### 描述

AES-CBC-256加密运算。输入输出数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc256_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-256加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-256待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-256待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-256加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc256\_hard\_decrypt

#### 描述

AES-CBC-256解密运算。输入输出数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-CBC-256解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-256待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-256待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-256解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_gcm128\_hard\_encrypt

#### 描述

AES-GCM-128加密运算。输入输出数据都使用cpu传输。

#### 函数原型

```c
void aes_gcm128_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-GCM-128加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-128待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-128待加密明文数据的长度        | 输入 |
|output\_data  |AES-GCM-128加密运算后的结果存放在这个buffer| 输出 |
|gcm\_tag  |AES-GCM-128加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm128\_hard\_decrypt

#### 描述

AES-GCM-128解密运算。输入输出数据都使用cpu传输。

#### 函数原型

```c
void aes_gcm128_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context    |AES-GCM-128解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-128待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-128待解密密文数据的长度        | 输入 |
|output\_data  |AES-GCM-128解密运算后的结果存放在这个buffer| 输出 |
|gcm\_tag  |AES-GCM-128解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm192\_hard\_encrypt

#### 描述

AES-GCM-192加密运算。输入输出数据都使用cpu传输。

#### 函数原型

```c
void aes_gcm192_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-GCM-192加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-192待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-192待加密明文数据的长度        | 输入 |
|output\_data  |AES-GCM-192加密运算后的结果存放在这个buffer| 输出 |
|gcm\_tag  |AES-GCM-192加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm192\_hard\_decrypt

#### 描述

AES-GCM-192解密运算。输入输出数据都使用cpu传输。

#### 函数原型

```c
void aes_gcm192_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-GCM-192解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-192待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-192待解密密文数据的长度        | 输入 |
|output\_data  |AES-GCM-192解密运算后的结果存放在这个buffer| 输出 |
|gcm\_tag  |AES-GCM-192解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm256\_hard\_encrypt

#### 描述

AES-GCM-256加密运算。输入输出数据都使用cpu传输。

#### 函数原型

```c
void aes_gcm256_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|context      |AES-GCM-256加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-256待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-256待加密明文数据的长度        | 输入 |
|output\_data  |AES-GCM-256加密运算后的结果存放在这个buffer| 输出 |
|gcm\_tag  |AES-GCM-256加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm256\_hard\_decrypt

#### 描述

AES-GCM-256解密运算。输入输出数据都使用cpu传输。

#### 函数原型

```c
void aes_gcm256_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称    |  描述                          |输入输出|
| :------:  |:-----                         | :----: |
|context |AES-GCM-256解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-256待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-256待解密密文数据的长度        | 输入 |
|output\_data  |AES-GCM-256解密运算后的结果存放在这个buffer| 输出 |
|gcm\_tag  |AES-GCM-256解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_ecb128\_hard\_encrypt\_dma

#### 描述

AES-ECB-128加密运算。输入数据使用cpu传输，输出数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|input\_key    |AES-ECB-128加密的密钥                | 输入 |
|input\_data   |AES-ECB-128待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-128待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-128加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。|输出 |

#### 返回值

无。

### aes\_ecb128\_hard\_decrypt\_dma

#### 描述

AES-ECB-128解密运算。输入数据使用cpu传输，输出数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|input\_key    |AES-ECB-128解密的密钥                | 输入 |
|input\_data   |AES-ECB-128待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-128待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-128解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_ecb192\_hard\_encrypt\_dma

#### 描述

AES-ECB-192加密运算。输入数据使用cpu传输，输出数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|input\_key    |AES-ECB-192加密的密钥                | 输入 |
|input\_data   |AES-ECB-192待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-192待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-192加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_ecb192\_hard\_decrypt\_dma

#### 描述

AES-ECB-192解密运算。输入数据使用cpu传输，输出数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|input\_key    |AES-ECB-192解密的密钥                | 输入 |
|input\_data   |AES-ECB-192待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-192待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-192解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_ecb256\_hard\_encrypt\_dma

#### 描述

AES-ECB-256加密运算。输入数据使用cpu传输，输出数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|input\_key    |AES-ECB-256加密的密钥                | 输入 |
|input\_data   |AES-ECB-256待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-256待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-256加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_ecb256\_hard\_decrypt\_dma

#### 描述

AES-ECB-256解密运算。输入数据使用cpu传输，输出数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### 函数原型

```c
void aes_ecb256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|input\_key    |AES-ECB-256解密的密钥                | 输入 |
|input\_data   |AES-ECB-256待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-256待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-256解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc128\_hard\_encrypt\_dma

#### 描述

AES-CBC-128加密运算。输入数据使用cpu传输，输出数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-CBC-128加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-128待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-128待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-128加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc128\_hard\_decrypt\_dma

#### 描述

AES-CBC-128解密运算。输入数据使用cpu传输，输出数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context    |AES-CBC-128解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-128待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-128待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-128解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc192\_hard\_encrypt\_dma

#### 描述

AES-CBC-192加密运算。输入数据使用cpu传输，输出数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-CBC-192加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-192待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-192待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-192加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc192\_hard\_decrypt\_dma

#### 描述

AES-CBC-192解密运算。输入数据使用cpu传输，输出数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-CBC-192解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-192待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-192待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-192解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc256\_hard\_encrypt\_dma

#### 描述

AES-CBC-256加密运算。输入数据使用cpu传输，输出数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-CBC-256加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-256待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-256待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-256加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_cbc256\_hard\_decrypt\_dma

#### 描述

AES-CBC-256解密运算。输入数据使用cpu传输，输出数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### 函数原型

```c
void aes_cbc256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-CBC-256解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-256待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-256待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-256解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。| 输出 |

#### 返回值

无。

### aes\_gcm128\_hard\_encrypt\_dma

#### 描述

AES-GCM-128加密运算。输入数据使用cpu传输，输出数据都使用dma传输。

#### 函数原型

```c
void aes_gcm128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-GCM-128加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-128待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-128待加密明文数据的长度。| 输入 |
|output\_data  |AES-GCM-128加密运算后的结果存放在这个buffer。。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。| 输出 |
|gcm\_tag  |AES-GCM-128加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm128\_hard\_decrypt\_dma

#### 描述

AES-GCM-128解密运算。输入数据使用cpu传输，输出数据都使用dma传输。

#### 函数原型

```c
void aes_gcm128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context    |AES-GCM-128解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-128待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-128待解密密文数据的长度。| 输入 |
|output\_data  |AES-GCM-128解密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。| 输出 |
|gcm\_tag  |AES-GCM-128解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm192\_hard\_encrypt\_dma

#### 描述

AES-GCM-192加密运算。输入数据使用cpu传输，输出数据都使用dma传输。

#### 函数原型

```c
void aes_gcm192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-GCM-192加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-192待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-192待加密明文数据的长度。| 输入 |
|output\_data  |AES-GCM-192加密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。| 输出 |
|gcm\_tag  |AES-GCM-192加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm192\_hard\_decrypt\_dma

#### 描述

AES-GCM-192解密运算。输入数据使用cpu传输，输出数据都使用dma传输。

#### 函数原型

```c
void aes_gcm192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-GCM-192解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-192待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-192待解密密文数据的长度。| 输入 |
|output\_data  |AES-GCM-192解密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。| 输出 |
|gcm\_tag  |AES-GCM-192解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm256\_hard\_encrypt\_dma

#### 描述

AES-GCM-256加密运算。输入数据使用cpu传输，输出数据都使用dma传输。

#### 函数原型

```c
void aes_gcm256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| :------:      |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context      |AES-GCM-256加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-256待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-256待加密明文数据的长度。| 输入 |
|output\_data  |AES-GCM-256加密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。| 输出 |
|gcm\_tag  |AES-GCM-256加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm256\_hard\_decrypt\_dma

#### 描述

AES-GCM-256解密运算。输入数据使用cpu传输，输出数据都使用dma传输。

#### 函数原型

```c
void aes_gcm256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称    |  描述                          |输入输出|
| :------:  |:-----                         | :----: |
|dma\_receive\_channel\_num|AES输出数据的DMA通道号  | 输入 |
|context |AES-GCM-256解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-256待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-256待解密密文数据的长度。| 输入 |
|output\_data  |AES-GCM-256解密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。| 输出 |
|gcm\_tag  |AES-GCM-256解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_init

#### 描述

AES硬件模块的初始化

#### 函数原型

```c
void aes_init(uint8_t *input_key, size_t input_key_len, uint8_t *iv,size_t iv_len, uint8_t *gcm_aad,aes_cipher_mode_t cipher_mode, aes_encrypt_sel_t encrypt_sel, size_t gcm_aad_len, size_t input_data_len)
```

#### 参数

| 参数名称    |  描述                          |输入输出|
| :------:  |:-----                         | :----: |
|input\_key  |待加密/解密的密钥                | 输入 |
|input\_key_len|待加密/解密密钥的长度          | 输入 |
|iv       |AES加密解密用到的iv数据            | 输入 |
|iv\_len  |AES加密解密用到的iv数据的长度，CBC固定为16bytes，GCM固定为12bytes| 输出 |
|gcm\_aad  |AES-GCM加密解密用到的aad数据       | 输出 |
|cipher\_mode|AES硬件模块执行的加密解密类型，支持AES\_CBC/AES\_ECB/AES\_GCM| 输入 |
|encrypt\_sel  |AES硬件模块执行的模式：加密或解密| 输入 |
|gcm\_aad\_len |AES-GCM加密解密用到的aad数据的长度| 输入 |
|input\_data\_len |待加密/解密的数据长度          | 输入 |

#### 返回值

无。

### aes\_process

#### 描述

AES硬件模块执行加密解密操作

#### 函数原型

```c
void aes_process(uint8_t *input_data, uint8_t *output_data, size_t input_data_len, aes_cipher_mode_t cipher_mode)
```

#### 参数

| 参数名称    |  描述                          |输入输出|
| :------:   |:-----                          | :----: |
|input\_data |这个buffer存放待加密/解密的数据   | 输入 |
|output\_data|这个buffer存放加密/解密的输出结果 | 输出 |
|input\_data\_len|待加密/解密的数据的长度        | 输入 |
|cipher\_mode |AES硬件模块执行的加密解密类型，支持AES\_CBC/AES\_ECB/AES\_GCM| 输入 |

#### 返回值

无。

### gcm\_get\_tag

#### 描述

获取AES-GCM计算结束后的tag

#### 函数原型

```c
void gcm_get_tag(uint8_t *gcm_tag)
```

#### 参数

| 参数名称    |  描述                          |输入输出|
| :------:  |:-----                         | :----: |
|gcm\_tag |这个buffer存放AES-GCM加密/解密后的tag，固定为16bytes的大小| 输入出|

#### 返回值

无。

### 举例

```c
cbc_context_t cbc_context;
cbc_context.input_key = cbc_key;
cbc_context.iv = cbc_iv;
aes_cbc128_hard_encrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
memcpy(aes_input_data, aes_output_data, 16L);
aes_cbc128_hard_decrypt(&cbc_context, aes_input_data, 16L, aes_output_data);

```

## 数据类型

相关数据类型、数据结构定义如下：

- `aes_cipher_mode_t`：AES加密/解密的方式。

### aes\_cipher\_mode\_t

#### 描述

AES加密/解密的方式。

#### 定义

```c
typedef enum _aes_cipher_mode
{
    AES_ECB = 0,
    AES_CBC = 1,
    AES_GCM = 2,
    AES_CIPHER_MAX
} aes_cipher_mode_t;
```

- `gcm_context_t`：AES-GCM加密/解密时参数用到的结构体

### gcm\_context\_t

#### 描述

AES-GCM参数用到的结构体，包括密钥、偏移向量、aad数据、aad数据长度。

#### 定义

```c
typedef struct _gcm_context
{
    uint8_t *input_key;
    uint8_t *iv;
    uint8_t *gcm_aad;
    size_t gcm_aad_len;
} gcm_context_t;
```

- `cbc_context_t`：AES-CBC加密/解密时参数用到的结构体

### cbc\_context\_t

#### 描述

AES-CBC参数用到的结构体，包括密钥、偏移向量。

#### 定义

```c
typedef struct _cbc_context
{
    uint8_t *input_key;
    uint8_t *iv;
} cbc_context_t;
```

#### 成员

| 成员名称 | 描述 |
| :----- | :--- |
| AES\_ECB | ECB加密/解密 |
| AES\_CBC | CBC加密/解密 |
| AES\_GCM | GCM加密/解密 |