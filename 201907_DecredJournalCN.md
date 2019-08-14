# Decred月报 - 2019年7月

![Image: Staking discussion at StakingCon 2019 in Beijing](img/stakingcon2019-384.jpg)

_图片: 北京 StakingCon 2019 关于Staking的讨论_

七月重大新闻:

* 一个重要里程碑诞生:DecredDEX的[规范](https://github.com/decred/dcrdex)文本已经发布。开发计划由dcrdata的开发者在八月初通过[提案](https://proposals.decred.org/proposals/417607aaedff2942ff3701cdb4eff76637eca4ed7f7ba816e5c0bd2e971602e1)提交。
* 3家提供做市公司在8月7日分别提交了他们的提案。8月10日发布的RFP提案旨在询问利益相关者是否想要聘请做市商，若投票通过则开启做市商的提案投票，若不通过则关闭做市商的提案。详细内容会在Politeia摘要和下月月报中介绍。
* TinyDecred是一个python工具包，由@ buck54321发布，他是去年开始从事dcrdata开发工作的承包商。TinyDecred最初是Brian的个人兴趣项目，但随着时间的推移发展成为一组有用的工具，可以为大量的Python编码器打开与Decred相关的开发。他提交了一份[提案](https://proposals.decred.org/proposals/20e967dad9e7398901decf3cfe0acf4e0853f6558a62607265c63fe791b8b124)，要求8,000美元用于TinyDecred的工作 - 这似乎得到了强有力的支持。
* dcrdata beta v5.1现已上线，充满了渐进式改进。dcrextdata也取得了很好的进展，收集了更多的市场数据，并在网络上部署了节点来收集有关mempool和块传播时间的数据。
* [@muststopmurad](https://www.youtube.com/watch?v=XkvcdjSH0c0)和[@permabullnino](https://www.youtube.com/watch?v=HxECplK3kAs)发布了Decred in Depth语音录播，他们谈到了他们为什么加入Decred以及他们对未来的机遇和挑战提出了自己的看法。
* 在社交媒体上，Decred相关的讨论似乎越来越多，参与讨论的人的圈子也在扩大。毫无疑问，这是受到Decred的支持，由@checkmate发起并推广，他还发表了一篇关于Decred货币溢价的[文章](https://medium.com/@_Checkmatey_/monetary-premiums-can-altcoins-compete-with-bitcoin-54c97a92c6d4)，并提交了继续进行这一研究的 [提案](https://proposals.decred.org/proposals/78b50f218106f5de40f9bd7f604b048da168f2afbec32c8662722b70d62e4d36) （现已批准）。@Checkmate的文章已经被一篇来自BlockheadCapital的[投资论文](https://www.blockheadcap.com/post/decred-investment-thesis)引用了，他貌似也要奶一下Decred。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd):代码维护优化、bug修复和为各种即将推出的功能添加基础设施。

引入了[rpcclient](https://github.com/decred/dcrd/pull/1807)，[database](https://github.com/decred/dcrd/pull/1799)，[blockchain/stake](https://github.com/decred/dcrd/pull/1803)和[dcrjson](https://github.com/decred/dcrd/pull/1779)模块的最新核心版本，以利用其它模块的最新改进。新的dcrjson模块进行了重大改进，同时保留了向后兼容的API。这将允许用户模块在完全升级到新API之前通过旧API获取大部分改动。用核心版本碰撞的机会来断开紧密耦合并删除未使用的代码。

增加了Go编译器代码生成问题的 [解决方案](https://github.com/decred/dcrd/pull/1801)，以避免chainCfg/v2二进制模块崩溃。

[dcrwallet](https://github.com/decred/dcrwallet): 代码库升级和错误修复。已经合并了对JSON-RPC代码的大量[重构](https://github.com/decred/dcrwallet/pull/1509)和[去除](https://github.com/decred/dcrwallet/pull/1496)过时的gRPC代码。

[Decrediton](https://github.com/decred/decrediton): 较小的用户界面改进和错误修复。[实施](https://github.com/decred/decrediton/pull/2146)响应式购票视图。大量依赖项已[升级](https://github.com/decred/decrediton/pull/2156)，以弥补漏洞。

[Politeia](https://github.com/decred/politeia): 继续重新设计Politeia的界面。7月份的另一项主要任务涉及将谷歌开源[Trillian](https://github.com/google/trillian)数据存储的tlog [集成](https://github.com/decred/politeia/pull/951)到后端作为Git的替代品。tlog ([透明日志](https://research.swtch.com/tlog)) 将提高可伸缩性，允许单独对记录添加时间戳，并允许将来切换到类似ipfs的文件系统。

通过电子邮件登录[已被替换](https://github.com/decred/politeia/pull/940)为使用用户名登陆，并将在下一次更新时部署在politeia上。

[dcrstakepool](https://github.com/decred/dcrstakepool): 用户界面和性能改进，错误修复。修改了“[连接到钱包](https://github.com/decred/dcrstakepool/pull/427)”视图，并添加了VSP的[块高度](https://github.com/decred/dcrstakepool/pull/440)显示作为正常指示器。将dcrstakepool和dcrwallet[分离](https://github.com/decred/dcrstakepool/issues/227)的更多工作（dcrstakepool应该只与管理投票钱包的stakepoold服务对话）。

Raedah Group已开始改进VSP身份[验证](https://github.com/raedahgroup/dcrstakepool/pull/4)API。这将允许使用[无账户的VSP](https://github.com/decredcommunity/issues/issues/100)，这将大大简化新用户的设置过程，并允许[选择电子邮件](https://github.com/decred/dcrstakepool/issues/274) ([讨论](https://matrix.to/#/!wSdymYrEpBhsWlDJuk:decred.org/$15605505894685ViDcj:decred.org))。

[dcrlnd](https://github.com/decred/dcrlnd): 已经移植了来自[lnd](https://github.com/lightningnetwork/lnd)的上游更改，私有dev分支大多与上游lnd主[分支](https://github.com/decred/dcrlnd/pull/36#issuecomment-509370199)同步。要审查的最新上游[合并请求](https://github.com/lightningnetwork/lnd/commit/add905d17f7bbb11d0df2761cdf8accf2fef2b00) 已于7月25日提交给lnd。

[闪电水龙头](https://github.com/decred/lightning-faucet)回购已经从@matheusd的github迁移到官方颁布的组织，在这个月，水龙头在生成闪电发票和增加持续集成的表单上看到了细微的改进。新的付款[发票单](https://github.com/decred/lightning-faucet/pull/9)已经开始工作，它[允许](https://github.com/decred/lightning-faucet/pull/10)用户通过水龙头付款（目前用户必须使用"dcrlncli"在命令行上支付发票）。

[dcrandroid](https://github.com/decred/dcrandroid): 用户界面优化和错误修复，添加 [重命名帐户](https://github.com/decred/dcrandroid/pull/386)功能。

在通知和[状态页面](https://github.com/decred/dcrandroid/pull/397)中添加[生物识别认证](https://github.com/decred/dcrandroid/pull/343)、[声音和振动](https://github.com/decred/dcrandroid/pull/399)的工作正在进行中。

[dcrios](https://github.com/raedahgroup/dcrios): 用户界面优化和错误修复，[西班牙语](https://github.com/raedahgroup/dcrios/pull/500)，[越南语](https://github.com/raedahgroup/dcrios/pull/498)和[葡萄牙语](https://github.com/raedahgroup/dcrios/pull/497)的新翻译。

[dcrdata](https://github.com/decred/dcrdata): v5.1版本现已上线。这个版本添加了许多用户界面增强功能，包括向市场仪表板添加Fiat和Percent值、 [提案页面](https://explorer.dcrdata.org/proposal/decentralized-exchange-specification-document)上的[新样式](https://github.com/decred/dcrdata/pull/1446)、对“预测”硬币供应图表的调整、全屏[地址图表](https://github.com/decred/dcrdata/pull/1443)（对于[社区基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)地址很有用）和退票[进度条](https://github.com/decred/dcrdata/pull/1447)。

随着 [地址端点](https://github.com/decred/dcrdata/pull/1438)的改进、几个错误修复以及客户机连接的最大数量从1000[增加](https://github.com/decred/dcrdata/pull/1481)到16384，Insight API受到了一些关注。

> dcrdata现在是Decred的官方Insight API。Exodus wallet现在使用主机insight.dcrdata.decred.org来满足他们的Insight API需求。在任何给定时间，大约有800个socket.io客户端连接（Insight websocket位）到dcrdata，我们没有来自这些用户的抱怨。（与 @chappjc [聊天](https://matrix.to/#/!LmKzrmxJIXNHNiEmIh:decred.org/$15651246158457opycs:decred.org)）

合并dcrd[变更](https://github.com/decred/dcrdata/pull/1491)。[更新](https://github.com/decred/dcrdata/pull/1467)了NPM依赖项以关闭已知的漏洞。

Raedah Group继续研究[dcrextdata](https://github.com/raedahgroup/dcrextdata)，这是一个用于收集dcrdata上尚未找到的外部（脱链）数据的软件包。在收集关于mempool和块传播时间的节点数据方面取得了进展。现在可以从单个节点跟踪这些数据，并且在完成跟踪数据的完整历史记录（使用图表）时可以使用它们。dcrextdata还可以从PoW池和VSP中提取和存储数据，这将允许维护这些属性的历史记录。[这里](http://dcrextdata.raedahgroup.com/)提供了实时数据的演示。

其它:

* DecredDEX规范文本已经发布并添加到新的[dcrdex](https://github.com/decred/dcrdex)存储库中。
* Raedah Group正在为BTC/DCR交易开发一款移动应用程序（目前该项工作属于私人回购）。
* [Bug赏金](https://bounty.decred.org/)网站[更新](https://twitter.com/degeri_crypto/status/1154776087374770176)：添加了3个新漏洞的详细信息。该计划共处理了67份提交文件，其中9份有资格获得支付，其中8份已经修补和披露。

7月份的开发活动统计数据：51个活动PR，219个主提交，50K添加和29K删除的行分布在15个存储库中。贡献来自每个存储库1-6个开发人员。


## 人员

欢迎新的代码贡献者：bgptr（[decrediton](https://github.com/decred/decrediton/commits?author=bgptr)）、emesterhazy（([decrediton](https://github.com/decred/decrediton/commits?author=emesterhazy)）、reevesak（[dcrwallet](https://github.com/decred/dcrwallet/commits?author=ReevesAk)）。

恭喜在decred.org上列出的4位[decred.org](https://decred.org/contributors/)：

* Akin Sawyerr (@akinsawyerr, Africa Lead & Strategy)
* Kevin Hebert (@klebe, Developer)
* Leslie Ankney (@cryptoleslie, Public Relations)
* Victor Guedes (@VictorGuedes, Developer)

Decred澳大利亚社区一直在建设良好。上个月分享的[更新](https://medium.com/@sahand.bagheri/decred-australia-building-a-community-brick-by-brick-89928041687e)回顾了已建立的伙伴关系，组织的活动，吸引的人以及下一个目标。6月的月报对此进行了报道，但结果不仅仅是一篇文章。

社区统计截至8月1日：:

* Politeia用户: 154 (-35, 通过新的更准确的计数方法调整)
* Twitter粉丝: 40,572 (+93)
* Reddit订阅: 9,556 (+51)
* Matrix用户: 384 (+20)
* Slack用户: 6,809 (+40)
* Discord用户: 2,377 (+67), verified to post: 281 (+35)
* Telegram用户: 3,290 (-115)
* YouTube订阅: 3,800 (+13)
* Facebook粉丝: 3,253 (+23), likes: 2,983 (+19)
* LinkedIn粉丝: 591 (+24)
* GitHub dcrd 星星: 498 (+4), forks: 1,365 (+28)

## 治理

7月，[社区基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了15,517个DCR，并花费了10,344个DCR。使用7月份的每日平均DCR /美元汇率为28.97美元，这是收到的45万美元和30万美元的花费。这些付款用于6月完成的工作，费率为28.90美元。截至8月1日，财政部余额为627,514 DCR（1680万美元，26.75美元）。

7月，提交了2份新提案：:

* [Decred Fundamental Metrics Research Proposal - Phase 1](https://proposals.decred.org/proposals/78b50f218106f5de40f9bd7f604b048da168f2afbec32c8662722b70d62e4d36) 由@Checkmate提出, 要求12,000美元，为期3个月的研究和社交媒体工作，加上2000美元之前完成的工作([monetary premiums article](https://medium.com/@_Checkmatey_/monetary-premiums-can-altcoins-compete-with-bitcoin-54c97a92c6d4) article)）。投票已经结束，该提案得到了92％的支持。 

* [TinyDecred: A Python Toolkit for Decred](https://proposals.decred.org/proposals/20e967dad9e7398901decf3cfe0acf4e0853f6558a62607265c63fe791b8b124) 由@buck54321提出, 要求在TinyDecred上完成的工作需要8,000美元，这是一套用于与Python中的Decred区块链交互的工具。提案投票于8月6日开始，目前已获得89％的批准。

8月提交了另外5项提案，4项与做市商有关，1项与DEX发展有关。即将出版的Politeia摘要将深入介绍这些内容，并将在8月的月报中说明。

“Politeia 摘要t” 第[19期](https://medium.com/politeia-digest/issue-19-june-30-july-31-2019-c591fcb79d98)更详细地介绍了7月的提案活动和讨论。

已经准备了一个 [数据集](https://github.com/RichardRed0x/pi-research/blob/master/data/comments-and-updown-votes/pi-users.csv)和 [简短报告](https://github.com/RichardRed0x/pi-research/blob/master/analysis/comments-and-updown-votes/users-review.md)，它根据用户名聚合Politeia数据，生成每个用户评论和投票频率的准确数字，以及他们的评论得分情况。

## 网络

Hashrate：7月的哈希值以~503 Ph/s的速度开启，关闭了〜583 Ph/s，最低时达到319 Ph/s，整个月达到687 Ph/s。截至8月2日的池哈希值分布：F2Pool 21％，UUPool 19％，lab.antpool.com 16.5％，Poolin 9.5％，BTC.com 7.3％，Luxor 2.2％，BeePool 0.14％，Coinmine 0.12％，suprnova 0.08％和其他24％每个[dcrstats.com](https://dcrstats.com/pow)。池分布数是近似值。

根据dcrstats.com，7月5日观察到哈希值从550降至319 Ph/s，然后在约20小时内快速恢复。关于下降的原因及其准确性进行了长时间的[讨论](https://matrix.to/#/!NNzHoaSdnsbZDQOXJr:decred.org/$156245221914434sRKEL:decred.org)。

Staking: 每个dcrstats.com的30天平均票价为125.8 DCR（+5.8）。票价在118.8-129.5DCR之间变化。锁定金额为483-506万DCR，相当于可用供应量的48.25-49.84％。

自2017年7月选票难度算法共识变化以来，票价达到最高水平（129.46）。有人提出一个[论点](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$156359151625133psHEo:decred.org)，认为该值不应被视为“ATH”，因为在算法更改之前，选票的价格已经高达238.9 DCR。

有关[VSP数据](https://charts.dcr.farm/d/000000016/proof-of-stake-pools?orgId=1&from=1514764800000&to=now)的历史图表，请访问dcr.farm。最近在[dcrextdata](http://dcrextdata.raedahgroup.com/)上提供了类似的数据，但dcr.farm自2018年1月以来就有数据。设置一个长时间间隔揭示了VSP竞争的有趣趋势：

* dcr.stakeminer.com在6月份触底反弹至14％，并且自从收回超过15％的现场门票
* stakey.net在2019年从2.8％增长到6.9％的活票，这与其用户数量从300增加到500相关
* 自2018年10月成立以来，megapool增长到3.5％
* tokensmart有一条坎坷的发展道路：自2018年4月成立以来，它增长到2％，在2019年4月下降到0.8％，然后在6月迅速上升到接近3％，接着又下降到0.8％

错过的选票比例的移动平均线图也很有趣，可用于选择VSP。

Nodes: 整个 [7月份](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1561939200000&to=1564617600000)，每个dcr.farm大约有173个监听节点和360-530个节点。截至8月2日，大约70％运行dcrd v1.4.0,7.5％运行dcrwallet v1.4.0,6％运行v1.5.0（预）开发版本。

截至8月2日，DCR [闪电网络测试网](https://charts.dcr.farm/d/DHPdAO4Wz/lightning-network?orgId=1)显示网络拥有18个节点，52个信道，总容量为410 DCR。

## 整合

[Everstake](https://everstake.one/) 选票托管服务提供商Everstake[宣布](https://medium.com/everstake/welcome-decred-voting-on-everstake-b2d0371426ad)在[decred.everstake.one](https://decred.everstake.one/)上推出Decred VSP。

[Exodus](https://www.exodus.io/) 钱包[获得](https://twitter.com/exodus_io/status/1148593861549334528)了 Trezor对DCR管理和交换的支持。

[Vertbase](https://www.vertbase.com/)是一家提供法定货币的交易所，已上线DCR支付网关。该基金会将捐赠给Vertbase列出和支持的项目的开发，并由这些项目的贡献者核心团队成员组成。

[MixinNetwork](https://twitter.com/Mixin_Network/status/1153272304790433793) 集成Decred。在他们的[网站](https://mixin.one/)上，“Mixin是一个公开发行的分类账，旨在帮助其他公开分发的分类账获得数万亿的TPS，实现次级的最终确认，零交易费用，增强的隐私和无限的可扩展性。”

警告：Decred月报的作者不知道上述任何服务的可信度。在将您的个人信息或资产信任给任何实体之前，请先进行自己的研究。

## 采用

来自葡萄牙的蜜蜂产品制造商DrApis[宣布](https://twitter.com/drapiscom/status/1146539277028909058)他们接受DCR支付。

Blockhead Capital [宣布](https://twitter.com/jyashouafar/status/1152238301593657344)他们对Decred的投资，并分享了一份 [研究论文](https://www.blockheadcap.com/post/decred-investment-thesis)。他们的结论：

> Decred是一种具有严格货币政策的自适应加密货币。严格的货币政策提供了实现货币溢价所需的基础，而其链上治理的适应性允许整合更具活力的特性。混合共识机制在各个生态系统各方之间创造了充分的制衡，同时消除了有争议的硬件作为解决纠纷的主要方法 - 这是一个有抱负的全球储备资产的一个非常理想的特征。此外，混合共识创建了更安全的块容量，使块容量更有价值，并提供了更具审查性的货币。Decred迭代了比特币的优势并弥补了它的许多缺点，使其能够作为数字存储的价值来补充或与之竞争。

## 外联活动

教育基础设施在7月继续建设，这将有助于Decred简化外联活动和教育。网站更新已接近完成，并应在8月底之前生效，新的子页面包括Decred的安全性，适应性，自筹资金和历史记录。此外，我们已经就模式达成一致，目前正在组建一个基于Max Bronstein的[Canon](https://github.com/maxbron08/Decred-Canon)的资源库，这将有助于为参与#DecredChallenge的人们形成一个自然的学习空间。

为了实现这一点，我们稍微改进了消息传递，主要关注Decred的基本原则，因为所有消息都来自那里。这将在下周的聊天中出现，供社区参与。为社区提供的其他资源包括社交媒体手册，其中介绍了如何以建设性的方式与他人互动的最佳实践，这些实践很好地反映了Decred并帮助教育其他人关于项目。

此外，社区组织者手册将很快分享给社区。这有助于澄清角色和责任，以便在全球范围内实现一致，提高效率并分享最佳实践。在这些方面，Decred正在寻找地理营销线索，以帮助运营世界各地。来自不同地区的各种提案正在进行中，并且应该会在接下来的几个月内触及Politeia。我们仍然在寻找欧洲和亚洲的领导者，所以请加入我们的#marketing或#local_ops在Matrix讨论帮助分散组织。

我们还在努力协调一个为期一周的活动闪电战，该活动将于10月份在亚洲一些最重要的城市举办各种Decred社区活动。细节应在下个月内发布。

在[Murad Mahmudov](https://soundcloud.com/decredindepth/murad-mahmudov-dcr-investment-thesis-sov-narrative-crypto-economics)和[Permabull Nino](https://soundcloud.com/decredindepth/ep-5-decred-as-strong-accounting-ticket-metrics-with-permabull-nino)发行的深度录播发行，这些录音集非常受欢迎，并在社交媒体上引发了很多关于Decred的相关讨论。

Ditto的七月成就:

* 我们与各社区成员就推动在Twitter上采用高效/教育方式的策略和策略进行了升级。
* 建立了更广泛的Decred发言人名单，以及新的媒体目标愿望清单。
* 与社区讨论如何最好地为Decred标语建立可见性。
* 获得四次采访，并在发布时分享更多细节。
* 通过@ moo31337主持的采访，获得了财务咨询通讯Legacy Research的一篇文章。
* 通过@ jy-p讨论他对天秤座的看法以及Decred在成为DAO方面的进展，在[BlockTV](https://blocktv.com/watch/2019-07-30/5d404e65ea3f5-decred-s-jake-yocom-piatt-talks-decentralized-governance)上获得了10分钟的片段。
* 在CCN](https://www.ccn.com/news/libra-friend-or-foe/2019/07/21/)上有关Libra的@ jy-p's byline的安全发布。
* 与社区合作，扩大/参与宣布Decred的DEX规范的[#DEX推特风暴](https://twitter.com/decredproject/status/1156652694502817793)。
* 开启消息刷新，添加常见问题解答以解决常见的误解。
* 对Decred网站的教育资源库进行最后润色，使记者和新手更容易在一个地方找到我们。
* 制定长期媒体关系计划，针对Decred的所有受众（投资者，开发者，加密爱好者），以及过去未覆盖过Decred的媒体。
* 媒体培训是否正在与@ jy-p进行复习以准备接受广播采访。

## 社区活动

出席：

* 7月4日至5日 - [Blockchain Summit Latam](https://twitter.com/Decred_ES/status/1146093986806976513) - 墨西哥城，墨西哥。Ana Dalia 代表 Decred。会议结束后，Decred赞助了一个 [晚宴](https://twitter.com/Decred_ES/status/1147522846513618945)。
* 7月10日 - [Decred meetup](https://twitter.com/Decred_BR/status/1147201276058505216) - 巴西圣保罗。由@guisso组织。
* 7月10日 - [StakingCon](https://twitter.com/BlockBeatsChina/status/1147570186519638017) - 中国北京。@Dominic“设法吸引组织者插入Decred视频并参加圆桌会议讨论”。由@BlockBeatsChina组织。 ([照片](https://twitter.com/DecredCN/status/1148983482732830720))
* 7月11日 - [Staked US event](https://twitter.com/staked_us/status/1148687292032323584) - 美国纽约。Fireside与@joshuam聊天，由Staked和TokenTax共同主持。
* 7月19日 - Meetup - 阿根廷布宜诺斯艾利斯。这次聚会是为即将于8月12日举行的Crypto周一做准备。[@Camilolwi](https://twitter.com/Camilolwi) [宣发](https://twitter.com/cryptorocketok/status/1152260099072778240)了 Decred。由[Crypto Rocket Group](https://twitter.com/cryptorocketok)主办。
* 7月21日 - [OKEx meetup](https://twitter.com/wanbihou/status/1151704823533723648) - 中国青岛。与@Dominic聊天。
* 7月25日 - [算法+区块链节CDMX 2019](https://twitter.com/LegalHackersMX/status/1153832499333795840) - 墨西哥城，墨西哥。@elian [代表](https://twitter.com/elianhuesca/status/1154452590983299073)出席。
* 7月25 - 26日 - 2019年Cointime Summit - 越南胡志明市。Duyen Em向会议区的个人介绍了Decred。来自其他项目的一些演讲嘉宾已经熟悉并高度评价了Decred，但大多数越南人都只是在学习它。Duyen Em认为，Decred在越南蓬勃发展的加密货币领域应该有更大的影响力，并分享建立联系和发展社区的想法。完整报告将在Reddit上发布。
* 7月28日 - 越南Staking经济 - 越南胡志明市。Duyen Em代表Decred并向许多对加密货币感兴趣的年轻人回答了问题。有关详细信息，请参阅Cointime Summit的报告。
* 7月31日 - [Open Banking Summit](https://theopenbankingsummit.com/)初步聚会 - 墨西哥墨西哥城。@elian代表该项目并就Decred [发表了演讲](https://twitter.com/elianhuesca/status/1157313830969630725)。峰会将于11月13日开始。

即将到来的：

* 8月8日 - [Blockchain Bajio](https://www.eventbrite.com/e/blockchain-bajio-2do-meetup-tickets-66510186759) - Leon，瓜纳华托，墨西哥。
* 8月12日 - [Crypto Monday](https://www.meetup.com/Bitcoin-Argentina/events/263594472) - 阿根廷布宜诺斯艾利斯。加密周一是Espacio比特币的月度活动，Espacio比特币是一个与阿根廷主要比特币非政府组织比特币阿根廷有着强大联系的本地联合空间。
* 8月13日至14日 -[Futurist Conference](https://eventmobi.com/futurist/) - 加拿大多伦多。Decred宣布成为赞助商，并在“Blockchain Social Impact＆Governance for Good” 小组中有一个[圆桌论坛](https://twitter.com/decredproject/status/1157416657670868997)，其中@zubair将代表出席。
* 8月16日至18日 - [Campus Party Natal](https://brasil.campus-party.org/campus-party-natal/) - 巴西纳塔尔。@guisso将讨论Decred如何作为一个组织工作。
* 8月20日 - [Crypto Alchemy: Mining and Staking Decred](https://www.meetup.com/Philadelphia-Technology-for-Blockchain-and-Cryptocurrency/events/ffssfryzlbbc/) - 美国费城。由@mikeghen主办。
* 8月28日 - [Blockchain Bootcamp](https://www.blockchainbootcamp.net/) - 澳大利亚Docklands。@zohand和co被邀请参加区块链治理活动，作为其中一个主流的一部分。该活动是维多利亚州政府主办的年度数字创新节的一部分。
* 9月30日 - 10月1日 -  [Voice of Blockchain](https://twitter.com/BlockchainVoice/status/1154772731575099392) - 美国芝加哥。@ jy-p将发表主题演讲“为什么权力拆解下放和多利益相关方的包容性治理将获得无尽的寿命”。
* 11月4日至7日 - [Websummit](https://websummit.com/) - 葡萄牙里斯本。@ moo31337将在TBD面板上发言，而Decred将有一个2x2米的展位。

## 媒体

精选文章：

* Decred: What Gold and Bitcoin Wanted to Be by Pascal Thellmann ([seekingalpha.com](https://seekingalpha.com/instablog/49962360-pascal-thellmann/5324856-decred-gold-bitcoin-wanted))
* Monetary Premiums, Can Altcoins Compete with Bitcoin? by @Checkmate ([medium](https://medium.com/@_Checkmatey_/monetary-premiums-can-altcoins-compete-with-bitcoin-54c97a92c6d4))
* Libra: Friend or Foe? by @jy-p ([ccn.com](https://www.ccn.com/news/libra-friend-or-foe/2019/07/21/))
* Bitcoin & Decred / Historical Documents of a Digital Financial Revolution by BlackBearXVII ([medium](https://medium.com/@imagnusholdings/bitcoin-decred-historical-documents-of-a-digital-financial-revolution-4debfa0d10d9))
* Sovereign (Crypto) Networks by Joel Monegro ([placeholder.vc](https://www.placeholder.vc/blog/2019/7/31/lvhpfydo4m3uoezhwhicyxo06og0mn)) - mentions Decred as an example
* Introduction to Crypto-Accounting: An Analysis of Decred as an Accounting System by Permabull Nino ([medium](https://medium.com/@permabullnino/introduction-to-crypto-accounting-an-analysis-of-decred-as-an-accounting-system-4d3e67fce28))
* Blockhead Capital: Decred Investment Thesis ([blockheadcap.com](https://www.blockheadcap.com/post/decred-investment-thesis))

翻译：

* @Dominic将整个[Decred DEX](https://github.com/decred/dcrdex/blob/master/README.mediawiki)规范文本翻译成[中文](https://github.com/DominicTing/dcrdexStandard-CN-/blob/master/README.mediawiki)。该链接已提交至中国Binance [信息页面](https://info.binance.com/cn/currencies/decred)。
* Decred的5月和6月月报被翻译成阿拉伯语（@arij），中文（@Dominic，@ guang，@ Changhugo），意大利语和俄语（@DZ），波兰语（@kozel）和越南语（Duyen Em）。谢谢你们。

视频：

* Libra: 朋友还是敌人？- [Block TV](https://blocktv.com/watch/2019-07-30/5d404e65ea3f5-decred-s-jake-yocom-piatt-talks-decentralized-governance)@ jy-p采访

音频：

* Decred in Depth Ep. 4 Murad Mahmudov - DCR投资论文+ SoV叙事+加密经济学 ([libsyn](https://decredindepth.libsyn.com/murad-mahmudov-dcr-investment-thesis-sov-narrative-crypto-economics-0), [soundcloud](https://soundcloud.com/decredindepth/murad-mahmudov-dcr-investment-thesis-sov-narrative-crypto-economics), [twitter](https://twitter.com/decredproject/status/1150836740665552896))
* Decred in Depth Ep. 5 Permabull Nino - Decred 被认为是强大的会计+票务指标 ([libsyn](https://decredindepth.libsyn.com/ep-5-decred-as-strong-accounting-ticket-metrics-with-permabull-nino-0), [twitter](https://twitter.com/decredproject/status/1157000762611896320))
* POV Crypto: Decred: Luke Powell拆分比特币和以太币之间的差异 ([medium](https://medium.com/@TrustlessState/decred-splitting-the-difference-between-bitcoin-and-ethereum-with-luke-powell-758cf6e1218d), [libsyn](http://povcryptopod.btc.libsynpro.com/decred-splitting-the-difference-between-bitcoin-and-ethereum))
* The Sound Money Podcast: @joshuam的链上原子交换 ([spotify](https://open.spotify.com/episode/1SuzMUUmtm6xR7ofGN6t4a), [itunes](https://podcasts.apple.com/us/podcast/the-sound-money-podcast/id1470774235?i=1000443695629))

## 社区讨论

通讯系统新闻：

* [chat.decred.org](https://chat.decred.org/)现在托管Matrix协议的Riot Web客户端。自托管有很多好处吗，最明显的一点是[链接](https://decred.org/matrix/) 很容易记住，并且让新手更快地设置- 新人常常对正确设置homeserver感到困惑。不太明显的好处是，它有助于在[四月月报](201904.md)的matrix.org服务器泄露事件期间保持联系。最后，通过从注册页面中删除Google重新获取指纹识别并减少到外部域的流量来增加[隐私](https://github.com/decredcommunity/issues/issues/25)。并非每个项目都能够承担自我托管这样的基础设施并且具有自主性。非常感谢我们的管理员向导。
* 在发布新版本后，Riot用户现在可以[编辑](https://medium.com/@RiotChat/%EF%B8%8Fmessage-editing-%EF%B8%8F-reactions-5cffec8f71a2)他们的消息。Riot用户请注意，编辑您的消息将通过桥梁将其重播给使用Slack和Discord的人。

主题:

* #DecredChallenge [开始于](https://twitter.com/_Checkmatey_/status/1145764832362319872)7月1日，当时@Checkmate挑战Bitcoiners花了一个月的时间研究Decred，并且认为它不应该是＃2，邀请那些没有被说服其优点的人参与辩论。它[迅速](https://twitter.com/RichardRed0x/status/1146132909713240065) [发展](https://twitter.com/_Checkmatey_/status/1146136667448913921)成为一个模仿传递行为，得到一个[哈希标签](https://twitter.com/Ammarooni/status/1146171552213479425)，然后（主要是感谢@Checkmate）它成长为一个推文过程的原因，为什么Decred值得认真调查（见下文）。
* 另一篇[文章](https://bravenewcoin.com/insights/decred-price-analysis-a-sustained-increase-in-mining-activity-2)将Decred描述为“比特币分叉”，可能基于[CoinMarketCap](https://coinmarketcap.com/currencies/decred/)和[Messari](https://messari.io/asset/decred)的描述中使用该术语（公平地说，使用更有限的“比特币代码库分叉”）。这是一个让社区感到沮丧的错误特征，因为“比特币分叉”通常被解释为分配比特币核心软件和/或BTC UTXO集合的硬币 - 在Decred中不是这样。“比特币分叉”并没有反映出Decred的软件是由创建Decred的从头开始创建的事实，从btcd开始，这是比特币全节点的独立Go实现。@lukebp 发推文关于这一点并收到Messari的回应，@ Checkmate 扩展了@lukebp的评论，以便在#DecredChallenge中创建另一个章节。
* @Ammarooni采取了#DecredChallenge并提出了一些担忧，涉及与非法提案的利益相关者责任相关的攻击媒介以及LLC对资金扣押的敏感性。@lukebp和@jz回答了Decred如何向完整DAO迈进的解释，以及这将如何解决这些问题。
* 是否更改了Decred的最小单位（原子）的名称或将名称中的“信用”整合到另一个面额中的主题在[Twitter](https://twitter.com/OfficialCryptos/status/1151603316167720960)上出现，并在聊天和GitHub [issue](https://github.com/decredcommunity/issues/issues/129)中进行了讨论。开发人员指出，“原子”在Decred代码库中使用了数千次，这阻碍了一些支持者的改变而不是其他支持者。

@Checkmate在Twitter上一直非常活跃，并围绕#DecredChallenge和#DontSleepOnDecred主题标签产生良好的参与度，这里有一些亮点：

* [公布](https://twitter.com/_Checkmatey_/status/1148682397875167233) 货币溢价
* [非比特币分叉](https://twitter.com/_Checkmatey_/status/1155901635257929728)
* [Skin in the game](https://twitter.com/_Checkmatey_/status/1148354974390390784)
* [对冲](https://twitter.com/_Checkmatey_/status/1149560942654414848) Bitcoiners和Ethereuns
* [区分](https://twitter.com/_Checkmatey_/status/1150831105081298944)重点
* [社区基金](https://twitter.com/_Checkmatey_/status/1157342578787913733)
* [Politeia 提案](https://twitter.com/_Checkmatey_/status/1156293040509739010)
* [数字有机体](https://twitter.com/_Checkmatey_/status/1155567971823226881) 旨在提供最具弹性的方案

其他选定的推文：

* #DecredChallenge：找到一个工程团队，挑战自己的[力量和影响](https://twitter.com/RichardRed0x/status/1146917561751212032)，就像Company 0 Decred 那样严谨
* Chris Burniske让他对 Decred项目[感兴趣](https://twitter.com/lefebvre_dustin/status/1156316679040901125)
* Decred的混合PoW + PoS [支持](https://twitter.com/NoahPierau/status/1155466908738686977) 3种正式的治理机制
* Decred月报目前发布在[Binance](https://twitter.com/Binance_Info/status/1153575996487954432)信息栏中

@lukebp的 [推文](https://twitter.com/lukebp_/status/1154398108538658816)发表:

> 技术变革很难预测。协议需要能够适应这些变化。决定这些变化的人应该是这个游戏中的人，即利益相关者。

选定的Reddit讨论:

* Decred [社区发展](https://www.reddit.com/r/decred/comments/c9xtml/decred_community_growth/)
* 我是[来自未来的时间旅行者](https://www.reddit.com/r/decred/comments/c9jxml/i_am_a_timetraveler_from_the_future_here_to_beg/), 希望你继续你的工作
* 建议删除#random聊天室
* 关注并讨论过去的Reddit[提议](https://www.reddit.com/r/decred/comments/cb7g8g/general_is_there_an_optimal_rdecred_format_that/)；报告、编辑式论坛、行动语言
* [贡献者支付](https://www.reddit.com/r/decred/comments/cf773y/discussion_per_delivery_vs_per_hour/)隐私与利益相关者透明度之间的平衡
The balance between privacy of individual [贡献者支付]
* 选票持有人是否可以确保[双重花费](https://www.reddit.com/r/decred/comments/cgz12h/in_a_scenario_in_which_a_miner_submits_a_block/)的区块没有得到验证，以及选票持有人在防止51％攻击中的作用
* Decred的[governance model](https://www.reddit.com/r/decred/comments/cirkvr/decreds_governance_model/);
* 为什么Decred会[胜利](https://www.reddit.com/r/decred/comments/cc8c0h/why_decred_wins_in_the_end_incrementalism/)？

## 市场表现

7月份DCR的交易价格为25.20-35.64USD，0.00262-0.00296BTC。平均每日为28.97美元。

在快速达到1.3万美元的价格之后，比特币价格开始下跌，在7月的大部分时间里，比特币的价格都维持在1万美元上方。

## 相关外部信息

Placeholder VC的Chris Burniske（Decred和Zcash的持有人）提供了一份关于创始者奖励到期时Zcash社区面临的情况的摘要，主张继续在未来4年内，将20%的区块奖励用于项目开发，其中70%用于“协议开发”，30%用于“增长基金”。

Zooko Wilcox发表了一封说明关于新Zcash-dev基金的可能性，这说明他始终知道资金将耗尽并创建一个只有通过“混乱和困难的过程”才能解决的问题，如Zcash社区目前正在经历。Zooko再次表示，他不能是做出决定的人，决定应该来自社区，但作为ECC的首席执行官，他在社区中具有相当大的影响力，社区没有既定的决策方法。

正在考虑的所有各种选项都已在此兆量级中得到了有益的总结。 正如Chris Burniske在其帖子中所说，第一个问题是如何以一种被认为合法的方式做出有关决定的决定。 考虑到时间限制，Chris主张使用轮询来衡量对各种选项的偏好，并使用ECC和Zcash Foundation 2-of-2 multisig做出最终决定。 Zooko表示，ECC将在8月初宣布一种决策方法。

Neblous宣布了一轮325万美元的种子轮的融资，并有许多风险投资家参与。

在以太坊社区，资金也是一些讨论的主题，更加关注EIP-2025，它将在18个月内每个区块增加0.0055 ETH（总计17K ETH），为ETH 1.x开发提供资金（因为主要开发商关注ETH 2.0）。区块奖励将用于偿还贷款，在4个不同领域工作的团队将收到多个合同地址。

与任何有争议的以太坊改进方案一样，外界很难知道EIP-2025是否会走向任何地方。Vitalik发来的一条微博说，它似乎没有多少支持，这可能表明它不会被列入伊斯坦布尔的“硬叉”计划。

另一篇关于以太坊的Circle研究文章关注的是由Consensys创建的Infura服务公司的中心性，该公司允许DAPP开发人员回避设置和运行自己的节点。文章认为，由于全节点运行的难度和需求量的增加（空间需求量同比增长25-48%），导致全节点数量从2018年12月的12000个减少到2019年7月的8000个。Infura很受欢迎，因为它允许以太坊开发者避免直接与区块链连接带来的不便，但它为50000个dapp和依赖它的开发者引入了一个中心故障点。反过来，infura依靠AWS服务来运行其节点。

甜甜圈实验，其中subreddit参与者根据他们的subreddit业力赚取积分并使用这些参与民意调查，正在进入另一个阶段。已经准备好智能合约，允许将甜甜圈转移到以太坊区块链，而一些Reddit管理员正在Reddit端为此提供便利。由于社区对链条治理的担忧，由于甜甜圈正在“分散”，民意调查将成为非约束性信号投票。根据对公告的评论，这似乎是一个有争议的选择，并且对于甜甜圈的目的存在一些混淆。

Aragon [完成](https://blog.aragon.org/final-results-from-aragon-network-vote-3/)了第三轮治理建议投票，提交了11项提案，8项被允许纳入阿拉贡协会投票。其中7项提案获得批准，所有提案均为99％或更高，4项获得一致通过（1项或更少的ANT代币投票否决）。在8个提案中，ANT投票率平均为2.6％。

[AGP-64](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-64.md)表示支持安静结束投票，如果结果在投票结束时翻转，这将延长AGP投票的持续时间。这是对鲸鱼后期投票影响先前AGP结果的观察结果的回应。该提案没有具体说明具体的实施方案，但表明支持将资源用于为阿拉贡开发安静的结束投票。

[AGP-59](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-59.md) 要求AGP提交的讨论期限最短。[AGP-70](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-70.md)表示支持将Nest授权计划的管理从Aragon Association转移到DAO，AGP-71将Nest计划的预算扩展到600K DAI和300K ANT。 [AGP-73](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-73.md)是最大的预算提案，进一步为Autark提供了160万DAI和487K ANT的资金，为期一年。被拒绝的提案要求为Aragon投票开发本机移动应用程序。

Dash [完成](https://blog.dash.org/the-dash-investment-foundation-supervisor-election-results-96a28309744b)第一次年度选举仓，作为短跑投资基金的监管，使用一些软件定制制造用于这一目的。

在TzScan Baker的布雷斯特提案未能取得足够的进展支持后，另一轮Tezos协议修正程序正在进行中。Cryptium实验室注入上月2名为巴比伦建议，与游牧实验室共同编制的，于7月26日，然后经修订的2.0版这项建议将作出一些更改协议，包括一致性算法和新迈克尔逊的一个新变种特征和新提案的法定人数要求将被引入，这将阻止具有最多upvotes的提案进展到第二阶段，除非它得到至少5％的股份支持。这将允许很少支持的提议（如布雷斯特）早先被拒绝，然后提案周期更快地重新启动。

0x分散交换协议团队宣布第三方安全研究人员报告了一个安全漏洞，并作为预防措施关闭了交换合同。0x智能合约管道在第二天被修补并重新部署。

StopAndDecrypt发布了挖掘池如何滥用其所信任的散列能力的方法概述，并为BetterHash提供了案例 - BetterHash的替代挖掘协议的工作名称旨在将权力交还给各个矿工并剥离其影响的采矿池。

后门潜入 Ruby库以检查密码强度。注入的恶意软件从pastebin.com获取并运行代码，使攻击者能够远程执行代码。具有讽刺意味的是，劫持是可能的，因为密码强度检查库的作者具有弱且重用的密码，并且他的RubyGems帐户上没有2FA。在一个使用自动化工具盲目地吸引数十个或数百个依赖关系的世界中，审核依赖关系非常重要。

OpenPGP密钥服务器网络受到证书泛滥攻击。有人为两名GnuPG贡献者的公钥上传了大量的认证，有效地“毒害”了他们。任何试图将中毒密钥导入易受攻击的安装的人都有可能因为性能大幅下降而使密钥环无法使用。密钥服务器网络设计的缺陷早已为人所知。它基本上维护了一个分散的审查抗性只写数据库，但没有强大的滥用保护。在已知这个漏洞的十多年中，网络无法协调升级的开发和部署。这再一次提醒我们，设计一个有弹性的分散协议是多么具有挑战性，以及分散式网络有一个适应治理机制的重要性。

## 关于月报

这是Decred月报的第16期。[这里](https://xaur.github.io/decred-news/)提供所有问题，镜像和翻译的索引。

来自第三方的大多数信息在经过小范围的检查后直接转发。Decred月报的作者无法验证所有声明。请注意诈骗并做自己的研究。

我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢(字母排列):

* 编写和编辑： bee, cryptoleslie, degeri, Dustorf, lukebp, raedah, richardred, s\_ben
* 评论和反馈： chappjc, davecgh, jholdstock, jy-p, margaret\_mei, matheusd

## 中文社区

* [社区web](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [优酷频道](https://i.youku.com/decredproject)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)
