# Decred月报 - 2019年6月

![abstract art](img/JUN19_journal-201906-384.jpg "Blue Dragon by @saender. Dragon resembles power/fear/terror/chaos. Blue dragon is calm and intelligent, but nevertheless powerful. It resembles a balance of power and wisdom.")

六月重点:

* Politeia 批准了 Ditto（PR）预算、错误赏金计划、开源研究、去中心化交易所(DEX)规范和区块头共识变更(提升SPV安全性并为其他改进铺路)。

* iOS Wallet v1.0于7月10日在App Store上发布。

* dcrdata v5.0发布。新图表用于显示Decred数据，改进性能、安全性和代码结构。

* 承包商管理系统（CMS）错误修复和UI改进，改善承包商递交发票的流程 - 这是推出DCC和财务报告的重要里程碑。

* 这个月我们看到了一些重要的播客以及有更多文章、社交媒体提及Decred。推特#DecredChallenge正在获得进展，鼓励人们研究和理解Decred，并讨论Decred应否在加密货币领域中占据更重要的位置。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 代码维护和更多测试覆盖。

升级了几个模块以提高代码质量。[升级](https://github.com/decred/dcrd/pull/1767) `dcrutil` v2 以减少耦合并防止处理地址时的细微错误。升级 `chaincfg` v2 模块的大改动[完成](https://github.com/decred/dcrd/pull/1698)。这样做的好处包括：通过将区块1支付定义为脚本而不是地址来减少显示关键共识代码。 `txscript` v2 [使用](https://github.com/decred/dcrd/pull/1774)了新版本 `chaincfg` 和 `dcrutil`。新版本也解决了v1的其他几个问题

[五月月报](https://github.com/xaur/decred-news/blob/master/journal/201905.md)中提到的背景模板生成器已[合并](https://github.com/decred/dcrd/pull/1748).。

我们非常谨慎地进行大型代码升级。首先，引入了一个新的模块版本，然后逐步更新关联模块以使用新版本。在任何时候，一切都必须重新构建并通过所有测试，每个提交必须通过最大程度的审查。

在其他较小的改进中，[增加了](https://github.com/decred/dcrd/pull/1757)在Go 1.13上生成Ed25519 TLS证书的支持。

[dcrwallet](https://github.com/decred/dcrwallet): 错误修复和增量改进。

默认[TLS曲线](https://github.com/decred/dcrwallet/pull/1468)更改为更安全的P-256。默认情况下，在Go 1.13上添加并启用了对[Ed25519](https://github.com/decred/dcrwallet/pull/1477) TLS证书的支持。

通过增加[`ticketbuyer.limit`](https://github.com/decred/dcrwallet/pull/1476)标志来改善票据处理，用以限制每个区块购买的最大票数和更正 `lockedbytickets` [余额计算](https://github.com/decred/dcrwallet/pull/1330)，解决solo，VSP和分票买票者面临的几个问题。一个[RPC补丁](https://github.com/decred/dcrwallet/pull/1478)将允许VSP分开显示[不成熟的选票](https://github.com/decred/dcrstakepool/pull/404)。添加了几个新的[钱包地址API](https://github.com/decred/dcrwallet/pull/1474)，以简化与地址相关功能的开发。

[正在进行](https://github.com/decred/dcrwallet/pull/1471)允许任意xpub帐户导入的开发。此功能将允许自动购票者生成不同的投票地址，避免地址重用，提高[匿名](https://github.com/decredcommunity/issues/issues/25)性。

[Decrediton](https://github.com/decred/decrediton): 继续开展[闪电网络钱包](https://github.com/decred/decrediton/pull/2107)的集成工作。改进[配置](https://github.com/decred/decrediton/pull/2129)处理，修复错误和维护。

正在测试使用有限[状态机](https://github.com/decred/decrediton/pull/2130)来更好地管理启动期间的复杂性并提高正确性。

[Politeia](https://github.com/decred/politeia): Politeia用户数据库中添加了 [插件](https://github.com/decred/politeia/pull/929)结构，可以更轻松地在Politeia的Web服务器（politeiawww）上构建通用应用程序。这将允许应用程序更轻松地存储应用程序的用户数据（例如来自承包商管理系统（CMS）的数据），同时仍然可以重新使用主用户路由。另外还创建了一个通用的dcrdata websocket [实现](https://github.com/decred/politeia/pull/933)，帮助在politeiawww上构建的应用程序更容易地监视地址余额和其他区块链数据。
 
与CMS相关的一些增量改进和错误修复，这是一个运行politeiawww的应用程序，它重用了Politeia的大部分前端。提交发票过程显着变得更容易。自5月初以来，CMS一直在处理承包商发票。

正在[重新设计](https://twitter.com/lukebp_/status/1147528570581000193)Politeia，以清理用户界面并使用与Decred品牌一致的设计，应在一个月左右的时间内推出。

五月份确定并修复了重复投票的[问题](https://github.com/decred/politeia/issues/882)，但在5月份的月报中没有提及。由于在重新检查缓存之前出现重复投票的错误，去中心化财政支出提案中有15个投票重复进入了Politeia数据存储库。我们在第一个重复投票时发现该错误并已立即[修复](https://github.com/decred/politeia/pull/893)。

容许[同时](https://github.com/decred/politeia/issues/665)运行多个Politeia系统的开发取得了进展，使电子邮件[变得可选](https://github.com/decred/politeia/issues/860)并公开费用[报告](https://github.com/decred/politeia/pull/921)。

[dcrstakepool](https://github.com/decred/dcrstakepool): 最近几个月，VSP软件越来越[受欢迎](https://github.com/decred/dcrstakepool/pull/339)。在五月[重新设计](https://github.com/decred/dcrstakepool/issues/227)之后，很多重构工作要在组件之间实现，适当的层分离对于安全性和性能会有改善。

[dcrlnd](https://github.com/decred/dcrlnd): 继续从[lnd](https://github.com/lightningnetwork/lnd)代码库移植[上游更改](https://github.com/decred/dcrlnd/pull/36)。现在已经合并了大约190个（共270个）PR合并到lnd，包括许多错误修复和两个重要功能：链下数据安全备份和监控客户端用来防止入侵。

在回答关于LN的BTC-DCR交换问题时，@matheusd多方面[澄清了](https://www.reddit.com/r/decred/comments/c17xxh/is_it_possible_to_exchange_btclightning_for/ere1skv/)这个难题的解决方案。

[dcrandroid](https://github.com/decred/dcrandroid): 小错误修复和UI改进，[西班牙语](https://github.com/decred/dcrandroid/pull/363)和[葡萄牙语（BR）](https://github.com/decred/dcrandroid/pull/367)的新翻译，以及新的发送/预算[功能](https://github.com/decred/dcrandroid/pull/371)。

[dcrios](https://github.com/raedahgroup/dcrios): v1.0.0 在6个月的活跃开发工作后在[App Store](https://apps.apple.com/us/app/decred-wallet/id1462247643)上[发布](https://www.reddit.com/r/decred/comments/cbjqff/decred_wallet_for_ios_v100_on_the_app_store/)！

初始版本有英文，俄文和简体中文版本，将来有更多翻译版本。[Release Candidate 1](https://www.reddit.com/r/decred/comments/bxje6l/decred_wallet_for_ios_release_client_1/)和[Release Candidate 2](https://www.reddit.com/r/decred/comments/c7ir8d/decred_wallet_for_ios_release_client_2/)中报告的错误已经修复，并且已经实施了一些小的UI调整。

恭喜dcrios团队：macsleven，itswisdomagain，collins，ensoreus，rktr09（开发人员），DZ（设计）和所有测试人员。

[dcrdata](https://github.com/decred/dcrdata): 正式版本，v5.0现已上线。除了体系结构，安全性和性能改进之外，v5.0还引入了许多用于探索Decred数据的新图表。

新的[市场](https://explorer.dcrdata.org/market?chart=depth&xc=aggregated&bin=1h&stack=1)页面显示来自几个主要交易所的数据，包括汇总的DCR价格信息，交易深度等。[提案](https://explorer.dcrdata.org/proposals) 页面已完成测试，并显示所有Politeia提案统计和投票图表（实时和历史）。[错过的选票](https://explorer.dcrdata.org/charts?chart=missed-votes)图表显示了一个重要的网络健康指标。

架构改进包括升级到[PostgreSQL](https://github.com/decred/dcrdata/commit/676e2ae2381e900854c2fe664a92d39a122d6ed7)（精简模式已被删除），改进的数据库模式版本控制，dcrd通知通道的[重构](https://github.com/decred/dcrdata/commit/856d0466c82338dd1aaec2945ab189da3c4ab060)，[CockroachDB](https://github.com/decred/dcrdata/commit/3ddc034e672c84313fae789c558ead139ad39f8a)的实验支持，默认的[区块预取](https://github.com/decred/dcrdata/commit/5ceb56b5c8e1ed53b6b92b5deee6e2a05903f61f)，以及带地址订阅的新pubsub模块版本。

加快了图表加载速度，包括[改进的](https://github.com/decred/dcrdata/commit/5eb60c4633d128ab64783b75b851a012ed8024fa)内存管理和新的预编码图表缓存系统。

有关更改的完整列表，请参阅[发行说明](https://github.com/decred/dcrdata/releases/tag/release-v5.0.0)。

[docs](https://github.com/decred/dcrdocs): “DAE”（Distributed Autonomous Entity）名称已[被](https://github.com/decred/dcrdocs/pull/958) “DAO”（Distributed Autonomous Organization）取代。

新页面添加了有关[算法](https://github.com/decred/dcrdocs/pull/963)，解释如何随机选择PoS票据。

其他:

* Decred二进制文件已上载到IPFS，以防GitHub / AWS无法访问。如果您运行IPFS节点，请指定哈希以增加副本并提高下载性能。我们还创建了3个HTTP网关，因此不使用IPFS的人也可以访问这些文件。最新的IPFS哈希值将始终列在此处：[dcr.jz.bz](https://dcr.jz.bz/).
* Decred[二进制文件](https://keybase.pub/jz_bz/decred/dcr-binaries/)和[视频](https://keybase.pub/jz_bz/decred/dcr-videos/)已上传到Keybase。
* 源代码在 [GitLab](https://gitlab.com/dcr-bak)上。
* [dcr-setup](https://github.com/jzbz/dcr-setup): 基于Debian和RedHat的Linux发行版的投票钱包设置脚本。

6月的开发活动统计数据：28个活动PR，321个主要提交，62K添加和29K删除的代码分布在15个存储库中。贡献来自每个存储库1-8个程序员。

## 人员

欢迎第一次代码贡献者：Marton([politeia](https://github.com/decred/politeia/commits?author=martonp)),，Amos Ezeme([dcrandroid](https://github.com/decred/dcrandroid/commits?author=crux25))，Quadri Anifowose ([dcrandroid](https://github.com/decred/dcrandroid/commits?author=Quadriyanney))，Lore([dcrandroid](https://github.com/decred/dcrandroid/commits?author=hanelore))。

虽然@DZ在[dcrandroid](ttps://github.com/decred/dcrandroid/commits?author=denyszayets) 中合并的提交被第一次检测到，但他是一个长期的Decred贡献者。

## 治理

6月，[社区基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到15,135 DCR，并花费6,657 DCR。使用6月份的平均DCR/USD价格28.90美元， 收到437,000美元和花费的192,000美元。由于这些付款用于5月份完成的工作，因此可以套用5月的平均价格27.71美元 - 在这种情况下，美元收到/支出的数字是419,000美元/ 184K美元。截至7月1日，财政部余额为622,472 DCR（1836万美元，29.50美元）。

以下是截至7月1日的提案状态。

以下提案获得批准：

* [Decred Bug Bounty Proposal: Phase 2](https://proposals.decred.org/proposals/073694ed82d34b2bfff51e35220e8052ad4060899b23bc25791a9383375cae70)- 93.5％的批准，31.5％的选民参与
* [Ditto Communications Proposal for Decred: Phase 2](https://proposals.decred.org/proposals/52ea110ea061c72d3b31ed2f5635720b212ce5e3eaddf868d60f53a3d18b8c04) - 75.8％的批准，29.2％的选民参与
* [Decred开源研究提案：第2阶段](https://proposals.decred.org/proposals/67de0e901143400ae2f247391c4d5028719ffea8308fbc5854745ad859fb993f) - 90.2％的批准，32.4％的选民参与
* [去中心化交易工具规范](https://proposals.decred.org/proposals/a4f2a91c8589b2e5a955798d6c0f4f77f2eec13b62063c5f4102c21913dcaf32) - 98.4％的批准，30％的选民参与
* [Block Header Commitments Consensus Change](https://proposals.decred.org/proposals/0a1ff846ec271184ea4e3a921a3ccd8d478f69948b984445ee1852f272d54c58) - 99.2％的批准，33.5％的选民参与。提案和[Reddit](https://www.reddit.com/r/decred/comments/buv18c/block_header_commitments_consensus_change_proposal/)上的评论者对该提案如何为技术和非技术受众提供部分表示赞赏，并且还注意到Decred的链式投票系统如何在没有多年毫无结果的讨论的情况下实现优雅的更新。

发布了2个新提案：

* [Supplemental Proposal For Decred Tutorials By Denni Lovejoy](https://proposals.decred.org/proposals/d8d7ff7ad138ed322422aaa4d2a3e1c61f296ae56a2c2316cc5ecd10cf8dd8bd). 该提案要求将教程视频的原始预算750美元增加到7,500美元。@Denni Lovejoy在看到反对意见后要求撤销该提案。目前正在讨论如何处理这些方案，其中提案的工作量大大超出预算。

* [Decred Media Campaign Proposal - Crypto Economy - 2019/2020](https://proposals.decred.org/proposals/1a367dcb91b55c60ad5fd038b219201154fcab965edd7a4639f157e409b1f4bf). 该提案要求33,600美元以多种方式宣传Decred，包括横幅广告，新闻稿，Decred赠品和时事通讯。评论说，其中一些已经得到很好的覆盖，而另一些则不可取。该提案随后被其作者撤销。

该[图](https://twitter.com/RichardRed0x/status/1139860218010058753)显示了Politeia选民参与迄今已完成投票的28项提案。

如需更深入地了解Politeia上发生的[事情](https://medium.com/politeia-digest/issue-18-june-10-june-29-97d140569ad0)，请查看6月发表的[两期](https://medium.com/politeia-digest/issue-17-may-28-june-9-bc5bb77e4f6c) “Politeia Digest”。

以下[问题](https://www.reddit.com/r/decred/comments/bx00fu/so_about_the_exmo_exchange/)在Reddit上，Exmo发布了简短的[更新](https://twitter.com/Exmo_Com/status/1138020825137930240)，并接着于6月18日[开放](https://exmo.com/en/news_view?id=2776)DCR交易。

r/decred subreddit上的一些帖子试图在Decred社区中对[最佳Politeia批准门槛](https://www.reddit.com/r/decred/comments/bynidz/poll_optimal_politeia_pass_threshold/)进行投票，[将Decrediton重命名为Declaration](https://www.reddit.com/r/decred/comments/c4ilpw/poll_rename_decrediton_to_declaration/)，[将Decrediton称为钱包以外的其他内容](https://www.reddit.com/r/decred/comments/c52hqd/question_is_a_hybrid_finance_governance_tool/)，并询问Decred是否应该开始[使用DAO而不是DAE](https://www.reddit.com/r/decred/comments/c02geh/poll_rename_dae_to_dao/)来描述去中心化利益相关者对项目的治理。

最后一次轮询（将DAE重命名为DAO）可以被@s_ben视为“软提案”。这个提案背后的理由是，虽然最初选择DAE（Distributed Autonomous Entity）这个名称是为了避免与以太坊[DAO黑客](https://www.google.com/search?q=ethereum+dao+hack)关联，但DAO从此成为加密中的热门话题，与DAO hack几乎没有联系。 。因为Decred已经建立了一个正常运行的DAO（制作了这份月报），Decred更有代表性参与相关对话。曾考虑发起一项Politeia提案，但各通信渠道都对提案没有异议（如此[评论](https://www.reddit.com/r/decred/comments/c02geh/poll_rename_dae_to_dao/er1g4px)所述）），粗略的共识是，除非有任何强烈反对，否则这种改变不需要Politeia提案。@s_ben更改了[文档](https://docs.decred.org/governance/politeia/overview/#decentralized-autonomous-organization-dao)的引用，并提交了一个[代码请求](https://github.com/decred/dcrweb/pull/681)来更改decred.org上的术语。这一举措的讨论总结在[这里](https://github.com/decredcommunity/issues/issues/134).。

虽然其中一些民意调查及其周围的讨论很有意思，但社区成员已经注意到使用Reddit和民意调查网站来衡量Decred利益相关者的意见存在问题。这些平台向非利益相关者开放，允许他们的创建者任意删除或修改民意调查/帖子。在讨论这种现象的过程中，基于Politeia的[Decred版本的Reddit](https://github.com/decredcommunity/issues/issues/38)似乎得到了强有力的支持，这将允许创建有限数量的民意调查。

## 网络

网络算力：6月份的哈希值从~504 Ph/s开启，月底约为540 Ph/s，最低369 Ph/s，整个月最高达到607 Ph/s。截至7月2日的池哈希值分布：lab.antpool.com 18％，UUPool 17.7％，F2Pool 14％，Poolin 9.5％，BTC.com 9％，Luxor 2.2％，CoinMine 0.21％，BeePool 0.15％，suprnova 0.03％和其他人 29%，数据来自[dcrstats.com](https://dcrstats.com/pow)。池分布数是近似值，无法准确确定。


Staking: 每个dcrstats.com的30天平均票价为120 DCR（+4）。价格在116.8-127.3 DCR之间变化。锁定金额为475-484万DCR，相当于可用供应量的[48.01-49.03%](https://charts.dcr.farm/d/000000003/proof-of-stake?orgId=1&from=1559347200000&to=1561939200000) 。

节点数: 整个6月，根据[dcr.farm](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1559347200000&to=1561939200000)大约有200个监听节点和340-510个总节点。截至7月8日，大约80％运行v1.4.0,9％运行dcrwallet v1.4.0（SPV）和4％运行v1.5.0（pre）dev版本。

dcr.farm更新了[闪电网络](https://charts.dcr.farm/d/DHPdAO4Wz/lightning-network?orgId=1)仪表板。截至7月8日，DCR testnet LN显示15个节点，45个通道，总容量为370 DCR。

6月27日，DCR供应量[超过](https://twitter.com/raedahgroup/status/1144655370234880000) 10,000,000 DCR。1000万DCR分布意味着初始[预挖](https://docs.decred.org/advanced/premine/)占当前流通DCR的17％，到目前为止，PoW矿工获得50％，PoS选民获得25％，财政部获得8％。

选票持有人提出请求说某些VSP[错过了](https://www.reddit.com/r/decred/comments/c862ee/assistance_needed_missed_tickets/)他们的门票。经过调查，发现Grassfed和d1pool已从网络中分叉并且错过了对他们的选票的投票。 [Grassfed](https://dcr.grassfed.network/)做出了回应并承诺将继续保持未来的更新。我们无法访问[d1pool](https://d1pool.com) ，目前正在讨论将它们从decred.org 的[VSP列表](https://decred.org/vsp/)中删除。

同时也出现了一个[问题](https://github.com/decred/dcrstakepool/issues/413)和一个[讨论](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$156207152510654HMiFp:decred.org) 如何将这些问题能在未来避免。另一个讨论的想法是持续努力让更多人建立自己的[投票钱包](https://matrix.to/#/!dhHYPTtCtvPSUfTepT:decred.org/$156207972910815kERGq:decred.org).

## 整合

Exmo完成他们的 [提案](https://proposals.decred.org/proposals/950e8149e594b01c010c1199233ab11e82c9da39174ba375d286dc72bb0a54d7)，在6月18日[上线](https://exmo.com/en/news_view?id=2776)了 DCR/BTC，DCR/RUB和DCR/UAH交易对。

Vertbase 为美国客户增加了[定期订单](https://twitter.com/vertbase/status/1141826092564701184)和[出售](https://twitter.com/vertbase/status/1141735926059716611)美元数字资产的选项。

EliteX [上线](https://twitter.com/elitexcrypto/status/1143044131800977409)了 DCR交易对，并写了[一篇文章](https://medium.com/@elitexexchange/the-lowdown-on-decred-dcr-2a36520079f5)向他们的用户解释Decred。

抹茶交易所（MXC Exchange）[上线](https://twitter.com/wanbihou/status/1143846271645437952)了DCR / USDT交易对。

Bleutrade [宣布](https://bleutrade.com/announcements/) DCR将在7月15日计划的大规模清理中被退市 - 今年的第二次退市 ([讨论](https://www.reddit.com/r/decred/comments/c86a75/bleutrade_will_delist_dcr_20190715_1500_utc/))。Bleutrade非常[支持](https://twitter.com/BLEUTRADE/status/999683568791060481)Decred。他们是第一个上线Decred的交易所，在[2016年2月8日](https://bitcointalk.org/index.php?topic=1290358.1640)主网上线的第一天。

Decred的Trust Wallet集成部分 [即将完成](https://github.com/trezor/blockbook/pull/216)。在三月份获得批准后，该[提案](https://proposals.decred.org/proposals/2ababdea7da2b3d8312a773d477272135a883ed772ba99cdf31eddb5f261d571)分成两部分。Trust Wallet团队负责核心钱包集成（完成）与我们负责整合Trust Wallet用于托管交易数据的Blockbook服务器。

警告: Decred 月报作者无法确认以上交易所可靠性。请自行进行审核才将您的个人信息或财产信托于任何实体。

## 外联活动

在外展方面继续取得进展，重点关注在教育，让人更容易学习Decred。正在进行建立社交媒体指引，鼓励每个社区成员都做出贡献。[Checkmate](https://twitter.com/_Checkmatey_) 已经在推特上引入了[#DecredChallenge](https://twitter.com/hashtag/DecredChallenge)标签，并[挑战](https://twitter.com/_Checkmatey_/status/1145764832362319872)每个人学习Decred 30天，并解释为什么Decred不应该是市值＃2。结果非常积极，Decred社交媒体活动和效果显着提升。喜欢和评论Decred信息非常重要，因为这样可以增加覆盖范围，并可以编写更多故事。

在教育的基础上，网站即将上线，会有新的介绍视频和关于安全，适应性，自筹资金，历史和教育子页面。这项工作将有助于更容易理解Decred，从而帮助社区发展。

@anshawblack在访问@lukebp和Joel Monegro后发行了Decred in Depth播客剧集。@Dustorf和@jy-p录制了Decred Assembly剧集，包括Decred Distributed with @akinsawyerr在Decred in Africa，Deep Dive with @moo31337 on the Treasury proposal，以及Decred Distributed with @richardred。后两集将很快发布。

世界各地正在计划各种活动，包括德国，日本，中国和多伦多。该项目为2019年欧洲和亚洲的重大活动提供资金，尚未作出具体承诺。如果您有具体想法，请分享到#event_planning。我们依靠世界各地的社区来帮助识别和执行机会。

Decred在治理问题上取得了重大进展。CoinDesk中提到了Decred作为staking的领先项目，而@akinsawyerr 在沃顿商学院治理会议上与该领域的主要发言人一起[发表了讲话](https://github.com/decredcommunity/events/blob/master/reports/20190701-wharton-governance-workshop-san-francisco-usa.md)。有很多关于Decred的讨论，Decred作为治理的先驱和领导者受到广泛尊重，Decred已被邀请在日本的治理会议上发言。

Ditto六月成就:

* 促进了@jy-p和CoinDesk之间关于治理和staking的介绍性访谈
* 促进了Legacy Research分析师Greg Wilson和@moo31337的采访，他们对Decred进行了概述和更新，面向投资者
* 促进了Morgan Creek Digital的创始人Anthony Pompliano和@jy-p的[Off the Chain](https://podcasts.apple.com/us/podcast/jake-yocom-piatt-project-lead-for-decred-crypto-ego/id1434060078?i=1000441486954)播客
* 促进了Delphi Digital的Tom Shaughnessy和@jy-p的[Chain Reaction](https://www.youtube.com/watch?v=kO_11gehyls)播客
* 在以下媒体报导Facebook Libra时提到Decred：[CNBC](https://www.cnbc.com/2019/06/18/facebooks-libra-will-give-billions-access-to-cryptocurrency.html)，[Mashable](https://mashable.com/article/facebook-libra-experts/)，[CoinTelegraph](https://cointelegraph.com/news/what-is-libra-breaking-down-facebooks-new-digital-currency)和[Forbes](https://www.forbes.com/sites/kenrapoza/2019/06/20/facebooks-libra-coin-is-both-vampire-project-and-regulatory-nightmare/)（[第二次](https://www.forbes.com/sites/rachelwolfson/2019/06/19/facebooks-cryptocurrency-libra-validates-blockchain-but-industry-experts-voice-concerns/)!）。旁注：CNBC和Mashable是主流媒体，吸引那些对加密货币知之甚少的人，我们正在大大扩展其覆盖范围
* CoinDesk治理文章[引用](https://www.coindesk.com/how-blockchain-voting-is-supposed-to-work-but-in-practice-rarely-does)@jy-p。
* @richardred 在CoinTelegraph上 [引用](https://cointelegraph.com/news/internet-authority-history-of-centralized-companies-being-hostile-toward-crypto) 了关于CCN“关闭”的文章。
* 参加旧金山比特币聚会，组织者表示有兴趣组建一个治理圆桌，给予Decred演讲机会
* 制作了如何对退市做出回应（或不做出回应）的社交媒体[指南](https://github.com/decredcommunity/pr/blob/release/engagement-guide-delist.md)
* 召集社区参与并在社交媒体上分享媒体报道
* 提交[Ditto提案：第2阶段](https://proposals.decred.org/proposals/52ea110ea061c72d3b31ed2f5635720b212ce5e3eaddf868d60f53a3d18b8c04)到Politeia，参与讨论，然后被Decred利益相关方批准！感谢您的信任投票。在Decred工作是一种绝对的快乐，我们期待未来6个月

社区活动:

* 6月5日 - [Decred x Blueyard](https://www.eventbrite.co.uk/e/decred-x-blueyard-berlin-meetup-tickets-61631192556) - 德国柏林。@Haon的完整报告在[这里](https://github.com/decredcommunity/events/blob/master/reports/20190605-decred-x-blueyard-berlin-germany.md)
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

经过改进的活动报告库现在有14个[详细报告](https://github.com/decredcommunity/events)。请提交您的报告并在Reddit / Twitter上分享，以了解每个月发生的事件。

## 媒体

Ditto的公关指南已收集在新的[代码库中](https://github.com/decredcommunity/pr)，目前包括[基础消息传递](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md), [选票消息传递](https://github.com/decredcommunity/pr/blob/release/ticket-messaging.md) 和 [参与指南](https://github.com/decredcommunity/pr/blob/release/engagement-guide-delist.md)如何对退市/地理围栏做出反应。

为任何不适合decred.org或文档的知识启动了一个新的[社区wiki](https://github.com/decredcommunity/wiki)存储库。第一个创建的页面是Decred[社交媒体](https://github.com/decredcommunity/wiki/blob/master/wiki/social-media.md)组的综合列表。

精选文章:

* @Haon的[区块链治理象限](https://medium.com/@NoahPierau/the-blockchain-governance-quadrant-2a878a9cacb9（[中文]（https://github.com/Guang168/DCR_CommunityArticles/blob/master/The_Blockchain_Governance_Quadrant_CN.md））
* 监管机构即将到来 - Canary在Decred Hash Mine: [第一部分](https://medium.com/coinmonks/the-regulators-are-coming-a1ba2f8c02be) - 另见关于Reddit的 [讨论](https://www.reddit.com/r/decred/comments/byffz1/the_regulators_are_coming_canary_in_the_decred/)。
* 为什么Decred这个名字很棒 by @Haon ([medium](https://medium.com/decred/why-the-name-decred-is-awesome-9627ae9b4e2))
* @George Pro在非洲采用加密货币的障碍 ([medium](https://medium.com/@aappiahpro1/the-roadblocks-to-cryptocurrency-adoption-in-africa-3be2c656ec07))
* Decred 澳大利亚 -by @zohand ([medium](https://medium.com/@sahand.bagheri/decred-australia-building-a-community-brick-by-brick-89928041687e))
* Staking不仅仅可以赚取加密货币 -by @jy-p ([coindesk.com](https://www.coindesk.com/staking-isnt-just-a-way-to-earn-crypto-money-and-it-shouldnt-be)) -  [韩语](https://www.coindeskkorea.com/staking/).
* 由EliteX Exchange 撰写 - EliteX交易所采访了@changhugo并撰写了一份简短的概述，他们在上线DCR的同时发布了这一[文章](https://medium.com/@elitexexchange/the-lowdown-on-decred-dcr-2a36520079f5)。
* 加密货币社会: by @nnnko56 ([write.as](https://write.as/nnnko56/cryptocurrency-a-mistaken-identity))

翻译:

* [Decred as a DAE Infrastructure Provider](https://medium.com/@changhugo/decred-as-a-dae-infrastructure-provider-970677f38179) - [意大利语](https://medium.com/decred-ita/decred-come-fornitore-di-infrastruttura-dae-310df09f8595) 和 [俄罗斯语](https://medium.com/decred-russia/decred-%D0%BA%D0%B0%D0%BA-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA-%D0%B8%D0%BD%D1%84%D1%80%D0%B0%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D1%8B-dae-1f89952b0bab) by @DZ.
* [Decred Foundational Messaging](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md) - [越南语](https://github.com/raedahgroup/translations/blob/master/vietnamese/decred_foundational_messaging.md) by @duyenemdo.
* [Decred: Where did it all begin?](https://thedecreddigest.com/2017/06/10/decred-where-did-it-all-begin/) - [阿拉伯语](https://insaf01.github.io/decred-arabic/articles/decred-where-did-it-all-begin.html) by @arij and [越南语](https://github.com/raedahgroup/translations/blob/master/vietnamese/decred_where_did_it_all_begin.md) by @duyenemdo.
* [Why the name Decred is awesome](https://medium.com/decred/why-the-name-decred-is-awesome-9627ae9b4e2) - [阿拉伯语](https://insaf01.github.io/decred-arabic/articles/why-the-name-decred-is-awesome.html) by @arij.
* 新的Decred月报翻译 - @arij的阿拉伯语，@guang和其他人的中文，@DZ的俄语，@elian的西班牙语，@duyenemdo的越南语。这里很难列出所有这些（很好的问题！），查看[索引](https://xaur.github.io/decred-news/)和[镜像](https://xaur.github.io/decred-news/mirrors.html)页面上的所有翻译。
*提示：我们正在努力构建一个翻译[索引](https://github.com/artikozel/decred-translations/blob/master/article_index.md)并收集[数据](https://github.com/artikozel/decred-translations/blob/master/effort_stats.md)，包括翻译所需时间。请提交你的数据。

视频:

* Decred Assembly：Deep Dive：DEX([youtube](https://www.youtube.com/watch?v=NuBkLA8o8ds))([优酷](https://v.youku.com/v_show/id_XNDI0NjM4MzI1Mg==.html?spm=a2h0k.11417342.soresults.dtitle))
* Decred在2019年共识会议([youtube](https://www.youtube.com/watch?v=h-AfggMHVvE))上发表的演讲 - @jy-p提供了Decred路线图更新。

音频:

* Decred in Depth - Ep. 2 Luke Powell - Politeia + dcrtime ([soundcloud](https://soundcloud.com/decredindepth/ep2-luke-powell-politeia-decred-contractor-model), [youtube](https://www.youtube.com/watch?v=W6yUVq97cd8))
* Decred in Depth - Ep. 3 Joel Monegro - Placeholder VC DCR 投资论文 + 治理 ([soundcloud](https://soundcloud.com/decredindepth/joel-monegro-placeholder-capital-dcr-investment-thesis))
* Decred Distributed: 非洲 with Akin Sawyerr ([youtube](https://www.youtube.com/watch?v=0aZfkqdLOcI))
* Hacekernoon Podcast E55 - 建造去中心化基础设施的经验分享 with Jake Yocom-Piatt from Decred ([hackernoon.com](https://podcast.hackernoon.com/e/the-insights-of-building-decentralized-infrastructure-with-jake-yocom-piatt-of-decred/), [youtube](https://www.youtube.com/watch?v=9i1d9C7DT9Y))
* Off the Chain with Anthony Pompliano: Jake Yocom-Piatt, Decred项目领导: Crypto 权力管理 ([player.fm](https://player.fm/series/off-the-chain-2428336/jake-yocom-piatt-project-lead-for-decred-crypto-ego-management))
* Chain Reaction with Tom Shaughnessy: Decred's Co-Founder Jake Yocom-Piatt: 治理加密货币在挑战比特币 ([youtube](https://www.youtube.com/watch?v=kO_11gehyls), [player.fm](https://player.fm/series/chain-reaction-2478788/decreds-co-founder-jake-yocom-piatt-governance-first-crypto-aims-to-challenge-bitcoin), [podbean.com](https://fiftyonepercent.podbean.com/e/decreds-jake-yocom-piatt-a-differentiated-cryptos-goal-of-overtaking-bitcoin))
* Inclusionism: Guest Akin Sawyerr on African Blockchain ([jamesfeltonkeith.com](https://www.jamesfeltonkeith.com/radioshow/episode/c184d5d5/inclusionism-guest-akin-sawyerr-on-african-blockchain-crypto-and-serial-entrepreneur-in-fintech), Decred 在38分钟)
* Decred 俄罗斯播客 by @DZ ([soundcloud](https://soundcloud.com/decred-russia), 俄罗斯语)

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

* Matrix协议的[第一个稳定版本](https://matrix.org/blog/2019/06/11/introducing-matrix-1-0-and-the-matrix-org-foundation/)发布后，几个Matrix会议室进行了升级。用户必须加入新房间，但过程非常简单，所有历史记录都会被保留。
* 开发流程中的Hot Matrix / Riot功能包括：可编辑的消息，反应，线程以及用于端到端加密的更好的设备验证UX。

部分 Reddit 讨论:

* 一篇[帖子](https://www.reddit.com/r/decred/comments/c60aho/governance_would_matrixlike_channel_discussions/)询问在Reddit上发布的类似Matrix的渠道讨论是否会增加采用和教育。
* [POLL：最佳Politeia通过门槛](https://www.reddit.com/r/decred/comments/bynidz/poll_optimal_politeia_pass_threshold/) - 57％表示当前水平可以，7％表示不到60％，26％表示赞成提高审批门槛。
* [POLL：将Decrediton重新命名声明](https://www.reddit.com/r/decred/comments/c4ilpw/poll_rename_decrediton_to_declaration/) - Reddit得分为0，这应该被解释为缺乏支持。
* [问题](https://www.reddit.com/r/decred/comments/c52hqd/question_is_a_hybrid_finance_governance_tool/)：混合型金融和治理工具被称为“钱包”还是完全不同的东西？
* [POLL：将DAE重命名为DAO？](https://www.reddit.com/r/decred/comments/c02geh/poll_rename_dae_to_dao/) - 得分为15，最高评论说“我支持将其改为DAO”，得到8分。另请参阅此[评论](https://www.reddit.com/r/decred/comments/c02geh/poll_rename_dae_to_dao/er1g4px)以及聊天讨论支持的说明。

Twitter讨论:

本月在Twitter上发现了更多狂野的非极端主义者，他们认为自己是比特币，但也喜欢Decred。显然，有更多这些不公开的Decred粉丝，他们不敢公开承认喜欢Decred，因为会导致他们在圈子失去地位。

* @Ammarooni [推文](https://twitter.com/Ammarooni/status/1145213941146181632)如何“比特币解决了法定货币的结构性缺陷，缺乏透明度。Decred解决现在并不明显的Bitcoin缺点。”
* @\_Checkmatey\_ [推文](https://twitter.com/_Checkmatey_/status/1142918632546156544) Decred是智能物种，被权益相关者推动，并[比较了](https://twitter.com/_Checkmatey_/status/1145944145141411840) Decred与比特币的stock-to-flow比率。最后向比特币爱好者提出了[挑战](https://twitter.com/_Checkmatey_/status/1145764832362319872): 花一个月时间学习Decred，看看Decred是不是应该排在比特币后的第二位。
* @CryptoBrekkie 创建了一个[投票](https://twitter.com/CryptoBrekkie/status/1145713705415372800) 并有720个回应. "我最近注意到一些比特币极端主义者希望看到能跟比特币竞争的货币项目，这种竞争对手最终可以帮助比特币变得更好。我注意到许多极端主义者对[@decredproject](https://twitter.com/decredproject)情有独钟。 Decred可能是那个竞争对手吗？“ 36％的人说是，52％的人说不是。

## 市场

6月份DCR的交易价格为24.77-37.06美元/ BTC 0.0026-0.0035。平均每日房价为28.90美元。

6月22日，比特币兑换1万美元，在几天内上涨至13,670美元。这导致包括Decred在内的大多数项目BTC交易对价格下降。

## 相关外部信息

Facebook在6月18日发布了[Libra 白皮书](https://libra.org/en-US/white-paper/) ，并且主导了区块链新闻和讨论。@jy-p对Libra的评论出现在数个主要媒体上(参见上面的Ditto更新)，质疑Facebook的名声以及思考是否应该让他们处理我们的金融交易。我们不会在这里详细讨论Libra，值得注意的是白皮书上提及的治理模式 - 通过一个协会，验证者（提供必要资本并被批准加入的组织）投票决定。 21个组织(主要是大型跨国公司)[已宣布](https://www.theblockcrypto.com/2019/06/14/facebooks-cryptocurrency-partners-revealed-we-obtained-the-entire-list-of-inaugural-backers/)加入，目标是在Libra上线之前和100个验证者达成合作。比较Decred staker运营的分布式账本和100家大型公司运营的分布式账本，将会很有趣。

Parity Technologies [推出](https://www.parity.io/parity-releases-zebra-in-collaboration-with-zcash-foundation/) Zebra 测试版本, 用Rust编写的Zcash节点实现。[代码库](https://github.com/ZcashFoundation/zebra) 已经递交给 Zcash。Parity 在2018年10月 [公布](https://www.parity.io/parity-teams-up-with-zcash-foundation-for-parity-zcash-client/) 编写节点实现的计划。Zebra 跟 Parity 的 Rust [比特币节点](https://github.com/paritytech/parity-bitcoin) 类似，将会用作连接Polkadot。

Dovey Wan [公布](https://www.coindesk.com/hard-core-fund-collects-50-btc-in-china-to-support-bitcoin-developers) "Hard Core 基金" 已经累积了50个比特币用作支持比特币开发，并描述了为比特币开发寻找可持续资金是2019年生态面临的最大挑战。该基金每月向提交工作报告的验证程序员付款。

比特币现金发展基金[公布](https://news.bitcoin.com/bitcoin-cash-development-fund-receives-massive-support/)在开发资金方面取得了良好进展，已经从900名捐助者中筹集了760 BCH，目标是800 BCH。

在意识到缺乏正式的治理流程和需要依赖贡献者管理共享资源(捐赠的资金)，造成中心化后，Grin正试图[采用](https://www.grin-forum.org/t/proposal-grin-governance-iteration/5191)不那么中心化的治理形式，Grin理事会将成为核心团队。创立了征求意见流程，开放讨论未来开发项目，开发分队将与他们自己的领导人建立独立组织。

Zcash打算通过一部分区块奖励来长期资助发展，可能是10％。 Zooko（Electric Coin Company的首席执行官）[声明](https://finance.yahoo.com/news/zooko-wilcox-gives-zcash-community-154140125.html)ECC需要12个月才能运行，如果在创始人奖励之前一年没有资金支持ECC，那么ECC将不得不考虑转向其他可以产生收入的项目。 Zooko还表示，ECC不应该在决定这种筹资机制如何运作方面起带头作用，而且它应该比目前的设置更加去中心化。作为这个过程的一部分，Zooko在Decred的治理机制中一直[寻找](https://twitter.com/zooko/status/1137494548148416512)答案：“在一个有很多冷代币的投票系统中，比如Zcash，我预计会有很好的投票率，约为1％。“

Monero社区众筹系统在[资助](https://ccs.getmonero.org/proposals/RandomX-audit.html)3的对新PoW算法的审核，遵循[流程](https://www.reddit.com/r/Monero/comments/bozr0z/randomx_auditor_selection/)其中monero-dev IRC频道的20名参与者投票决定审核的优先顺序。创建了一个CCS提案，涵盖了所有3项审计(分别花费18,000美元，47,000美元和53,000美元)。

Aragon Black [发布](https://blog.aragon.black/aragon-fundraising-the-return-of-the-commons/)一篇关于Aragon筹款系统的文章，该系统将在几个月后上线主网。这是一个进行去中心化ICO的平台（DAICO，这是Vitalik Buterin最初[描述](https://ethresear.ch/t/explanation-of-daicos/465)的概念）。投资DAICO的投资者将获得代币，这些代币授予他们投票权和DAO资产的所有权（可能包括对知识产权的象征性权利）。

MakerDAO将[投票](https://blog.makerdao.com/multi-collateral-dai-collateral-types/)确定7个预先选定资产的投票顺序，用作多方担保DAI。

Tezos创始人Arthur Breitman发布了一个[博客](https://medium.com/@arthurb/potential-design-for-a-simple-and-evolvable-on-chain-treasury-77cfe2176423) “简单，可进化的链上基金会”。作为一个起点，他建议将资金收集在3-of-5的多签合约，其中签名由信誉良好的各方控制。从那里，财政部可以演变成一个系统，有许多参与者在链上提出建议。听起来很熟悉。

Tezos软件开发团队之间存在一些摩擦。 OCamlPro团队提出了一项解决安全问题并通过通胀资金奖励自己的提议，尽管当时其他开发团队不想在现在提出提案。 OCamlPro的“早期”[提交](https://www.reddit.com/r/tezos/comments/by5xy8/proposal_for_amendment_brest_a/)意味着Baker会投反对票。 OCamlPro [似乎](https://www.reddit.com/r/tezos/comments/byqc9i/ocamlpro_what_is_the_real_motivation_behind/)觉得被其他团队排挤，提交了错误报告但得不到奖励。随后，Tezos公告发表了一篇[文章](https://medium.com/tezoscommons/a-cautionary-tale-ocamlpro-65d692af09f8)，其中据称揭示了OCamlPro计划的细节，将Tezos链分叉并捕获部分Tezos社区和市值 - 并推测OCamlPro团队正在采取行动，在计划破坏Tezos社区。

声称是Chainalysis的现任或前任员工的匿名用户参与了r/Bitcoin 的AMA，随后被删除但存档[在此](https://www.reddit.com/r/Bitcoin/comments/c4so58/i_am_a_current_or_former_employee_of_chainalysis/)(感谢[u/Fiach_Dubh](https://www.reddit.com/r/Bitcoin/comments/c4so58/i_am_a_current_or_former_employee_of_chainalysis/eryukx6))。回答表明，像CoinJoin和Wasabi钱包这样的比特币隐私技术，以及所有具有隐私功能的代币，都受到了Chainalysis的憎恨，所以他认为区块链分析前景并不光明。

说到CoinJoin，以隐私为中心的Wasabi Wallet社区[执行](https://www.coindesk.com/bitcoin-users-perform-what-might-be-the-largest-coinjoin-ever)了100位用户的CoinJoin交易，可能是迄今为止最大的交易。 CoinJoin中的交易越多，每个人获得的隐私就越多，但协调这么多人是一项挑战。

币安正在[停止](https://techcrunch.com/2019/06/14/binance-begins-to-restrict-us-customers/)通过其全球binance.com网站向美国客户提供服务，同时[宣布](https://www.binance.com/en/blog/346119082624540672/Binance-Announces-Partnership-with-BAM-to-Launch-US-Exchange)将启动独立的美国服务。

印度政府正[考虑](https://www.theblockcrypto.com/tiny/indias-draft-bill-proposes-a-10-year-jail-sentence-for-using-cryptocurrencies/)一项法案将挖掘加密货币，持有或交易的人定为刑事犯罪，并处以长达10年的监禁和巨大罚款。

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

感谢 (按字母排序): dominic, guang, hugo

