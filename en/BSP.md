# 平台相关（BSP）

## 概述

平台相关的通用函数。

## 功能描述

提供获取当前运行程序的CPU核编号的接口以及启动第二个核的入口。

## API 参考

对应的头文件 `bsp.h`

为用户提供以下接口

- register\_core1

- current\_coreid

### register\_core1

#### 描述

向1核注册函数，并启动1核。

#### 函数原型

```c
int register_core1(core_function func, void *ctx)
```

#### 参数

| 参数名称                         |   描述                   |  输入输出  |
| ------------------------------- | ------------------------ | --------- |
| func                            | 向1核注册的函数           | 输入       |
| ctx                             | 函数的参数，没有设置为NULL | 输入       |

#### 返回值

| 返回值  | 描述   |
| :----  | :------ |
| 0      | 成功    |
| 非0    | 失败    |

### current\_coreid

#### 描述

获取当前CPU核编号。

#### 函数原型

```c
#define current_coreid()       read_csr(mhartid)
```

#### 参数

无。

#### 返回值

当前所在CPU核的编号。

### 举例

```c
/* 0核获取CPU核编号打印Hello world，然后启动1核获取CPU核编号打印Hello world */
#include <stdio.h>
#include "bsp.h"

int core1_function(void *ctx)
{
    uint64_t core = current_coreid();
    printf("Core %ld Hello world\n", core);
    while(1);
}

int main()
{
    uint64_t core = current_coreid();
    printf("Core %ld Hello world\n", core);
    register_core1(core1_function, NULL);
    while(1);
}
```

## 数据类型

相关数据类型、数据结构定义如下：

- core\_function：CPU核调用的函数。

### core\_function

#### 描述

CPU核调用的函数。

#### 定义

```c
typedef int (*core_function)(void *ctx);
```