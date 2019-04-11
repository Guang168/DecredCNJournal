# Decred月报 - 3月

![abstract art](img/MAR19_journal-201903-384.jpg "Undercurrent by @saender. It is empirical and abstract but the concept is to let people know via Journal and the image about the unseen forces that move it forward.")


在3月份里，治理方面看到了一些重要的提案和投票，并且在开发方面的核心软件上取得了可靠的进展 - 这是Decred的一个相当典型的月份。

最新的[共识投票](https://voting.decred.org/)[修复](https://github.com/decred/dcps/blob/master/dcp-0004/dcp-0004.mediawiki)闪电网络序列锁定目前在几乎100% 的支持率和 54% 的参与率即将完成，投票预计将于 4月11日结束。

在 Politeia 上，发起了 5 项新提案，并有两项提案完成投票（一个通过，一个不通过）。被提交的提案中包括了 @moo31337 提交的[重要提案](https://proposals.decred.org/proposals/c96290a2478d0a1916284438ea2c59a1215fe768a87648d04d45f6b7ecb82c3f)，其中概述了利益相关者去中心化控制社区基金开销的途径。

在 dcrd 里也看到了一些巨大的[重构](https://github.com/decred/dcrd/pull/1656)，这将在 v1.5.0 发布时为用户带来显著的性能改进，当然高级用户也可以从源码构建。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 一项大的[重构](https://github.com/decred/dcrd/pull/1656)让初始完全同步时间增快 [20-25%](https://twitter.com/davecgh/status/1110649183185317889), 在典型硬件耗时大约 45 分钟。另一个好处是降低了投票广播的延迟：

> 影响\[延迟\]的因素很多,但在我的节点里平均每节点为 ～70 毫秒至 5 毫秒以下。我们需要更多的数据才能获得更准确的数值。这个本身是好事，但真正的好处将在重大网络升级时更能体现，在多个投票节点节省的时间更可观。全面部署整体改善高达～90％。([@davecgh](https://twitter.com/davecgh/status/1110721000172384256))

作为优化的一部分，`txscript`模块使用新的零分配脚本标记器进行完全重构。

> 初始同步当然是一个重要因素，但真正的好处在于 mempool 正在进行的交易处理。另一个非常好的方面是导出的标记化器，这意味着可以对 txscript 之外的脚本进行零分配分析，这对于构建应用程序（例如原子交换，主根等）非常有用。([@davecgh](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$155249146926580yNJqU:decred.org))

由于共识代码的关键且容易出错的区域进行更改，因此通过精心制作一系列122个单独的提交，让每个提交消息彻底描述其目的，确保保持共识，因此通过所有测试，使这些更改更容易推理和审查。

另外：重构大幅削减了大约 2K 行代码。越少代码行，越少漏洞！

另外也发现了一个删除额外 10-15 分钟的初始块下载的机会，但它需要几个月的扎实工作 _(贡献者来吧)_。

其他已整合工作:

* 初始的 Bech32 ([BIP 173](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki)) 支持已从 btcsuite [移植](https://github.com/decred/dcrd/pull/1646)。
* 推出可重用的 [LRU cache](https://github.com/decred/dcrd/pull/1683)模块。
* [重构](https://github.com/decred/dcrd/pull/1696)`hdkeychain`模块使代码更简洁及更易测试。
* [增加](https://github.com/decred/dcrd/pull/1424)新的背景区块模版生成器。
* 许多重构及测试改进以增强代码对于意外改动的抵抗性。

在3月份里，总共有 9 位贡献者的[209 份提交](https://github.com/decred/dcrd/compare/4e7f080b7b2cb11a8680d54dc5fb9ce735119d15...8f5019e083e92f31b2799f9d23809e0c0692d465)被整合。

进行中:

* 另一项针对`chaincfg`模块中几个问题的重大重构工作已[开始](https://github.com/decred/dcrd/pull/1698)。
* 有关保护节点播种过程中免受基于 DNS 攻击的讨论已经[展开](https://github.com/decred/dcrd/issues/1645)。

总体而言，像背景区块模板生成器和`txscript`优化的一部分这样的变化旨在通过改进挖矿基础设施和减少投票传播延迟来提高可扩展性并减少网络的错过票数量。`txscript`和`chaincfg`重构的另一部分是基础设施工作，以正确引入新的脚本引擎版本，以便进行未来理想的共识变更，例如去中心化财政支出。即使该提案没有通过，我们仍然需要这些基础设施来进行各种未来与脚本相关的共识变更。

[dcrwallet](https://github.com/decred/dcrwallet): 错误修复和代码维护。整合了6位贡献者的[12 份提交](https://github.com/decred/dcrwallet/compare/9f5f1163d8bf8037138f07734002470d4100de21...9450c9183e71231065dc0ea25087a47e8e5bb38e)。

[Decrediton](https://github.com/decred/decrediton): 选票活动热图可视化和一些较小的修复 - 2位贡献者的 [5 份提交](https://github.com/decred/decrediton/compare/35ab6e216dde0bc90d76334e25eb5174bf62e623...f80e832e55231a8f4cb7b1aa69f6e2faea2709df)。

[Politeia](https://github.com/decred/politeia): 添加提案文本[预览](https://github.com/decred/politeiagui/pull/1018)标签，完成提案版本的[查看差异](https://github.com/decred/politeiagui/pull/1004)功能，更改[默认评论排序]((https://github.com/decred/politeiagui/pull/1034))为先显示最高分评论，添加在 URL 中设置排序功能。同时也修复了许多错误。这些更改已在主分支中合并，并将在[测试网页](https://test-proposals.decred.org/)测试后部署在[主提案网页](https://proposals.decred.org/)上。

在代码基础设施方面，承包商管理系统的几个部分在快速开发阶段后进行代码库清理，之后进入主分支。测试覆盖率已从13％[增加](https://github.com/decred/politeia/pull/727)到19％。

一个高级用户可以在投票期结束后投票漏洞被发现。漏洞被发现已有一段时间了，目前正在等待部署修复。在发现有些选票选择晚投票后，修复程序已于3月13日部署。Politeia UI 可能会显示某些提案的投票计数略有错误，但投票结果不受影响。

> 有关 Politeia，最令人放心的是所有数据都是公开的，并且定期时间戳到 Decred 区块链上。这意味着任何人都可以从 github 中提取数据并加密验证在投票期内（+/- 1小时）投出的选票以及在投票期结束后投票的选票。(@lukebp 在 [Politeia Digest 第12期](https://richardred0x.github.io/politeia-digest/issue-012.html))

来自 6-9 位贡献者，总共 40 份提交已在[politeia](https://github.com/decred/politeia/compare/8057ced5e4c0a04823a261cc064602f1a8a2ab1b...13eb0038975ff4fcddb70565687434354d208a0f) 及 [politeiagui](https://github.com/decred/politeiagui/compare/52c775330beb1b77ed817c85bccaaf2a8e199cdc...72885ed6e58c8a2f1bfbd2d039f6cd19b52912fe)合并。

[dcrandroid](https://github.com/decred/dcrandroid): 小错误修复，添加中文翻译，查看交易历史的速度优化。

[dcrios](https://github.com/raedahgroup/dcrios): dcrios beta 已经完成并可以接受更多测试。欢迎测试人员在[TestFlight](https://testflight.apple.com/join/dvq51tCh)中下载 app。目前还存在数个小的错误。在 iPod Touch 设备上有已知并正在修复的排版错误。目前的问题是处理一些批准 Apple Store 账户的手续。一旦完成将立即正式发布客户端。

[dcrdata](https://github.com/decred/dcrdata): 第4版[已发布](https://twitter.com/decredexplorer/status/1110618796975370240)并上线[explorer.dcrdata.org](https://explorer.dcrdata.org/)。

面向用户的变化包括大幅度的重新设计页面样式，更多信息和更好的组织，Politeia提案页面，时间间隔的区块信息，图表的日志和线性缩放，汇率监控和许多小改动。据说，HODL水印也已经消失。对于开发更新，请查看完整的[发布说明](https://github.com/decred/dcrdata/releases/tag/v4.0.0)。

在 3 个月的开发过程中，v4 版本在 11 个贡献者的 325 个提交中获得了惊人的 48K 行添加和19K 行删除。恭喜dcrdata！

> 有些功能和改进已经在酝酿 4.1版本，因此应该相对较快地发布次要版本。4.0范围相当大，但都有充分的理由并且是值得的。([@chappjc](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155305431834229kjptE:decred.org))

进行中: 继续进行负载测试和性能优化，通过 Go 模块改进依赖管理，实时共识[投票跟踪](https://github.com/decred/dcrdata/pull/1125), 更快的[图表](https://github.com/decred/dcrdata/pull/1126), 提案投票[图表](https://github.com/decred/dcrdata/pull/1210) 和 [dcrextdata](https://github.com/raedahgroup/dcrextdata) -  dcrdata的一个组件，用于跟踪区块链中不存在的数据，例如有关交易价格和矿池的信息。

[Ticket splitting](https://github.com/matheusd/dcr-split-ticket-matcher): [已发布](https://github.com/matheusd/dcr-split-ticket-matcher/releases/tag/v0.7.6)的 v0.7.6 优化从 dcrdata 获取未使用输出并添加 macOS 的二进制文件。

[docs](https://github.com/decred/dcrdocs): 全新更详细的[分票 Ticket Splitting](https://docs.decred.org/proof-of-stake/ticket-splitting/)指引,重做并扩展[共识投票规则Consensus Rules Voting](https://docs.decred.org/governance/consensus-rule-voting/consensus-rules-voting/)，[提案指南](https://docs.decred.org/governance/politeia/proposal-guidelines/)更新以包括社区基金资助提案的关键要求。

[decred.org](https://github.com/decred/dcrweb): 更新交易所信息和翻译，[自托管](https://github.com/decred/dcrweb/pull/604)介绍影片以去除对 YouTube 请求。

其他:

* Raedah Group 正在尝试使用 Go 编写 [godcr](https://github.com/raedahgroup/godcr/) - 一个拥有多种用户界面模式的替代钱包客户端。命令行界面，终端，浏览器[nucular](https://github.com/aarzilli/nucular) 和 [Fyne](https://github.com/fyne-io/fyne) 前端 GUI 的工作在进行中。([截屏](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$155329781839253ivNYC:decred.org))。
* Raedah Group 也正在开发 [dcrseedgen](https://github.com/raedahgroup/dcrseedgen) - 一个使用 Go 和 nucular UI 编写的独立 Decred 种子生成器。
* [timestamp.decred.org](https://timestamp.decred.org/)获得了重新设计，文本也被重新编写。
* 新的 [dcrtime_checker](https://github.com/decred/dcrtime/tree/master/cmd/dcrtime_checker)工具可以（不通过 dcrtime）直接验证区块链的锚点。
* 大约一半的选票矿池 （VSP） 已升级到[自托管验证（self-host captcha）](https://github.com/decred/dcrstakepool/issues/279)来保护他们用户的隐私。请在[这里](https://github.com/decred/dcrstakepool/issues/326)追踪状态。

3 月开发活动数据: 分布于 8 个最活跃存储库（repositories) 有 360 个有效 PRs, 497 个主要提交, 46K 行添加 及 34K 行删除。每个存储库中有来自 2-9 位开发者的贡献。

## 人员

欢迎新到来的首次贡献者，代码在 GitHub 上合并：@devwarrior ([atomicswap](https://github.com/decred/atomicswap/commits?author=devwarrior-cool)) 及 DominicTing ([dcrweb](https://github.com/decred/dcrweb/pull/588)).

## 治理

在 3月里，[DCR 基金会](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了 16,288 DCR，并花了 13,595 DCR，使用 DCR 在 3 月份的每日平均美元价格 18.14 美元计算，本月收到 29.6 万 美元以及支出 24.7 万 美元。由于这些付款用于支付 2 月份完成的工作，因此可以用 2 月份的平均价格 16.51 美元计算 - 在这种情况下，美元收到的数字是 26.9 万美元以及支出 22.4 万美元。4月9日 为止，基金会余额为 608,560 DCR (按 25.26 美元计算相当于 153万 美金)。

于 4月10日 的提案状态:

* [Trust 钱包整合提案](https://proposals.decred.org/proposals/2ababdea7da2b3d8312a773d477272135a883ed772ba99cdf31eddb5f261d571) 在 9.3K 投出的票中以 67% Yes 通过。在投票通过前，Trust 钱包开发人员已经[开始了](https://github.com/TrustWallet/wallet-core/issues/43)钱包端的整合。 
* [ATM 整合 - 计划阶段提案](https://proposals.decred.org/proposals/aea224a561cfed183f514a9ac700d68ba8a6c71dfbee71208fb9bff5fffab51d) 在 12.7K 投出的票以 52.5% Yes，未能达到 60% 而不通过。[这里](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15542882616188dHEHP:decred.org)讨论了重新提出投票的讨论
* [非洲（加纳）提案 - Bring decred to Africa(Ghana) Adoption program for merchants and businesses](https://proposals.decred.org/proposals/dac06f18bfeb5f7667e56554774de3bb99151018ce16a64f5353bab45819763b) 由 @georgepro 提出，要求 41,054 美元资助 3 个月的加纳商家采用计划。投票已经开始，并在 4月10日为止达到法定票数以及 95% 的 No 票。 
* 咖啡钱包[提案](https://proposals.decred.org/proposals/45de9806c952c5ffc2fc6782fddbc74c852c26e3fb0e950144b92d75082c4731)在被废弃后重新提交的申请被[拒绝](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$155144086813111EMAcC:decred.org)。管理员认为这是尝试使用Politeia 来推广产品的手段。
* [社区资金开销去中心化提案 - Decentralize Treasury Spending](https://proposals.decred.org/proposals/c96290a2478d0a1916284438ea2c59a1215fe768a87648d04d45f6b7ecb82c3f) 由 @moo31337 提出。提案概述了两步流程，其中支出交易草案在 Politeia 上发布被审查后，由利益相关者在链上投票。预计开发，测试和达成共识的投票需时 9-12 个月，预算为 20-25 万美元。
* [EXMO 交易所的法币交易对集成提案-Fiat pairs integration on EXMO Exchange](https://proposals.decred.org/proposals/950e8149e594b01c010c1199233ab11e82c9da39174ba375d286dc72bb0a54d7) 由 vadymprykhodko 提交。这是续在 r/decred 发布的[预提案](https://www.reddit.com/r/decred/comments/b0y9le/integration_on_exmo_exchange_new_fiat_pairs/)发布的。提案要求 23，8000 美元以支持在一个东欧地区受欢迎的交易所 EXMO 增加 Decred 的法币交易对。
* [修订 Decred 宪法提案 - Amendment to Decred Constitution](https://proposals.decred.org/proposals/fd56bb79e0383f40fc2d92f4473634c59f1aa0abda7aabe29079216202c83114) 由 @richardred 提交。这是随着一连串的讨论后提交的。[这里](https://github.com/xaur/decred-issues/issues/107)追踪讨论内容。

预提案:

* [印度教育和宣传活动提案 - India education and awareness campaign](https://www.reddit.com/r/decred/comments/awb5y0/preproposal_decred_india_community_new_user/) 由 u/Blocknext 提出。在聊天室[讨论](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15515162772723165JzrFj:matrix.org)中，有用户指出在 Dash 的提案系统里也有个[类似的提案](https://www.dash.org/forum/threads/building-commercial-dash-use-in-the-freelancing-industry-across-south-asia.17890/)。
* [第二次宪法修正提案 - Second constitutional amendment](https://www.reddit.com/r/decred/comments/b84t6b/preproposal_second_constitutional_amendment_to/) 由 @richardred 提出，宣布 2月8日 为国际 Stakey 日。

decredcommunity.org 受到了一些[批评](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$155227203622209rOKeX:decred.org)表示该网站并不开源而且在提案内容里面没有明确说明。其中一个论点是社区基金从未资助过任何非开源工作内容，除了一些不能公开的整合工作外。同时资助非开源软件也违背项目[宪法](https://docs.decred.org/governance/decred-constitution/)。讨论内容记录在[这里](https://github.com/karamble/dcrcommunityweb/issues/1)，这些讨论同时也激发了一些提案指南的[改进](https://github.com/decred/dcrdocs/pull/896)，列明任何成果的任何限制。

@richardred 发布了一项[分析](https://github.com/RichardRed0x/pi-research/blob/master/analysis/voting/early-voting-influence.md)，探讨早期投票在什么程度上会影响晚期投票者的行为，和这种影响是否会改变投票结果。

更多细节，分析与评论请参考 @richardred 的 Politeia 简报[第 12 期](https://richardred0x.github.io/politeia-digest/issue-012.html) 和 [第 13 期](https://richardred0x.github.io/politeia-digest/issue-013.html)。

要获得有关 Politeia 提案活动的通知，请在您的 Politeia 个人资料中启用电子邮件通知，或在推特上关注 [@pi_crumbs](https://twitter.com/pi_crumbs) 和 [@slices_of_pi](https://twitter.com/slices_of_pi)。

其他讨论:

* [社区基金开销速度](https://www.reddit.com/r/decred/comments/b5vlrl/we_have_spent_23_of_decred_treasury_should_we_be/)和资金的分配。
* 有关[财政报告](https://www.reddit.com/r/decred/comments/b2zopq/simple_financial_reporting/)格式的主意.
* 对于推自己的评论问题再次被提出并达成共识决定禁用该选项。相关[讨论](https://github.com/decred/politeiagui/issues/845)记录了该课题的所有讨论。
* @richardred 提议将法定票数存粹基于[Yes 票](https://github.com/decred/politeia/issues/729)的比例。(目前 Yes+No 选票都被计算)。他也制作了一个[模拟](https://github.com/RichardRed0x/pi-research/blob/master/analysis/voting/quorum-change-examples.md)视化不同的法定票数计算方法场景。

## 网络

算力: 3 月算力在低点 221 Ph/s 及新高 570 Ph/s 浮动。在 3 月份上半月分算力维持 320 Ph/s 左右，但在月底时升高超过了 400 Ph/s。 在 4 月 1 日 根据 [dcrstats.com](https://dcrstats.com/pow) 数据显示，矿池算力分布为：F2Pool 23%, Poolin 20%, lab.antpool.com 16%, BTC.com 12%, UUPool 11%, Luxor 3.2%, CoinMine 0.4% 及其他 14%。矿池分布数据为大约值无法精确计算。

投票: 按 4月1日 dcrstats.com（数据显示）, 30日 平均票价为 112.3 DCR (+0.6)。价格在 108.6 DCR 至 117.9 DCR之间浮动。锁仓数额为 4.47-4.61 百万 DCR, 大约为总流通量的 46.9-48.6%。

节点: 截止于 4月1日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 191 public listening Node 及 336 Normal Node。版本分布: v1.5.0 dev builds: 6.3% (-2.3%), v1.4.0: 55% (+12%), v1.4.0 dev and rc builds: 5% (-2%), v1.3.0: 17% (-6%), v1.2.0: 9.5% (-0.5%), v1.1.2: 4%, v1.1.0: 1.7% (-0.3%)。

## 挖矿

* [dcrstats](https://dcrstats.com/pow)显示新矿池: 蚂蚁矿池[lab.antpool.com](http://lab.antpool.com/)
* OKEx 中文[页面](https://support.okex.com/hc/zh-cn/articles/360024177931-%E6%94%AF%E6%8C%81%E5%B8%81%E7%A7%8D)显示 OKEx 已增加支持 Decred 的新矿池。
* Scott Offord 在推特上[公布](https://twitter.com/offordscott/status/1111714556529831936) MicroBT 将以 750 美元售卖最后 200 台 D1矿机并之后不打算推出新的 Decred矿机。

## 落地应用

OKCoin [公布](https://twitter.com/OKCoin/status/1105892924586258434) 上线 DCR/BTC，DCR/ETH 及 DCR/USD 交易对。这为 DCR 增加了另一个法币渠道。该消息是在三藩市联合筹办的[活动](https://www.eventbrite.com/e/decred-okcoin-present-the-next-10-years-crypto-boom-bust-or-buidl-tickets-57549671617)后发布的。

[CoinText](https://cointext.io/) 已[支持 DCR](https://twitter.com/vinarmani/status/1111034078847995905)。该服务将允许用户发送 DCR 至任何美国及加拿大手机号。请了解该服务如何运作并注意只发送小额 DCR。

## 外联活动

3月份是 Decred-Ditto 关系历史上最成功的月份之一。从帮助在旧金山 OKCoin 办公室组织非常成功的活动，到登上“华尔街日报”的专题文章，Ditto 和 Decred 在宣传方面都取得了一些重大成果。 Ditto 收到了许多其他加密货币公司和爱好者的信息，祝贺华尔街日报并赞扬他们举办了一场成功的活动。

Ditto's 三月份成就:

* 通过协调与Jake Yocom-Piatt 和 Placeholder VC，Chris Burniske 的多个访问，在华尔街日报中发布了一篇关于 Decred 的[专题文章](https://www.wsj.com/articles/gerons-take-decred-aims-to-reach-cryptos-decentralized-ideals-11552523191)。这篇文章比迄今为止的媒体报道都更有效地针对广泛，非加密货币圈子，主流的金融决策者观众描述了 Decred。 - 这显着提高了 Decred 在加密货币圈外的知名度和可信度。全文[请参阅](https://www.reddit.com/r/decred/comments/b12z34/gerons_take_decred_aims_to_reach_cryptos/eiiwnpm/), 并在[这里](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155268940829940XRdUb:decred.org)查阅有趣的事件发展经过。

* 在 The Block 知名媒体中发布了一篇深度[技术简介](https://www.theblockcrypto.com/2019/03/20/decred-an-experiment-in-on-chain-governance/)。纯文字版[请查阅这里](https://pastebin.com/Dg2ELYat).
* 促成了 5 个访问: 与Laura Shin (the host of the Unchained/Unconfirmed podcasts) 的背景访问, 与 CryptoBriefing 分析员用于一篇深度研究报告的 2 个访问，一个与 The Block 并成功打造有效深度推广 Decred 的访问，以及跟华尔街日报成功登上专题文章的访问。
* 协助举办 OKCoin-Decred 的上线活动。
* 参与了旧金山第一个 Decred meetup。感谢团队成功组织这个60多人出席的活动。
* 为Decred Assembly 视频提供格式和内容创意。
* 起草一份关于选票如何运作的高级消息（待定）。
* 在 investinblockchain.com 上为社区基金起草了一份文章并在四月份成功[发布](https://www.investinblockchain.com/put-your-money-where-your-mouth-is-decreds-treasury-proposal-closer-true-dae/)

有关更多细节，请参阅 Ditto 于 [3月1日](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155148239113862OPjOD:decred.org), [3月15日](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155268940829940XRdUb:decred.org) 及 [3月29日](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$1553889088955UNmaG:decred.org)发布的双周更新。

讨论:

* [重新探讨](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$155298850932396heGyM:decred.org)给予“decentralized credits” 更多关注的[老想法](https://github.com/decred/dcrweb/issues/66)。
* 有关 Decred 是否需要一个更具体的术语，而不是 “skin in the game”[被讨论](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$155309851735051wGBlh:decred.org)，这是一个模糊和许多加密货币项目使用的陈述。放弃流动性以换取参与治理权的决定需要一个更有意义的术语，以反映 Decred 与其他项目之间的差异。这个概念及其他提议的概念名词在[这个 issue](https://github.com/xaur/decred-issues/issues/65)中被记录。

## 社区活动

已出席:

* [首个旧金山 Decred Meetup](https://www.meetup.com/San-Francisco-Decred-Meetup/events/259126130/) 美国旧金山。 @max_bronstein [分享](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155198454119792Tdajl:decred.org)到: "活动非常成功！活动出席率很高，超过 50 人出席并且群众很活跃。Chris 对网络的发展给了很好的概述，并提到了 HAS 框架 - （高安全性，适应性强的代码，和可持续性的资助模式（hypersecure, adaptable code, and sustainable funding model）。([照片](https://twitter.com/danzuller/status/1103504733023555584))
* [Decred and Decentralized Governance](https://www.meetup.com/decredpdx/events/259229063/) 美国波特兰。 @Eli 和 @oregonisaac [表示](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$1552437600641341ZEHPe:matrix.org): "虽然灯光不太好，但是出席率很好！我们有 14 位热情的出席者参与 Isaac 关于 Decred 及 去中心化治理的演讲。我们一直讨论到包间关上，酒吧关门并在外面继续讨论。参与者包括了波特兰加密货币社区及社区成员/贡献者。我们很惊讶在meetup结束后延续到晚上 10 点的讨论（原定计划 meetup 8点结束([照片](https://twitter.com/DecredPdx/status/1106279797619998721))
* [Just HODL It @ SXSW 2019](https://www.eventbrite.com/e/just-hodl-it-sxsw-2019-with-dblitz-2nd-annual-bitcoin-event-tickets-56351957221) 美国奥斯汀。 @moo31337 代表 Decred 出席。
* [The Next 10 Years: Crypto Boom, Bust, or Buidl?](https://www.eventbrite.com/e/decred-okcoin-present-the-next-10-years-crypto-boom-bust-or-buidl-tickets-57549671617) 由 Decred 和 OKCoin 在美国旧金山举办。如 @liz\_bagot [报导](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155268940829940XRdUb:decred.org), "该活动非常成功 - 大约 110 人出席，包括很多的 VC 和加密货币公司 CEO。Ditto 接收到很多赞赏，而且很多人在活动结束后留下交流更现实该活动质量很高。来自 Placeholder VC 的 Chris Burniske 和 Alex Evans，还有 Jake 在该活动演讲并吸引了很多的群众。“([照片](https://twitter.com/liz_bagot/status/1105693679426007042))
* [Restoring Trust through Blockchain Governance](https://www.meetup.com/Decred-GTA/events/259126224/) 加拿大多伦多。 ([照片](https://twitter.com/Decred_CA/status/1107304663626457089))
* 澳洲墨尔本的 Swinburne 科技大学演讲。@eSizeDave 和 @Zohand 向金融科技课程的研究所学生介绍加密货币。观众对于演讲有关法币的事实感到惊讶，之后演讲简要的介绍了比特币然后介绍 Decred 的 PoW/PoS 混合共识机制，治理，Politeia，项目发展及路线图。完整报告查阅[这里](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15539115821116YDOQM:decred.org). ([照片](https://twitter.com/DecredAustralia/status/1109430422717399040))
* [Crypto Conference 2019](https://crypto-conference.com/) 德国柏林。该活动是[柏林区块链周](https://www.berlin-blockchain-week.com/)的一部分。@karamble 介绍 "数字货币的适应性 Adaptability in Digital Currencies". (照片: [1](https://twitter.com/karamblez/status/1111312069251530752), [2](https://twitter.com/karamblez/status/1111333206110932992))
* 中国青岛 海创链 HCHchain Accelerator 的演说。@Dominic 介绍了 "什么是Decred?" 并 "展示了 Decred 中国社区的活力。活动中也收到了许多有趣的提问, 例如目前在微信上讨论的将投票权委托给VSP可能会如何影响链上投票结果。([照片](https://twitter.com/wanbihou/status/1112264821989236736))

即将到来的:

* [Coordinating Open Source: Today and Tomorrow](https://www.meetup.com/San-Francisco-Decred-Meetup/events/260046546/) 美国旧金山，4月18日。该活动将在 Coinbase 总部，与 Coinbase 托管服务联合举办。@lukebp 将介绍 Decred 独特的治理及资助模式。介绍过后也将会有个关于不同的资助模式的讨论。
* [Crypto Governance - It is a matter of survival](https://www.meetup.com/BlockchainMelbourne/events/260266298/) 澳大利亚墨尔本，4月18日。该活动将会有个关于治理的小组讨论，及Politeia 的演示。活动由 Apollo Capital 和 Decred 合办。
* [Jalisco Talent Land](https://www.talent-land.mx/#entradas) 墨西哥瓜达拉哈拉，4月22-26日。细节可联系@elian
* [Blockchain Summit](http://blockchainsummit.ma/) 摩洛哥拉巴特，4月24日。 @arij (Slack 用户@butterfly) 将介绍 Decred。
* 德国柏林的 Decred Meetup， 5月5日。@jholdstock 将介绍 Decred 概述，而 BlueYard 的 Philipp Banhardt 将讨论他们的投资论文。由 BlueYard Capital 举办。
* 美国纽约区块链周 NYC Blockchain Week，5月11-16日。7 位社区成员组成的团队将在各地点出席活动。
* [Criptolatinfest](https://criptolatinfest.com/) 哥伦比亚波哥大，5月18日。Decred 将有个演讲机会。

## 媒体

社区活动:

* @Denni Lovejoy 积极参与 #writers\_room 讨论为通过的钱包教程[提案](https://proposals.decred.org/proposals/a3def199af812b796887f4eae22e11e45f112b50c2e17252c60ed190933ec14f)的视频制作准确的脚本。
* @anshawblack 将在 5 月前往纽约与多位录制播客。
* Decred 月报现已[复制](https://decredcommunity.org/filter?tag=Decred%20Journal&key=category)到 decredcommunity.org。注意角落漂亮的国家旗帜按键转换翻译语言。
* @max\_bronstein 整合了 [Decred Canon](https://github.com/maxbron08/Decred-Canon) - 一系列帮助人们熟悉 Decred 项目的阅读材料和资源。
* 由 stakey.club 的 @mm 发布的新文章: 与多个设备[分享 dcrd](https://stakey.club/en/sharing-the-dcrd/), [Decred Verifier](https://stakey.club/en/decred-verifier/) 检测哈希及签名的脚本。

部分文章:

* How Close to Absolute Decentralization is Decred's Unique Consensus Mechanism? by Trevor Holman ([cryptonewsz.com](https://www.cryptonewsz.com/how-close-to-absolute-decentralization-is-decreds-unique-consensus-mechanism/8998/), _missed in Feb issue_)
* The best on-chain governance system by @Haon ([medium](https://medium.com/@NoahPierau/the-best-on-chain-governance-system-67759bf25335), _missed in Feb issue_)
* Decred: Deep Dive Report by Smith + Crown ([smithandcrown.com](https://www.smithandcrown.com/decred-deep-dive-report/), 19-page research report)
* The Cryptocurrency Industry Has a Forking Problem! Can On-Chain Governance Help Solve It? by Florian Gheorghe ([beincrypto.com](https://beincrypto.com/the-cryptocurrency-industry-has-a-forking-problem-can-on-chain-governance-help-solve-it/))
* Decred Aims to Reach Crypto's Decentralized Ideals by Tomio Geron ([wsj.com](https://www.wsj.com/articles/gerons-take-decred-aims-to-reach-cryptos-decentralized-ideals-11552523191), paywall, sharing far and wide recommended to amplify impact)
* Decred, an experiment in on-chain governance by Steven Zheng ([theblockcrypto.com](https://www.theblockcrypto.com/2019/03/20/decred-an-experiment-in-on-chain-governance/), paywall)
* Hybrid PoW/PoS Consensus Explained by @richardred ([binance.vision](https://www.binance.vision/blockchain/hybrid-pow-pos-consensus-explained))
* Decred's "Skin-in-the-Game" Governance Experiment by Jeremy Epstein ([neverstopmarketing.com](https://www.neverstopmarketing.com/decred-and-democracy/) _thanks for the kind words!_)
* More Exchanges, More Access: Decred Grows Availability & Liquidity by @Dustorf ([medium](https://medium.com/decred/more-exchanges-more-access-decred-grows-availability-liquidity-95accbbf6835))
* Decred Overview by Casey Caruso ([medium](https://medium.com/@caseycaruso/decred-dcr-1c809eb8bc5d))
* How I pitch Decred in Africa by @George Pro ([medium](https://medium.com/@aappiahpro1/how-i-pitch-decred-in-africa-62b9ee8da7e1))

New info leaked about c0:

> Haon: https://crypto.bi/tape/blog/dcr/ - "The founders of decred originally worked on the development of Bitcoin in a project called biscuits."  
> jy-p: working on biscuits for a while gave us the perspective we needed to start decred. our second project, fried chicken, is what led us to create our own louisiana kitchen

A few more gems were found on [Crunchbase](https://www.crunchbase.com/organization/decred): Decred is a "Private", "For Profit" company, "uses 8 technology products and services including PHP, nginx, and Google Drive", and "is actively using 24 technologies for its website. These include Viewport Meta, IPhone / Mobile Compatible, and SSL by Default". Finally, the team includes _two_ Jacob Yocom-Piatt, which somewhat explains the amount of foresight behind the project.

翻译:

* Decred: Where did it all begin? [in Dutch](https://github.com/Arriu/Decred/blob/master/translations/wherediditallbegin_dutch.md) by @jazzah
* Detailed analysis of Decred fork resistance [in Dutch](https://decredcommunity.org/nl/blog/detailed-analysis-of-decred-fork-resistance) by @jazzah
* Decred Journal January and February issues were [translated](https://xaur.github.io/decred-news/) to - hold your breath: Arabic by @arij (victorious after long fight with right-to-left issues), Chinese by @guang, Polish by @kozel, Russian by @DZ, Spanish by @elian and Vietnamese by Duyên Em. Thank you so much for spreading the word!
* Translators, note that there is an index of translated articles [here](https://github.com/artikozel/decred-translations/blob/master/article_index.md). Reach out in [#writers_room](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) or via pull request to add your translations.

音频:

* Did You Know Crypto - Episode 26: On Decred. @moo31337 talks about his background, what is Decred, its hybrid consensus, stability, proposal system and the DEX. ([didyouknowcrypto.com](http://didyouknowcrypto.com/ep26/))
* The Blockcrunch - How Does Decred's Governance Work? Part 1 of interview with @Haon talks about Decred's governance, stakeholder rewards, voting topics and why both miners and voters are needed. ([libsyn.com](https://blockcrunch.libsyn.com/how-does-decreds-governance-work-noah-pierau-decred-project), [itunes](https://itunes.apple.com/us/podcast/how-does-decreds-governance-work-noah-pierau-decred-part-1/id1350649166?i=1000431532255&mt=2), [spotify](https://open.spotify.com/episode/7xST0eTxy4xnaK6NILXcbx?si=o3AJJuLvQka7lnpT1BrzWw))
* The Blockcrunch - Defending Decred's Onchain Governance. Part 2 of interview with @Haon continues about enforceability of on-chain votes, stake-based vs entity-based voting, fairness and centralization in PoS and threat of malicious actors. ([libsyn.com](https://blockcrunch.libsyn.com/defending-decred-noah-pierau-decred-part-2))

CoinMarketCap [开始显示](https://medium.com/@davebalter/coinmarketcap-partners-with-flipside-crypto-to-distribute-project-health-scores-f181374f3d0e)加密资产的新指标 FCAS 等级。Fundamental Crypto Asset Score （FCAS）是由 Flipside Crypto 自 2017 年初开始追踪并对于超过450个项目的评级。在[这里](https://www.flipsidecrypto.com/fcas-explained)的解释说明系统的目标是通过尽量无视价格浮动而专注于客户活动及开发者行为，来回答 “这个加密项目是否可以推出人们要用的产品，和人们是否正在使用它？”。于 4月9日位置 Decred [被评级](https://coinmarketcap.com/currencies/decred/#ratings) 为 "A" 778/1000。一些背景数据：Litecoin 752, Zcash 792, Bitcoin 862, EOS 910, Ethereum 914.

## 社区

截止于 4月1日 的社区数据 :

* Twitter 关注量: 40,309 (+512)
* Reddit 关注用户: 9,405 (+40)
* Matrix 用户: 284 (+18)
* Slack 用户: 6,639 (+58)
* Discord 用户: 2,124 (+23), 发帖数: 161 (+30)
* Telegram 用户: 4,042 (-23)
* YouTube 关注量: 3,764 (+18)
* Facebook 关注: 3,165 (+24), likes: 2,906 (+10)
* LinkedIn 关注: Decred page 495 (+12), Politeia page 29 (+0)
* GitHub dcrd : 479 (+5), fork: 1,257 (+20)

社交系统新闻：

* Stakey 表情包已在 Riot 网页版，安卓版及iOS Matrix客户端[上线](https://twitter.com/dcrstakey/status/1104032806513115136)。感谢 @lustosa 和 Matrix 团队! 表情包的激动测试完全[瘫痪了](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155205491220668sKKGI:decred.org) #general频道。已知问题：Matrix表情包不会桥接到 Slack 和 Discord。@jrick 提示到: 这些表情包是在 Matrix 所有频道，即便与Decred无关都可以使用。请明智的使用。
* 桥接已关闭信息修改。如果您在Discord 或 电报修改信息，修改的信息将不会转送到 Matrix（不会生成重复信息）
* 正在关闭桥接软件([matterbridge](https://github.com/42wim/matterbridge))的信息修改选项后 Right after disabling message edits in our bridge software , an untested code path was hit that took down the bridge for a few hours. @dhill quickly located the bug and submitted a pull request.
* 新的[#101](https://matrix.to/#/!MiucsxxSPQBpoidaHN:decred.org)聊天室是为了帮助新手和解决简单问题而创建。该聊天室已桥接到 Slack，Discord 和 电报。由于电报群的广告很多，桥接到电报群是少见的。之前的 #telegram 聊天室就是因为太多广告并缺乏管理而被终止桥接的。
* Telegram 防护: @Aztec 团队将机器人"slapper bots" 升级，会基于低质量内容剔除用户或机器人，并增加机器人 "shield bot" 以对新用户进行验证。
* 中文社区成员成功入驻[链节点](https://www.chainnode.com/forum/305)，链节点为巴比特论坛 8btc.com 的升级版，为最大的中文加密货币社区之一

部分 Reddit 讨论: "Skepticism Sunday" 帖 - [Mar 3](https://www.reddit.com/r/decred/comments/awv5yt/skepticism_sunday_march_3_2019/) 及 [Mar 24](https://www.reddit.com/r/decred/comments/b4xx9h/skepticism_sunday_march_24_2019/); 多少人愿意以[in DCR](https://www.reddit.com/r/decred/comments/axdfvd/how_many_of_you_would_want_part_of_your_paycheck/)接收工资; 关于[使用 Kialo](https://www.reddit.com/r/decred/comments/axyxw2/should_the_decred_network_utilize_kialo_as/) 作为环绕着做决定更系统性沟通的工具; 提议在 Politeia 上增加[民意调查](https://www.reddit.com/r/decred/comments/b5smyl/testing_the_waters_with_this_idea_maybe/)功能。



## 市场

在 3月中 DCR 交易价格为 美金 15.93-23.26 / BTC 0.00414-0.00596。平均日汇率为 18.14 美元。

## 相关外部信息

GitHub is [updating](https://github.blog/2019-03-14-githubs-site-policy-updates-are-ready-for-your-feedback/) their policy. New drafts were published for feedback till Apr 12 and will come into effect Apr 19. Among the changes is commitment to react to [Do Not Track](https://en.wikipedia.org/wiki/Do_Not_Track), sharing user data with [more](https://github.com/github/site-policy/pull/154) 3rd party processors and updated use of third party user trackers. The change to clarify influence of U.S. sanctions triggered a question how this might impact Decred contributors - if you know, please comment in [this issue](https://github.com/xaur/decred-issues/issues/125) or [on Reddit](https://old.reddit.com/r/decred/comments/b2xsw3/github_terms_update_has_more_sanctions_stuff/). Some changes might be unpleasant but are pretty common for most companies and give us a good moment to reflect on our beliefs about free stuff. Also, unlike most companies, GitHub has all their policy documents versioned transparently in a Git repo that anybody can clone and inspect. The idea to have a similar repository for Decred was discussed a few times and there is a concept sandbox [repository](https://github.com/RichardRed0x/governance-docs) showing how it might look like.

Stellar (XLM) [experienced](https://messari.io/article/messari-research-stellar-suffered-and-quietly-patched-a-2-2-billion-xlm-inflation-bug-in-2017) an inflation bug which was exploited to print 2.25 billion XLM (worth $10 million at the time, and nearly 25% of the circulating supply) in April 2017. This bug was lightly reported at the time, it was fixed by the Stellar Development Foundation (SDF) who burned an equal amount from its community reserve to offset the unintended inflation. That the SDF could identify, fix and mitigate such a major exploit so quietly says something about how decentralized Stellar is.

PIVX experienced an inflation bug which was [exploited](https://medium.com/@dev.pivx/report-wrapped-serials-attack-5f4bf7b51701) in March. The bug concerned the network's zerocoin protocol (zPIV), and allowed an attacker to fake serial numbers and spend zerocoins that had never been minted. Over the course of five days, transactions creating and spending 568,897 PIV (~$438,000) were made before the exploit was identified and zPIV transactions were disabled (until it could be fixed). Besides regular takeaways like "consensus code is hard" and "cryptography is hard", this case has more food for thought. First, zerocoin functionality was disabled immediately after the exploit was discovered using one of the "sporks". Someone with the keys for these sporks can affect the whole network. Second, the bug was spotted because some nodes were [switching away](https://github.com/PIVX-Project/PIVX/pull/681) from OpenSSL that let the bug go unnoticed (OpenSSL is long [famous](https://www.peereboom.us/assl/assl/html/openssl.html) for its quality). While those nodes were not full alternative implementations, it still shows how a mismatch between diverse software helps to discover bugs. Third, it is possible to know exactly how many coins were minted because PIVX's zerocoin protocol allows supply to be [auditable](https://zcoin.io/zcoins-privacy-technology-compares-competition/), unlike some other privacy protocols.

Ethereum is actively discussing a dev fund funded from block rewards. Kickstarted by Gitcoin co-founder, [ERC 1789](https://github.com/ethereum/EIPs/issues/1789) (continued as [EIP 1890](https://github.com/ethereum/EIPs/pull/1890)) provides an overview of funding models employed by open source and [makes a case](https://medium.com/gitcoin/funding-open-source-in-the-blockchain-era-8ded753bf05f) for inflation funding for protocol maintenance. A supplementary GitHub project was organized with a collection of [documents](https://github.com/ethereum-funding/docs) and more than 50 [issues](https://github.com/ethereum-funding/blockrewardsfunding/issues).

Monero's new [Community Crowdfunding System](https://ccs.getmonero.org/) was [launched](https://www.reddit.com/r/Monero/comments/ay0j5n/the_new_ffs_is_complete_please_use_and_explore_it/), and a number of projects were funded.

Dash held an [election](https://blog.dash.org/announcing-the-dash-dao-irrevocable-trust-election-results-bfe134c113b0) for Trust Protectors, people who will oversee the operation of a legal trust that has been [set up](https://blog.dash.org/dash-network-elected-trust-protectors-closing-the-governance-loop-4f07b46da03e) to own and control Dash Core Group.

Dash also [finished](https://blog.dash.org/deterministic-masternode-list-and-automatic-instantsend-now-live-f2028d833388) the deployment of the Deterministic Masternode List, enabling automatic instant payments for transactions with fewer than 4 inputs.

Dash Core Group further [tightened](https://www.theblockcrypto.com/2019/03/04/corporation-behind-dash-lays-off-senior-staff-as-bear-market-grip-tightens/) its budget with layoffs and salary freezes.

Tezos [concluded](https://www.coindesk.com/welcome-to-athens-tezos-completes-historic-first-blockchain-vote) the first round of voting for its Athens upgrade. In this round bakers were choosing from between two versions of the Athens upgrade which increases the gas limit, and they chose the Athens A version which also decreases the minimum roll size and lowers the barrier to entry for bakers. The process has now moved on to its next phase, where bakers must confirm that the selected proposal should proceed to a subsequent testing and confirmation phase.

Grin developers [voted](https://www.coindesk.com/privacy-cryptocurrency-grin-votes-to-fund-third-full-time-developer) to fund 3rd full time developer in a weekly [governance meeting](https://github.com/mimblewimble/grin-pm/blob/master/notes/20190312-meeting-governance.md). An interesting aspect of Grin is their efforts towards reporting and transparency: multiple versioned documents are published on GitHub, including [decision log](https://github.com/mimblewimble/grin-pm/blob/master/decision_log.md), [meeting notes](https://github.com/mimblewimble/grin-pm/tree/master/notes), income and [expenses](https://github.com/mimblewimble/grin-pm/tree/master/financials).

Poloniex [committed](https://medium.com/circle-blog/poloniex-welcomes-grin-commits-to-share-transaction-fees-for-1-year-d07bc92cc0f8) to share a portion of Grin trading fees with [Grin General Fund](https://grin-tech.org/general_funding). 50% of all fees will be donated during the first month, and 25% for the next 11 months. Pretty rare and generous act in the space.

Jack Dorsey [announced](https://www.coindesk.com/square-hiring-crypto-engineers-bitcoin) Square is looking to fund engineers and a designer to work full-time on Bitcoin and cryptocurrency ecosystem, as a way to give back to the community. One [response](https://twitter.com/MartyBent/status/1108494280484630528) noted that "dev fund" embedded in a protocol is not needed because network participants have enough incentives to fund their infrastructure. In Decred's case, if the Treasury is ever deemed no longer necessary, it is within stakeholders' power to repurpose it for investing into a wider crypto/open source/open hardware ecosystem, or disband it entirely.

Investigation of QuadrigaCX by Ernst & Young [found](https://cointelegraph.com/news/report-quadrigacx-wallets-have-been-empty-unused-since-april) that exchange's cold wallets were empty and unused since April 2018. Kraken [offered](https://blog.kraken.com/post/2155/were-offering-a-100000-reward-for-discovery-of-quadriga-coins/) a $100K reward for tips that lead to the discovery of the missing $190 million.

New research from @BitwiseInvest [suggests](https://twitter.com/BitwiseInvest/status/1109114656944209921) 95% of reported BTC spot volume is fake, but also notes much good news about the crypto ecosystem.

IMF found an [elegant solution](https://blogs.imf.org/2019/02/05/cashing-in-how-to-make-negative-interest-rates-work/) to make negative interest rates work as a counter-measure to a possible future crisis. A negative interest rate of -3% would mean you deposit $100 to a bank and withdraw $97 a year later. Such rates are currently hard to enforce because people would just withdraw to cash. The "straightforward" solution would be to move into a happy "cashless world" where the bank can set arbitrary negative rates and you simply can't withdraw to cash to save your value from melting. This is expected to "make consumption and investment more attractive, ... jolt lending, boost demand, and stimulate the economy". But getting rid of cash is not easy and is years away. So another solution to sustain a negative interest rate that is easier to roll today is to split a fiat currency into e-money and cash and introduce a floating conversion rate between them. This way, in a -3% interest rate scenario, you either deposit 100 cash dollars into e-dollars and get 97 e-dollars in a year, or hold cash and enjoy a 3% value loss against both goods and the e-dollar. In such a system there is no benefit to hold cash relative to bank deposits. Hasu and Su Zhu argue that crypto can [serve as a hedge](https://uncommoncore.co/bitcoin-is-a-hedge-against-the-cashless-society/) against the cashless society. Disclaimer: this paragraph is written by a layman. Economists are welcome to [comment](https://www.reddit.com/r/decred/) how this is healthy at all.

[Coinbase Custody](https://custody.coinbase.com/) [enabled](https://twitter.com/CoinbaseCustody) deposits and withdrawals for ZIL, KNC, ZEC, XTZ and [claim](https://blog.coinbase.com/coinbase-custody-launches-staking-support-for-tezos-makerdao-governance-to-follow-68f7bc51bc53) to hold $600 million for 60 clients. The service offers regulated, insured and full offline custodial storage of crypto. The plan is to allow clients to fully participate in crypto networks besides just holding: Tezos baking (staking) is already implemented while voting in Tezos and MakerDAO is planned for Q2 2019.

Coinbase received a [backlash](https://www.coindesk.com/bitcoin-delete-coinbase-neutrino-crypto) from users who deleted their accounts to protest the acquisition of Neutrino, a blockchain analysis startup. The users were upset because Neutrino's executives previously worked for Hacking Team, which sold spyware to governments to aid surveillance and crackdown on journalists and critics. By coincidence, several user faced [difficulties](https://www.reddit.com/r/Bitcoin/comments/avw5uu/unable_to_close_coinbase_account/) closing their accounts. The Block [reported](https://www.theblockcrypto.com/2019/02/26/coinbase-responds-to-its-controversial-acquisition-of-blockchain-intelligence-platform-neutrino/) that Coinbase knew about Neutrino's background but still decided to proceed with the acquisition. A week later Coinbase CEO Brian Armstrong called it a "gap in our diligence process" and [announced](https://blog.coinbase.com/living-up-to-our-values-and-the-neutrino-acquisition-ba98174cdcf6) that people who worked at Hacking Team will transition out of Coinbase.

The problem Coinbase tried to solve with that acquisition was their KYC contractors "selling client data", as [slipped](https://news.bitcoin.com/coinbase-severs-ties-with-hacking-team-members-while-data-sharing-backlash-intensifies/) in one interview. Many exchanges don't verify ID directly but instead hand it to 3rd parties, who may in turn hand it to more 3rd parties, and so on so it quickly gets [out of control](https://twitter.com/NickSzabo4/status/1102353760276275206). Per another [report](https://bitcoinmagazine.com/articles/coinbase-bought-neutrino-because-its-old-analysis-providers-sold-user-data/) there was not much choice for Coinbase due to another problem - many such firms moved to a 'give-get' data model, where Coinbase would only be permitted to use the service in return for providing its own data. Besides spreading to an unknown set of entities, another risk is that enormous amount of interlinked personal data may concentrate in a single place that will become an attractive target. For example, [Jumio](https://en.wikipedia.org/wiki/Jumio)'s Netverify is [used](https://cybersecurity-excellence-awards.com/candidates/netverify) by 5 of the top 10 exchanges including Coinbase, Bittrex and Bitstamp, and an increasing number of ICO issuers.

New Android malware was [detected](https://www.group-ib.com/media/gustuff/) that targets more than 100 global banking apps including 32 cryptocurrency apps such as Bitcoin Wallet, BitPay, Cryptopay, Coinbase and others. Another [report](https://securelist.com/cryptocurrency-businesses-still-being-targeted-by-lazarus/90019/) about an old crypto hacking group recommends Windows and macOS users to be more cautious when dealing with new 3rd parties, installing software, and to never 'Enable Content' (macro scripting) in Microsoft Office documents received from new or untrusted sources.

Beta of Neutrino wallet for Bitcoin Cash was [released](https://news.bitcoin.com/bitcoin-cash-developers-launch-privacy-preserving-light-client-neutrino/) for Android. It uses the same SPV tech as Decred to connect wallets directly to the nodes without intermediaries. Decred and [gcash](https://github.com/gcash) project have common code which makes an opportunity for code reuse and collaboration - see [December](201812.md) issue for more coverage.

## 公告: Decred 月报要休息啦

12 期标志着一整年的 Decred 月报展示了 Decred 精神，深度和社区的参与。

本人（@bee) 已在生活上和 Decred 里累积了很多我个人想完成的事情，而且我也需要休息一下。因此，未来月报还会不会发布仍然不确定。但是我将继续在 Matrix 中，尽力帮助任何愿意继续制作 Decred 月报的人。有兴趣的请加入[#writers_room](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org)。 

在此感谢所有读者和贡献者！ 

## 关于月报
三月为英文第12期 [GitHub](https://xaur.github.io/decred-news/journal/201903) 月报。点击[这里](https://xaur.github.io/decred-news/)浏览所有往期月报，翻译等。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues) 和 [Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

感谢 (按字母排序): bee, davecgh, degeri, Dustorf, guang, jholdstock, liz\_bagot, raedah, richardred, saender, sambiohazard.

## 中文社区

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

感谢 (按字母排序):
