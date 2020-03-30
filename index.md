[EIDE](https://marketplace.visualstudio.com/items?itemName=CL.eide): A Keil C51/STM32 **project migration tool** and **IDE** with multiple toolchains. Provide development, compilation, burning, management functions for **8051**, **stm32** projects on vscode. Keil 5 version is mainly supported.

***

[toc]

***

## last update time: 2020/3/29 11:55
***

## Be sure to check the plug-in's CHANGE.LOG after each update for version changes
### [CHANGE.LOG](https://marketplace.visualstudio.com/items/CL.eide/changelog)

***
## Project directory basic structure
![directory structure](https://img-blog.csdnimg.cn/20200130134904722.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
- `.EIDE` Directory of project files and EIDE log location
- `dependence` Dependencies of project, where the content is automatically added, created, and managed by EIDE, and added by using [add-dependencies](# 从包中添加依赖项)
- `out` Default output directory, where the compiled files are stored
- `pack` ARM package installation location, the user does not need to change the contents of this folder
- `src` Directory of source files. You can add new directories to it by [add-source-dir](#添加新的源文件目录到搜索列表中)

> Other unlisted directories are not managed by EIDE, are not created by EIDE, and are managed by the developer

## Start

在开始你的项目之前，需要设置正确的 keil TOOLS.INI文件的路径， 否则**编译功能**将无法正常工作，因为插件需要使用 keil 自带的编译工具

**对于非 Keil 的工具链，设置工具链路径请前往 插件设置**

**两个路径按需求设置，如果你只需要开发 Keil_C51，那么 ARM 路径可以选择忽略；反之亦然**

- ### Keil 路径设置
	`绿色`✅：路径已完全设置完毕
	`橙色感叹号`⚠：C51 和 ARM 路径中**有一个**无效，此时点击`设置 Keil 路径`，C51 和 ARM 选项后面有一个描述：**Verified** 表示已验证的，**Invalid** 表示无效的，此描述表示了路径设置的状态，见下图
	![在这里插入图片描述](https://img-blog.csdnimg.cn/20200218114627748.png)
	`红色叉叉`❌：两个路径**都**为无效
	
***

- ### 打开项目

打开项目：可以使用操作菜单里的 **打开项目** 选项，也可以直接使用 vscode 打开**工作区文件**，建议使用**后者**；

***
	
- ### 创建和导入项目

- #### 手动创建
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200222121836922.gif)

- #### 从 Keil 5 导入

**注意：** 带有 `.uvproj` 后缀的**必须是** C51 项目，带有 `.uvprojx` 后缀的**必须是** Keil MDK 项目
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200222122221758.gif)
其中 **storageLayout** 为 RAM/ROM 布局，如果你选择了 **useCustomScatterFile**（即使用自定义的 ARM sct 文件），这个选项将被忽略


- #### 使用模板完成创建 
	> 创建一个项目是一个繁琐的过程，尤其是STM32的项目，你也许会在为各种文件夹的复制粘贴而苦恼。
	而有了模板功能，我们可以快速搭建项目的主体框架，除去那些繁琐而无意义的过程。
	插件提供的有两种选择模板的方式：从 **本地磁盘** 或 **Github 远程仓库**。
	对于 Github 方式，用户可以自由设置自己的模板仓库位置，仓库必须是公开的，插件无法访问私有的仓库
	默认的仓库位置是 [eide-doc](https://github.com/github0null/eide-doc), 作者在仓库里存放了一些简单的项目模板，以后也会不断进行添加
    ![示例](https://img-blog.csdnimg.cn/2020020817433511.gif)

***
## 安装 Keil 包组件
> 如果不想手动复制芯片的HAL库；可以通过安装 Keil 包，再安装相应外设组件完成，已安装的组件会在 `dependence` 目录中出现，内容包括此组件的需要的源文件，头文件等，这些组件都会被自动加入到编译流程

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020022212243396.gif)
***

## 编译项目
### 工具链说明 （对于非 Keil 的工具链，设置工具链路径请前往 插件设置）
#### 8051
**支持的工具链**：Keil_C51、SDCC

**注意**：插件使用的 Keil_C51 **链接器**和**汇编器**为 **LX51** 和 **AX51**，而不是 **BL51**和**A51**

***
#### ARM
**支持的工具链**：ARMCC V5、ARMCC V6

***
### 编译配置
#### 路径变量
在**编译配置**->**afterBuildTasks、beforeBuildTasks** 中可用的 **路径变量**, 变量名不区分大小写

> 变量名：${targetName}，含义：输出 hex 的文件名称
> 变量名：${exeDir}，含义：构建工具所在目录；
> 变量名：${binDir}，含义： 工具链根目录；
> 变量名：${OutDir}，含义：项目输出目录；
> 变量名：${CompileToolDir}，含义：编译工具所在目录；
> .
> 命令示例：del "${OutDir}\\*.o"，含义：删除输出目录下所有的 .o 文件
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200314130436141.png)
***

#### C51/SDCC
**v1.7.0** 以后，8051 类的编译配置也转移至 json 配置，带有悬停和补全

对于 **SDCC** 的配置，见下图：
1. 其中带有 **<>** 的选项，被 **<>** 包含的内容应该 **被替换为某个确定的值** ，见下图，如何取值见 **SDCC** 的手册
2. 当你成功替换了 **<>** 中的值，json验证器会产生警告，不用理会它，如下图
3. 悬停提示带有 **[]** 的选项，被 **[]** 包含的内容代表着此选项适用的 **设备** ，如下图

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032621351451.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
***
#### ARM
**v1.5.0** 以后，ARM 编译选项转移到 .EIDE 目录的 json 文件中，**旧版本（v1.4.0及以前）的编译配置将会失效** 如下图**划线的**；

**这些失效的配置将会在项目关闭时被清理，以后打开该项目时将不会出现。**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200316133632852.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
打开**编译配置**：点击下图 **options** 按钮打开对应的配置
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200314125025896.png)
**编译配置** 带有 **悬停提示** 和 **自动补全**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200316134804816.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

**切换工具链**：可在 **AC5** 和 **AC6** 之间切换
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200315135116101.png)
***

### 开始编译
快捷键：
 - **编译**：F6；
 - **快速编译**：F9；说明：只编译更改过的源文件

***

#### C51
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200315165539542.gif)
***

#### ARM
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200314131533560.gif)
##### 多线程编译模式（v1.6.0+）
**如果开启了多线程模式(默认开启)且编译的文件数 >= 16 时， 就会使用多线程模式完成编译，主要用于提高编译的速度；**
       
**下图是一些对比，`编译用时` 是经过多次编译后取的稳定值**

`开启前`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319163612978.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

`开启后`
![开启后](https://img-blog.csdnimg.cn/20200319163024916.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
`keil 开启后`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031916304464.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
***
## 下载到目标芯片
### C51（仅支持 STC），[stcgal 工具](https://github.com/grigorig/stcgal)
> 此工具需要 **Python3** 支持
> 在**开始**之前，需要安装 stcgal 工具
> 使用命令：**pip3 install stcgal --user** 完成安装

- STC 51 的下载配置较多，将在配置文件里进行，可以点击下图按钮打开配置（没有配置会在**EIDE**目录里创建一个新的配置文件）
**如果忽略此步骤，将使用默认配置**，默认配置见 [stcgal usage](https://github.com/grigorig/stcgal/blob/master/doc/USAGE.md)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200303140346649.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
配置文件的配置描述翻译自 [stcgal usage](https://github.com/grigorig/stcgal/blob/master/doc/USAGE.md)，带有悬停提示和自动补全
**"[]" 号**里描述了适用于此配置的芯片型号，例如：**[ALL]** 表示适用于所有型号
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200303140748914.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

- **开始烧录**；
	[stcgal 工具](https://github.com/grigorig/stcgal)用法与 STC 官方的烧录工具一样，**在面板输出 Cycling power done 之后**，需要**复位 stc 芯片**，这样才能检测到 ISP 命令，进入到下载流程；
	如果配置没有问题，下载完成之后将会退出连接，配置有错误会失败并提示，请注意阅读失败后的**提示信息**；
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020030314175653.gif)
###  ARM
**v1.8.0+** 以及之后的版本**将不会附带内置的 JLink 烧录工具**，**请到插件选项中设置 JLink 安装路径**

**在下载之前必须配置好芯片型号等设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200222122825416.gif)
***

## 导出项目
### 导出 Keil 工程
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200222124535137.gif)
### 导出 eide 模板
> 在项目视图中点击导出模板，即可将此工程打包压缩，方便重复创建，如果你想与大家分享你的模板，可以使用 pull request 提交到默认的仓库[eide-doc](https://github.com/github0null/eide-doc)

**压缩工程需要耗费一定时间，完成导出后会弹出提示**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200223123507326.png)
`默认的排除目录，导出的模板中将不会含有这些目录`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319161607901.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
***
## 串口监视器
> 在使用串口监视器前，必须设置好串口配置，见插件设置；
> 默认配置：`波特率`：9600, `位宽度`：8, `奇偶校验`：无, `停止位`：1，`模式`：Receive Mode(仅接收)

### 监视器模式
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200222134927566.png)
#### Receive Mode（接收模式，只接收，适用于日志打印）
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020022214042578.gif)

#### Send and Receive Mode（双向模式，可收发，适用于调试串口）
`下图为调试 WIFI模块 ESP-01S 的示例`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319161753567.gif)
***

## 常用选项
### 从包中添加添加要使用的依赖项
- dependence 目录用于存放已添加的依赖项；依赖项包含的内容是与此外设相关的头文件，源文件，asm 文件，被添加的依赖项都会被加入到编译过程中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200130143132377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
***
### 添加新的源文件目录到搜索列表中
- 被添加的目录的所有子目录也会被自动添加进入搜索目录，因此不必再为其子目录单独进行添加操作
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200130142239901.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
***
### 将一个源文件目录从搜索列表移除, 操作不会从磁盘删除该目录
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200130142307314.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
****
### 添加头文件目录
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200229225858257.png)

***

### 添加预编译的宏
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200130142323314.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
***
## 注意事项和常见问题
### 注意事项
#### SDCC
##### 工具链路径
SDCC 工具链路径需要在**插件选项中进行设置**

***
##### 编译选项
SDCC 在链接时，**被链接的第一个.rel 文件必须是含有 main() 函数的源文件生成的**，因此**必须要设置包含 main 函数的源文件名**，
**默认是 main**（即 main() 函数位于 main.c 中），如下图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200327163530845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

***
#### 快速编译
只编译被修改过的文件，这意味着如果仅更改了宏定义列表中的某些全局的宏开关，你必须重新进行完全编译，如果仍然进行快速编译，那么被这些宏所影响的文件**不会参加编译**，最终将不会产生预期的结果。
***
#### 语法提示
插件**不提供**语法提示等功能，这些功能由 C/C++ 插件提供， C51/STM32 有很多标准 c/c++ 里没有的关键字，会导致 C/C++ 插件产生语法错误，你需要关闭 C/C++ 插件的错误提示。只需要保留智能提示就行。 如果你打开了工作区，插件会自动帮你关掉错误提示。**如下图，__forceinline 是 ARM 特殊的关键字，在这里会导致语法错误，因此对于 STM32/C51，C/C++插件的语法提示是没有意义的，你应该关掉它**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200325113213777.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
**如何关闭C/C++插件的错误提示**： 打开工作区文件，添加此项，或者直接在设置中更改
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200325114206935.png)
***
### SDCC常见问题
#### 问题：无法加载项目
**确保设置了正确的工具链路径**

***
### C51 常见问题
#### 问题：烧录无法打开串口
这很有可能是其他程序占用了串口，引发了冲突；`解决办法`：关闭占用串口的程序重试
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200303143110142.png)
***
### STM32 常见问题
#### 问题：无法找到 "core_cm[x].h" 头文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200212161254490.png)
`解决方法`：移动到 项目视图面板->项目依赖项，点击 `修复依赖`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226000152776.png)

***
## 小技巧
### 将 hex 转换为 bin，ARM 项目已自动添加
在编译选项 ->**afterBuildTasks** 中添加下图所示命令

```json
{
	"name": "Output bin",
    "command": "\"${exeDir}\\hex2bin\" -b -c \"${outDir}\\${targetName}.hex\""
}
```
***

### 
