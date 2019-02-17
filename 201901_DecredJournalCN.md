# Decred月报 - 1月 

Decred 以一项重大软件发布和其他重大进展启动了2019年的第一个月份。

新版本节点及钱包软件(v1.4.0)[发布](https://github.com/decred/decred-binaries/releases/tag/v1.4.0) 将启动一项共识规则投票（及其他重大更改）。请大家及时升级。

使用Decred点对点SPV模式的安卓移动钱包(v1.0)已发布。用户可以到[谷歌 Play Store](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet)下载。

@jy-p在博客文章中描述的去中心化交易基础设施 RFP 提案已在Politeia [发布](https://proposals.decred.org/proposals/5431da8ff4eda8cdbf8f4f2e08566ffa573464b97ef6d6bae78e749f27800d3a)。

定义Decred基础信息的社区咨询过程已经[结束](https://pastebin.com/E5L6u2RV)。其中这项消息传递中的标语为：“Decred: Secure. Adaptable. Self-Funding.”。外联工作目前已经转移到计划年度活动。预发布版的[活动](https://www.reddit.com/r/decred/comments/anhh8n/proposal_to_get_events_spending_approved_via/)及[推广](https://www.reddit.com/r/decred/comments/aolr79/politeia_proposal_to_fund_marketing_ops_for_2019/)开销提案也已在聊天室和reddit上共享。

由于二月第一周推出的几项重要发展，本期月报也将包括二月初的一些进展。

## v1.4.0 升级和共识投票

节点及钱包软件v1.4.0版本已发布。请到[GitHub](https://github.com/decred/decred-binaries/releases/tag/v1.4.0)查看完整发布说明和下载链接同时建议务必[验证下载版本](https://docs.decred.org/advanced/verifying-binaries/)。

Decred的1.4.0版本带来了重大改进，同时也包含了一项修改共识规则建议，以修复闪电网络支持的一个bug。建议节点运营尽快升级以协助网络达成升级门槛值。升级软件后, 用户将可设置[投票偏好](https://docs.decred.org/governance/how-to-vote/)。升级进度可在[voting.decred.org](https://voting.decred.org/)查看。

有关共识更改的技术细节请查看[DCP0004](https://github.com/decred/dcps/blob/master/dcp-0004/dcp-0004.mediawiki)和@matheusd发布的[文章](https://matheusd.com/post/dcp0004-and-hardforks/)。

v1.4.0 最终版本和[12月](https://xaur.github.io/decred-news/journal/201812.html)发布的Release Candidate 2版本相比，除了增加了投票议程外并没有其他大的改动。 


## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 在 v1.4.0 RC1 中发现了一个问题在[issue](https://github.com/decred/dcrd/issues/1568)中被提出。对于UTXO反转的设置语义更改意外的修复了一个共识规则漏洞。目前不正确行为将被[保留](https://github.com/decred/dcrd/pull/1570) 至下一个共识更改投票更正。感谢所有帮助发现和修复候选版本中错误的人。

共识更改投票的代码目前已[完成](https://github.com/decred/dcrd/pull/1579)并收录到最终[v1.4.0 发布版](https://github.com/decred/decred-binaries/releases/tag/v1.4.0)。由于闪电网络的需要，该修复和投票应获得优先处理。[DCP004](https://github.com/decred/dcps/blob/master/dcp-0004/dcp-0004.mediawiki) (Decred Change Proposal) 中说明了应该更改的细节并提出对于其他除了闪电网络的应用。这部分工作也为这部分带来[重构](https://github.com/decred/dcrd/pull/1583)及加强测试。 @matheusd 发布了篇[部落格文章](https://matheusd.com/post/dcp0004-and-hardforks/)概述了该漏洞，它的发现和响应方式。

开始讨论如何[改进权益算法](https://github.com/decred/dcrd/issues/1593) 以消除票价震荡-这会使票价变化更加稳定. 

[Decrediton](https://github.com/decred/decrediton): 发布v1.4.0版本客户端并修复了漏洞。

将配置选项指定为命令行参数的功能[合并](https://github.com/decred/decrediton/pull/1975)到主服务器。

[Politeia](https://github.com/decred/politeia): 启用了查看早期版本题案的功能。

正在开发的: 登陆弹出窗口被新的定向文档链接[取代](https://github.com/decred/politeiagui/pull/986) 。 感谢lemonkabir发现了这些[安全](https://github.com/decred/politeia/issues/647) [问题](https://github.com/decred/politeia/issues/650). [缓存层](https://github.com/decred/politeia/pull/660)进入审核阶段。 

讨论:

* 已确定缺少用于审查公共提案的管理员[功能](https://github.com/decred/politeia/issues/662):要有一种方法来删除编辑后包含无关内容的公开提案。 或者，管理员必须先审核所有修改的内容，然后才能在提案系统上显示这些修改的内容。
* [自动化端到端测试](https://github.com/decred/politeiagui/issues/976) 和 [质量检测目录](https://github.com/decred/politeiagui/issues/977) 的变更。
* 大型代码前端 [重构](https://github.com/decred/politeiagui/issues/990)以解决复杂性、性能和开发效率的问题。提出的[解决方案](https://github.com/decred/politeiagui/issues/990#issuecomment-454535696)是使用GraphQL。

[dcrandroid](https://github.com/decred/dcrandroid): 安卓版钱包正式版v1.0发布了! 你可以在Google Play商店获取[主网](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet)或 [测试网](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.testnet)钱包。你可以在[faucet](http://faucet.decred.org/)获取测试网代币。欢迎来[Reddit](https://www.reddit.com/r/decred/comments/am7j40/decred_wallet_for_android_v10_released/)以及[GitHub](http://github.com/decred/dcrandroid/issues)对测试发现的漏洞进行反馈。

与第二个测试版本不同的是, 正式版增加了区块同步进度提示、wifi断开连接报警、 新的启动画面以及漏洞修复。这里是 [更改日志](https://github.com/decred/dcrandroid/compare/v1.0.0-rc2...v1.0.0-rc3)。恭喜dcrandroid团队!

[dcrios](https://github.com/raedahgroup/dcrios):ios钱包在苹果app测试工具Apple TestFlight上[提供](https://testflight.apple.com/join/dvq51tCh)预览版。

[dcrdata](https://github.com/decred/dcrdata):新的主页设计正在 [进行](https://github.com/decred/dcrdata/pull/921)。现在当发现新的区块时，主页上的数值[会自动更新](https://github.com/decred/dcrdata/pull/961)。将汇率监控[添加](https://github.com/decred/dcrdata/pull/951) to the 到后端以便用户查看其实时美元价格。在资源管理器和Mainnet子域上强制使用HTTPS([正在讨论](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$154818146313660CWvZy:decred.org)).

新的主页设计包含汇率、新的地址显示图、改进的图表以及速度的优化，你可以在[beta.dcrdata.org](https://beta.dcrdata.org/)中的测试版v4中[获取](https://twitter.com/decredexplorer/status/1093182831487053825)。 详细的发布说明将与测试版本一起编译。

Dev side: @buck54321正在[破坏](https://github.com/decred/dcrdata/pull/915)命令式jQuery代码. 团队正在准备对Insight API进行压力测试（他们称之为酷刑测试！）。

[Ticket splitting](https://github.com/matheusd/dcr-split-ticket-matcher): 内部代码改进，完成在Decrediton集成的初步工作。创建了一个[监控页面](https://mainnet-split-tickets.matheusd.com/)，它显示所有支持的VSP处在活跃状态。

[docs](https://github.com/decred/dcrdocs):新的页面: [Operating a VSP](https://docs.decred.org/advanced/operating-a-vsp/)概述了搭建vps（Pos池）的配置要求以及维护人员的技能要求, [Solo PoS Voting](https://docs.decred.org/advanced/solo-proof-of-stake-voting/)@jz更新solo投票教程提供给所有文档阅读者, [Address Details](https://docs.decred.org/advanced/address-details/)描述了所有可能的地址类型, [Contributing to Decred](https://docs.decred.org/contributing/contributing-to-decred/)解释了如何成为Decred的付费承包商。

在documentation中对于深层次的安全得出结论，可以汇编对整个空间有益的通用[计算机安全指南](https://github.com/xaur/decred-issues/issues/101)。

[decred.org](https://github.com/decred/dcrweb):@peter_zen [完成](https://github.com/decred/dcrweb/pull/491)了将网站迁移到Hugo的巨大努力。 Hugo是一个用Go语言编写的静态站点生成器，可以更轻松地更新网站内容。已启用多个站点速度[优化](https://github.com/decred/dcrweb/pull/513)。 [voting.decred.org](https://voting.decred.org/) 仪表板正在 [更新](https://github.com/decred/hardforkdemo/commits/master)为即将到来的链上共识投票做准备，祝贺@jholdstock加入Go语言阵营！

Other:

* 新的[Bug Bounty](https://bounty.decred.org/)网站也是用Hugo搭建的。代码[存储库](https://github.com/decred/dcrbounty)对错误报告和贡献是开放的。
* dcrwallet，dcrdocs和dcrweb中的术语得到更改。
* 项目逐渐转向使用更快的“golangci-lint linter”进行开发。
* 在decred.org上[启用](https://github.com/decred/dcrweb/pull/537)了更多安全标头。
* Decred链上数据的[SQL interface](https://www.reddit.com/r/decred/comments/agpkjv/sql_interface_to_live_onchain_decred_data/)可能对研究人员很有意思
* GitHub现在允许私人存储库与最多3个免费帐户的协作者。

1月开发活动数据: 分布于8个存储库（repositories) 有 242 有效PRs, 243 主要提交, 60K 行添加 及 47K 行删除。每个存储库中有来自2-8个开发者的贡献。

---

## 人员

欢迎新到来的首次贡献者，代码在GitHub上合并：Sarlor([dcrd](https://github.com/decred/dcrd/commits?author=Sarlor))，laszlolm([decrediton](https://github.com/decred/decrediton/commits?author=laszlolm))，dezryth ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=dezryth))。

恭喜在decred.org上[列出的](https://github.com/decred/dcrweb/pull/486)6位新贡献者：

* David Habibi (@eSizeDave，社区经理 - 澳大利亚)
* Elian Huesca (@elian，社区经理 - 墨西哥)
* Marcelo Martins (@mm，社区经理 - 葡萄牙)
* Mariusz Szyma (@donmario，社区经理 - 波兰)
* Morphy Tsai (@morphymore，社区经理 - 台湾)
* Tomasz Porwit (@kozel，教育和外展)

4名不活跃的开发者从decred.org中[移除](https://github.com/decred/dcrweb/issues/528): Cruz Molina (@freethinkingaway, dcrdata), Huy Nguyen Tuan (@huyntsgs, dcrwallet), Macaulay Davies (@mcedward), Rohit Nagori.

独立Decred承包商[发布了](https://medium.com/decred/decred-independent-contractor-roadmap-884faba3db39)他们2019年的计划，感谢他们大约15个人的贡献。这篇文章发布了关于路线图，核心规划和承包商自治的 [讨论](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15476119656176jVTYW:decred.org)，以及来自Ditto的评论。

## 治理

1月，[DCR基金会](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了16,776 DCR，并花了9,991 DCR。使用DCR1月份的每日平均美元价格为17.1美元计算，本月收到28.6万美元以及支出17万美元。由于这些付款用于12月完成的工作，因此在12月平均每日费率17.5美元的情况下考虑它们也是有益的 - 在这种情况下，美元收到/支出的数字是29.4万美元以及支出17.5万美元。

承包商现在大约每月15日[收到](https://docs.decred.org/contributing/contributor-compensation/)上个月工作的报酬。分发报酬和收到报酬之间的延迟从30天减少了一半。目前正在努力进一步降低这种延迟。

“RFP：基于Decred的去中心化交换基础设施”提案由@jy-p[提交](https://proposals.decred.org/proposals/5431da8ff4eda8cdbf8f4f2e08566ffa573464b97ef6d6bae78e749f27800d3a)。它在2018年6月第一次描述了构建DEX的动机和高水平的设计[职位](https://blog.decred.org/2018/06/05/A-New-Kind-of-DEX/)。该项目预计在不到6个月内完成，预算在100,000美元至1,000,000美元之间。投票将分两个阶段进行：第一个阶段，提案将决定利益相关方是否想要实现这一目标，如果第一个提案获得批准，那么将邀请感兴趣的团队提出建议，第二阶段将选择其中一个。此过程称为[提议请求](https://en.wikipedia.org/wiki/Request_for_proposal).。

在去年12月成功投票[提案](https://proposals.decred.org/proposals/d33a2667469b56942adf42453def6cc2292325251e4cf791e806939ea9efc9e1)后[推出](https://twitter.com/decredproject/status/1087486930093264897)了Decred Bug Bounty计划（Bug奖励计划）。在[bounty.decred.org](https://bounty.decred.org/)和 [hackernoon](https://hackernoon.com/decred-launches-debug-decred-bug-bounty-program-7e4d2af27ec9)的简介博客帖子上可以查看规则。大部分现场工作归功于@fernandoabolafio和@jholdstock。决定提交和支付有效性的赏金团队包括@degeri，@ddldd，@fernandoabolafio，@jholdstock和@matheusd。恭喜团队顺利推出！

@Dustorf正在准备提高透明度和增加利益相关者对营销活动资金分配的控制的[建议](https://www.reddit.com/r/decred/comments/anhh8n/proposal_to_get_events_spending_approved_via/)。在[matrix](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154896889724431Mxlvj:decred.org)中首次迭代后，发布了预先提案的事件，以便对Reddit提供反馈。营销预算预提案也在[matrix](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154897255124536mFHoo:decred.org)开始，并在第一轮反馈后[记录在reddit中](https://www.reddit.com/r/decred/comments/aolr79/politeia_proposal_to_fund_marketing_ops_for_2019/)。

@oregonisaac正在[寻找](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15474111512672Whvns:decred.org)Java开发人员来评估对于ATM集成的要求。提案草案已在[matrix](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$154828004015153jWdiD:decred.org)中发布和讨论。使用两阶段RFP投票达成了一些共识。讨论的另一个好处是在继续使用ATM之前是否等待移动应用程序发布。

讨论:

* Baeond 提案引起了一阵关于向利益相关者提供代币空投换取提案批准攻击维度的[讨论](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15468733339790vCEoH:decred.org)。
* 关于Politeia目前的[参与率](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15481365491827928DiBLm:matrix.org)和满意度。
* [增强UX](https://github.com/decred/politeia/issues/678)如何可以帮助投票者保持警惕并有效解决坏提案。

## 网络

算力: 1月算力以 ～187 Ph/s开始，以 ～225 Ph/s结束，本月中最高 312 Ph/s及最低 144 Ph/s。在2月8日根据[dcrstats.com](https://dcrstats.com/pow)数据显示，矿池算力分布为：Poolin 29%, F2pool 26%, BTC.com 19%, UUPool 8%, Luxor 4%, CoinMine 1% 及 其他 13%。矿池分布数据为大约值无法精确计算。 

投票: 按2月4日dcrstats.com（数据显示）, 30日 平均票价为 109.4 DCR (+6.4)。价格在 101.5 DCR 至 111.6 DCR之间浮动。锁仓数额为 4.20-4.38 百万 DCR, 大约为总流通量的 46.3-47.5%。

一月份中共有 90 张份票。[数据](https://gist.github.com/oregonisaac/8eb4d50af9fa888c920666fb73ba44b2)自2018年5月起稳定增长。

节点: 截止于2月4日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 197 public listening Node 及 369 Normal Node。版本分布: v1.5.0 dev builds: 4.3% (+2.8%), v1.4.0 dev and rc builds: 13% (+6%), v1.3.0: 55%, v1.2.0: 14% (-6%), v1.1.2: 8% (-2%), v1.1.0: 3% (-1%).

## 挖矿

Obelisk 第2-5批次 [已发货](https://us16.campaign-archive.com/?u=393b2698d17bdfe48ac0422ac&id=4211e39081), 第二代固件 [更新](https://us16.campaign-archive.com/?u=393b2698d17bdfe48ac0422ac&id=c501bf724d) 包含新功能及漏洞修复。用户对于Obelisk SC1 和DCR1 发出了[集体诉讼](https://www.reddit.com/r/decred/comments/ae8hy8/class_action_lawsuit_officially_filed_against/)。

开源Decred挖矿池实现工作由@dnldd[进行中](https://medium.com/decred/decred-independent-contractor-roadmap-884faba3db39)。

## 整合

新矿池(VSP) [dcr.grassfed.network](https://dcr.grassfed.network)加入了目前总共23个VSP的列表。

交易所整合:

* 土耳其交易所 Bitturk [宣布](https://twitter.com/bitturkcom/status/1082201314912862209) DCR/TRY 法币对, 其他讨论及相关背景可参考[这里](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15468134682383442wwDSE:matrix.org)。
* 巴西交易所 BitJa [宣布](https://twitter.com/bitjabr/status/1090066185302036480) DCR/BRL 法币对。

Ellipal 钱包[宣布](https://twitter.com/ellipalwallet/status/1089850526202613760) 在最新固件发布中已支持 Decred。 

Exodus 钱包[集成](https://twitter.com/exodus_io/status/1090263399122923520) USDC, 一个Circle推出的美金挂钩代币。

@kozel的基础设施访问系列第二集[特别访问](https://medium.com/@artikozel/decred-infrastructure-interviews-stephen-founder-of-crypto-only-luxury-goods-marketplace-68d3214a4fd7)Stephen，奢侈品店Crypto Emporium的创始人。他分享了经营企业，接受加密货币，处理订单，供应链和未来计划的见解。

> 我们网站上最畅销的产品无疑是着名的[Decred Jacket](https://www.cryptoemporium.eu/product/decred-jacket/)！非常荣幸能够为Decred社区服务这么长一段时间并帮助推广一个我真正相信的项目。

在使用任何钱包或服务*之前*请务必进行研究，特别是那些保管您资金的服务。

## Adoption

BlueYard [宣布](https://medium.com/@BlueYard/blueyard-2-3d0bbaf1f1b6)第二个基金筹集并解释了他们投资逆势项目的策略。

## 外联活动

推广团队正在[计划](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15468814029997AWtQJ:decred.org)向媒体记者澄清关于Decred的不实新闻。  作为该工作流程的测试案例，社区对一篇可怕的文章进行了详细审查，并且Ditto收集了针对该案例和未来案例的反馈。Ditto有[系统的](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154690407510431bVTJQ:decred.org)收集关于Decred的每一篇报道。随着他们更好地了解社区，可以实时解决不准确问题。另外一个讨论的问题是如何将Ditto的[矫正工作](https://github.com/xaur/decred-issues/issues/71)与社区成员的自发纠正相结合。

Decred的推广标语在[#marketing](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154711632712869dqRko:decred.org)以及[Reddit](https://www.reddit.com/r/decred/comments/afctai/tagline_to_capture_the_decred_project/)上进行了广泛的讨论。最终版本获得最多认可的是“Decred: 安全、适应性强、自有资金”。随着时间的推移，推广标语将会不断修改以应对市场。

1月份来自Ditto的更新:

* 经历了基础消息传递文档的多次迭代，其中包含重要的社区投入，并获得了对[最终版本](https://pastebin.com/E5L6u2RV)的积极反馈。(讨论: [第二版](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154706728112462ubmNo:decred.org),[最终版](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154880432321730DYSYl:decred.org))
* 与社区合作，获取对关于51%攻击的看法，以便将来不可避免的发生攻击时与记者一起使用——目标是当没有什么好消息要分享的时候，在记者面前得到Decred的信息。
* 媒体培训了三名Decred成员。
* 安全的媒体报道：“福布斯”[专题](https://www.forbes.com/sites/leslieankney/2019/01/11/who-should-hold-power-decred-governance-and-what-it-means-for-investors/)文章（[报导](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$1547232200845NiZnO:decred.org)），Joshua对Bitsonline的[视频采访](https://www.youtube.com/watch?v=CUxDxJ4YAUA)，@richardred在[Breaker Mag](https://breakermag.com/what-we-know-about-the-vulnerability-behind-ethereums-rollback-of-constantinople/)以及[Crypto Briefing](https://cryptobriefing.com/scaling-delay-ethereum-constantinople/)中发表了对以太坊硬分叉延迟的相关看法。
* 起草了一个关于bug赏金计划的公告并将其[置于](https://hackernoon.com/decred-launches-debug-decred-bug-bounty-program-7e4d2af27ec9)Hacker Noon上 - 从而与Decred自己的渠道相比，这样可以覆盖更广泛的开发人员。
* 促进了两个正在等待媒体报道的采访。
* 飞到北美比特币会议，在那里，Ditto促成了记者（切达电视台，Altcoin Buzz等等）对Decred的采访，并与团队共度了美妙的时光。
* 与Dustin密切合作并制定了一项活动计划，其中包括Decred想要发表演讲的活动以及想要参加展位的活动。
* 提交了jake的申请，在2019年的共识发言。
* 与Dustin密切合作，制定了2019年上半年的营销和传播计划，涵盖信息传递、媒体培训、媒体关系、活动和演讲以及战略。该计划仍在等待中。

建议个人分享媒体报道，因为其作用与媒体播报一样重要。

有关更多细节，请参阅[1月7日](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154688457110052CiWYd:decred.org)和[1月18日](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15478384869864RTCsv:decred.org)两周的更新。在其中你会发现：

> 社区欢迎并鼓励发言提问，即使有人担心他们的问题是“愚蠢的”。 我们观察到了在其他社区中没有见过的“合作精神”和“自发帮助精神”。 真令人耳目一新！

其它:

* 有[传言](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15478503329998HCAzR:decred.org)称，Ditto可以安排一个有炫酷胡子的人穿上银色Decred夹克。
* @anshawblack在迈阿密的所有唱片店[放下](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154792069410439nSRtR:decred.org)了Decred标识。
* 令人难以置信的商店[更新了](https://www.reddit.com/r/decred/comments/ae07as/custom_decred_merch_with_19_discount_in_the/)额外的物品和新的Decred徽标。 所有产品都可以进行个性化设置和调整。

紧急通知：新批次的Stakey毛绒玩具[可供选择](https://www.reddit.com/r/decred/comments/ahalex/new_batch_of_stakey_plushies_available/)！！

## 社区活动

出席：

* [在美国迈阿密举行的北美比特币会议](https://btcmiami.com/)。 出席率低得惊人：预计会有6000人，结束后统计只有1800人参与。@jy-p的介绍[区块链时间戳](https://btcmiami.com/session/applications-of-blockchain-time-stamping/)的应用做得很好，并且考虑到整体数据，参与人数很多。 3名成员接受了媒体培训，发现它很有用，还有7名预定。 价值存储，“安全、适应性、自筹资金。”，以及随附的消息传递被认为是谈论Decred的一种非常有效的方式。 它被发现是最清晰和最有影响力的。 完整报告，这里有照片和视频的[链接](https://github.com/heyvj/decred-events/blob/master/reports/20190116-tnabc-miami.md)。
* [OKEx Global Meetup Tour](https://www.eventbrite.hk/e/okex-global-meetup-tour-2019-taiwan-tickets-54689867867)在台北举行。 @morphymore讲述了Decred及其工作原理。 “与2018年相比，人们开始更好地认识Decred。有些人告诉我他们从去年的Placeholder's Investment Thesis的中文翻译中了解Decred。这非常令人鼓舞，表明Decred在台湾被更多的人知道。 ([报告](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15478245399446fDEQa:decred.org), [照片](https://photos.app.goo.gl/rXd9PeYmyAGrVTQN7))
* [10 lat Bitcoina](https://10latbitcoina.com.pl/)在波兰的华沙。 @karamble在Decred的基础上谈到了加密货币的长久生存。4人团队与几个加密网点建立了关系，并与一些企业合作。 BitHub.pl指出：“Decred团队成员非常积极地回答那些感兴趣的人的问题，因为这些问题源源不断的在提出！”。([报告](https://github.com/heyvj/decred-events/blob/master/reports/20190126-10LatBitcoina-Warsaw.md))

即将到来的：

* [Campus Party](http://brasil.campus-party.org/cpbr12/patrocinadores/)巴西圣保罗，二月12-17日。
* [How To Keep Your Crypto Secure](https://www.meetup.com/Decred-Australia/events/258211699/) 澳大利亚墨尔本，二月18日。
* [Decred in 30 minutes](https://www.eventbrite.com/e/decred-en-30-minutos-tickets-55764142050) 墨西哥墨西哥城，二月27日。细节可联系@elian。
* [Jalisco Talent Land](https://www.talent-land.mx/#entradas) 墨西哥瓜达拉哈拉，四月22-26日。如果您有兴趣帮忙或出席请联系@elian。

开源及黑客主题活动，如DEFCON，CCC和FOSDEM在这个[issue](https://github.com/xaur/decred-issues/issues/83)中被讨论和记录

## 媒体

社区:

* [blog.dcrclub.org](https://blog.dcrclub.org/)是一个新上线，集合各个文章及翻译于一处的中文网站。源代码在[GitHub](https://github.com/0x5826/blog.dcrclub.org)使得社区更容易贡献或复原网站到其他域名感谢@TogT4V (电报)制作了这个网站。
* @butterfly (@arij on Matrix)开始了新的关于Decred的[阿拉伯语部落格](https://decred-arabia.blogspot.com/2019/01/blog-post.html)。在网站发布阿拉伯文字遇到了一些难题，欢迎到 #writers_room提出建议。
* 葡萄牙语播客由@michae2xl[制作](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$1548814257223928fVjiP:matrix.org), 在[Soundcloud](https://soundcloud.com/user-770106247/), Spotify, Apple Podcasts 及 Google Podcasts 上请搜索"Decred Brasil"。
* [@decredexplorer](https://twitter.com/decredexplorer)是一个专注于dcrdata的新推特账户。感谢 @michae2xl 帮忙组织。
* @Matt D 在电报群[推出](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154825336714293nfWdU:decred.org) [Decred Aggregator](https://t.me/DecredAgg)。目标为集合新闻，媒体，视频，播客，Decred 公告，热门推特和Reddit链接以及市场数据。
* @anshawblack正计划一个播客。

维基百科上的[Decred页面](https://en.wikipedia.org/wiki/Decred)已被删除。 1月8日，用户[删除](https://archive.today/ApV3P)了一堆“坏消息来源”，并在1月10日通过删除大量重要内容来破坏页面。 仅仅4个小时后，另一位用户提名了Decred页面进行删除 - [第三次](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%283rd_nomination%29)尝试将其删除。 作为背景，第二次删除提名的作者对于显着性有着有趣的看法，并被认定为一个“傀儡马甲”。 在1月11日，内容删除被还原，其作者被认定为“傀儡马甲”，但[第二次](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%282nd_nomination%29）删除被另一个用户[继续应用](https://archive.today/fZUHW)，没有太多[提议](https://archive.today/QAlRp)论。 [禁止后](https://en.wikipedia.org/wiki/User:Prince_of_Thieves)，页面变得非常小，所有评论者都投[投票决定](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%283rd_nomination%29)删除它，因为缺乏信誉良好的来源。 所有关于主要加密媒体的最近文章都被认为是[不好的](https://archive.today/4xwaN)参考文献。 1月18日，该页面被删除并从加密货币列表中删除，其中留下了[更多值得注意的加密货币](https://en.wikipedia.org/wiki/List_of_cryptocurrencies)。 有关讨论的详细信息和[链接](https://github.com/xaur/decred-issues/issues/79)，请参阅本期文章。欢迎有经验的维基百科编辑提供帮助。

精选文章（按时间顺序排列）：

* 来自比特币女博士的“DCR的链上治理了解一下” (中文, [qq.com](https://mp.weixin.qq.com/s/z3hzILiPBsLJR72Q2tP7TQ), [英文翻译页面](https://translate.google.com/translate?sl=auto&tl=en&hl=en&u=https%3A%2F%2Fmp.weixin.qq.com%2Fs%2Fz3hzILiPBsLJR72Q2tP7TQ),2018年12月份期刊遗漏记载)
* 来自Piotr Arendarski的“Decred基本面分析”([linkedin.com](https://www.linkedin.com/pulse/funadamental-analysis-decred-dcr-piotr-arendarski-ph-d))
* 来自@jy-p的“如何简单的度过加密货币寒冬？”([coindesk.com](https://www.coindesk.com/how-to-last-the-crypto-winter-seek-simplicity-manage-complexity),标语在#marketing中集体头脑风暴)
* Janusz Zielinski对Decred社区经理@donmario的采访 ([bithub.pl](https://bithub.pl/wywiady/decred-wywiad-z-community-managerem/))
* 最佳Decred钱包：Steve Walters存储DCR的前6位（[coinbureau.com](https://www.coinbureau.com/analysis/best-decred-wallets/)，当作者回应并纠正所有报告的问题时，这是一个很好的案例）
* 谁应该掌握权力？Decred社区自治对其投资者意味着什么。 ([forbes.com](https://www.forbes.com/sites/leslieankney/2019/01/11/who-should-hold-power-decred-governance-and-what-it-means-for-investors/))
* 2019年颁布的独立承包商路线图([medium](https://medium.com/decred/decred-independent-contractor-roadmap-884faba3db39))
* 来自Paul de Havilland的“Decred的独特共识机制——这是真正的权力下放吗？”([bitsonline](https://bitsonline.com/consensus-mechanism-of-decred-decentralization/))
* 来自殷国超的“从福布斯的一篇文章谈Decred（DCR）的价值存储功能”(中文, [qq.com](https://mp.weixin.qq.com/s/_-lY0rtWSPiyLPZeTRR7gg), [英文翻译页面](https://translate.google.com/translate?sl=auto&tl=en&hl=en&u=https%3A%2F%2Fmp.weixin.qq.com%2Fs%2F_-lY0rtWSPiyLPZeTRR7gg))
* 来自Evaluape的“区块链项目审查: Decred:自主的数字货币”([medium](https://medium.com/@EVALUAPE1/blockchain-project-review-decred-8-4-autonomous-digital-currency-323771d65529), Decred评分8.4/10)
* 来自Edwin的“Decred替代比特币？”(荷兰[bitcoinsaltcoins.nl](https://www.bitcoinsaltcoins.nl/decred-coin-review-vervanger-van-btc/),Decred评分8.8/10)
* 来自Daniel Frumkin的“在这个加密货币寒冬，3种加密货币交给Hodl（意见）” ([investinblockchain.com](https://www.investinblockchain.com/cryptocurrencies-hodl-during-crypto-winter/))
* 加密货币的基本价值；比特币和Decred在LCC投资研究中作为价值存储的投资价值([seekingalpha.com](https://seekingalpha.com/article/4235521-fundamental-value-crypto-bitcoin-decred-store-value-investments))
* 来自@richardred的“Decred选民在防御攻击中的作用”([medium](https://medium.com/@richardred/the-role-of-decred-voters-in-defending-against-majority-attacks-ec658af0a8fd))
* 来自@Haon的“在数字货币背景下的链下分散治理”([goodaudience.com](https://blog.goodaudience.com/decentralized-off-chain-governance-in-the-context-of-digital-currencies-ef6db7d97412))
* 来自@kozel的“Decred基础设施访谈：由Stephen创建的仅限加密货币支付的奢侈品市场CryptoEmporium”([medium](https://medium.com/@artikozel/decred-infrastructure-interviews-stephen-founder-of-crypto-only-luxury-goods-marketplace-68d3214a4fd7))
* 来自Lee Banfield的“Decred审查”([weeklyglobalresearch.wordpress.com](https://weeklyglobalresearch.wordpress.com/2019/01/31/decred-dcr-review/))

翻译:

* [Detailed analysis of Decred fork resistance](https://medium.com/decred/detailed-analysis-of-decred-fork-resistance-93022e0bcde7) by @Haon - [俄罗斯语](https://medium.com/decred-russia/%D0%B4%D0%B5%D1%82%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7-%D1%83%D1%81%D1%82%D0%BE%D0%B9%D1%87%D0%B8%D0%B2%D0%BE%D1%81%D1%82%D0%B8-decred-%D0%BA-%D1%84%D0%BE%D1%80%D0%BA%D1%83-b30c78f764ea) by @DZ
* Decred Journal - December 2018 [中文](https://www.jianshu.com/p/65e7a83ac27c) by @guang, [波兰语](https://github.com/artikozel/DecredJournalPL/blob/master/journal/201812_DecredJournalPL.md) by @kozel, [葡萄牙语](https://medium.com/@maiconjunge/jornal-decred-dezembro-de-2018-947c616b894f) by @maiconjunge, [俄罗斯语](https://medium.com/decred-russia/decred-journal-%D0%B4%D0%B5%D0%BA%D0%B0%D0%B1%D1%80%D1%8C-2018-9528f7a9d24d) by @DZ 及 [西班牙语](https://medium.com/@decred_es/revista-decred-diciembre-2018-79093f957aac) by @elian. 哇，感谢大家把Decred月报发扬到全世界！所有的翻译都已收录到此[链接](https://xaur.github.io/decred-news/).

视频:

* 区块链时间戳的应用@jy-p([youtube](https://www.youtube.com/watch?v=3RRTidXh_Lw))
* TNABC的采访 [with @joshuam](https://www.youtube.com/watch?v=Kyihc6Uh4XA)来自Hack Crypto, [with @joshuam](https://bitsonline.com/decred-disputes-inevitable-buirski/)来自Bitsonline, [with @DZ](https://www.youtube.com/watch?v=h3bII-vjOsA), [with @jz](https://www.youtube.com/watch?v=4oKRVXGN6Fs)来自CNBC Crypto Trader。
* 治理：区块链最受忽视的支柱 - 由@oregonisaac在Token Forum 2上发表演讲 ([tfblock.io](https://www.tfblock.io/post/governance-blockchain-s-most-overlooked-pillar))

音频:

* 利用Decred深入挖掘自主加密货币：@moo31337和@BAB谈论分散决策和自筹资金如何使得Decred能够建立一个强大的，不断发展的数字货币且不受第三方影响（与Rachel Wolfson一起使用Crypto Chick Podcast），[badcryptopodcast.com](https://badcryptopodcast.com/2019/01/08/autonomous-crypto-decred/))
* Noah Pierau关于区块链治理：Decred、比特币、Dash、以太坊（Tom Shaughnessy、[itunes](https://itunes.apple.com/us/podcast/noah-pierau-on-blockchain-governance-decred-bitcoin/id1438148082?i=1000428113722&mt=2)的51%加密研究）
* 来自Marco Peereboom的“怎样革命性的改变加密货币” Michael Nye和Marco讨论了当前的加密状态，Decred是如何开始的，PoW与PoS，Decred的自治基金会模式等(Evolvement播客, [evolvement.io](https://evolvement.io/how-decred-revolutionizes-funding-in-crypto-with-marco-peereboom/))

## 社区讨论

截止于 Feb 4 的社区数据 :

* Twitter followers: 39,778 (-106)
* Reddit subscribers: 9,330 (+89)
* Matrix users: 247 (+26)
* Slack users: 6,529 (+110)
* Telegram users: 4,503 (-231)
* YouTube subscribers: 3,752 (+14)
* Facebook followers: 3,132 (+11), likes: 2,891 (+11)
* LinkedIn followers: Decred page 466 (+16), Politeia page 27 (+3)
* GitHub dcrd stars: 468 (+10), forks: 1,221 (+29)

社交系统新闻：

* Twitter不明原因且缓慢的[掉粉](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$1549500437341uJIFK:decred.org)欢迎任何的想法提交。
* 电报群粉丝减少可能是由于机器人的剔除。
* @sambiohazard写了一个彻底的[计划](https://github.com/xaur/decred-issues/issues/16)来解决Discord垃圾邮件，实施它，并测试在最初几周后报告没有收到垃圾邮件。 几个重要的渠道与Discord联系在一起。 有了这个，我们终于可以将Discord作为一个机会来吸引更多人。 谢谢！
* [decred.org/matrix](https://decred.org/matrix/)引导新matrix用户进入系统。
* 截至2月9日，[decred-issues](https://github.com/xaur/decred-issues）增加到105个问题。看看，也许你会发现一些有趣的事情要做！

来自比特币极端主义者的[批评](https://twitter.com/tonevays/status/1086702239853379584)引发了关于Decred如何看待证券法背景的[讨论](https://www.reddit.com/r/decred/comments/ahuawl/decred_launch_security_laws/)。 一位矢量评论家使用的是Decred的预设和空投是不公平和“手选”。 这是对过滤掉空投作弊者的（巨大的）手工努力的误导，根据[这一讨论](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154810656412322VrQLg:decred.org)也有很多有用的链接描述了Decred开始的发布。 一个有趣的见解是，约300K（35％）空投硬币从未移动过。 另一个相关的[聊天](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$15467943549316LjeYZ:decred.org)是关于Twitter攻击声称Decred的初始分发是如何不透明或公平的，同时避免了有关比特币早期采矿和Satoshi百万BTC的不便事实。 最后，[历史解释了](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15467944729319gvTvt:decred.org)早期的赌注，并指出原始开发者从第1天开始就没有单方面控制共识规则。

建立Reddit社区的重要性存在巨大争论。 [查看详情](https://www.reddit.com/r/decred/comments/aib2x3/noah_pierau_on_blockchain_governance_decred/)。

## 市场

在一月中DCR交易价格为 美金 15.5-19.5 / BTC 0.00435-0.00487。平均日汇率为 17.1美元。

## 相关外部信息

以太坊经典（ETC）受到51％的攻击，CoinNess于1月7日提出警报。然后[CoinNess](https://www.coinness.com/news/198264)宣布它已经检测到ETC链的深度重组并停止了ETC交易。 文章列出了涉及双重花费的一些重组，在15个不同的重组活动中涉及的总金额为110万美元。 Coinbase[本身](https://blog.coinbase.com/ethereum-classic-etc-is-currently-being-51-attacked-33be13ce32de)并不是这些攻击的目标。 Gate.io交易所随后[公布了](https://www.gate.io/article/16735)它已成为目标并且已经损失了大约20万美元，并且它将承担损失。 Gate.io还显着增加了ETC存款所需的确认数量。 在一个不寻常的发展中，攻击者随后将100万美元的ETC[返还](https://www.gate.io/article/16740)给Gate.io，他们已经尝试但未能与攻击者联系并且不知道返还资金的原因。 ETC双重花费的其他受害者还没有挺身而出。

Ethereum的开发人员（暂时）于1月4日[决定](https://www.coindesk.com/ethereum-developers-give-tentative-greenlight-to-asic-blocking-code)继续将Ethash的挖矿算法改为ProgPoW。 此举旨在阻止ASIC开采以太坊。 Block[概述](https://www.theblockcrypto.com/2019/01/11/despite-core-dev-consensus-proposition-progpow-faces-community-concerns/)了转换后降低的攻击成本，GPU矿工的激励措施较弱，从Bitmain和Innosilicon向AMD和Nvidia转移电力的好处以及可能出现连锁拆分等问题。 他们的结论是围绕算法转换的辩论将是以太坊治理过程的一个很好的测试。

以太坊开发商也在1月15日[推迟](https://breakermag.com/what-we-know-about-the-vulnerability-behind-ethereums-rollback-of-constantinople/)了君士坦丁堡的硬分叉，因为一个安全漏洞可能会[导致](https://medium.com/chainsecurity/constantinople-enables-new-reentrancy-attack-ace4088297d9).“重放攻击”。

David Vorick撰写的“工作量证明基础”[文章](https://blog.sia.tech/fundamentals-of-proof-of-work-beaa68093d2b)介绍了独有的硬件加密货币，并将其与存在多个问题的共享硬件加密货币进行了对比，特别是那些追求ASIC阻力的问题。 非专用硬件的一个问题是硬件的价值与资产没有密切关系（因为它可以挖掘许多其他链）。 另一个问题是哈希算力市场，它们允许硬件所有者通过出租他们的设备开采其它加密货币获得更多利润，即使哈希值被租给攻击者。 从专用硬件中获得的好处是迄今为止其算法（Blake256r14）的主要硬币。 虽然这个硬件不能被认为是Decred的“独家”，但除了当前的哈希值优势之外，Decred还有PoS共识能够拒绝对行为不端的矿工（例如打包空块）。

第一轮Aragon提案投票于1月26日[结束](https://blog.aragon.org/final-results-from-aragon-network-vote-1/)。在提交的12项提案中，3项被Aragon贡基金会排除在投票之外（1名因缺乏全职领导和工程人才，2名被排除在外，以减少对选民的认知负担）。 投票通过的9项提案中有8项获得了ANT持有人的[批准](https://mainnet.aragon.org/#/governance.aragonproject.eth/0x277bfcf7c2e162cb1ac3e9ae228a3132a75f83d4)，其中一项提案（将投票期限从48小时改为1周）被拒绝。 ANT参与率[介于](https://mainnet.aragon.org/#/governance.aragonproject.eth/0x277bfcf7c2e162cb1ac3e9ae228a3132a75f83d4)2.3％至7.8％之间。 要获得批准的最昂贵的[建议](https://github.com/aragon/flock/blob/master/teams/Aragon%20One/2019.md)将向Aragon One支付400万美元的2019年运营成本加上一项激励计划，其中包括一项为期5年的归属计划中的167.5万ANT。 除了在DAI中支付的主要成本之外，大多数提案都包括ANT的奖励和归属时间表。 总共这一轮批准的提案将耗资约594万美元+252万ANT（约合880,000美元）。

EOS的宪法修正案公民投票制度于1月11日开始[实施](https://medium.com/@eosnationbp/the-fate-of-eos-is-in-the-hands-of-token-holders-3d345147ef6)。迄今已[提交](https://bloks.io/vote/referendums)了77项提案。 这些提案的投票期是灵活的，由提交者指定，有些期限长达四个月。 得票最多的投票（截至1月31日）的投票率约为流通EOS的2％，但大多数提案的参与率非常低（只有10个参与者的参与率超过0.5％）。 到目前为止，最受欢迎的建议[改变](https://bloks.io/vote/referendums/rex4all)简称和RAM购买的费用，[删除](https://bloks.io/vote/referendums/decaf)EOS核心仲裁论坛，并在eosio.saving中[燃烧](https://bloks.io/vote/referendums/burnsaving)通货膨胀资金（用于资助工人提案系统）。

NEM基金会[宣布](https://forum.nem.io/t/nem-foundation-message-to-the-community/21753)其财务困难，需要缩减其员工队伍。 1月1日，一个新的理事会接管了这个基金会，当他们打开记录时，他们看到了一个问题。 上一届理事会每月的燃烧率为900万XEM（现在为360,000美元，当时要多得多），这是独立区域实体在促销活动中花费很少的责任。 这被认为是不可持续的，新的理事会已经重组了基金会，目前正在寻求额外的资金。

Wassim Alsindi（@parallelind）“分叉学”的研究随着[最新](https://medium.com/@parallelind/forkonomy-revisited-where-are-they-now-73fbfbec6b4d)的更新[发布](https://hackernoon.com/towards-an-analytical-discipline-of-forkonomy-summer-2018-e6da993ee3f9) 。

Hcash项目fork（复制并修改）了几个Decred的[项目](https://archive.today/rEhWX)：[Autonomy](https://archive.today/KTCdX)（Politeia），[hcexplorer](https://archive.today/2KTtW)和[hctime](https://archive.today/K151A)e。 在Politeia，他们[意外](https://archive.today/ECplt)删除了Decred开发人员的版权，忘了重命名该项目。 收到通知后，他们迅速做出反应，删除多个存储库，[恢复](https://github.com/TKFORKED/autonomy/commit/4b05c2c31829df64be69e546d939a563247e1927)许可证并将Politeia fork[重命名](https://github.com/TKFORKED/autonomy/commit/98d5f63f676e45e6a91eba99da3db985effdb1f2)为Autonomy。 [修复](https://twitter.com/michae2xl/status/1084270468234915840)了一些微妙Decred图标。 一些[项目](https://archive.today/https://github.com/HcashOrg/hc*)被分叉，它们的提交历史被删除，并且没有在GitHub上将它们标记为分叉。 他们的subreddit上的投诉([1](https://www.reddit.com/r/hcash/comments/adwmx2/hcash_being_shady_again/), [2](https://www.reddit.com/r/hcash/comments/afepsc/hcash_cant_be_bothered_to_change_the_decred_logo/))被默默审查，没有回复。哇哦，[r/hcash](https://archive.today/Edy7T)样式看起来很熟悉。 在[这里](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$154696507010921TRgid:decred.org)讨论。

一个[令人遗憾的例子](https://twitter.com/BrianDColwell/status/1090286752831434752)，说明当团队资金耗尽时会发生什么。

ICO项目于2018年12月从总量中[收回](https://diar.co/ethereum-ico-treasury-balances/)了约441K ETH（截至2月9日为5,250万美元）。

[Staked](https://staked.us/about/)是一家为机构投资者提供赌注服务的创业公司，从[CoinDesk](https://www.coindesk.com/pantera-coinbase-join-4-5-million-round-in-staking-as-a-service-startup), [The Block](https://www.theblockcrypto.com/2019/01/31/winklevoss-twins-pantera-get-behind-a-new-business-thats-capitalizing-on-a-new-trend-sweeping-crypto-hedge-funds/)，[Bloomberg](https://www.bloomberg.com/news/articles/2019-02-01/some-crypto-investors-are-playing-it-safe-after-volatile-run)等公司筹集了450万美元。 由CoinDesk，The Block和Bloomberg所涵盖。 Staked自2018年11月开始运营Decred [VSP](https://decred.staked.us/)。

Binance现在[允许](https://support.binance.com/hc/en-us/articles/360022498052)用Visa和MasterCard购买加密货币（[限制](https://support.binance.com/hc/en-us/articles/360022204152)列表告诉我们关于Decred的事情）。

Coinbase[禁止](https://cryptocoinspy.com/coinbase-bans-gab-again/)社交媒体平台Gab的账户。 这不是交易所暂停账户的[第一个](https://www.cnbc.com/2018/04/23/coinbase-suspends-wikileaks-bitcoin-account.html)大案例。

Medium[审查](https://bitcoinist.com/how-to-use-bitcoin-anonymously-ban-medium/)了一篇文章“如何匿名使用比特币”，这引发了讨论以及有关迁移它的[问题](https://github.com/xaur/decred-issues/issues/70)，或者至少将其视为多个内容镜像之一。 备份您的Medium帖子，以防万一。

国际清算银行（Bank for International Settlements）发布了一项非常乐观的加密货币[研究](https://www.bis.org/publ/work765.htm)。

[Vulnerability](https://cryptoslate.com/researchers-discover-vulnerability-bitcoin-ethereum-ripple-digital-signatures/)在比特币和其他一些系统的数字签名中发现了漏洞。 使用签名算法的错误实现生成了一小组签名，该签名算法可用于显示私钥。 在审查的近10亿比特币签名中，只有几千个签名易受攻击。 据研究人员称，绝大多数加密货币用户不必担心。

历史上最大的数据泄露包含数千个被黑客入侵的 [数据库](https://www.troyhunt.com/the-773-million-record-collection-1-data-reach/)。 明智地选择与谁共享数据。

Cryptopia被[黑客攻击](https://www.investinblockchain.com/cryptopia-hack-estimated-16-million-lost/)，损失估计在3-16百万美元之间。 Binance[冻结](https://www.investinblockchain.com/binance-freezes-funds-cryptopia-hack/) 了来自黑客的一些资金。

据最新报道，针对比特币矿机的新一波hAnt[感染](https://www.zdnet.com/article/new-ransomware-strain-is-locking-up-bitcoin-mining-rigs-in-china/)（首次见于8月）。 勒索软件需要感染1000个其他设备需其支付10 BTC，否则它可能会烧毁钻机。 到目前为止，没有关于设备被毁的报告。

称为假冒PoS股权攻击的资源耗尽漏洞是在26个基于PoSv3的区块链中[发现](https://medium.com/@dsl_uiuc/fake-stake-attacks-on-chain-based-proof-of-stake-cryptocurrencies-b8b05723f806)的，其中大多数都采用了缓解措施。 部分原因在于，在许多此类系统中，股权证明层不安全地“嫁接”到比特币核心代码库。 报告的一位作者发推文说Decred[没有受到影响](https://twitter.com/Sanket1729/status/1087829688347701254)。


## 关于月报
1月为英文第10期 [GitHub](https://xaur.github.io/decred-news/journal/201901) 月报。 点击[这里](https://xaur.github.io/decred-news/)浏览所有往期月报，翻译等。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues) 和 [Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

感谢 (按字母排序): bee, davecgh, degeri, Dustorf, guang, Haon, jholdstock, liz_bagot, lukebp, matheusd, richardred, zubairzia0.


## 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

感谢 (按字母排序): 
