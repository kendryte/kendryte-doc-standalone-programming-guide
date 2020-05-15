# 麦克风阵列处理器 (APU)

## 概述

APU 麦克风阵列语音数据加速计算处理器，能够实时计算不同方向的语音延时累加值，通过这个值来判断语音方向，以及选取某一方向的增强语音数据。

## 功能描述

APU 具备以下几个特点：

- 支持最多八个麦克风的数据

- 可以实时计算16个方向的语音延时累加值

- 支持选定方向的增强语音输出

## API 参考

对应的头文件 `apu.h`

为用户提供以下接口

- apu\_dir\_set\_prev\_fir

- apu\_dir\_set\_post\_fir

- apu\_voc\_set\_prev\_fir

- apu\_voc\_set\_post\_fir

- apu\_set\_delay

- apu\_voc\_set\_direction

- apu\_set\_channel\_enabled

- apu\_dir\_enable

- apu\_voc\_enable

### apu\_dir\_set\_prev\_fir

#### 描述

在计算各个方向的延时累加值之前的fir滤波系数。

#### 函数定义

```c
void apu_dir_set_prev_fir(uint16_t *fir_coef)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| fir\_coef                        | 17位滤波系数指针       | 输入      |

#### 返回值

无。

### apu\_dir\_set\_post\_fir

#### 描述

在计算各个方向的延时累加值之后的fir滤波系数。

#### 函数原型

```c
void apu_dir_set_post_fir(uint16_t *fir_coef)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| fir_coef                        | 17位滤波系数指针          | 输入      |

#### 返回值

无。

### apu\_voc\_set\_prev\_fir

#### 描述

在计算选定方向的延时累加值之前的fir滤波系数。

#### 函数原型

```c
void apu_voc_set_prev_fir(uint16_t *fir_coef)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| fir\_coef                       | 17位滤波系数指针          | 输入      |

#### 返回值

无。

### apu\_voc\_set\_post\_fir

#### 描述

在计算选定方向的延时累加值之后的fir滤波系数。

#### 函数原型

```c
void apu_voc_set_post_fir(uint16_t *fir_coef)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| fir_coef                        | 17位滤波系数指针          | 输入      |

#### 返回值

无。

### apu\_set\_delay

#### 描述

初始化圆形麦克风阵列板子上麦克风之间的声波延时参数。

#### 函数原型

```c
void apu_set_delay(float R, uint8_t mic_num_a_circle, uint8_t center, float I2s_fs)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| R                            | 麦克风围成的圆半径           | 输入      |
| mic_num_a_circle             | 在圆周上的麦克风个数         | 输入      |
| center                       | 圆心点上是否有麦克风         | 输入      |
| I2s_fs                       | 麦克风采样率                | 输入      |

#### 返回值

无。

### apu\_voc\_set\_direction

#### 描述

选择语音增强的方向。

#### 函数原型

```c
void apu_voc_set_direction(enum en_bf_dir direction)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| direction                       | 选择语音增强的方向，取0~15 | 输入      |

#### 返回值

无。

### apu\_set\_channel\_enabled

#### 描述

选择使用的麦克风通道，I2S可用4路，每路有左右声道，共8个通道，相应位为1，则选择使用这个通道。

#### 函数原型

```c
void apu_set_channel_enabled(uint8_t channel_bit)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| channel_bit                 | 相应位为1，则选择使用这个通道。  | 输入      |

#### 返回值

无。

### apu\_dir\_enable

#### 描述

使能各个方向的延时累加计算。

#### 函数原型

```c
void apu_dir_enable(void)
```

#### 参数

无。

#### 返回值

无。

### apu\_voc\_enable

#### 描述

使能选定方向的延时累加计算。

#### 函数原型

```c
void apu_voc_enable(uint8_t enable_flag)
```

#### 参数

无。

#### 返回值

无。

### 举例

```c
uint16_t fir_prev_t[17] = {
0x8000, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, 0,
};

apu_dir_set_prev_fir(fir_prev_t);
apu_dir_set_post_fir(fir_post_t);
apu_voc_set_prev_fir(fir_prev_t);
apu_voc_set_post_fir(fir_post_t);

apu_set_delay(3, 7, 1, 44100);
apu_voc_set_direction(0);
apu_set_channel_enabled(0xff);

apu_dir_enable();
apu_voc_enable(1);
```

## 数据类型

相关数据类型、数据结构定义如下：

- apu\_reg\_t：apu任务结构体。

### apu\_reg\_t

#### 描述

kpu任务结构体。

#### 定义

```c
typedef struct _apu_reg
{
    //0x200
    apu_ch_cfg_t         bf_ch_cfg_reg;
    //0x204
    apu_ctl_t            bf_ctl_reg;
    //0x208
    apu_dir_bidx_t       bf_dir_bidx[16][2];
    //0x288
    apu_fir_coef_t       bf_pre_fir0_coef[9];
    //0x2ac
    apu_fir_coef_t       bf_post_fir0_coef[9];
    //0x2d0
    apu_fir_coef_t       bf_pre_fir1_coef[9];
    //0x2f4
    apu_fir_coef_t       bf_post_fir1_coef[9];
    //0x318
    apu_dwsz_cfg_t       bf_dwsz_cfg_reg;
    //0x31c
    apu_fft_cfg_t        bf_fft_cfg_reg;
    // 0x320
    volatile uint32_t    sobuf_dma_rdata;
    // 0x324
    volatile uint32_t    vobuf_dma_rdata;
    /*0x328*/
    apu_int_stat_t       bf_int_stat_reg;
    /*0x32c*/
    apu_int_mask_t       bf_int_mask_reg;
    /*0x330*/
    uint32_t             saturation_counter;
    /*0x334*/
    uint32_t             saturation_limits;
} __attribute__((packed, aligned(4))) apu_reg_t;
```

#### 成员

| 成员名称                | 描述                                       |
| ---------------------- | ------------------------------------------ |
|bf\_ch\_cfg\_reg          |  通道配置         |
|bf\_ctl\_reg             |  控制寄存器         |
|bf\_dir\_bidx[16][2]     |           |
|bf\_pre\_fir0\_coef[9]    |  各个方向延时累加计算前滤波系数         |
|bf\_post\_fir0\_coef[9]   |  各个方向延时累加计算后滤波系数         |
|bf\_pre\_fir1\_coef[9]    |  计算选定方向延时累加值之前滤波系数         |
|bf\_post\_fir1\_coef[9]   |  计算选定方向延时累加值之后滤波系数         |
|bf\_dwsz\_cfg\_reg        |  下采样系数         |
|bf\_fft\_cfg\_reg         |  fft控制寄存器         |
|sobuf\_dma\_rdata        |  方向数据源地址         |
|vobuf\_dma\_rdata        |  选定方向数据源地址         |
|bf\_int\_stat\_reg        |  中断状态寄存器         |
|bf\_int\_mask\_reg        |  中断选定寄存器         |
|saturation\_counter     |           |
|saturation\_limits      |           |
