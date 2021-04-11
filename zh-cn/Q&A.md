# 常见问题 ❓

## 问题：插件无法启动

**问题详情**：

 打开 eide 侧边栏，发现 Operations 为空，无法进行相关操作

> 原因：windows 某些环境不正常, 或者插件的某些依赖项未安装，导致插件无法激活

**解决办法**：

 按以下步骤操作：

 1. 打开输出面板，选择 日志（扩展宿主）
   
 2. ctrl+f 在日志里搜索 eide, 复制相关的错误日志
 
 3. 将日志内容发送到论坛，并 @admin

***

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
