# Advanced Encryption Standard acceleration engine(AES)

## Features

K210 have a built-in AES(Advanced Encryption Standard acceleration engine).
Compared with software, it can greatly improve the speed of AES operation.
The AES accelerator supports multiple encryption/decryption modes (ECB, CBC, GCM)
and multiple length of KEY (128, 192, 256).

## API

Corresponding header file `aes.h`

Provide the following interfaces

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

#### Description

Provides efficient AES-ECB-128 encryption operation acceleration.
Input and output data are transmitted using CPU. ECB encryption encrypts the
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient. The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb128_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                                      Description                                                                       | Input or output |
| :------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
|   input\_key   | AES-ECB-128 encryption key                                                                                                                             |      Input       |
|  input\_data   | AES-ECB-128 plaintext data to be encrypted                                                                                                             |      Input       |
|   input\_len   | AES-ECB-128 length of plaintext data to be encrypted                                                                                                   |      Input       |
|  output\_data  | The result of the AES-ECB-128 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be guaranteed to be 16bytes aligned. |      Output       |

#### Return value

None.

### aes\_ecb128\_hard\_decrypt

#### Description

Provides efficient AES-ECB-128 decryption operation.
Input or output data is transmitted using CPU. ECB encryption encrypts the
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient. The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb128_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|   input\_key   | AES-ECB-128解密的密钥                                                                   |      Input       |
|  input\_data   | AES-ECB-128待解密的密文数据                                                             |      Input       |
|   input\_len   | AES-ECB-128待解密密文数据的长度                                                         |      Input       |
|  output\_data  | AES-ECB-128解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb192\_hard\_encrypt

#### Description

AES-ECB-192加密运算。Input or output数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb192_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|   input\_key   | AES-ECB-192加密的密钥                                                                   |      Input       |
|  input\_data   | AES-ECB-192待加密的明文数据                                                             |      Input       |
|   input\_len   | AES-ECB-192待加密明文数据的长度                                                         |      Input       |
|  output\_data  | AES-ECB-192加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb192\_hard\_decrypt

#### Description

AES-ECB-192解密运算。Input or output数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb192_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|   input\_key   | AES-ECB-192解密的密钥                                                                   |      Input       |
|  input\_data   | AES-ECB-192待解密的密文数据                                                             |      Input       |
|   input\_len   | AES-ECB-192待解密密文数据的长度                                                         |      Input       |
|  output\_data  | AES-ECB-192解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb256\_hard\_encrypt

#### Description

AES-ECB-256加密运算。Input or output数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb256_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|   input\_key   | AES-ECB-256加密的密钥                                                                   |      Input       |
|  input\_data   | AES-ECB-256待加密的明文数据                                                             |      Input       |
|   input\_len   | AES-ECB-256待加密明文数据的长度                                                         |      Input       |
|  output\_data  | AES-ECB-256加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb256\_hard\_decrypt

#### Description

AES-ECB-256解密运算。Input or output数据都使用cpu传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|   input\_key   | AES-ECB-256解密的密钥                                                                   |      Input       |
|  input\_data   | AES-ECB-256待解密的密文数据                                                             |      Input       |
|   input\_len   | AES-ECB-256待解密密文数据的长度                                                         |      Input       |
|  output\_data  | AES-ECB-256解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc128\_hard\_encrypt

#### Description

AES-CBC-128加密运算。Input or output数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc128_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-CBC-128加密计算的结构体，包含加密密钥与偏移向量                                     |      Input       |
|  input\_data   | AES-CBC-128待加密的明文数据                                                             |      Input       |
|   input\_len   | AES-CBC-128待加密明文数据的长度                                                         |      Input       |
|  output\_data  | AES-CBC-128加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc128\_hard\_decrypt

#### Description

AES-CBC-128解密运算。Input or output数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc128_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-CBC-128解密计算的结构体，包含解密密钥与偏移向量                                     |      Input       |
|  input\_data   | AES-CBC-128待解密的密文数据                                                             |      Input       |
|   input\_len   | AES-CBC-128待解密密文数据的长度                                                         |      Input       |
|  output\_data  | AES-CBC-128解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc192\_hard\_encrypt

#### Description

AES-CBC-192加密运算。Input or output数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc192_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-CBC-192加密计算的结构体，包含加密密钥与偏移向量                                     |      Input       |
|  input\_data   | AES-CBC-192待加密的明文数据                                                             |      Input       |
|   input\_len   | AES-CBC-192待加密明文数据的长度                                                         |      Input       |
|  output\_data  | AES-CBC-192加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc192\_hard\_decrypt

#### Description

AES-CBC-192解密运算。Input or output数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc192_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-CBC-192解密计算的结构体，包含解密密钥与偏移向量                                     |      Input       |
|  input\_data   | AES-CBC-192待解密的密文数据                                                             |      Input       |
|   input\_len   | AES-CBC-192待解密密文数据的长度                                                         |      Input       |
|  output\_data  | AES-CBC-192解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc256\_hard\_encrypt

#### Description

AES-CBC-256加密运算。Input or output数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc256_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-CBC-256加密计算的结构体，包含加密密钥与偏移向量                                     |      Input       |
|  input\_data   | AES-CBC-256待加密的明文数据                                                             |      Input       |
|   input\_len   | AES-CBC-256待加密明文数据的长度                                                         |      Input       |
|  output\_data  | AES-CBC-256加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc256\_hard\_decrypt

#### Description

AES-CBC-256解密运算。Input or output数据都使用cpu传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                       Description                                       | Input or output |
| :------------: | :-------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-CBC-256解密计算的结构体，包含解密密钥与偏移向量                                     |      Input       |
|  input\_data   | AES-CBC-256待解密的密文数据                                                             |      Input       |
|   input\_len   | AES-CBC-256待解密密文数据的长度                                                         |      Input       |
|  output\_data  | AES-CBC-256解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_gcm128\_hard\_encrypt

#### Description

AES-GCM-128加密运算。Input or output数据都使用cpu传输。

#### Function prototype

```c
void aes_gcm128_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                   Description                                    | Input or output |
| :------------: | :------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-128加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度                   |      Input       |
|  input\_data   | AES-GCM-128待加密的明文数据                                                      |      Input       |
|   input\_len   | AES-GCM-128待加密明文数据的长度                                                  |      Input       |
|  output\_data  | AES-GCM-128加密运算后的结果存放在这个buffer                                      |      Output       |
|    gcm\_tag    | AES-GCM-128加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes |      Output       |

#### Return value

None.

### aes\_gcm128\_hard\_decrypt

#### Description

AES-GCM-128解密运算。Input or output数据都使用cpu传输。

#### Function prototype

```c
void aes_gcm128_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                   Description                                    | Input or output |
| :------------: | :------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-128解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度                   |      Input       |
|  input\_data   | AES-GCM-128待解密的密文数据                                                      |      Input       |
|   input\_len   | AES-GCM-128待解密密文数据的长度                                                  |      Input       |
|  output\_data  | AES-GCM-128解密运算后的结果存放在这个buffer                                      |      Output       |
|    gcm\_tag    | AES-GCM-128解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes |      Output       |

#### Return value

None.

### aes\_gcm192\_hard\_encrypt

#### Description

AES-GCM-192加密运算。Input or output数据都使用cpu传输。

#### Function prototype

```c
void aes_gcm192_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                   Description                                    | Input or output |
| :------------: | :------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-192加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度                   |      Input       |
|  input\_data   | AES-GCM-192待加密的明文数据                                                      |      Input       |
|   input\_len   | AES-GCM-192待加密明文数据的长度                                                  |      Input       |
|  output\_data  | AES-GCM-192加密运算后的结果存放在这个buffer                                      |      Output       |
|    gcm\_tag    | AES-GCM-192加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes |      Output       |

#### Return value

None.

### aes\_gcm192\_hard\_decrypt

#### Description

AES-GCM-192解密运算。Input or output数据都使用cpu传输。

#### Function prototype

```c
void aes_gcm192_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                   Description                                    | Input or output |
| :------------: | :------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-192解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度                   |      Input       |
|  input\_data   | AES-GCM-192待解密的密文数据                                                      |      Input       |
|   input\_len   | AES-GCM-192待解密密文数据的长度                                                  |      Input       |
|  output\_data  | AES-GCM-192解密运算后的结果存放在这个buffer                                      |      Output       |
|    gcm\_tag    | AES-GCM-192解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes |      Output       |

#### Return value

None.

### aes\_gcm256\_hard\_encrypt

#### Description

AES-GCM-256加密运算。Input or output数据都使用cpu传输。

#### Function prototype

```c
void aes_gcm256_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                   Description                                    | Input or output |
| :------------: | :------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-256加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度                   |      Input       |
|  input\_data   | AES-GCM-256待加密的明文数据                                                      |      Input       |
|   input\_len   | AES-GCM-256待加密明文数据的长度                                                  |      Input       |
|  output\_data  | AES-GCM-256加密运算后的结果存放在这个buffer                                      |      Output       |
|    gcm\_tag    | AES-GCM-256加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes |      Output       |

#### Return value

None.

### aes\_gcm256\_hard\_decrypt

#### Description

AES-GCM-256解密运算。Input or output数据都使用cpu传输。

#### Function prototype

```c
void aes_gcm256_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                   Description                                    | Input or output |
| :------------: | :------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-256解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度                   |      Input       |
|  input\_data   | AES-GCM-256待解密的密文数据                                                      |      Input       |
|   input\_len   | AES-GCM-256待解密密文数据的长度                                                  |      Input       |
|  output\_data  | AES-GCM-256解密运算后的结果存放在这个buffer                                      |      Output       |
|    gcm\_tag    | AES-GCM-256解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes |      Output       |

#### Return value

None.

### aes\_ecb128\_hard\_encrypt\_dma

#### Description

AES-ECB-128加密运算。Input数据使用cpu传输，Output数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|         input\_key         | AES-ECB-128加密的密钥                                                                   |      Input       |
|        input\_data         | AES-ECB-128待加密的明文数据                                                             |      Input       |
|         input\_len         | AES-ECB-128待加密明文数据的长度                                                         |      Input       |
|        output\_data        | AES-ECB-128加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb128\_hard\_decrypt\_dma

#### Description

AES-ECB-128解密运算。Input数据使用cpu传输，Output数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|         input\_key         | AES-ECB-128解密的密钥                                                                   |      Input       |
|        input\_data         | AES-ECB-128待解密的密文数据                                                             |      Input       |
|         input\_len         | AES-ECB-128待解密密文数据的长度                                                         |      Input       |
|        output\_data        | AES-ECB-128解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb192\_hard\_encrypt\_dma

#### Description

AES-ECB-192加密运算。Input数据使用cpu传输，Output数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|         input\_key         | AES-ECB-192加密的密钥                                                                   |      Input       |
|        input\_data         | AES-ECB-192待加密的明文数据                                                             |      Input       |
|         input\_len         | AES-ECB-192待加密明文数据的长度                                                         |      Input       |
|        output\_data        | AES-ECB-192加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb192\_hard\_decrypt\_dma

#### Description

AES-ECB-192解密运算。Input数据使用cpu传输，Output数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|         input\_key         | AES-ECB-192解密的密钥                                                                   |      Input       |
|        input\_data         | AES-ECB-192待解密的密文数据                                                             |      Input       |
|         input\_len         | AES-ECB-192待解密密文数据的长度                                                         |      Input       |
|        output\_data        | AES-ECB-192解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb256\_hard\_encrypt\_dma

#### Description

AES-ECB-256加密运算。Input数据使用cpu传输，Output数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|         input\_key         | AES-ECB-256加密的密钥                                                                   |      Input       |
|        input\_data         | AES-ECB-256待加密的明文数据                                                             |      Input       |
|         input\_len         | AES-ECB-256待加密明文数据的长度                                                         |      Input       |
|        output\_data        | AES-ECB-256加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_ecb256\_hard\_decrypt\_dma

#### Description

AES-ECB-256解密运算。Input数据使用cpu传输，Output数据都使用dma传输。ECB加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。ECB模式没有用到向量。

#### Function prototype

```c
void aes_ecb256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|         input\_key         | AES-ECB-256解密的密钥                                                                   |      Input       |
|        input\_data         | AES-ECB-256待解密的密文数据                                                             |      Input       |
|         input\_len         | AES-ECB-256待解密密文数据的长度                                                         |      Input       |
|        output\_data        | AES-ECB-256解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc128\_hard\_encrypt\_dma

#### Description

AES-CBC-128加密运算。Input数据使用cpu传输，Output数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|          context           | AES-CBC-128加密计算的结构体，包含加密密钥与偏移向量                                     |      Input       |
|        input\_data         | AES-CBC-128待加密的明文数据                                                             |      Input       |
|         input\_len         | AES-CBC-128待加密明文数据的长度                                                         |      Input       |
|        output\_data        | AES-CBC-128加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc128\_hard\_decrypt\_dma

#### Description

AES-CBC-128解密运算。Input数据使用cpu传输，Output数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|          context           | AES-CBC-128解密计算的结构体，包含解密密钥与偏移向量                                     |      Input       |
|        input\_data         | AES-CBC-128待解密的密文数据                                                             |      Input       |
|         input\_len         | AES-CBC-128待解密密文数据的长度                                                         |      Input       |
|        output\_data        | AES-CBC-128解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc192\_hard\_encrypt\_dma

#### Description

AES-CBC-192加密运算。Input数据使用cpu传输，Output数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|          context           | AES-CBC-192加密计算的结构体，包含加密密钥与偏移向量                                     |      Input       |
|        input\_data         | AES-CBC-192待加密的明文数据                                                             |      Input       |
|         input\_len         | AES-CBC-192待加密明文数据的长度                                                         |      Input       |
|        output\_data        | AES-CBC-192加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc192\_hard\_decrypt\_dma

#### Description

AES-CBC-192解密运算。Input数据使用cpu传输，Output数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|          context           | AES-CBC-192解密计算的结构体，包含解密密钥与偏移向量                                     |      Input       |
|        input\_data         | AES-CBC-192待解密的密文数据                                                             |      Input       |
|         input\_len         | AES-CBC-192待解密密文数据的长度                                                         |      Input       |
|        output\_data        | AES-CBC-192解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc256\_hard\_encrypt\_dma

#### Description

AES-CBC-256加密运算。Input数据使用cpu传输，Output数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|          context           | AES-CBC-256加密计算的结构体，包含加密密钥与偏移向量                                     |      Input       |
|        input\_data         | AES-CBC-256待加密的明文数据                                                             |      Input       |
|         input\_len         | AES-CBC-256待加密明文数据的长度                                                         |      Input       |
|        output\_data        | AES-CBC-256加密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_cbc256\_hard\_decrypt\_dma

#### Description

AES-CBC-256解密运算。Input数据使用cpu传输，Output数据都使用dma传输。CBC加密将明文按照固定大小16bytes的块进行加密的，块大小不足则进行填充。

#### Function prototype

```c
void aes_cbc256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                       Description                                       | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                  |      Input       |
|          context           | AES-CBC-256解密计算的结构体，包含解密密钥与偏移向量                                     |      Input       |
|        input\_data         | AES-CBC-256待解密的密文数据                                                             |      Input       |
|         input\_len         | AES-CBC-256待解密密文数据的长度                                                         |      Input       |
|        output\_data        | AES-CBC-256解密运算后的结果存放在这个buffer。<br/>这个buffer的大小需要保证16bytes对齐。 |      Output       |

#### Return value

None.

### aes\_gcm128\_hard\_encrypt\_dma

#### Description

AES-GCM-128加密运算。Input数据使用cpu传输，Output数据都使用dma传输。

#### Function prototype

```c
void aes_gcm128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                 Description                                                                  | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                                                                       |      Input       |
|          context           | AES-GCM-128加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度                                                                               |      Input       |
|        input\_data         | AES-GCM-128待加密的明文数据                                                                                                                  |      Input       |
|         input\_len         | AES-GCM-128待加密明文数据的长度。                                                                                                            |      Input       |
|        output\_data        | AES-GCM-128加密运算后的结果存放在这个buffer。。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。 |      Output       |
|          gcm\_tag          | AES-GCM-128加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes                                                             |      Output       |

#### Return value

None.

### aes\_gcm128\_hard\_decrypt\_dma

#### Description

AES-GCM-128解密运算。Input数据使用cpu传输，Output数据都使用dma传输。

#### Function prototype

```c
void aes_gcm128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                Description                                                                 | Input or output |
| :------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                                                                     |      Input       |
|          context           | AES-GCM-128解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度                                                                             |      Input       |
|        input\_data         | AES-GCM-128待解密的密文数据                                                                                                                |      Input       |
|         input\_len         | AES-GCM-128待解密密文数据的长度。                                                                                                          |      Input       |
|        output\_data        | AES-GCM-128解密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。 |      Output       |
|          gcm\_tag          | AES-GCM-128解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes                                                           |      Output       |

#### Return value

None.

### aes\_gcm192\_hard\_encrypt\_dma

#### Description

AES-GCM-192加密运算。Input数据使用cpu传输，Output数据都使用dma传输。

#### Function prototype

```c
void aes_gcm192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                Description                                                                 | Input or output |
| :------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                                                                     |      Input       |
|          context           | AES-GCM-192加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度                                                                             |      Input       |
|        input\_data         | AES-GCM-192待加密的明文数据                                                                                                                |      Input       |
|         input\_len         | AES-GCM-192待加密明文数据的长度。                                                                                                          |      Input       |
|        output\_data        | AES-GCM-192加密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。 |      Output       |
|          gcm\_tag          | AES-GCM-192加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes                                                           |      Output       |

#### Return value

None.

### aes\_gcm192\_hard\_decrypt\_dma

#### Description

AES-GCM-192解密运算。Input数据使用cpu传输，Output数据都使用dma传输。

#### Function prototype

```c
void aes_gcm192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                Description                                                                 | Input or output |
| :------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                                                                     |      Input       |
|          context           | AES-GCM-192解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度                                                                             |      Input       |
|        input\_data         | AES-GCM-192待解密的密文数据                                                                                                                |      Input       |
|         input\_len         | AES-GCM-192待解密密文数据的长度。                                                                                                          |      Input       |
|        output\_data        | AES-GCM-192解密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。 |      Output       |
|          gcm\_tag          | AES-GCM-192解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes                                                           |      Output       |

#### Return value

None.

### aes\_gcm256\_hard\_encrypt\_dma

#### Description

AES-GCM-256加密运算。Input数据使用cpu传输，Output数据都使用dma传输。

#### Function prototype

```c
void aes_gcm256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                Description                                                                 | Input or output |
| :------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                                                                     |      Input       |
|          context           | AES-GCM-256加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度                                                                             |      Input       |
|        input\_data         | AES-GCM-256待加密的明文数据                                                                                                                |      Input       |
|         input\_len         | AES-GCM-256待加密明文数据的长度。                                                                                                          |      Input       |
|        output\_data        | AES-GCM-256加密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。 |      Output       |
|          gcm\_tag          | AES-GCM-256加密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes                                                           |      Output       |

#### Return value

None.

### aes\_gcm256\_hard\_decrypt\_dma

#### Description

AES-GCM-256解密运算。Input数据使用cpu传输，Output数据都使用dma传输。

#### Function prototype

```c
void aes_gcm256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                Description                                                                 | Input or output |
| :------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | AESOutput数据的DMA通道号                                                                                                                     |      Input       |
|          context           | AES-GCM-256解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度                                                                             |      Input       |
|        input\_data         | AES-GCM-256待解密的密文数据                                                                                                                |      Input       |
|         input\_len         | AES-GCM-256待解密密文数据的长度。                                                                                                          |      Input       |
|        output\_data        | AES-GCM-256解密运算后的结果存放在这个buffer。<br/>由于DMA搬运数据的最小粒度为4bytes，<br/>所以需要保证这个buffer大小至少为4bytes的整数倍。 |      Output       |
|          gcm\_tag          | AES-GCM-256解密运算后的tag存放在这个buffer。<br/>这个buffer大小需要保证为16bytes                                                           |      Output       |

#### Return value

None.

### aes\_init

#### Description

AES硬件模块的初始化

#### Function prototype

```c
void aes_init(uint8_t *input_key, size_t input_key_len, uint8_t *iv,size_t iv_len, uint8_t *gcm_aad,aes_cipher_mode_t cipher_mode, aes_encrypt_sel_t encrypt_sel, size_t gcm_aad_len, size_t input_data_len)
```

#### Parameter

|  Parameter name  |                            Description                            | Input or output |
| :--------------: | :---------------------------------------------------------------- | :-------------: |
|    input\_key    | 待加密/解密的密钥                                                 |      Input       |
|  input\_key_len  | 待加密/解密密钥的长度                                             |      Input       |
|        iv        | AES加密解密用到的iv数据                                           |      Input       |
|     iv\_len      | AES加密解密用到的iv数据的长度，CBC固定为16bytes，GCM固定为12bytes |      Output       |
|     gcm\_aad     | AES-GCM加密解密用到的aad数据                                      |      Output       |
|   cipher\_mode   | AES硬件模块执行的加密解密类型，支持AES\_CBC/AES\_ECB/AES\_GCM     |      Input       |
|   encrypt\_sel   | AES硬件模块执行的模式：加密或解密                                 |      Input       |
|  gcm\_aad\_len   | AES-GCM加密解密用到的aad数据的长度                                |      Input       |
| input\_data\_len | 待加密/解密的数据长度                                             |      Input       |

#### Return value

None.

### aes\_process

#### Description

AES硬件模块执行加密解密操作

#### Function prototype

```c
void aes_process(uint8_t *input_data, uint8_t *output_data, size_t input_data_len, aes_cipher_mode_t cipher_mode)
```

#### Parameter

|  Parameter name  |                          Description                          | Input or output |
| :--------------: | :------------------------------------------------------------ | :-------------: |
|   input\_data    | 这个buffer存放待加密/解密的数据                               |      Input       |
|   output\_data   | 这个buffer存放加密/解密的Output结果                             |      Output       |
| input\_data\_len | 待加密/解密的数据的长度                                       |      Input       |
|   cipher\_mode   | AES硬件模块执行的加密解密类型，支持AES\_CBC/AES\_ECB/AES\_GCM |      Input       |

#### Return value

None.

### gcm\_get\_tag

#### Description

获取AES-GCM计算结束后的tag

#### Function prototype

```c
void gcm_get_tag(uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                        Description                         | Input or output |
| :------------: | :--------------------------------------------------------- | :-------------: |
|    gcm\_tag    | 这个buffer存放AES-GCM加密/解密后的tag，固定为16bytes的大小 |     Output      |

#### Return value

None.

### Example

```c
cbc_context_t cbc_context;
cbc_context.input_key = cbc_key;
cbc_context.iv = cbc_iv;
aes_cbc128_hard_encrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
memcpy(aes_input_data, aes_output_data, 16L);
aes_cbc128_hard_decrypt(&cbc_context, aes_input_data, 16L, aes_output_data);

```

## Data type

相关数据类型、数据结构定义如下：

- `aes_cipher_mode_t`：AES加密/解密的方式。

### aes\_cipher\_mode\_t

#### Description

AES加密/解密的方式。

#### Type definition

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

#### Description

AES-GCM参数用到的结构体，包括密钥、偏移向量、aad数据、aad数据长度。

#### Type definition

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

#### Description

AES-CBC参数用到的结构体，包括密钥、偏移向量。

#### Type definition

```c
typedef struct _cbc_context
{
    uint8_t *input_key;
    uint8_t *iv;
} cbc_context_t;
```

#### Enumeration element

| Element name | Description  |
| :------- | :----------- |
| AES\_ECB | ECB加密/解密 |
| AES\_CBC | CBC加密/解密 |
| AES\_GCM | GCM加密/解密 |