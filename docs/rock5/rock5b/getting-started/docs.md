---
sidebar_position: 9
description: "向 Radxa Docs 贡献技术文档。"
---

# docs 贡献指南 

## 获取源码

- 假设你的 github 用户名为 Test

- 你需要 fork 一份 https://github.com/radxa-docs/docs.git 到自己仓库，

- 下载源代码

```bash
git clone https://github.com/Test/docs.git
```

## 文档目录框架

-  SBC

	-  上手指南

		- 产品介绍

		- 快速上手

		- 安装系统

		- 快速设置

		- 接口使用说明

		- 电源选择

	- 资源下载汇总

	- 瑞莎系统

		- 自动登陆

		- 多媒体

		- 应用

		... ...

	- 应用开发

		- GPIOD

		- MRAA

		- WiringX

		- QT

		- RKNN

		... ...

	- 硬件信息

		- 硬件接口说明

	- 底层开发

		- 通过 USB 刷机

			- Windows

			- Linux

			- MacOS

			- 清空 eMMC 或者 SPI Flash

		- U-boot

		- Kernel

		- Build System Image

	- 其他系统

		- Android

		- Windows On Arm

		... ...

	- FAQ

## 写作原则

- 注意专业术语的规范

	不同的专业术语有它自己的专业名词， 以下举些例子：

		- PCIe 应写作 "PCIe", 而不是 "pcie"

		- SATA 应写作 "SATA"， 而不是 "sata"

		-  eMMC 应写作 "eMMC", 而不是 "emmc"

- 产品名需要大写， 如 "Radxa ROCK 5A"

- 英文部分文档不得出现中文字符

- 中文部分，当有中英文混合时，英文字符需要与中文字符隔开一各空格，如 "这篇文章介绍 Radxa ROCK 5B 相关内容"

- 段落之间需要有一个空行进行分割

- 每一个目录需要有一个唯一的 README.md 文件作为该目录的 id, 且只需要一个一级标签表示该目录的名称

- 提交需要注意的事项

	:::warning
	尽量使用英文写 commit

	需要[格式化](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/) commit

	提交之前需要运行一次 pre-commit 检查文档是否符合 pre-commit 的既定格式
	:::

## 如何使用 mdx 组件

### 使用 mdx 组件的意义

- 主要是为了提高文档的可复用性

### 如何使用组件

- mdx 组件的命名通常是以 "_" 开头，中间使用 "-" 连接各个单词

- 使用 **import** 关键字将组件引用进来

- 将组件当作一种 html 标签使用

- 情景：

	- 某路径下有一个 名为 " _test-common-file.mdx" 的组件， 在 a.md 文件中，如果需要使用 "_test-common-files.mdx" 组件

	- a.md 内容如下

		```md
		import TEST from "/relative/path/of/_test-common-file.mdx"
		
		<TEST />
		```

### 组件传参

- **props** 关键字含义

	```files
	在 mdx 文件中 props 关键字有占位符的作用，用于设置接收 md 文件传进来的参数
	```

- 示例

	- 某路径下有一个 名为 " _test-common-file.mdx" 的组件， 其内容如下

		```mdx
		这篇文件主要介绍 props.product 的相关内容
		```

	- 某路径下的 a.md 需要引用 " _test-common-file.mdx" 组件，其内容如下
	
		```md
		import TEST from "/relative/path/of/_test-common-file.mdx"
		
		<TEST product="Radxa ROCK 5B" />
		```
	- 编译之后显示效果
	
		```md
		这篇文件主要介绍 Radxa ROCK 5B 的相关内容
		```

### 示例组件的使用

在 docs/common 目录下，按照不同分类分成了几种不同的组件，这些组件基本都能够进行复用

#### i2c.mdx

- 导出该组件

	egg:

	```md
	import I2C from '../../../../common/dev/\_i2c.mdx';
	```

- 查看该组件需要传入哪些变量

	如果该组件没有出现关键字 "props", 则表明该组件没有需要传入的变量，如果出现 "props" 关键字， 则我们需要传入相关变量。

	如，通过阅读 i2c.mdx， 我们需要传入 "product_name i2c_overlay_name scl_pin sda_pin i2c_connection" 这些变量

- 传入变量

	具体传入的变量值是什么，我们需要根据上下文来看，或者参考已经使用过该组件的例子

	egg:

	```md
	<I2C product_name="Radxa CM3 IO" model="radxa-cm3-io" i2c_overlay_name="I2C2" sda_pin="PIN_3" scl_pin="PIN_5" i2c_connection="/img/cm3/cm3_io_i2c-connection.webp" />
	```
