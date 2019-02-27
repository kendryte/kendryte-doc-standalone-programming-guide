# DVP

## Overview

Digital Video Port (DVP) unit is a camera interface unit that supports
forwarding camera input image data to KPU or memory.

## Features

The DVP unit has the following features:

- Support RGB565, RGB422 and single channel Y gray scale input mode
- Support for setting frame interrupt
- Support setting transfer address
- Supports writing data to two addresses at the same time (output format is RGB888 and RGB565 respectively)
- Support for discarding frames that do not need to be processed

## API

Corresponding header file `dvp.h`

Provide the following interfaces

- dvp\_init

- dvp\_set\_output\_enable

- dvp\_set\_image\_format

- dvp\_set\_image\_size

- dvp\_set\_ai\_addr

- dvp\_set\_display\_addr

- dvp\_config\_interrupt

- dvp\_get\_interrupt

- dvp\_clear\_interrupt

- dvp\_start\_convert

- dvp\_enable\_burst

- dvp\_disable\_burst

- dvp\_enable\_auto

- dvp\_disable\_auto

- dvp\_sccb\_send\_data

- dvp\_sccb\_receive\_data

### dvp\_init

#### Description

Initialize DVP.

#### Function prototype

```c
void dvp_init(uint8_t reg_len)
```

#### Parameter

| Parameter name |     Description      | Input or output |
| -------------- | -------------------- | --------------- |
| reg\_len       | SCCB register length | Input           |

#### Return value

None.

### dvp\_set\_output\_enable

#### Description

Set the output mode to enable or disable.

#### Function prototype

```c
void dvp_set_output_enable(dvp_output_mode_t index, int enable)
```

#### Parameter

| Parameter name |          Description          | Input or output |
| -------------- | ----------------------------- | --------------- |
| index          | Image output to memory or KPU | Input           |
| enable         | 0: Disable 1: Enable          | Input           |

#### Return value

None.

### dvp\_set\_image\_format

#### Description

Set the image receiving mode, RGB or YUV.

#### Function prototype

```c
void dvp_set_image_format(uint32_t format)
```

#### Parameter

| Parameter name |              Description              | Input or output |
| -------------- | ------------------------------------- | --------------- |
| format         | Image format selection[^image_format] | Input           |

[^image_format]: DVP\_CFG\_RGB\_FORMAT is RGB format, DVP\_CFG\_YUV\_FORMAT is YUV format.

#### Return value

None.

### dvp\_set\_image\_size

#### Description

Set the DVP image capture size.

#### Function prototype

```c
void dvp_set_image_size(uint32_t width, uint32_t height)
```

#### Parameter

| Parameter name | Description  | Input or output |
| -------------- | ------------ | --------------- |
| width          | Image width  | Input           |
| height         | Image height | Input           |

#### Return value

None.

### dvp\_set\_ai\_addr

#### Description

Set the image address required by the KPU,
in order to facilitate the KPU to perform algorithm processing.

#### Function prototype

```c
void dvp_set_ai_addr(uint32_t r_addr, uint32_t g_addr, uint32_t b_addr)
```

#### Parameter

| Parameter name |       Description       | Input or output |
| -------------- | ----------------------- | --------------- |
| r\_addr        | Red component address   | Input           |
| g\_addr        | Green component address | Input           |
| b\_addr        | Blue component address  | Input           |

#### Return value

None.

### dvp\_set\_display\_addr

#### Description

Set the storage address of the captured image in the memory, which can be used for display.

#### Function prototype

```c
void dvp_set_display_addr(uint32_t addr)
```

#### Parameter

| Parameter name |          Description           | Input or output |
| -------------- | ------------------------------ | --------------- |
| addr           | Memory address to store images | Input           |

#### Return value

None.

### dvp\_config\_interrupt

Configure the DVP interrupt type.

#### Function prototype

```c
void dvp_config_interrupt(uint32_t interrupt, uint8_t enable)
```

#### Description

Set image capture start and end interrupt status, enable or disable.

#### Parameter

| Parameter name |               Description               | Input or output |
| -------------- | --------------------------------------- | --------------- |
| interrupt      | DVP interrupt type[^dvp_interrupt_type] | Input           |
| enable         | 0: Disable 1: Enable                    | Input           |

[^dvp_interrupt_type]: DVP\_CFG\_START\_INT\_ENABLE for the interrupt of image
capture begin; DVP\_CFG\_FINISH\_INT\_ENABLE for the interrupt of image capture end.

#### Return value

None.

### dvp\_get\_interrupt

#### Description

Determine if it is the specified interrupt type.

#### Function prototype

```c
int dvp_get_interrupt(uint32_t interrupt)
```

#### Parameter

| Parameter name |               Description               | Input or output |
| -------------- | --------------------------------------- | --------------- |
| interrupt      | DVP interrupt type[^dvp_interrupt_type] | Input           |

#### Return value

| Return value | Description |
| :----------- | :---------- |
| 0            | False       |
| Others       | True        |

### dvp\_clear\_interrupt

#### Description

Clear the interrupt.

#### Function prototype

```c
void dvp_clear_interrupt(uint32_t interrupt)
```

#### Parameter

| Parameter name |               Description               | Input or output |
| -------------- | --------------------------------------- | --------------- |
| interrupt      | DVP interrupt type[^dvp_interrupt_type] | Input           |

#### Return value

None.

### dvp\_start\_convert

#### Description

Start capturing images and call them after determining that the image capture begins.

#### Function prototype

```c
void dvp_start_convert(void)
```

#### Parameter

None.

#### Return value

None.

### dvp\_enable\_burst

#### Description

Enable burst transfer mode.

#### Function prototype

```c
void dvp_enable_burst(void)
```

#### Parameter

None.

#### Return value

None.

### dvp\_disable\_burst

#### Description

Disable burst transfer mode.

#### Function prototype

```c
void dvp_disable_burst(void)
```

#### Parameter

None.

#### Return value

None.

### dvp\_enable\_auto

#### Description

Enable automatic image mode reception.s

#### Function prototype

```c
void dvp_enable_auto(void)
```

#### Parameter

None.

#### Return value

None.

### dvp\_disable\_auto

#### Description

Disable automatic image reception mode.

#### Function prototype

```c
void dvp_disable_auto(void)
```

#### Parameter

None.

#### Return value

None.

### dvp\_sccb\_send\_data

#### Description

Send data via scbb.

#### Function prototype

```c
void dvp_sccb_send_data(uint8_t dev_addr, uint16_t reg_addr, uint8_t reg_data)
```

#### Parameter

| Parameter name |        Description        | Input or output |
| -------------- | ------------------------- | --------------- |
| dev\_addr      | Image sensor SCCB address | Input           |
| reg\_addr      | Image sensor register     | Input           |
| reg\_data      | Sent data                 | Input           |

#### Return value

None.

### dvp\_sccb\_receive\_data

#### Description

Receive data through the SCCB.

#### Function prototype

```c
uint8_t dvp_sccb_receive_data(uint8_t dev_addr, uint16_t reg_addr)
```

#### Parameter

| Parameter name |        Description        | Input or output |
| -------------- | ------------------------- | --------------- |
| dev\_addr      | Image sensor SCCB address | Input           |
| reg\_addr      | Image sensor register     | Input           |

#### Return value

Read the data of the register.

### Example

```c
/*
 * Capture 320 * 240 RGB image data transfer to lcd_gram0,
 * and 0x40600000 0x40612C00 0x40625800 address
 */
uint32_t lcd_gram0[38400] __attribute__((aligned(64)));

int on_irq_dvp(void* ctx)
{
    if (dvp_get_interrupt(DVP_STS_FRAME_FINISH))
    {
        dvp_clear_interrupt(DVP_STS_FRAME_FINISH);
    }
    else
    {
        dvp_start_convert();
        dvp_clear_interrupt(DVP_STS_FRAME_START);
    }
    return 0;
}
plic_init();
dvp_init(8);
dvp_enable_burst();
dvp_set_output_enable(DVP_OUTPUT_AI, 1);
dvp_set_output_enable(DVP_OUTPUT_DISPLAY, 1);
dvp_set_image_format(DVP_CFG_RGB_FORMAT);
dvp_set_image_size(320, 240);
dvp_set_ai_addr((uint32_t)0x40600000, (uint32_t)0x40612C00, (uint32_t)0x40625800);
dvp_set_display_addr(lcd_gram0);
dvp_config_interrupt(DVP_CFG_START_INT_ENABLE | DVP_CFG_FINISH_INT_ENABLE, 0);
dvp_disable_auto();
plic_set_priority(IRQN_DVP_INTERRUPT, 1);
plic_irq_register(IRQN_DVP_INTERRUPT, on_irq_dvp, NULL);
plic_irq_enable(IRQN_DVP_INTERRUPT);
| dvp_clear_interrupt(DVP_STS_FRAME_START       | DVP_STS_FRAME_FINISH);         |
| dvp_config_interrupt(DVP_CFG_START_INT_ENABLE | DVP_CFG_FINISH_INT_ENABLE, 1); |
sysctl_enable_irq();
/*
 * Send 0x01 to the peripheral 0xFF register of address 0x60 through SCCB,
 * read data from register 0x1D.
 */
dvp_sccb_send_data(0x60, 0xFF, 0x01);
dvp_sccb_receive_data(0x60, 0x1D)
```

## Data type

The relevant data types and data structures are defined as follows:

- dvp\_output\_mode\_t: DVP output image mode.

### dvp\_output\_mode\_t

#### Description

DVP output image mode.

#### Type definition

```c
typedef enum _dvp_output_mode
{
    DVP_OUTPUT_AI,
    DVP_OUTPUT_DISPLAY,
} dvp_output_mode_t;
```

#### Enumeration element

|     Element name     |         Description          |
| -------------------- | ---------------------------- |
| DVP\_OUTPUT\_AI      | Output to KPU                |
| DVP\_OUTPUT\_DISPLAY | Output to memory for display |