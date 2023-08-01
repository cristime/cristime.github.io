---
title: noi linux 2.0 体验
date: 2023-08-02 01:36:01
tags:
  - Linux
  - OI
  - 杂谈
categories:
  - 杂谈
---

## 一、起因
下午，我打开 noi 官网准备报名 csp j/s，一看官网展板：“noi linux 2.0 发布” 我就兴奋了起来。（9 月 1 日起开始使用，
也就意味着 csp j/s 使用 noi linux 2.0）

<!-- more -->

[![flndoj.png](https://z3.ax1x.com/2021/08/08/flndoj.png)](https://imgtu.com/i/flndoj)

啪的一下很快啊，我点击了这个图片链接。

[![flnOTH.png](https://z3.ax1x.com/2021/08/08/flnOTH.png)](https://imgtu.com/i/flnOTH)

一看这个配置：Ubuntu 20.04.1、vscode、sublime、code::blocks、gcc-9，
同时也去除了辣鸡 IDE（GUIDE）。
相比于之前的 noi linux，这简直是天堂啊！

回想去年参加 csp，使用的是老版的 noi linux，回想起来真是一把辛酸泪啊：那个老旧的 Ubuntu 14.04、莫名其妙卡死的桌面、
不能称之为 IDE 的 IDE（GUIDE）、gdb 崩溃......我当时用的 emacs 和 vim（emacs稍微好一些，但是我比较习惯 vim），比赛前
还特意查了 vim 的用法、背了配置文件。真是难以言表。

难道 CCF 终于了解到 OIer 们的痛点了吗？他终于醒悟了吗？

## 二、安装系统
抱着试试看的心态，我下载了 noi linux 2.0 的 iso 文件（3.4G），使用 VirtualBox 安装了虚拟机（vmware 我感觉不好用），
当然也可以实体机安装双系统，网上教程一大堆，自行搜索。

[![flnawQ.png](https://z3.ax1x.com/2021/08/08/flnawQ.png)](https://imgtu.com/i/flnawQ)

这里注意，新的 Ubuntu 20.04 是 64 位系统（32位的可以歇歇了），RAM 最少需要开 2048 MB（否则系统无法启动）。

安装系统就一路默认（一开始语言选的是中文，后来我后悔了，最好选英文），键盘布局选择 Chinese - Chinese 就行。

大概 20 分钟左右系统安装完成，重启后弹出虚拟光驱进入系统。

## 三、使用系统
整个系统给我第一眼的印象感觉还行（可以在桌面右键点击
更换壁纸），但是系统似乎没有网络模块，所以无法联网。

[![fln0Fs.png](https://z3.ax1x.com/2021/08/08/fln0Fs.png)](https://imgtu.com/i/fln0Fs)

点击左下角的点，打开 VS Code、Terminal、Sublime Text、Code::Blocks。我写了一份测试代码（本人 C++ 党）。

[![flnBYn.png](https://z3.ax1x.com/2021/08/08/flnBYn.png)](https://imgtu.com/i/flnBYn)

```c++
#include <cstdio>
#include <cctype>
#include <vector>
using namespace std;

#define reg register

// 快读模板
int readInt() {
    reg int x = 0, f = 1; char ch = getchar();
    while (!isdigit(ch)) { if (ch == '-') f = -1; ch = getchar(); }
    while (isdigit(ch)) { x = x * 10 + ch - 48; ch = getchar(); }
    return x * f;
}

int main(void) {
    freopen("test.in", "r", stdin);
    freopen("test.out", "w", stdout);

    vector<int> v;
    int n = readInt();
    for (reg int i = 0; i < n; i++) v.push_back(read());
    for (auto el& : v) printf("%d ", el);
    puts("");

    fclose(stdin); fclose(stdout);
    return 0;
}
```
保存在 ~/test.cpp

同时创建 ~/test.in 并输入以下内容
```
5
1 2 3 4 5
```

在终端中输入
```bash
$ g++ test.cpp -o test -std=c++11 -O2  # C++11 和 O2 优化
$ ./test
```
打开 ~/test.out 查看，输出为：
```
1 2 3 4 5
```

VS Code、Sublime Text、Code::Blocks 我都进行了测试，并得出以下结论：

* VS Code 默认安装了 C/C++、Python、Pylance、Jupyter 插件，但是由于 C/C++ 插件安装后需要从 github 下载依赖文件，而系统又无法联网，所以 C/C++ 插件基本无用，这也导致了 VS Code 在 noi linux 下尴尬的境地。（但是不得不说 VS Code 在其他地方非常好用，平常用来写代码非常方便，同时跨平台支持，上手难度非常低，想使用的话教程网上都有）所以在这里不推荐使用 VS Code。
* Sublime Text 是另一款轻量化编辑器，和 VS Code 一样颜值高，在 noi linux 下有 C++ 的语法提示，同时支持单文件编译，其万能搜索栏（Ctrl+Shift+P）也是非常顺手。推荐使用 Sublime Text。
* Code::Blocks 是一款 C/C++ IDE（集成开发环境）。同时可以支持 C++ 语法提示，支持单文件编译，但是颜值非常朴素（~~与 Dev-C++ 类似~~）。Code::Blocks 跨平台支持，使用难度低，可以平时在其他系统使用。推荐 Code::Blocks。
* Vim/Emacs 上手难度较高，简洁高效，但是在不熟悉其快捷键的时候效率非常低。所以这里并未使用 Vim/Emacs 进行测试。

建议平时刷题的时候使用 Code::Blocks，~~可以抛弃老旧的 Dev-C++ 了~~。

**小提示：Linux 的命令行非常高效，建议熟练掌握其常见命令，有时甚至在比赛时可以救你一命（亲身经历）**

## 四、总结
noi linux 2.0 相比旧版本做了很大的改动，其使用更加方便，更加适合 OIer。

编程工具建议使用 Code::Blocks 和 Sublime Text。两者都有较好的语法提示和单文件编译功能。

~~CCF 终于开窍了！~~