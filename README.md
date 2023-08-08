---
title: Hello World!
date: 2023-08-07 15:43:37
tags: Chinese
---
# 建站初衷

大一下接手了大创负责人，需要学习python、机器学习等相关知识，但是学了一个暑假之后发现，之前学过的已经忘得差不多了。

尤其是这种课外的知识，学完就忘，学习期间也想过要记录下学习成果，尝试了包括但不限于以下方法：

- 每学习python的一个新功能，就新建一个文件夹，把相关功能代码塞进去，显然，太笨
- 用Xmind做思维导图，但这种导图工具只适合做大纲，不可能把功能代码也放进去
- 把代码塞进word文档，后经过对比，markdown在做笔记方面好像更符合我的口味捏

用md来写文章，存放在哪呢？考虑过公众号、CSDN、简书等，但公众号主题单独，CSDN广告漫天飞，到处是复制粘贴，简书...平时不怎么用。最主要的原因还是：基于第三方平台的博客可扩展性不强，限制太多，也许还会存在审核。如果是个人建站，就具有丰富的主题和插件，完全取决于自己，而且审核人就是我自己呀，我是自由的！（雾

遂有了搭建独立博客的念头，专门用来存放笔记以便日后查阅（纯小白笔记，大佬请绕路）。如果是基于Wordpress的个人博客，云服务器就算是学生购买好像也不便宜，wp后台那个图形界面也不太喜欢，而且如果在未备份的前提下服务器销毁了，那辛辛苦苦写的文章就全没了。转念一想，这不是有现成的github嘛，也无需考虑备份的问题（赞美开源精神），于是本博客基于Hexo+github+vercel搭建（可能以后闲了去尝试一遍基于wp搭建

关于搭建教程，b站+知乎+谷歌，阅读Hexo官方文档，原理问题不懂的问GPT

---

# 建站历程

既然决定了用md写文章，那就要选一个自己心仪的md编辑器，目前我熟悉的两款就是Typora和VSCode。VSCode界面太乱，不适合写文章，相比之下Typora界面非常干净，不巧的是，前两年Typora开始商业收费，就算是个人用也同样要花15刀。对于一个把白嫖玩到极致的人，当然是给你破解啦哈哈哈哈私密马赛~

## Typora破解

1. 在typora安装目录找到此js文件：`LicenseIndex.180dd4c7.8ed91174.chunk.js`，用记事本打开就行

2. 搜索代码`e.hasActivated="true"==e.hasActivated`，改为`e.hasActivated="true"=="true"`，保存

3. 重新打开typora，激活成功![](https://s1.imagehub.cc/images/2023/08/08/-2023-08-06-202300.png)

这样平时写文章的地方就搞定了，下面搭建博客：

## 环境配置

- Node.js:https://nodejs.org/en

搭建Hexo首先需要有node.js的环境，安装完成后输入`node -v`进行验证，后续使用在`git bash`中进行

- Git:https://git-scm.com

## Hexo安装

> 官网：[Hexo](https://hexo.io/zh-cn/)

Hexo是一个基于node.js的静态博客网站生成器，作者是来自台湾的`Tommy Chen`，适合搭建轻量级博客

1. `npm install hexo-cli -g`在`git bash`中运行，其中`-g`参数表示全局安装

2. `hexo init blog-name`在当前目录下新建一个名为`blog-name`的文件夹，得到如下反馈信息：

> INFO  Cloning hexo-starter https://github.com/hexojs/hexo-starter.git
> INFO  Install dependencies
> INFO  Start blogging with Hexo!

3. `cd blog-name`进入博客文件夹

4. `npm install`安装依赖项，在`package.json`文件的`dependencies`字段中可以看到
5. `hexo server`->`hexo s`访问本地博客

## 写文章

- `hexo new "title"`创建文章（根据scafflod模板来创建）

那么这种方式和手动创建的md文件有何区别？代码创建的文件在开头会有一些预置代码，可以在`scafflods\post.md`中对`Front-matter`进行修改：

```yaml
---
title: Hello World!
date: 2023-08-07 15:43:37
tags:
---
```

*不同于分割线，这是一个YAML元数据块，是一种用于添加元数据信息的格式（理解为本文章的配置信息），通常被用于静态网站生成器（如Hexo）中。由于其并不属于Markdown标准语法的一部分，所以大多数渲染器会忽略此数据块，即不会以文本形式显示，仅仅是元数据信息。此数据块将由Hexo进行特定的处理*

没有此数据块的话会报错：`YAMLException: end of the stream or a document separator is expected`

### 注意事项

- 超链接跳转需要的是url地址，不是单纯的域名
- 关于Hexo对md图片语法的处理，并不支持绝对路径，此路径下的图片只有本地才能看到，考虑到博客还需发布至公网，那么图片也需要一个url地址，也就是需要存放至一台公共服务器上。问了GPT后发现，原来还有图像托管网站这种东西，我选的是[imagehub](https://www.imagehub.cc/)，上传图片后即可得到url地址（国外也有一家叫[imgur](https://imgur.com/)，可惜被墙了，那图片的url八成也被墙，我还是老老实实用国内的吧

## 更换 配置主题

选了一个Ayer主题，按[官网教程](https://shen-yu.gitee.io/2019/ayer/)运行`git clone https://github.com/Shen-Yu/hexo-theme-ayer.git themes/ayer`安装，`_config`文件里修改主题为ayer（文件夹名字）即可

到这里对于本地做笔记来说已经够用了，下面是把博客发布到公网：

## 本地Push至云端

---

# 小结

整个流程下来，已经对本应该学习的python失去了兴趣，赶紧趁热打铁去学习前端三件套（html css javascript），能用本地浏览器加载自己编写的html文件，简直太吸引人了。先定个小目标：编写一个简陋的html界面，用vercel部署（本地和云端都试一下）再通过域名访问（也许下一个目标是脱离vercel自己买服务器部署？暂时不想系统地学linux系统啊啊啊啊——

正如开头所说，这个网站会专门记录我学习的课外知识，专业课再看吧，上难度的话我应该也会写写。未来想学的东西也非常多，包括但不限于：

> Python MATLAB LaTeX 类Unix系统 Git命令 JavaScript 单片机等

素的，全部和专业课无关（悲

其实这篇文章在博客还未搭建好时就已经开始写了，以后也会采取这种方式，一边调试学习一边写文章，把自己的所思所想，遇到的问题以及解决方案都记下来。日后也许会对我认为不再有价值的文章进行删除或者合并，目前就先这样吧

