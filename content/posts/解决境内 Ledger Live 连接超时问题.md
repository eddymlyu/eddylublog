---
title: "解决境内 Ledger Live 连接超时问题"
date: 2022-12-23T14:08:56+08:00
draft: false
url: "posts/ledgerlive"

ShowToc: true
TocOpen: true

tags: ["blockchain","crypto","proxifier","ledger"]
categories: ["blockchain","personal finance"]
---



### 背景
在11月FTX事件爆发很多人开始把crypto资产转入冷钱包，Ledger作为其中一个大厂成为很多人的选择。而我在中旬尝试使用Ledger时，发现我的账户始终无法同步，重置也无效。继而发现Nano S Plus的固件始终停留在1.0.3，而无法升级成最新的1.0.4。把软件都重新卸载安装，然后连验证产品真伪这一步也无法通过了。

询问了客服之后，原因很简单 — 大陆境内的Ledger Live被墙了。

![](/img/ledgertimeout.png)

### 设置Proxifier
#### 1. Proxifier是啥
Proxifier是一款简单易用的代理客户端软件，可以使本不支持通过代理服务器工作的网络程序能通过HTTPS或SOCKS代理，同时经过设置端口，指定的程序能够轻松让软件/游戏走直连/代理，经常和Clash，V2Ray这种代理工具配合使用。Proxifier本质是能让一些例外或者特殊程序能够顺利走代理。

本文就是通过设置Proxifier让Ledger Live能够走代理，实现连接。

![](/img/proxifier.png)

#### 2. 获得代理工具信息
本地代理的IP一般情况下是 127.0.0.1, 我使用的是Clash for Mac V3.7，使用 http+socks 混合协议的默认代理端口 7890。

![](/img/ClashforMac.png)


#### 3. 完成Proxifier常规设置
如果是第一次添加服务器Proxy Sever，它会问你是否把这个服务器当作默认服务器，点击yes。

打开Proxifier，点击Proxies，然后点击Add添加代理server。
![](/img/proxifier1.png)

输入Address地址，端口，勾选Socks version 5，Save！

![](/img/proxifier2.png)


#### 4. 设置程序代理规则

📌必要设置
→ 让Clash/代理程序走正常的网络Direct(但我测试成功Clash走的是Rule不是Direct)；
→ 让加速器程序走直连Direct；

🤏可选设置：
→ 特定聊天软件不经代理走Direct，如微信等；
→ 不会自定义Clash规则，设置指定程序走Clash的全部代理。

点击Rules设置规则，点击Add添加。

例如添加Ledger Live，命名下Name，“+”号添加应用程序，Action选Direct，Save！可依次添加google chrome和Clash等。

![](/img/proxifier3.png)
![](/img/proxifier4.png)

#### 5. 设置DNS代理
这个设置一般情况下不用设置，如果碰到有程序，无法通过你所用的代理工具走代理，可能需要让DNS也走代理，那可以尝试通过这个设置解决问题。

点击DNS，取消Detect DNS Settings Automatically前面的勾，然后给Resolve Hostnames through Proxy 打勾，Save！

![](/img/proxifier5.png)


### 实测
经过上面一连串的设置，代理软件通过Proxifier实现按需代理基本就实现了，运行正常的情况下界面如下。早前我也尝试过使用V2rayU，但是不成功，总是显示红色字的connect error。

![](/img/proxifier6.png)
可以继续DCA比特币了！

![](/img/proxifier7.png)
