# Decred月报 - 11月 

![里斯本的Web Summit](img/NOV18_websummit18-300.png "里斯本Web Summit")

Decred在11月取得激动人心的进展。社区开始从Politeia的提案系统获得好处。 持币者相继通过Decred钱包 （Decrediton或dcrcli) 积极表达对于项目未来方向的提案， 包括项目服务商管理，公共关系和区块链研究。

Decred 已进展到可以支持任何利益相关者对Decred的愿景 - 更多公司和贡献者加入Decred生态，而一些长期贡献者则根据兴趣和能力提出议案。

在社区的兴奋，成长和变化中，Decred保持项目的更新步伐。桌面和移动钱包的测试版本表现出Decred一贯对稳定和创新的传统坚持。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 上个月开始的两个重大的更改在经过大量测试后合并。第一个是[UTXO反转的设置语义](https://github.com/decred/dcrd/pull/1471) 随附的[数据库迁移](https://github.com/decred/dcrd/pull/1520)， 这是一项重要的更改，将提供更简单有效率的处理未花费的交易输出。这样做的额外好处是让区块重组测试运行时速度提高了40％。第二个是[优化重组处理](https://github.com/decred/dcrd/pull/1500)。新的[--maxsameip](https://github.com/decred/dcrd/pull/1517)参数允许限制具有相同IP地址的连接数。修复了一个从上游btcd[移植](https://github.com/decred/dcrd/pull/1533)过来，超级罕见的bug。

[dcrwallet](https://github.com/decred/dcrwallet): 增加新的RPC，支持使用[ticketbuyer v2](https://github.com/decred/dcrwallet/pull/1307), 购买[单张票](https://github.com/decred/dcrwallet/issues/1317) 和[流动账户](https://github.com/decred/dcrwallet/pull/1098)。另加使用替代数据库后端的[能力](https://github.com/decred/dcrwallet/pull/1282)，这对移动平台很有用。修复bugs: [监视常用钱包地址](https://github.com/decred/dcrwallet/pull/1320), [遗漏或双重交易](https://github.com/decred/dcrwallet/pull/1321), [丢失地址和交易](https://github.com/decred/dcrwallet/issues/1333).

一个大的[锁定余额](https://github.com/decred/dcrwallet/pull/1330)算法的改进工作已经开始，这会为 solo，选票矿池及分票投票者解决某些问题。

[Decrediton](https://github.com/decred/decrediton): 增加功能: 用以选择SPV或全节点的[新页面](https://github.com/decred/decrediton/issues/1755)和显示Decred [基金会余额](https://github.com/decred/decrediton/pull/1764)。自动购票器已更新到[ticketbuyer v2](https://github.com/decred/decrediton/pull/1744)。由于票价稳定，它的选项较少，而且比v1更易于使用。现在，用户只需要指定保留余额，账户及使用的选票矿池。[大钱包](https://github.com/decred/decrediton/pull/1727)的启动性能也有所改进。Politeia整合也有所改进包括[反应更快](https://github.com/decred/decrediton/pull/1825)的提案加载和[新提案及投票的通知](https://github.com/decred/decrediton/pull/1835). UI/UX调整:更新了[提案列表设计](https://github.com/decred/decrediton/pull/1771), [概览设计改进](https://github.com/decred/decrediton/issues/1818),更新 [账户图标](https://github.com/decred/decrediton/issues/1811)以及[导航图标和微动画](https://github.com/decred/decrediton/issues/1809)的改进。为了确保持续的跨平台稳定性和性能，Decrediton更新到[Electron 3](https://github.com/decred/decrediton/pull/1777)

提到的功能已合并到主分支中，并将在下一版Decrediton中体现。

Trezor: Model T已[发布](https://blog.trezor.io/firmware-updates-2-0-9-and-1-7-1-developed-by-the-community-for-the-community-c4b965741ca3) 支持Decred的最新固件 version 2.0.9。感谢 @matheusd。现在Decrediton开发员可以开始整合工作。

注意：市面发现假的Trezor One，关于如何验证和购买正版设备，请查看[官方博客](https://blog.trezor.io/psa-non-genuine-trezor-devices-979b64e359a7)。

[Politeia](https://github.com/decred/politeia): [politeiavoter](https://github.com/decred/politeia/tree/master/politeiavoter) 的隐私和性能通过随机的[选票投票顺序](https://github.com/decred/politeia/issues/565), 随机[投票间延迟](https://github.com/decred/politeia/pull/579)和[过滤](https://github.com/decred/politeia/issues/562)已投票的选票得到改善。按大众要求，创建了邮件通知系统以支持对[新提案](https://github.com/decred/politeiagui/pull/848)和[评论](https://github.com/decred/politeiagui/pull/919)更新的消息。通过[票证功能搜索](https://github.com/decred/politeiagui/pull/899)可以验证投票。[评论永久链接](https://github.com/decred/politeiagui/issues/753)和[可区分的作者评论](https://github.com/decred/politeiagui/issues/877)已上线。新的["Abandoned"（被放弃）状态](https://github.com/decred/politeiagui/issues/889) 用来处理被放弃的提案。"结束" 选项被 [分成](https://github.com/decred/politeiagui/issues/904) "通过" 和 "不通过" 选项。SVG支持被[关闭](https://github.com/decred/politeia/pull/626)直至合适用来清理SVG的工具出现位置。一个[小漏洞](https://github.com/decred/politeia/issues/563)被修复了,感谢@iemlisted 的报告。及很多较小的改进和修复。

某些功能将在[主网页](https://proposals.decred.org/)下一次更新后才能体现。

针对查看提案修订[之间差异](https://github.com/decred/politeiagui/issues/754)和[突显新评论](https://github.com/decred/politeiagui/pull/897)的工作也已经开启。

[Android](https://github.com/decred/dcrandroid):安卓版Decred钱包开发在本月实现了一次飞跃-在[Google Play商店](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet)推出了预发布版本。 Play商店版本包括更新的货币转换，以[本地货币显示费用](https://github.com/decred/dcrandroid/issues/192)和[高级密码保护](https://github.com/decred/dcrandroid/issues/134)，能够[锁定所有数据](https://github.com/decred/dcrandroid/issues/187)并使用[访问密码](https://github.com/decred/dcrandroid/issues/180)。此版本还包括一个安全菜单，允许用户[签署](https://github.com/decred/dcrandroid/issues/226)证明地址所有权的消息。 另一个成功实施的社区创新是“[隐藏帐户](https://github.com/decred/dcrandroid/issues/175)”功能。隐藏帐户允许移动用户将资金存放在他们的移动钱包中，但资金将不会显示在主屏幕余额上。在本地聚会中交易Decred的社区成员为这项功能提供的额外隐私和安全感到兴奋。账户之间的资金转账在本月也得到了升级，只需简单的[下拉选择](https://github.com/decred/dcrandroid/issues/119)让转账更快速简便。

[iOS](https://github.com/raedahgroup/dcrios):iOS移动钱包目前正处于测试阶段，需要额外的开发周期才能合并Android上提供的功能集。

[dcrdata](https://github.com/decred/dcrdata): 本月集成到基本代码中的新功能包括[网络哈希算力表](https://github.com/decred/dcrdata/issues/723)，在导航菜单添加[Decred基金会](https://github.com/decred/dcrdata/issues/784)以及更详细的交易信息，例如在[内存池上显示交易输出花费](https://github.com/decred/dcrdata/issues/825)，在显示[地址视图的交易类型](https://github.com/decred/dcrdata/issues/741)和改进的[时间戳信息](https://github.com/decred/dcrdata/issues/776)。

预览[新网页](https://github.com/decred/dcrdata/pull/718),及所有的新功能都已上线[alpha网站](https://alpha.dcrdata.org/nexthome)。目前它运行的是master的v3.2.0-pre built。更稳定的[beta网站](https://beta.dcrdata.org/)运行v3.1.0-beta。最稳定的[explorer.dcrdata.org](https://explorer.dcrdata.org/)运行的是v3.0.2-发布。为了与Insight链接保持一致,后者也可到[mainnet.dcrdata.org](https://mainnet.dcrdata.org/)访问。

在开发方面，@gozart开始了重构将javascript代码库[转换](https://github.com/decred/dcrdata/pull/805)到ES6模块，添加用于前端开发工具和生产资产捆绑的webpack，强制执行代码样式并将CSS转换为[SCSS partials](https://github.com/decred/dcrdata/pull/839)。

[dcrstakepool](https://github.com/decred/dcrstakepool)：这是大多数(如果不是全部)VSP(选票矿池)使用的软件。自述文件[更新](https://github.com/decred/dcrstakepool/pull/285)了包含Go模块的构建说明。交易链接已从Insight更改为[dcrdata](https://github.com/decred/dcrstakepool/issues/264)。

发现并讨论了几个隐私问题。目前正在测试补丁以[自托管CAPTCHA](https://github.com/decred/dcrstakepool/pull/281)取代Google recaptcha，以避免利益相关者的指纹识别--欢迎VSP(选票矿池)运营商加入测试。[已删除](https://github.com/decred/dcrstakepool/pull/283)对Cloudflare的请求。提出了[让电子邮件可选](https://github.com/decred/dcrstakepool/issues/274)的问题。

[Ticket splitting](https://github.com/matheusd/dcr-split-ticket-matcher)：分票测试版在11月份继续增长，每天都有分票。两个集成了分票的VSP，[decredbrasil.com](https://stake.decredbrasil.com/)和[decredvoting.com](https://decredvoting.com/)，除了他们网站上的指南,还发布了[教程视频](https://www.youtube.com/watch?v=3RGoUQK0g24)(葡萄牙语和英语)以及[分票概述](https://www.reddit.com/r/decred/comments/9vhpby/decred_ticket_splitting_overview/)。该软件已更新，以支持SPV轻钱包模式。请阅读[问题](https://github.com/matheusd/dcr-split-ticket-matcher/issues/29)以考虑隐私问题。

[Decred Slack](https://decred.slack.com)和[电报](https://t.me/dcrticketsplit)都有分票群以及VSP的[分票教程](https://t.me/dcrticketsplit/2666)。

[design](https://github.com/decred/dcrdesign): Kyle 在[Firethought](https://firethought.net/) 中发布了[Decred图标动态包](https://medium.com/@firethought/base-iconset18-motion-pack-readme-a96f96e868)。以[eeter.co](http://www.eeter.co/)设计的图标包为基础构建的图标包将带来“更具吸引力的Decred应用程序体验”

[docs](https://github.com/decred/dcrdocs)：11月对于文档来说是一个重要的月份，其中包含各种社区支持的更改和更新。[VSP更改语言提案](https://proposals.decred.org/proposals/522652954ea7998f3fca95b9c4ca8907820eb785877dcf7fba92307131818c75)通过，证实了社区希望在所有Decred文档中将“PoS Mining”更改为“PoS投票”，并从“stakepool”更改为“Voting Service Provide(VSP)”。第一批[文档的更改](https://github.com/decred/dcrdocs/pull/590)已合并。基金会[采用“Decred Treasury”](https://github.com/decred/dcrdocs/pull/690)也已更新。对于那些希望更深入了解Politeia的人们，我们创建了一个新的"[Politeia数据导航](https://docs.decred.org/advanced/navigating-politeia-data/)"文档。期待已久的[Decred Glossary](https://github.com/decred/dcrdocs/pull/675)(Decred词汇)在本月完成并发布，@s_ben和许多支持这项工作的人付出了巨大努力提供反馈和建议。我们强烈建议使用[词汇表](https://docs.decred.org/glossary/)来改善我们对共享社区的理解。

11月开发活动数据: 分布于8个存储库（repositories) 有 266 有效PRs, 268 主要提交, 44,955 行添加 及 25,448 行删除。每个存储库中有来自3-11个开发者的贡献。([图表](https://twitter.com/decredproject/status/1070413196555636736))

## 人员

热烈欢迎新人的第一次贡献: [logicminds](https://github.com/decred/dcrd/commits?author=logicminds) (dcrd, _10月月报遗漏_), [@itswisdomagain](https://github.com/decred/dcrdata/commits?author=itswisdomagain) (dcrdata), [rocknet](https://github.com/decred/decrediton/commits?author=rocknet) (decrediton), [@brunobraga](https://github.com/decred/politeiagui/commits?author=brunobraga95) (politeiagui).

恭喜5位新贡献者[列入](https://github.com/decred/dcrweb/pull/444)decred.org: Insaf Nori (@butterfly, community manager - Middle East), Guang (@guang, community manager - Asia), Seth Benton (@s_ben, developer), Youssef Boukenken (@sef, developer), Zubair Zia (@zubairzia0, research and strategy).

@kozel 访问了建立已久[coinmine.pl](https://www2.coinmine.pl/)的运营Feeleep，[深度讨论了Decred的基础设施](https://medium.com/decred/decred-intriguing-and-extraordinary-an-interview-with-coinmine-pl-mining-pool-operator-5c5592443cb4).

> 我必须说，从技术角度来看，Decred的守护进程是在我所有业务经验中唯一一个未遇到过任何稳定性或同步问题的守护进程

10月的月报中有关于新的承包商公司一个简短提及。让我们来好好的介绍一下。[Block 42](https://42block.io/)是一家总部位于白俄罗斯明斯克的区块链开发公司，利用区块链技术为金融，保险，物流和供应链行业带来更高的透明度和效率。 他们的母公司[Grinteq](https://grinteq.com/)位于美国纽约。 目前为止的贡献团队如下：

* Nick Kaeshko (@Nick) - 联合创办人, 确保所有事情顺利进行
* Maria Pleshkova (@Maria) - UI/UX 设计师, 在[选票矿池主题改革](https://github.com/decred/dcrdesign/issues/23)中贡献，确保和目前Decrediton的UI保持一致性。目前工作专注于[Politeia的重新设计](https://github.com/decred/dcrdesign/issues/77)：包括UI/UX更新和新功能的实现。
* Dmitry Fedorov (@klka) - Golang开发员,目前为加快区块处理方面制作区块链索引[异步（asynchronous）](https://github.com/decred/dcrd/issues/1470)
* 很快将有另一成员正式加入
再次欢迎！

## 治理

团队开启了＃proposals 和 #research中的Politeia数据整理工作。@snr01 分享了[投票数据图表](https://github.com/snr01/PiVotingCharts)。

深入讨论了低质量的提案会使得Politeia混乱，并提出了多种想法。 @richardred在[Politeia Digest #4](https://medium.com/politeia-digest/politeia-digest-issue-4-nov-7-nov-13-2018-685e18e7491a)中对此进行了很好的概述。

在聊天渠道中的 #proposals 聊天室非常活跃并有着许多对提案系统及提案深入的讨论。欢迎加入 [Matrix](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org)或[Slack](https://decred.slack.com/messages/CDL5DRZU6)。

由@richardred整理每周的Politeia简报 “Politeia Digest” 包含着所有Politeia重要活动的细节。请查阅本月发布的[第4期](https://medium.com/politeia-digest/politeia-digest-issue-4-nov-7-nov-13-2018-685e18e7491a), [第5期](https://medium.com/politeia-digest/issue-5-nov-14-nov-20-2018-62e8aed223b7)及[第6期](https://medium.com/politeia-digest/issue-6-nov-21-nov-27-2018-3260d03d26a1)。同时也可以通过这个[搜索](https://www.reddit.com/r/decred/search?include_over_18=on&restrict_sr=on&q=politeia%20digest)Reddit 讨论区。

### 本月完成投票 - 6 份 

**1.[Decred Contractor Clearance Process](https://proposals.decred.org/proposals/fa38a3593d9a3f6cb2478a24c25114f5097c572f6dadf24c78bb521ed10992a4)** 

* 投票结束 - 11月21日 **通过**
* 法定票数：13228/8173 票，13206 通过(95.71%) 
* 提案建议设立 Decred Contractor Clearance (DCC) 为服务商作为对项目参与及贡献的条件。获取DCC必需要有 3个合格服务商／贡献者担保有相关工作需要的技能。相同的，撤掉服务商资格也只需要3个合格服务商／贡献者投票撤除。

**2.[Wachsman Communications Proposal for Decred](https://proposals.decred.org/proposals/bc8776180b5ea8f5d19e7d08e9fcc35f0d1e3d16974963e3e5ded65139e7b092)**

* 投票结束 - 11月5日 **不通过**
* 法定票数：13202/8192 票，3646 通过(27.62%) 
* 专业的宣传公司合作提案。要求为期6个月，每月 2万美金的经费。

**3.[Ditto Communications Proposal for Decred](https://proposals.decred.org/proposals/27f87171d98b7923a1bd2bee6affed929fa2d2a6e178b5c80a9971a92a5c7f50)**

* 投票结束 - 11月5日 **通过**
* 法定票数：21191/8192 票，13206 通过(62.32%) 
* 专业的宣传公司合作提案。要求为期6个月，每月 2万5千美金的经费。

**4.[Decred Open Source Research](https://proposals.decred.org/proposals/c68bb790ba0843980bb9695de4628995e75e0d1f36c992951db49eca7b3b4bcd)**

* 投票结束 - 11月5日 **通过**
* 法定票数：13141/8192 票，11854 通过(90.21%) 
* 提案设立一个开源研究项目，要求 一万美金 作为起始经费，投入区块链研究并发布文章。提案通过后，第二个提案可以用来决定研究内容／题材。
 
**5.[Change language: PoS Mining to PoS Voting, Stakepool to Voting Service Provider](https://proposals.decred.org/proposals/522652954ea7998f3fca95b9c4ca8907820eb785877dcf7fba92307131818c75)**

* 投票结束 11月5日 **通过**
* 法定票数：12745/8192 票，11991 通过（94.08%）
* 提案建议把一些Decred专用词更替，并提议以后类似大规模转换专用名词可以通过提案系统做决定

**6.[Premium Listing for Decred on Easyrabbit](https://proposals.decred.org/proposals/34707d34b09c3ebcf0d4aa604e8a08244e8f0f082c0af3f33d85778c93c81434)**

* 投票结束 11月23日 **不通过**
* 法定票数：8756/8156 票，444 通过（5.07%）
* Easyrabbit 交易所已于10月底上线DCR交易。
* 提案要求 30 DCR 将项目升级为高级用户，以获得一些宣传福利 包括将 DCR 标志放到主页面上，低交易费，自媒体宣传DCR 等等。 

### 截止12月4日的新提案如下

**[Upgrade mining algorithm to ProgPoW](https://proposals.decred.org/proposals/0aaab331075d08cb03333d5a1bef04b99a708dcbfebc8f8c94040ceb1676e684) 由engineerking于Nov 11提交**

* 作者提案把Decred的挖矿算法改成[ProgPoW](https://github.com/ifdefelse/ProgPOW)。
* 状态：作者未授权开启投票

**[Decred Open Source Research proposal 2 - research projects](https://proposals.decred.org/proposals/5d9cfb07aefb338ba1b74f97de16ee651beabc851c7f2b5f790bd88aea23b3cb) 由@richardred于Nov 21提交**

* 续第一个[研究提案](https://proposals.decred.org/proposals/c68bb790ba0843980bb9695de4628995e75e0d1f36c992951db49eca7b3b4bcd)，目标为搜集并确定研究项目想法的提案
* 状态：作者未授权开启投票

**[Decred integration into Crypto-ATMs](https://proposals.decred.org/proposals/bb7e19283d5c65fed598d5a2f4afcc2b5d2eab187b9cb84fc4304430f80b5ad1)由 bcashgr于Nov 24提交**

* 公司名为Bcash提案要求资助把Decred整合到他们提供的提款机中。开发成本 25，000欧元 及 每月 1，650 欧元的维持费。
* 状态：投票于12月4日开启

**[Decred Radio Advertising, 190+ FM and AM Stations, + Intl. Satellite](https://proposals.decred.org/proposals/7fe5d07a4ffff7dc6a83383018823d880b1c1db0a29305e74934817cf2b4e2ce)由ftl_ian于Nov 26提交**

* 这项提案要求Decred在一个“Free Talk Live” 的电台做广告。为期13周的成本是 22,750美元
* 状态：投票于12月4日开启

**[Decredex](https://proposals.decred.org/proposals/e78bc28631d0e682912e3ece25944481bf978b906ea44b1ed36470c0f48b27fc)由fabianreum于Nov 26提交**

* 提案要求对于公司REUM Ltd开启去中心化交易所工作的资助。总预算为 1,086,500美元。
* 状态：投票于12月4日开启

**[Add Decred support to Coffee Wallet](https://proposals.decred.org/proposals/45de9806c952c5ffc2fc6782fddbc74c852c26e3fb0e950144b92d75082c4731) 由francio于Nov 29提交**

* 这项提案要求资助将Decred整合到 “Coffee Wallet” 多币种钱包。要求数额为150DCR 及预期在一月初完成
* 状态：作者未授权开启投票

**[Stable coin - USDD](https://proposals.decred.org/proposals/85fc65cef080cfc3564906fd3d488b827d74fc99bb29143ed8aa6c400b765be9)由fabianreum 于Nov 29提交**

* 这项提案要求资助一个Decred背书名为 USDD 的稳定币(stablecoin)项目。4年预算为 1，576，000美金。提案里提供了明细。
* 状态：作者未授权开启投票

**[Decred Bug Bounty Proposal](https://proposals.decred.org/proposals/d33a2667469b56942adf42453def6cc2292325251e4cf791e806939ea9efc9e1)由@degeri于30 Nov提交**

* 这项提案为Decred建立一个bug赏金计划，通过该计划可以补偿／奖赏报告错误或漏洞的人。该提案要求6个月的预算为5,000美元，以支付设置和运营成本，并预算在此期间赏金支付的上限为100,000美元。 @degeri投入了大量精力与社区就如何运作这个赏金计划进行协商，特别是确保当前与该计划合作的Decred承包商都参与其中。
* 状态：作者未授权开启投票

## DCR网络
### 算力 

![PoWStats](img/NOV18_PoWStats.png)

*图片源：https://dcred.eu/powStats*

算力: 11月算力开始大约156 PH/s 结束大约159 PH/s，之间最低为125 PH/s 最高为234 PH/s。BeePool 矿池份额大约19-30%, F2Pool 15-46%, Luxor 1.6-4%, 及 Coinmine 1.9-4%. 未命名算力保持 25-50% (低点15% 及高点75%)。矿池分布数据无法精确计算。

### 票价

![PoWStats](img/NOV18_TicketPrice.png)

*图片源：https://dcred.eu/posStats*

### 锁仓数额 

![PoWStats](img/NOV18_DCRLocked.png)

*图片源：https://dcred.eu/posStats*

投票: 30日 平均票价为 103 DCR (+3.2)。价格与96.7至110.2 DCR之间浮动。锁仓数额为4.02-4.18 百万 DCR, 大约总流通量的 45.9-47.2%。

票价跌到96.7后，在单一时间窗售出了1，378票，票价即时经过9个连续涨价抬至110.2DCR。这是自从2017年7月更改票价算法，[sdiff algorithm](https://github.com/decred/dcps/blob/master/dcp-0001/dcp-0001.mediawiki)后的新高。

[@permabull nino](https://twitter.com/ImacallyouJawdy) 分享了[更多](https://twitter.com/ImacallyouJawdy/status/1065272779447009281) [其他](https://twitter.com/ImacallyouJawdy/status/1060990375064522752) 表示DCR锁定有上升趋势的图表。

### 币价

![PoWStats](img/NOV18_USDPrice.png)

*图片源：https://dcrstats.com/*

![PoWStats](img/NOV18_BTCPrice.png)

*图片源：https://dcrstats.com/*

### 节点数

![PoWStats](img/NOV18_NodesCount.png)

*图片源：https://dcred.eu/nodeStats*

节点: [dcred.eu](https://dcred.eu/nodeStats)显示 Dec 01为止 共有 204 public listening Node 及 332 Normal Node。版本分部: 6.5% 是 v1.4.0(pre) dev builds (+0.5%), 50% 为 v1.3.0 (+5%), 25% 为 v1.2.0 (-3%), 11% 为 v1.1.2 (-3%), 5% 为 v1.1.0。

## 挖矿

Obelisk [开始生产](https://us16.campaign-archive.com/?u=393b2698d17bdfe48ac0422ac&id=28096412c5) 第 2-5 批矿机 并预期12月初开始发货,之后大约4周后将满足所有订单。他们在12月4日也公布了几个促销：用户可以购买 SC1 hashing boards 安装到DCR1机子上, DCR1也可转换成 第6批 SC1 矿机或由Obelisk回收。细节可参看[通讯文章](https://us16.campaign-archive.com/?u=393b2698d17bdfe48ac0422ac&id=88576cef2a)。


The Whatsminer D1 [算力](https://twitter.com/Pangolinminer/status/1061521332498624512) 为48 TH/s, 从预期的44 TH/s 提高了9%。[Pangolin](https://pangolinminer.com/product/whatsminer-dcr-with-psu-shipout-on-dec-5/)的价格为4,850美元。MicroBT的发货延迟以及价格和性能的变化引起了社区[各种不同的意见](https://bitcointalk.org/index.php?topic=5068845.msg47865706#msg47865706)。社区也提起关于最佳实践和关于分销网络以及官方经销商构成的[混淆](https://www.reddit.com/r/decred/comments/9fdz9d/psa_do_not_purchase_the_whatsminer_44th_decred/)。

竞争对手Bitmain(比特大陆)宣布推出[Antminer DR5](https://shop.bitmain.com.cn/product/detail?pid=0002018111918225889369SR3N9s0646)，算力为34 TH/s，功率为1800 W，价格为人民币19,000元（2750美元），12月下旬发货。[DR5](https://www.antminerdistribution.com/antminer-dr5/)的欧洲进口商列出12月21日的暂定交货期，价格为[3299美元](https://french.alibaba.com/product-detail/asic-miner-bitmain-antminer-dr5-34th-blake256r14-dcr-digging-machine-decred-mining-machine-ant-miner-with-psu-60820041330.html)至[EUR3291(3724美元)](https://miningwholesale.eu/product/bitmain-antminer-dr5-34th/)。

[youtube](https://www.youtube.com/watch?v=U0QjhvaoQpc)上发布对于Obelisk DCR1 矿机的评论影片。加拿大创意的冷却方式照片在聊天室里[泄露](https://matrix.to/#/!NNzHoaSdnsbZDQOXJr:decred.org/$154146601110108OYpjf:decred.org)了。

## 整合

Luxor pool [公布了](https://twitter.com/LuxorTechTeam/status/1067110171057381376) 给Decred矿工 3-5%算力提升

### 新的投票矿池

* [decred.staked.us](https://decred.staked.us/) 5% 矿池费。[Staked](https://staked.us/about/)是一个提供[多个](https://staked.us/yields/)加密货币矿池服务的公司，最近[发布](https://medium.com/coinmonks/decred-staking-guide-2e569d0390ff)了一个如何使用他们投票矿池投Decred的教程。
* [dcrpool.dittrex.com](https://dcrpool.dittrex.com) 1% 矿池费。

### 交易所

* [Bitqist](https://bitqist.com/) [在r/decred](https://www.reddit.com/r/decred/comments/9y5dru/you_can_now_instantly_exchange_decred_on_bitqist/)公布Decred的整合。交易所[位置](https://support.bitqist.com/hc/en-us/articles/360003566512-About-Us)在荷兰。@Haon [报告](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$154342154026995puxog:decred.org)提币没问题但存币目前未开通。
* [Kaiserex](https://www.kaiserex.com/)自2015开始牵涉OTC交易，正式[推出](https://twitter.com/kaiserexcom/status/1064494181224206336)[OTC柜台](https://www.kaiserex.com/kaiserex-otc-desk/)。DCR是支持的加密货币之一，法币方面支持的有 USD, EUR, GPB and JPY. 最低交易额是 50,000 欧元，费用为0.05-1%
* DragonEx 龙网交易所[增加](https://twitter.com/Dragonex_io/status/1062613644276428800)DCR/BTC交易对。

## 落地应用

英国假期购物者在这季节多了一个花费Decred的选择。MonetaryUnit[公布](https://twitter.com/monetaryunit/status/1062127668769050626) 在他们夏天收购的英国市场[Flubit](https://flubit.com/)[接受](https://blog.flubit.com/pay-crypto-flubit-com/)DCR。[部落格](https://blog.flubit.com/crypto-coins-drive-xmas-strategy-largest-eshop-200bn-cryptocurrency-industry-goes-mainstream-online-shopping-flubit-com/)文中: Flubit 是个已运作8年，过去一年服务三百万购物者的电商。加密货币的集成过程非常顺畅。

[Coinstop](https://coinstop.io/), 澳大利亚的Trezor，Ledger和KeepKey硬件钱包代理，现在已[接受](https://twitter.com/COINSTOPio/status/1067927790320664576)DCR。

## 外展活动

11月份的外展活动主要是规划，尽管如此，世界各地仍然举办过许多本地聚会，包括在墨尔本和胡志明市的重要活动。 @eSizeDave和@joshuam在亚太地区推广Decred方面做得非常出色。

@Dustorf发布了一篇的博客文章，详细介绍了Ditto的提案批准过程，从初步的审查，提案讨论和投票，到下一步的规划和执行。该博客在发布前在#marketing上收到了大量的反馈，展示了我们作家们的能力和技巧。大量的汇总数据，上传并与Ditto团队分享的工作已经进行中，这是为了我们可以在12月份开始运行做好的准备。 @Dustorf在12月3日星期一有一个入职通话，他和@ jy-p计划在那个星期亲自与Ditto方见面。

按照@ Dustorf的博客，初步重点将是要在定位和消息传递上获得社区的共识，然后将其转换为一些网站更新，同时还计划2019年的执行方案。Ditto将在Matrix的#marketing中公开参与讨论，敏感信息将保留给名为“Ditto PR”的新Matrix聊天室。如果您认为可以提供帮助并希望被邀请到这个聊天室，请联系@jz或@Dustorf加入。

12月将是计划筹备月，@jy-p将于1月16日至18日在美国迈阿密举行的北美比特币会议上展示“区块链时间戳应用”。其他活动可能会在12月的第一周确认，并将在#marketing中公布。

除了规划中期和长期的战略，我们的公关也会如#marketing中所述，根据当前的机会采取行动，。

@Haon在Reddit中展开了关于Ditto合作伙伴关系的期望的讨论，并根据他在Decred社区的经验以及与之前公关公司（PRWithBrains）的合作分享了其想法。

## 社区活动
### 过去

* Raedah Group 在美国，波特兰的培训及计划会议。 ([照片](https://twitter.com/raedahgroup/status/1058493594452004864))
* [Web Summit](https://twitter.com/WebSummit)-里斯本，葡萄牙。非常拥挤的一项活动，很多群众到访Decred展位。@moo31337给葡萄牙总理，Antonio Costa [介绍](https://twitter.com/marco_peereboom/status/1059790693802094592) Decred。@vj和 @jholdstock随后在[这里](https://github.com/heyvj/decred-events/blob/master/reports/20181106-Web-Summit-Lisbon.md)发布了报告。@karamble 在[这](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154258437019744ukkoN:decred.org)发布了更多有关私人区块链公司的笔记(照片: [1](https://twitter.com/NoahPierau/status/1059742659974193153) [2](https://twitter.com/NoahPierau/status/1060107159411810304) [3](https://twitter.com/NoahPierau/status/1060489795485478912) [4](https://twitter.com/blockblanc/status/1060541037733658625) [5](https://twitter.com/NoahPierau/status/1059837388225236992) [整合图](https://twitter.com/LolekBolek74/status/1060551925563826183), 影片在底部)
* [PDX Blockchain Summit & Hackathon](https://pdxblockchainsummit.org) -波特兰，美国。Raedah Group分享Decred的去中心化治理 (照片: [1](https://twitter.com/raedahgroup/status/1061722513615527936) [2](https://twitter.com/dantrevino/status/1061283707099594752))
* [Token Forum](https://www.thetokenforum.com/) 西雅图,美国。@oregonisaac 分享Decred和区块链治理。@Eli-RG [分享](https://decred.slack.com/archives/C66363X44/p1542039292115100)说该活动非常成功并的到许多好评。@oregonisaac在[这](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154183054312819Bkteq:decred.org). ([photo](https://matrix.decred.org/_matrix/media/v1/download/decred.org/RtgfjRzYbrvNjslhOZQNsNtc))也提供了更多的笔记。
* [Blockmaster](https://www.blockmaster.com.br/eventos/forum-blockmaster-2018-sao-paulo/)圣保罗，巴西。@Rhama分享Decred和Politeia(照片: [1](https://matrix.decred.org/_matrix/media/v1/download/decred.org/TgiORGBFSiEAQcuPzPvtZczZ) [2](https://matrix.decred.org/_matrix/media/v1/download/decred.org/UFigpyKJeaOozzbiCeIiNSdH))
* [FinTech Melbourne Community Networking](https://www.meetup.com/Melbourne-FinTech-Startups-Meetup/events/256195153/)-墨尔本，澳大利亚。@eSizeDave [报告](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154217119815341VaPZS:decred.org): "虽然只有一周的见面会宣传时间，反应非常热烈。参与的人很高兴并要求更频繁的举办这类活动。参与的人来自金融机构，金融科技监管分析专员，初创公司，和其他区块链项目代表。两位ANZ银行的数据科学家主动的寻找这类活动并表示很巧的找到了这活动。这表示这类活动有一定的市场需求，这个活动结果很好，我们将更投入参与下一个金融科技类活动。” 随后社群里有更多[讨论](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154220759315790UMKqT:decred.org)。(照片: [1](https://twitter.com/coder_bec/status/1062251105198002177) [2](https://www.instagram.com/p/BqHJmarns8B/))
* [BlockchainFiesta](http://blockchainfiesta.io/)克拉科夫，波兰。@kozel和@donmario和[FXMag](https://www.fxmag.pl/)做了篇还未发布的访问。 完整的[活动报告](https://github.com/heyvj/decred-events/blob/master/reports/20181116-Blockchain-Fiesta-Krakow.md): "我们接触的一些峰会发言人表示对Decred的远见以及“打造第一，炒作第二”的精神印象深刻非常". ([电视新闻](https://krakow.tvp.pl/39996203/kryptowaluty-przyszlosc-platnosci-xxi-wieku)报告,照片: [相册](https://photos.google.com/share/AF1QipOhLa_L0g5NrBWzKFTxMeDD7VJeUBzHzEyker-DRdZGuQoXS9ogpN3waxW26vj0CQ?key=Ty1jZ1NYRkdTY0dRRmNLc1JGcTdNby1BUlZ0eGZ3))
* [Blockchain Melbourne](https://www.meetup.com/BlockchainMelbourne/events/256295215/)-墨尔本，澳大利亚。@eSizeDave 先介绍了Decred,随后两位Apollo Capital代表的演讲。第一位介绍了公司的服务及如何做项目分析，强调Decred如何符合这些标准。第二位演讲人专门讲解了Decred。活动笔记：“非常有知识的人群。令人惊讶的是，尽管我们只有大约1.5周的推广，加上目前低迷的市场环境，我们还有这么多人参与投资分析。此项活动主要归功于@Zohand 与阿波罗资本的长期关系。[相关讨论](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154165462111747igExP:decred.org),[这里](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154271915121075kJobf:decred.org) 和[这里](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154312938324664CVmxQ:decred.org)也有相关的后期笔记。([照片](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154271920421079Uwail:decred.org))
* [Lessons from DevCon4 & Web3 Summit](https://www.meetup.com/Web3-Melbourne/events/bnrhmqyxpblc/)墨尔本，澳大利亚。@eSizeDave: "该活动在RMIT区块链创新中心举行。 皇家墨尔本理工学院（RMIT）是墨尔本的一所大学，也是澳大利亚第一所，作为其经济学院的一部分，建立自己专用区块链创新中心的大学。(......）官方组织者最近从布拉格的Devcon回来，并将介绍从会议中吸取的经验分享。 他们于11月20日参加我们的活动，并邀请我们和Apollo Capital出席介绍Decred，特别是Politeia。“。活动主要是以太坊社区，但Apollo Capital的James介绍的Politeia[貌似](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154340368426560pechG:decred.org)有着不错的效果。([照片](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154340368426560pechG:decred.org))
* 胡志明，越南的与Decred晚饭中@joshuam介绍Decred。主办人([@BitcoinSaigon](https://twitter.com/BitcoinSaigon)) 后来[表示](https://www.facebook.com/BitcoinSaigon/posts/938886146306840): "昨晚激发了一些非常有趣，环绕着本质，重要性和可行性的去中心化系统的讨论，在市场营销声音盖过实质内容的环境，这是非常令人耳目一新的讨论。"(照片: [1](https://www.facebook.com/BitcoinSaigon/posts/938886146306840) [2](https://twitter.com/DominikWeil/status/1068425588258435072))

### 未来活动:

* [The North American Bitcoin Conference](https://btcmiami.com/)-迈阿密，美国。一月16-18。@jy-p 将在主讲台上花15分钟介绍Politeia。他也会探讨更广阔的Politeia应用,包括加密货币，机构及政府角度的应用。例如代币，保存记录，及投票系统。Decred也会有一个10'x8'的活动展位,所以我们需要组织团队。我们希望社区成员可以加入我们，如果您有兴趣请联系 @Dustorf。
* [Campus Party](http://brasil.campus-party.org/cpbr12/patrocinadores/)圣保罗，巴西。二月 12-17。Decred将在hackathons里有发言人和黑客马拉松专属区.
* [Jalisco Talent Land](https://www.talent-land.mx/#entradas) 瓜达拉哈拉，墨西哥。四月22-26。Decred将有一个3x3 m 展位及 10 张峰会门票。@elian将介绍Decred（45分钟）和 Q&A（15分钟）。另外会有两个小时的分组会议。我们将在分组会议里演练如何使用Decrediton，投票流程，选票的生命周期，和如何使用Politeia。如果您有兴趣帮忙或出席请联系@elian。

@jz 发布了一些在会议上代表Decred的[指南](https://gist.github.com/jzbz/4431f620f2bad8032dc3caef2ed9112b)。

## 中文媒体／文章链接
* [老胡评测：比特币核心团队开发永不分裂的币DCR](https://www.jinse.com/bitcoin/265836.html)
* [区块链治理：Decred如何迭代比特币](https://medium.com/@guang.dcr/%E8%AF%91%E6%96%87-%E5%8C%BA%E5%9D%97%E9%93%BE%E6%B2%BB%E7%90%86-decred%E5%A6%82%E4%BD%95%E8%BF%AD%E4%BB%A3%E6%AF%94%E7%89%B9%E5%B8%81-53f434b26105) 
* [DCR 通过混合共识机制平衡权益分配｜标准共识评级](https://michelangelo.sncrating.com/report/168)
* [解析评级 — DCR 通过混合共识机制平衡权益分配](https://medium.com/@guang.dcr/%E8%A7%A3%E6%9E%90%E8%AF%84%E7%BA%A7-dcr-%E9%80%9A%E8%BF%87%E6%B7%B7%E5%90%88%E5%85%B1%E8%AF%86%E6%9C%BA%E5%88%B6%E5%B9%B3%E8%A1%A1%E6%9D%83%E7%9B%8A%E5%88%86%E9%85%8D-%E6%A0%87%E5%87%86%E5%85%B1%E8%AF%86%E8%AF%84%E7%BA%A7-5edc6f03dc1c)
* [扫盲-Decred分票](https://medium.com/@guang.dcr/%E6%89%AB%E7%9B%B2-decred%E5%88%86%E7%A5%A8-ffe3eb2de64d)

## 英文媒体链接
### Articles:

* Blockchain forks and chain splits: why we should avoid them by @Haon ([medium](https://blog.goodaudience.com/blockchain-forks-and-chain-splits-why-we-should-avoid-them-f54c693a90f1), _missed in Oct issue_)
* Marco Peereboom Interview: Governance, Decred & Politeia ([coinbureau.com](https://www.coinbureau.com/interview/marco-peereboom-decred/))
* Decred Infrastructure Interviews: feeleep, Operator, coinmine.pl ([medium](https://medium.com/decred/decred-intriguing-and-extraordinary-an-interview-with-coinmine-pl-mining-pool-operator-5c5592443cb4)) also [in Polish](https://medium.com/decred-polska/decred-interesuj%C4%85cy-i-nieszablonowy-wywiad-z-operatorem-coinmine-pl-11e92657136e))
* PR in Politeia: Process, Progress, and Pitching In by @Dustorf ([medium](https://medium.com/@dlefebvr/pr-in-politeia-process-progress-and-pitching-in-d88771183dd4))
* Blockchain governance: how Decred iterates upon Bitcoin by @zubairzia0 ([medium](https://medium.com/decred/blockchain-governance-how-decred-iterates-upon-bitcoin-3cc7030c655e))
* DCR Ticket Splitting - All you need to know! by @David ([medium](https://medium.com/decred/dcr-ticket-splitting-all-you-need-to-know-b8edc6b65db3), [reddit](https://www.reddit.com/r/decred/comments/9vhpby/decred_ticket_splitting_overview/))
* Hash War Theater: A Costly Spectacle by @richardred ([medium](https://medium.com/@richardred/hash-war-theater-67d3fcac3e97))
* What is Decred? by @kozel (Polish, [bithub.pl](https://bithub.pl/artykuly/czym-jest-decred/))
* Decred Review – Democratic Governance Puts Users in Control ([coiniq.com](https://coiniq.com/decred-review/))
* Smaller PoW coins are in constant danger of 51% attacks – Decred (DCR) governance model is the solution ([captainaltcoin.com](https://captainaltcoin.com/smaller-pow-coins-are-in-constant-danger-of-51-attacks-decred-dcr-governance-model-is-the-solution/))
* Decred Ticket Splitting by @guang (Chinese, [medium](https://medium.com/@guang.dcr/%E6%89%AB%E7%9B%B2-decred%E5%88%86%E7%A5%A8-ffe3eb2de64d))

More articles on various websites were published, but we only listed a selected few. The [decred-media-tracker](https://github.com/RichardRed0x/decred-media-tracker) project is intended to track all articles.

### Translations:

* [Blockchain governance: how Decred iterates upon Bitcoin](https://medium.com/decred/blockchain-governance-how-decred-iterates-upon-bitcoin-3cc7030c655e) by @zubairzia0 - [in Chinese](https://medium.com/@guang.dcr/%E8%AF%91%E6%96%87-%E5%8C%BA%E5%9D%97%E9%93%BE%E6%B2%BB%E7%90%86-decred%E5%A6%82%E4%BD%95%E8%BF%AD%E4%BB%A3%E6%AF%94%E7%89%B9%E5%B8%81-53f434b26105) by @guang
* [Decred: Where did it all begin?](https://thedecreddigest.com/2017/06/10/decred-where-did-it-all-begin/) by @thedecreddigest - [in Spanish](https://medium.com/@decred_es/decred-d%C3%B3nde-comenz%C3%B3-todo-aaa49fed0091) by @elian
* [Decred Recruiting](https://blog.decred.org/2017/07/25/Decred-Recruiting/) by @jy-p - [in Spanish](https://medium.com/@decred_es/c%C3%B3mo-ser-contratista-en-decred-d0f05386f799) by @elian
* [Politeia in Production](https://blog.decred.org/2018/10/15/Politeia-in-Production/) by @jy-p - [in Portuguese](https://stakey.club/translated/politeia-em-producao/) by @mm
* Decred Journal - October 2018 [in Russian](https://medium.com/decred-russia/decred-journal-%D0%BE%D0%BA%D1%82%D1%8F%D0%B1%D1%80%D1%8C-2018-1eeffc65344c) and [in Italian](https://medium.com/decred-ita/decred-journal-ottobre-2018-a68e88c926ff) by @DZ. This is epic work, October issue was a 53 kilobytes of text, 1.5x larger than previous record.
* [Decred Infrastructure Interviews: feeleep, Operator, coinmine.pl](https://medium.com/decred/decred-intriguing-and-extraordinary-an-interview-with-coinmine-pl-mining-pool-operator-5c5592443cb4) by @kozel - [in Polish](https://medium.com/decred-polska/decred-interesuj%C4%85cy-i-nieszablonowy-wywiad-z-operatorem-coinmine-pl-11e92657136e) by @kozel

### Videos:

* Several videos were added to Decred's Texas Bitcoin Conference [playlist](https://www.youtube.com/playlist?list=PLaMrpvQ0yJ_x4L3vtUwfZOM6euh3P8-fx) which now has 18 videos. All 52 videos from the event are in [this playlist](https://www.youtube.com/playlist?list=PLlLSsIJ2O_cTIaALNXExlEqu3jP6IQyc_).
* @moo31337 gave an extended [interview with Paul Snow](https://www.youtube.com/watch?v=MgtBRlAfu2k) after the Texas Bitcoin Conference discussing the behind the scenes history of Decred and other open source projects.
* Videos with @moo31337 from Web Summit: [Investing in Crypto](https://www.youtube.com/watch?v=GO_Iv4vRjZs), [Is crypto here to stay?](https://www.youtube.com/watch?v=L-OzMPHbDi4).
* Crypto with Chingas [interviewed @joshuam](https://www.youtube.com/watch?v=o5jSLGiAdb8) about the importance of dispute resolution in a decentralized project.

Standard & Consensus rated Decred C+. The original report is in [Chinese](https://michelangelo.sncrating.com/report/168) and @guang wrote a [review](https://medium.com/@guang.dcr/%E8%A7%A3%E6%9E%90%E8%AF%84%E7%BA%A7-dcr-%E9%80%9A%E8%BF%87%E6%B7%B7%E5%90%88%E5%85%B1%E8%AF%86%E6%9C%BA%E5%88%B6%E5%B9%B3%E8%A1%A1%E6%9D%83%E7%9B%8A%E5%88%86%E9%85%8D-%E6%A0%87%E5%87%86%E5%85%B1%E8%AF%86%E8%AF%84%E7%BA%A7-5edc6f03dc1c) of it in Chinese also. The weak aspects noted by the report are low social media activity, low trading volume and high liquidity risk. The strong aspects are hybrid PoW+PoS system that balances holders, miners and developers, experienced development team and better sovereignty of the community enabled by voting systems.

## 社区讨论

社区数据(Dec 1):

* Twitter followers 40,004 (-1598)
* Reddit subscribers 9,131 (+147)
* Matrix users 203 (+10)
* Slack users 6,353 (+82)
* Telegram users 4,642 (+213)
* YouTube subscribers 3,736 (+10)
* Facebook 3,105 (+20) followers and 2,867 (+18) likes
* LinkedIn followers: Decred Page 433 (+27), Politeia page 20 (+8) 
* GitHub 447 (+17) stars and 1,159 (+41) forks of dcrd repository

通讯系统新闻：

* 创建聊天室[#research](https://matrix.to/#/!vGasNHFXqjoEWUBTIi:decred.org)处理开源研究提案工作。
* Slack到Matrix的连接受到干扰导致某些信息无法转达。
* 为了解决最近在r/decred 讨论审查事件而设立了一个新的subreddit。更多[讨论](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$154302771624142JbZDI:decred.org). _(bee: yes I'm trolling)_
* 在r/reddit中增加了两项新[规矩](https://www.reddit.com/r/decred/about/rules/): "任何时候只能有一个价格讨论帖子" 和 "不允许喊价"。[这篇文章](https://www.reddit.com/r/decred/comments/9zy3xt/new_rule_one_price_thread_at_a_time/)解释背后的动机。
* 仍然在寻找合适的Discord管理员及实施防垃圾信息系统。
* 在MyEtherWallet 用户有报告指出钓鱼欺骗尝试。请大家保持警惕。

Twitter: 到底公开Politeia投票是否为好的流程[投票](https://twitter.com/KyleSamani/status/1062382292860059648) ; 链上治理区块链[不完全一样](https://twitter.com/spencernoon/status/1062482562482868224), Decred vs Tezos治理系统。

Reddit: DCR 鲸鱼大户对于Decred来说[是好是坏](https://www.reddit.com/r/decred/comments/9t9sju/the_placeholder_whales_good_or_bad_for_decred_in/);使用基金会资金[投资](https://www.reddit.com/r/decred/comments/9wpx1b/treasuryenhancing_products_built_in_top_of_decred/)和利益冲突; 私人torrent追踪器的 Politeia [轴辐路网理论](https://www.reddit.com/r/decred/comments/9yu6pr/politeia_hubandspoke_model_for_private_torrent/); [信任](https://www.reddit.com/r/decred/comments/9zi8tz/will_it_be_possible_to_sign_tickets_with_ledger/) 硬件钱包; 到底已经有[多少](https://www.reddit.com/r/decred/comments/a0utmf/how_many_atomic_swaps_have_actually_been_achieved/)原子互换交易。

## 中文社区讨论

*  讨论 - @Dante正编写节点教程，希望鼓励更多人运行DCR节点。全节点完全是义务贡献没有任何短期收益，只是如果大家都能搭建全节点，网络的健壮性强。比特币现有10000多节点，所以抗打击性很强。DCR想变更安全更去中心化必需把节点数也拉起来。 
*  讨论 - @Neil 与社区讨论DCR的抗分叉性。翻译文章-[详细分析Decred的分叉抵抗性](https://www.dcr66.com/threads/decred.40/) 重新被分享并讨论。
*  分享 - @Guang 分享翻译文章 - [区块链治理：Decred如何迭代比特币](https://www.dcr66.com/threads/decred.992/) 
*  分享 - @Guang 分享 [微博](https://weibo.com/DecredProject)链接终于上线到[Decred项目网站社区](https://www.decred.org/community/)页面，正式加入社区行列。 
*  讨论 - Copay钱包出现漏洞，slack群里Dev澄清对DCR钱包不影响。
*  讨论 - 多个新提案上线，引起了社区的讨论。提案分别是Dex提案，提款机提案，和电台广播广告提案

## 关于月报
11月为英文第8期[GitHub](https://xaur.github.io/decred-news/journal/201811)月报。 点击[这里](https://xaur.github.io/decred-news/)浏览往期月报。


## 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

月报贡献者 @Guang @Hugo @画面

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

