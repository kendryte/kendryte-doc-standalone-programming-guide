# Advanced Encryption Standard acceleration engine(AES)

## Overview

The AES module uses hardware to implement AES operation acceleration.

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

AES-ECB-128 encryption operation.
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
|   input\_key   | AES-ECB-128 encryption key                                                                                                                             |      Input      |
|  input\_data   | AES-ECB-128 plaintext data to be encrypted                                                                                                             |      Input      |
|   input\_len   | AES-ECB-128 length of plaintext data to be encrypted                                                                                                   |      Input      |
|  output\_data  | The result of the AES-ECB-128 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be guaranteed to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb128\_hard\_decrypt

#### Description

AES-ECB-128 decryption operation.
Input or output data is transmitted using CPU. ECB encryption encrypts the
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient. The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb128_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|   input\_key   | AES-ECB-128 decryption key                                                                                                            |      Input      |
|  input\_data   | AES-ECB-128 ciphertext data to be decrypted                                                                                           |      Input      |
|   input\_len   | AES-ECB-128 length of ciphertext data to be decrypted                                                                                 |      Input      |
|  output\_data  | The result of the AES-ECB-128 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb192\_hard\_encrypt

#### Description

AES-ECB-192 encryption operation.
Input or output data is transmitted using CPU. ECB encryption encrypts the
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient. The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb192_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|   input\_key   | AES-ECB-192 encryption key                                                                                                            |      Input      |
|  input\_data   | AES-ECB-192 plaintext data to be encrypted                                                                                            |      Input      |
|   input\_len   | AES-ECB-192 length of plaintext data to be encrypted                                                                                  |      Input      |
|  output\_data  | The result of the AES-ECB-192 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb192\_hard\_decrypt

#### Description

AES-ECB-192 decryption operation.
Input or output data is transmitted using CPU. ECB encryption encrypts the
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient. The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb192_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|   input\_key   | AES-ECB-192 decryption key                                                                                                            |      Input      |
|  input\_data   | AES-ECB-192 Ciphertext data to be decrypted                                                                                           |      Input      |
|   input\_len   | AES-ECB-192 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|  output\_data  | The result of the AES-ECB-192 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb256\_hard\_encrypt

#### Description

AES-ECB-256 encryption operation.
Input or output data is transmitted using CPU. ECB encryption encrypts the
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient. The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb256_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|   input\_key   | AES-ECB-256 encryption key                                                                                                            |      Input      |
|  input\_data   | AES-ECB-256 plaintext data to be encrypted                                                                                            |      Input      |
|   input\_len   | AES-ECB-256 length of plaintext data to be encrypted                                                                                  |      Input      |
|  output\_data  | The result of the AES-ECB-256 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb256\_hard\_decrypt

#### Description

AES-ECB-256 decryption operation.
Input or output data is transmitted using CPU. ECB encryption encrypts the
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient. The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|   input\_key   | AES-ECB-256 decryption key                                                                                                            |      Input      |
|  input\_data   | AES-ECB-256 Ciphertext data to be decrypted                                                                                           |      Input      |
|   input\_len   | AES-ECB-256 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|  output\_data  | The result of the AES-ECB-256 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc128\_hard\_encrypt

#### Description

AES-CBC-128 encryption operation.
Input or output data is transferred using the CPU. CBC encryption encrypts
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient.

#### Function prototype

```c
void aes_cbc128_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|    context     | AES-CBC-128 encryption operation structure containing encryption key and offset vector                                                |      Input      |
|  input\_data   | AES-CBC-128 plaintext data to be encrypted                                                                                            |      Input      |
|   input\_len   | AES-CBC-128 length of plaintext data to be encrypted                                                                                  |      Input      |
|  output\_data  | The result of the AES-CBC-128 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc128\_hard\_decrypt

#### Description

AES-CBC-128 decryption operation.
Input or output data is transferred using the CPU. CBC encryption encrypts
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient.

#### Function prototype

```c
void aes_cbc128_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|    context     | AES-CBC-128 Decryption operation structure, including decryption key and offset vector                                                |      Input      |
|  input\_data   | AES-CBC-128 Ciphertext data to be decrypted                                                                                           |      Input      |
|   input\_len   | AES-CBC-128 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|  output\_data  | The result of the AES-CBC-128 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc192\_hard\_encrypt

#### Description

AES-CBC-192 encryption operation.
Input or output data is transferred using the CPU. CBC encryption encrypts
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient.

#### Function prototype

```c
void aes_cbc192_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|    context     | AES-CBC-192 encryption operation structure containing encryption key and offset vector                                                |      Input      |
|  input\_data   | AES-CBC-192 plaintext data to be encrypted                                                                                            |      Input      |
|   input\_len   | AES-CBC-192 length of plaintext data to be encrypted                                                                                  |      Input      |
|  output\_data  | The result of the AES-CBC-192 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc192\_hard\_decrypt

#### Description

AES-CBC-192 decryption operation.
Input or output data is transferred using the CPU. CBC encryption encrypts
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient.

#### Function prototype

```c
void aes_cbc192_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|    context     | AES-CBC-192 Decryption operation structure, including decryption key and offset vector                                                |      Input      |
|  input\_data   | AES-CBC-192 Ciphertext data to be decrypted                                                                                           |      Input      |
|   input\_len   | AES-CBC-192 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|  output\_data  | The result of the AES-CBC-192 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc256\_hard\_encrypt

#### Description

AES-CBC-256 encryption operation.
Input or output data is transferred using the CPU. CBC encryption encrypts
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient.

#### Function prototype

```c
void aes_cbc256_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|    context     | AES-CBC-256 encryption operation structure containing encryption key and offset vector                                                |      Input      |
|  input\_data   | AES-CBC-256 plaintext data to be encrypted                                                                                            |      Input      |
|   input\_len   | AES-CBC-256 length of plaintext data to be encrypted                                                                                  |      Input      |
|  output\_data  | The result of the AES-CBC-256 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc256\_hard\_decrypt

#### Description

AES-CBC-256 decryption operation.
Input or output data is transferred using the CPU. CBC encryption encrypts
plaintext according to a block of fixed size of 16 bytes, and fills it when the
block size is insufficient.

#### Function prototype

```c
void aes_cbc256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name |                                                              Description                                                              | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
|    context     | AES-CBC-256 Decryption operation structure, including decryption key and offset vector                                                |      Input      |
|  input\_data   | AES-CBC-256 Ciphertext data to be decrypted                                                                                           |      Input      |
|   input\_len   | AES-CBC-256 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|  output\_data  | The result of the AES-CBC-256 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_gcm128\_hard\_encrypt

#### Description

AES-GCM-128 encryption operation.
Input or output data is transferred using the CPU.

#### Function prototype

```c
void aes_gcm128_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                                              Description                                                               | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-128 The structure of the encryption operation, including the encryption key / offset vector / aad / aad length                 |      Input      |
|  input\_data   | AES-GCM-128 plaintext data to be encrypted                                                                                             |      Input      |
|   input\_len   | AES-GCM-128 length of plaintext data to be encrypted                                                                                   |      Input      |
|  output\_data  | The result of the AES-GCM-128 encryption operation is stored in this buffer.                                                           |     Output      |
|    gcm\_tag    | AES-GCM-128 The tag after the encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes |     Output      |

#### Return value

None.

### aes\_gcm128\_hard\_decrypt

#### Description

AES-GCM-128 decryption operation.
Input or output data is transferred using the CPU.

#### Function prototype

```c
void aes_gcm128_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                                              Description                                                               | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-128 The structure of the decryption operation, including the decryption key/offset vector/aad/aad length                       |      Input      |
|  input\_data   | AES-GCM-128 Ciphertext data to be decrypted                                                                                            |      Input      |
|   input\_len   | AES-GCM-128 Length of ciphertext data to be decrypted                                                                                  |      Input      |
|  output\_data  | The result of the AES-GCM-128 decryption operation is stored in this buffer                                                            |     Output      |
|    gcm\_tag    | AES-GCM-128 The tag after the decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes |     Output      |

#### Return value

None.

### aes\_gcm192\_hard\_encrypt

#### Description

AES-GCM-192 encryption operation.
Input or output data is transferred using the CPU.

#### Function prototype

```c
void aes_gcm192_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                                              Description                                                               | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-192 The structure of the encryption operation, including the encryption key / offset vector / aad / aad length                 |      Input      |
|  input\_data   | AES-GCM-192 plaintext data to be encrypted                                                                                             |      Input      |
|   input\_len   | AES-GCM-192 length of plaintext data to be encrypted                                                                                   |      Input      |
|  output\_data  | The result of the AES-GCM-192 encryption operation is stored in this buffer.                                                           |     Output      |
|    gcm\_tag    | AES-GCM-192 The tag after the encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes |     Output      |

#### Return value

None.

### aes\_gcm192\_hard\_decrypt

#### Description

AES-GCM-192 decryption operation.
Input or output data is transferred using the CPU.

#### Function prototype

```c
void aes_gcm192_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                                              Description                                                               | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-192 The structure of the decryption operation, including the decryption key/offset vector/aad/aad length                       |      Input      |
|  input\_data   | AES-GCM-192 Ciphertext data to be decrypted                                                                                            |      Input      |
|   input\_len   | AES-GCM-192 Length of ciphertext data to be decrypted                                                                                  |      Input      |
|  output\_data  | The result of the AES-GCM-192 decryption operation is stored in this buffer                                                            |     Output      |
|    gcm\_tag    | AES-GCM-192 The tag after the decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes |     Output      |

#### Return value

None.

### aes\_gcm256\_hard\_encrypt

#### Description

AES-GCM-256 encryption operation.
Input or output data is transferred using the CPU.

#### Function prototype

```c
void aes_gcm256_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                                              Description                                                               | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-256 The structure of the encryption operation, including the encryption key / offset vector / aad / aad length                 |      Input      |
|  input\_data   | AES-GCM-256 plaintext data to be encrypted                                                                                             |      Input      |
|   input\_len   | AES-GCM-256 length of plaintext data to be encrypted                                                                                   |      Input      |
|  output\_data  | The result of the AES-GCM-256 encryption operation is stored in this buffer.                                                           |     Output      |
|    gcm\_tag    | AES-GCM-256 The tag after the encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes |     Output      |

#### Return value

None.

### aes\_gcm256\_hard\_decrypt

#### Description

AES-GCM-256 decryption operation.
Input or output data is transferred using the CPU.

#### Function prototype

```c
void aes_gcm256_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                                              Description                                                               | Input or output |
| :------------: | :------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
|    context     | AES-GCM-256 The structure of the decryption operation, including the decryption key/offset vector/aad/aad length                       |      Input      |
|  input\_data   | AES-GCM-256 Ciphertext data to be decrypted                                                                                            |      Input      |
|   input\_len   | AES-GCM-256 Length of ciphertext data to be decrypted                                                                                  |      Input      |
|  output\_data  | The result of the AES-GCM-256 decryption operation is stored in this buffer                                                            |     Output      |
|    gcm\_tag    | AES-GCM-256 The tag after the decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes |     Output      |

#### Return value

None.

### aes\_ecb128\_hard\_encrypt\_dma

#### Description

AES-ECB-128 encryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. ECB encryption encrypts the plaintext according to a block of
fixed size of 16 bytes, and fills it when the block size is insufficient.
The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|         input\_key         | AES-ECB-128 encryption key                                                                                                            |      Input      |
|        input\_data         | AES-ECB-128 plaintext data to be encrypted                                                                                            |      Input      |
|         input\_len         | AES-ECB-128 length of plaintext data to be encrypted                                                                                  |      Input      |
|        output\_data        | The result of the AES-ECB-128 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb128\_hard\_decrypt\_dma

#### Description

AES-ECB-128 decryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. ECB encryption encrypts the plaintext according to a block of
fixed size of 16 bytes, and fills it when the block size is insufficient.
The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|         input\_key         | AES-ECB-128 decryption key                                                                                                            |      Input      |
|        input\_data         | AES-ECB-128 Ciphertext data to be decrypted                                                                                           |      Input      |
|         input\_len         | AES-ECB-128 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|        output\_data        | The result of the AES-ECB-128 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb192\_hard\_encrypt\_dma

#### Description

AES-ECB-192 encryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. ECB encryption encrypts the plaintext according to a block of
fixed size of 16 bytes, and fills it when the block size is insufficient.
The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|         input\_key         | AES-ECB-192 encryption key                                                                                                            |      Input      |
|        input\_data         | AES-ECB-192 plaintext data to be encrypted                                                                                            |      Input      |
|         input\_len         | AES-ECB-192 length of plaintext data to be encrypted                                                                                  |      Input      |
|        output\_data        | The result of the AES-ECB-192 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb192\_hard\_decrypt\_dma

#### Description

AES-ECB-192 decryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. ECB encryption encrypts the plaintext according to a block of
fixed size of 16 bytes, and fills it when the block size is insufficient.
The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|         input\_key         | AES-ECB-192 decryption key                                                                                                            |      Input      |
|        input\_data         | AES-ECB-192 Ciphertext data to be decrypted                                                                                           |      Input      |
|         input\_len         | AES-ECB-192 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|        output\_data        | The result of the AES-ECB-192 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb256\_hard\_encrypt\_dma

#### Description

AES-ECB-256 encryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. ECB encryption encrypts the plaintext according to a block of
fixed size of 16 bytes, and fills it when the block size is insufficient.
The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|         input\_key         | AES-ECB-256 encryption key                                                                                                            |      Input      |
|        input\_data         | AES-ECB-256 plaintext data to be encrypted                                                                                            |      Input      |
|         input\_len         | AES-ECB-256 length of plaintext data to be encrypted                                                                                  |      Input      |
|        output\_data        | The result of the AES-ECB-256 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_ecb256\_hard\_decrypt\_dma

#### Description

AES-ECB-256 decryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. ECB encryption encrypts the plaintext according to a block of
fixed size of 16 bytes, and fills it when the block size is insufficient.
The initialization vector(iv) is not used in ECB mode.

#### Function prototype

```c
void aes_ecb256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|         input\_key         | AES-ECB-256 decryption key                                                                                                            |      Input      |
|        input\_data         | AES-ECB-256 Ciphertext data to be decrypted                                                                                           |      Input      |
|         input\_len         | AES-ECB-256 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|        output\_data        | The result of the AES-ECB-256 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc128\_hard\_encrypt\_dma

#### Description

AES-CBC-128 encryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. CBC encryption encrypts plaintext according to a block of fixed
size of 16 bytes, and fills it when the block size is insufficient.

#### Function prototype

```c
void aes_cbc128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|          context           | AES-CBC-128 encryption operation structure containing encryption key and offset vector                                                |      Input      |
|        input\_data         | AES-CBC-128 plaintext data to be encrypted                                                                                            |      Input      |
|         input\_len         | AES-CBC-128 length of plaintext data to be encrypted                                                                                  |      Input      |
|        output\_data        | The result of the AES-CBC-128 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc128\_hard\_decrypt\_dma

#### Description

AES-CBC-128 decryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. CBC encryption encrypts plaintext according to a block of fixed
size of 16 bytes, and fills it when the block size is insufficient.

#### Function prototype

```c
void aes_cbc128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|          context           | AES-CBC-128 Decryption operation structure, including decryption key and offset vector                                                |      Input      |
|        input\_data         | AES-CBC-128 Ciphertext data to be decrypted                                                                                           |      Input      |
|         input\_len         | AES-CBC-128 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|        output\_data        | The result of the AES-CBC-128 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc192\_hard\_encrypt\_dma

#### Description

AES-CBC-192 encryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. CBC encryption encrypts plaintext according to a block of fixed
size of 16 bytes, and fills it when the block size is insufficient.

#### Function prototype

```c
void aes_cbc192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|          context           | AES-CBC-192 encryption operation structure containing encryption key and offset vector                                                |      Input      |
|        input\_data         | AES-CBC-192 plaintext data to be encrypted                                                                                            |      Input      |
|         input\_len         | AES-CBC-192 length of plaintext data to be encrypted                                                                                  |      Input      |
|        output\_data        | The result of the AES-CBC-192 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc192\_hard\_decrypt\_dma

#### Description

AES-CBC-192 decryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. CBC encryption encrypts plaintext according to a block of fixed
size of 16 bytes, and fills it when the block size is insufficient.

#### Function prototype

```c
void aes_cbc192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|          context           | AES-CBC-192 Decryption operation structure, including decryption key and offset vector                                                |      Input      |
|        input\_data         | AES-CBC-192 Ciphertext data to be decrypted                                                                                           |      Input      |
|         input\_len         | AES-CBC-192 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|        output\_data        | The result of the AES-CBC-192 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc256\_hard\_encrypt\_dma

#### Description

AES-CBC-256 encryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. CBC encryption encrypts plaintext according to a block of fixed
size of 16 bytes, and fills it when the block size is insufficient.

#### Function prototype

```c
void aes_cbc256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|          context           | AES-CBC-256 encryption operation structure containing encryption key and offset vector                                                |      Input      |
|        input\_data         | AES-CBC-256 plaintext data to be encrypted                                                                                            |      Input      |
|         input\_len         | AES-CBC-256 length of plaintext data to be encrypted                                                                                  |      Input      |
|        output\_data        | The result of the AES-CBC-256 encryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_cbc256\_hard\_decrypt\_dma

#### Description

AES-CBC-256 decryption operation.
The Input data is transmitted using the CPU, and the Output data is transmitted
using the DMA. CBC encryption encrypts plaintext according to a block of fixed
size of 16 bytes, and fills it when the block size is insufficient.

#### Function prototype

```c
void aes_cbc256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

|       Parameter name       |                                                              Description                                                              | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                 |      Input      |
|          context           | AES-CBC-256 Decryption operation structure, including decryption key and offset vector                                                |      Input      |
|        input\_data         | AES-CBC-256 Ciphertext data to be decrypted                                                                                           |      Input      |
|         input\_len         | AES-CBC-256 Length of ciphertext data to be decrypted                                                                                 |      Input      |
|        output\_data        | The result of the AES-CBC-256 decryption operation is stored in this buffer.<br/>The size of this buffer needs to be 16bytes aligned. |     Output      |

#### Return value

None.

### aes\_gcm128\_hard\_encrypt\_dma

#### Description

AES-GCM-128 encryption operation.
The Input data is transmitted using the CPU,
and the Output data is transmitted using the DMA.

#### Function prototype

```c
void aes_gcm128_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                                                                     Description                                                                                                                     | Input or output |
| :------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                                                                                                                               |      Input      |
|          context           | AES-GCM-128 The structure of the encryption operation, including the encryption key / offset vector / aad / aad length                                                                                                                              |      Input      |
|        input\_data         | AES-GCM-128 plaintext data to be encrypted                                                                                                                                                                                                          |      Input      |
|         input\_len         | AES-GCM-128 length of plaintext data to be encrypted。                                                                                                                                                                                              |      Input      |
|        output\_data        | The result of the AES-GCM-128 encryption operation is stored in this buffer.。<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes. |     Output      |
|          gcm\_tag          | AES-GCM-128 The tag after the encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes                                                                                                              |     Output      |

#### Return value

None.

### aes\_gcm128\_hard\_decrypt\_dma

#### Description

AES-GCM-128 decryption operation.
The Input data is transmitted using the CPU,
and the Output data is transmitted using the DMA.

#### Function prototype

```c
void aes_gcm128_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                                                                    Description                                                                                                                    | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                                                                                                                             |      Input      |
|          context           | AES-GCM-128 The structure of the decryption operation, including the decryption key/offset vector/aad/aad length                                                                                                                                  |      Input      |
|        input\_data         | AES-GCM-128 Ciphertext data to be decrypted                                                                                                                                                                                                       |      Input      |
|         input\_len         | AES-GCM-128 Length of ciphertext data to be decrypted。                                                                                                                                                                                           |      Input      |
|        output\_data        | The result of the AES-GCM-128 decryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes. |     Output      |
|          gcm\_tag          | AES-GCM-128 The tag after the decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes                                                                                                            |     Output      |

#### Return value

None.

### aes\_gcm192\_hard\_encrypt\_dma

#### Description

AES-GCM-192 encryption operation.
The Input data is transmitted using the CPU,
and the Output data is transmitted using the DMA.

#### Function prototype

```c
void aes_gcm192_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                                                                    Description                                                                                                                    | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                                                                                                                             |      Input      |
|          context           | AES-GCM-192 The structure of the encryption operation, including the encryption key / offset vector / aad / aad length                                                                                                                            |      Input      |
|        input\_data         | AES-GCM-192 plaintext data to be encrypted                                                                                                                                                                                                        |      Input      |
|         input\_len         | AES-GCM-192 length of plaintext data to be encrypted。                                                                                                                                                                                            |      Input      |
|        output\_data        | The result of the AES-GCM-192 encryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes. |     Output      |
|          gcm\_tag          | AES-GCM-192 The tag after the encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes                                                                                                            |     Output      |

#### Return value

None.

### aes\_gcm192\_hard\_decrypt\_dma

#### Description

AES-GCM-192 decryption operation.
The Input data is transmitted using the CPU,
and the Output data is transmitted using the DMA.

#### Function prototype

```c
void aes_gcm192_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                                                                    Description                                                                                                                    | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                                                                                                                             |      Input      |
|          context           | AES-GCM-192 The structure of the decryption operation, including the decryption key/offset vector/aad/aad length                                                                                                                                  |      Input      |
|        input\_data         | AES-GCM-192 Ciphertext data to be decrypted                                                                                                                                                                                                       |      Input      |
|         input\_len         | AES-GCM-192 Length of ciphertext data to be decrypted。                                                                                                                                                                                           |      Input      |
|        output\_data        | The result of the AES-GCM-192 decryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes. |     Output      |
|          gcm\_tag          | AES-GCM-192 The tag after the decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes                                                                                                            |     Output      |

#### Return value

None.

### aes\_gcm256\_hard\_encrypt\_dma

#### Description

AES-GCM-256 encryption operation.
The Input data is transmitted using the CPU,
and the Output data is transmitted using the DMA.

#### Function prototype

```c
void aes_gcm256_hard_encrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                                                                    Description                                                                                                                    | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                                                                                                                             |      Input      |
|          context           | AES-GCM-256 The structure of the encryption operation, including the encryption key / offset vector / aad / aad length                                                                                                                            |      Input      |
|        input\_data         | AES-GCM-256 plaintext data to be encrypted                                                                                                                                                                                                        |      Input      |
|         input\_len         | AES-GCM-256 length of plaintext data to be encrypted。                                                                                                                                                                                            |      Input      |
|        output\_data        | The result of the AES-GCM-256 encryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes. |     Output      |
|          gcm\_tag          | AES-GCM-256 The tag after the encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes                                                                                                            |     Output      |

#### Return value

None.

### aes\_gcm256\_hard\_decrypt\_dma

#### Description

AES-GCM-256 decryption operation.
The Input data is transmitted using the CPU,
and the Output data is transmitted using the DMA.

#### Function prototype

```c
void aes_gcm256_hard_decrypt_dma(dmac_channel_number_t dma_receive_channel_num, gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

|       Parameter name       |                                                                                                                    Description                                                                                                                    | Input or output |
| :------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------: |
| dma\_receive\_channel\_num | DMA channel number of AES output data                                                                                                                                                                                                             |      Input      |
|          context           | AES-GCM-256 The structure of the decryption operation, including the decryption key/offset vector/aad/aad length                                                                                                                                  |      Input      |
|        input\_data         | AES-GCM-256 Ciphertext data to be decrypted                                                                                                                                                                                                       |      Input      |
|         input\_len         | AES-GCM-256 Length of ciphertext data to be decrypted。                                                                                                                                                                                           |      Input      |
|        output\_data        | The result of the AES-GCM-256 decryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes. |     Output      |
|          gcm\_tag          | AES-GCM-256 The tag after the decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes                                                                                                            |     Output      |

#### Return value

None.

### aes\_init

#### Description

Initialization of the AES hardware module

#### Function prototype

```c
void aes_init(uint8_t *input_key, size_t input_key_len, uint8_t *iv,size_t iv_len, uint8_t *gcm_aad,aes_cipher_mode_t cipher_mode, aes_encrypt_sel_t encrypt_sel, size_t gcm_aad_len, size_t input_data_len)
```

#### Parameter

|  Parameter name  |                                                       Description                                                       | Input or output |
| :--------------: | :---------------------------------------------------------------------------------------------------------------------- | :-------------: |
|    input\_key    | Encryption/decryption key                                                                                               |      Input      |
|  input\_key_len  | The length of the key to be used for encryption/decryption                                                              |      Input      |
|        iv        | AES encryption and decryption iv data                                                                                   |      Input      |
|     iv\_len      | The length of the iv data used for AES encryption and decryption, CBC is fixed to 16bytes, and GCM is fixed to 12bytes. |     Output      |
|     gcm\_aad     | aad data used by AES-GCM encryption and decryption                                                                      |     Output      |
|   cipher\_mode   | The type of encryption and decryption performed by the AES hardware module, supporting AES\_CBC/AES\_ECB/AES\_GCM       |      Input      |
|   encrypt\_sel   | Execution mode of the AES hardware module: encryption or decryption                                                     |      Input      |
|  gcm\_aad\_len   | Length of aad data used by AES-GCM encryption and decryption                                                            |      Input      |
| input\_data\_len | Length of data to be encrypted/decrypted                                                                                |      Input      |

#### Return value

None.

### aes\_process

#### Description

AES hardware module performs encryption and decryption operations

#### Function prototype

```c
void aes_process(uint8_t *input_data, uint8_t *output_data, size_t input_data_len, aes_cipher_mode_t cipher_mode)
```

#### Parameter

|  Parameter name  |                                              Description                                               | Input or output |
| :--------------: | :----------------------------------------------------------------------------------------------------- | :-------------: |
|   input\_data    | This buffer stores the data to be encrypted/decrypted                                                  |      Input      |
|   output\_data   | This buffer stores the output result of encryption/decryption                                          |     Output      |
| input\_data\_len | Length of data to be encrypted/decrypted                                                               |      Input      |
|   cipher\_mode   | Encryption and decryption type performed by AES hardware module, supporting AES\_CBC/AES\_ECB/AES\_GCM |      Input      |

#### Return value

None.

### gcm\_get\_tag

#### Description

Get the tag after the AES-GCM calculation is completed

#### Function prototype

```c
void gcm_get_tag(uint8_t *gcm_tag)
```

#### Parameter

| Parameter name |                                     Description                                     | Input or output |
| :------------: | :---------------------------------------------------------------------------------- | :-------------: |
|    gcm\_tag    | This buffer stores the AES-GCM encrypted/decrypted tag, fixed to a size of 16bytes. |     Output      |

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

The relevant data types and data structures are defined as follows:

- `aes_cipher_mode_t`：AES encryption/decryption method.

### aes\_cipher\_mode\_t

#### Description

AES encryption/decryption method.

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

- `gcm_context_t`：AES-GCM structure used for parameters during encryption/decryption

### gcm\_context\_t

#### Description

The structure used by the AES-GCM parameters, including the key, offset vector, aad data, and aad data length.

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

- `cbc_context_t`：AES-CBC structure used for parameters during encryption/decryption

### cbc\_context\_t

#### Description

The structure used by the AES-CBC parameter, including the key and offset vector.

#### Type definition

```c
typedef struct _cbc_context
{
    uint8_t *input_key;
    uint8_t *iv;
} cbc_context_t;
```

#### Enumeration element

| Element name |          Description          |
| :----------- | :---------------------------- |
| AES\_ECB     | ECB encryption and decryption |
| AES\_CBC     | CBC encryption and decryption |
| AES\_GCM     | GCM encryption and decryption |
