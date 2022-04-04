
## 准备工作

> **运行环境要求**
> 
> - `系统要求`：Windows 7 SP1 及以上 或 Linux Ubuntu
> 

!> 注意：从 **v2.9.0** 开始，构建程序的运行时已更改为 Mono 因此无需任何 .NET 环境

### Windows

Windows 版本必须是 Windows 7 SP1 及以上

### Linux (Ubuntu)

根据不同的 Ubuntu 发行版，需要提前预装 Mono 运行时

> 可参考 Mono 官方安装教程：https://www.mono-project.com/download/stable/#download-lin

#### Ubuntu 20.04 

打开 shell 终端，在其中执行如下命令添加 mono 软件源:

```shell
sudo apt install gnupg ca-certificates
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb https://apt-mirror.github0null.io/download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
```

之后，在终端中执行如下命令安装 Mono:

```shell
sudo apt install mono-devel
```

> 当下载完成后，安装过程会持续几分钟，请耐心等待

#### Ubuntu 18.04

打开 shell 终端，在其中执行如下命令添加 mono 软件源:

```shell
sudo apt install gnupg ca-certificates
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb https://apt-mirror.github0null.io/download.mono-project.com/repo/ubuntu stable-bionic main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
```

之后，在终端中执行如下命令安装 Mono:

```shell
sudo apt install mono-devel
```

> 当下载完成后，安装过程会持续几分钟，请耐心等待

#### Ubuntu 16.04

打开 shell 终端，在其中执行如下命令添加 mono 软件源:

```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
sudo apt install apt-transport-https ca-certificates
echo "deb https://apt-mirror.github0null.io/download.mono-project.com/repo/ubuntu stable-xenial main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
```

之后，在终端中执行如下命令安装 Mono:

```shell
sudo apt install mono-devel
```

> 当下载完成后，安装过程会持续几分钟，请耐心等待

***

## 安装

- Embedded IDE 是以插件的方式集成到 vscode 中的，因此首先需要在 vscode 插件商店中搜索并安装

  ![search](../img/search_eide.png)

- 插件安装完毕后，vscode 左侧活动栏会出现 Embedded IDE 的图标，点击它即可打开 Embedded IDE 的功能区域

  ![func region](../img/eide_func_region.png)

!> 注意：由于 eide 插件依赖 `ms-vscode.cpptools` 插件，因此必须保证 **cpptools 插件**正常完成加载，**否则 eide 插件将无法被激活**

***
