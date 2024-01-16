---
title: ARM嵌入式复习笔记
date: 2023-05-29 11:37:03
tags: 嵌入式
---


## 填空

### 嵌入式系统概念填空

1. 嵌入式系统是以**应用系统**为中心，以**计算机为基础**，**软硬件可裁剪**，~~适应应用系统对功能、可靠性、成本、体积、功耗严格要求~~的**专用**计算机系统。
2. ARM处理器是ARM公司设计的基于RISC架构的**32位**高性能微处理器，一般采用**哈佛**总线结构，具有高速指令缓存和数据缓存，指令长度固定且多级流水线执行。

### 工作频率填空

1. Cortex-M3内核CPU通过总线阵列和高性能总线（AHB）以及AHB-APB总线桥与两类APB总线相连接，即APB1总线和APB2总线，**APB1总线的最高工作频率为36MHz。**
2. Cortex-M3内核CPU通过总线阵列和高性能总线（AHB）以及AHB-APB总线桥与两类APB总线相连接，即APB1总线和APB2总线，**APB2总线的最高工作频率为72MHz。**
3. Cortex-M3**内核的最高工作时钟频率为72MHz。**

### 时钟填空

1. 32F103的系统时钟SYSCLK可以来自**HSI（内部高速时钟）、HSE（外部高速时钟）和PLL（锁相环）**三个时钟源中的一个。
2. 当STM32F103外接8MHz的晶体时，若使内核达到最高工作时钟频率，PLL的倍频系数应设置为9倍。
3. STM32F103外接的**32768Hz晶体主要用来为芯片内部的RTC部件提供时钟源。**

PLL倍频系数的设置

```tex
计算步骤如下：
系统时钟SYSCLK = (输入时钟频率) × (PLL倍频系数)
72 MHz = 8 MHz × 9
因此，PLL的倍频系数应设置为9倍
```

### 存储器填空

1. STM32F103芯片是**32位**的微控制器，**可寻址存储空间的大小为4GB。**
2. STM32F103芯片可寻址存储空间的大小为 4GB，分为 8个512MB的存储块。
3. 当BOOT0 = 0时，STM32F103上电后，用户程序将从Flash存储器启动。

### GPIO填空

1. STM32F103ZET6芯片包含**7 个16位**的通用目的输入/输出口（GPIO）。。
2. STM32F103ZET6芯片共有**112根GPIO引脚**，可从其中**任选16根**作为外部中断输入口。

### 中断填空

1. STM32F103微控制器具有**10个异常和60个中断**，**中断优先级为16 级**。
2. STM32F103微控制器的EXTI模块有**16个连接GPIO的外部中断线**，对应**16个外部中断向量**。
3. STM32F103微控制器共**有3个串口**，其中**USART1的工作时钟源来自于APB2总线** 。
4. STM32F103微控制器共有**3个串口**，其中**USART2的工作时钟源来自于APB1总线** 。

### ADC填空

1. STM32F103微控制器的ADC模块**支持单次和连续转换模式**。
2. STM32F103微控制器的ADC模块**分辨率为12位**，**最小转换时间为1.17微妙**
3. STM32F103的ADC1有16个外部模拟输入通道，**分辨率为12 位。**
4. STM32F103的ADC的**分辨率为12位**，**最高转换速率是1MHz**

### 操作系统填空

1. 嵌入式操作系统根据各个任务的要求，进行内存管理、多任务管理、资源管理、任务调度、消息管理和异常处理等工作。
2. uC/OS-II操作系统是一个**源代码公开、可移植、可固化、可裁剪、可配置式**的实时多任务操作系统，**最多可支持255个任务**。
3. 在uC/OS-II操作系统中，通过**互斥信号量**可实现对共享资源的**抢占式访问**。

## 简答

### 嵌入式系统概念简答

#### 从技术角度来说什么是嵌入式系统？8051单片机应用系统是否属于嵌入式系统？

1. 嵌入式系统是**以应用系统为中心**，**以计算机为基础**，**软硬件可裁剪**，~~适应应用系统对功能、可靠性、成本、体积、功耗严格要求~~的**专用计算机系统**
2. 8051单片机应用系统**可以**被归类为嵌入式系统。

#### 嵌入式实时操作系统中的“实时性”指的是什么？

1. 实时性是**系统对外部事件的及时响应和任务的及时完成能力。** *实时性可以分为硬实时和软实时两种类型。*
2. 硬实时要求系统在严格的时间约束下，对外部事件作出及时的响应。**任务的截止时间是固定的，任何超出时间限制的情况都可能导致系统功能失效或系统崩溃。**
3. 软实时要求系统尽可能在特定的时间约束下，对外部事件作出及时的响应，但允许偶尔的违反时间限制。**任务的截止时间相对宽松，系统可以容忍一定程度的任务响应时间超出。**

### 时钟简答

#### STM32F103微控制器的工作时钟源有哪几种？各时钟源的频率范围分别是多少？

1. **HSI（High-Speed Internal）高速内部时钟**：频率为8MHz。
2. **HSE（High-Speed External）高速外部时钟**：频率范围通常为4MHz至16MHz。
3. **PLL（Phase-Locked Loop）锁相环时钟**：可以使用HSI或HSE作为输入时钟源，并通过倍频系数进行倍频。具体的频率范围取决于倍频系数的设置。

#### 在STM32F103内部的时钟树中，锁相环PLL有什么用途？

1. **时钟倍频**：PLL可以将输入时钟频率倍增，提供更高的系统时钟频率。
2. **稳定时钟源**：PLL可以提供更稳定的时钟源，减小时钟的抖动和波动。
3. **系统时钟源**：在STM32F103中，PLL经常被配置为系统时钟源（SYSCLK），即整个微控制器系统的主要时钟源。

#### 嵌入式系统中的启动代码（startup_stm32f10x_hd.s）程序的功能是什么？

1. **初始化向量表**：启动代码会定义和初始化微控制器的向量表，其中包含了中断处理函数的入口地址。向量表的初始化是确保中断处理能够正确触发和执行的重要步骤。
2. **初始化堆栈和堆栈指针**：启动代码会设置初始堆栈指针，指向程序的堆栈空间。这是确保函数调用和中断处理正常工作的必要步骤。
3. **初始化系统时钟**：启动代码会进行系统时钟的初始化，包括配置时钟源、设置时钟分频器等操作，以确保系统在正确的时钟频率下运行。
4. **初始化存储器和外设**：启动代码可能包括对存储器和外设的初始化操作，例如设置存储器映射、配置外设寄存器等。
5. **调用主函数**：启动代码最终会调用应用程序的主函数（如`main`函数），使应用程序正式开始执行。

#### STM32F103微控制器的最小系统由哪几部分构成？

1. **STM32F103微控制器芯片**：这是系统的核心部分，包含了CPU、存储器、外设等功能模块。
2. **时钟源**：最小系统需要提供适当的时钟源，以驱动微控制器的各个部分。常见的时钟源包括晶体振荡器、外部时钟源或者内部时钟源。
3. **复位电路**：复位电路用于在系统上电或者复位时将微控制器置于初始状态。它通常由复位按钮、电容和电阻等组成。
4. **电源管理电路**：为STM32F103微控制器提供稳定的电源供应，并对电源进行滤波和保护。这包括电源连接器、电源滤波电容、稳压器等。
5. **外部连接器**：用于与外部设备或外部电路进行连接，包括通信接口（如UART、SPI、I2C）、GPIO引脚、ADC输入等。

#### STM32F103微控制器有哪几种启动模式？如何来配置系统启动模式？

1. **主启动模式（Main Boot Mode）**：在主启动模式下，微控制器从FLASH存储器的起始地址处开始执行代码。
2. **系统存储器模式（System Memory Boot Mode）**：在系统存储器模式下，微控制器从内部的系统存储器（一般为ROM或者Flash）的起始地址处开始执行代码。
3. **内存模式（RAM Boot Mode）**：在内存模式下，微控制器从系统RAM中的特定地址处开始执行代码。

系统启动模式的配置是通过BOOT pins（BOOT0和BOOT1）的状态来实现的。这些引脚通常通过跳线帽或者外部电平转换器与微控制器连接。

具体的配置方式如下：

- 如果BOOT0引脚为高电平，那么微控制器将进入内存模式。
- 如果BOOT0引脚为低电平（接地），那么微控制器将根据BOOT1引脚的状态来选择启动模式。
  - 如果BOOT1引脚也为低电平，那么微控制器将进入主启动模式。
  - 如果BOOT1引脚为高电平，那么微控制器将进入系统存储器模式。

### 存储器简答

#### 什么是存储器重映射？STM32F103微控制器的哪些存储区域需要进行存储器重映射？

存储器重映射**是指将某些存储器区域的物理地址重新映射到不同的逻辑地址的过程。**

在STM32F103微控制器中，存储器重映射主要涉及以下两个存储区域：

1. **系统存储器（System Memory）**：系统存储器包含了微控制器的启动代码和ROM固件库。在存储器重映射时，系统存储器的物理地址将被映射到内部的ROM或者Flash存储器的起始地址，使得系统可以从内部存储器中执行代码。

2. **外部SRAM（External SRAM）**：STM32F103微控制器具有一些器件型号支持外部SRAM的扩展。在存储器重映射时，外部SRAM的物理地址可以被映射到微控制器的内部存储器的地址空间中，使得外部SRAM可以像内部存储器一样被访问和使用。

### 中断简答

#### STM32F103微控制器的异常和中断有什么区别？优先级最高的是哪个异常/中断？

在STM32F103微控制器中，异常和中断是两种不同的事件处理机制，它们有以下区别：

1. **异常（Exception）**：异常是指**由于指令执行或系统事件引起的处理器中断。它们通常表示了一些严重的错误或特殊情况，需要立即处理。**~~异常包括复位、非屏蔽中断（如硬件故障）、系统调试异常等。异常的处理优先级高于中断。~~

2. **中断（Interrupt）**：中断是指**外部设备或特定事件触发的处理器中断。它们通常表示了一些需要优先处理的异步事件**，如外部输入信号、定时器溢出等。中断可以根据优先级配置，并**可被屏蔽或使能。**

在STM32F103微控制器中，优先级最高的异常是**复位（Reset）**异常。复位异常在系统上电或者复位时触发，用于将系统重置到初始状态。它的优先级最高，无法被屏蔽。

### GPIO简答

#### STM32F103微控制器的GPIO有哪几种工作模式？GPIO作按键输入时应选择哪种工作模式？

1. **输入模式（Input Mode）**：将GPIO配置为输入模式，用于读取外部信号或按键的状态。可以选择不同的输入模式，如**浮空输入、上拉输入和下拉输入**，以适应不同的电路连接方式。
2. **输出模式（Output Mode）**：将GPIO配置为输出模式，用于控制外部设备或驱动器。输出模式可以选择**推挽输出、开漏输出、推挽输出带上拉或下拉等**。
3. **复用功能模式（Alternate Function Mode）**：将GPIO配置为复用功能模式，可以使用GPIO引脚来实现其他外设功能，如串口、定时器、SPI等。
4. **模拟模式（Analog Mode）**：将GPIO配置为模拟模式，用于连接模拟信号输入或输出。

当GPIO用作按键输入时，应选择**输入模式**。可以根据实际情况选择浮空输入、上拉输入或下拉输入，以确保按键的状态能够正确读取。*浮空输入适用于按键有外部上拉或下拉电阻的情况，上拉输入适用于按键接地时为低电平，下拉输入适用于按键接VCC时为高电平的情况。*具体的选择取决于按键连接电路的设计和要求。


#### 请用端口输出数据寄存器(ODR )，编写控制GPIOC口的PC3-PC5引脚输出高电平，其它引脚输出低电平的语句

要使用端口输出数据寄存器（ODR）控制GPIOC口的PC3-PC5引脚输出高电平，其它引脚输出低电平，可以使用以下语句：

```c
GPIOC->ODR |= GPIO_ODR_ODR3 | GPIO_ODR_ODR4 | GPIO_ODR_ODR5; // 设置PC3、PC4、PC5引脚为高电平
GPIOC->ODR &= ~(GPIO_ODR_ODR0 | GPIO_ODR_ODR1 | GPIO_ODR_ODR2); // 设置PC0、PC1、PC2引脚为低电平
```

#### 请用端口置位/清零寄存器(BSRR )，编写控制GPIOB口的PB0-PB5引脚输出高电平，其它引脚保持不变的语句

要使用端口置位/清零寄存器（BSRR）控制GPIOB口的PB0-PB5引脚输出高电平，同时保持其他引脚状态不变，可以使用以下语句：

```c
GPIOB->BSRR = GPIO_BSRR_BS0 | GPIO_BSRR_BS1 | GPIO_BSRR_BS2 | GPIO_BSRR_BS3 | GPIO_BSRR_BS4 | GPIO_BSRR_BS5; // 设置PB0-PB5引脚为高电平
```

#### 请用端口清零寄存器(BRR )，编写控制GPIOD口的PD0-PD3引脚输出低电平，其它引脚保持不变的语句

要使用端口清零寄存器（BRR）控制GPIOD口的PD0-PD3引脚输出低电平，同时保持其他引脚状态不变，可以使用以下语句：

```c
GPIOD->BRR = GPIO_BRR_BR0 | GPIO_BRR_BR1 | GPIO_BRR_BR2 | GPIO_BRR_BR3; // 设置PD0-PD3引脚为低电平
```

#### 简述STM32F103微控制器的GPIO相关各个寄存器的含义和作用

1. GPIO配置寄存器（GPIOx_CRL和GPIOx_CRH）：用于配置GPIO引脚的工作模式、输入/输出类型、输出速度和上下拉等特性。
2. 端口输入数据寄存器（GPIOx_IDR）：用于读取GPIO引脚的输入状态，包括输入高低电平。
3. 端口输出数据寄存器（GPIOx_ODR）：用于设置或读取GPIO引脚的输出状态，可以控制引脚的高低电平。
4. 端口状态寄存器（GPIOx_SR）：用于读取GPIO引脚的状态标志位，包括引脚的输入状态、输出状态和事件状态等。
5. 端口配置锁定寄存器（GPIOx_LCKR）：用于锁定GPIO引脚的配置，防止误操作修改引脚的配置设置。
6. 端口复位寄存器（GPIOx_BRR）：用于通过写入引脚位控制寄存器（BRR）的对应位，将GPIO引脚置为低电平，实现引脚的复位操作。

#### 对比分析STM32寄存器编程和库函数编程两种编程方式的特点

1. 寄存器编程方式：
   - 直接操作硬件寄存器：寄存器编程方式直接操作硬件寄存器，能够直接控制硬件的各个功能和特性。
   - 精确控制：通过寄存器编程可以对硬件进行细粒度的控制，可以灵活地配置和调整各种参数，满足特定的需求。
   - 低层访问：寄存器编程是对硬件的直接访问，属于底层编程方式，对硬件细节要求较高，需要更多的了解和掌握。
   - 更高的性能：由于直接操作寄存器，避免了函数调用和库函数的开销，寄存器编程方式可以获得更高的性能和响应速度。
2. 库函数编程方式：
   - 抽象封装：库函数编程方式通过提供封装好的函数接口，屏蔽了底层的寄存器操作细节，提供了更高层次的抽象。
   - 简化开发：库函数提供了丰富的功能库，包括GPIO、定时器、串口等模块，简化了开发者的工作，减少了代码量。
   - 更高的可移植性：库函数编程方式抽象了底层硬件细节，使得代码更具可移植性，可以在不同的芯片和平台上进行移植和复用。
   - 需要更多的资源：库函数需要占用一定的存储空间，同时运行时需要更多的内存资源，因此对于资源有限的嵌入式系统可能需要权衡。

综上所述，寄存器编程方式适用于对硬件控制要求高、对性能要求高的场景，需要更底层的控制和精确配置；而库函数编程方式则适用于快速开发、提高可移植性和简化开发流程的场景。选择哪种编程方式取决于具体的需求和开发环境。

### 中断

#### 简述STM32F103嵌套向量中断控制器（NVIC）的作用和特点

STM32F103嵌套向量中断控制器（Nested Vectored Interrupt Controller，NVIC）是STM32F103微控制器中负责管理和控制中断的重要模块。它的作用是**协调和处理各种中断请求，并根据中断的优先级和状态进行中断服务程序的调度。**

以下是STM32F103 NVIC的主要特点和作用：

1. 中断优先级管理：NVIC支持对各个中断通道的优先级进行配置和管理。中断通道的优先级可以根据应用需求进行设置，以确保关键的中断能够得到及时响应。
2. 嵌套中断支持：NVIC支持嵌套中断的处理。当一个中断正在处理时，如果有更高优先级的中断请求到达，NVIC会暂时中断当前中断的处理，优先处理更高优先级的中断请求。这种机制确保了关键中断的实时性和优先级的保障。
3. 中断向量表：NVIC维护着中断向量表，用于存储中断服务程序的入口地址。每个中断通道都对应着中断向量表中的一个位置，当中断请求到达时，NVIC会根据中断通道找到对应的中断服务程序并执行。
4. 中断使能和屏蔽：NVIC提供了使能和屏蔽中断的功能。通过设置相应的控制寄存器，可以启用或禁用特定的中断通道，以满足应用的需求。
5. 中断状态管理：NVIC能够管理中断的状态，包括中断挂起、中断激活和中断标志等。这些状态信息可以帮助开发者更好地管理和调试中断程序。

#### 简述STM32F103的NVIC中断优先级分组方法和优先级划分

STM32F103的NVIC中断优先级分组方法和优先级划分主要通过两个寄存器来配置：~~NVIC_IPR（Interrupt Priority Register）和NVIC_ISER（Interrupt Set Enable Register）。~~

1. 中断优先级分组方法：
   - STM32F103支持4种中断优先级分组方式，即分为Group 0、Group 1、Group 2和Group 3。不同的分组方式决定了优先级位数的分配。
   - ~~通过SCB_AIRCR（Application Interrupt and Reset Control Register）寄存器的位[10:8]来配置中断优先级分组方法。~~
2. 优先级划分：
   - 在STM32F103中，中断的优先级范围是从0（最高优先级）到15（最低优先级）。数字越小，优先级越高。
   - 根据选择的中断优先级分组方式，优先级位数的分配有所不同。以下是各个分组方式下的优先级划分情况：
     - Group 0：全局抢占式优先级分组，优先级分配为4位。
     - Group 1：1位抢占式优先级和3位子优先级，优先级分配为3位抢占优先级和1位子优先级。
     - Group 2：2位抢占式优先级和2位子优先级，优先级分配为2位抢占优先级和2位子优先级。
     - Group 3：3位抢占式优先级和1位子优先级，优先级分配为1位抢占优先级和3位子优先级。

通过配置NVIC_IPR寄存器，可以为每个中断通道分配相应的抢占式优先级和子优先级。优先级越高的中断在发生时将优先得到处理，而优先级相同的中断将按照先到先服务（FIFO）的顺序进行处理。

需要注意的是，在STM32F103中，具有相同优先级的中断中，越靠近中断向量表的位置的中断具有更高的优先级。因此，在进行中断优先级划分时，需要根据中断的重要性和实时性要求进行合理的分配。

#### 简述STM32F103的NVIC中断优先级分组中抢占优先级和响应优先级的区别

1. 抢占优先级（Preemption Priority）：
   - 抢占优先级指的是中断发生时，当前正在执行的中断能否被其他中断打断。具有较高抢占优先级的中断可以打断正在执行的低优先级中断，优先获得处理器的控制权。
   - 抢占优先级的数值越小，表示优先级越高，能够打断的中断范围越广。

2. 响应优先级（Subpriority）：
   - 响应优先级指的是在同一抢占优先级下，多个中断同时请求服务时的优先级排序。具有较高响应优先级的中断将首先得到处理器的服务。
   - 响应优先级的数值越小，表示优先级越高。


#### 假定设置中断优先级组为2，然后设置：中断3（ RTC 中断）的抢占优先级为2，响应优先级为1；中断6（外部中断0）的抢占优先级为3，响应优先级为0；中断7（外部中断1）的抢占优先级为2，响应优先级为0。写出这3个中断的优先级顺序。

根据您提供的中断优先级设置，结合中断优先级分组为2，可以确定以下中断的优先级顺序：

1. 中断3（RTC中断）的优先级：抢占优先级 2，响应优先级 1。
2. 中断6（外部中断0）的优先级：抢占优先级 3，响应优先级 0。
3. 中断7（外部中断1）的优先级：抢占优先级 2，响应优先级 0。

根据中断优先级的设置规则：

- 具有较高的抢占优先级的中断可以打断正在执行的低优先级中断。
- 在相同抢占优先级下，具有较高的响应优先级的中断将首先得到处理器的服务。

根据上述设置，优先级顺序为：

1. 中断6（外部中断0）：抢占优先级 3，响应优先级 0。
2. 中断7（外部中断1）：抢占优先级 2，响应优先级 0。
3. 中断3（RTC中断）：抢占优先级 2，响应优先级 1。

因此，中断6（外部中断0）具有最高优先级，中断3（RTC中断）具有次高优先级，中断7（外部中断1）具有最低优先级。

### 定时器/计数器简答

#### STM32F103微控制器的常规定时器分为哪3种?

1. TIM1（定时器1）：这是一个高级定时器，具有较复杂的功能和多路输出通道，可用于实现高级的定时和PWM控制。
2. TIM2（定时器2）：这是一个通用定时器，具有基本的定时功能，可用于一般的定时和计数应用。
3. TIM3（定时器3）：这是一个通用定时器，与TIM2类似，也具有基本的定时和计数功能，可广泛应用于定时和计数需求。

#### STM32F103微控制器的高级定时器和通用定时器的功能主要有什么区别？

高级定时器（如TIM1）：

1. 多路输出通道：高级定时器通常具有多个输出通道，可以用于实现更复杂的PWM控制和输出信号。
2. 高级控制功能：高级定时器提供更多的高级控制功能，如编码器模式、输入捕获、输出比较、PWM生成等，能够满足更复杂的定时和控制需求。
3. 高精度定时：高级定时器通常具有更高的计数精度和更大的计数范围，可以实现更精确的定时操作。

通用定时器（如TIM2、TIM3等）：

1. 基本定时功能：通用定时器提供基本的定时和计数功能，能够满足常见的定时需求。
2. 灵活性和易用性：通用定时器的配置和使用相对简单，适用于一般的定时和计数应用。
3. 低功耗模式：通用定时器通常支持低功耗模式，可以在需要时降低功耗，延长电池寿命。

总体而言，高级定时器具有更多的高级功能和扩展性，适用于复杂的定时和控制需求，而通用定时器则更适用于常见的定时和计数应用，并具有简单易用和低功耗的特点。选择合适的定时器取决于具体的应用需求和功能要求。

#### STM32F103定时器的计数器模式有哪3种?

1. 向上计数模式（Up Counter Mode）：定时器从0开始计数，逐渐增加，直到计数值达到设定的上限值（比如自动重载值），然后重新从0开始计数。在该模式下，定时器的输出信号可以用于生成定时中断或驱动其他外设。
2. 向下计数模式（Down Counter Mode）：定时器从设定的上限值（比如自动重载值）开始计数，逐渐减小，直到计数值为0。在该模式下，定时器的输出信号可以用于生成定时中断或驱动其他外设。
3. 中央对齐模式（Center-aligned Mode）：定时器在向上计数和向下计数之间来回切换，计数器值会在自动重载值的一半处反向。这种模式下的计数器可以产生对称的波形，对于一些特定的应用场景如PWM输出很有用。

### ADC简答

#### 简述STM32F103的ADC规则通道组和注入通道组之间的关系

**规则通道组是用于常规的模数转换，它可以配置多个通道进行连续的模数转换。**规则通道组的转换顺序可以根据需要进行设置，可以按照顺序依次转换多个通道的模拟输入信号。

**注入通道组则是用于特定的应用场景，如精确的采样或触发转换。注入通道组可以单独配置一个或多个通道进行模数转换**，并且可以使用特定的触发源来触发转换。

规则通道组和注入通道组之间是相互独立的，它们有各自独立的转换序列和设置。在配置时，可以选择使用规则通道组、注入通道组或两者同时使用，以满足不同的应用需求。

总结而言，规则通道组和注入通道组是用于不同的模数转换应用场景的两种通道组，可以根据具体需求配置和使用。

### 串口简答

#### 简述如何判断STM32F103的串口是否完成数据发送和接收

1. 发送完成标志位（TXE）：通过读取串口状态寄存器（SR）中的TXE标志位来判断是否完成数据发送。当TXE标志位为1时，表示发送缓冲器为空，可以继续发送数据；当TXE标志位为0时，表示发送缓冲器正在发送数据，还未完成发送。
2. 数据接收完成标志位（RXNE）：通过读取串口状态寄存器（SR）中的RXNE标志位来判断是否完成数据接收。当RXNE标志位为1时，表示接收缓冲器中已有接收到的数据，可以读取；当RXNE标志位为0时，表示接收缓冲器为空，还未有新的数据接收。

可以使用相关的寄存器和标志位来进行判断，具体操作如下：

1. 判断发送完成：**通过检查USART_SR寄存器中的TXE标志位，当TXE为1时，表示发送完成。**
2. 判断数据接收完成：**通过检查USART_SR寄存器中的RXNE标志位，当RXNE为1时，表示数据接收完成。**

#### 串行通信分为异步通信和同步通信，简述异步通信和同步通信的区别

异步通信和同步通信是两种不同的串行通信方式，它们的区别在于*数据传输的时钟信号的处理方式和数据帧的组织方式。*

异步通信：

- 异步通信**使用两个信号线，分别是数据线（TXD和RXD）和单个的时钟信号线（通常为波特率时钟）。**
- 数据的传输是基于起始位、数据位、奇偶校验位和停止位构成的数据帧进行的。**每个数据帧之间没有固定的时间间隔。**
- **发送端和接收端的时钟频率可以略有差异**，因此需要在接收端通过起始位的边沿检测来同步数据。
- 异步通信**适用于短距离和低速率的通信**，例如串口通信。

同步通信：

- 同步通信**使用单独的时钟信号线来同步数据的传输**，也称为时钟同步通信。
- 数据的传输是基于固定的时钟信号来同步发送和接收的。数据被切分成多个连续的数据帧，**每个数据帧的长度和时钟信号的周期相对应。**
- **发送端和接收端的时钟频率必须保持一致**，以确保数据的正确接收。
- 同步通信**适用于高速率和长距离的通信**，例如以太网通信和SPI通信。

总结：
异步通信和同步通信的主要区别在于时钟信号的处理方式和数据帧的组织方式。
**异步通信使用单个时钟信号和数据帧的起始位、数据位、奇偶校验位和停止位进行数据传输，而同步通信则使用单独的时钟信号来同步数据的传输，数据被切分成连续的数据帧并通过固定的时钟信号周期来同步发送和接收。**

### 操作系统简答

#### uC/OS-II操作系统中，信号量和互斥信号量在功能上的主要区别是什么？

1. 信号量（Semaphore）：
   - 信号量是一种**用于控制对资源的访问的机制，可以用来表示可用资源的数量。**
   - 信号量可以实现资源的共享和同步，**允许多个任务对同一资源进行访问。**
   - 信号量有两种类型：**二进制信号量和计数信号量。**
   - *二进制信号量的值只能为0或1，用于实现互斥访问，即只允许一个任务访问资源。*
   - *计数信号量的值可以是任意非负整数，用于表示可用资源的数量。*
   - 任务可以**通过等待信号量来获取资源**，*如果资源不可用，则任务会被阻塞，直到资源可用为止。*
2. 互斥信号量（Mutex）：
   - 互斥信号量是一种**特殊的信号量，用于实现互斥访问共享资源。**
   - 互斥信号量可以**保证同一时间只有一个任务可以访问共享资源**，避免了多个任务同时访问导致的数据竞争和冲突。
   - 互斥信号量*在任务访问共享资源之前需要进行获取（P操作），在任务使用完资源后需要进行释放（V操作）。*
   - 如果互斥信号量已经被一个任务获取，*其他任务尝试获取该互斥信号量时会被阻塞，直到互斥信号量被释放。*

总结：

信号量用于控制对资源的访问，可以实现资源的共享和同步；

而互斥信号量是一种特殊的信号量，用于实现互斥访问共享资源，确保同一时间只有一个任务可以访问共享资源。

互斥信号量是信号量的一种特殊形式，用于解决共享资源的互斥访问问题。

#### uC/OS-II操作系统中，信号量和消息邮箱在功能上的主要区别是什么？

1. 信号量（Semaphore）：
   - 信号量用于控制对资源的访问和同步任务的执行顺序。
   - 信号量可以表示可用资源的数量，任务可以通过等待信号量来获取资源，如果资源不可用，则任务会被阻塞，直到资源可用为止。
   - 信号量的值可以是任意非负整数，可以用来表示资源的数量或者某种条件的满足情况。
   - 信号量可以用于实现资源的共享和同步，多个任务可以同时等待和释放同一个信号量。
2. 消息邮箱（Message Mailbox）：
   - 消息邮箱用于在任务之间传递消息和数据。
   - 消息邮箱可以存储一个或多个消息，每个消息可以是一个固定长度的数据结构。
   - 任务可以通过发送消息到邮箱来向其他任务传递数据，也可以通过接收消息来获取其他任务发送的数据。
   - 消息邮箱具有缓冲区的功能，当邮箱已满时，发送任务会被阻塞，直到有空间可用；当邮箱为空时，接收任务会被阻塞，直到有消息可接收。

总结：

**信号量用于控制资源的访问和同步任务的执行顺序，多个任务可以同时等待和释放同一个信号量；而消息邮箱用于在任务之间传递消息和数据，具有缓冲区的功能，可以存储多个消息。信号量更适用于控制资源的共享和同步，而消息邮箱更适用于任务间的数据传递和通信。**

#### uC/OS-II操作系统中，消息邮箱和消息队列在功能上的主要区别是什么？

1. 消息邮箱（Message Mailbox）：
   - 消息邮箱用于在任务之间传递消息和数据。
   - 消息邮箱可以存储一个或多个消息，每个消息可以是一个固定长度的数据结构。
   - 发送任务通过发送消息到邮箱来向其他任务传递数据，接收任务通过接收消息来获取其他任务发送的数据。
   - 消息邮箱具有缓冲区的功能，当邮箱已满时，发送任务会被阻塞，直到有空间可用；当邮箱为空时，接收任务会被阻塞，直到有消息可接收。
2. 消息队列（Message Queue）：
   - 消息队列用于在任务之间传递消息和数据。
   - 消息队列可以存储一个或多个消息，每个消息可以是一个可变长度的数据结构。
   - 发送任务通过发送消息到队列来向其他任务传递数据，接收任务通过接收消息来获取其他任务发送的数据。
   - 消息队列具有先进先出（FIFO）的特性，保证消息按照发送的顺序进行接收。

总结：

**消息邮箱和消息队列都用于任务间的消息传递和数据通信，但它们在消息存储方式和特性上有所不同。消息邮箱适用于固定长度的消息存储和同步发送和接收任务的操作，而消息队列适用于可变长度的消息存储和按照发送顺序进行接收的操作。**

## 程序设计

### GPIO程序设计

#### 采用库函数编写通用GPIO控制程序，实现PB5控制LED灯周期闪烁，闪烁周期约为1s，采用软件延时方法。程序应包括GPIO初始化函数和主函数main（）代码

以下是使用库函数编写通用GPIO控制程序，实现PB5控制LED灯周期闪烁的示例代码：

```c
#include "stm32f10x.h"  // 包含STM32F103系列的头文件

// GPIO初始化函数
void GPIO_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStructure;

    // 使能GPIOB的时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB, ENABLE);

    // 配置PB5引脚为推挽输出
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_5;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOB, &GPIO_InitStructure);
}

// 这部分考试时候可不写
// 延时函数，使用软件延时
void Delay(uint32_t nCount)
{
    for (volatile uint32_t i = 0; i < nCount; i++)
    {
        for (volatile uint32_t j = 0; j < 1000; j++)
        {
            // 空操作，用于延时
        }
    }
}

int main(void)
{
    // 初始化GPIO
    GPIO_Init();

    while (1)
    {
        // 控制LED灯亮
        GPIO_SetBits(GPIOB, GPIO_Pin_5);

        // 延时约1s
        Delay(1000);

        // 控制LED灯灭
        GPIO_ResetBits(GPIOB, GPIO_Pin_5);

        // 延时约1s
        Delay(1000);
    }
}
```

上述代码中，首先在`GPIO_Init()`函数中初始化了GPIOB的PB5引脚为推挽输出模式。然后，在`main()`函数中，通过循环控制LED灯周期性地闪烁。通过调用`GPIO_SetBits()`和`GPIO_ResetBits()`函数来控制PB5引脚的电平，实现LED灯的亮和灭。通过调用`Delay()`函数进行软件延时，延时约1秒的时间。循环执行这个过程，就可以实现LED灯的周期性闪烁。

#### 采用库函数编写通用GPIO控制程序，实现PB5和PE5控制的2个LED灯交替闪烁，闪烁周期约为1s。程序应包括GPIO初始化函数和主函数main（）代码

以下是使用库函数编写通用GPIO控制程序，实现PB5和PE5控制的两个LED灯交替闪烁的示例代码：

```c
#include "stm32f10x.h"  // 包含STM32F103系列的头文件

// GPIO初始化函数
void GPIO_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStructure;

    // 使能GPIOB和GPIOE的时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOB | RCC_APB2Periph_GPIOE, ENABLE);

    // 配置PB5引脚为推挽输出
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_5;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOB, &GPIO_InitStructure);

    // 配置PE5引脚为推挽输出
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_5;
    GPIO_Init(GPIOE, &GPIO_InitStructure);
}

// 考试时可不写
// 延时函数，使用软件延时
void Delay(uint32_t nCount)
{
    for (volatile uint32_t i = 0; i < nCount; i++)
    {
        for (volatile uint32_t j = 0; j < 1000; j++)
        {
            // 空操作，用于延时
        }
    }
}

int main(void)
{
    // 初始化GPIO
    GPIO_Init();

    while (1)
    {
        // 控制PB5引脚为高电平，PE5引脚为低电平
        GPIO_SetBits(GPIOB, GPIO_Pin_5);
        GPIO_ResetBits(GPIOE, GPIO_Pin_5);

        // 延时约1s
        Delay(1000);

        // 控制PB5引脚为低电平，PE5引脚为高电平
        GPIO_ResetBits(GPIOB, GPIO_Pin_5);
        GPIO_SetBits(GPIOE, GPIO_Pin_5);

        // 延时约1s
        Delay(1000);
    }
}
```

上述代码中，首先在`GPIO_Init()`函数中初始化了GPIOB的PB5引脚和GPIOE的PE5引脚为推挽输出模式。然后，在`main()`函数中，通过循环控制两个LED灯的交替闪烁。通过调用`GPIO_SetBits()`和`GPIO_ResetBits()`函数来控制PB5和PE5引脚的电平，实现LED灯的亮和灭。通过调用`Delay()`函数进行软件延时，延时约1秒的时间。循环执行这个过程，就可以实现两个LED灯的交替闪烁。

#### 采用库函数编写通用GPIO控制程序，实现8个LED循环依次点亮功能，8个LED由PE0~PE7控制，低电平点亮。程序应包括GPIO初始化函数和主函数main（）代码

以下是使用库函数编写通用GPIO控制程序，实现8个LED循环依次点亮的示例代码：

```c
#include "stm32f10x.h"  // 包含STM32F103系列的头文件

// GPIO初始化函数
void GPIO_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStructure;

    // 使能GPIOE的时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOE, ENABLE);

    // 配置PE0~PE7引脚为推挽输出
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3 |
                                  GPIO_Pin_4 | GPIO_Pin_5 | GPIO_Pin_6 | GPIO_Pin_7;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOE, &GPIO_InitStructure);
}

int main(void)
{
    // 初始化GPIO
    GPIO_Init();

    while (1)
    {
        // 依次点亮8个LED，通过循环和位运算实现
        for (int i = 0; i < 8; i++)
        {
            // 将对应的引脚设置为低电平，点亮LED
            GPIO_ResetBits(GPIOE, (1 << i));

            // 延时一段时间
            for (volatile int j = 0; j < 1000000; j++)
            {
                // 空操作，用于延时
            }

            // 将对应的引脚设置为高电平，熄灭LED
            GPIO_SetBits(GPIOE, (1 << i));
        }
    }
}
```

上述代码中，首先在`GPIO_Init()`函数中初始化了GPIOE的PE0~PE7引脚为推挽输出模式。然后，在`main()`函数中，通过循环依次点亮8个LED。通过循环和位运算，将对应的引脚设置为低电平，点亮LED，并延时一段时间。然后将对应的引脚设置为高电平，熄灭LED。循环执行这个过程，就可以实现8个LED的循环依次点亮的效果。

#### 采用库函数编写通用GPIO控制程序，实现PC口（PC0~PC7）控制1位共阳极数码管循环显示数字0~9的功能，每个数字显示停留时间约为1s。程序应包括GPIO初始化函数和主函数main（）代码

以下是使用库函数编写通用GPIO控制程序，实现PC口控制1位共阳极数码管循环显示数字0~9的示例代码：

```c
#include "stm32f10x.h"  // 包含STM32F103系列的头文件

// 数码管数字编码表
const uint8_t digitCode[] = {
    0x3F,  // 0
    0x06,  // 1
    0x5B,  // 2
    0x4F,  // 3
    0x66,  // 4
    0x6D,  // 5
    0x7D,  // 6
    0x07,  // 7
    0x7F,  // 8
    0x6F   // 9
};

// GPIO初始化函数
void GPIO_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStructure;

    // 使能GPIOC的时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);

    // 配置PC0~PC7引脚为推挽输出
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3 |
                                  GPIO_Pin_4 | GPIO_Pin_5 | GPIO_Pin_6 | GPIO_Pin_7;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOC, &GPIO_InitStructure);
}

int main(void)
{
    // 初始化GPIO
    GPIO_Init();

    uint8_t digit = 0;  // 当前显示的数字

    while (1)
    {
        // 根据当前数字设置PC0~PC7引脚的输出状态
        GPIO_Write(GPIOC, digitCode[digit]);

        // 延时一段时间
        for (volatile int i = 0; i < 1000000; i++)
        {
            // 空操作，用于延时
        }

        // 切换到下一个数字
        digit++;
        if (digit > 9)
        {
            digit = 0;
        }
    }
}
```

上述代码中，首先在`GPIO_Init()`函数中初始化了GPIOC的PC0~PC7引脚为推挽输出模式。然后，在`main()`函数中，通过循环依次显示数字0~9。在每个循环中，根据当前数字设置PC0~PC7引脚的输出状态，通过写入相应的数码管数字编码。然后延时一段时间，切换到下一个数字，再次循环显示。通过这个过程，可以实现PC口控制1位共阳极数码管循环显示数字0~9的功能。

### EXTI程序设计

#### 采用库函数编写程序，实现对按键的外部中断输入（PE2）的响应，用LED灯（PC5）状态反映按键的按下，每次按键按下时（下降沿中断）将LED灯状态取反。（写出PE2外部中断初始化代码和外部中断服务函数的代码）

下面是使用库函数编写的程序示例，实现对按键的外部中断输入的响应，用LED灯状态反映按键的按下：

```c
#include "stm32f10x.h"  // 包含STM32F103系列的头文件

// GPIO初始化函数
void GPIO_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStructure;

    // 使能GPIOC和GPIOE的时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOE, ENABLE);

    // 配置PC5引脚为推挽输出
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_5;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOC, &GPIO_InitStructure);

    // 配置PE2引脚为上拉输入
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_2;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
    GPIO_Init(GPIOE, &GPIO_InitStructure);
}

// 外部中断初始化函数
void EXTI_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStructure;
    EXTI_InitTypeDef EXTI_InitStructure;
    NVIC_InitTypeDef NVIC_InitStructure;

    // 使能AFIO的时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);

    // 配置PE2引脚为中断输入
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_2;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPD;  // 下拉输入
    GPIO_Init(GPIOE, &GPIO_InitStructure);

    // 配置外部中断线路
    GPIO_EXTILineConfig(GPIO_PortSourceGPIOE, GPIO_PinSource2);

    // 配置外部中断参数
    EXTI_InitStructure.EXTI_Line = EXTI_Line2;
    EXTI_InitStructure.EXTI_Mode = EXTI_Mode_Interrupt;
    EXTI_InitStructure.EXTI_Trigger = EXTI_Trigger_Falling;  // 下降沿触发
    EXTI_InitStructure.EXTI_LineCmd = ENABLE;
    EXTI_Init(&EXTI_InitStructure);

    // 配置中断优先级
    NVIC_InitStructure.NVIC_IRQChannel = EXTI2_IRQn;
    NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 0x00;  // 抢占优先级为0
    NVIC_InitStructure.NVIC_IRQChannelSubPriority = 0x00;         // 响应优先级为0
    NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
    NVIC_Init(&NVIC_InitStructure);
}

// 外部中断服务函数
void EXTI2_IRQHandler(void)
{
    if (EXTI_GetITStatus(EXTI_Line2) != RESET)
    {
        // 等待一段时间消除抖动
        for (volatile int i = 0; i < 100000; i++)
        {
            // 空操作，用于延时
        }

        // 检查按键是否按下（下降沿触发）
        if (GPIO_ReadInputDataBit(GPIOE, GPIO_Pin_2) == RESET)
        {
            // 反转LED灯状态
            GPIO_WriteBit(GPIOC, GPIO_Pin_5, (BitAction)(1 - GPIO_ReadOutputDataBit(GPIOC, GPIO_Pin_5)));
        }

        // 清除中断标志位
        EXTI_ClearITPendingBit(EXTI_Line2);
    }
}

```

#### 采用库函数编写程序，实现对按键的外部中断输入（PE4）的响应，用LED灯（PC5）状态反映按键的按下，每次按键按下时（上升沿中断）将LED灯状态取反。（写出PE4外部中断初始化代码和外部中断服务函数的代码）

下面是使用库函数编写的程序示例，实现对按键的外部中断输入的响应，用LED灯状态反映按键的按下：

```c
#include "stm32f10x.h"  // 包含STM32F103系列的头文件

// GPIO初始化函数
void GPIO_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStructure;

    // 使能GPIOC和GPIOE的时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOE, ENABLE);

    // 配置PC5引脚为推挽输出
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_5;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOC, &GPIO_InitStructure);

    // 配置PE4引脚为上拉输入
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_4;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
    GPIO_Init(GPIOE, &GPIO_InitStructure);
}

// 外部中断初始化函数
void EXTI_Init(void)
{
    GPIO_InitTypeDef GPIO_InitStructure;
    EXTI_InitTypeDef EXTI_InitStructure;
    NVIC_InitTypeDef NVIC_InitStructure;

    // 使能AFIO的时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);

    // 配置PE4引脚为中断输入
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_4;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPD;  // 下拉输入
    GPIO_Init(GPIOE, &GPIO_InitStructure);

    // 配置外部中断线路
    GPIO_EXTILineConfig(GPIO_PortSourceGPIOE, GPIO_PinSource4);

    // 配置外部中断参数
    EXTI_InitStructure.EXTI_Line = EXTI_Line4;
    EXTI_InitStructure.EXTI_Mode = EXTI_Mode_Interrupt;
    EXTI_InitStructure.EXTI_Trigger = EXTI_Trigger_Rising;  // 上升沿触发
    EXTI_InitStructure.EXTI_LineCmd = ENABLE;
    EXTI_Init(&EXTI_InitStructure);

    // 配置中断优先级
    NVIC_InitStructure.NVIC_IRQChannel = EXTI4_IRQn;
    NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 0x00;  // 抢占优先级为0
    NVIC_InitStructure.NVIC_IRQChannelSubPriority = 0x00;         // 响应优先级为0
    NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
    NVIC_Init(&NVIC_InitStructure);
}

// 外部中断服务函数
void EXTI4_IRQHandler(void)
{
    if (EXTI_GetITStatus(EXTI_Line4) != RESET)
    {
        // 等待一段时间消除抖动
        for (volatile int i = 0; i < 100000; i++)
        {
            // 空操作，用于延时
        }

        // 检查按键是否按下（上升沿触发）
        if (GPIO_ReadInputDataBit(GPIOE, GPIO_Pin_4) == SET)
        {
            // 反转LED灯状态
            GPIO_WriteBit(GPIOC, GPIO_Pin_5, (BitAction)(1 - GPIO_ReadOutputDataBit(GPIOC, GPIO_Pin_5)));
        }

        // 清除中断标志位
        EXTI_ClearITPendingBit(EXTI_Line4);
    }
}

```

#### 补充 : (BitAction)(1 - GPIO_ReadOutputDataBit(GPIOC, GPIO_Pin_5)是什么含义

```tex
在之前的案例中，`(BitAction)(1 - GPIO_ReadOutputDataBit(GPIOC, GPIO_Pin_5)`是一个表达式，用于取反GPIOC的第5个引脚（即PC5）的输出状态。

`GPIO_ReadOutputDataBit(GPIOC, GPIO_Pin_5)`函数用于读取GPIOC的第5个引脚（即PC5）的输出状态，返回值为0或1，表示引脚的电平状态。

`(1 - GPIO_ReadOutputDataBit(GPIOC, GPIO_Pin_5)`中的`(1 - ...)`部分将读取的引脚状态取反，即如果引脚的输出为0，则结果为1，如果引脚的输出为1，则结果为0。

最外层的`(BitAction)`则将取反后的结果转换为`BitAction`类型，`BitAction`是一个枚举类型，表示引脚的状态，取值可以是`Bit_RESET`（低电平）或`Bit_SET`（高电平）。

因此，`(BitAction)(1 - GPIO_ReadOutputDataBit(GPIOC, GPIO_Pin_5)`的含义是将GPIOC的第5个引脚的输出状态取反，并将结果转换为`BitAction`类型，用于控制该引脚的输出状态。
```

### TIM

#### 采用库函数编写通用定时器TIM2的初始化程序，设置定时器TIM2的预分频值为7199，定时时间为10ms，加计数模式，使能TIM2的刷新中断，中断抢占优先级为2，响应优先级为3

下面是使用库函数编写的通用定时器TIM2的初始化程序，设置定时器TIM2的预分频值为7199，定时时间为10ms，加计数模式，使能TIM2的刷新中断，并设置中断优先级为抢占优先级2，响应优先级3的代码：

```c
#include "stm32f10x.h"  // 包含STM32F103系列的头文件

// 定时器TIM2初始化函数
void TIM2_Init(void)
{
    TIM_TimeBaseInitTypeDef TIM_TimeBaseStructure;
    NVIC_InitTypeDef NVIC_InitStructure;

    // 使能TIM2的时钟
    RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);

    // 配置定时器TIM2
    TIM_TimeBaseStructure.TIM_Period = 999;  // 计数器自动重装值
    TIM_TimeBaseStructure.TIM_Prescaler = 7199;  // 预分频值
    TIM_TimeBaseStructure.TIM_CounterMode = TIM_CounterMode_Up;  // 加计数模式
    TIM_TimeBaseStructure.TIM_ClockDivision = TIM_CKD_DIV1;  // 时钟分频
    TIM_TimeBaseStructure.TIM_RepetitionCounter = 0;
    TIM_TimeBaseInit(TIM2, &TIM_TimeBaseStructure);

    // 配置TIM2的更新中断
    TIM_ITConfig(TIM2, TIM_IT_Update, ENABLE);

    // 配置中断优先级
    NVIC_InitStructure.NVIC_IRQChannel = TIM2_IRQn;
    NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 0x02;  // 抢占优先级为2
    NVIC_InitStructure.NVIC_IRQChannelSubPriority = 0x03;         // 响应优先级为3
    NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
    NVIC_Init(&NVIC_InitStructure);

    // 使能定时器TIM2
    TIM_Cmd(TIM2, ENABLE);
}

// 定时器TIM2中断服务函数
void TIM2_IRQHandler(void)
{
    if (TIM_GetITStatus(TIM2, TIM_IT_Update) != RESET)
    {
        // 在此处理定时器中断相关的操作

        // 清除中断标志位
        TIM_ClearITPendingBit(TIM2, TIM_IT_Update);
    }
}
```

请注意，以上代码只是TIM2定时器的初始化和中断处理部分，你还需要在主函数中调用`TIM2_Init()`函数进行初始化，并启用全局中断。

#### 采用库函数编写通用定时器TIM3的初始化程序，设置定时器TIM3的预分频值为7199，定时时间为100ms，加计数模式，使能TIM3的刷新中断，中断抢占优先级为1，响应优先级为2。

下面是使用库函数编写的通用定时器TIM3的初始化程序，设置定时器TIM3的预分频值为7199，定时时间为100ms，加计数模式，使能TIM3的刷新中断，并设置中断优先级为抢占优先级1，响应优先级2的代码：

```c
#include "stm32f10x.h"  // 包含STM32F103系列的头文件

// 定时器TIM3初始化函数
void TIM3_Init(void)
{
    TIM_TimeBaseInitTypeDef TIM_TimeBaseStructure;
    NVIC_InitTypeDef NVIC_InitStructure;

    // 使能TIM3的时钟
    RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM3, ENABLE);

    // 配置定时器TIM3
    TIM_TimeBaseStructure.TIM_Period = 9999;  // 计数器自动重装值
    TIM_TimeBaseStructure.TIM_Prescaler = 7199;  // 预分频值
    TIM_TimeBaseStructure.TIM_CounterMode = TIM_CounterMode_Up;  // 加计数模式
    TIM_TimeBaseStructure.TIM_ClockDivision = TIM_CKD_DIV1;  // 时钟分频
    TIM_TimeBaseStructure.TIM_RepetitionCounter = 0;
    TIM_TimeBaseInit(TIM3, &TIM_TimeBaseStructure);

    // 配置TIM3的更新中断
    TIM_ITConfig(TIM3, TIM_IT_Update, ENABLE);

    // 配置中断优先级
    NVIC_InitStructure.NVIC_IRQChannel = TIM3_IRQn;
    NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 0x01;  // 抢占优先级为1
    NVIC_InitStructure.NVIC_IRQChannelSubPriority = 0x02;         // 响应优先级为2
    NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
    NVIC_Init(&NVIC_InitStructure);

    // 使能定时器TIM3
    TIM_Cmd(TIM3, ENABLE);
}

// 定时器TIM3中断服务函数
void TIM3_IRQHandler(void)
{
    if (TIM_GetITStatus(TIM3, TIM_IT_Update) != RESET)
    {
        // 在此处理定时器中断相关的操作

        // 清除中断标志位
        TIM_ClearITPendingBit(TIM3, TIM_IT_Update);
    }
}
```

请注意，以上代码只是TIM3定时器的初始化和中断处理部分，你还需要在主函数中调用`TIM3_Init()`函数进行初始化，并启用全局中断。

#### 补充 : 计算TIM_TimeBaseStructure.TIM_Period(计数器自动重装载值)

```tex
在上个案例中，`TIM_TimeBaseStructure.TIM_Period`的值设置为9999，是为了实现100ms的定时时间。

定时器的计数器值会在0到TIM_Period之间循环计数，当计数器达到TIM_Period时，就会产生更新事件（溢出），并触发中断（如果使能了中断）。因此，定时器的定时时间可以通过设置TIM_Period的值来控制。

在STM32F103微控制器中，定时器的计数器位数是16位，因此最大计数值为65535。要计算TIM_Period的值以实现100ms的定时，可以使用以下公式：

TIM_Period = (定时时间 / 计数周期) - 1

其中，定时时间是以秒为单位，计数周期是定时器的预分频值与定时器时钟频率之间的比例关系。在这个案例中，预分频值为7199（`TIM_TimeBaseStructure.TIM_Prescaler = 7199`），定时器时钟频率为72 MHz。

计算过程如下：

计数周期 = 预分频值 + 1 = 7199 + 1 = 7200
定时时间 = 0.1 秒（100ms）

TIM_Period = (0.1 / 7200) - 1 = 0.0000138888 - 1 ≈ 1388

因为TIM_Period是一个16位的无符号整数，所以需要确保计算出的值在16位的范围内。在这种情况下，取TIM_Period = 1388是一个合适的值，可以实现约100ms的定时。
```

### 综合题

#### 采用库函数编写程序，实现对按键的外部中断输入（PC3）的响应，每次按键按下时记录按下的次数，并通过串口2将按键次数传送给上位机的串口助手显示

题目
采用库函数编写程序，实现对按键的外部中断输入（PC3）的响应，每次按键按下时记录按下的次数，并通过串口2将按键次数传送给上位机的串口助手显示。要求：
（1）写出按键外部中断初始化代码，初始化为上升沿触发中断。
（2）写出串口2的初始化代码，初始化串口2的波特率为19200bps，8位数据位，1位停止位，PA2作为发送端，PA3作为接收端。
（3）编写按键的外部中断服务函数，完成按键次数计数和串口2向上位机发送计数值的功能。

下面是针对上述要求的示例代码：

```c
#include "stm32f10x.h"
#include "stm32f10x_gpio.h"
#include "stm32f10x_rcc.h"
#include "stm32f10x_exti.h"
#include "stm32f10x_usart.h"

// 定义按键引脚和外部中断线
#define BUTTON_PIN GPIO_Pin_3
#define BUTTON_PORT GPIOC
#define BUTTON_EXTI_LINE EXTI_Line3

// 定义串口2引脚和相关参数
#define USART_TX_PIN GPIO_Pin_2
#define USART_RX_PIN GPIO_Pin_3
#define USART_PORT GPIOA
#define USART USART2

// 全局变量，记录按键次数
volatile uint32_t buttonPressCount = 0;

// 函数声明
void EXTI_Configuration(void);
void USART_Configuration(void);
void USART_SendDataString(uint8_t* data);

int main(void)
{
    // 初始化外部中断
    EXTI_Configuration();

    // 初始化串口2
    USART_Configuration();

    while (1)
    {
        // 主循环中不需要做其他操作
    }
}

// （1）写出按键外部中断初始化代码，初始化为上升沿触发中断。
void EXTI_Configuration(void)
{
    // 使能GPIOC时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);

    // 配置按键引脚为输入模式
    GPIO_InitTypeDef GPIO_InitStructure;
    GPIO_InitStructure.GPIO_Pin = BUTTON_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU; // 上拉输入
    GPIO_Init(BUTTON_PORT, &GPIO_InitStructure);

    // 使能AFIO时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);

    // 连接外部中断线到按键引脚
    GPIO_EXTILineConfig(GPIO_PortSourceGPIOC, GPIO_PinSource3);

    // 配置外部中断线为上升沿触发中断
    EXTI_InitTypeDef EXTI_InitStructure;
    EXTI_InitStructure.EXTI_Line = BUTTON_EXTI_LINE;
    EXTI_InitStructure.EXTI_Mode = EXTI_Mode_Interrupt;
    EXTI_InitStructure.EXTI_Trigger = EXTI_Trigger_Rising; // 上升沿触发
    EXTI_InitStructure.EXTI_LineCmd = ENABLE;
    EXTI_Init(&EXTI_InitStructure);

    // 使能外部中断通道
    NVIC_InitTypeDef NVIC_InitStructure;
    NVIC_InitStructure.NVIC_IRQChannel = EXTI3_IRQn;
    NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 0x02; // 抢占优先级为2
    NVIC_InitStructure.NVIC_IRQChannelSubPriority = 0x03;        // 响应优先级为3
    NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
    NVIC_Init(&NVIC_InitStructure);
}


// （2）写出串口2的初始化代码，初始化串口2的波特率为19200bps，8位数据位，1位停止位，PA2作为发送端，PA3作为接收端。
void USART_Configuration(void)
{
    // 使能GPIOA时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);

    // 使能USART2时钟
    RCC_APB1PeriphClockCmd(RCC_APB1Periph_USART2, ENABLE);

    // 配置USART引脚为复用功能
    GPIO_InitTypeDef GPIO_InitStructure;
    GPIO_InitStructure.GPIO_Pin = USART_TX_PIN | USART_RX_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP; // 复用推挽输出
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(USART_PORT, &GPIO_InitStructure);

    // 配置USART参数


    USART_InitTypeDef USART_InitStructure;
    USART_InitStructure.USART_BaudRate = 19200;
    USART_InitStructure.USART_WordLength = USART_WordLength_8b;
    USART_InitStructure.USART_StopBits = USART_StopBits_1;
    USART_InitStructure.USART_Parity = USART_Parity_No;
    USART_InitStructure.USART_HardwareFlowControl = USART_HardwareFlowControl_None;
    USART_InitStructure.USART_Mode = USART_Mode_Tx; // 仅发送模式
    USART_Init(USART, &USART_InitStructure);

    // 使能USART
    USART_Cmd(USART, ENABLE);
}

// （3）编写按键的外部中断服务函数，完成按键次数计数和串口2向上位机发送计数值的功能。
void EXTI3_IRQHandler(void)
{
    // 检查按键外部中断是否发生
    if (EXTI_GetITStatus(BUTTON_EXTI_LINE) != RESET)
    {
        // 延时一段时间，防止抖动
        for (volatile uint32_t i = 0; i < 100000; i++);

        // 记录按键次数
        buttonPressCount++;

        // 发送按键次数到串口
        char countStr[10];
        sprintf(countStr, "Press count: %lu\r\n", buttonPressCount);
        USART_SendDataString((uint8_t*)countStr);

        // 清除中断标志位
        EXTI_ClearITPendingBit(BUTTON_EXTI_LINE);
    }
}

void USART_SendDataString(uint8_t* data)
{
    while (*data)
    {
        USART_SendData(USART, *data++);
        while (USART_GetFlagStatus(USART, USART_FLAG_TXE) == RESET);
    }
}
```

以上代码实现了对PC3按键的外部中断响应，每次按键按下时会记录按下的次数，并通过串口2将按键次数发送给上位机的串口助手进行显示。在初始化时，外部中断被配置为上升沿触发中断，串口2被初始化为波特率为19200bps、8位数据位、1位停止位的配置。按键的外部中断服务函数中，会先进行一段延时以避免按键抖动，然后记录按键次数并将其通过串口2发送出去。

#### 采用库函数编写程序，实现对按键的外部中断输入（PE2）的响应，每次按键按下时记录按下的次数，并通过串口1将按键次数传送给上位机的串口助手显示

题目 :

采用库函数编写程序，实现对按键的外部中断输入（PE2）的响应，每次按键按下时记录按下的次数，并通过串口1将按键次数传送给上位机的串口助手显示。要求：

（1）写出按键的外部中断初始化代码，初始化为下降沿触发中断。
（2）写出串口1的初始化代码，初始化串口1的波特率为9600bps，8位数据位，1位停止位，PA9作为发送端，PA10作为接收端。
（3）编写按键的外部中断服务函数，完成按键次数计数和串口1向上位机发送计数值的功能。

下面是针对上述要求的示例代码：

```c
#include "stm32f10x.h"
#include "stm32f10x_gpio.h"
#include "stm32f10x_rcc.h"
#include "stm32f10x_exti.h"
#include "stm32f10x_usart.h"

// 定义按键引脚和外部中断线
#define BUTTON_PIN GPIO_Pin_2
#define BUTTON_PORT GPIOE
#define BUTTON_EXTI_LINE EXTI_Line2

// 定义串口1引脚和相关参数
#define USART_TX_PIN GPIO_Pin_9
#define USART_RX_PIN GPIO_Pin_10
#define USART_PORT GPIOA
#define USART USART1

// 全局变量，记录按键次数
volatile uint32_t buttonPressCount = 0;

// 函数声明
void EXTI_Configuration(void);
void USART_Configuration(void);
void USART_SendDataString(uint8_t* data);

int main(void)
{
    // 初始化外部中断
    EXTI_Configuration();

    // 初始化串口1
    USART_Configuration();

    while (1)
    {
        // 主循环中不需要做其他操作
    }
}

// （1）写出按键的外部中断初始化代码，初始化为下降沿触发中断。
void EXTI_Configuration(void)
{
    // 使能GPIOE时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOE, ENABLE);

    // 配置按键引脚为输入模式
    GPIO_InitTypeDef GPIO_InitStructure;
    GPIO_InitStructure.GPIO_Pin = BUTTON_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPD; // 下拉输入
    GPIO_Init(BUTTON_PORT, &GPIO_InitStructure);

    // 使能AFIO时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_AFIO, ENABLE);

    // 连接外部中断线到按键引脚
    GPIO_EXTILineConfig(GPIO_PortSourceGPIOE, GPIO_PinSource2);

    // 配置外部中断线为下降沿触发中断
    EXTI_InitTypeDef EXTI_InitStructure;
    EXTI_InitStructure.EXTI_Line = BUTTON_EXTI_LINE;
    EXTI_InitStructure.EXTI_Mode = EXTI_Mode_Interrupt;
    EXTI_InitStructure.EXTI_Trigger = EXTI_Trigger_Falling; // 下降沿触发
    EXTI_InitStructure.EXTI_LineCmd = ENABLE;
    EXTI_Init(&EXTI_InitStructure);

    // 使能外部中断通道
    NVIC_InitTypeDef NVIC_InitStructure;
    NVIC_InitStructure.NVIC_IRQChannel = EXTI2_IRQn;
    NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 0x02; // 抢占优先级为2
    NVIC_InitStructure.NVIC_IRQChannelSubPriority = 0x03;        // 响应优先级为3
    NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
    NVIC_Init(&NVIC_InitStructure);
}

// （2）写出串口1的初始化代码，初始化串口1的波特率为9600bps，8位数据位，1位停止位，PA9作为发送端，PA10作为接收端。
void USART_Configuration(void)
{
    // 使能GPIOA时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);

    // 使能USART1时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_USART1, ENABLE);

    // 配置USART引脚为复用功能
    GPIO_InitTypeDef GPIO_InitStructure;
    GPIO_InitStructure.GPIO_Pin = USART_TX_PIN | USART_RX_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP; // 复用推挽输出
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(USART_PORT, &GPIO_InitStructure);

    // 配置USART参数


    USART_InitTypeDef USART_InitStructure;
    USART_InitStructure.USART_BaudRate = 9600;
    USART_InitStructure.USART_WordLength = USART_WordLength_8b;
    USART_InitStructure.USART_StopBits = USART_StopBits_1;
    USART_InitStructure.USART_Parity = USART_Parity_No;
    USART_InitStructure.USART_HardwareFlowControl = USART_HardwareFlowControl_None;
    USART_InitStructure.USART_Mode = USART_Mode_Tx; // 仅发送模式
    USART_Init(USART, &USART_InitStructure);

    // 使能USART
    USART_Cmd(USART, ENABLE);
}

// （3）编写按键的外部中断服务函数，完成按键次数计数和串口1向上位机发送计数值的功能。
void EXTI2_IRQHandler(void)
{
    // 检查按键外部中断是否发生
    if (EXTI_GetITStatus(BUTTON_EXTI_LINE) != RESET)
    {
        // 延时一段时间，防止抖动
        for (volatile uint32_t i = 0; i < 100000; i++);

        // 记录按键次数
        buttonPressCount++;

        // 发送按键次数到串口
        char countStr[10];
        sprintf(countStr, "Press count: %lu\r\n", buttonPressCount);
        USART_SendDataString((uint8_t*)countStr);

        // 清除中断标志位
        EXTI_ClearITPendingBit(BUTTON_EXTI_LINE);
    }
}

void USART_SendDataString(uint8_t* data)
{
    while (*data)
    {
        USART_SendData(USART, *data++);
        while (USART_GetFlagStatus(USART, USART_FLAG_TXE) == RESET);
    }
}
```

以上代码实现了对PE2按键的外部中断响应，每次按键按下时会记录按下的次数，并通过串口1将按键次数发送给上位机的串口助手进行显示。在初始化时，外部中断被配置为下降沿触发中断，串口1被初始化为波特率为9600bps、8位数据位、1位停止位的配置。按键的外部中断服务函数中，会先进行一段延时以避免按键抖动，然后记录按键次数并将其通过串口1发送出去。

#### 采用库函数编写程序，实现定时器TIM2定时1s，每次定时中断时，通过串口1将中断次数计数值（0~99）发送给上位机的串口助手显示

采用库函数编写程序，实现定时器TIM2定时1s，每次定时中断时，通过串口1将中断次数计数值（0~99）发送给上位机的串口助手显示。要求：

（1）写出定时器TIM2的初始化程序，设置TIM2的预分频值为7199，加计数模式，使能TIM2的刷新中断，中断抢占优先级为2，响应优先级为2。
（2）写出串口1的初始化代码，初始化串口1的波特率为9600bps，8位数据位，1位停止位，PA9作为发送端，PA10作为接收端。
（3）编写TIM2的中断服务函数，完成定时通过串口1向上位机发送中断次数计数值（0~99）的功能。

下面是针对上述要求的示例代码：

```c
#include "stm32f10x.h"
#include "stm32f10x_gpio.h"
#include "stm32f10x_rcc.h"
#include "stm32f10x_usart.h"
#include "stm32f10x_tim.h"

// 定义串口1引脚和相关参数
#define USART_TX_PIN GPIO_Pin_9
#define USART_RX_PIN GPIO_Pin_10
#define USART_PORT GPIOA
#define USART USART1

// 定义定时器TIM2参数
#define TIM_PERIOD 7199
#define TIM_PRESCALER 7199

// 全局变量，记录中断次数计数值
volatile uint8_t interruptCount = 0;

// 函数声明
void TIM2_Configuration(void);
void USART_Configuration(void);
void USART_SendDataString(uint8_t* data);

int main(void)
{
    // 初始化定时器TIM2
    TIM2_Configuration();

    // 初始化串口1
    USART_Configuration();

    while (1)
    {
        // 主循环中不需要做其他操作
    }
}

// （1）写出定时器TIM2的初始化程序，设置TIM2的预分频值为7199，加计数模式，使能TIM2的刷新中断，中断抢占优先级为2，响应优先级为2。
void TIM2_Configuration(void)
{
    // 使能TIM2时钟
    RCC_APB1PeriphClockCmd(RCC_APB1Periph_TIM2, ENABLE);

    // 初始化TIM2参数
    TIM_TimeBaseInitTypeDef TIM_InitStructure;
    TIM_InitStructure.TIM_Period = TIM_PERIOD;
    TIM_InitStructure.TIM_Prescaler = TIM_PRESCALER;
    TIM_InitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
    TIM_InitStructure.TIM_CounterMode = TIM_CounterMode_Up;
    TIM_InitStructure.TIM_RepetitionCounter = 0;
    TIM_TimeBaseInit(TIM2, &TIM_InitStructure);

    // 配置TIM2中断优先级
    NVIC_InitTypeDef NVIC_InitStructure;
    NVIC_InitStructure.NVIC_IRQChannel = TIM2_IRQn;
    NVIC_InitStructure.NVIC_IRQChannelPreemptionPriority = 0x02; // 抢占优先级为2
    NVIC_InitStructure.NVIC_IRQChannelSubPriority = 0x02;        // 响应优先级为2
    NVIC_InitStructure.NVIC_IRQChannelCmd = ENABLE;
    NVIC_Init(&NVIC_InitStructure);

    // 使能TIM2更新中断
    TIM_ITConfig(TIM2, TIM_IT_Update, ENABLE);

    // 启动定时器TIM2
    TIM_Cmd(TIM2, ENABLE);
}

// （2）写出串口1的初始化代码，初始化串口1的波特率为9600bps，8位数据位，1位停止位，PA9作为发送端，PA10作为接收端。
void USART_Configuration(void)
{
    // 使能GPIOA时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);

    // 使能USART1时钟
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_USART1, ENABLE);

    // 配置USART引脚为复用功能
    GPIO_InitTypeDef GPIO_InitStructure;
    GPIO_InitStructure.GPIO_Pin = USART_TX_PIN | USART_RX_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP; // 复用推挽输出
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(USART_PORT, &GPIO_InitStructure);

    // 配置USART参数
    USART_InitTypeDef USART_InitStructure;
    USART_InitStructure.USART_BaudRate = 9600;
    USART_InitStructure.USART_WordLength = USART_WordLength_8b;
    USART_InitStructure.USART_StopBits = USART_StopBits_1;
    USART_InitStructure.USART_Parity = USART_Parity_No;
    USART_InitStructure.USART_HardwareFlowControl = USART_HardwareFlowControl_None;
    USART_InitStructure.USART_Mode = USART_Mode_Tx; // 仅

发送模式
    USART_Init(USART, &USART_InitStructure);

    // 使能USART
    USART_Cmd(USART, ENABLE);
}

// （3）编写TIM2的中断服务函数，完成定时通过串口1向上位机发送中断次数计数值（0~99）的功能。
void USART_SendDataString(uint8_t* data)
{
    while (*data)
    {
        USART_SendData(USART, *data++);
        while (USART_GetFlagStatus(USART, USART_FLAG_TXE) == RESET);
    }
}

void TIM2_IRQHandler(void)
{
    // 检查TIM2更新中断是否发生
    if (TIM_GetITStatus(TIM2, TIM_IT_Update) != RESET)
    {
        // 延时一段时间，防止按键抖动
        for (volatile uint32_t i = 0; i < 100000; i++);

        // 增加中断次数计数值
        interruptCount++;

        // 发送中断次数到串口
        char countStr[10];
        sprintf(countStr, "Interrupt count: %d\r\n", interruptCount);
        USART_SendDataString((uint8_t*)countStr);

        // 清除中断标志位
        TIM_ClearITPendingBit(TIM2, TIM_IT_Update);
    }
}
```

以上代码实现了对PE2按键的外部中断响应，每次中断发生时会记录中断次数计数值，并通过串口1将其发送给上位机的串口助手进行显示。定时器TIM2被初始化为定时1s，通过中断实现定时功能。串口1被初始化为波特率为9600bps、8位数据位、1位停止位的配置。在TIM2的中断服务函数中，会进行一段延时以防止按键抖动，然后记录中断次数计数值并通过串口1发送出去。

## 程序分析

### 题一

基于uC/OS-II操作系统的程序中，主函数及任务函数主要代码如下。分析程序并回答下列问题：

```c
int main (void)
{
    BSPInit();
    OSInit();
    OSTaskCreate(TaskLED,  (void *)0,  &TaskLEDStk[TASK_STK_SIZE - 1],  9); 
	OSTaskCreate(TaskKEY,  (void *)0,  &TaskKEYStk[TASK_STK_SIZE - 1],  10);
    OSStart();
    return 0;
}

void  TaskLED(void *pdata)            //LED控制任务
{
    INT8U err;
    sem01 = OSSemCreate(0);
    while (1)
    {
        OSSemPend(sem01,0,&err);	
		LED(1, LEDON);             
		OSTimeDlyHMSM(0, 0, 1, 0); 
		LED(1, LEDOFF);            
		OSTimeDlyHMSM(0, 0, 1, 0);
    }
} 

void  TaskKEY(void *pdata)         //按键检测任务
{   
    while (1) 
    {  
       while(KEY1!=0)	          
           {  OSTimeDly(1); }
	   OSSemPost(sem01);				        
	   while(KEY1==0)	
           { OSTimeDly(1); }   
    }    
}
```

回答下面问题：
（1）程序中任务TaskLED和TaskKEY的优先级是多少？其中优先级较高的是哪个任务?
（2）程序中任务TaskLED和TaskKEY之间采用了哪种事件通信机制？采用该事件实现的功能是资源同步还是行为同步？
（3）任务TaskLED调用OSSemPend(sem,0,&err)函数后，将进入哪种状态？满足什么条件后退出该状态？


(1) 程序中任务TaskLED的优先级为9，任务TaskKEY的优先级为10。优先级较高的任务是TaskKEY。

```c
// 通过OSTaskCreate() 的最后一个参数判断优先级
OSTaskCreate(TaskLED,  (void *)0,  &TaskLEDStk[TASK_STK_SIZE - 1],  9); // TaskLED 优先级为9
OSTaskCreate(TaskKEY,  (void *)0,  &TaskKEYStk[TASK_STK_SIZE - 1],  10); // TaskKEY 优先级为10
```

(2) 程序中任务TaskLED和TaskKEY之间采用了信号量（sem01）作为事件通信机制。该事件实现的功能是资源同步，用于TaskKEY任务向TaskLED任务发出信号。

程序中使用了信号量sem01作为事件通信机制。TaskKEY任务通过OSSemPost()函数向sem01信号量发出信号，而TaskLED任务通过OSSemPend()函数等待sem01信号量的触发。这种事件通信机制用于任务之间的同步操作

```c
void  TaskLED(void *pdata)            //LED控制任务
{
    INT8U err;
    sem01 = OSSemCreate(0);
    while (1)
    {
        OSSemPend(sem01,0,&err); // TaskLED 通过 OSSemPend() 等待 sem01 信号量的触发
		LED(1, LEDON);             
		OSTimeDlyHMSM(0, 0, 1, 0); 
		LED(1, LEDOFF);            
		OSTimeDlyHMSM(0, 0, 1, 0);
    }
} 

void  TaskKEY(void *pdata)         //按键检测任务
{   
    while (1) 
    {  
       while(KEY1!=0)	          
           {  OSTimeDly(1); }
	   OSSemPost(sem01); // TaskKEY 通过 OSSemPost() 向 sem01 信号量发出信号
	   while(KEY1==0)	
           { OSTimeDly(1); }   
    }    
}
```

(3) 任务TaskLED调用OSSemPend(sem, 0, &err)函数后，将进入等待状态（阻塞状态）。TaskLED任务将等待sem01信号量的触发，即等待TaskKEY任务通过OSSemPost()函数释放sem01信号量。当TaskKEY任务调用OSSemPost()函数释放sem01信号量后，TaskLED任务会退出等待状态，并开始执行LED控制代码。

分析

```tex
 当TaskLED任务调用OSSemPend(sem01, 0, &err)函数后，将进入等待状态（阻塞状态）。该函数的第二个参数为0，表示如果sem01信号量当前不可用，则任务会被阻塞而进入等待状态。任务会一直等待，直到sem01信号量可用或超时（在此情况下不会超时，因为第二个参数为0）。

满足以下条件之一后，TaskLED任务将退出等待状态：

    当TaskKEY任务调用OSSemPost()函数释放sem01信号量时，TaskLED任务会检测到sem01信号量可用，从而退出等待状态。
    如果TaskLED任务的阻塞期间发生了其他中断或事件，导致任务切换，则当TaskLED任务再次运行时，会重新检查sem01信号量的可用性，并根据情况决定是否退出等待状态。
```

### 题二

基于uC/OS-II操作系统的程序中，主函数及任务函数主要代码如下。分析程序并回答下列问题：

```c
int main（void）
{
OSInit();
OSTaskCreate(task1, (void *)0, &task1Stk[TASK_STK_SIZE - 1],  12 );
OSTaskCreate(task2, (void *)0, &task2Stk[TASK_STK_SIZE - 1],  9 );
OSTaskCreate(task3, (void *)0, &task3Stk[TASK_STK_SIZE - 1],  6);
OSStart();
}

void task1（）
{	
ClearScreen();                    //LCD清屏
LCD_Printf(“ task1 \n”);            //LCD显示字符串 
OSTimeDly(200);
}

void task2（）
{	
ClearScreen();
LCD_Printf(“ task2 \n”);            //LCD显示字符串
OSTimeDly(300);
}

void task3（）
{	
ClearScreen();
LCD_Printf(“ task3 \n”);            //LCD显示字符串
OSTimeDly(500);
}
```

回答下面问题：
（1）程序中三个任务task1、task2、task3的优先级分别为什么，其中优先级最高的是哪个任务？         。
（2）uC/OS-II操作系统中，按照任务的执行方式可分为哪几种类型？本程序中任务task1、task2、task3属于其中哪一种？
（3）uC/OS-II操作系统中，任务有哪几种状态？本程序中任务调用OSTimeDly( )函数后，将进入哪种状态？
（4）在LCD上的显示结果为：
第一次：                  	      第二次：                  	
第三次：                  	      第四次：                  	
第五次：                  	      第六次：                  	

(1) 程序中三个任务task1、task2、task3的优先级分别为：12、9、6。优先级数值越小，优先级越高。因此，优先级最高的任务是task3。

(2) uC/OS-II操作系统中，按照任务的执行方式可分为两种类型：抢占式任务和非抢占式任务。本程序中的任务task1、task2、task3属于非抢占式任务，因为它们在任务执行期间不会被其他优先级更高的任务打断。

(3) uC/OS-II操作系统中，任务有四种状态：就绪状态（READY）、运行状态（RUNNING）、阻塞状态（BLOCKED）和挂起状态（SUSPENDED）。本程序中，任务调用OSTimeDly()函数后，任务将进入阻塞状态。OSTimeDly()函数会使任务延迟一段指定的时间，任务在此期间将处于阻塞状态，不会被调度执行。

(4) 在LCD上的显示结果为：
第一次： task1                   	  第二次： task2
第三次： task3                   	  第四次： task1
第五次： task2                   	  第六次： task3

分析

```tex
根据程序的执行逻辑，任务task1、task2、task3依次执行，每个任务都会先清屏，然后在LCD上显示对应的任务名，并通过OSTimeDly()函数延迟一定时间。因此，首次执行时LCD上会显示"task1"，然后延迟200个时钟节拍，接着显示"task2"，再延迟300个时钟节拍，最后显示"task3"，再延迟500个时钟节拍。之后，任务会不断循环执行，按照相同的顺序在LCD上显示任务名，并延迟指定的时间。
```
