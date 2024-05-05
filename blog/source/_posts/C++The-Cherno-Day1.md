---
title: C++(The Cherno)-Day1
top: false
cover: false
toc: true
mathjax: false
date: 2024-05-03 20:55:59
author: junbo
img:
coverImg:
password:
summary:
tags: C++
categories: [C++学习,C++]
---
# C++(The Cherno)-Day1

## How C++ Works

C++是一种功能强大的编程语言，它的工作原理涉及**编译**和**链接**过程。**编译器将C++源代码文件转换为目标代码，然后链接器将目标文件组合成可执行文件**。下面是C++编译和链接过程的详细解释：



### 预处理

**预处理**：预处理器处理C++源代码文件，处理#include和#define等预处理指令。输出是一个不包含预处理指令的“纯”C++文件。

> 预处理在编译之前就已完成，以#开头，实现了包含各种库/宏定义以便在接下来的编程中更好的使用库函数/宏定义

```cpp
// 示例代码
#include <iostream> //预处理

int main() {
    std::cout << "Hello, World!";
    return 0;
}
```

### 编译

**编译（Compiling）**：编译器将预处理器的输出转换为汇编代码，然后将其组装成目标文件。目标文件包含编译的代码和符号定义。

>  编译由编译器完成，在VS中编译器编译（快捷键Ctrl+F7）生成`.obj`文件

```bash
g++ -c hello.cpp -o hello.o
```

编译阶段出现的错误通常以**Cxxx**形式出现

### 链接

**链接（Linking）**：链接器将编译器生成的目标文件组合成可执行文件。它会解析未定义的符号引用，并将它们与其他目标文件或库中的定义进行关联。

> 链接由链接器将VS编译生成的`.obj`文件转换为`.exe`可执行文件

```bash
g++ hello.o -o hello
```

这就是C++程序的基本工作原理。通过编译和链接过程，C++源代码被转换为可执行文件，可以在计算机上运行。

链接阶段出现的错误通常以**Lxxx**形式出现

### 常见错误总结

一个函数需要声明（Linking要做的）和定义（compiling要做的）

声明与定义不一致时：会产生`unresolved external symbol`的报错信息

多重定义时（重复定义一个函数）会产生编译错误（Compiling error）

多重声明时会产生链接错误（Linking error）

### 碎碎念

Cherno在视频里用VS演示的真绝了！看到最后有种恍然大悟的感觉，为什么要声明、定义和包含头文件讲的很透彻。可惜我主要用C++学习SLAM相关，演示有意思的编译和链接在vscode中不太好复现（CMake搞定了）

## Variables in C++

### 基础知识

C++中的变量是用来存储数据的标识符。变量的类型决定了变量可以存储的数据类型。C++中有几种基本的数据类型，包括字符类型、整数类型、浮点类型、布尔类型和空类型。以下是一些常见的C++变量类型和示例代码：

```cpp
// Character types
char myChar = 'A';

// Integer types
int myInt = 7;
unsigned int myUnsignedInt = 1024;

// Floating-point types
float myFloat = 3.14;
double myDouble = 0.01;

// Boolean type
bool myBool = true;

// Void type
void* myVoidPoi
nter = nullptr;
```

变量的名称必须是有效的C++标识符，以字母或下划线开头，可以包含字母、数字和下划线。C++是大小写敏感的，因此大写和小写字母不同。变量的名称不能是C++的保留关键字，如if、else、int等。

除了基本数据类型外，C++还支持复合数据类型，如数组、结构体、指针等。这些数据类型可以存储更复杂的数据结构。

### 为什么要有Char类型？

**char**类型主要是用来定义**字符类型**的变量，下面用程序演示一下

```cpp
char CharacterWithNum = 65;
cout << "define char with number:" << CharacterWithNum << endl;
char CharacterWithChar = 'A';
cout << "define char with character:" << CharacterWithChar << endl;
```

上面这段程序的输出结果是什么呢？

是`65`和`A`吗？

运行了一下我们发现，结果如下

<img src="C:\Users\20200\AppData\Roaming\Typora\typora-user-images\image-20240114215801431.png" alt="image-20240114215801431" style="zoom: 80%;" />

恍然大悟，原来char类型存在的意义就是为了程序员输出字符使用的，char类型一般使用ASCII表数字与字符的对应关系。

### float与double的定义

<img src="C:\Users\20200\AppData\Roaming\Typora\typora-user-images\image-20240114220216257.png" alt="image-20240114220216257" style="zoom: 50%;" />

我们在定义float类型后，运行一下程序，再回到定义的float类型变量会发现，float类型变为double类型了。

我认为这其中存在隐式转换，是系统或者编译器为了提升精度而产生的“副作用”。

那如果就要使用float类型我们可以在数字后面加上`f`（大小写都可以）

<img src="C:\Users\20200\AppData\Roaming\Typora\typora-user-images\image-20240114220704501.png" alt="image-20240114220704501" style="zoom: 50%;" />

这样我们便得到flaot类型的变量了。

### 常见错误总结

对于新手运行完c++程序后，我们会修改代码再次运行，但有时会报这个错误：

`严重性    代码    说明    项目    文件    行    禁止显示状态
错误    LNK1168    无法打开C:\Users\20200\Desktop\Day1ForLearnCpp\Debug\Day1ForLearnCpp.exe 进行写入    Day1ForLearnCpp    C:\Users\20200\Desktop\Day1ForLearnCpp\LINK    1    `

我们一般检查代码发现并没有问题，那么问题出现到哪里了呢？

**错误原因：**

这个错误通常是由于另一个进程正在使用该文件，或没有对该文件或其所在目录的写入权限所致。

**解决办法：**

把上一个运行结果的终端关掉再次运行即可（这个错误哭笑不得）
