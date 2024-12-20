---
sidebar_position: 10
description: "Buildroot"
---

import SSDISKTOOL from "../../../common/general/\_sddisktool.mdx"

# Buildroot

## 环境准备

需要准备一台 Ubuntu 20.04/22.04 x86_64 主机。

也可以使用虚拟主机

- ubuntu-22.04.5-live-server-amd64 虚拟主机，带 120G 硬盘容量。

## 安装编译依赖包

```
sudo apt update
sudo apt install python2 git rsync gcc g++ make device-tree-compiler bc flex bison lz4 libssl-dev libgmp-dev libmpc-dev expect expect-dev file unzip bzip2 fakeroot bsdmainutils
sudo ln -s /bin/python2 /bin/python
```

## 获取 Rockchip 原始 SDK

- Mega：https://mega.nz/file/JugCGDDC#NNL5_qRDRr-NL6TS3F1FSzkoXFwRCwDTNTW3KAiTtpI
- 百度网盘：https://pan.baidu.com/s/12rQmYaRMKwgz8cOBNjc4yQ?pwd=35mj

## 解压 SDK

在 Ubuntu PC 上，使用如下命令解压 SDK。

```
tar xvf rk356x_linux5.10_rkr8_sdk.repo.tar
.repo/repo/repo  sync -l
```

## 添加板子 Zero 3E 板子支持

使用 Radxa 维护的 rockchip 仓库。

```
cd device/rockchip
git remote add radxa https://github.com/radxa/device-rockchip.git
git fetch radxa
git checkout -b rk3566_rk3568-linux-5.10 remotes/radxa/rk3566_rk3568-linux-5.10
```

使用 Radxa 维护的 kernel 仓库。

```
cd kernel
git remote add radxa https://github.com/radxa/kernel.git
git fetch radxa
git checkout -b linux-5.10-gen-rkr8-buildroot remotes/radxa/linux-5.10-gen-rkr8-buildroot
```

## 构建 SDK

在 SDK 的顶层目录，执行命令：

```
./build.sh
```

然后选中配置文件 `rockchip_rk3566_radxa_zero_3e_defconfig`。

构建完成后，将会在 `rockdev/` 目录下生成镜像。

## 使用 SDDiskTool 将生成的镜像烧录到 SDCard 中

<SSDISKTOOL />
