# 注意事项 🚩

## SDCC 编译选项

SDCC 在链接时，**被链接的第一个.rel 文件必须是含有 main() 函数的源文件生成的**，因此**必须要设置包含 main 函数的源文件名**。

**默认是 main**（即 main() 函数位于 main.c 中），如下图

![](https://img-blog.csdnimg.cn/20200327163530845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

***

## 语法检查，补全，高亮

> 语法检查，补全，高亮 这些功能由 C/C++ 插件提供，eide 只负责为 C/C++ 插件生成配置
