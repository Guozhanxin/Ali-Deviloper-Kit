# STM32L496 Ali Develoeprkit BSP 说明

## 简介

本文档为 RT-Thread 开发团队为 STM32L496 Ali Developer Kit 提供的 BSP (板级支持包) 说明。

主要内容如下：

- 开发板资源介绍
- BSP 快速上手
- 进阶使用方法

通过阅读快速上手章节开发者可以快速地上手该 BSP，将 RT-Thread 运行在开发板上。在进阶使用指南章节，将会介绍更多高级功能，帮助开发者利用 RT-Thread 驱动更多板载资源。

## 开发板介绍

Developer Kit STM32L496 是阿里联合[诺行](http://www.notioni.com/)推出的一款基于 ARM Cortex-M4 内核的开发板，最高主频为 80Mhz，该开发板具有丰富的板载资源，可以充分发挥 STM32L496 的芯片性能。

开发板外观如下图所示：

![board](figures/board.png)

该开发板常用 **板载资源** 如下：

- MCU：STM32L496VGT6 ，主频 80MHz，1MB FLASH ，320KB RAM
- 常用外设
  - LED灯：3个
  - 按键：3个，A（PE11），M（PE14），B（PE10）
  - 光环境传感器：1个
  - 六轴传感器：1个
  - 磁力计：1个
  - 压力传感器：1个
  - 高性能音频解码芯片：1个
  - 温湿度传感器（SHTC1）：1个
  - TFTLCD 显示屏：1个
  - WIFI 模块（BK7231）：1个
  - 板载 ST LINK V2.1 功能
- 常用接口：SD 卡接口、USB OTG Micro USB 接口
- 调试接口，ST-LINK Micro USB 接口

开发板更多详细信息请参考阿里 [开发板硬件介绍](https://github.com/alibaba/AliOS-Things/wiki/AliOS-Things-Developer-Kit-Hardware-Guide)。

## 外设支持

本 BSP 目前对外设的支持情况如下：

| **板载外设**        | **支持情况** | **备注**                              |
| :------------------ | :----------: | :------------------------------------ |
| 板载 ST-LINK 转串口 |     支持     | lpuart1                               |
| SD卡                |     支持     |                                       |
| 温湿度传感器        |   暂不支持   | 即将支持                              |
| 六轴传感器          |     支持     |                                       |
| 光环境传感器        |   暂不支持   | 即将支持                              |
| 音频解码            |    不支持    |                                       |
| TFTLCD              |    不支持    |                                       |
| WIFI                |    不支持    |                                       |
| **片上外设**        | **支持情况** | **备注**                              |
| GPIO                |     支持     | PA0, PA1... PI15 ---> PIN: 0, 1...144 |
| UART                |     支持     | LPUART1,UART2/3                       |
| SPI                 |     支持     | SPI1/2                                |
| QSPI                |    不支持    |                                       |
| I2C                 |     支持     | 软件 I2C 2/3/4                        |
| TIM                 |     支持     | TIM15/16/17                           |
| ADC                 |     支持     | ADC1                                  |
| RTC                 |     支持     | 支持外部晶振和内部低速时钟            |
| WDT                 |     支持     |                                       |
| PWM                 |     支持     | PWM3                                  |
| USB Device          |     支持     |                                       |
| USB Host            |   暂不支持   |                                       |
| **扩展模块**        | **支持情况** | **备注**                              |

## 使用说明

使用说明分为如下两个章节：

- 快速上手

    本章节是为刚接触 RT-Thread 的新手准备的使用说明，遵循简单的步骤即可将 RT-Thread 操作系统运行在该开发板上，看到实验效果 。

- 进阶使用

    本章节是为需要在 RT-Thread 操作系统上使用更多开发板资源的开发者准备的。通过使用 ENV 工具对 BSP 进行配置，可以开启更多板载资源，实现更多高级功能。


### 快速上手

本 BSP 为开发者提供 MDK5 和 IAR 工程，并且支持 GCC 开发环境。下面以 MDK5 开发环境为例，介绍如何将系统运行起来。

#### 硬件连接

使用数据线连接开发板到 PC，打开电源开关。

#### 编译下载

双击 project.uvprojx 文件，打开 MDK5 工程，编译并下载程序到开发板。

> 工程默认配置使用板载 ST-LINK 下载程序，只需一根 USB 线连接开发板，点击下载按钮即可下载程序到开发板

#### 运行结果

下载程序成功之后，系统会自动运行，观察开发板上 LED 的运行效果，红色 LED 会周期性闪烁。

连接开发板对应串口到 PC , 在终端工具里打开相应的串口（115200-8-1-N），复位设备后，可以看到 RT-Thread 的输出信息:


```bash
 \ | /
- RT -     Thread Operating System
 / | \     3.1.1 build Nov 19 2018
 2006 - 2018 Copyright by rt-thread team
msh >
```
### 进阶使用

此 BSP 默认只开启了 GPIO 和 低功耗串口1 的功能，如果需使用 SD 卡等更多高级功能，需要利用 ENV 工具对BSP 进行配置，步骤如下：

1. 在 bsp 下打开 env 工具。

2. 输入`menuconfig`命令配置工程，配置好之后保存退出。

3. 输入`pkgs --update`命令更新软件包。

4. 输入`scons --target=mdk5/iar` 命令重新生成工程。

本章节更多详细的介绍请参考 [STM32 系列 BSP 外设驱动使用教程](../docs/STM32系列BSP外设驱动使用教程.md)。

## 注意事项

暂无

## 联系人信息

维护人:

- [guozhanxin](https://github.com/guozhanxin)