# docs contribution guide 

## Getting the source code

- Let's say your github username is Test.

- You need to fork a copy of https://github.com/radxa-docs/docs.git to your own repository.

- Download the source code

```bash
git clone https://github.com/Test/docs.git
```

## Document Catalog Framework

-  SBC

	-  Getting Started

		- Product Introduction

		- Quick Start

		- Installing the system

		- Quick Setup

		- Interface Usage Guidelines

		- Power supply options

	- Summary of resource downloads

	- Radxa OS

		- Auto Login

		- Multimedia

		- Apps

		... ...

	- Application development

		- GPIOD

		- MRAA

		- WiringX

		- QT

		- RKNN

		... ...

	- Hardware Information

		- Hardware Interface Description

	- Low-level Development

		- Install os via usb

			- Windows

			- Linux

			- MacOS

			- Clear eMMC or SPI Flash

		- U-boot

		- Kernel

		- Build System Image

	- Other-OS

		- Android

		- Windows On Arm

		... ...

	- FAQ

## 写作原则

- One document in Chinese and one in English.

- Attention to the standardization of terminology

	Different terminology has its own terminology, and the following are some examples:

		- PCIe should be written as "PCIe", not "pcie".

		- SATA should be written as "SATA", not "sata".

		- eMMC should be written as "eMMC", not "emmc".

- The product name needs to be capitalized, e.g. "Radxa ROCK 5A".

- Chinese characters are not allowed in the English part of the document

- In the Chinese section, when there is a mix of English and Chinese characters, the English characters need to be separated from the Chinese characters by a space, e.g., "This article introduces Radxa ROCK 5B related content".

- Paragraphs need to be separated by a blank line

- Each directory should have a unique README.md file as the id of the directory, and only one first level tag for the name of the directory.

- Submission considerations

	:::warning
	Try to write commit in English

	Need to [format](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/) commit

	You need to run a pre-commit before committing to check that the document conforms to the pre-commit's established format.
	:::

## How to use mdx components

### What is the point of using mdx components?

- The main reason for using mdx components is to increase the reusability of documents.

### How to use components

- mdx components are usually named with a "_" in the beginning and a "-" in the middle.

- Use the **import** keyword to refer to components.

- Use components as html tags

- Scenario:

	- There is a component named " _test-common-files.mdx" under a path, and in the file a.md, if you need to use the component "_test-common-files.mdx", the content of a.md is as follows

	- a.md file, if the "_test-common-files.mdx" component needs to be used

		```md
		import TEST from "/relative/path/of/_test-common-files.mdx"
		
		<TEST />
		```

### Component passing parameters

- **props** Keyword meaning

	```files
	The props keyword is used as a placeholder in mdx files to set up the parameters that are passed in by the md file
	```

- Example

	- There is a component named " _test-common-file.mdx" in the path of the mdx file.

		```mdx
		This document is about props.product.
		```

	- A.md in a path needs to reference the " _test-common-file.mdx" component, which looks like this
	
		``` md
		import TEST from "/relative/path/of/_test-common-file.mdx"
		
		<TEST product="Radxa ROCK 5B" />
		```
	- After compiling, the result is displayed
	
		```md
		This file is about Radxa ROCK 5B.
		```

### Use of example components

In the docs/common directory, there are several different components categorized by different categories, all of which can be reused in general

#### i2c.mdx

- Export this component

	egg.

	```md
	import I2C from '../../../../common/dev/\_i2c.mdx';
	```

- See what variables need to be passed in for this component

	If the keyword "props" does not appear in the component, then there are no variables that need to be passed into the component, but if the keyword "props" does appear, then we need to pass in the relevant variables.

	For example, by reading i2c.mdx, we need to pass in the variables "product_name i2c_overlay_name scl_pin sda_pin i2c_connection".

- Passing in variables

	What the values of the passed-in variables are, we need to look at them in context, or refer to examples where the component has already been used

	egg.

	```md
	<I2C product_name="Radxa CM3 IO" model="radxa-cm3-io" i2c_overlay_name="I2C2" sda_pin="PIN_3" scl_pin="PIN_5" i2c_connection="/img/cm3/cm3 _io_i2c-connection.webp" />
	```
