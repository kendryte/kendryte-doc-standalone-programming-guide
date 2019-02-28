# WDT

## Overview

A watchdog timer (WDT) is a hardware timer that automatically generates a system reset if the main program neglects to periodically service it.

## Features

The WDT module has the following features:

- Configure timeout
- Manually set the restart time
- Configure to reset or enter interrupt after timeout
- Clear the interrupt after entering the interrupt to cancel the reset, otherwise wait for the second timeout after reset

## API

Corresponding header file `wdt.h`

Provide the following interfaces

- wdt\_start

- wdt\_stop

- wdt\_feed

- wdt\_clear\_interrupt

### wdt\_start

#### Description

Start the watchdog.

#### Function prototype

```c
void wdt_start(wdt_device_number_t id, uint64_t time_out_ms, plic_irq_callback_t on_irq)
```

#### Parameter

| Parameter name |         Description         | Input or output |
| -------------- | --------------------------- | --------------- |
| id             | Watchdog number             | Input           |
| time\_out\_ms  | Timeout (ms)                | Input           |
| on\_irq        | Interrupt callback function | Input           |

#### Return value

None.

### wdt\_stop

#### Description

Stop the watchdog.

#### Function prototype

```c
void wdt_stop(wdt_device_number_t id)
```

#### Parameter

| Parameter name |   Description   | Input or output |
| -------------- | --------------- | --------------- |
| id             | Watchdog number | Input           |

#### Return value

None.

### wdt\_feed

#### Description

Feed the watchdog (clear the counter of watchdog).

#### Function prototype

```c
void wdt_feed(wdt_device_number_t id)
```

#### Parameter

| Parameter name |   Description   | Input or output |
| -------------- | --------------- | --------------- |
| id             | Watchdog number | Input           |

#### Return value

None.

### wdt\_clear\_interrupt

#### Description

Clear the interrupt. If the interrupt is cleared in the interrupt function, the watchdog will not restart.

#### Function prototype

```c
void wdt_clear_interrupt(wdt_device_number_t id)
```

#### Parameter

| Parameter name |   Description   | Input or output |
| -------------- | --------------- | --------------- |
| id             | Watchdog number | Input           |

#### Return value

None.

### Example

```c
/*
 * After 2 seconds, enter the watchdog interrupt function to print Hello_world,
 * and then reset after 2 seconds.
 */
int wdt0_irq(void)
{
    printf("Hello_world\n");
    return 0;
}
plic_init();
sysctl_enable_irq();
wdt_start(WDT_DEVICE_0, 2000, wdt0_irq);
```

## Data type

The relevant data types and data structures are defined as follows:

- wdt\_device\_number\_t

### wdt\_device\_number\_t

#### Description

Watchdog number。

#### Type definition

```c
typedef enum _wdt_device_number
{
    WDT_DEVICE_0,
    WDT_DEVICE_1,
    WDT_DEVICE_MAX,
} wdt_device_number_t;
```

#### Enumeration element

|  Element name  | Description |
| -------------- | ----------- |
| WDT\_DEVICE\_0 | Watchdog 0    |
| WDT\_DEVICE\_1 | Watchdog 1    |
