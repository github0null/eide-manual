# 项目依赖 

## 包含目录

**添加/删除包含目录**

> 可以通过 包含目录 功能来 添加/删除 头文件的搜索路径

!> 注意：重复添加同一个路径将不会有任何效果出现，也不会弹出任何提示

![](https://img-blog.csdnimg.cn/20200612015716140.png)

**查看包含目录**

> 你可以通过这个功能查看当前项目所有的包含路径

![](https://img-blog.csdnimg.cn/20200612020433395.png)

下图展示了这个功能的效果

![](https://img-blog.csdnimg.cn/20200612020607959.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

> 每个包含路径后都有一个标签，将以较暗的颜色显示，这个标签说明了这个路径源自何处

- `custom`：表示这个包含路径是用户手动添加的
- `build-in`：表示这是工具链内置的包含路径
- `source`：表示这个路径是从源文件目录中自动搜索到的
- `STMxxxx`：表示这个路径来自 keil 包 里安装的组件，**此标签的名字就是 keil 包的名字**

***

## 库目录

可以通过添加 库目录 来指定 **静态链接库**和**链接脚本** 的搜索路径（在 gcc 系列工具链中，这种参数通常用 `-L` 参数进行指定）

!> 注意：该功能仅支持 **GCC**, **SDCC** 系列编译器，使用其他系列编译器的，请将 **静态库二进制文件（xx.a, xxx.o ...）** 直接添加到项目中

![](../img/dep_add_lib_inc.png)

***

## 宏定义

可以通过添加 宏定义 来为源文件指定 宏开关

> 提示：你可以一次添加多个宏，不同的宏之间必须以 “;” 作为间隔，例如: 输入 `ST;DEBUG;_RTE_` 将会把 `ST`，`DEBUG`，`_RTE_` 这三个宏一次性添加到项目中

![](https://img-blog.csdnimg.cn/20200612021943618.png)

!> 注意：该功能只适用于 C/C++ 源文件，**要为 ASM 汇编源文件添加宏开关，请到 '构建器选项' -> '汇编器' 中添加，汇编器宏开关格式见下方**

**汇编器**宏开关格式：

| 汇编器类型 | 格式（`<key>`为宏名称，`<value>` 为宏的值） |
|:--|:--|
| ARMCC 5/6 | `"<key> SETA <value>"` |
| ARMCC 6（asm-clang） | `<key>=<value>` |
| ARM GCC | `<key>=<value>` |
| RISCV GCC | `<key>=<value>` |
| SDCC | `<key>=<value>` |
| IAR STM8 | `<key>=<value>` |

***