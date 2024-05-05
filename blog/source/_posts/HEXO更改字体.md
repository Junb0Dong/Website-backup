---
title: HEXO更改字体
top: false
cover: false
toc: true
mathjax: false
date: 2024-05-04 23:27:17
author:
img:
coverImg:
password:
summary:
tags: HEXO
categories: [HEXO建站指南]
---



# HEXO更改字体

hexo自带的字体很不好看，可能是创始人是台湾的原因？字体有一种简繁之间的感觉，看着有点别扭，于是想着更改一下字体。

参考教程：

[如何修改Hexo主题：Butterfly网站字体](https://www.luxiyue.com/server/%E5%A6%82%E4%BD%95%E4%BF%AE%E6%94%B9hexo%E4%B8%BB%E9%A2%98%EF%BC%9Abutterfly%E7%BD%91%E7%AB%99%E5%AD%97%E4%BD%93/)

[【Hexo】自定义字体](https://blog.aizhiqian.xyz/posts/ca2ce3bc/)

参考以上教程，我是这么操作的：

1. 在`/source`目录下创建存储字体的文件夹`font`和存储css的文件夹`css`

2. 字体网站下载喜欢的字体，我用的是[谷歌字体](https://fonts.google.com/)，将下载好的字体存储到`/source/font`文件夹中

3. 在`/source/css`文件夹中创建文件`custom.css`

4. 编写`custom.css`文件

   ```css
   @font-face {
       /* 为载入的字体取名字(随意) */
       font-family: 'Junbo Font';	
       /* 字体文件地址(相对或者绝对路径都可以) */
       src: url('/font/sunny-spells-basic-font/SunnySpellsBasicRegular-Yz1Wv.ttf') format("truetype");
       /* 定义加粗样式(加粗多少) */
       font-weight: normal;
       /* 定义字体样式(斜体/非斜体) */
       font-style: normal;
       /* 定义显示样式 */
       font-display: block;
     }
   ```

5. 在`_config.butterfly.yml`中修改inject部分为：

   ```yml
   inject:
     head: 
       - <link rel="stylesheet" href="/css/custom.css">	# custom.css文件
       # - <link rel="stylesheet" href="/xxx.css">
     bottom:
       # - <script src="xxxx"></script>
   ```

6. 再在`_config.butterfly.yml`中修改字体font为：

   ```yaml
   font:
     global-font-size: '18px'	# 全局字体大小
     code-font-size: '14px'	# 代码字体大小
     font-family: apple-system # Junbo Font	# 全局字体的样式（更改为你喜欢的字体）
     # -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Lato, Roboto, "PingFang SC", "Microsoft JhengHei", "Microsoft YaHei", sans-serif
     code-font-family: consolas, Menlo, "PingFang SC", "Microsoft JhengHei", "Microsoft YaHei", sans-serif	# 代码字体样式，同上
   ```

   

