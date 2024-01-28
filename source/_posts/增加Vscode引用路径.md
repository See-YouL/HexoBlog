---
title: 增加Vscode引用路径
date: 2024-01-27 22:02:55
tags: Vscode
---

## 问题说明

在嵌入式开发中需要经常用到库函数(SPL), Vscode需要配置引用路径才能对函数名或变量进行跳转

## 解决思路1

与Keil5 MDK类似, 在配置C/C++的json文件中添加所使用的头文件路径

### 在Vscode中进行配置

在vscode中按Ctrl+Shift+P 输入configuration, 如图选择C/C++编程配置(json)

![Vscode配置](https://raw.githubusercontent.com/See-YouL/MarkdownPhotos/main/202401272209160.png)

在"includePath"后面增加所要使用的头文件的路径, 如下图所示

![Vscode配置](https://raw.githubusercontent.com/See-YouL/MarkdownPhotos/main/202401272342499.png)

### 缺点

配置起来较为繁琐, 且部分函数依然无法跳转

## 解决思路2

在思路1的基础上, 向编写的文件中包含"stm32f10x_conf.h文件"

```c
#include "stm32f10x_conf.h"
```

在stm32f10x_conf文件中有对于所有外设头文件的包含

```c
/* Includes ------------------------------------------------------------------*/
/* Uncomment/Comment the line below to enable/disable peripheral header file inclusion */
#include "stm32f10x_adc.h"
#include "stm32f10x_bkp.h"
#include "stm32f10x_can.h"
#include "stm32f10x_cec.h"
#include "stm32f10x_crc.h"
#include "stm32f10x_dac.h"
#include "stm32f10x_dbgmcu.h"
#include "stm32f10x_dma.h"
#include "stm32f10x_exti.h"
#include "stm32f10x_flash.h"
#include "stm32f10x_fsmc.h"
#include "stm32f10x_gpio.h"
#include "stm32f10x_i2c.h"
#include "stm32f10x_iwdg.h"
#include "stm32f10x_pwr.h"
#include "stm32f10x_rcc.h"
#include "stm32f10x_rtc.h"
#include "stm32f10x_sdio.h"
#include "stm32f10x_spi.h"
#include "stm32f10x_tim.h"
#include "stm32f10x_usart.h"
#include "stm32f10x_wwdg.h"
#include "misc.h" /* High level functions for NVIC and SysTick (add-on to CMSIS functions) */
```

所以在思路1的基础上加上思路2可以较好的解决该问题

