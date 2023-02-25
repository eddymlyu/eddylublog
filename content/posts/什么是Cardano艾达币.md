---
title: "什么是Cardano艾达币"
date: 2022-08-05T14:08:56+08:00
draft: false
url: "posts/cardano"

tags: ["crypto","blockchain","cardano"]
categories: ["blockchain"]
---

![](/img/cardano.png)

### 区块链3.0

- 区块链1.0代表：比特币BTC

解决的问题：我想给千里之外的德国的一位朋友转账100欧元帮我代购，传统方法复杂而且困难，目前可以通过公司名义在银行申请结汇欧元填一大堆申请表，几个工作日才能完成转账，并且银行收取手续费；但如果使用BTC，只需要用网络，输入对方钱包地址即可通过闪电网络，几分钟完成转账。

- 区块链2.0代表：以太坊ETH

解决的问题：交易往往需要很多条件，比如德国朋友完成代购我才肯给他转账，比如公司买卖是否需要定金？多少定金？是否分批发货等等？这个时候就需要合约，而在区块链世界中，即智能合约Smart contract，通过部署编程语言，实现买卖的自动化。

- 区块链3.0代表：Cardano

解决的问题：2.0的主链（如ETH）很难扩展到成千上万的用户，并且有TPS每秒交易量不够高（15tps）以及网络拥堵造成Gas fee高等问题；Cardono通过三个方面，从scalability可拓展性，interoperability可操作性和sustainability可持续性解决这些问题。

### Cardano的创立

创始人Charles Hoskinson，在2013年读了Vitalik（ETH创始人）的文章后觉得他超屌然后决定帮助他一起创建区块链这个未来科技。以太坊在2015年首次发布。

然后，双方在以太坊运营上出现分歧，V神认为应该无盈利模式而Hoskinson觉得应该按公司模式运营，所以Hoskinson走人了自己创立了Cardano，并在2017年发布了Cardano。

发行的代币是ADA艾达币，总量450亿个，目前流通大概340亿个。拥有三个组织，一个Cardano Foundation，一个IOG（前IOHK），一个日本的Emurgo。

### Cardano的三大支柱

1. Scalability可拓展性

运用Ouroboro为共识机制，是一种PoS（Proof of Stake)协议，而ETH和BTC是采用PoW机制（ETH2.0会从PoW转为PoS）；

目前Cardano的TPS（Transaction Per Second）是250tps，而BTC是4.6tps，ETH是15tps，SOL是65000tps，未来Cardano会上升到1 million tps；

Cardano网络会选举出一些节点Slot在纪元Epoch上，这些Slot有产生区块的权利。Ouroboro可处理无上限条Epoch链，每条Epoch上的Slot，就像是BTC区块链上挖矿一样，但是来的更便宜以及消化更低的算力；

1 Epoch= 5天，21,000 slots, 1 slot= 20s。

2. Interoperability可操作性

区块链和传统金融之间存在三个问题，元数据Metadata，归属问题Attribution，合规性Compliance；

在web2，一些平台如twitter和FB，如果你发推，则在FB平台并不能看到信息，各平台项目独立，而在web3，Cardano可以通过侧链互通，即你在“区块链twitter”发推，则在“区块链FB”上也能看到推文；

Crypto是区块链密码和凭证的工厂，他提供了信任之网web of trust，让我们不需要像web2那样再去需要账号和密码；

由于数据过于庞大，很多时候大多数人并不是获取全部信息，Cardano运用修剪（Purning），订阅（Subscription）和压缩（Compression）等技术，使得每个用户大体上都只需要保存他们需要的一个块（Chunk）的数据。

3. Sustainability可持续性

两方面，如何做支付以及如何技术持续发展；

Cardano也在探索加密货币是机器能够自主学习，能够自动识别一些钱包信息等。

关于Roadmap，团队目前在Basho的拓展阶段，最后一个阶段是Voltaire — 链上自治，让网络成为一个自我维持的系统。

### Cardano的非洲计划

Cardano在帮助埃塞尔比亚政府完善他们的教育系统，比如储存超过500w学生的数据，提供防串改记录，学生成绩验证，增加监控的功能和最安全的方法取得奖学金等；

在非洲提供更安全，更快，费用更低的转账服务和技术（挑战中心化机构；

帮助非洲本地开发者开发项目；

帮助非洲小额贷款更安全更可靠，财务系统更有效率的运作；

帮助非洲医疗机构更好的传输健康数据；

帮助非洲本地的制造业。