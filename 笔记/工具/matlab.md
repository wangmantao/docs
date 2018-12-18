# MATLAB 学习笔记
## 学习stateflow
[stateflow教程](https://wenku.baidu.com/view/bbdf948f04a1b0717fd5dda0.html?sxts=1544972680576)
1. 创建状态
    状态元素的规则
        name
        /* 注释 */
        状态动作的关键词: 进入、退出、运行时
2. 节点
3. 转移
    通过箭头把原对象变为非活动，目标对象变为活动
    [转移添加标签]  标签书写方式：
        /*comment*/
        Event [Condition] {Condition Actions} /Transition Actions
        事件[条件]{条件动作}/转移动作
        条件动作：条件满足即执行
        转移动作：执行转移时才执行
        (动作：数学、逻辑表达式；调用函数；事件广播)
4. 默认转移 （第一个被激活的状态）
    先点默认转移图标，再点某个状态元素或节点元素。

## 灵感　
14. simulink 的实例怎么结合datasheet, 便于更了解MCU的用法
   怎么搜索PDF相关的关键词
	1. 首先快速的打开PDF 文件	
	2. 在其中搜索关键词
13. 有个库：　Rapidstm32
12. 回到windows+matlab
	matlab启动也不快
	环境都装置全了，在windows下了解STM32仿真的过程
	代码可以生成了，我直接的目的是想要控制一个Gpio
	实验方法是：
		从原示示例中复制一份GPIO项目，找出生成的代码部分
			有Driers / EWARM(ewp文件定义了库文件) / Inc / SimpleGpio /SimpleGPIO_stm32 / Src / slprj / --> for IAR 生成
			(https://blog.csdn.net/dongganxiao_maidou/article/details/64904944?locationNum=14&fps=1) --> for keil 
			-------------> (ProjectManager.TargetToolchain ioc文件定义的编译ide)

		改变新项目的cpuConfig(创新指定ioc文件), 然后重新生成代码，并在 MDK中打开
		编译并烧入F103中查看动作

11. matlab 官方的　stm hardware
	1. 为Discovery Board 安装支持包
		支持硬件和它的特性
		模块库有相应模型
		有使用Discovery Bord的例子
	2. 为Discovery Board 安装驱动

10. 砍去多余的库与工具
	* /opt/MATLAB (插件)
	3p.insert/gnuarm-armcortex.insert ---> 是arm toolchain, 将不要用它，要用/opt/arm-gcc/(高版toolchain)

9. 关于Exsamples 移到了/home/wmt/temp/test/中

6. matlab在用户模式下配置插件和toolchain
	* /root/.matlab/matlab.settings
		41行设置Add-Ons      (/home/wmt/.matlab/下设置好了，把root下的Document/MATLAB删除-->因为它转移到了opt下)
	* /root/.matlab/slhistory.settings
		6行设置toolchain
5. wmt use root pacage:
	* 硬件实现
	硬件板：    ARM Cortex-M3(QEMU)
	硬件实现：　ert.tlc       ---> 指向path? (Embeded Corder : /usr/local/MATLAB/R2018a/rtw/c/ert.tlc)
	设备供应商：ARM 兼容 type: cortex
	* 代码生成
	系统目标文件: ert.tlc
	Toolchain: GNU Tools for ARM Embeded Processors ----> 在什么文件中定义?又被定义在哪？
	......

4. STM32-MAT LINUX下不能用
	**附加功能管理器** 84
	Embedded Coder Support Package for ARM Cortex-M Processors 版本 18.1.1 
	第三方软件:
	GNU Tools for ARM Embedded Processors
	CMSIS
	**附加功能管理器** ??

	这是以下项所需要的:
	Embedded Coder Support Package for ARM **Cortex-M** Processors

	其实还有个： (for vision)
	Arm **Cortex-A** Embedded Coder Support Package


1. 嵌入式coder started
	s1: 为生成代码而配置模型
	用的不是setm32成功了．
2. 我要实现smt32f1x的matlab仿真, 然后再生成代码，然后再烧入iC，然后再用PIL仿真

3. 错误
	Error evaluating 'MaskDialog' callback of GPIO_Write block (mask) 'untitled/GPIO_Write'. Callback string is 'GPIO_Write_callback('Port_Select');' 
	未定义函数或变量 'Pin_idx'。
	No GPIO configured as output!
	
##知识点滴：
3. QEMU emulator 开源的虚拟机（此处虚拟ARM M3运行simulink的模型）
2. 关于matlab中，Target System工具包是由STM32-MAT/TARGET提供
	设定了pathtool才会有
1. 安装的问题和软件源 (在ARM笔记中)

## 资源
[Real-time workshop RTW](https://baike.baidu.com/item/Real-time%20workshop/9001254?fr=aladdin)
