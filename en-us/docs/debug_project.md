# 调试你的程序 🔧

eide 会根据不同的烧录器自动生成相应的调试配置，你可以将其当作模板来编写自己的调试配置

## 准备工作

- 调试 ARM 的工程

  **要调试 ARM 的工程，需要安装 [cortex-debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug)**

  **关于配置 和 使用 cortex-debug 的方法，请参阅 Cortex-Debug 首页 或者 参见此博客 [Cortex-debug 使用介绍](https://discuss.em-ide.com/blog/67-cortex-debug)**

- 调试 STM8 的工程

  **要调试 STM8 的工程，需要安装 [stm8-debugger](https://marketplace.visualstudio.com/items?itemName=CL.stm8-debug)**

- 调试 8051 工程 ?

  **没有 8051 的调试器可用，因此暂不支持 8051 项目的调试**

***

## 启动调试

1. 打开烧录配置，选择好烧录器，并配置相关选项 (**eide 会根据不同的烧录器自动生成相应的调试配置**)
   
2. 打开 launch.json, 检查生成的配置是否完整，[配置方法](https://discuss.em-ide.com/blog/67-cortex-debug)

3. 点击 vscode 侧边栏的 **Debug** 图标切换到调试视图，点击调试配置下拉菜单，切换到相应的配置

  ![](./../img/open_vsc_debug_view.png)

4. 连接你的板子，在一切就绪之后，按 F5 启动调试器进入调试。

  ![](https://img-blog.csdnimg.cn/20200331222117510.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

***

## 附加调试

> cortex-debug 支持将调试器附加到正在运行的程序，这样可以跳过 gdb 在调试前将程序下载到 FLASH 的环节。
>
> 附加调试适用于程序在外部的 FLASH 中运行的场景，因为要对外扩的 FLASH 进行编程，需要使用相应的下载算法，在正常调试模式下，gdb 在调试前会先将程序下载到 FLASH，而对于外扩的 FLASH，gdb 并不知道使用何种下载算法，因此会下载失败，从而无法进入调试；而附加模式会跳过下载程序的环节，直接发送调试命令使芯片进入到调试模式，这样就能确保调试能够正常启动

1. 打开 launch.json，进行如下修改：
  
    - 将 `request` 字段的值设置为 `attach`

    - 删除 `runToMain` 字段 

2. 点击 vscode 侧边栏的 **Debug** 图标切换到调试视图，点击调试配置下拉菜单，切换到修改后的配置

3. 连接你的板子，在一切就绪之后，按 F5 启动调试器进入调试。

  本例使用 STM32H750VBT6 + 外部的 QSPI-FLASH，程序正在外部的 FLASH 中运行，PC 寄存器的值为 `0x90000a32`

  ![](../img/debug_attach.png)


!> **注意：**在调试开始前必须保证程序已正常下载到芯片，并已经开始运行，这样调试器才能正常附加到程序中









