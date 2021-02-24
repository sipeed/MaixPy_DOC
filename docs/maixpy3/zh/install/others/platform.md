---
title: 如何适配你的平台
keywords: MaixPy, MaixPy3, Python, Python3, MicroPython
desc: maixpy doc: 如何适配你的平台
--- 

> 前文交待了如何编译和开发的基本方法和开发上的一些观念认知，但对于项目的架构结构上的还未说明。

用户有一台计算机，恰好安装了 Python3 和 pip ，所以想试试安装 MaixPy3 来开始编程之旅。

但是会发现无法使用 `pip install maixpy3` 来安装 MaixPy3 ，它会提示一些错误并告诉包无法安装。

这是因为用户所在的系统平台下没有相应的开发依赖和编译环境，无法完成该环境下 MaixPy3 的编译安装。

接下来就以 Linux 系统为例，说说 MaixPy3 是如何适配芯片平台的？要适配的模块可以是哪些？这个开发移植的过程又是怎样的？

## 有哪些需要了解的内容？

待补充

## 准备一个 Python3 解释器

可以忽略在 x86_64 机器上的移植问题。

解决交叉编译的问题，什么是交叉编译？

如果是嵌入式 arm linux 平台，以 rv1126 为例，需要先提取目标平台的交叉编译链。

要适配某个 Linux 芯片平台的 Python 解释器，它需要准备如下基础环境：

目标编译器与目标机器的依赖文件与目录。

## 以 Maix 包为公共包入口

待补充

### Python3 与 MaixPy3 的不同表现

MaixPy3 是 Python3 的一个环境包，它不仅是自身的安装包，还依赖多个外部包，这也就意味着，不同平台会有不同的依赖包。

### MaixPy3 的项目结构

项目的各目录功能描述。

- [docs](https://github.com/sipeed/MaixPy3/blob/main/docs/) [ 存放一些通用的开发文档 ]
- [envs](https://github.com/sipeed/MaixPy3/blob/main/envs/) [ 存放不同平台的编译配置 ]
- [examples](https://github.com/sipeed/MaixPy3/blob/main/examples/) [ 存放不同平台的示例或应用 ]
- [ext_modules](https://github.com/sipeed/MaixPy3/blob/main/ext_modules/) [ 存放需要编译的项目模块 ]
- [maix](https://github.com/sipeed/MaixPy3/blob/main/maix/) [ 提供 maix 入口 Python 模块 ]
- [tests](https://github.com/sipeed/MaixPy3/blob/main/tests/) [ 提供 tox 的通用测试项目 ]
- [setup.py](https://github.com/sipeed/MaixPy3/blob/main/setup.py) [ MaixPy3 项目编译入口 ]

如果你想要提交其他平台的配置，参考如下：

- [general.py](https://github.com/sipeed/MaixPy3/blob/main/envs/general.py)
- [maix_v831.py](https://github.com/sipeed/MaixPy3/blob/main/envs/maix_v831.py)

```python

_maix_modules = [
    libi2c_module,
]

_maix_data_files = [
    ('/maix', get_srcs(ext_so, ['so'， 'ko'])),
]

_maix_py_modules = [
    "numpy",
]

```

如果你想要提交一些需要编译的 Python 编译 C 的模块，推荐使用子仓库导入，参考如下：

- [_maix](https://github.com/sipeed/MaixPy3/blob/main/ext_modules/_maix)
- [_maix_nn](https://github.com/sipeed/MaixPy3/blob/main/ext_modules/_maix_nn)
- [libi2c](https://github.com/sipeed/MaixPy3/blob/main/ext_modules/libi2c)

更多内容就去看仓库吧。