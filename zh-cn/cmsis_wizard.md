# CMSIS Configuration Wizard

[CMSIS Configuration Annotations](https://arm-software.github.io/CMSIS_5/Pack/html/configWizard.html) 是一种注释格式，用于结构化地描述内含大量宏定义头文件

通过一定的工具对其进行解析，可以生成 GUI 配置向导，方便用户查看和修改头文件中的配置

Keil上效果如下（截图来自官网）：

![](../img/cmsis_wizard.png)

***

## 用法

目前 eide 上也集成了该功能，使用起来也十分简单。

1. 打开 **带有 CMSIS Configuration Annotations 格式** 的头文件，右键菜单选择 CMSIS Configuration Wizard 即可打开
   
   !> **不带有 CMSIS Configuration Annotations 格式** 的头文件，**无法使用该功能，并且工具不会弹出任何提示**

   ![](../img/open_cmsis_header.png)

2. CMSIS Configuration Wizard 配置 UI 会以一个新的页面打开，修改相应配置，按下 `Save All` 或者 `ctrl+s` 即可保存
   
   ![](../img/cmsis_wizard_preview.png)
   
   选中相应的配置项，点击 `Open Header`，即可跳转至相应的行

   ![](../img/cmsis_wizard_jump.png)

***

## 细节

本配置向导的功能细节参考 keil 中的实现，并没有完全实现 [CMSIS Configuration Annotations](https://arm-software.github.io/CMSIS_5/Pack/html/configWizard.html) 中的所有语法

**目前未实现的语法如下：**

1. 数组类型 
   
   ![](../img/cmsis_no_impl/array.png)

2. 以 `..` 作为分隔符的 Modifier

   ![](../img/cmsis_no_impl/modifier.png)

3. 数字的格式化显示功能

   ![](../img/cmsis_no_impl/format.png)

**注意事项：**

1. 对于 string 类型的宏定义，宏定义的值**必须为一个正常的字符串**，如下图：

   ![](../img/cmsis_no_impl/string.png)

   **不得为**任何其他的宏定义或者表达式，例如：

   ```cpp
   // <s> APP_USBD_STRINGS_LANGIDS - Supported languages identifiers.
   // <i> Note: This value is not editable in Configuration Wizard.
   // <i> Comma-separated list of supported languages.
   #ifndef APP_USBD_STRINGS_LANGIDS
   #define APP_USBD_STRINGS_LANGIDS APP_USBD_LANG_AND_SUBLANG(APP_USBD_LANG_ENGLISH, APP_USBD_SUBLANG_ENGLISH_US)
   #endif
   ```


