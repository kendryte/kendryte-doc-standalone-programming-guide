# 平臺相關（BSP）

## 概述

平臺相關的通用函數，核之間鎖的相關操作。

## 功能描述

提供獲取當前運行程序的CPU核編號的介面以及啟動第二個核的入口。

## API 參考

對應的頭文件 `bsp.h`

為用戶提供以下介面

- register\_core1

- current\_coreid

- read\_cycle

- corelock\_lock

- corelock\_trylock

- corelock\_unlock

### register\_core1

#### 描述

向1核註冊函數，並啟動1核。

#### 函數原型

```c
int register_core1(core_function func, void *ctx)
```

#### 參數

| 參數名稱                         |   描述                   |  輸入輸出  |
| ------------------------------- | ------------------------ | --------- |
| func                            | 向1核註冊的函數           | 輸入       |
| ctx                             | 函數的參數，沒有設置為NULL | 輸入       |

#### 返回值

| 返回值  | 描述   |
| :----  | :------ |
| 0      | 成功    |
| 非0    | 失敗    |

### current\_coreid

#### 描述

獲取當前CPU核編號。

#### 函數原型

```c
#define current_coreid()       read_csr(mhartid)
```

#### 參數

無。

#### 返回值

當前所在CPU核的編號。

#### read\_cycle

#### 描述

獲取CPU開機至今的時脈數。可以用使用這個函數精準的確定程序運行時脈。可以配合sysctl\_clock\_get\_freq(SYSCTL\_CLOCK\_CPU)計算運行的時間。

#### 函數原型

```c
#define read_cycle()        read_csr(mcycle)
```

#### 參數

無。

#### 返回值

開機至今的CPU時脈數。

### corelock\_lock

#### 描述

獲取核間鎖，核之間互斥的鎖，同核內該鎖會嵌套，只有異核之間會阻塞。不建議在中斷使用該函數，中斷中可以使用corelock\_trylock。

#### 函數原型

```c
void corelock_lock(corelock_t *lock)
```

#### 參數

核間鎖，要使用全局變數，參見舉例。

#### 返回值

無。

### corelock\_trylock

#### 描述

獲取核間鎖，同核時鎖會嵌套，異核時非阻塞。成功獲取鎖會返回0，失敗返回-1。

#### 函數原型

```c
corelock_trylock(corelock_t *lock)
```

#### 參數

核間鎖，要使用全局變數，參見舉例。

#### 返回值

無。

### corelock\_unlock

#### 描述

核間鎖解鎖。

#### 函數原型

```c
void corelock_unlock(corelock_t *lock)
```

#### 參數

核間鎖，要使用全局變數，參見舉例。

#### 返回值

無。

### 舉例

```c
/* 1核在0核第二次釋放鎖的時候才會獲取到鎖，通過讀cycle計算時間 */
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

## 資料類型

相關資料類型、資料結構定義如下：

- core\_function：CPU核調用的函數。

- spinlock\_t：自旋鎖。

- corelock\_t：核間鎖。

### core\_function

#### 描述

CPU核調用的函數。

#### 定義

```c
typedef int (*core_function)(void *ctx);
```

### spinlock\_t

自旋鎖。

#### 定義

```c
typedef struct _spinlock
{
    int lock;
} spinlock_t;
```

### corelock\_t

核間鎖。

#### 定義

```c
typedef struct _corelock
{
    spinlock_t lock;
    int count;
    int core;
} corelock_t;
```