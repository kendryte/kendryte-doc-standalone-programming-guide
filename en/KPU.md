# 神经网络处理器 (KPU)

## Summary

KPU 是通用的神经网络处理器，它可以在低功耗的情况下实现卷积神经网络计算，实时获取被检测目标的大小、坐标和种类，对人脸或者物体进行检测和分类。
使用kpu时，必须结合model compiler。

## Features

KPU 具备以下几个特点：

- 支持主流训练框架按照特定限制规则训练出来的定点化模型

- 对网络层数无直接限制，支持每层卷积神经网络参数单独配置，包括输入输出通道数目、输入输出行宽列高

- 支持两种卷积内核 1x1 和 3x3

- 支持任意形式的激活函数

- 实时工作时最大支持神经网络参数大小为 5.5MiB 到 5.9MiB

- 非实时工作时最大支持网络参数大小为（Flash 容量-软件体积）

## API

对应的头文件 `kpu.h`

为用户提供以下接口

- kpu\_task\_init

- kpu\_run

- kpu\_get\_output\_buf

- kpu\_release\_output\_buf

### kpu\_task\_init

#### 描述

初始化kpu任务句柄，该函数具体实现在model compiler生成的gencode_output.c中。

#### 函数定义

```c
kpu_task_t* kpu_task_init(kpu_task_t* task)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任务句柄             | 输入      |

#### 返回值

KPU任务句柄。

### kpu\_run

#### 描述

启动KPU，进行AI运算。

#### 函数原型

```c
int kpu_run(kpu_task_t* v_task, dmac_channel_number_t dma_ch, const void *src, void* dest, plic_irq_callback_t callback)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任务句柄             | 输入      |
| dma\_ch                         | DMA通道                 | 输入      |
| src                             | 输入图像数据             | 输入      |
| dest                            | 运算输出结果             | 输出      |
| callback                        | 运算完成回调函数         | 输入      |

#### 返回值

| 返回值  | 描述         |
| :----  | :------------|
| 0      | 成功         |
| 非0    | KPU忙，失败   |

### kpu\_get\_output\_buf

#### 描述

获取KPU输出结果的缓存。

#### 函数原型

```c
uint8_t *kpu_get_output_buf(kpu_task_t* task)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| task                            | KPU任务句柄             | 输入      |

#### 返回值

KPU输出结果的缓存的指针。

### kpu\_release\_output\_buf

#### 描述

释放KPU输出结果缓存。

#### 函数原型

```c
void kpu_release_output_buf(uint8_t *output_buf)
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| output\_buf                     | KPU输出结果缓存         | 输入      |

#### 返回值

无

## 数据类型

相关数据类型、数据结构定义如下：

- kpu\_task\_t：kpu任务结构体。

### kpu\_task\_t

#### 描述

kpu任务结构体。

#### 定义

```c
typedef struct
{
    kpu_layer_argument_t* layers;
    uint32_t length;
    int dma_ch;
    uint64_t* dst;
    uint32_t dst_length;
    plic_irq_callback_t cb;
} kpu_task_t;
```

#### 成员

| 成员名称                | 描述              |
| ---------------------- | ----------------- |
| layers                 | KPU参数指针        |
| length                 | 层数               |
| dma_ch                 | DMA通道            |
| dst                    | 运算结果输出指针    |
| dst_length             | 运算结果长度        |
| cb                     | 运算完成回调函数    |