# Decred月报 - 12月 

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

共识更改投票的代码目前已[完成](https://github.com/decred/dcrd/pull/1579)并收录到最终[v1.4.0 发布版](https://github.com/decred/decred-binaries/releases/tag/v1.4.0)。由于闪电网络的需要，该修复和投票应获得优先处理。[DCP004](https://github.com/decred/dcps/blob/master/dcp-0004/dcp-0004.mediawiki) (Decred Change Proposal) 中说明了改更改的细节并提出对于其他除了闪电网络的应用。这部分工作也为这部分带来[重构](https://github.com/decred/dcrd/pull/1583)及加强测试。 @matheusd 发布了篇[部落格文章](https://matheusd.com/post/dcp0004-and-hardforks/)概述了该漏洞，它的发现和响应方式。

开始讨论如何[改进权益算法](https://github.com/decred/dcrd/issues/1593) 以消除票价震荡-这会使票价变化更加稳定. 

[Decrediton](https://github.com/decred/decrediton): 发布v1.4.0版本客户端并修复了漏洞。

将配置选项指定为命令行参数的功能[合并](https://github.com/decred/decrediton/pull/1975)到主服务器。

[Politeia](https://github.com/decred/politeia): 启用了查看早起版本题案的功能。

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

在去年12月成功投票[提案](https://proposals.decred.org/proposals/d33a2667469b56942adf42453def6cc2292325251e4cf791e806939ea9efc9e1)后[推出](https://twitter.com/decredproject/status/1087486930093264897)了Decred Bug Bounty计划（Bug奖励计划）。在[bounty.decred.org](https://bounty.decred.org/)和 [hackernoon](https://hackernoon.com/decred-launches-debug-decred-bug-bounty-program-7e4d2af27ec9)的简介博客帖子上可以查看规则。大部分现场工作归功于@fernandoabolafio和@jholdstock。决定提交和支付有效性的赏金团队包括@ degeri，@ ddldd，@ fernandoabolafio，@ jholdstock和@matheusd。恭喜团队顺利推出！

@Dustorf正在准备提高透明度和增加利益相关者对营销活动资金分配的控制的[建议](https://www.reddit.com/r/decred/comments/anhh8n/proposal_to_get_events_spending_approved_via/)。在[matrix](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154896889724431Mxlvj:decred.org)中首次迭代后，发布了预先提案的事件，以便对Reddit提供反馈。营销预算预提案也在[matrix](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154897255124536mFHoo:decred.org)开始，并在第一轮反馈后[记录在reddit中](https://www.reddit.com/r/decred/comments/aolr79/politeia_proposal_to_fund_marketing_ops_for_2019/)。

@oregonisaac正在[寻找](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15474111512672Whvns:decred.org)Java开发人员来评估对于ATM集成的要求。提案草案已在[matrix](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$154828004015153jWdiD:decred.org)中发布和讨论。使用两阶段RFP投票达成了一些共识。讨论的另一个好处是在继续使用ATM之前是否等待移动应用程序发布。

讨论:

* Baeond proposal spurred a [discussion](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15468733339790vCEoH:decred.org) of an attack vector where stakeholders are offered an airdrop of some token in return for them approving a proposal.
* [Engagement](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15481365491827928DiBLm:matrix.org) and satisfaction with Politeia so far.
* How [UX enhancements](https://github.com/decred/politeia/issues/678) can help voters to pre-emptively address bad proposals and stay vigilant.

## 网络

算力: 1月算力以 ～187 Ph/s开始，以 ～225 Ph/s结束，本月中最高 312 Ph/s及最低 144 Ph/s。在2月8日根据[dcrstats.com](https://dcrstats.com/pow)数据显示，矿池算力分布为：Poolin 29%, F2pool 26%, BTC.com 19%, UUPool 8%, Luxor 4%, CoinMine 1% 及 其他 13%。矿池分布数据为大约值无法精确计算。 

投票: 按2月4日dcrstats.com（数据显示）, 30日 平均票价为 109.4 DCR (+6.4)。价格在 101.5 DCR 至 111.6 DCR之间浮动。锁仓数额为 4.20-4.38 百万 DCR, 大约为总流通量的 46.3-47.5%。

一月份中共有 90 张份票。[数据](https://gist.github.com/oregonisaac/8eb4d50af9fa888c920666fb73ba44b2)自2018年5月起稳定增长。

节点: 截止于2月4日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 197 public listening Node 及 369 Normal Node。版本分布: v1.5.0 dev builds: 4.3% (+2.8%), v1.4.0 dev and rc builds: 13% (+6%), v1.3.0: 55%, v1.2.0: 14% (-6%), v1.1.2: 8% (-2%), v1.1.0: 3% (-1%).

## 挖矿

Obelisk 第2-5批次 [已发货](https://us16.campaign-archive.com/?u=393b2698d17bdfe48ac0422ac&id=4211e39081), 第二代固件 [更新](https://us16.campaign-archive.com/?u=393b2698d17bdfe48ac0422ac&id=c501bf724d) 包含新功能及漏洞修复。用户对于Obelisk SC1 和DCR1 发出了[集体诉讼](https://www.reddit.com/r/decred/comments/ae8hy8/class_action_lawsuit_officially_filed_against/)。

Open source Decred mining pool implementation is [in the works](https://medium.com/decred/decred-independent-contractor-roadmap-884faba3db39) by @dnldd.

## 整合

New VSP [dcr.grassfed.network](https://dcr.grassfed.network) joined a list of total 23 VSPs.

Exchange integrations:

* Turkish exchange Bitturk [announced](https://twitter.com/bitturkcom/status/1082201314912862209) DCR/TRY fiat pair, discussion and some background [here](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15468134682383442wwDSE:matrix.org).
* Brazilian exchange BitJa [announced](https://twitter.com/bitjabr/status/1090066185302036480) DCR/BRL fiat pair.

Ellipal wallet [announced](https://twitter.com/ellipalwallet/status/1089850526202613760) Decred support in latest firmware release.

Exodus wallet [integrated](https://twitter.com/exodus_io/status/1090263399122923520) USDC, a USD-pegged token by Circle.

Second episode of infrastructure interview series by @kozel [featured](https://medium.com/@artikozel/decred-infrastructure-interviews-stephen-founder-of-crypto-only-luxury-goods-marketplace-68d3214a4fd7) Stephen, founder of the luxury goods outlet Crypto Emporium. Stephen shared insights into running a business, accepting crypto, processing orders, supply chain and future plans.

> Our best selling product on the website has undoubtedly been the famed [Decred Jacket](https://www.cryptoemporium.eu/product/decred-jacket/)! It's been an honour to serve the Decred community for so long and help market a project I truly believe in.

Always do your research _before_ using wallets or services, especially those that take custody of your funds.

## Adoption

BlueYard [announced](https://medium.com/@BlueYard/blueyard-2-3d0bbaf1f1b6) second fund raise and explained their strategy of investing into contrarian projects.

## 外联活动

Marketing team is [planning](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15468814029997AWtQJ:decred.org) to approach reporters publishing inaccuracies about Decred. As a test case for that workflow one horrible article was scrutinized by the community and Ditto collected the feedback for that and future cases. Ditto has [systems](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154690407510431bVTJQ:decred.org) to catch every piece of media written about Decred. As they get to know the community better, it will be possible to address inaccuracies in real time. Another issue discussed was integrating Ditto's [corrections workflow](https://github.com/xaur/decred-issues/issues/71) with voluntary submissions from the community.

Tagline for Decred was extensively discussed [in #marketing](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154711632712869dqRko:decred.org) and [on Reddit](https://www.reddit.com/r/decred/comments/afctai/tagline_to_capture_the_decred_project/). Final version of messaging settled it on "Decred: Secure. Adaptable. Self-Funding." which gathered most support. As time goes this will be revised to adapt to the ever changing space.

January update from Ditto:

* Went through several iterations of the foundational messaging document with significant community input and received positive feedback on the [final version](https://pastebin.com/E5L6u2RV). (discussions: [second](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154706728112462ubmNo:decred.org) version, [final](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154880432321730DYSYl:decred.org) version)
* Worked with the community to source commentary on 51% attacks for future use with reporters when another attack inevitably happens - the goal being to get Decred's message in front of journalists even when it doesn't have any hard news to share.
* Media trained three Decred members.
* Secured media coverage: [feature article](https://www.forbes.com/sites/leslieankney/2019/01/11/who-should-hold-power-decred-governance-and-what-it-means-for-investors/) in Forbes ([report](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$1547232200845NiZnO:decred.org)), [video interview](https://www.youtube.com/watch?v=CUxDxJ4YAUA) with Joshua for Bitsonline, commentary by @richardred on the delay in Ethereum's hard fork in [Breaker Mag](https://breakermag.com/what-we-know-about-the-vulnerability-behind-ethereums-rollback-of-constantinople/) and [Crypto Briefing](https://cryptobriefing.com/scaling-delay-ethereum-constantinople/).
* Drafted an announcement of the bug bounty program and [placed](https://hackernoon.com/decred-launches-debug-decred-bug-bounty-program-7e4d2af27ec9) it in Hacker Noon - thereby reaching a much broader pool of developers, compared to Decred's own channels.
* Facilitated two interviews that are pending media coverage.
* Flew down to the North American Bitcoin Conference, where Ditto facilitated interviews between Decred and reporters (Cheddar TV, Altcoin Buzz, etc.) and spent quality time with the team.
* Worked closely with Dustin on an events plan that encompasses both events Decred wants to speak at and events it wants to have a booth at.
* Submitted an application for Jake to speak at Consensus 2019.
* Worked closely with Dustin on a marketing and communications plan for the first half of 2019, spanning messaging, media training, media relations, events and speaking, and strategy. This plan is still pending.

Individuals are advised to share media coverage because amplification is just as important as the media placement itself.

For even more detail see the biweekly updates on [Jan 7](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154688457110052CiWYd:decred.org) and [Jan 18](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15478384869864RTCsv:decred.org). Nice discovery in one of them:

> The community welcomes and encourages questions, even if the person asking fears that their questions are "stupid." We've observed a spirit of collaboration and willingness to help that we haven't seen in other communities. It's refreshing!

Other:

* It is [rumored](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15478503329998HCAzR:decred.org) that Ditto can arrange a mad beard that entitles one to wear Silver Decred Jacket.
* @anshawblack [dropped](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154792069410439nSRtR:decred.org) Decred merch in all record stores of Miami.
* Decredible shop was [renewed](https://www.reddit.com/r/decred/comments/ae07as/custom_decred_merch_with_19_discount_in_the/) with extra items and new Decred logos. All products can be personalized and tweaked.

Urgent Notice: new batch of Stakey plushies is [available](https://www.reddit.com/r/decred/comments/ahalex/new_batch_of_stakey_plushies_available/)!

## 社区活动

Attended:

* [The North American Bitcoin Conference](https://btcmiami.com/) in Miami, USA. Attendance was surprisingly low: 6K people were expected but only 1.8K were claimed after the event. @jy-p's presentation [Applications of Blockchain Time-Stamping](https://btcmiami.com/session/applications-of-blockchain-time-stamping/) was well done and well attended given the overall numbers. 3 members went through media training and found it useful, 7 more are scheduled. Store of value, "Secure. Adaptable. Self-Funding.", and the accompanying messaging was found to be a very effective way of talking about Decred. It was found to be most clear and impactful. Full report with links to photos and videos [here](https://github.com/heyvj/decred-events/blob/master/reports/20190116-tnabc-miami.md).
* [OKEx Global Meetup Tour](https://www.eventbrite.hk/e/okex-global-meetup-tour-2019-taiwan-tickets-54689867867) in Taipei, Taiwan. @morphymore told the story of Decred and how it works. "Compared to 2018, people are starting to recognize Decred better. A few people told me that they know about Decred from the Chinese translation I did last year of the Placeholder's Investment Thesis. It was very encouraging and shows that the Decred awareness in Taiwan is indeed growing." ([report](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15478245399446fDEQa:decred.org), [photos](https://photos.app.goo.gl/rXd9PeYmyAGrVTQN7))
* [10 lat Bitcoina](https://10latbitcoina.com.pl/) in Warsaw, Poland. @karamble talked about longevity in cryptocurrencies on the basis of Decred. The team of 4 people established relations with several crypto outlets and engaged with a few businesses. BitHub.pl noted: "The Decred boys were intensely engaged in answering questions of those interested displaying tons of patience at that, since the questions poured in basically all the time!". ([report](https://github.com/heyvj/decred-events/blob/master/reports/20190126-10LatBitcoina-Warsaw.md))

Upcoming:

* [Campus Party](http://brasil.campus-party.org/cpbr12/patrocinadores/) in Sao Paulo, Brazil on Feb 12-17.
* [How To Keep Your Crypto Secure](https://www.meetup.com/Decred-Australia/events/258211699/) in Melbourne, Australia on Feb 18.
* [Decred in 30 minutes](https://www.eventbrite.com/e/decred-en-30-minutos-tickets-55764142050) in Mexico City, Mexico on Feb 27. Contact @elian for details.
* [Jalisco Talent Land](https://www.talent-land.mx/#entradas) in Guadalajara, Mexico on Apr 22-26. Contact @elian if you're interested in helping/attending.

Open source and hacker oriented events like DEFCON, CCC and FOSDEM were discussed and captured in [this issue](https://github.com/xaur/decred-issues/issues/83).

## 媒体

Community initiatives:

* [blog.dcrclub.org](https://blog.dcrclub.org/) is a new website in Chinese that collects various articles and translations in one place. The source hosted [on GitHub](https://github.com/0x5826/blog.dcrclub.org) makes it easy to contribute or mirror the website on other domain for more resiliency. Credits to @TogT4V (Telegram) for starting the site.
* New [Arabic blog](https://decred-arabia.blogspot.com/2019/01/blog-post.html) about Decred started by @butterfly (@arij on Matrix). There are some challenges with publishing arabic text on the web, advice is welcome in #writers_room.
* Portuguese podcasts [started](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$1548814257223928fVjiP:matrix.org) by @michae2xl, available on [Soundcloud](https://soundcloud.com/user-770106247/), Spotify, Apple Podcasts and Google Podcasts - search for "Decred Brasil".
* [@decredexplorer](https://twitter.com/decredexplorer) is a new Twitter account dedicated to dcrdata. Thanks to @michae2xl for organizing.
* @Matt D [introduced](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154825336714293nfWdU:decred.org) [Decred Aggregator](https://t.me/DecredAgg) Telegram channel. It aims to collect news, press, videos, podcasts, Decred announcements, trending tweets and Reddit posts, as well as market stats.
* @anshawblack is planning a podcast.

[Decred page](https://en.wikipedia.org/wiki/Decred) on Wikipedia was deleted. On Jan 8 a user [removed](https://archive.today/ApV3P) a bunch of "bad sources" and on Jan 10 vandalized the page by removing a large and important part of content. Just 4 hours later another user nominated Decred page for deletion - the [3rd attempt](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%283rd_nomination%29) to take it down. For background, the author of [2nd nomination](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%282nd_nomination%29) for deletion had interesting [views](https://archive.today/QAlRp) on notability and was [banned](https://en.wikipedia.org/wiki/User:Prince_of_Thieves) as a sockpuppet. On Jan 11 content removal was reverted and its author was banned as sockpuppet, but next day the removal was [applied again](https://archive.today/fZUHW) by another user without much commentary. After the slicing the page became very small and all reviewers [voted](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%283rd_nomination%29) to delete it due to lack of reputable sources. All suggested recent articles in major crypto media were deemed [not good enough](https://archive.today/4xwaN) references. On Jan 18 the page was deleted and removed from [List of cryptocurrencies](https://en.wikipedia.org/wiki/List_of_cryptocurrencies) that was left with more notable coins. Details and links to discussions are captured in [this issue](https://github.com/xaur/decred-issues/issues/79). Experienced Wikipedia editors are welcome to help.

Selected articles (chronological order):

* Understanding Decred Governance by Dr. Bitcoin (Chinese, [qq.com](https://mp.weixin.qq.com/s/z3hzILiPBsLJR72Q2tP7TQ), [translation](https://translate.google.com/translate?sl=auto&tl=en&hl=en&u=https%3A%2F%2Fmp.weixin.qq.com%2Fs%2Fz3hzILiPBsLJR72Q2tP7TQ), _missed in Dec issue_)
* Fundamental Analysis: Decred by Piotr Arendarski ([linkedin.com](https://www.linkedin.com/pulse/funadamental-analysis-decred-dcr-piotr-arendarski-ph-d))
* How to Last the Crypto Winter? Seek Simplicity, Manage Complexity by @jy-p ([coindesk.com](https://www.coindesk.com/how-to-last-the-crypto-winter-seek-simplicity-manage-complexity), tagline was collectively brainstormed in #marketing)
* Decred - an Interview with the Community Manager @donmario by Janusz Zielinski ([bithub.pl](https://bithub.pl/wywiady/decred-wywiad-z-community-managerem/))
* Best Decred Wallets: Top 6 Places to Store Your DCR by Steve Walters ([coinbureau.com](https://www.coinbureau.com/analysis/best-decred-wallets/), a nice case when authors were responsive and corrected all [reported issues](https://github.com/xaur/decred-issues/issues/68))
* Who Should Hold Power? Decred Governance and What It Means For Investors by Leslie Ankney ([forbes.com](https://www.forbes.com/sites/leslieankney/2019/01/11/who-should-hold-power-decred-governance-and-what-it-means-for-investors/))
* Decred Independent Contractor Roadmap for 2019 ([medium](https://medium.com/decred/decred-independent-contractor-roadmap-884faba3db39))
* The Unique Consensus Mechanism of Decred - Is This True Decentralization? by Paul de Havilland ([bitsonline](https://bitsonline.com/consensus-mechanism-of-decred-decentralization/))
* Decred as Store of Value by Yin Guochao, inspired by Forbes article (Chinese, [qq.com](https://mp.weixin.qq.com/s/_-lY0rtWSPiyLPZeTRR7gg), [translation](https://translate.google.com/translate?sl=auto&tl=en&hl=en&u=https%3A%2F%2Fmp.weixin.qq.com%2Fs%2F_-lY0rtWSPiyLPZeTRR7gg))
* Blockchain Project Review: Decred: 8.4 Autonomous Digital Currency by Evaluape ([medium](https://medium.com/@EVALUAPE1/blockchain-project-review-decred-8-4-autonomous-digital-currency-323771d65529), Decred rated 8.4/10)
* Decred coin review: Replacing BTC? by Edwin (Dutch, [bitcoinsaltcoins.nl](https://www.bitcoinsaltcoins.nl/decred-coin-review-vervanger-van-btc/), Decred scored 8.8/10)
* 3 Cryptocurrencies to HODL during This Crypto Winter (Opinion) by Daniel Frumkin ([investinblockchain.com](https://www.investinblockchain.com/cryptocurrencies-hodl-during-crypto-winter/))
* Fundamental Value in Crypto; Bitcoin and Decred as Store of Value Investments by LCC Investment Research ([seekingalpha.com](https://seekingalpha.com/article/4235521-fundamental-value-crypto-bitcoin-decred-store-value-investments))
* The role of Decred voters in defending against majority attacks by @richardred ([medium](https://medium.com/@richardred/the-role-of-decred-voters-in-defending-against-majority-attacks-ec658af0a8fd))
* Decentralized off-chain governance in the context of digital currencies by @Haon ([goodaudience.com](https://blog.goodaudience.com/decentralized-off-chain-governance-in-the-context-of-digital-currencies-ef6db7d97412))
* Decred Infrastructure Interviews: Stephen, founder of crypto-only luxury goods marketplace CryptoEmporium by @kozel ([medium](https://medium.com/@artikozel/decred-infrastructure-interviews-stephen-founder-of-crypto-only-luxury-goods-marketplace-68d3214a4fd7))
* Decred Review by Lee Banfield ([weeklyglobalresearch.wordpress.com](https://weeklyglobalresearch.wordpress.com/2019/01/31/decred-dcr-review/))

Translations:

* [Detailed analysis of Decred fork resistance](https://medium.com/decred/detailed-analysis-of-decred-fork-resistance-93022e0bcde7) by @Haon - [in Russian](https://medium.com/decred-russia/%D0%B4%D0%B5%D1%82%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7-%D1%83%D1%81%D1%82%D0%BE%D0%B9%D1%87%D0%B8%D0%B2%D0%BE%D1%81%D1%82%D0%B8-decred-%D0%BA-%D1%84%D0%BE%D1%80%D0%BA%D1%83-b30c78f764ea) by @DZ
* Decred Journal - December 2018 [in Chinese](https://www.jianshu.com/p/65e7a83ac27c) by @guang, [in Polish](https://github.com/artikozel/DecredJournalPL/blob/master/journal/201812_DecredJournalPL.md) by @kozel, [in Portuguese](https://medium.com/@maiconjunge/jornal-decred-dezembro-de-2018-947c616b894f) by @maiconjunge, [in Russian](https://medium.com/decred-russia/decred-journal-%D0%B4%D0%B5%D0%BA%D0%B0%D0%B1%D1%80%D1%8C-2018-9528f7a9d24d) by @DZ and [in Spanish](https://medium.com/@decred_es/revista-decred-diciembre-2018-79093f957aac) by @elian. Wow. Thank you all for spreading Decred Journal around the world! All translations are listed [here](https://xaur.github.io/decred-news/).

Videos:

* Applications of Blockchain Time-Stamping - talk by @jy-p at TNABC ([youtube](https://www.youtube.com/watch?v=3RRTidXh_Lw))
* Interviews at TNABC: [with @joshuam](https://www.youtube.com/watch?v=Kyihc6Uh4XA) by Hack Crypto, [with @joshuam](https://bitsonline.com/decred-disputes-inevitable-buirski/) by Bitsonline, [with @DZ](https://www.youtube.com/watch?v=h3bII-vjOsA), [with @jz](https://www.youtube.com/watch?v=4oKRVXGN6Fs) by CNBC Crypto Trader.
* Governance: Blockchain's Most Overlooked Pillar - talk by @oregonisaac at Token Forum 2 ([tfblock.io](https://www.tfblock.io/post/governance-blockchain-s-most-overlooked-pillar))

Audio:

* Taking a Deep Dive into Autonomous Cryptocurrency with Decred - @moo31337 and @BAB talk how decentralized decision-making and self-funding have enabled Decred to build a robust, evolving digital currency, free from third party influence (The Crypto Chick Podcast with Rachel Wolfson, [badcryptopodcast.com](https://badcryptopodcast.com/2019/01/08/autonomous-crypto-decred/))
* Noah Pierau on Blockchain Governance: Decred, Bitcoin, Dash, Ethereum (51percent Crypto Research by Tom Shaughnessy, [itunes](https://itunes.apple.com/us/podcast/noah-pierau-on-blockchain-governance-decred-bitcoin/id1438148082?i=1000428113722&mt=2))
* How Decred Revolutionizes Funding in Crypto with Marco Peereboom - Michael Nye and Marco discuss current state of crypto, how Decred began, PoW vs PoS, Decred's funding model and more (Evolvement Podcast, [evolvement.io](https://evolvement.io/how-decred-revolutionizes-funding-in-crypto-with-marco-peereboom/))

## 社区讨论

Community stats as of Feb 4:

* Twitter followers: 39,778 (-106)
* Reddit subscribers: 9,330 (+89)
* Matrix users: 247 (+26)
* Slack users: 6,529 (+110)
* Telegram users: 4,503 (-231)
* YouTube subscribers: 3,752 (+14)
* Facebook followers: 3,132 (+11), likes: 2,891 (+11)
* LinkedIn followers: Decred page 466 (+16), Politeia page 27 (+3)
* GitHub dcrd stars: 468 (+10), forks: 1,221 (+29)

Comm systems news:

* Slow Twitter [follower bleed](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$1549500437341uJIFK:decred.org) continues for unkown reasons. Any ideas are welcome.
* Drop in Telegram user count is likely due to a bot purge.
* @sambiohazard wrote a thorough [plan](https://github.com/xaur/decred-issues/issues/16) to address Discord spam, implemented it, and reported no spam after first few weeks. Several important channels were bridged with Discord. With this in place we can finally appreciate Discord as an opportunity to onboard more people. Thank you!
* [decred.org/matrix](https://decred.org/matrix/) guides new matrix users into the system.
* [decred-issues](https://github.com/xaur/decred-issues) grew to 105 issues as of Feb 9. Check it out, perhaps you'll find something interesting to do!

[Criticism](https://twitter.com/tonevays/status/1086702239853379584) from Bitcoin maximalists triggered a [discussion](https://www.reddit.com/r/decred/comments/ahuawl/decred_launch_security_laws/) on how Decred looks in context of securities laws. One vector critics use is that Decred's premine and airdrop was not fair and "hand selected". This is a misrepresentation of the (huge) manual effort to filter out airdrop cheaters, per [this discussion](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154810656412322VrQLg:decred.org) that also has many useful links describing Decred's launch. One interesting insight shared is that ~300K (35%) airdropped coins never moved. Another related [chat](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$15467943549316LjeYZ:decred.org) was about Twitter attacks claiming how Decred's initial distribution was not transparent or fair, while avoiding inconvenient facts about Bitcoin's early mining and Satoshi's million BTC. Finally, a [history lesson](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15467944729319gvTvt:decred.org) explained early days of staking and made a point that original devs had no unilateral control of consensus rules from day 1.

Huge debate about importance of building Reddit community [here](https://www.reddit.com/r/decred/comments/aib2x3/noah_pierau_on_blockchain_governance_decred/).

## 市场

In January DCR was trading between USD 15.5-19.5 / BTC 0.00435-0.00487. The average daily rate was 17.1美元。

## 相关外部信息

Ethereum Classic (ETC) was subject to a 51% attack, with the alert being raised by [CoinNess](https://www.coinness.com/news/198264) on Jan 7. Coinbase then [announced](https://blog.coinbase.com/ethereum-classic-etc-is-currently-being-51-attacked-33be13ce32de) that it had detected a deep reorganization of the ETC chain and had halted ETC transactions. The article lists a number of reorgs that involved double spends, putting the total amount involved at $1.1 million, across 15 distinct reorg events. Coinbase was not itself a target for these attacks. The Gate.io exchange subsequently [announced](https://www.gate.io/article/16735) that it had been targeted and had lost around $200K, and that it would absorb the loss. Gate.io also significantly increased the number of confirmations required for ETC deposits. In an unusual development, the attacker then [returned](https://www.gate.io/article/16740) $100K of the ETC to Gate.io, they have tried but failed to make contact with the attacker and do not know the reason for the return of funds. Other victims of the ETC double spends have not come forward.

Ethereum's developers [decided](https://www.coindesk.com/ethereum-developers-give-tentative-greenlight-to-asic-blocking-code) (tentatively) on Jan 4 to go ahead with a change of mining algorithm from Ethash to ProgPoW. This move is intended to stop ASICs from mining Ethereum. The Block [outlined](https://www.theblockcrypto.com/2019/01/11/despite-core-dev-consensus-proposition-progpow-faces-community-concerns/) concerns like reduced attack cost after the switch, weaker incentives of GPU miners, questionable benefit of transfer of power from Bitmain and Innosilicon to AMD and Nvidia, and a possible chain split. They concluded that the debate around the algorithm switch will be a good test for Ethereum's governance process.

Ethereum developers also [delayed](https://breakermag.com/what-we-know-about-the-vulnerability-behind-ethereums-rollback-of-constantinople/) the Constantinople hard fork on Jan 15 after a security vulnerability which would have enabled a "reentrancy attack" was [detected](https://medium.com/chainsecurity/constantinople-enables-new-reentrancy-attack-ace4088297d9).

Fundamentals of Proof of Work [article](https://blog.sia.tech/fundamentals-of-proof-of-work-beaa68093d2b) by David Vorick makes the case for exclusive hardware cryptocurrencies and contrasts them with shared hardware cryptocurrencies that suffer from multiple issues, especially those pursuing ASIC resistance. One of the issues with non specialized hardware is that the hardware's value is not closely related to the asset (because it can mine many other chains). Another issue is hashrate marketplaces, they allow hardware owners to get more profit by not caring about which coin they mine, even if the hashrate is rented to attackers. Decred benefits from specialized hardware and is by far the dominant coin for its algorithm (Blake256r14). Although this hardware cannot be considered "exclusive" to Decred, in addition to current hashrate dominance for its algorithm Decred has the PoS factor which is capable of denying rewards to misbehaving miners.

The first round of Aragon proposal voting [concluded](https://blog.aragon.org/final-results-from-aragon-network-vote-1/) on Jan 26. Of the 12 submitted proposals, 3 were excluded from the vote by the Aragon Foundation (1 because of lack of full time leadership and engineering talent, 2 were excluded to reduce cognitive load on voters). 8 of the 9 proposals voted on were [approved](https://mainnet.aragon.org/#/governance.aragonproject.eth/0x277bfcf7c2e162cb1ac3e9ae228a3132a75f83d4) by ANT holders, with one proposal (to change the voting period duration from 48 hours to 1 week) rejected. ANT participation rates [ranged](https://mainnet.aragon.org/#/governance.aragonproject.eth/0x277bfcf7c2e162cb1ac3e9ae228a3132a75f83d4) from 2.3 to 7.8%. The most expensive [proposal](https://github.com/aragon/flock/blob/master/teams/Aragon%20One/2019.md) to be approved will pay Aragon One $4 million for 2019 operating costs plus an incentive package consisting of 1.675 million ANT on a 5 year vesting schedule. An incentive in ANT with a vesting schedule was included as part of most proposals, in addition to the main cost to be paid in DAI. In total this round of approved proposals will cost around $5.94 million + 2.52 million ANT (~$880K).

The EOS referendum system for constitutional amendments went [live](https://medium.com/@eosnationbp/the-fate-of-eos-is-in-the-hands-of-token-holders-3d345147ef6) on Jan 11. So far 77 proposals have been [submitted](https://bloks.io/vote/referendums). The voting period for these proposals is flexible and specified by the submitter, some last as long as four months. The proposals with the most votes (as of Jan 31) have votes from around 2% of circulating EOS, but most proposals have very low participation (only 10 have greater than 0.5% participation). So far the most popular proposals are to [change](https://bloks.io/vote/referendums/rex4all) where the fees for short names and RAM purchases go, [delete](https://bloks.io/vote/referendums/decaf) the EOS Core Arbitration Forum, and [burn](https://bloks.io/vote/referendums/burnsaving) the inflation funds in eosio.saving (to be used for funding the worker proposal system).

The NEM Foundation [announced](https://forum.nem.io/t/nem-foundation-message-to-the-community/21753) that it is in financial difficulty and needs to downsize its workforce. A new council took over the foundation on Jan 1 and when they opened the books they saw a problem. The previous council had a burn rate of 9 million XEM per month ($360K now, considerably more at the time) which was spent by independent regional entities on promotional activities with little accountability. This was deemed not sustainable, and the new council has restructured the foundation and is presently seeking additional funds.

Updated version of the "forkonomy" research by Wassim Alsindi (@parallelind) was [published](https://hackernoon.com/towards-an-analytical-discipline-of-forkonomy-summer-2018-e6da993ee3f9) along with an up-to-date [follow-up](https://medium.com/@parallelind/forkonomy-revisited-where-are-they-now-73fbfbec6b4d).

Hcash forked a few [more](https://archive.today/rEhWX) Decred projects: [Autonomy](https://archive.today/KTCdX) (Politeia), [hcexplorer](https://archive.today/2KTtW) and [hctime](https://archive.today/K151A). In Politeia, they accidentally [removed](https://archive.today/ECplt) copyright of Decred developers and forgot to rename the project. After being notified they quickly reacted by removing multiple repositories, [reinstating](https://github.com/TKFORKED/autonomy/commit/4b05c2c31829df64be69e546d939a563247e1927) the license and [renaming](https://github.com/TKFORKED/autonomy/commit/98d5f63f676e45e6a91eba99da3db985effdb1f2) the Politeia fork to Autonomy. A few [missed](https://twitter.com/michae2xl/status/1084270468234915840) subtle Decred icons were fixed. Some [projects](https://archive.today/https://github.com/HcashOrg/hc*) were forked with their commit history erased and without marking them as forks on GitHub. Complaints ([1](https://www.reddit.com/r/hcash/comments/adwmx2/hcash_being_shady_again/), [2](https://www.reddit.com/r/hcash/comments/afepsc/hcash_cant_be_bothered_to_change_the_decred_logo/)) on their subreddit were silently [censored](https://archive.today/Edy7T) with no reply. Oh, and [r/hcash](https://archive.today/Edy7T) styles look [familiar](https://archive.today/e1rAw). Discussed [here](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$154696507010921TRgid:decred.org).

A [sad example](https://twitter.com/BrianDColwell/status/1090286752831434752) of what can happen when the team runs out of money.

ICO projects [withdrew](https://diar.co/ethereum-ico-treasury-balances/) ~441K ETH ($52.5M as of Feb 9) from treasuries in December 2018.

[Staked](https://staked.us/about/), a startup that provides staking services for institutional investors, raised $4.5M from Pantera, Coinbase, DCG and others. Covered by [CoinDesk](https://www.coindesk.com/pantera-coinbase-join-4-5-million-round-in-staking-as-a-service-startup), [The Block](https://www.theblockcrypto.com/2019/01/31/winklevoss-twins-pantera-get-behind-a-new-business-thats-capitalizing-on-a-new-trend-sweeping-crypto-hedge-funds/) and [Bloomberg](https://www.bloomberg.com/news/articles/2019-02-01/some-crypto-investors-are-playing-it-safe-after-volatile-run). Staked operates a Decred [VSP](https://decred.staked.us/) since Nov 2018.

Binance now [allows](https://support.binance.com/hc/en-us/articles/360022498052) one to buy crypto with Visa and MasterCard (and the list of [restrictions](https://support.binance.com/hc/en-us/articles/360022204152) tells us something about fiat).

Coinbase [banned](https://cryptocoinspy.com/coinbase-bans-gab-again/) accounts of social media platform Gab. This is [not the first](https://www.cnbc.com/2018/04/23/coinbase-suspends-wikileaks-bitcoin-account.html) big case of account suspension by the exchange.

Medium [censored](https://bitcoinist.com/how-to-use-bitcoin-anonymously-ban-medium/) an article "How to use Bitcoin anonymously" which spurred discussion and an [issue](https://github.com/xaur/decred-issues/issues/70) about migrating away from it, or at least treating it as one of multiple content mirrors. Backup your Medium posts, just in case.

Bank for International Settlements released a very optimistic [study](https://www.bis.org/publ/work765.htm) of cryptocurrencies.

[Vulnerability](https://cryptoslate.com/researchers-discover-vulnerability-bitcoin-ethereum-ripple-digital-signatures/) was discovered in digital signatures of Bitcoin and a few other systems. A tiny set of signatures was generated using an incorrect implementation of signature algorithm which can be used to reveal private keys. Only a few thousand signatures were vulnerable out of nearly a billion Bitcoin signatures examined. According to researchers, the vast majority of cryptocurrency users need not worry.

Largest [data breach](https://www.troyhunt.com/the-773-million-record-collection-1-data-reach/) in history contains a collection of thousands of hacked databases. Choose wisely who you share data with.

Cryptopia was [hacked](https://www.investinblockchain.com/cryptopia-hack-estimated-16-million-lost/) with loss estimates varying between $3-16 million. Binance [froze](https://www.investinblockchain.com/binance-freezes-funds-cryptopia-hack/) some funds coming from the hack.

New wave of hAnt infections (first seen in August) was [reported](https://www.zdnet.com/article/new-ransomware-strain-is-locking-up-bitcoin-mining-rigs-in-china/) targeting Bitcoin mining rigs. The ransomware demands to infect 1,000 other devices or pay 10 BTC, else it threatens to burn the rig. There have been no reports of destroyed equipment so far.

Resource exhaustion vulnerability known as Fake Stake attack was [discovered](https://medium.com/@dsl_uiuc/fake-stake-attacks-on-chain-based-proof-of-stake-cryptocurrencies-b8b05723f806) in 26+ blockchains based on PoSv3, the majority of them deployed mitigations. Part of the root cause is that in many such systems the Proof of Stake layer was "grafted in" to the Bitcoin Core codebase insecurely. One of report's authors tweeted that Decred is [not affected](https://twitter.com/Sanket1729/status/1087829688347701254).


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
