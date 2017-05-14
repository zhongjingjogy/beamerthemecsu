制作个人使用的beamer模版
=======================================

sty样式文件的编写和使用
------------------------

在进行格式定制前，先简单了解一下sty样式文件的编写和使用。新建文件名为beamerthemeCSU.sty的文件，然后在其中声明这个样式文件的名称。此处，sty样式定义的名称为beamerthemeCSU。
:: 
    \NeedsTeXFormat{LaTeX2e}[1994/06/01] 
    \ProvidesPackage{beamerthemeCSU} 
    [2017/05/9 v0.01 LaTeX package for my own purpose] 

暂时不添加别的内容，然后在当前路径下新建一个幻灯片源文件template.tex。
:: 
    \documentclass[xcolor=dvipsnames]{beamer}
    \usepackage{beamerthemeCSU}
    \usepackage[scheme=plain]{ctex}

    \title{自定义Beamer主题样式}
    \author{Jing Zhong}
    \begin{document}
    {
        \begin{frame}
        \titlepage
        \end{frame}
    }
    \end{document}

然后采用xelatex编译一下源文件，可以看看效果。


可定制内容
-------------------
在beamer中基本都是可以重新定义的，这里将要讨论的定制内容包括如下部分。在这个说明里面，将尽量保持不同部分的相互独立。

- 标题页
- 幻灯片标题
- 图表标题
- block样式
- 字体及颜色

在beamer环境中，提供了\defbeamertemplate和\setbeamertemplate两个命令帮助我们制作新的样式。前者可认为是重新声明新的样式，而后者这是能够对默认样式进行修改。

1. 标题页
```````````````
修改sty文件，添加标题页的样式到sty文件中。重新编译可预览样式效果。
:: 
    \defbeamertemplate*{title page}{customized}[1][]
    {
        %font setting for the title
        \usebeamerfont{subtitle}
        \usebeamercolor[fg]{subtitle}
        \setbeamercolor{postit}{fg=black,bg=white}

        \begin{beamercolorbox}[sep=1em,wd=1.062\textwidth,ht=0.2cm,dp=1cm,center]{postit}
        {
            \usebeamerfont{title} {\large \inserttitle}
            \par \usebeamerfont{subtitle} {\insertsubtitle}
        }
       \end{beamercolorbox}

        % format the information of the authors
        \begin{beamercolorbox}[sep=1em,wd=1.062\textwidth,ht=0.5cm,dp=0.5cm,center]{postit}
        {
            \setbeamercolor{author}{bg=black,fg=Red}
            \usebeamerfont{author} \insertauthor\par
            \usebeamerfont{institute}\insertinstitute\par 
        }
        \end{beamercolorbox}
    }

2. 幻灯片标题
````````````````
幻灯片标题定制
:: 
    \setbeamertemplate{frametitle}
    {
        \setbeamercolor{palette quaternary}{fg=white,bg=arsenic}
        \setbeamercolor{titlelike}{parent=palette quaternary}
        \nointerlineskip
        \begin{beamercolorbox}[sep=0.3cm,ht=2.0em,wd=\paperwidth]{frametitle}
            \vbox{}\vskip-4ex%
            \strut\insertframetitle\strut
            % \hfill
            % \raisebox{-2.0mm}{\includegraphics[width=0.7cm]{csu.png}}
            \vskip-0.8ex%
        \end{beamercolorbox}
    }

3. 图表标题
``````````````
图标标题定制
:: 
    \setbeamertemplate{caption}{
        \tiny \raggedright \insertcaptionname\ \insertcaptionnumber. \insertcaption\par
    }

4. block样式
`````````````````
block样式定制
:: 
    \setbeamercolor{block}{bg=red, fg=white}
    \setbeamercolor{block title}{bg=white, fg=arsenic}
    \setbeamerfont{block title}{size=\footnotesize}
    \setbeamerfont{block body}{size=\tiny}

5. 字体和颜色
`````````````````
可以设置全文的字体大小和颜色。
:: 
    \setbeamerfont{normal text}{size=\scriptsize}
    \setbeamercolor{normal text}{fg=black}
    \setbeamertemplate{footline}{}
    \setbeamertemplate{enumerate items}[square]

字体及颜色
------------
字体与颜色在这里单独的总结。首先是颜色可以根据rgb编码来自行定制，常用的配色表可以参考'Latex颜色表<http://latexcolor.com/>'_。
:: 
    \definecolor{satinsheengold}{rgb}{0.8, 0.63, 0.21}

定义过以后，就能在文中使用。可以在设置全局环境中使用，也能通过\\textcolor来使用。
:: 
    \textcolor{red}{\textbf{(1) Smoothing: which fitting function to be chosen?}}