制作个人使用的beamer模版
=======================================

sty样式文件的编写和使用
------------------------

在进行格式定制前，先简单了解一下sty样式文件的编写和使用。新建文件名为beamerthemeCSU.sty的文件，然后在其中声明这个样式文件的名称。此处，sty样式定义的名称为beamerthemeCSU。
:: 
    \\NeedsTeXFormat{LaTeX2e}[1994/06/01] 
    \\ProvidesPackage{beamerthemeCSU} 
    [2017/05/9 v0.01 LaTeX package for my own purpose] 

暂时不添加别的内容，然后在当前路径下新建一个幻灯片源文件template.tex。
::
    \\documentclass[xcolor=dvipsnames]{beamer}
    \\usepackage{beamerthemeCSU}
    \\usepackage[scheme=plain]{ctex}

    \\title{自定义Beamer主题样式}
    \\author{Jing Zhong}
    \\begin{document}
    {
        \\begin{frame}
        \\titlepage
        \\end{frame}
    }
    \\end{document}

然后采用xelatex编译一下源文件，可以看看效果。


可定制内容
-------------------
在beamer中基本都是可以重新定义的，这里将要讨论的定制内容包括如下部分。在这个说明里面，将尽量保持不同部分的相互独立。

- 标题页
- 幻灯片标题
- 图标标题
- block样式
- 字体及颜色

在beamer环境中，提供了\defbeamertemplate和\setbeamertemplate两个命令帮助我们制作新的样式。前者可认为是重新声明新的样式，而后者这是能够对默认样式进行修改。

1. 标题页

::
    \\defbeamertemplate*{title page}{customized}[1][]
    {
        %font setting for the title
        \\usebeamerfont{subtitle}
        \\usebeamercolor[fg]{subtitle}
        \\setbeamercolor{postit}{fg=darkcerulean,bg=white}

        \\begin{beamercolorbox}[sep=1em,wd=1.062\\textwidth,ht=0.2cm,dp=1cm,center]{postit}
        {
            \\usebeamerfont{title} {\\large \\inserttitle}
            \\par \\usebeamerfont{subtitle} {\\insertsubtitle}
        }
       \\end{beamercolorbox}

        % format the information of the authors
        \\begin{beamercolorbox}[sep=1em,wd=1.062\\textwidth,ht=0.5cm,dp=0.5cm,center]{postit}
        {
            \setbeamercolor{author}{bg=black,fg=Red}
            \usebeamerfont{author} \\insertauthor\\par
            \usebeamerfont{institute}\\insertinstitute\\par 
        }
        \\end{beamercolorbox}
}

