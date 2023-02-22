---
title: "搭建Hugo个人网站｜PaperMod主题"
date: 2023-02-21T14:08:56+08:00
draft: false
url: "posts/hugo"

ShowToc: true
TocOpen: true

tags: ["papermod","hugo","建站","静态网站"]
categories: ["lifestyle"]
---







## 前言

谈不上个人品牌的打造，也谈不上被动收入的项目，但我的确是受到近几年的FIRE运动浪潮和创作者经济的影响，不断的捏造这个个人博客的小泥人，不断的重新思考如果我做一个自己的网站，对自己和他人能有什么积极的意义。

想到就去做，做事情我喜欢start small。执行的过程中，现实这只手会慢慢推动你去往另外一个地方。况且，输出文字帮助我mental clarity，减压不少，单单是这一点，就已经是写作的动力了；而如果还能结交到同好两三，更是我的荣幸。

因为工作的原因一开始用wordpress建站，YouTube的算法把我带到[林猫先生的频道](https://www.youtube.com/watch?v=gm6zdoL1r0Y)，又开启了一扇门…经过疫情的催化，以及区块链技术的萌芽，更让我相信辛苦工作之余，必须抽出时间skin in the game，做一些更个人化、去中心化的项目以此反脆弱，给这个世界留下一点微不足道的声音，而通过做个人网站，这个声音可以很自由，很独立。

所以，why Hugo?

- 速度超快，之前的wordpress我习惯把主机架设在国外，国内用户访问速度受限；而Hugo是html静态网站不涉及后台运行；
- 维护简单，不存在wordpress整天在更新插件；
- 主题极简，例如目前使用的PaperMod，非常纯粹；
- 几乎免费，除了购买域名，搭建Hugo网站的服务如Github和Netlify都是免费的。  



## 建站
### 环境建设  


由于我使用的是Mac，以下的操作适用于macOS。

安装Homebrew。
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

需要注意的是如上code可能会被更新，请根据最新的安装代码执行；另，如果安装极度缓慢，可以执行如下国内镜像源备选（我就是执行第一个镜像源成功）。

```
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

可以通过如下检查版本验证Homebrew是否安装成功。

`brew -v`

安装git。

`brew install git`

可以通过如下检查版本验证git是否安装成功。

`git -v`

安装hugo。

`brew install hugo`

### 建立网站

可以选择你的网站资料所存放位置，比如文稿Documents，则先进入Documents。

`cd Documents`

例如新建一个名为demo-blog的网站；配置成Yaml是可选项，系统默认是Toml，选择成Yaml是因为语言比较简单（听说啦）；常见的语言有Yaml，Toml和Json。

`hugo new site demo-blog -f -yml`

### 安装主题

进入刚创建好的文件地址中（已进入Documents）。

`cd demo-blog`

进入hugo主题网站选一个合你心水的，比如我选的PaperMod，其[Github](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation#method-1)有其他安装方法，但第一个方法就可以给他run下去，theme文件夹里出现PaperMod文件夹说明安装成功。
```
git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
```



用[VS Code](https://code.visualstudio.com/)打开demo-blog，配置config.yml，增加theme命令以此连结主题PaperMod。
```
baseURL: "" # 网址这个地方可以先放空
languageCode: en-us
title: eddylu # 这个网站叫什么名字
theme: PaperMod # 主要是增加这个配对主题
```



试运行blog。

`hugo server`

终端运行出网站服务器，打开浏览器，输入http://localhost:1313，如果成功即可以看到个人网站的雏形。  
![](/img/hugoserver.png)


### 写篇文章试试！

posts指代的是content下的一个文件夹，我把所有文章都放在posts底下；first代表第一篇文章。

`hugo new posts/first.md`

如果想把文章做分类，比如美食和电影，则

`hugo new food/firstfood.md`

`hugo new movie/firstmovie.md`

进入刚建立的md文件，系统有自带的front matter模版，亦可以增添自己想要的功能。


```
---
title: "frist" # 此处修改文章名
date: 2023-02-20T14:08:56+08:00 # 日期可改
draft: false # 是否为草稿
---
你好，我是第一篇博客。
```


保存后刷新本地端口如果看到第一篇文章被同步了，那么代表个人主页已经成功建立了。这类的页面属于single page。

## 基础配置

有了网站的基础框架当然还不着急发布，因为还有一些连膝盖想都必须有的基础模块还未被加入。如下一些模块仅供参考，未来持续加入更多…

### 添加分类和标签

在config.yml里加入

```markdown
menu:
  main:
    - identifier: categories
      name: Categories
      url: /categories/
      weight: 10 # 重量越轻，就越往前面排，“1”则是置顶
    - identifier: tags
      name: Tags
      url: /tags/
      weight: 20
```

注：这是categories和tags是系统默认的类目 (taxonomy)，我们也可以添加其他的，但必须在config.yml里加入代码，比如想加入moods类目（比如happy或sad），如下代码，也必须把默认的categories和tags写上。这类的页面属于list page。
```
[taxonomies]
  tag = "tags"
  category = "categories"
  mood = "moods"
```

在posts里面的md文件，增加tags和categories的代码，后续可以串接到各自的list page。

```
---
title: "2022币圈7大崩坏" 
date: 2022-09-29T14:08:56+08:00
draft: false

tags: ["crypto","blockchain"]
categories: ["blockchain"]
---
```

### 添加时间轴

在config.yml里加入
```
menu:
  main:
  - identifier: archives
    name: Archives
    url: /archives/
    weight: 10
```

在content下面新建一个archives.md。

```
---
title: "Archives"
layout: "archives"
url: "/archives/"
summary: "archives"
---
```

### 添加搜索功能

在config.yml里加入
```
outputs:
  home:
    - HTML
    - RSS
    - JSON 
```
```
menu:
  main:
  - identifier: search
    name: Search
    url: /search/
    weight: 10
```

在content下面新建一个search.md。

```
---
title: "Search" 
layout: "search" 
summary: "search"
placeholder: "search"
---
```

### 建立layouts的html模版以覆盖系统模版

在layouts下建立一个新文件夹_default，再在底下建立一个archives.html；将themes/PaperMod下吗的layouts/_default的archives文件的html内容复制到刚才新建的archives.html里，则可以在里面做随心所欲的模版修改。

### 常用params参数
在config.yml配置一些基础的params，更多的配置可以见Github的[PaperMod模版](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-features/)

```
params:
  homeInfoParams:
    Title: '学习、思考和思考的地方' # 主题
    Content: '写一些给自己看的内容，然后觉得做一个网站比较屌而已' # 描述
  SocialIcons:
      -name: facebook # 可选
       url: 'www.facebook.com'
 
```

```
params:
  ShowBreadCrumbs: true # 面包屑导航
  ShowReadingTime: true # 阅读时间
  ShowShareButtons: true # 分享按钮
  ShowPostNavLinks: true # 文章前后页按钮
 
```

## 常用Markdown语法syntax

自定义url，在front matter增加：
```
url: "whateveryouwant” # 直接在域名后面的url
```

增加TOC (Table of Content)文章导航，在front matter增加：
```
ShowToc: true 
TocOpen: true # 默认展开
```

标题：
```
# 这是 H1
## 这是 H2
###### 这是 H6
```

列表：
```
- 列表项目
1. 列表项目
```

粗体、斜体和~~删除线~~：
```
*我是斜体超屌*   # 或_斜体_
**粗体才是真的屌**
***加粗斜体***
~~删除线~~
```


插入链接：
```
[链接文字](链接网址)
```

插入图片：
```
![alt text](/path/to/img.jpg)
```

插入行内代码块：用`包住头尾
```
`行内代码块`
```

插入代码块：用```包住头尾，并指定一种语言（也可以不指定）
```
我是代码块
```

引用：
```
> 引用内容Quote
```

分割线：
```
---
```

换行：
```
<br>
```

制作表格：`|`分隔不同的单元格，`-`分隔表头和其他行
```
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |

插入注解footnote
```
xxx[^1]
[^1]: 注解内容
```
更多的syntax可以见[这里](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)。
## 部署

Mac终端执行Hugo，则内部开始建立网站，此时本地public文件夹会多出许多文件。

`hugo`

### Github

注册一个[Github](https://github.com/)账号并创建一个仓库repository。
![](/img/repository.png)



终端进行git初始化。

`git init`

建立git模块。

`touch .gitmodules`

在VS Code输入git模块内容。

```
[submodule "themes/PaperMod"]
    path = themes/PaperMod
    url = "https://github.com/adityatelange/hugo-PaperMod.git"
```

提交版本库。

`git commit -m "first commit"`

创建分支。
```
touch git brach -M main

git remote add origin https://github.com/...git
```

推送至远程仓库。

`git push -u origin main`

### Netlify

注册一个[Netlify](https://www.netlify.com/)账号，串街到刚才github账号，完成设置，见[Adipurdila的第41分钟教学视频](https://www.youtube.com/watch?v=hjD9jTi_DQ4&t=733s)。

完成后Netlify会跑几分钟的设置，生成一个https://...netlify.app/的网址，意味着已经成功部署到Netlify。

Domain setting找到name servers的服务，进入自己域名提供商的DNS设置，将Netlify的dns记录贴到域名提供商的DNS条目中。
![](/img/nameservers.png)



稍等片刻，Netlify也会自动把网站配置上https；最后将自己的域名贴到config.yml，大功告成！
```
baseURL: "https://eddy.lu"
languageCode: en-us
title: eddylu 
theme: PaperMod
```

每次build完自己的内容，执行git的流程即可同步到网站。
```
git status
git add .
git commit -m "add"
git push
```

Have fun!!