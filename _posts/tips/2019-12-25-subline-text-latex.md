---

layout: post
title:  "Subline text 编辑Latex文档"
date:   2019-12-25 07:19:54
categories: tips
tags: tips
thumbnail: "assets/img/post/tips.jpg"
feature-img: "assets/img/post/tips.jpg"
excerpt: 使用subline text来编辑Latex文档
---

* content
{:toc}
>  之前是用TeXstudio来编写latex文档的，但是存在着一些小问题，一个软件比较久的而且就是和有道词典冲突了。所以想用其他的编辑器来进行编辑。



## 安装软件

1. 下载并安装[Sublime Text 3](https://www.sublimetext.com/3)：文本编辑工具。

2. 下载并安装[texlive](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)：编译Latex的工具。

3. 下载并安装[Sumatra PDF](https://www.sumatrapdfreader.org/download-free-pdf-viewer.html)：浏览编译的PDF文件的工具。

主要的思路是这样的：

> **Sublime Text 3**是主要的工具，在这个里面安装插件来支持Latex的编辑，然后在插件里面把texlive和Sumatra PDF的地址填写进去，来进行链接，这样我们在使用Sublime Text 3进行latex编写好后就会调用texlive来编译，并且使用Sumatra PDF来查看编译输出的PDF。

具体安装步骤不再编写。

## Sublime Text3 插件安装

### Package Control组件安装

> `Package control`是必装插件，所有其他的插件和主题都可以通过它来安装。

1）按Ctrl+`调出·console

2）粘贴以下代码到底部命令行并回车：

```c++
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.bui<br>ld_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ',<br>'%20')).read())
```

如果在`Perferences`中看到`package control`表示安装成功。

### 安装LaTeXTools

> LaTeXTools是sublime text3对于Latex的支持

1）按下`Ctrl+Shift+P`调出命令面板,或者是点击`package control`

2）输入`install` 调出 `Install Package `选项并回车，然后输入`LaTeXTools`进行安装。



## 配置LaTeXTools

选择`Preferences—>Pakage Settings --> LaTeXTools -->Settings-Default`,进入配置页面

`ctrl+F`查找"windows":

把`textpath`和`sumatra`更改为实际的安装地址

```c++
"textpath":"D:\\Program Files\\texlive\\2019\\bin\\win32;$PATH",
"distro":"texlive",
"sumatra":"D:\\Program Files\\Sumatra\\SumatraPDF\\SumatraPDF.exe",
```

`ctrl+F`查找"builder":

修改为

```c++
"builder":"simple",
```



## 配置SumatraPDF

### 添加环境变量

在我的电脑里打开`环境变量设置`，在user的环境变量中添加**SumatraPDF 的主程序目录**，比如：

```c++
D:\Program Files\SumatraPDF
```

### 配置反向搜索

打开命令提示符（win+R）,输入`cmd`，执行以下命令：（将其中的安装路径替换成你实际的安装路径）

```c
sumatrapdf.exe -inverse-search “\”D:\Program Files\Sublime Text 3\sublime_text.exe\” \”%f:%l\”“
```

## 使用

先`CTRL+S`，然后`CTRL+B`。Sublime Text 就会自动调用 LaTeXTools 的 build 系统来进行编译，如果编译成功，会自动打开 SumatraPDF 进行预览。





## 参考文献

[基于TeXlive,使用Sublime Text 3编写LaTeX](https://blog.csdn.net/qazxswed807/article/details/51234834)