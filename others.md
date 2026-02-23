---
layout: page
title: 杂项
permalink: /others/
toc: true
body_class: page
description: 君子终日乾乾夕惕若厉无咎
---

---
<figure style="text-align: center; margin: 20px 0;">
    <img src="/assets/img/qianli.jpg" alt="千里江山图" style="max-width: 100%; height: auto; border-radius: 2px;">
    <figcaption style="
        font-family: 'KaiTi', 'STKaiti', '楷体', serif; 
        font-size: 0.85rem; 
        color: #555; 
        margin-top: 8px;
    ">
        《千里江山图》卷 [北宋] 王希孟作
    </figcaption>
</figure>

---
{:toc}
<br>
#### LaTeX模板

由于苏绚习惯使用VS Code编辑、编译.tex文档，所以这里的LaTeX模板适用于VS Code及相关配置，对于其它平台的适用性不得而知。

常用中文字体包括Windows自带的（即中易系列）宋体、仿宋、楷体、思源黑体（Source Han Sans SC）和思源宋体（Source Han Serif SC）等；开源英文字体使用Source Sans 3、Source Serif 4、Fira Math和Cascadia系列。Source系列主要用于正文和标题等，可在[adobe-fonts](https://github.com/adobe-fonts)下载，Cascadia系列可在[cascadia-code](https://github.com/microsoft/cascadia-code)下载，Fira Math是无衬线公式字体，可在[firamath](https://github.com/firamath/firamath)下载。如果可变字体无法正常编译使用，可根据需求下载单个静态字体并尽量选择“为所有用户安装”。

这是苏绚常用的VS Code中LaTeX相关[配置](https://github.com/suxuanfox/suxuanfox.github.io/blob/main/files/tex_setting.json)，冗余或不足之处敬请谅解。

以下为常用的各LaTeX模板。
<br>
- [papertex](https://github.com/suxuanfox/papertex)用于日常作业等，仅在[中国科学技术大学学业论文LaTeX模板](https://github.com/ustctug/ustcthesis)的基础上做极少量修改，增加了从参考文献返回对应正文的跳转功能。
- [notetex](https://github.com/suxuanfox/notetex)是基于李文威老师的《代数学方法：卷二》的[源代码](https://github.com/wenweili/AlJabr-2)根据主观需求做少量修改得到的一份适用于课程笔记等方面的LaTeX书籍模板，主要修改了字体配置。[笔记模板测试](https://github.com/suxuanfox/notetex/blob/main/main.pdf)为一个简单的测试用的示例样稿。
- [prebeamer](https://github.com/suxuanfox/prebeamer)是参照李文威老师的著作[《代数学方法：卷二》](https://github.com/wenweili/AlJabr-2)及其源代码制作的中文Beamer模板，用于日常的交流展示等。[演示文稿测试](/files/main.pdf)为一个简单的示例。
