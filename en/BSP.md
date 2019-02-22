# 平台相关（BSP）

## Summary

平台相关的通用函数。

## Features

提供获取当前运行程序的CPU核编号的接口以及启动第二个核的入口。

## API

Corresponding header file `bsp.h`

Provide the following interfaces

- register\_core1

- current\_coreid

### register\_core1

#### Description

向1核注册函数，并启动1核。

#### Function prototype

```c
int register_core1(core_function func, void *ctx)
```

#### Parameter

| Parameter name                         |   Description                   |  Input or output  |
| ------------------------------- | ------------------------ | --------- |
| func                            | 向1核注册的函数           | Input       |
| ctx                             | 函数的参数，没有设置为NULL | Input       |

#### Return value

| Return value  | Description   |
| :----  | :------ |
| 0      | 成功    |
| 非0    | 失败    |

### current\_coreid

#### Description

获取当前CPU核编号。

#### Function prototype

```c
#define current_coreid()       read_csr(mhartid)
```

#### Parameter

None.

#### Return value

当前所在CPU核的编号。

### Example

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

## Data type

The relevant data types and data structures are defined as follows:

- core\_function：CPU核调用的函数。

### core\_function

#### Description

CPU核调用的函数。

#### Type definition

```c
typedef int (*core_function)(void *ctx);
```