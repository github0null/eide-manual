# 代码格式及风格

代码的格式化由 **C/C++插件** 提供的，**C/C++插件** 使用 **clang-format** 作为格式化程序

**clang-format** 在格式化源文件时，会搜索该目录下的 `.clang-format` 文件，如果发现，就会采用该文件内的格式配置

因此要想使用自定义的代码格式化风格，我们可以在**文件夹**内新建一个名为 `.clang-format` 文件，然后填写相关风格配置即可。
如果要应用到**项目的所有源文件**，在**项目根目录**下配置 `.clang-format` 文件就行了

## 格式配置示例

下面内容展示了一个基本的配置，与 **C/C++插件** 默认使用的格式配置基本一致：

还有更多的选项和字段没有列出，**clang-format** 配置字段文档：https://clang.llvm.org/docs/ClangFormatStyleOptions.html

```ini
---
BasedOnStyle: LLVM

###################################
#           缩进配置
###################################
UseTab: Never
IndentWidth: 4
TabWidth: 4
BreakBeforeBraces: Allman
ColumnLimit: 0
AccessModifierOffset: -4
NamespaceIndentation: All
FixNamespaceComments: false

###################################
#          其他样式选项
###################################

# 允许短的 if 语句保持在同一行
AllowShortIfStatementsOnASingleLine: true

# 允许短的循环保持在同一行
AllowShortLoopsOnASingleLine: true

# 缩进 case 标签
IndentCaseLabels: true

# 允许排序 #include
SortIncludes: false

```



