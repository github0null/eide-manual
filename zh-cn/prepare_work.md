# 准备工作

## 运行环境

`系统要求`：Windows 7 及以上

`.NET环境`：.NET FrameWork 3.5

> 提示：.NET FrameWork 4 及以上可能不兼容 .NET FrameWork 3 的程序。 如果构建工具无法启动，可能需要单独安装一下 .NET FrameWork 3.5

## 设置工具链的路径

由于各种编译器的体积过大，不适合与扩展打包到一起，因此你必须手动安装你要使用的编译器工具，然后在 `设置工具链路径` 选项中设置其安装路径

> 注：只需设置你要使用的编译工具的安装路径，不使用的可以不设置；如果你打算使用某种工具链来编译你的项目，但没有为其设置安装路径，插件会给出提示

**"设置工具链路径"** 选项的图标表明了路径设置的状态
 - `绿色`✔：所有的工具链已完全设置完毕
 - `橙色感叹号`⚠：某一个工具链路径是无效的
 - `红色叉`❌：还没有设置任何工具链路径

![](https://img-blog.csdnimg.cn/20200730115319837.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

## 了解项目目录结构 📚

基本结构如下：

![](https://img-blog.csdnimg.cn/20200825104645802.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODMzODEw,size_16,color_FFFFFF,t_70)

- `.eide` eide 项目文件, 项目依赖 和 日志存放的位置
- `.vscode` vscode 配置文件目录
- `out` EIDE 的默认编译输出目录, 编译产生的文件存放在此处，可以在项目的 `其他设置` 里进行修改
- `pack`  CMSIS 包的安装位置, 用户无需更改此文件夹下的内容
- `src` 默认的源文件的目录, 也可以通过 [添加源文件目录](#添加源文件目录) 来添加其他的目录
- `*.code-workspace` vscode 工作区文件，每个 eide 项目都存在此文件，不要删除此文件
