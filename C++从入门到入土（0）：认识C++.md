# C++从入门到入土（0）：认识C++
> 本篇面向零基础或只有一点点编程经验的初学者。不需要你提前装好任何东西，跟着走就行。
## 一、C++ 是什么东西？
简单说：
**C++ 是一门让你可以直接指挥电脑干活的编程语言。**
它诞生于 1985 年，相信应该比很多读者的年龄都大。但它至今依然是：
- 游戏引擎（Unreal、Unity底层）的首选语言
- 高频交易系统的标配- 操作系统、浏览器内核、数据库的核心语言
- 嵌入式、物联网、自动驾驶的常用工具

为什么这么老还这么能打？
因为 **C++ 快，而且能让你精确控制电脑的每一个角落**。当然代价是——学起来比 Python、JavaScript 那些语言要费劲一些。所以才叫"从入门到入土"嘛。但别怕，跟着这个系列一步步来，入土之前你至少能写出个像样的程序。（也许吧）
## 二、为什么选 Clang++？
编译器前面聊过了，这里直接给结论：**本系列统一使用 Clang++（LLVM 的 C++ 前端）作为教学编译器。**
理由：
| 对比项 | Clang++ | GCC | MSVC |
| :--- | :--- |:---|:---|
| 报错信息 | 清晰、带颜色、带提示 | 对新手不太友好 | 还行，但重 |
| 安装体积 | 相对轻量 | 中等 | 巨大 |
| 跨平台 | Y Windows/macOS/Linux | Y | N 基本只Windows |
| 编译速度 | 快 | 中等 | 中等 

一句话：
**Clang++ 报错看得懂，装起来不费劲，跨平台，适合学习。**
## 三、环境准备
### 3.1 安装 Clang++
**Windows：**
1. 下载安装 [LLVM 官网](https://llvm.org/) 的 Windows 版本（或者去 [GitHub Releases](https://github.com/llvm/llvm-project/releases) 下载 `LLVM-*-win64.exe`）
2. 安装时勾选 
**"Add LLVM to the system PATH"**
3. 安装完成后打开命令行（Win+R → 输入 `cmd` → 回车），输入：
```bash
clang++ --version
```
如果看到版本号输出，说明安装成功。
> ⚠️ Windows 用户注意：Clang++ 需要搭配一个标准库。最简单的方式是安装 **MinGW-w64**，然后让 Clang++ 使用它的 libstdc++。或者安装 Visual Studio Build Tools，让 Clang++ 使用 MSVC 的库。新手推荐后者——装个 Visual Studio Community 勾选 "Desktop development with C++" 就行，Clang++ 会跟着装好。

**macOS：**
```bash
xcode-select --install
```
一行命令搞定，系统自带 Clang++。
**Linux（Ubuntu/Debian）：**
```bash
sudo apt updatesudo apt install clang
```
**验证：**
```bash
clang++ --version
```
看到类似 `Ubuntu clang version 18.1.3` 或 `Apple clang version 15.0.0` 就对了。
### 3.2 准备一个代码编辑器
你不需要一上来就用庞大的 IDE（比如 Visual Studio）。
推荐：
- **VS Code**（免费、轻量、插件丰富）—— 装个 "C/C++" 插件就行
- **Notepad++** / **Sublime Text** —— 够用
- **Vim/Neovim** —— 如果你已经会用的话
本篇用最简单的文本编辑器，编译全靠命令行。
## 四、第一个程序：Hello World
打开编辑器，新建一个文件，输入以下内容：
```cpp
include <iostream>
int main() 
{
std::cout << "Hello, World!" << std::endl;
return 0;
}
```
保存为 `hello.cpp`。
## 五、代码逐行拆解别被这几行吓到，一行一行看：
### `#include <iostream>`
`#include` 是"把别人的代码拿过来用"的意思。`<iostream>` 是 C++ 标准库里负责**输入输出**的头文件。没有它，你就没法让程序往屏幕上打印东西。
> 打个比方：这就像你做菜之前，先把调料包拆开放在灶台上。### `int main() {`这是**主函数**。每个 C++ 程序都必须有且只有一个 `main` 函数，它是程序的入口——程序从这里开始执行。- `int` 表示这个函数执行完会返回一个整数- `main` 是函数名（固定写法，不能改）- `()` 里可以放参数，现在先不填- `{` 表示函数体开始
### `std::cout << "Hello, World!" << std::endl;`
这行是核心：- `std::cout` —— 标准输出（通常是你的屏幕/终端）- `<<` —— 把右边的东西"放进"左边的输出流里（可以理解为"在屏幕上打印东西"）
- `"Hello, World!"` —— 一个字符串，就是要显示的文字
- `std::endl` —— 换行，并且立刻把内容刷到屏幕上
- `;` —— 每条语句末尾必须有分号，漏了会编译报错
- 整行意思：**把 "Hello, World!" 送到屏幕上，然后换行。**
### `return 0;`
`main` 
函数返回 `0` 表示程序正常结束。操作系统看到返回 `0` 就知道"这程序跑完了，没出错"。
> 约定俗成：`0` = 成功，非 `0` = 出错了。
### `}`
函数体结束。总之就是代码结束了。
## 六、编译和运行
打开命令行，进入 `hello.cpp` 所在的目录，执行：
```bash
clang++ hello.cpp -o hello
```
这里先不讲解各个参数的具体含义。
如果没报错，说明编译成功。然后运行：
**Linux / macOS：**
```bash
./hello
```
**Windows：**
```bash
./hello.exe
```
你应该能看到屏幕上输出：
```
Hello, World!
```
恭喜，你的第一个 C++ 程序跑起来了。
如果报错可以检查是否是：
- 缺少头文件（库）
- 没有命名空间std
- 标点用了中文符号
- 缺少分号

##可选任务
让C++输出**my first project**