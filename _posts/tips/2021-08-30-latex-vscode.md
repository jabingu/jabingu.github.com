---

layout: post
title:  "使用VSCode编写LaTeX"
date:   2021-08-30 7:30:00
categories: tips
tags: latex
thumbnail: "assets/img/post/tips.jpg"
feature-img: "assets/img/post/tips.jpg"
excerpt: vscode配置latex
---

* content
{:toc}
> 主要是记录下vscode中对latex的配置，其他的软件安装较为简单。





## 1、软件安装

### 软件目录

 **texlive**、**VSCode** 和 **SumatraPDF**

### 1. 安装 texlive

镜像网站：

[https://mirrors.huaweicloud.com/CTAN/systems/texlive/Images/](https://mirrors.huaweicloud.com/CTAN/systems/texlive/Images/)

[https://mirrors.aliyun.com/CTAN/systems/texlive/Images/](https://mirrors.aliyun.com/CTAN/systems/texlive/Images/)

### 2. 安装 VSCode 上的latex插件

VSCode 安装完成之后，在扩展商店安装 `LaTeX Workshop` 插件。



## 2、VSCode配置

在 VSCode 界面下按下 `F1`，然后键入`“setjson”`，点击`“首选项: 打开设置(JSON)”`，

将以下代码放入设置区：

```latex
{
    // LaTeX
    "latex-workshop.latex.autoBuild.run": "never",
    "latex-workshop.message.error.show": false,
    "latex-workshop.message.warning.show": false,
    "latex-workshop.view.pdf.viewer": "external",
    "latex-workshop.view.pdf.ref.viewer":"external",
    "latex-workshop.view.pdf.external.viewer.command": "D:/Program Files (x86)/SumatraPDF/SumatraPDF.exe",
    "latex-workshop.view.pdf.external.viewer.args": [
        "%PDF%"
    ],
    "latex-workshop.view.pdf.external.synctex.command": "D:/Program Files (x86)/SumatraPDF/SumatraPDF.exe",
    "latex-workshop.view.pdf.external.synctex.args": [
        "-forward-search",
        "%TEX%",
        "%LINE%",
        "%PDF%"
    ],
}
```

主要是将pdf浏览器设定为外部浏览器



## 3、SumatraPDF 配置反向搜索

`设置`--> `选项`中输入

```python
"D:\Program Files\Microsoft VS Code\Code.exe" "D:\Program Files\Microsoft VS Code\resources\app\out\cli.js" -g "%f":%l
```

