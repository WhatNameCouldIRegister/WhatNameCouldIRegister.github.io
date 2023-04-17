---
layout: post
read_time: true
show_date: true
title:  cmake\make\makefile 整理
date:   2021-01-25 13:32:20 -0600
description: cpp模板常见混淆点做一个自我区分
img: posts/20230223/swans.jpg
tags: [cmake]
author: DD
mathjax: yes
---

文章结构参考自： https://zhuanlan.zhihu.com/p/111110992
## gcc

- GNU Compiler Collection (GNU编译套件)，可以直接理解成编译器，他可以编译的语言包括C、C++、Objective-C、Fortran、Java等等
- 如果编译少数文件时，可以利用gcc编译器的传入规则，传参规则直接进行编译选项、依赖项的配置、或者进行链接指示，编译器可以正常工作生成目标文件。
- 如果工程变的复杂，编译指南可能同时变得复杂，直接向compiler传参变得不现实。这个时候可以引入make工具

## make、makefile

- make 的凭证是makefile, 根据编写的makefile指引编译流程和依赖关系。make工具可以看成是一个智能的批处理工具，它本身并没有编译和链接的功能，而是用类似于批处理的方式—通过调用makefile文件中用户指定的命令来进行编译和链接的。
- makefile就是编译指引，在里面可以对需要使用的编译器进行指定，make命令按照makefile的指示逐步协调文件与依赖的关系，指引编译器编译
- makefile在一些简单的工程完全可以人工拿下，但是当工程非常大的时候，手写makefile也是非常麻烦的，如果换了个平台makefile又要重新修改，这时候就出现了下面的Cmake这个工具。

## cmake 
- cmake生成 makefile给make用，就这么简单
- why cmake?更直白的语法，跨平台的兼容、更多样的编译指示，在实际工程中，我甚至在编译前先利用cmake运行准备工作的脚本
- cmake更支持分支结构的导入，变量的设置与沿用，总之让编译工程的方式变得更加灵活。
- cmake凭证式CmakeList.txt

## 总结一下大体流程
1.用编辑器编写源代码，如.c文件。

2.用编译器编译代码生成目标文件，如.o。

3.用链接器连接目标代码生成可执行文件，如.exe。

但如果源文件太多，一个一个编译那得多麻烦啊？于是人们想到，为啥不设计一种类似批处理的程序，来批处理编译源文件呢？

于是就有了make工具，它是一个自动化编译工具，你可以使用一条命令实现完全编译。但是你需要编写一个规则文件，make依据它来批处理编译，这个文件就是makefile，所以编写makefile文件也是一个程序员所必备的技能。

对于一个大工程，编写makefile实在是件复杂的事，于是人们又想，为什么不设计一个工具，读入所有源文件之后，自动生成makefile呢，于是就出现了cmake工具，它能够输出各种各样的makefile或者project文件,从而帮助程序员减轻负担。但是随之而来也就是编写cmakelist文件，它是cmake所依据的规则。（cmake中有很多设置库的，此时还不是可执行文件，而make生成后才是二进制可执行文件。）

所以在编程的世界里没有捷径可走，还是要脚踏实地的。