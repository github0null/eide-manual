# 常见问题 ❓

## 问题：编译不通过

> 提示：请仔细阅读编译器给出的输出提示，将错误提示放到网络上查询，无法解决的，可通过 github issue 进行反馈

***

## 问题：SDCC 编译提示未定义的段

问题详情：

 使用 SDCC 编译 8051 项目，链接时出现以下提示：

 ```
 ASlink-Warning-No definition of area HOME
 ASlink-Warning-No definition of area XSEG
 ASlink-Warning-No definition of area PSEG
 ```

> 可能原因：SDCC 版本过低；`解决办法`：卸载旧版本，安装最新的 SDCC 之后重试

***

## 问题：安装了 stcgal 但启动下载时提示无法找到 stcgal 模块

> 原因：电脑上有多个 Python；`解决办法`：卸载多余的 python，删除环境变量 path 中多余的 python 路径，重启 vscode 后重试

***

## 问题：使用 Keil_C51 编译时链接失败,  提示 Error L257

问题截图：

![](https://img-blog.csdnimg.cn/20200506211039857.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

> 原因：Keil C51 未破解，存在大小限制，`解决办法`: 完全破解 Keil C51 后再尝试
