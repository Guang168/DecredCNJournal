# Decred月报 - 2019年5月

![abstract art](img/journal-201906-384.jpg "Blue Dragon by @saender. Dragon resembles power/fear/terror/chaos. Blue dragon is calm and intelligent, but nevertheless powerful. It resembles a balance of power and wisdom.")

六月重点:

* Politeia for Ditto（PR）批准的预算，错误赏金计划，开源研究，分散交换规范和块头承诺共识变更将提升SPV安全性并为其他改进铺平道路。

* iOS Wallet v1.0于7月10日在App Store上发布。

* dcrdata v5.0发布。用于探索Decred数据，性能，安全性和体系结构改进的新图表和数据可视化。

* 承包商在承包商管理系统（CMS）中提交错误修复和UI改进的发票的更顺畅的经验 - 这是推出DCC和财务报告的重要里程碑。

* 这个月出现了一些高调的播客出现以及文章和社交媒体上的Decred提及。#DecredChallenge正在获得一些牵引力，并鼓励人们研究Decred，了解它，并讨论它是否应该在加密货币领域更加突出。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 代码维护和更多测试覆盖。

升级了几个模块以提高组织和代码质量。[引入](https://github.com/decred/dcrd/pull/1767) dcrutil模块的第2版以减少耦合并防止处理地址中的细微错误。引入v2 模块[完成](https://github.com/decred/dcrd/pull/1698)的大改动。这样做的好处包括：通过将块1支付定义为脚本而不是地址来减少关键共识代码的表面，在导入包时消除不希望的副作用并改善网络参数的组织。该模块的第2版还 [引入](https://github.com/decred/dcrd/pull/1774)了使用新版本和模块。版本碰撞的机会也用于解决v1中的几个问题

[五月问题](201905.md)中涵盖的背景模板生成器的大修已[合并](https://github.com/decred/dcrd/pull/1748).。

这些大型代码升级非常谨慎。首先，引入了一个新的模块版本，然后逐步更新依赖模块以使用新版本。在任何时候，一切都必须构建并通过所有测试，每个提交必须最大限度地审查。

在其他较小的改进中，[增加了](https://github.com/decred/dcrd/pull/1757)对在Go 1.13上生成Ed25519 TLS证书的支持。

[dcrwallet](https://github.com/decred/dcrwallet): 错误修复和增量改进。

默认[TLS曲线](https://github.com/decred/dcrwallet/pull/1468)更改为更安全的P-256。默认情况下，在Go 1.13上添加并启用了对[Ed25519](https://github.com/decred/dcrwallet/pull/1477) TLS证书的支持。

通过增加[`ticketbuyer.limit`](https://github.com/decred/dcrwallet/pull/1476)标志来改善票务处理，以限制每个区块购买的最大票数和更正的lockedbytickets [余额计算](https://github.com/decred/dcrwallet/pull/1330)，以解决独立，VSP和分票票选民的几个问题。一个[RPC补丁](https://github.com/decred/dcrwallet/pull/1478)将允许VSP的显示[不成熟的选票](https://github.com/decred/dcrstakepool/pull/404)分开。添加了几个新的[钱包地址API](https://github.com/decred/dcrwallet/pull/1474)，以简化与地址相关的功能的开发。

[正在进行](https://github.com/decred/dcrwallet/pull/1471)工作以允许任意xpub帐户导入。此功能将允许自动票务购买者派生唯一的投票地址，从而避免地址重用，从而提高[匿名](https://github.com/decredcommunity/issues/issues/25)性。


[Decrediton](https://github.com/decred/decrediton): 继续开展[闪电网络钱包](https://github.com/decred/decrediton/pull/2107)的集成工作。处理[配置](https://github.com/decred/decrediton/pull/2129)，错误修复和维护的内部改进。

PoC正在使用有限[状态机](https://github.com/decred/decrediton/pull/2130)来更好地管理复杂性并提高启动期间的正确性。

[Politeia](https://github.com/decred/politeia): Politeia用户数据库中添加了一个 [插件](https://github.com/decred/politeia/pull/929)结构，可以更轻松地在Politeia的Web服务器（politeiawww）之上构建通用应用程序。这将允许应用程序更轻松地存储特定于应用程序的用户数据（例如来自承包商管理系统（CMS）的数据），同时仍然可以重新使用主用户路由。还创建了一个通用的dcrdata websocket [实现](https://github.com/decred/politeia/pull/933)，使得在politeiawww上构建的应用程序更容易监视地址平衡和其他区块链数据。
 
与CMS相关的一些增量改进和错误修复，这是一个运行politeiawww的应用程序，它重用了Politeia的大部分前端。提交发票过程中的摩擦力显着降低。自5月初以来，CMS一直在生产加工承包商发票。

完整的Politeia重新设计，以清理用户界面并使其与Decred品牌保持一致[正在进行中](https://twitter.com/lukebp_/status/1147528570581000193)，应在一个月左右的时间内启动。

五月份确定并修复了重复投票的[问题](https://github.com/decred/politeia/issues/882)，但在5月份的期刊中却没有。由于在重新检查缓存之前添加了并发投票的错误，如果在内存缓存中检查了传入投票的错误，因此在权力下放财政支出提案中的15个重复投票进入了Politeia期刊存储库。一旦提交了第一个重复投票，就会发现该错误并立即[修复](https://github.com/decred/politeia/pull/893)。

在[同时](https://github.com/decred/politeia/issues/665)运行多个Politeia实例方面取得了进展，使[电子邮件可选](https://github.com/decred/politeia/issues/860)并公开[报告](https://github.com/decred/politeia/pull/921)费用。

[dcrstakepool](https://github.com/decred/dcrstakepool): 最近几个月，VSP软件越来越[受欢迎](https://github.com/decred/dcrstakepool/pull/339)。在五月[重新设计](https://github.com/decred/dcrstakepool/issues/227)之后，有很多重构工作要在组件之间实现适当的层分离，这对于安全性和性能也会有很小的好处。


[dcrlnd](https://github.com/decred/dcrlnd): 工作继续从[lnd](https://github.com/lightningnetwork/lnd)存储库移植[上游更改](https://github.com/decred/dcrlnd/pull/36)。现在已经合并了大约190个（270个）PR合并到lnd，因为dcrlnd已经合并，包括许多错误修复和两个重要功能：安全备份用于脱链数据和了望塔客户端的违规保护和报复。

在回答关于LN的BTC-DCR交换的问题时，@ matheusd [澄清了](https://www.reddit.com/r/decred/comments/c17xxh/is_it_possible_to_exchange_btclightning_for/ere1skv/)这个难题的多个元素的状态。

[dcrandroid](https://github.com/decred/dcrandroid): 小错误修复和UI改进，[西班牙语](https://github.com/decred/dcrandroid/pull/363)和[葡萄牙语（BR）](https://github.com/decred/dcrandroid/pull/367)的新翻译，以及新的发送和估计[功能](https://github.com/decred/dcrandroid/pull/371)。

[dcrios](https://github.com/raedahgroup/dcrios): v1.0.0 在6个月的活跃工作后在[App Store](https://apps.apple.com/us/app/decred-wallet/id1462247643)上[发布](https://www.reddit.com/r/decred/comments/cbjqff/decred_wallet_for_ios_v100_on_the_app_store/)！

初始版本有英文，俄文和简体中文版本，有更多翻译版本。[Release Candidate 1](https://www.reddit.com/r/decred/comments/bxje6l/decred_wallet_for_ios_release_client_1/)和[Release Candidate 2](https://www.reddit.com/r/decred/comments/c7ir8d/decred_wallet_for_ios_release_client_2/)中报告的错误已经修复，并且已经实施了一些小的UI调整。

恭喜dcrios团队：macsleven，itswisdomagain，collins，ensoreus，rktr09（开发人员），DZ（设计）和所有测试人员。

[dcrdata](https://github.com/decred/dcrdata): 正式版本，v5.0现已上线。除了体系结构，安全性和性能改进之外，v5.0还引入了许多用于探索Decred数据的新图表和可视化。

新的[市场](https://explorer.dcrdata.org/market?chart=depth&xc=aggregated&bin=1h&stack=1)页面显示来自几个主要交易所的数据，包括汇总的DCR价格信息，交易深度等。该[建议](https://explorer.dcrdata.org/proposals) 页已完成测试，并显示所有Politeia建议统计和投票图表（实时和历史）。[错过的选票](https://explorer.dcrdata.org/charts?chart=missed-votes)图表显示了一个重要的网络健康指标。

架构改进包括升级到[PostgreSQL](https://github.com/decred/dcrdata/commit/676e2ae2381e900854c2fe664a92d39a122d6ed7)（精简模式已被删除），改进的数据库模式版本控制，dcrd通知通道的[重构](https://github.com/decred/dcrdata/commit/856d0466c82338dd1aaec2945ab189da3c4ab060)，[CockroachDB](https://github.com/decred/dcrdata/commit/3ddc034e672c84313fae789c558ead139ad39f8a)的实验支持，默认的[区块预取](https://github.com/decred/dcrdata/commit/5ceb56b5c8e1ed53b6b92b5deee6e2a05903f61f)，以及带地址订阅的新pubsub模块版本。

图表还应该通过性能改进加快速度，包括[改进的](https://github.com/decred/dcrdata/commit/5eb60c4633d128ab64783b75b851a012ed8024fa)内存管理和新的预编码图表缓存系统。

有关更改的完整列表，请参阅[发行说明](https://github.com/decred/dcrdata/releases/tag/release-v5.0.0)。

[docs](https://github.com/decred/dcrdocs): “DAE”（分布式自治实体）的实例已[修改为](https://github.com/decred/dcrdocs/pull/958) “DAO”（分布式自治组织）取代。新页面添加了有关[算法](https://github.com/decred/dcrdocs/pull/963)如何伪随机选择投票作品的详细信息。

其他:

* 现在，如果GitHub / AWS无法访问，则会在IPFS上镜像Decred二进制文件。如果您运行IPFS节点，请随意固定哈希以增加冗余并提高下载性能。还列出了3个HTTP网关，因此不使用IPFS的人也可以访问这些文件。最新的IPFS哈希值将始终列在此处：[dcr.jz.bz](https://dcr.jz.bz/).
* 还可以在Keybase上镜像Decred[二进制文件](https://keybase.pub/jz_bz/decred/dcr-binaries/)和[视频](https://keybase.pub/jz_bz/decred/dcr-videos/)。
* 源代码在 [GitLab](https://gitlab.com/dcr-bak)上镜像。
* [dcr-setup](https://github.com/jzbz/dcr-setup): 基于Debian和RedHat的Linux发行版的投票钱包设置脚本。

6月的开发活动统计数据：28个活动PR，321个主要提交，62K添加和29K删除的行分布在15个存储库中。贡献来自每个存储库1-8个开发人员。

## 人员

欢迎来到新的第一次贡献者与代码合并到掌握：Marton([politeia](https://github.com/decred/politeia/commits?author=martonp)),，Amos Ezeme([dcrandroid](https://github.com/decred/dcrandroid/commits?author=crux25))，Quadri Anifowose ([dcrandroid](https://github.com/decred/dcrandroid/commits?author=Quadriyanney))，Lore([dcrandroid](https://github.com/decred/dcrandroid/commits?author=hanelore))。

虽然@DZ在[dcrandroid](ttps://github.com/decred/dcrandroid/commits?author=denyszayets) 中合并的提交被第一次检测到，但应该注意到他是一个长期的Decred贡献者。

## 治理

6月，[社区基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到15,135 DCR，并花费6,657 DCR。使用6月份的每日平均DCR / USD为28.90美元，这是收到的437,000美元和花费的192,000美元。由于这些付款用于5月份完成的工作，因此在5月平均每日费率27.71美元的背景下考虑它们也是有用的 - 在这种情况下，美元收到/支出的数字是419,000美元/ 184K美元。截至7月1日，财政部余额为622,472 DCR（1836万美元，29.50美元）。

以下是截至7月1日的提案状态。

以下提案获得批准：

* [Decred Bug Bounty Proposal: Phase 2](https://proposals.decred.org/proposals/073694ed82d34b2bfff51e35220e8052ad4060899b23bc25791a9383375cae70)- 93.5％的批准，31.5％的选民参与
* [Ditto Communications Proposal for Decred: Phase 2](https://proposals.decred.org/proposals/52ea110ea061c72d3b31ed2f5635720b212ce5e3eaddf868d60f53a3d18b8c04) - 75.8％的批准，29.2％的选民参与
* [Decred开源研究提案：第2阶段](https://proposals.decred.org/proposals/67de0e901143400ae2f247391c4d5028719ffea8308fbc5854745ad859fb993f) - 90.2％的批准，32.4％的选民参与
* [去中心化交易工具规范](https://proposals.decred.org/proposals/a4f2a91c8589b2e5a955798d6c0f4f77f2eec13b62063c5f4102c21913dcaf32) - 98.4％的批准，30％的选民参与
* [Block Header Commitments Consensus Change](https://proposals.decred.org/proposals/0a1ff846ec271184ea4e3a921a3ccd8d478f69948b984445ee1852f272d54c58) - 99.2％的批准，33.5％的选民参与。提案和[Reddit](https://www.reddit.com/r/decred/comments/buv18c/block_header_commitments_consensus_change_proposal/)上的评论者对该提案如何为技术和非技术受众提供部分表示赞赏，并且还注意到Decred的链式投票系统如何在没有多年毫无结果的讨论的情况下实现优雅的更新。

发布了2个新提案：

* [Supplemental Proposal For Decred Tutorials By Denni Lovejoy](https://proposals.decred.org/proposals/d8d7ff7ad138ed322422aaa4d2a3e1c61f296ae56a2c2316cc5ecd10cf8dd8bd). 该提案要求将教程视频的原始预算750美元增加到7,500美元。@Denni Lovejoy要求在反对意见后放弃该提案。目前正在讨论如何处理这些方案，其中提案的工作量大大超出预算。

* [Decred Media Campaign Proposal - Crypto Economy - 2019/2020](https://proposals.decred.org/proposals/1a367dcb91b55c60ad5fd038b219201154fcab965edd7a4639f157e409b1f4bf). 该提案要求33,600美元以多种方式宣传Decred，包括横幅广告，新闻稿，Decred赠品和时事通讯。评论说，其中一些已经得到很好的覆盖，而另一些则不可取。该提案随后被其所有者放弃。

该[图](https://twitter.com/RichardRed0x/status/1139860218010058753)显示了Politeia选民参与迄今已完成投票的28项提案。

如需更深入地了解Politeia上发生的[事情](https://medium.com/politeia-digest/issue-18-june-10-june-29-97d140569ad0)，请查看6月发表的[两期](https://medium.com/politeia-digest/issue-17-may-28-june-9-bc5bb77e4f6c) “Politeia Digest”。

以下[问题](https://www.reddit.com/r/decred/comments/bx00fu/so_about_the_exmo_exchange/)在Reddit上，Exmo发布了简短的[更新](https://twitter.com/Exmo_Com/status/1138020825137930240)，并接着[列出](https://exmo.com/en/news_view?id=2776)DCR于6月18日。

r / decred subreddit上的一些帖子试图在Decred社区中对[最佳Politeia批准门槛](https://www.reddit.com/r/decred/comments/bynidz/poll_optimal_politeia_pass_threshold/)进行投票，[将Decrediton重命名为Declaration](https://www.reddit.com/r/decred/comments/c4ilpw/poll_rename_decrediton_to_declaration/)，[将Decrediton称为钱包以外的其他内容](https://www.reddit.com/r/decred/comments/c52hqd/question_is_a_hybrid_finance_governance_tool/)，并询问Decred是否应该开始[使用DAO而不是DAE](https://www.reddit.com/r/decred/comments/c02geh/poll_rename_dae_to_dao/)来描述分散的利益相关者对项目的治理。

最后一次轮询（将DAE重命名为DAO）可以被@s_ben视为“软提议”。这个提案背后的理由是，虽然最初选择DAE（分布式自治实体）这个名称是为了避免与以太坊[DAO黑客](https://www.google.com/search?q=ethereum+dao+hack)的关联，但DAO从此成为加密中的热门话题，与DAO hack在流行的想象中几乎没有联系。 。因为Decred在这个术语上可以说比其他项目更合理，因为已经建立了一个正常运行的DAO（正在制作这个时事通讯），所以参与对话更有意义。考虑了一项Politeia提案。但是，对于各种通信渠道的变化没有异议（如本[评论中](https://www.reddit.com/r/decred/comments/c02geh/poll_rename_dae_to_dao/er1g4px)所述）），粗略的共识是，除非有任何强烈反对，否则这种改变不需要Politeia提案。@s_ben更改了[文档](https://docs.decred.org/governance/politeia/overview/#decentralized-autonomous-organization-dao)的引用，并提交了一个[pull请求](https://github.com/decred/dcrweb/pull/681)来更改decred.org上的术语。活动而这一举措的讨论在跟踪[这个问题](https://github.com/decredcommunity/issues/issues/134).。

虽然其中一些民意调查及其周围的讨论很有意思，但社区成员已经注意到使用Reddit和民意调查网站来衡量Decred利益相关者的意见存在问题。这些平台向非利益相关者开放，允许他们的创建者任意删除或修改民意调查/帖子。在讨论这种现象的过程中，基于Politeia的[Decred版本的Reddit](https://github.com/decredcommunity/issues/issues/38)似乎得到了强有力的支持，这将允许创建有限数量的票证选民民意调查。

## 网络

网络算力：6月份的哈希值以~504 Ph / s的速度开启，月底约为540 Ph / s，最低369 Ph / s，整个月达到607 Ph / s。截至7月2日的池哈希值分布：lab.antpool.com 18％，UUPool 17.7％，F2Pool 14％，Poolin 9.5％，BTC.com 9％，Luxor 2.2％，CoinMine 0.21％，BeePool 0.15％，suprnova 0.03％和其他人每个[dcrstats.com](https://dcrstats.com/pow)29％。池分布数是近似值，无法准确确定。


Staking: 每个dcrstats.com的30天平均票价为120 DCR（+4）。价格在116.8-127.3 DCR之间变化。锁定金额为4.75-484万DCR，相当于可用供应量的[48.01-49.03%](https://charts.dcr.farm/d/000000003/proof-of-stake?orgId=1&from=1559347200000&to=1561939200000) 。

节点数: 整个6月，每个 [dcr.farm](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1559347200000&to=1561939200000)大约有200个监听节点和340-510个总节点。截至7月8日，大约80％运行v1.4.0,9％运行dcrwallet v1.4.0（SPV）和4％运行v1.5.0（pre）dev版本。

dcr.farm更新了[闪电网络](https://charts.dcr.farm/d/DHPdAO4Wz/lightning-network?orgId=1)仪表板。截至7月8日，DCR testnet LN显示15个节点，45个通道，总容量为370 DCR。

6月27日，DCR供应量[超过](https://twitter.com/raedahgroup/status/1144655370234880000) 10,000,000 DCR。1000万DCR分布意味着起源[预设](https://docs.decred.org/advanced/premine/)占当前流通DCR的17％，到目前为止，PoW矿工获得50％，PoS选民获得25％，财政部获得8％。

选票持有人提出支持请求说某些VSP[错过了](https://www.reddit.com/r/decred/comments/c862ee/assistance_needed_missed_tickets/)他们的门票。经过调查，发现Grassfed和d1pool已从网络中分离出来并且错过了对他们的门票的投票。 [Grassfed](https://dcr.grassfed.network/)做出了回应并承诺将继续保持未来的更新。我们无法访问[d1pool](https://d1pool.com) ，目前正在讨论将它们从decred.org 的[VSP列表](https://decred.org/vsp/)中删除。

同时也出现了一个[问题](https://github.com/decred/dcrstakepool/issues/413和[话题](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$156207152510654HMiFp:decred.org如何将这些问题能在未来避免。另一个讨论的想法是持续努力让更多人建立自己的[投票钱包](https://matrix.to/#/!dhHYPTtCtvPSUfTepT:decred.org/$156207972910815kERGq:decred.org)。

## 整合

Exmo在他们的 [提案l](https://proposals.decred.org/proposals/950e8149e594b01c010c1199233ab11e82c9da39174ba375d286dc72bb0a54d7)上发布，并在6月18日[启用](https://exmo.com/en/news_view?id=2776)了 DCR / BTC，DCR / RUB和DCR / UAH交易对。

Vertbase 为美国客户增加了[定期订单](https://twitter.com/vertbase/status/1141826092564701184)和[出售](https://twitter.com/vertbase/status/1141735926059716611)美元数字资产的选项。

EliteX [列出](https://twitter.com/elitexcrypto/status/1143044131800977409)了 DCR，并写了[一篇文章](https://medium.com/@elitexexchange/the-lowdown-on-decred-dcr-2a36520079f5)向他们的用户解释Decred。

抹茶交易所（MXC Exchange）[添加](https://twitter.com/wanbihou/status/1143846271645437952)了DCR / USDT交换对。

Bleutrade [宣布](https://bleutrade.com/announcements/) DCR将在7月15日计划的大规模清理中被除名 - 今年第二次退市 ([讨论](https://www.reddit.com/r/decred/comments/c86a75/bleutrade_will_delist_dcr_20190715_1500_utc/))。Bleutrade非常[支持](https://twitter.com/BLEUTRADE/status/999683568791060481)Decred。这是第一个列出Decred的产品，它是在[2016年2月8日](https://bitcointalk.org/index.php?topic=1290358.1640)网络启动的第一天就是这样做的。

Decred的Trust Wallet集成部分 [即将完成](https://github.com/trezor/blockbook/pull/216)。在三月份获得选民批准后，该[提案](https://proposals.decred.org/proposals/2ababdea7da2b3d8312a773d477272135a883ed772ba99cdf31eddb5f261d571)在负责核心钱包集成（完成）的Trust Wallet团队与负责整合和托管Trust Wallet用于托管交易数据的Blockbook服务器之间分离工作。

注意：Decred Journal的作者不知道上述任何服务的可信度。在将您的个人信息或资产信任给任何实体之前，请先进行自己的研究。

## 外联活动

在外展方面继续取得进展，重点关注教育并使其更容易学习Decred。正在进行具体工作以建立社交媒体剧本，使每个社区成员都能做出贡献。[Checkmate](https://twitter.com/_Checkmatey_) 已经在Twitter上出现，引入了[#DecredChallenge](https://twitter.com/hashtag/DecredChallenge)标签，并[挑战](https://twitter.com/_Checkmatey_/status/1145764832362319872)每个人学习Decred 30天，并解释为什么Decred不应该是市值的＃2。结果非常积极，Decred社交媒体活动和效果显着提升。喜欢和评论Decred故事非常重要，因为这样可以增加覆盖范围，并可以编写更多故事。

在教育的基础上，网站工作即将投入生产，新的介绍性视频和关于安全，适应性，自筹资金，历史和教育的一般存储库的新子页面。这项工作将有助于更容易理解Decred，从而帮助支持社区发展。

@anshawblack在@lukebp和Joel Monegro发行了Decred in Depth播客剧集。@Dustorf和@jy-p录制了Decred Assembly剧集，包括Decred Distributed with @akinsawyerr在Decred in Africa，Deep Dive with @ moo31337 on the Treasury proposal，以及Decred Distributed with @richardred。后两集将很快发布。

世界各地正在计划各种活动，包括德国，日本，中国和多伦多。该项目为2019年欧洲和亚洲的重大活动提供资金，尚未作出具体承诺。如果您有具体想法，请分享#event_planning。我们依靠世界各地的社区来帮助识别和执行机会。

Decred在治理问题上取得了重大进展。CoinDesk中的赌注是by Decred治理宣言的前身，而@akinsawyerr 在沃顿商学院治理会议上与该领域的主要发言人一起[发表了讲话](https://github.com/decredcommunity/events/blob/master/reports/20190701-wharton-governance-workshop-san-francisco-usa.md)。有很多关于Decred的讨论，它作为治理的先驱和领导者而受到广泛尊重。已邀请Decred在日本的下一次此类会议上发言。

Ditto六月成就:

* 促进了对@jy-p和CoinDesk之间治理和赌注的介绍性访谈
* 促进了对Legacy Research分析师Greg Wilson和@ moo31337的采访，他们对Decred进行了概述和更新，面向投资者
* 与Morgan Creek Digital的创始人Anthony Pompliano和@ jy-p一起安全并配备[Off the Chain](https://podcasts.apple.com/us/podcast/jake-yocom-piatt-project-lead-for-decred-crypto-ego/id1434060078?i=1000441486954)播客
* 使用Delphi Digital的Tom Shaughnessy和@ jy-p获得安全和人员配备的 [Chain Reaction](https://www.youtube.com/watch?v=kO_11gehyls)播客
* Got Decred引用了[CNBC](https://www.cnbc.com/2019/06/18/facebooks-libra-will-give-billions-access-to-cryptocurrency.html)，[Mashable](https://mashable.com/article/facebook-libra-experts/)，[CoinTelegraph](https://cointelegraph.com/news/what-is-libra-breaking-down-facebooks-new-digital-currency)和[Forbes](https://www.forbes.com/sites/kenrapoza/2019/06/20/facebooks-libra-coin-is-both-vampire-project-and-regulatory-nightmare/)的 Facebook Libra （[两次](https://www.forbes.com/sites/rachelwolfson/2019/06/19/facebooks-cryptocurrency-libra-validates-blockchain-but-industry-experts-voice-concerns/)!）。旁注：CNBC和Mashable是主流媒体，吸引那些对加密知之甚少的人。通过在他们面前获得Decred，我们正在大大扩展其覆盖范围
* @jy-p[引用](https://www.coindesk.com/how-blockchain-voting-is-supposed-to-work-but-in-practice-rarely-does)CoinDesk中的治理。
* @richardred 在CoinTelegraph上 [引用](https://cointelegraph.com/news/internet-authority-history-of-centralized-companies-being-hostile-toward-crypto) 了关于CCN“关闭”的文章。
* 参加旧金山比特币聚会，组织者表示有兴趣组建一个以Decred为发言人的治理小组
* 制作了关于如何对地理围栏或退市做出反应（或不做出反应）的社交媒体[指南](https://github.com/decredcommunity/pr/blob/release/engagement-guide-delist.md)
* 召集社区参与并在社交媒体上分享媒体报道
* 提交的[Ditto提案：第2阶段](https://proposals.decred.org/proposals/52ea110ea061c72d3b31ed2f5635720b212ce5e3eaddf868d60f53a3d18b8c04)到Politeia，参与讨论，然后看到Decred利益相关方批准的提案！感谢您的信任投票。在Decred工作是一种绝对的快乐，我们期待未来6个月

社区活动:

* 6月5日 - [Decred x Blueyard](https://www.eventbrite.co.uk/e/decred-x-blueyard-berlin-meetup-tickets-61631192556)d - 德国柏林。@Haon的完整报告就在[这里](https://github.com/decredcommunity/events/blob/master/reports/20190605-decred-x-blueyard-berlin-germany.md)
* 6月11日 - 区块链的裁定和工业用途 - 玻利维亚拉巴斯。@elian与圣安德烈斯大学的50-60名工程专业学生进行了交流。([照片](https://twitter.com/Decred_ES/status/1138899455346954240))
* 6月12日 - [Decred：一个分散的自治实体](https://www.meetup.com/Decred-Washington-DC-Meetup-Group/events/261144707/) - 美国华盛顿特区。该活动共有约11人参加。@akinsawyerr对Decred进行了概述，并回答了观众的提问。该活动由TechSpace Balston和Dartmouth Entrepreneurial Network of DC共同主办。有很多问题涉及我们的治理流程，我们如何支付和管理承包商，以及Decred与参与/贡献角度的以太网等平台的不同之处。
* 6月13日 - [加密会议](https://twitter.com/Decred_ES/status/1138908828370706432) - 玻利维亚拉巴斯。@elian向当地的加密社区发表了关于区块链治理的演讲。([照片](https://twitter.com/gamelendrez/status/1139325915475959808))
* 6月18日 - [TF Blockchain](https://www.eventbrite.com/e/tf-blockchain-portland-ep-03-june-18th-2019-tickets-61667348700) - 美国波特兰。
* 6月18日 - [NetEase](https://twitter.com/wanbihou/status/1142243367905943552) - 中国武汉。@Dominic介绍了Decred独特的融资模式和DCRDAO组织模式。（照片）
* 6月19日 - [Reston Virginia Golang](https://www.meetup.com/Golang-Reston/events/sfsjmpyzjbzb/)聚会 - 美国弗吉尼亚州雷斯顿。该活动有21人参加，主要是开发人员。@akinsawyerr对Decred进行了概述，并回答了观众的提问。该活动由康卡斯特主持。大多数问题都是关于如何获取加密货币，理解基本术语以及加密货币的潜在经济影响的一般性问题。发布一个参与者要求了解更多关于Decred利用Golang构建的内容的活动，希望看到实际的代码演示等。
* 6月19日至23日- 巴西利亚[校区派对](https://brasil.campus-party.org/) - 巴西巴西利亚。Decred[出席了](https://twitter.com/Decred_BR/status/1141782527637688322)大学聚会。@matheusd 在聊天中写了一份[报告](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156172492478087gSMWo:matrix.org)，描述了一个成功的活动，其中Decred有强大的存在并参与了3个不同的活动（加密儿童游戏时间，LN付费墙研讨会和参与主舞台）。([视频](https://www.youtube.com/watch?v=w792TaZTxgA))
* 6月20日 - [北京Decred Meetup](https://twitter.com/DecredCN/status/1138739545594220544) - 中国北京。Decred由@changhugo和@Dominic代表。该活动有100人参加，现场直播超过4,000名观众。@changhugo的完整报告在[这里](https://github.com/decredcommunity/events/blob/master/reports/20190620-first-meetup-beijing-china.md)。
* 6月26日 - [SF Decred Devs x Coinbase Custody Happy Hour](https://www.meetup.com/San-Francisco-Decred-Meetup/events/262420787/) - 美国旧金山。([照片](https://twitter.com/CryptoLeslie/status/1144092778017648641))
* 6月28日 - [Community Update on all things Decred](https://www.meetup.com/Decred-Australia/events/262550167/) - 澳大利亚墨尔本。

即将到来的:

* 7月11日 - [与Joshua Buirski - 美国纽约的炉边聊天](https://www.eventbrite.com/e/fireside-chat-with-joshua-buirski-decred-asia-pacific-lead-tickets-64832494737)。由Staked和TokenTax共同主持。
* 7月24日 - Decred Meetup - 美国芝加哥。

经过改进的活动报告库现在有14个[不错的报告](https://github.com/decredcommunity/events)。请提交您的报告并在Reddit / Twitter上分享，以了解每个月发生的事件数量。

## 媒体

Ditto的公关指南已收集在新的[存储库中](https://github.com/decredcommunity/pr)，目前包括[基础消息传递](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md), [选票消息传递](https://github.com/decredcommunity/pr/blob/release/ticket-messaging.md) and [参与指南](https://github.com/decredcommunity/pr/blob/release/engagement-guide-delist.md)如何对退市/地理围栏做出反应。

为任何不适合decred.org或文档的知识启动了一个新的[社区wiki](https://github.com/decredcommunity/wiki)存储库。第一个创建的页面是Decred[社交媒体](https://github.com/decredcommunity/wiki/blob/master/wiki/social-media.md)组的综合列表。

精选文章:

* The Blockchain Governance Quadrant by @Haon ([medium](https://medium.com/@NoahPierau/the-blockchain-governance-quadrant-2a878a9cacb9))
* The Regulators Are Coming - Canary in the Decred Hash Mine: Part I by u/Fiach\_Dubh ([medium](https://medium.com/coinmonks/the-regulators-are-coming-a1ba2f8c02be)) - see also [discussion](https://www.reddit.com/r/decred/comments/byffz1/the_regulators_are_coming_canary_in_the_decred/) on Reddit.
* Why the Name Decred is Awesome by @Haon ([medium](https://medium.com/decred/why-the-name-decred-is-awesome-9627ae9b4e2))
* The Roadblocks to Cryptocurrency Adoption in Africa by @George Pro ([medium](https://medium.com/@aappiahpro1/the-roadblocks-to-cryptocurrency-adoption-in-africa-3be2c656ec07))
* Decred Australia - Building a Community Brick by Brick by @zohand ([medium](https://medium.com/@sahand.bagheri/decred-australia-building-a-community-brick-by-brick-89928041687e))
* Staking Isn't Just a Way to Earn Crypto Money - And It Shouldn't Be by @jy-p ([coindesk.com](https://www.coindesk.com/staking-isnt-just-a-way-to-earn-crypto-money-and-it-shouldnt-be)) - also [in Korean](https://www.coindeskkorea.com/staking/).
* 由EliteX Exchange 撰写 - EliteX交易所采访了@changhugo并撰写了一份简短的概述，他们在列出DCR的同时发布了这一[文章](https://medium.com/@elitexexchange/the-lowdown-on-decred-dcr-2a36520079f5)。
* Cryptocurrency: A Mistaken Identity by @nnnko56 ([write.as](https://write.as/nnnko56/cryptocurrency-a-mistaken-identity)) - this article considers cryptocurrencies as being more than that label implies, and argues for a broader understanding of these projects as having important social components, or "cryptosocieties".

翻译:

* [Decred as a DAE Infrastructure Provider](https://medium.com/@changhugo/decred-as-a-dae-infrastructure-provider-970677f38179) - [in Italian](https://medium.com/decred-ita/decred-come-fornitore-di-infrastruttura-dae-310df09f8595) and [in Russian](https://medium.com/decred-russia/decred-%D0%BA%D0%B0%D0%BA-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA-%D0%B8%D0%BD%D1%84%D1%80%D0%B0%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D1%8B-dae-1f89952b0bab) by @DZ.
* [Decred Foundational Messaging](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md) - [in Vietnamese](https://github.com/raedahgroup/translations/blob/master/vietnamese/decred_foundational_messaging.md) by @duyenemdo.
* [Decred: Where did it all begin?](https://thedecreddigest.com/2017/06/10/decred-where-did-it-all-begin/) - [in Arabic](https://insaf01.github.io/decred-arabic/articles/decred-where-did-it-all-begin.html) by @arij and [in Vietnamese](https://github.com/raedahgroup/translations/blob/master/vietnamese/decred_where_did_it_all_begin.md) by @duyenemdo.
* [Why the name Decred is awesome](https://medium.com/decred/why-the-name-decred-is-awesome-9627ae9b4e2) - [in Arabic](https://insaf01.github.io/decred-arabic/articles/why-the-name-decred-is-awesome.html) by @arij.
* New Decred Journal translations - in Arabic by @arij, in Chinese by @guang and others, in Russian by @DZ, in Spanish by @elian, in Vietnamese by @duyenemdo. It's getting hard to list them all here (nice problem to have!), see all translations on the [index](https://xaur.github.io/decred-news/) and [mirrors](https://xaur.github.io/decred-news/mirrors.html) pages.
* Reminder: there is an effort to build [an index](https://github.com/artikozel/decred-translations/blob/master/article_index.md) of all translations and collect [statistics](https://github.com/artikozel/decred-translations/blob/master/effort_stats.md) of time it takes to produce them. Please submit yours.

视频:

* Decred Assembly：Deep Dive：DEX([youtube](https://www.youtube.com/watch?v=NuBkLA8o8ds))[优酷](https://v.youku.com/v_show/id_XNDI0NjM4MzI1Mg==.html?spm=a2h0k.11417342.soresults.dtitle)
* 在2019年共识([youtube](https://www.youtube.com/watch?v=h-AfggMHVvE))上发布 - @ jy-p提供了Decred路线图的更新。

音频:

* Decred in Depth - Ep. 2 Luke Powell - Politeia + dcrtime ([soundcloud](https://soundcloud.com/decredindepth/ep2-luke-powell-politeia-decred-contractor-model), [youtube](https://www.youtube.com/watch?v=W6yUVq97cd8))
* Decred in Depth - Ep. 3 Joel Monegro - Placeholder Capital DCR Investment Thesis + Governance ([soundcloud](https://soundcloud.com/decredindepth/joel-monegro-placeholder-capital-dcr-investment-thesis))
* Decred Distributed: Africa with Akin Sawyerr ([youtube](https://www.youtube.com/watch?v=0aZfkqdLOcI))
* Hacekernoon Podcast E55 - The Insights of Building Decentralized Infrastructure with Jake Yocom-Piatt from Decred ([hackernoon.com](https://podcast.hackernoon.com/e/the-insights-of-building-decentralized-infrastructure-with-jake-yocom-piatt-of-decred/), [youtube](https://www.youtube.com/watch?v=9i1d9C7DT9Y))
* Off the Chain with Anthony Pompliano: Jake Yocom-Piatt, Project lead for Decred: Crypto Ego Management ([player.fm](https://player.fm/series/off-the-chain-2428336/jake-yocom-piatt-project-lead-for-decred-crypto-ego-management))
* Chain Reaction with Tom Shaughnessy: Decred's Co-Founder Jake Yocom-Piatt: Governance-First Crypto Aims to Challenge Bitcoin ([youtube](https://www.youtube.com/watch?v=kO_11gehyls), [player.fm](https://player.fm/series/chain-reaction-2478788/decreds-co-founder-jake-yocom-piatt-governance-first-crypto-aims-to-challenge-bitcoin), [podbean.com](https://fiftyonepercent.podbean.com/e/decreds-jake-yocom-piatt-a-differentiated-cryptos-goal-of-overtaking-bitcoin))
* Inclusionism: Guest Akin Sawyerr on African Blockchain ([jamesfeltonkeith.com](https://www.jamesfeltonkeith.com/radioshow/episode/c184d5d5/inclusionism-guest-akin-sawyerr-on-african-blockchain-crypto-and-serial-entrepreneur-in-fintech), Decred talk starts 38 min in)
* Decred Russia podcast by @DZ ([soundcloud](https://soundcloud.com/decred-russia), in Russian)

## 社区

社区统计截至7月1日：

* Politeia用户：189（+14）
* Twitter粉丝：40,479（+17）
* Reddit订阅者：9,505（+46）
* Matrix用户：364（+27）
* Slack用户：6,769（+48）
* Discord用户：2310（+53）已通过验证：246（+20）
* 电报用户：3,407（-169）
* YouTube订阅者：3,787（+18）
* Facebook粉丝：3,230（+11），赞：2,964（+10）
* LinkedIn关注者：567（+23）
* GitHub dcrd星：494（+5），分叉：1,337（+13）

社交系统新闻:

* 在Matrix协议的[第一个稳定版本](https://matrix.org/blog/2019/06/11/introducing-matrix-1-0-and-the-matrix-org-foundation/)发布后，几个Matrix会议室进行了升级。用户必须加入新房间，但过程非常简单，所有历史记录都会保留。
* 开发流程中的Hot Matrix / Riot功能包括：可编辑的消息，反应，线程以及用于端到端加密的更好的设备验证UX。

部分 Reddit 讨论:

* 一篇[帖子](https://www.reddit.com/r/decred/comments/c60aho/governance_would_matrixlike_channel_discussions/)询问在Reddit上发布的类似Matrix的渠道讨论是否会增加采用和教育。
* [POLL：最佳Politeia通过门槛](https://www.reddit.com/r/decred/comments/bynidz/poll_optimal_politeia_pass_threshold/) - 57％表示当前水平可以，7％表示不到60％，26％表示赞成提高审批门槛。
* [POLL：将Decrediton重命名为声明](https://www.reddit.com/r/decred/comments/c4ilpw/poll_rename_decrediton_to_declaration/) - Reddit得分为0，这应该被解释为缺乏支持。
* [问题](https://www.reddit.com/r/decred/comments/c52hqd/question_is_a_hybrid_finance_governance_tool/)：混合型金融和治理工具被称为“钱包”还是完全不同的东西？
* [POLL：将DAE重命名为DAO？](https://www.reddit.com/r/decred/comments/c02geh/poll_rename_dae_to_dao/) - 得分为15，最高评论说“我支持将其改为DAO”，得到8分。另请参阅此[评论](https://www.reddit.com/r/decred/comments/c02geh/poll_rename_dae_to_dao/er1g4px)以及聊天讨论支持的说明。

Twitter讨论:

本月在Twitter上发现了更多狂野的非极端主义者，他们认为自己是比特币，但也喜欢Decred。显然，有更多这些关闭的Decred粉丝，他们不敢说出信用因为它会导致他们的圈子失去地位。

* @Ammarooni [线程](https://twitter.com/Ammarooni/status/1145213941146181632)如何“比特币地址是不是直接对肉眼可见，但将成为突出随着时间的法定货币的结构性缺陷。Decred是解决当今不在流行的Bitcoin的缺点，但可能成为表现随着时间的推移。”
* @\_Checkmatey\_ tweeted a [thread](https://twitter.com/_Checkmatey_/status/1142918632546156544) about Decred as a digital organism driven by a human hive-mind with skin in the game, then went on to [compare](https://twitter.com/_Checkmatey_/status/1145944145141411840) its stock-to-flow with Bitcoin's and finally issue a [challenge](https://twitter.com/_Checkmatey_/status/1145764832362319872) to all Bitcoiners: spend one month studying Decred and come out believing it is not a worthy number 2 to Bitcoin.
* @CryptoBrekkie created an interesting [poll](https://twitter.com/CryptoBrekkie/status/1145713705415372800) which received 720 responses. "So I've noticed a trend among some maximalists lately expressing a desire for a real, sound money competitor to Bitcoin, a rival that could ultimately help Bitcoin level up. I've also noticed many maximalists have a soft spot for [@decredproject](https://twitter.com/decredproject). Could Decred be that competitor?". 36% said Yes, 52% said No.

## 市场

6月份DCR的交易价格为24.77-37.06美元/ BTC 0.0026-0.0035。平均每日房价为28.90美元。

6月22日，比特币兑换1万美元，在几天内上涨至13,670美元。这导致包括Decred在内的大多数下降对BTC下降。

## 相关外部信息

Facebook published the [Libra white paper](https://libra.org/en-US/white-paper/) on Jun 18, and this dominated blockchain news and discussion for a spell more than any other subject has for some time. Quotes from @jy-p were featured in a number of articles about Libra on high profile sites (see Ditto update above), questioning Facebook's track record and whether inviting them to also handle our financial transactions is a good idea. We will not revisit the discussion of Libra here, except to note that the white paper addresses how it will be governed - through an association where validators (approved organizations that provide the necessary capital) vote to make decisions. 21 organizations, mostly large multinationals, were [announced](https://www.theblockcrypto.com/2019/06/14/facebooks-cryptocurrency-partners-revealed-we-obtained-the-entire-list-of-inaugural-backers/) with the white paper, with an aim to have 100 signed up before Libra launches. It will be interesting to see how a distributed ledger operated by 100 (mega-)corporations behaves in comparison to the one operated by the Decred stakeholders and their ~40,960 tickets.

Parity Technologies [released](https://www.parity.io/parity-releases-zebra-in-collaboration-with-zcash-foundation/) an alpha version of Zebra, an alternative Zcash node implementation written in Rust. The [codebase](https://github.com/ZcashFoundation/zebra) has been handed over to the Zcash Foundation. Parity first [announced](https://www.parity.io/parity-teams-up-with-zcash-foundation-for-parity-zcash-client/) plans to build an alternative node in Oct 2018. Zebra was derived from Parity's Rust [Bitcoin implementation](https://github.com/paritytech/parity-bitcoin) and will lay the foundation for a future Polkadot bridge.

Dovey Wan [announced](https://www.coindesk.com/hard-core-fund-collects-50-btc-in-china-to-support-bitcoin-developers) that the "Hard Core Fund" has accumulated 50 BTC which can be used to pay Bitcoin developers, and described the search for sustainable funding for Bitcoin developers as the biggest challenge facing the ecosystem in 2019. The fund makes payments to approved Bitcoin contributors when they send monthly reports about what they have worked on.

Another funding event for Bitcoin was two privacy projects, [Wasabi Wallet](https://www.wasabiwallet.io/) and [JoinMarket](https://github.com/JoinMarket-Org/joinmarket-clientserver), getting awarded [grants](https://bitcointalk.org/index.php?topic=279249.msg51274844#msg51274844) of 10 BTC each from a [bounty fund](https://bitcointalk.org/index.php?topic=279249.msg2983911#msg2983911) created in 2013 to incentivize work on CoinJoin. The fund is a 2-of-3 multisig controlled by Greg Maxwell, Theymos and Pieter Wuille.

The Bitcoin Cash Development Fund also [announced](https://news.bitcoin.com/bitcoin-cash-development-fund-receives-massive-support/) good progress on a development funding drive, with 760 BCH of a targeted 800 BCH raised from 900 donors.

Grin is attempting to [iterate](https://www.grin-forum.org/t/proposal-grin-governance-iteration/5191) towards a less centralized form of governance, after recognizing that the absence of formal governance processes plus the need for trusted contributors to manage shared resources (donated funds) has led to a de facto centralization of responsibility for the project. The Grin council is to become the core team. A Request for Comment process is being introduced through which feedback is sought on proposed development work. Sub-teams will organize independently with their own leaders.

Zcash continues to move towards a method of funding development long-term through a portion of the block reward, likely 10%. Zooko (CEO of Electric Coin Company) has [stated](https://finance.yahoo.com/news/zooko-wilcox-gives-zcash-community-154140125.html) that the ECC needs 12 months of runway to function and if no continuation of funding for ECC is established one year before the founder's reward, then ECC will have to consider pivoting to other projects which can generate revenue. Zooko has also expressed the opinion that the ECC should not take the lead on deciding how this funding mechanism should work, and that it should be more decentralized than the current setup. Zooko has been [looking](https://twitter.com/zooko/status/1137494548148416512) at Decred's governance as part of this process: "In a voting system with lots of cold coins, like Zcash, I would expect a good turnout to be around 1%.".

Monero Community Crowdfunding System is [funding](https://ccs.getmonero.org/proposals/RandomX-audit.html) 3 audits of the new PoW algorithm, following a [process](https://www.reddit.com/r/Monero/comments/bozr0z/randomx_auditor_selection/) in which 20 participants in the #monero-dev IRC channel voted to prioritize the audits. A CCS proposal was created which covers all 3 audits (costing $18K, $47K and $53K respectively), with audits being greenlit as enough funds became available to pay for the preferred audits.

Aragon Black [published](https://blog.aragon.black/aragon-fundraising-the-return-of-the-commons/) an article about Aragon Fundraising, which will be coming to mainnet in a few months. This is a platform for conducting Decentralized Autonomous Initial Coin Offerings (DAICOs, a concept initially [described](https://ethresear.ch/t/explanation-of-daicos/465) by Vitalik Buterin). Individuals who invest in a DAICO will receive tokens which grant them voting rights and some degree of ownership of the DAO's assets (which may come to include tokenized rights to intellectual property).

MakerDAO will be [voting](https://blog.makerdao.com/multi-collateral-dai-collateral-types/) to determine the order in which 7 pre-selected assets will be proposed for review and ratification as part of the multi-collateral DAI upgrade.

Arthur Breitman, Tezos founder, published a [blog](https://medium.com/@arthurb/potential-design-for-a-simple-and-evolvable-on-chain-treasury-77cfe2176423) with a design for a "simple and evolvable on-chain treasury". As a starting point, he suggests that funds be collected in a 3-of-5 multisig contract where the signatures are controlled by reputable parties. From there, the treasury could evolve into a system with many participants where proposals are made on chain. Sounds familiar.

There has been some friction between the developer groups working on Tezos software. The OCamlPro team introduced a proposal to fix a security issue and reward themselves from inflation funding - at a time when the other developer teams had agreed to wait and inject a proposal at a later time. OCamlPro's "early" [submission](https://www.reddit.com/r/tezos/comments/by5xy8/proposal_for_amendment_brest_a/) means that the bakers will likely vote it down and thus it will take longer before the "real" proposal is submitted. OCamlPro [appeared](https://www.reddit.com/r/tezos/comments/byqc9i/ocamlpro_what_is_the_real_motivation_behind/) to be feeling frozen out by the other teams, having submitted a bug report and failed to receive acknowledgment. Subsequently, Tezos commons published an [article](https://medium.com/tezoscommons/a-cautionary-tale-ocamlpro-65d692af09f8) which purportedly uncovers details of a plan by OCamlPro to fork the Tezos chain and capture part of the Tezos community and market capitalization - and speculates that the OCamlPro team are acting to destabilize the Tezos community ahead of this move.

An anonymous user claiming to be a current or former employee of Chainalysis participated in an AMA on r/Bitcoin, subsequently deleted but archived [here](https://www.reddit.com/r/Bitcoin/comments/c4so58/i_am_a_current_or_former_employee_of_chainalysis/) (thanks [u/Fiach_Dubh](https://www.reddit.com/r/Bitcoin/comments/c4so58/i_am_a_current_or_former_employee_of_chainalysis/eryukx6)). The answers suggested that Bitcoin privacy techniques like CoinJoin and Wasabi wallet, and all of the coins with privacy features, were hated by Chainalysis, and did not see a bright future for blockchain forensic analysis.

Speaking of CoinJoin, the community of privacy-centric Wasabi Wallet [performed](https://www.coindesk.com/bitcoin-users-perform-what-might-be-the-largest-coinjoin-ever) a 100-user CoinJoin transaction which might be the biggest to date. The more transactions in a CoinJoin, the more privacy everyone gets, but coordinating so many people is a challenge.

FATF has [finalized](https://www.coindesk.com/fatf-crypto-travel-rule) its recommendation for handling crypto. Per the new standards, businesses like exchanges and wallet providers must obtain and store information to identify both sender and recipient, and exchange this information with each other like banks do (the "travel route"). Member countries have 12 months to adopt the guidelines which will be reviewed in June 2020. The recommendations are not binding but non-complying countries risk being put on a blacklist.

Some experts [warned](https://www.coindesk.com/beyond-kyc-global-regulators-appear-set-to-adopt-tough-new-rules-for-crypto-exchanges) FATF that the new standard "could have the unintended consequence of 'encouraging P2P transfers via non-custodial wallets...'" (which sounds strikingly familiar to the intended way of using crypto). Another quote from [CoinDesk](https://www.coindesk.com/regulators-begin-to-debate-cryptocurrency-legislation-ahead-of-g20-summit) on this possible dynamic: "a common concern is that new regulations could push the public out of controlled platforms".

The recent spate of geofencing continued, with Bittrex [stopping](https://bittrex.zendesk.com/hc/en-us/articles/360028996652) US customers from trading 32 assets (DCR unaffected), and Gate.io [restricting](https://www.gate.io/article/16909) 19 assets for US customers (including DCR).

Binance is [stopping](https://techcrunch.com/2019/06/14/binance-begins-to-restrict-us-customers/) service to US customers via their global binance.com site, while [announcing](https://www.binance.com/en/blog/346119082624540672/Binance-Announces-Partnership-with-BAM-to-Launch-US-Exchange) that they will launch a separate US-based service.

Bancor is going to [block access](https://support.bancor.network/hc/en-us/articles/360029588431-US-Service-Restriction) for US users to its web application for exchanging assets.

The Indian government is [considering](https://www.theblockcrypto.com/tiny/indias-draft-bill-proposes-a-10-year-jail-sentence-for-using-cryptocurrencies/) a draft bill which would criminalize those who mine, hold, or transact with cryptocurrencies, with stiff penalties of up to 10 years in prison and fines amounting to 3 times the perpetrator's gains.

The Bitsane exchange, made famous by CNBC in a broadcast tutorial on how to buy XRP, [appears](https://thenextweb.com/hardfork/2019/06/28/cnbc-shilled-cryptocurrency-exchange-bitsane-pulls-exit-scam-on-246k-users/) to have pulled an exit scam and disappeared, along with the cryptoassets of any unfortunate users who were storing their crypto on the exchange.

A [vulnerability](https://www.yubico.com/support/security-advisories/ysa-2019-02/) in certain YubiKey products allowed an attacker to guess private keys.

Ad blocking browser extensions like uBlock are about to get hit by new Google Chrome [restrictions](https://www.theregister.co.uk/2019/06/13/google_chrome_ad_blockers/). The move was controversial, partly because the stated intent to protect users from malicious extensions also restricts their ability to block unwanted and dangerous web content.

The rate of SIM swapping attacks is [increasing](https://www.tonysheng.com/sim-swap), [educate yourself](https://medium.com/mycrypto/what-to-do-when-sim-swapping-happens-to-you-1367f296ef4d) and do what's necessary to protect your accounts.

Komodo team [exploited](https://cryptobriefing.com/komodo-developers-hacked-users/) a bug to capture $13M of users' KMD and BTC during a preventive white-hat counterattack. Komodo's version of Agama wallet was targeted by a hacker who spent months making useful contributions before inserting a dependency that steals wallet seeds. Malicious package was detected by the npm security team who [wrote](https://blog.npmjs.org/post/185397814280/plot-to-steal-cryptocurrency-foiled-by-the-npm) that this attack is becoming more popular: publish a "useful" package, wait until it is used by the target, and then update it to include a malicious payload. After being notified by npm, the Komodo team decided to use the same exploit and managed to safeguard the majority of vulnerable funds before the hacker could steal them. Affected users can submit a Google Form to claim their funds. Not identical but related incidents happened earlier when an npm package was [infected](https://thehackernews.com/2018/11/nodejs-event-stream-module.html) to steal coins from Copay wallets that used it, and when a bounty hunter added an inflation [consensus bug](https://medium.com/@bitcoinprivate/official-statement-on-coinmetrics-report-6f1cef176c05) to Bitcoin Private. These incidents show that it is crucial to carefully vet and verify contributors and to audit not only your own code but also all dependencies and all of their updates (which is not a small task).

Who would have thought that a 27-year old _text editor_ can still have an arbitrary code execution [vulnerability](https://www.theregister.co.uk/2019/06/12/vim_remote_command_execution_flaw/)? This is a reminder that correctness is hard and why it takes so much work to build and test robust software.

## 关于月报

这是Decred Journal的第15期。[此处](https://xaur.github.io/decred-news/)提供所有问题，镜像和翻译的索引。

来自第三方的大多数信息在经过最小的健全性检查后直接从源中转发。Decred Journal的作者无法验证所有声明。请注意诈骗并做自己的研究。

欢迎您在Reddit，[GitHub](https://github.com/xaur/decred-news/issues)和[Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org).上提供反馈和贡献。

感谢(字母排序）:

* 编写和编辑: bee, cryptoleslie, degeri, Dustorf, kozel, lukebp, richardred, s\_ben
* 评论和反馈: jholdstock, jz, Haon, matheusd, raedah
* 标题图片: saender

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


