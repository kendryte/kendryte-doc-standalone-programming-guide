# 平台相关（BSP）

## 概述

平台相关的通用函数，核之间锁的相关操作。

## 功能描述

提供获取当前运行程序的CPU核编号的接口以及启动第二个核的入口。

## API 参考

对应的头文件 `bsp.h`

为用户提供以下接口

- register\_core1

- current\_coreid

- read\_cycle

- corelock\_lock

- corelock\_trylock

- corelock\_unlock

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

#### read\_cycle

#### 描述

获取CPU开机至今的时钟数。可以用使用这个函数精准的确定程序运行时钟。可以配合sysctl_clock_get_freq(SYSCTL_CLOCK_CPU)计算运行的时间。

#### 函数原型

```c
#define read_cycle()        read_csr(mcycle)
```

#### 参数

无。

#### 返回值

开机至今的CPU时钟数。

### corelock\_lock

#### 描述

获取核间锁，核之间互斥的锁，同核内该锁会嵌套，只有异核之间会阻塞。不建议在中断使用该函数，中断中可以使用corelock_trylock。

#### 函数原型

```c
void corelock_lock(corelock_t *lock)
```

#### 参数

核间锁，要使用全局变量，参见举例。

#### 返回值

无。

### corelock\_trylock

#### 描述

获取核间锁，同核时锁会嵌套，异核时非阻塞。成功获取锁会返回0，失败返回-1。

#### 函数原型

```c
corelock_trylock(corelock_t *lock)
```

#### 参数

核间锁，要使用全局变量，参见举例。

#### 返回值

无。

### corelock\_unlock

#### 描述

核间锁解锁。

#### 函数原型

```c
void corelock_unlock(corelock_t *lock)
```

#### 参数

核间锁，要使用全局变量，参见举例。

#### 返回值

无。

### 举例

```c
/* 1核在0核第二次释放锁的时候才会获取到锁，通过读cycle计算时间 */
#include <stdio.h>
#include "bsp.h"
#include <unistd.h>
#include "sysctl.h"

corelock_t lock;

uint64_t get_time(void)
{
    uint64_t v_cycle = read_cycle();
    return v_cycle * 1000000 / sysctl_clock_get_freq(SYSCTL_CLOCK_CPU);
}

int core1_function(void *ctx)
{
    uint64_t core = current_coreid();
    printf("Core %ld Hello world\n", core);
    while(1)
    {
        uint64_t start = get_time();
        corelock_lock(&lock);
        printf("Core %ld Hello world\n", core);
        sleep(1);
        corelock_unlock(&lock);
        uint64_t stop = get_time();
        printf("Core %ld lock time is %ld us\n",core, stop - start);
        usleep(10);
    }
}

int main(void)
{
    uint64_t core = current_coreid();
    printf("Core %ld Hello world\n", core);
    register_core1(core1_function, NULL);
    while(1)
    {
        corelock_lock(&lock);
        sleep(1);
        printf("1> Core %ld sleep 1\n", core);
        corelock_lock(&lock);
        sleep(2);
        printf("2> Core %ld sleep 2\n", core);
        printf("2> Core unlock\n");
        corelock_unlock(&lock);
        sleep(1);
        printf("1> Core unlock\n");
        corelock_unlock(&lock);
        usleep(10);
    }
}
```

## 数据类型

相关数据类型、数据结构定义如下：

- core\_function：CPU核调用的函数。

- spinlock\_t：自旋锁。

- corelock\_t：核间锁。

### core\_function

#### 描述

CPU核调用的函数。

#### 定义

```c
typedef int (*core_function)(void *ctx);
```

### spinlock\_t

自旋锁。

#### 定义

```c
typedef struct _spinlock
{
    int lock;
} spinlock_t;
```

### corelock\_t

核间锁。

#### 定义

```c
typedef struct _corelock
{
    spinlock_t lock;
    int count;
    int core;
} corelock_t;
```