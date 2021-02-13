# 常用功能 🔥

## 从包中添加外设组件

> 解释：外设组件包含的内容是与此外设相关的头文件，源文件，asm 文件；添加某个外设，该外设的所有内容将会被复制到 dependence/<包名>/<外设名> 目录下，此目录会被自动加入到源文件目录列表中，同时此目录的 创建，删除，更新 由 eide 管理，但目录里的文件可以由用户随意删改

!> 注意：每当发生如下事件，某些外设组件目录里的内容将会更新，因为对于不同的工具链和不同的芯片，外设组件的内容可能有所不同

- `切换芯片型号`
- `切换工具链`

![](https://img-blog.csdnimg.cn/20200612014937405.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)
***

## 添加包含目录

> 解释：包含目录是指头文件的搜索路径，将会被直接传递给编译器

!> 注意：重复添加同一个路径将不会有任何效果出现，也不会弹出任何提示
!> 注意：keil 包组件的包含目录、已加入到项目中的源文件目录以及所有子目录、系统的包含目录，都将会被自动添加到包含路径，即使再添加也是重复的，会被丢弃，`添加包含目录` 功能 只用于添加出现在这三者之外的目录

![](https://img-blog.csdnimg.cn/20200612015716140.png)

## 查看项目所有的包含路径

> 解释：你可以通过这个功能查看当前项目所有的包含路径

![](https://img-blog.csdnimg.cn/20200612020433395.png)

下图展示了这个功能的效果

![](https://img-blog.csdnimg.cn/20200612020607959.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

> 解释：每个包含路径后都有一个标签，将以较暗的颜色显示，这个标签说明了这个路径源自何处

- `custom`：表示这个包含路径是用户手动添加的
- `build-in`：表示这是工具链内置的包含路径
- `source`：表示这个路径是从源文件目录中自动搜索到的
- `STMxxxx`：表示这个路径来自 keil 包 里安装的组件，**此标签的名字就是 keil 包的名字**

***

## 添加宏

> 解释：可以通过这个功能添加一些宏开关到项目中，这些宏开关将会被直接传递给编译器
>
> 提示：你可以一次添加多个宏，不同的宏之间必须以 “;” 作为间隔，例如: 输入 ST;DEBUG;\_RTE\_ 将会把 ST，DEBUG，\_RTE\_ 这三个宏一次性添加到项目中

!> 注意：使用 Keil_C51 工具链的 8051 项目，不能给宏添加值

![](https://img-blog.csdnimg.cn/20200612021943618.png)

