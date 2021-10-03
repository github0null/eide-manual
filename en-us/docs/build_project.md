# Build Project 🔨

> Click <img width="16px" bor src="../img/build.svg"> button to start build

## Toolbar

> 这里有几个常用的工具按钮：**编译**，**清理**，**重新编译**，**烧录**，它们的含义如下
> 
> ![](../img/prj_toolbar.png)

- **编译 <img width="16px" bor src="../img/build.svg">**: 增量构建，只编译更改过的文件
  
- **清理 <img width="16px" bor src="../img/clean.svg">**: 删除 `build` 目录下的所有内容
  
- **重新编译 <img width="16px" bor src="../img/rebuild.svg">**: 重新编译整个项目

- **烧录 <img width="16px" bor src="../img/download.svg">**: 执行烧录命令，将程序烧录到芯片

***

## 操作展示

### C51 项目

> 使用 SDCC 工具链编译

![sdcc build](../img/sdcc_build.gif)

### STM8 项目

> 使用 SDCC 工具链编译

![stm8 build](../img/stm8_build.gif)

### Cortex-M 项目

> 使用 ARMCC 工具链编译

![armcc build](../img/armcc_build.gif)
