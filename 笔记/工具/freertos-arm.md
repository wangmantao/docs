# FreeRTOS & ARM 用法 (主要Linux下的STM32开发方法)
## 资源

1. [stm社区](http://www.stmcu.org.cn/)(下载快)
2. st官方注册: wangmantao@163.com st456321 you mother's name? hmh
3. **Matalb 相关部分转移 st matlab**
-	 [matlab 配置](https://alpha-ss.sohu.com/infonews/article/6345903537284710401) 
	matlab重下载（安装）
-	[安装教程和资源](https://www.macxin.com/archives/4722.html)
	This error occurs when your computer cannot load a certain font display library through MATLAB. 
	mv /usr/local/MATLAB/R2018b/bin/glnxa64/libfreetype* exclude/
-	[Consolas YaHei hybrid.ttf](https://www.cnblogs.com/Qling/p/9487647.html)matlab字体
-	[Matlab&Simulink开发STM32F4](https://blog.csdn.net/sky_in_my_mind/article/details/51194635)
4. 
## 灵感

18. simulink代码生成位置
17. 定下目标：仿真gpio, 实现gpio
	












16. matlab的嵌入式的用法demo 
	arm_cortex_m_gettingstarted 编译通过有diagnostics日志

15. Matlab 嵌入式ARM支持包放在/root/Document
	file:///root/Documents/MATLAB/SupportPackages/R2018a/help/supportpkg/armcortexm/index.html

14. 多重arm-gcc 工具链
	(两个工具链差不多，待熟悉后删除一个，留下哪个待定)
	1. /opt/gcc-arm/bin/arm-none-eabi-gcc (最新，由gdb.pdf为证)
	2. /root/Documents/MATLAB/SupportPackages/R2018a/3P.instrset/gnuarm-armcortex.instrset/gcc-arm-none-eabi-5_2-2015q4/bin/arm-none-eabi-gcc

13. 多重stm32Cube库
	(两个位置的库暂留，待统一再删除不常用的)
	1. /home/wmt/STM32Cube/Repository/
	2. /opt/STM32Cube

12. stm32开发with Matlab
-	[STM32-MAT](https://www.st.com/en/development-tools/stm32-mat-target.html)
	1. 在matlab中集成stm32-mat
		cmd: pathtool (matlab search path)
	2. 存储pathdef.m ->　matlab目录
	2. 新建model
		配置参数：code generation -> System target: stm32.tlc
		先择setm32.tlc -> ok后，却出现了：
			警告：请把stm32包添加到Matlab的default路径中，用toolpath命令．
		设置stm32cubeMx的安装路径：/usr/local/STMicroelectronics/STM32Cube/STM32CubeMX
		Error: 执行PostApplyCallback of the target stm32.tlc:路径没有找到．
	 
11. stm32流程
	(1)烧写程序 
		st-flash write a.bin 0x8000000
	(2)编写.gdbinit
	(2)开启openocd server
		openocd -f interface/stlink-v2.cfg -f target/stm32f4x_stlink.cfg
	(3)开启gdb
		arm-none-eabi-gdb uart.elf	
10. 列出一些openocd的基本用法，并实验
<<OpenOCD User’s Guide >> 放在本地文摘中"openocd_debug.pdf" [网络](http://openocd.org/doc/pdf/openocd.pdf)
	Open On-Chip Debugger:  for release 0.10.0+dev 19 November 2018

1. 在demo stm32中，学会怎么设置项目的make
2. 想办法提出make文件（keil的），然后移植到linux下Make
3. [stm32-cmake](https://github.com/ObKo/stm32-cmake) 学习笔记见 st cmake
4. [A demo project of FreeRTOS running on a STM32F4 Discovery board.](https://github.com/wangyeee/STM32F4-FreeRTOS) (利用现存的的例子，结合以上cmake工具)
5. 利用以上freeRTOS项目剖析并对照<<stm32>>书，和以上第３项cmake
	目的是编译这个项目没错，这个项目的东西，在CMAKE中是怎么对应的；并可以理解各部分的作用．
	编译　STM32F4-FreeRTOS-> 只需编辑makefile设定编译器的路径．-> make
6. openocd 不能运行
　Can't find openocd.cfg
7. 6项不行，从官网软件突破jlink for linux 
	有两份文档(JLink JFlash)已经下载(在文摘中)
-	rpm软件　[JLink_Linux_x86_64.rpm](https://www.segger.com/downloads/jlink/JLink_Linux_x86_64.rpm)
	安装之后，知识点滴13
	  		
8. 要转CMSIS-DAP OPENOCD [那些事][https://blog.csdn.net/m454078356/article/details/78986205]

9. 野火CMSIS-DAP, 给的openOCD
  https://zhidao.baidu.com/question/1047512972598364779.html?spm=a1z09.2.0.0.393b2e8djKSl0A
[ARM官方][https://os.mbed.com/handbook/CMSIS-DAP]

10. 第８项＂那些事＂提到了一个配置文件ocd-stm32.cfg ---它是一个脚本
	它指定了interface和transport (界面卡和传输端口)
		cmsis-dap	jtag
	再指source(源)为target/stm32f1x.cfg ---它是一个脚本

## 知识点滴
17. grt.tcl ert.tcl 区别
	grt.tcl general 一般用来做sil测试，看生成软件的架构功能正确性
	ert.tcl embeded 针对器件对代码优化 
16. 启动openocd　server
	openocd -f interface/stlink-v2.cfg -f target/stm32f4x_stlink.cfg
15. stlink-v2 : 0483:3748
14. st-link v2 连接OPENOCD与STM32
	
13. J-link 软件结构 --所买野火不支持　(将不会用jlink,要把这些删除)
	cat /etc/udev/rules.d/99-jlink.rules
	tree /opt/SEGGER/JLink	
	ll usr/bin/J*
	locate jlink (可看到stm32 用到jlink的demo)
12. FreeRTOSConfig.h
	rtos下的示例子项目，对这个文件的配置可能不相同

11. FreeRTOS API的利用 p80 子项目：rtos/blinky2(rtos子目录有很多可以学)
	make clobber & make & make flash

10. FreeRTOS (以下的概念须了解)
	• Multi-tasking and scheduling
	• Message queues
	• Semaphores and mutexes
	• Timers
	• Event groups

9. GPIO API
	#include <libopencm3/stm32/rcc.h>
	#include <libopencm3/stm32/gpio.h> 

8. make flash
	在子项目中也可以这样，当前的BIN文件烧入FLAS8. make flash

7. objcopy -Obinary 
	把可执行的elf文件转成img文件（bin文件）-> to flash

6. 在子文件夹中也可以make
	产生了elf bin文件
	elf文件是可执行文件，
	arm-none-eabi-objcopy -Obinary miniblink.elf miniblink.bin

5. make clobber 
	是把上一次make命令生成的文件或目录清除掉,效果比make clean更严格。
	清除之后，只剩下一个c文件和Makefile


1. Project.mk STM32项目中rtos子目录中
	改变FREERTOS 对应的版本号(目录)
	目的让make file可以正确的工作
2. Makefile.incl
	PREFIX ?= arm-none-eabi
	为gcc设定正确的前缀
3. make命令
	执行build
4. st-flash (write / read / erase)
	执行烧写
	st-flash write a.bin 0x8000000

