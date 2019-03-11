# 看門狗定時器 (WDT)

## 概述

WDT 提供系統出錯或無響應時的恢復功能。

## 功能描述

WDT 模組具有以下功能：

- 配置超時時間

- 手動重啟計時

## API 參考

對應的頭文件 `wdt.h`

為用戶提供以下介面

- wdt\_init

- wdt\_start(0.6.0後不再支持，請使用wdt\_init)

- wdt\_stop

- wdt\_feed

- wdt\_clear\_interrupt

### wdt\_init

#### 描述

配置參數，啟動看門狗。不使用中斷的話，將on_irq設置為NULL。

#### 函數原型

```c
uint32_t wdt_init(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq, void *ctx)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------  | --------- |
| id              | 看門狗編號        | 輸入       |
| time\_out\_ms   | 超時時間（毫秒）   | 輸入      |
| on\_irq         | 中斷回調函數      | 輸入       |
| ctx             | 回調函數參數      | 輸入       |

#### 返回值

看門狗超時重啟的實際時間（毫秒）。與time\_out\_ms有差異，一般情況會大於這個時間。在外部晶振26M的情況下，最大超時時間為330毫秒。

### wdt\_start

#### 描述

啟動看門狗。

#### 函數原型

```c
void wdt_start(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------  | --------- |
| id              | 看門狗編號        | 輸入       |
| time\_out\_ms   | 超時時間（毫秒）   | 輸入      |
| on\_irq          | 中斷回調函數     | 輸入       |

#### 返回值

無

### wdt\_stop

#### 描述

關閉看門狗。

#### 函數原型

```c
void wdt_stop(wdt_device_number_t id)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------  | --------- |
| id              | 看門狗編號        | 輸入       |

#### 返回值

無。

### wdt\_feed

#### 描述

喂狗。

#### 函數原型

```c
void wdt_feed(wdt_device_number_t id)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------  | --------- |
| id              | 看門狗編號        | 輸入       |

#### 返回值

無。

### wdt\_clear\_interrupt

#### 描述

清除中斷。如果在中斷函數中清除中斷，則看門狗不會重啟。

#### 函數原型

```c
void wdt_clear_interrupt(wdt_device_number_t id)
```

#### 參數

| 參數名稱         |   描述           |  輸入輸出  |
| --------------- | ---------------  | --------- |
| id              | 看門狗編號        | 輸入       |

#### 返回值

無。

### 舉例

```c
/* 2秒後進入看門狗中斷函數列印Hello_world，再過2s複位 */
int wdt0_irq(void *ctx)
{
    printf("Hello_world\n");
    return 0;
}
plic_init();
sysctl_enable_irq();
wdt_init(WDT_DEVICE_0, 2000, wdt0_irq, NULL);
```

## 資料類型

相關資料類型、資料結構定義如下：

- wdt\_device\_number\_t

### wdt\_device\_number\_t

#### 描述

看門狗編號。

#### 定義

```c
typedef enum _wdt_device_number
{
    WDT_DEVICE_0,
    WDT_DEVICE_1,
    WDT_DEVICE_MAX,
} wdt_device_number_t;
```

#### 成員

| 成員名稱         | 描述         |
| --------------- | ------------ |
| WDT\_DEVICE\_0  | 看門狗 0      |
| WDT\_DEVICE\_1  | 看門狗 1      |