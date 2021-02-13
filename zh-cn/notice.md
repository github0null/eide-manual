# 注意事项 🚩

## SDCC 编译选项

SDCC 在链接时，**被链接的第一个.rel 文件必须是含有 main() 函数的源文件生成的**，因此**必须要设置包含 main 函数的源文件名**。

**默认是 main**（即 main() 函数位于 main.c 中），如下图

![](https://img-blog.csdnimg.cn/20200327163530845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

***

## 语法提示

**v1.10.1** 及以后，对于 ARMCC 、SDCC、GCC 工具链已完成了关键字的基本扩展，不再默认关闭语法提示，如需要请手动关闭。

!> 插件**不提供**语法提示等功能，这些功能由 C/C++ 插件提供， C51/STM32 有很多标准 c/c++ 里没有的关键字，会导致 C/C++ 插件产生语法错误，你需要关闭 C/C++ 插件的错误提示。只需要保留智能提示就行。 如果你打开了工作区，插件会自动帮你关掉错误提示。

![](https://img-blog.csdnimg.cn/20200417161831638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

**如何关闭C/C++插件的错误提示**： 打开工作区文件，在 settings 中添加此项，或者直接在设置中更改, 如下图

![](https://img-blog.csdnimg.cn/20200325114206935.png)

