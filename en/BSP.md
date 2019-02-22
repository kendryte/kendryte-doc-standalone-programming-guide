# Architecture support package（BSP）

## Summary

Architecture level support function of k210 SoC.

## Features

Provides an interface to get the CPU core ID of the currently running program
and an entry to start the second core.

## API

Corresponding header file `bsp.h`

Provide the following interfaces

- register\_core1

- current\_coreid

### register\_core1

#### Description

Register the function with core 1 and start core 1.

#### Function prototype

```c
int register_core1(core_function func, void *ctx)
```

#### Parameter

| Parameter name                         |   Description                   |  Input or output  |
| ------------------------------- | ------------------------ | --------- |
| func                            | Function registered to core 1           | Input       |
| ctx                             | The parameter of the function, set to NULL means not used | Input       |

#### Return value

| Return value  | Description   |
| :----  | :------ |
| 0      | Success    |
| Other    | Fail    |

### current\_coreid

#### Description

Get the current CPU core ID.

#### Function prototype

```c
#define current_coreid()       read_csr(mhartid)
```

#### Parameter

None.

#### Return value

The ID of the current CPU core.

### Example

```c
/* Core 0 gets the CPU core ID and prints Hello world, then starts core 1 to get the CPU core ID and prints Hello world */
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

- core\_function：The function called by the CPU core.

### core\_function

#### Description

The function called by the CPU core.

#### Type definition

```c
typedef int (*core_function)(void *ctx);
```
