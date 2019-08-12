# Decred Journal – July 2019

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

[Everstake](https://everstake.one/), provider of staking services, [announced](https://medium.com/everstake/welcome-decred-voting-on-everstake-b2d0371426ad) the launch of their Decred VSP at [decred.everstake.one](https://decred.everstake.one/).

[Exodus](https://www.exodus.io/) wallet [gained](https://twitter.com/exodus_io/status/1148593861549334528) Trezor support for managing and exchanging of DCR.

[Vertbase](https://www.vertbase.com/), an exchange offering DCR with a fiat gateway, [announced](https://twitter.com/vertbase/status/1147840898564120577) that they will be starting a foundation. An interesting event in the space, the foundation will donate to the development of projects that Vertbase lists and supports, and have its board composed of volunteer core team members from these project.

[MixinNetwork](https://twitter.com/Mixin_Network/status/1153272304790433793) integrated Decred. From their [website](https://mixin.one/), "Mixin is a publicly distributed ledger aimed to help other publicly distributed ledgers gain trillions of TPS, achieve sub second final confirmations, zero transaction fees, enhanced privacy, and unlimited extensibility.".

Warning: the authors of Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## 采用

Portuguese unprocessed honeybee products maker DrApis [announced](https://twitter.com/drapiscom/status/1146539277028909058) that they accept DCR.

Blockhead Capital [announced](https://twitter.com/jyashouafar/status/1152238301593657344) their investment in Decred and shared a [research paper](https://www.blockheadcap.com/post/decred-investment-thesis). Their conclusion:

> Decred is an adaptive cryptocurrency with a rigid monetary policy. The rigid monetary policy provides the base required to achieve monetary premium while the adaptive nature of its on-chain governance allows for integration of more dynamic features. The hybrid consensus mechanism creates adequate checks and balances between the various ecosystem parties while eliminating contentious hardforks as the primary method to resolve disputes - a highly desirable feature for an aspiring global reserve asset. Further, the hybrid consensus creates for more secure blockspace, making the blockspace more valuable, and provides for a more censorship resistant currency. Decred iterates on Bitcoin's strengths and shores up many of its shortcomings, putting it in a position to complement or compete with it as a digital store of value.

## 外联活动

Infrastructure continued to build in July that will help Decred streamline outreach and education. The website update is close to complete, and should be live by the end of August with new subpages on Decred's Security, Adaptability, Self-Funding, and History. Additionally, we've agreed upon a schema and are currently assembling a resource repository building on Max Bronstein's [Canon](https://github.com/maxbron08/Decred-Canon) that will help form a natural funnel of learning for people taking the #DecredChallenge.

In order to achieve this, we're slightly refining the messaging, focusing largely on the fundamental principles of Decred, as all messaging flows from there. That will appear in chat within the next week for community input. Other resources for the community that have been in the works include the Social Media Playbook, featuring best practices for how to engage with others in a constructive way that reflects well on Decred and helps educate others about the project.

Additionally, a Community Organizer Handbook will be shared for community input shortly. This well help clarify roles and responsibilities in order to gain alignment, improve efficiency, and share best practices around the world. Along these lines, Decred is looking for geographic marketing leads to help run areas of the world. Various proposals from different regions are in the works, and should hit Politeia in the next couple of months. We are still looking for leaders in Europe and Asia, so join us in #marketing or #local\_ops in Matrix to discuss helping to decentralize the organization.

We're also working to coordinate a week-long events blitz in October featuring various Decred community members in some of the most important cities across Asia. Details should be released within the next month.

Decred in Depth episodes featuring [Murad Mahmudov](https://soundcloud.com/decredindepth/murad-mahmudov-dcr-investment-thesis-sov-narrative-crypto-economics) and [Permabull Nino](https://soundcloud.com/decredindepth/ep-5-decred-as-strong-accounting-ticket-metrics-with-permabull-nino) were released which were very well received and created a lot of chatter about Decred on social media.

Ditto's July achievements:

* Escalated our work with various community members on strategies and tactics for engaging in a productive/educational way on Twitter.
* Built out a wider list of Decred spokespeople, along with a new wish list of media targets.
* Strategized with the community on how to best build visibility for the Decred tagline.
* Secured four interviews, and will share more details when published.
* Secured an article in financial advisory newsletter, Legacy Research, as a result of an interview we hosted with @moo31337.
* Secured a 10-minute segment on [BlockTV](https://blocktv.com/watch/2019-07-30/5d404e65ea3f5-decred-s-jake-yocom-piatt-talks-decentralized-governance) with @jy-p discussing his take on Libra and how Decred's progress towards becoming a DAO.
* Secured publication of @jy-p's byline on Libra in [CCN](https://www.ccn.com/news/libra-friend-or-foe/2019/07/21/).
* Worked with the community to amplify/engage with the [#DEX tweet storm](https://twitter.com/decredproject/status/1156652694502817793) announcing Decred's DEX spec.
* Began a messaging refresh, adding FAQs to counter common misunderstandings.
* Put the finishing touches on the schema for an educational resources repository for the Decred website that makes it easier for journalists and newbies to find out about us in one place.
* Put together a long-term media relations plan that targets all of Decred's audiences (investors, developers, crypto enthusiasts), as well as media who haven't covered Decred in the past.
* Did media training refresher with @jy-p to prepare for broadcast interviews.

## 社区活动

Attended:

* Jul 4-5 - [Blockchain Summit Latam](https://twitter.com/Decred_ES/status/1146093986806976513) - Mexico City, Mexico. Ana Dalia [represented](https://twitter.com/AnaDaliacd23/status/1146873685229416450) Decred. After the conference there was a [dinner](https://twitter.com/Decred_ES/status/1147522846513618945) sponsored by Decred.
* Jul 10 - [Decred meetup](https://twitter.com/Decred_BR/status/1147201276058505216) - São Paulo, Brazil. Organized by @guisso.
* Jul 10 - [StakingCon](https://twitter.com/BlockBeatsChina/status/1147570186519638017) - Beijing, China. @Dominic "managed to charm the organizer to slot in a Decred video and particpated in the roundtable discussion". Organized by @BlockBeatsChina. ([photos](https://twitter.com/DecredCN/status/1148983482732830720))
* Jul 11 - [Staked US event](https://twitter.com/staked_us/status/1148687292032323584) - New York, USA. Fireside chat with @joshuam, co-hosted by Staked and TokenTax.
* Jul 19 - Meetup - Buenos Aires, Argentina. The meetup was a preparation for the upcoming Crypto Monday on Aug 12. [@Camilolwi](https://twitter.com/Camilolwi) [presented](https://twitter.com/cryptorocketok/status/1152260099072778240) Decred. Hosted by [Crypto Rocket Group](https://twitter.com/cryptorocketok).
* Jul 21 - [OKEx meetup](https://twitter.com/wanbihou/status/1151704823533723648) - Qingdao, China. Chat with @Dominic.
* Jul 25 - [Computational Law + Blockchain Festival CDMX 2019](https://twitter.com/LegalHackersMX/status/1153832499333795840) - Mexico City, Mexico. @elian [represented](https://twitter.com/elianhuesca/status/1154452590983299073) the project.
* Jul 25-26 - Cointime Summit 2019 - Ho Chi Minh City, Vietnam. Duyen Em introduced Decred to individuals in the conference area. Some guest speakers from other projects were already familiar and spoke highly of Decred, but most Vietnamese speakers are just learning about it. Duyen Em suggests that Decred deserves a much bigger presence in the thriving cryptocurrency space of Vietnam and shares ideas for establishing connections and growing the community. Full report will be published on Reddit.
* Jul 28 - Vietnam Staking Economy - Ho Chi Minh City, Vietnam. Duyen Em represented Decred and answered questions to many young people interested in cryptocurrencies. The details are in the report for Cointime Summit.
* Jul 31 - [Open Banking Summit](https://theopenbankingsummit.com/) preliminary meetup - Mexico City, Mexico. @elian represented the project and [gave a talk](https://twitter.com/elianhuesca/status/1157313830969630725) on Decred. The summit will start on Nov 13.

Upcoming:

* Aug 8 - [Blockchain Bajio](https://www.eventbrite.com/e/blockchain-bajio-2do-meetup-tickets-66510186759) - Leon, Guanajuato, Mexico.
* Aug 12 - [Crypto Monday](https://www.meetup.com/Bitcoin-Argentina/events/263594472) - Buenos Aires, Argentina. Crypto Monday is a monthly event hosted at Espacio Bitcoin, a local coworking space with a strong bond with the main Argentina Bitcoin NGO, Bitcoin Argentina.
* Aug 13-14 - [Futurist Conference](https://eventmobi.com/futurist/) - Toronto, Canada. Decred announced as a sponsor and has a slot on the [panel](https://twitter.com/decredproject/status/1157416657670868997) "Blockchain Social Impact & Governance for Good", where @zubair will represent the project.
* Aug 16-18 - [Campus Party Natal](https://brasil.campus-party.org/campus-party-natal/) - Natal, Brazil. @guisso will talk about how Decred works as an organization.
* Aug 20 - [Crypto Alchemy: Mining and Staking Decred](https://www.meetup.com/Philadelphia-Technology-for-Blockchain-and-Cryptocurrency/events/ffssfryzlbbc/) - Philadelphia, USA. Hosted by [@mikeghen](https://twitter.com/mikeghen/status/1155594343702511616).
* Aug 28 - [Blockchain Bootcamp](https://www.blockchainbootcamp.net/) - Docklands, Australia. @zohand and co have been [invited](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15644812201506dzVgU:decred.org) to run a blockchain governance event as part of one of the main streams. The event is part of the annual [Digital Innovation Festival](https://dif.vic.gov.au/) hosted by Victorian State Government.
* Sep 30 - Oct 1 - [Voice of Blockchain](https://twitter.com/BlockchainVoice/status/1154772731575099392) - Chicago, USA. @jy-p will present a keynote "Why Direct Sovereignty & Multi-Stakeholder Inclusive Governance Will Last".
* Nov 4-7 - [Websummit](https://websummit.com/) - Lisbon, Portugal. @moo31337 will speak on a panel TBD, and Decred will have a 2x2m exhibit booth.

## 媒体

Selected articles:

* Decred: What Gold and Bitcoin Wanted to Be by Pascal Thellmann ([seekingalpha.com](https://seekingalpha.com/instablog/49962360-pascal-thellmann/5324856-decred-gold-bitcoin-wanted))
* Monetary Premiums, Can Altcoins Compete with Bitcoin? by @Checkmate ([medium](https://medium.com/@_Checkmatey_/monetary-premiums-can-altcoins-compete-with-bitcoin-54c97a92c6d4))
* Libra: Friend or Foe? by @jy-p ([ccn.com](https://www.ccn.com/news/libra-friend-or-foe/2019/07/21/))
* Bitcoin & Decred / Historical Documents of a Digital Financial Revolution by BlackBearXVII ([medium](https://medium.com/@imagnusholdings/bitcoin-decred-historical-documents-of-a-digital-financial-revolution-4debfa0d10d9))
* Sovereign (Crypto) Networks by Joel Monegro ([placeholder.vc](https://www.placeholder.vc/blog/2019/7/31/lvhpfydo4m3uoezhwhicyxo06og0mn)) - mentions Decred as an example
* Introduction to Crypto-Accounting: An Analysis of Decred as an Accounting System by Permabull Nino ([medium](https://medium.com/@permabullnino/introduction-to-crypto-accounting-an-analysis-of-decred-as-an-accounting-system-4d3e67fce28))
* Blockhead Capital: Decred Investment Thesis ([blockheadcap.com](https://www.blockheadcap.com/post/decred-investment-thesis))

Translations:

* @Dominic translated the whole [Decred DEX spec](https://github.com/decred/dcrdex/blob/master/README.mediawiki) draft into [Chinese](https://github.com/DominicTing/dcrdexStandard-CN-/blob/master/README.mediawiki). The link was submitted to Chinese Binance [info page](https://info.binance.com/cn/currencies/decred).
* May and June issues of Decred Journal were translated to Arabic (@arij), Chinese (@Dominic, @guang, @changhugo), Italian and Russian (@DZ), Polish (@kozel) and Vietnamese (Duyen Em). Thank you all.

Videos:

* Libra: Friend or Foe? - @jy-p interview on [Block TV](https://blocktv.com/watch/2019-07-30/5d404e65ea3f5-decred-s-jake-yocom-piatt-talks-decentralized-governance)

Audio:

* Decred in Depth Ep. 4 Murad Mahmudov - DCR Investment Thesis + SoV Narrative + Crypto Economics ([libsyn](https://decredindepth.libsyn.com/murad-mahmudov-dcr-investment-thesis-sov-narrative-crypto-economics-0), [soundcloud](https://soundcloud.com/decredindepth/murad-mahmudov-dcr-investment-thesis-sov-narrative-crypto-economics), [twitter](https://twitter.com/decredproject/status/1150836740665552896))
* Decred in Depth Ep. 5 Permabull Nino - Decred as Strong Accounting + Ticket Metrics ([libsyn](https://decredindepth.libsyn.com/ep-5-decred-as-strong-accounting-ticket-metrics-with-permabull-nino-0), [twitter](https://twitter.com/decredproject/status/1157000762611896320))
* POV Crypto: Decred: Splitting the Difference Between Bitcoin and Ethereum with Luke Powell ([medium](https://medium.com/@TrustlessState/decred-splitting-the-difference-between-bitcoin-and-ethereum-with-luke-powell-758cf6e1218d), [libsyn](http://povcryptopod.btc.libsynpro.com/decred-splitting-the-difference-between-bitcoin-and-ethereum))
* The Sound Money Podcast: On-Chain Atomic Swaps with @joshuam ([spotify](https://open.spotify.com/episode/1SuzMUUmtm6xR7ofGN6t4a), [itunes](https://podcasts.apple.com/us/podcast/the-sound-money-podcast/id1470774235?i=1000443695629))

## 社区讨论

Comm systems news:

* [chat.decred.org](https://chat.decred.org/) now hosts the Riot web client for the Matrix protocol. There are multiple [advantages](https://github.com/decredcommunity/issues/issues/62) of self-hosted Riot. The most visible one is that the link is easy to remember and sets you up faster than the [onboarding page](https://decred.org/matrix/) - new people were often confused about setting the homeserver correctly. Less obvious benefit is that it helps to stay connected during incidents like the matrix.org server compromise reported [in April](201904.md). Finally, the [privacy](https://github.com/decredcommunity/issues/issues/25) is increased by removing Google recaptcha fingerprinting from the registration page and reducing the traffic to external domains. Not every project can afford to self-host such infrastructure and be autonomous. Huge thanks to our admin wizards.
* Riot users are now enjoying reactions and can edit their messages, following the [release](https://medium.com/@RiotChat/%EF%B8%8Fmessage-editing-%EF%B8%8F-reactions-5cffec8f71a2) of new versions. Riot users please be aware that editing your messages will replay them across the bridge to people using Slack and Discord.

Selected topics:

* The #DecredChallenge [started](https://twitter.com/_Checkmatey_/status/1145764832362319872) on Jul 1 when @Checkmate challenged Bitcoiners to spend a month looking into Decred and come out believing it should not be #2, inviting people who are not persuaded of its merits to engage in a debate about it. It [evolved](https://twitter.com/RichardRed0x/status/1146132909713240065) [quickly](https://twitter.com/_Checkmatey_/status/1146136667448913921) into a meme, got a [hash tag](https://twitter.com/Ammarooni/status/1146171552213479425), and then (thanks mostly to @Checkmate) it grew into a tweet course of reasons why Decred merits serious investigation (see below).
* Another [article](https://bravenewcoin.com/insights/decred-price-analysis-a-sustained-increase-in-mining-activity-2) was published which described Decred as a "Bitcoin fork", likely based on the use of this term in descriptions on [CoinMarketCap](https://coinmarketcap.com/currencies/decred/) and [Messari](https://messari.io/asset/decred) (which, to be fair, uses the more limited "Bitcoin codebase fork"). This is a mischaracterization which frustrates the community because "Bitcoin fork" would usually be interpreted to mean a coin which forked the Bitcoin Core software and/or BTC UTXO set - neither of which are true in Decred's case. "Bitcoin fork" does not reflect the fact that Decred's software was created from scratch by the same people who launched Decred, beginning its life as btcd, an independent Go implementation of a Bitcoin full node. @lukebp [tweeted](https://twitter.com/lukebp_/status/1155886623147429889) about this and received a response from Messari, @Checkmate [expanded](https://twitter.com/_Checkmatey_/status/1155901635257929728) on @lukebp's comment to produce another chapter in the #DecredChallenge.
* @Ammarooni took the #DecredChallenge and came out with some [concerns](https://twitter.com/Ammarooni/status/1148013517016113152) about attack vectors related to stakeholder liability for illegal proposals and the susceptibility of the LLC to seizure of funds. @lukebp and @jz responded with an explanation of how Decred is moving towards a full DAO and how this will address the issues.
* The subject of whether to change the name for Decred's smallest units (atoms) or to integrate "credits" in the names for another denomination came up on [Twitter](https://twitter.com/OfficialCryptos/status/1151603316167720960) and was discussed in chats and in this GitHub [issue](https://github.com/decredcommunity/issues/issues/129). Developers pointed out that "atom" is used thousands of times in the Decred codebase, which discouraged some proponents of the change but not others.

@Checkmate has been very active on Twitter and generating good engagement around the #DecredChallenge and #DontSleepOnDecred hashtags, here are some highlights:

* [Announcement](https://twitter.com/_Checkmatey_/status/1148682397875167233) of the Monetary Premiums article
* [Not a Bitcoin fork](https://twitter.com/_Checkmatey_/status/1155901635257929728)
* [Skin in the game](https://twitter.com/_Checkmatey_/status/1148354974390390784)
* [The hedge](https://twitter.com/_Checkmatey_/status/1149560942654414848) for Bitcoiners and Ethereuns
* [Differentiate](https://twitter.com/_Checkmatey_/status/1150831105081298944) where it matters
* [Treasury Fund](https://twitter.com/_Checkmatey_/status/1157342578787913733)
* [Politeia Proposals](https://twitter.com/_Checkmatey_/status/1156293040509739010)
* [A digital organism](https://twitter.com/_Checkmatey_/status/1155567971823226881) designed to deliver the most resilient sound money

Other selected tweets:

* #DecredChallenge: Find an engineering team that takes the challenge of [limiting its own power](https://twitter.com/RichardRed0x/status/1146917561751212032) and influence as seriously as Company 0 has done with Decred
* Chris Burniske on what got him [interested](https://twitter.com/lefebvre_dustin/status/1156316679040901125) in the Decred project
* Decred's hybrid PoW + PoS [enables](https://twitter.com/NoahPierau/status/1155466908738686977) 3 formal governance mechanisms
* The Decred Journal is now being [circulated](https://twitter.com/Binance_Info/status/1153575996487954432) on Binance Info

@lukebp's Decred investment thesis in one [tweet](https://twitter.com/lukebp_/status/1154398108538658816):

> Technological change is hard to predict. A protocol needs to be able to adapt to those changes. The people making decisions about those changes should be the people with skin in the game, i.e. the stakeholders.

Selected Reddit threads:

* Decred [community growth](https://www.reddit.com/r/decred/comments/c9xtml/decred_community_growth/)
* I am a [time-traveler from the future](https://www.reddit.com/r/decred/comments/c9jxml/i_am_a_timetraveler_from_the_future_here_to_beg/), here to beg you to continue what you are doing
* [Suggestion](https://www.reddit.com/r/decred/comments/casb4b/decred_project_live_chat_infrastructure/) to remove #random chat room
* Format to keep an eye and discuss [past proposals](https://www.reddit.com/r/decred/comments/cb7g8g/general_is_there_an_optimal_rdecred_format_that/); reporting, Reddit-like forum, language of doing
* The balance between privacy of individual [contractor payments](https://www.reddit.com/r/decred/comments/cf773y/discussion_per_delivery_vs_per_hour/) and transparency for stakeholders
* Whether stakers can ensure that a block with a [double spend](https://www.reddit.com/r/decred/comments/cgz12h/in_a_scenario_in_which_a_miner_submits_a_block/) is not validated and the role of stakers in preventing majority/51% attacks
* Decred's [governance model](https://www.reddit.com/r/decred/comments/cirkvr/decreds_governance_model/); it's hard to add governance after launch
* Why Decred Wins in the End? [Incrementalism](https://www.reddit.com/r/decred/comments/cc8c0h/why_decred_wins_in_the_end_incrementalism/)
* Can [Flair](https://www.reddit.com/r/decred/comments/ch0gey/governance_can_flair_increase_the_odds_of/) increase the odds of self-guided education on r/decred?
* David Ogilvy talks [Direct Response Advertising](https://www.reddit.com/r/decred/comments/ci82iy/david_ogilvy_talks_direct_response_advertising/); targeting groups that share our values and value sovereignty as high as we do
* What [metaphor/analogy](https://www.reddit.com/r/decred/comments/cc40hb/general_what_metaphoranalogy_helps_you_understand/) helps you understand different actors within the project?

## 市场表现

7月份DCR的交易价格为25.20-35.64USD，0.00262-0.00296BTC。平均每日为28.97美元。

在快速达到1.3万美元的价格之后，比特币价格开始下跌，在7月的大部分时间里，比特币的价格都维持在1万美元上方。

## 相关外部信息

Chris Burniske of Placeholder VC (holders of Decred and Zcash) provided a good [summary](https://forum.zcashcommunity.com/t/placeholder-considerations-resources-governance-and-legitimacy-in-nu4/34045) of the situation facing the Zcash community as the founders reward expires, advocating for a continuation of 20% block reward to fund project development for another 4 years, with a split of 70% to "Protocol Development" and 30% to "Growth Funds".

Zooko Wilcox published a [personal letter](https://medium.com/@zooko_25893/a-personal-letter-about-the-possibility-of-a-new-zcash-dev-fund-f6d30df64392) about the possibility of a new Zcash dev fund, which explains that he always knew that the time would come when funding would run out and create a problem that could only be solved through a "messy and difficult process" such as the Zcash community is currently going through. Zooko stated again that he cannot be the one to make the decision and that it should come from the community, but as the CEO of ECC he has considerable influence in the community, and the community has no established method of making decisions.

All of the various options being considered have been helpfully summarized in this [megathread](https://forum.zcashcommunity.com/t/future-of-zcash-dev-funding-megathread-everything-in-one-place/34063). As Chris Burniske remarked in his post, the first question is how to make the decision about the decision in a way which is perceived as legitimate. Given time constraints Chris advocates the use of polling to gauge preference for the various options, with a final decision made using the ECC and Zcash Foundation 2-of-2 multisig. Zooko stated that the ECC will announce a method of decision-making in early Aug.

Nebulous, the company building the Sia network, announced the [completion](https://sia.tech/funding2019) of a $3.25 million seed round with participation by a number of venture capitalists.

Funding has also been the subject of some discussion in the Ethereum community, with more [attention](https://research.circle.com/insights/the-great-ethereum-funding-debate) being paid to [EIP-2025](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-2025.md), which would add 0.0055 ETH per block for 18 months (17K ETH in total) to fund ETH 1.X development (as the main developers focus on ETH 2.0). The block rewards would be used to pay back a loan which the teams working in 4 different areas would receive to multisig contract addresses.

As with any controversial Ethereum Improvement Proposal, it is difficult for outsiders to know if EIP-2025 will go anywhere. A [tweet](https://twitter.com/VitalikButerin/status/1154733914881179648) from Vitalik stating that it seems to have little support probably indicates that it won't be included in the Istanbul hard fork.

Another Circle Research [article](https://research.circle.com/insights/degrees-of-architectural-decentralization-to-infura-and-beyond) published about Ethereum concerns the centrality of Infura, a service company created by Consensys which allows dapp developers to sidestep setting up and running their own nodes. The article considers the difficulty and increasing demands of running a full node (space requirements have increased 25-48% year to date) as causing a decrease in the number of full nodes from 12,000 in Dec 2018 to 8,000 in Jul 2019. Infura is welcome because it allows Ethereum developers to avoid the inconvenience of interfacing with the blockchain directly, but it introduces a central point of failure for the 50,000 dapps and developers who rely on it. Infura is in turn reliant on AWS services to run its nodes.

The /r/ethtrader [Donuts experiment](https://www.reddit.com/r/ethtrader/wiki/donuts), where subreddit participants earn points based on their subreddit karma and use these to participate in polls, is moving into another [phase](https://www.reddit.com/r/ethtrader/comments/c3f1ku/the_next_phase_for_donuts/). Smart contracts have been prepared which will allow Donuts to be moved to the Ethereum blockchain, and some Reddit admins are facilitating this on the Reddit end. As the Donuts are being "decentralized", the polls are to become non-binding signal votes, due to fears in the community about on-chain governance. This appears to be controversial choice, based on comments on the announcement, and there is some confusion about what the purpose of Donuts are.

Aragon [completed](https://blog.aragon.org/final-results-from-aragon-network-vote-3/) its 3rd round of governance proposal voting, 11 proposals were submitted and 8 were allowed to be included in the vote by the Aragon Association. 7 of these proposals were approved, all with 99% or greater yes votes, 4 were unanimous (with 1 or less ANT token voting no). ANT turnout was 2.6% averaged across the 8 proposals.

[AGP-64](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-64.md) signals support for Quiet Ending Voting, which would extend the duration of AGP voting if the outcome is flipped towards the end of the voting period. This is in response to the [observation](https://www.evanvanness.com/post/184616403861/aragon-vote-shows-the-perils-of-onchain-governance) that late voting by a whale had swayed the outcome of previous AGPs. This proposal does not specify a particular implementation but signals support for resources to be invested in developing quiet ending voting for Aragon.

[AGP-59](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-59.md) mandates a minimum length for discussion period on AGP submissions. [AGP-70](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-70.md) signals support for shifting management of the Nest grant program away from the Aragon Association and to a DAO, AGP-71 extended the budget of the Nest program by 600K DAI and 300K ANT. [AGP-73](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-73.md) is the biggest budget proposal, with further flock funding for Autark of 1.6 million DAI and 487K ANT to cover one year. The rejected proposal called for development of a native mobile app for Aragon voting.

Dash [completed](https://blog.dash.org/the-dash-investment-foundation-supervisor-election-results-96a28309744b) the first annual elections for positions as supervisors of the Dash Investment Foundation, using some software custom [made](https://blog.dash.org/trust-protector-election-software-93ed67c7455b) for this purpose.

Another round of the Tezos protocol amendment process is underway, after the Brest proposal by TzScan Baker failed to achieve enough upvotes to progress. Cryptium Labs [injected](https://blog.nomadic-labs.com/babylon-proposal-injected.html) a proposal called Babylon, prepared jointly with Nomadic Labs, on Jul 26, then an amended version 2.0 on Aug 2. This proposal would make a number of changes to the protocol, including a new variant of the consensus algorithm and new Michelson features, and a new proposal quorum requirement would be introduced which would prevent the proposal with the most upvotes progressing to the second phase unless it has support from at least 5% of the stake. This would allow for proposals with little support (like Brest) to be rejected earlier, and the proposal cycle to restart more quickly thereafter.

The 0x decentralized exchange protocol team [announced](https://blog.0xproject.com/shut-down-of-0x-exchange-v2-0-contract-and-migration-to-patched-version-6185097a1f39) that a security vulnerability had been reported by a 3rd party security researcher, and shut down the exchange contract as a precaution. The 0x smart contract pipeline was patched and re-deployed the next day.

StopAndDecrypt published an [overview](https://medium.com/hackernoon/betterhash-decentralizing-bitcoin-mining-with-new-hashing-protocols-291de178e3e0) of ways how mining pools could abuse the hash power trusted to them and made the case for BetterHash - the working name for alternative mining protocols that aim to give the power back to individual miners and strip mining pools of their influence.

A backdoor [sneaked](https://nakedsecurity.sophos.com/2019/07/09/backdoor-discovered-in-ruby-strong_password-library/) into a Ruby library for checking password strength. The injected malware fetches and runs the code from pastebin.com, giving the attackers the power of remote code execution. The irony here is that the hijacking was possible because the author of the password strength checking library had [weak and reused password](https://news.ycombinator.com/item?id=20382779), and had no 2FA on his RubyGems account. It is important to audit dependencies in a world where it is getting common to blindly pull in dozens or hundreds of dependencies using automated tools.

The network of OpenPGP keyservers was subject to certificate flooding [attack](https://gist.github.com/rjhansen/67ab921ffb4084c865b3618d6955275f). Someone uploaded a ton of certifications for public keys of two GnuPG contributors, effectively "poisoning" them. Anyone who attempts to import a poisoned key into a vulnerable installation risks making their keyring unusable because of a massive performance degradation. Flaws of the keyserver network design were known for a long time. It basically maintains a decentralized censorship-resistant write-only database but with no robust abuse protection. During more than a decade of this vulnerability being known, the network was unable to coordinate the development and deployment of an upgrade. This once again reminds us how challenging it is to design a resilient decentralized protocol and how critical it is for a decentralized network to have a governance mechanism to adapt.

## About This Issue

This is issue 16 of Decred Journal. Index of all issues, mirrors and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

* writing and editing: bee, cryptoleslie, degeri, Dustorf, lukebp, raedah, richardred, s\_ben
* reviews and feedback: chappjc, davecgh, jholdstock, jy-p, margaret\_mei, matheusd

## 中文社区

* [社区web](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [优酷频道](https://i.youku.com/decredproject)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

感谢 (按字母排序): 
