# 烧录程序到目标芯片 💾

## C51 工程

### 使用 stcgal 烧录

#### 安装

> 1. 安装 **Python3**
>
> 2. 安装 **stcgal** 模块, 命令：`pip3 install stcgal --user`

#### 用法

STC 的下载配置较多，将在配置文件里进行，可以点击下图按钮打开配置

**如果忽略此步骤，将使用默认配置**，默认配置见 [stcgal usage](https://github.com/grigorig/stcgal/blob/master/doc/USAGE.md)

![](https://img-blog.csdnimg.cn/20201204182929347.png)

配置文件的配置描述翻译自 [stcgal usage](https://github.com/grigorig/stcgal/blob/master/doc/USAGE.md)，带有悬停提示和自动补全

**"[]" 号**里描述了适用于此配置的芯片型号，例如：**\[ALL\]** 表示适用于所有型号

![](https://img-blog.csdnimg.cn/20200303140748914.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

!> 注意：stcgal 用法与 STC 官方的烧录工具一样，在面板输出 **Cycling power done** 之后，需要**复位 stc 芯片 或者 关闭然后打开芯片电源**，这样芯片才能检测到 ISP 命令，进入到下载流程

### 使用 stcflash 烧录

#### 安装

> 1. 安装 **Python3**
> 
> 2. 安装 **pyserial** 模块, 命令：`pip3 install pyserial --user`
> 
> 3. 下载 [stcflash.py](https://github.com/sms-wyt/stcflash/blob/master/stcflash.py), **并复制到项目的目录下**，快捷下载地址：https://cloud.em-ide.com/s/R4SY?path=%2F%E7%83%A7%E5%BD%95%E5%B7%A5%E5%85%B7

#### 用法

- 首点击切换烧录工具到 Custom, 如下图

  ![](../img/uploader_cus.png)

- 之后修改 `命令行` 属性，填写 stcflash 的烧录命令, 示例命令如下：
  
  `python ./tools/stcflash.py -p COM23 "${hexFile}"`

- 点击下载按钮，开始烧录

- 命令行会提示正在检测芯片，这时需要复位芯片，才能进入到下载流程

!> 注意：stcflash 支持的芯片型号有限，不能保证全系列支持

***

## STM8 工程

> 烧录 STM8 工程需要先安装 STVP，官方下载地址：https://www.st.com/zh/development-tools/stvp-stm8.html
> 
> STVP 精简版下载地址：https://cloud.em-ide.com/s/R4SY?path=%2F%E7%83%A7%E5%BD%95%E5%B7%A5%E5%85%B7

安装完成之后需要在 eide 插件设置中设置 `STVP_CmdLine.exe` 的绝对路径

打开 vscode 设置，搜索栏输入：`EIDE.STM8.STVP.CliExePath`, 搜索到 STVP 设置后，将路径填写到其中即可

![](../img/stvp_setting.png)

STVP 工具配置界面如图

![](https://img-blog.csdnimg.cn/2020120418415026.png)

!> **注意：** 如果需要设置选项字节以开启相关外设，请打开 STVP 完成选项字节的配置，然后生成为 hex 或 bin 文件，将此文件路径添加到项目的 STVP 烧录设置: `选项字节文件路径` 中

在修改好配置之后，连接好 STLink，点击下载按钮开始下载

![](https://img-blog.csdnimg.cn/20201204184429743.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

***

## 使用自定义命令行烧录

> 如果你想使用支持命令行的其他烧录程序，你可以使用 `自定义shell命令` 来进行烧录

首点击切换烧录工具到 Custom, 如下图

![](../img/uploader_cus.png)

之后修改 `命令行` 属性，填写你要使用的烧录工具的相应的命令即可

命令行中所需要的 `hex/bin 文件路径` 可以由变量 `${programFile}` 或 `${hexFile}` 进行替换, 例如：

```bash
NuLink.exe -w APROM "${hexFile}"
```

***

## ARM 工程

eide 支持主流的 4 种烧录工具

![](./../img/flasher_list.png)

### 使用 JLink 烧录程序

> 要使用 JLink, 必须先安装 JLink 软件，并且 JLink 软件的版本必须在 V6.50 及以上
> 
> JLink_V650 下载地址：https://www.segger.com/downloads/jlink/JLink_Windows_V650.exe

安装完之后，打开 vscode 设置，在搜索栏输入：`EIDE.ARM.JLink.ToolDirectory`

搜索到 JLink 设置后，将 JLink 安装目录位置填写到输入框内即可完成 JLink 路径设置

![](../img/jlink_setting.png)

之后打开 eide 项目的 “烧录配置” 栏，切换到 JLink，进行配置

配置完毕之后，即可点击 “下载程序” 按钮进行烧录

![](../img/jlink_flash_conf.png)

### 使用 STLink 烧录程序

> 要使用 STLink, 必须先安装 STLink Utility 软件
> 
> STLink Utility 官方下载地址：https://www.st.com/zh/development-tools/stsw-link004.html
>
> 共享下载地址：https://cloud.em-ide.com/s/R4SY?path=%2F%E7%83%A7%E5%BD%95%E5%B7%A5%E5%85%B7

安装完之后，打开 vscode 设置，在搜索栏输入：`EIDE.ARM.StlinkExePath`

搜索到 STLink 设置后，**在 STLink Utility 安装目录中找到 `STLink_CLI.exe` 的位置**，并将其填写到输入框内即可完成 STLink 路径设置

![](../img/stlink_setting.png)

之后打开 eide 项目的 “烧录配置” 栏，切换到 STLink，进行配置

配置完毕之后，即可点击 “下载程序” 按钮进行烧录

![](../img/stlink_flasher_conf.png)

### 使用 pyocd 烧录程序

> 注意：pyocd 需要 python3 支持，必须先安装 python3
>
> pyocd 主要被用来支持 DAPLink 和 STLink

1. 命令行输入 `pip3 install pyocd` 安装 pyocd

2. 从 github 下载 [usblib](https://github.com/libusb/libusb/releases/tag/v1.0.21)

 **解压 usblib 后，将 libusb.dll 复制到 python.exe 所在的目录，注意：所选择的 libusb.dll 必须要和电脑上安装的 python 是同一体系结构，例如：python3_x86 版本对应 MS32 目录下的 dll**

 ![](https://img-blog.csdnimg.cn/20200707213346603.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

3. 连接 目标板，命令行输入 `pyocd list` 检查 pyocd 是否能够正常工作，如果没有问题则会输出已连接的设备列表

 ![](https://img-blog.csdnimg.cn/20200707213951601.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

4. 打开 EIDE 项目，配置烧录设置
   
   - 填写目标芯片名称

     ![](https://img-blog.csdnimg.cn/20200707214308226.png)

   - 命令行输入 `pyocd list -t`，查看内置支持的芯片，如果上一步填写的芯片名存在，**则可以跳过后续步骤**，否则继续下一步

     ![](https://img-blog.csdnimg.cn/2020070721482367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

   - 打开 config 属性，**配置包含该芯片的 keil 包路径 (如果完整的 keil 包太大，可以用简化版的, 仓库地址: https://cloud.em-ide.com/s/R4SY?path=%2Fpyocd%20%E8%8A%AF%E7%89%87%E5%8C%85)**

     提示：此配置文件里也可以填写一些其他的 pyocd 配置选项，具体参考 [pyocd 配置文档](https://github.com/pyocd/pyOCD/tree/master/docs)**

     ![](https://img-blog.csdnimg.cn/20200707215417409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

5. 连接目标板，点击下载按钮启动下载

 ![](https://img-blog.csdnimg.cn/20200707215605884.png)

***

### 使用 OpenOCD 烧录程序

> OpenOCD-v0.10.0 下载地址：https://cloud.em-ide.com/s/R4SY?path=%2F%E7%83%A7%E5%BD%95%E5%B7%A5%E5%85%B7

1. 打开设置搜索：`EIDE.ARM.OpenOCD.ExePath`, 设置好 OpenOCD.exe 的路径

 ![](../img/openocd_conf.png)

2. 将烧录配置切换到 OpenOCD，设置 `target` 和 `interface`。

 !> **注意：** eide 将从 <OpenOCD安装目录>/scripts/target 和 <OpenOCD安装目录>/scripts/interface 目录读取配置文件列表，**如果 openOCD.exe 路径是无效的，可选的列表将为空**

 ![](https://img-blog.csdnimg.cn/20200714121238782.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

3. 点击下载按钮完成下载

 ![](https://img-blog.csdnimg.cn/20200714121616638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

