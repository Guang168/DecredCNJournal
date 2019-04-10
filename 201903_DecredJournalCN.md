# Decred月报 - 3月

![](img/)


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

[Politeia](https://github.com/decred/politeia): Added tab to [preview](https://github.com/decred/politeiagui/pull/1018) proposal text, completed feature to [view difference](https://github.com/decred/politeiagui/pull/1004) between proposal versions, changed [default comment sort]((https://github.com/decred/politeiagui/pull/1034)) to show comments with highest score on Top, added feature to set sort in the URL. Many bugs were fixed. These changes were merged in the master branch and will be deployed on the [main proposals site](https://proposals.decred.org/) after some testing on the [test site](https://test-proposals.decred.org/).

In terms of code infrastructure, several parts of contractor management system landed in master, completed several steps of refactoring to fix accumulated layer violations and better support contractor management system, test coverage [increased](https://github.com/decred/politeia/pull/727) from 13% to 19%.

A bug was detected that allowed advanced users to cast votes beyond the end of the voting period. It was known for some time and the fix was awaiting deployment. Upon learning that late votes were occurring the fix was deployed on Mar 13.

> The reassuring part about Politeia is that all of the data is publicly available and is periodically timestamped onto the Decred blockchain. This means that anyone can pull the data down from github and cryptographically verify which votes were cast within the voting period (+/- 1 hour) and which ones were cast after the voting period had ended. (@lukebp in [Politeia Digest 12](https://richardred0x.github.io/politeia-digest/issue-012.html))

Merged a total of 40 commits in [politeia](https://github.com/decred/politeia/compare/8057ced5e4c0a04823a261cc064602f1a8a2ab1b...13eb0038975ff4fcddb70565687434354d208a0f) and [politeiagui](https://github.com/decred/politeiagui/compare/52c775330beb1b77ed817c85bccaaf2a8e199cdc...72885ed6e58c8a2f1bfbd2d039f6cd19b52912fe) from 6-9 contributors.

[dcrandroid](https://github.com/decred/dcrandroid): minor bug fixes, Chinese translation added, speed optimizations for viewing the transaction history.

[dcrios](https://github.com/raedahgroup/dcrios): dcrios beta is in good shape and ready for more public exposure. Testers are welcome and they can get the app at [TestFlight](https://testflight.apple.com/join/dvq51tCh). There are only a couple of minor outstanding bugs. There are known layout bugs for iPod Touch devices which are still in the works. The blocker at the moment is dealing with some formalities to approve Apple Store account. As soon as that is done, an official release client will be made.

[dcrdata](https://github.com/decred/dcrdata): Version 4 [released](https://twitter.com/decredexplorer/status/1110618796975370240) and is available at [explorer.dcrdata.org](https://explorer.dcrdata.org/).

User facing changes include complete redesign with new page styles, more information and better organization, Politeia proposal pages, aggregate block information on time intervals, log and linear scaling for charts, exchange rate monitoring, and lots of smaller changes. It is rumored that the HODL watermark is gone. For development side check the full [release notes](https://github.com/decred/dcrdata/releases/tag/v4.0.0).

During 3 months of development, the v4 release received a stunning 48K added and 19K deleted lines in 325 commits from 11 contributors. Congrats!

> There are features and improvements already brewing 4.1, so minor release should follow relatively quickly. 4.0 scope creeped quite a bit, but all for good reason, and it was worth it. ([@chappjc](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155305431834229kjptE:decred.org))

In progress:

* Load testing and performance optimization continues.
* Dependency management improvements with Go modules.
* Live consensus [vote tracking](https://github.com/decred/dcrdata/pull/1125).
* Faster [charts](https://github.com/decred/dcrdata/pull/1126).
* Proposal votes [charts](https://github.com/decred/dcrdata/pull/1210).
* [dcrextdata](https://github.com/raedahgroup/dcrextdata), a component for dcrdata that will allow tracking of data not present on the blockchain, such as historical information about exchange prices and mining pools.

[Ticket splitting](https://github.com/matheusd/dcr-split-ticket-matcher): v0.7.6 [released](https://github.com/matheusd/dcr-split-ticket-matcher/releases/tag/v0.7.6) that optimizes the fetching of unspent outputs from dcrdata and adds macOS binaries.

[docs](https://github.com/decred/dcrdocs): new detailed [Ticket Splitting](https://docs.decred.org/proof-of-stake/ticket-splitting/) guide, [Consensus Rules Voting](https://docs.decred.org/governance/consensus-rule-voting/consensus-rules-voting/) reworked and extended, [Proposal Guidelines](https://docs.decred.org/governance/politeia/proposal-guidelines/) updated to include key requirements for proposals funded from Treasury.

[decred.org](https://github.com/decred/dcrweb): updated exchanges and translations, [self-hosted](https://github.com/decred/dcrweb/pull/604) intro video to remove a YouTube request.

Other:

* Raedah Group is experimenting with an alternative [godcr](https://github.com/raedahgroup/godcr/) wallet client written in Go with multiple user interface modes. Work is in progress for CLI, terminal _(yes!)_, web browser, [nucular](https://github.com/aarzilli/nucular) and [Fyne](https://github.com/fyne-io/fyne) GUI front-ends ([screenshots](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$155329781839253ivNYC:decred.org)).
* Raedah Group is also working on [dcrseedgen](https://github.com/raedahgroup/dcrseedgen) - a standalone Decred seed generator using Go and the nucular UI.
* [timestamp.decred.org](https://timestamp.decred.org/) was redesigned and the text was rewritten to be more useful.
* New [dcrtime_checker](https://github.com/decred/dcrtime/tree/master/cmd/dcrtime_checker) tool was created to verify anchors against the blockchain directly (without interacting with dcrtimed).
* About half VSPs upgraded to [self-host captcha](https://github.com/decred/dcrstakepool/issues/279) to protect privacy of their users. Status can be tracked [here](https://github.com/decred/dcrstakepool/issues/326).

Dev activity stats for March: {} active PRs, {} master commits, {} added and {} deleted lines spread across {} repositories. Contributions came from {}-{} developers per repository. ([chart]({}))

## 人员

欢迎新到来的首次贡献者，代码在 GitHub 上合并：@devwarrior ([atomicswap](https://github.com/decred/atomicswap/commits?author=devwarrior-cool)) 及 DominicTing ([dcrweb](https://github.com/decred/dcrweb/pull/588)).

## 治理

在 3月里，[DCR 基金会](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了 16,288 DCR，并花了 13,595 DCR，使用 DCR 在 3 月份的每日平均美元价格 18.14 美元计算，本月收到 29.6 万 美元以及支出 24.7 万 美元。由于这些付款用于支付 2 月份完成的工作，因此可以用 2 月份的平均价格 16.51 美元计算 - 在这种情况下，美元收到的数字是 26.9 万美元以及支出 22.4 万美元。4月{}日 为止，基金会余额为 {} DCR (按 {} 美元计算相当于 {}万 美金)。

于 4月{}日 的提案状态:

  Proposal status as of {}:

  * [Trust Wallet integration](https://proposals.decred.org/proposals/2ababdea7da2b3d8312a773d477272135a883ed772ba99cdf31eddb5f261d571) approved by 67% Yes of the 9.3K tickets that voted. Ahead of the vote, Trust Wallet developers [moved forward](https://github.com/TrustWallet/wallet-core/issues/43) to integrate Decred on their end.
  * [ATM Integration - Planning Phase](https://proposals.decred.org/proposals/aea224a561cfed183f514a9ac700d68ba8a6c71dfbee71208fb9bff5fffab51d) rejected with 52.5% Yes among 12.7K voting tickets. Possibility of a second attempt was discussed [here](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15542882616188dHEHP:decred.org).
  * Re-submission of the Coffee Wallet [proposal](https://proposals.decred.org/proposals/45de9806c952c5ffc2fc6782fddbc74c852c26e3fb0e950144b92d75082c4731) after it was abandoned was [blocked](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$155144086813111EMAcC:decred.org) by admins as an attempt to use Politeia to market the product.
  * [Decentralize Treasury Spending](https://proposals.decred.org/proposals/c96290a2478d0a1916284438ea2c59a1215fe768a87648d04d45f6b7ecb82c3f) by @moo31337 outlines 2-step process where a draft spending transaction is published on Politeia for review, and then voted on-chain by the stakeholders. The development, testing and a required consensus vote are projected to be on the order of 9-12 months, with the budget of $200,000-250,000.
  * [Fiat pairs integration on EXMO Exchange](https://proposals.decred.org/proposals/950e8149e594b01c010c1199233ab11e82c9da39174ba375d286dc72bb0a54d7) by vadymprykhodko was published following a [pre-proposal](https://www.reddit.com/r/decred/comments/b0y9le/integration_on_exmo_exchange_new_fiat_pairs/) on r/decred. The proposal seeks $23,800 to add DCR fiat pairs on EXMO, an exchange popular in Eastern Europe.
  * [Amendment to Decred Constitution](https://proposals.decred.org/proposals/fd56bb79e0383f40fc2d92f4473634c59f1aa0abda7aabe29079216202c83114) by @richardred was submitted following a lot of discussion linked in [this issue](https://github.com/xaur/decred-issues/issues/107).

  Pre-proposals:

  * [India education and awareness campaign](https://www.reddit.com/r/decred/comments/awb5y0/preproposal_decred_india_community_new_user/) by u/Blocknext. In a chat [discussion](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15515162772723165JzrFj:matrix.org) it was pointed out that a [similar proposal](https://www.dash.org/forum/threads/building-commercial-dash-use-in-the-freelancing-industry-across-south-asia.17890/) was submitted for Dash.
  * [Second constitutional amendment](https://www.reddit.com/r/decred/comments/b84t6b/preproposal_second_constitutional_amendment_to/) by @richardred to declare February 8th the International day of Stakey.

  decredcommunity.org got some [criticism](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$155227203622209rOKeX:decred.org) for not being open source and not explicitly stating it in the body of the proposal. One of the arguments is that the Treasury never paid for closed source work before, except for some integrations where it could not be disclosed. Captured in [this issue](https://github.com/karamble/dcrcommunityweb/issues/1), the discussion also triggered some [improvements](https://github.com/decred/dcrdocs/pull/896) in proposal guidelines to state any restrictions on deliverables.

  @richardred posted an [analysis](https://github.com/RichardRed0x/pi-research/blob/master/analysis/voting/early-voting-influence.md) exploring to what degree early votes influence the behavior of late voters, and eventually the result of the vote.

  For greater detail, analysis and commentary see @richardred's Politeia Digest [issue 12](https://richardred0x.github.io/politeia-digest/issue-012.html) and [issue 13](https://richardred0x.github.io/politeia-digest/issue-013.html).

  To get notified about Politeia proposal activity, enable email notifications in your Politeia profile or follow [@pi_crumbs](https://twitter.com/pi_crumbs) and [@slices_of_pi](https://twitter.com/slices_of_pi) on Twitter.

  Discussions:

  * The rate of [spending the Treasury](https://www.reddit.com/r/decred/comments/b5vlrl/we_have_spent_23_of_decred_treasury_should_we_be/) and allocation of funds.
  * Ideas for [financial reporting](https://www.reddit.com/r/decred/comments/b2zopq/simple_financial_reporting/).
  * Upvoting of own comments was brought up again with some consensus around disabling that ability. All discussions are indexed in [this issue](https://github.com/decred/politeiagui/issues/845) which was reopened.
  * @richardred suggested to base the quorum solely on the percentage of [Yes votes](https://github.com/decred/politeia/issues/729) (currently Yes+No votes are counted) and produced a [simulation](https://github.com/RichardRed0x/pi-research/blob/master/analysis/voting/quorum-change-examples.md) that visualizes different quorum calculation methods.

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
GitHub is [updating](https://github.blog/2019-03-14-githubs-site-policy-updates-are-ready-for-your-feedback/) their policy. New drafts were published for feedback till Apr 12 and will come into effect Apr 19. Among the changes is commitment to react to [Do Not Track](https://en.wikipedia.org/wiki/Do_Not_Track), sharing user data with [more](https://github.com/github/site-policy/pull/154) 3rd party processors, updated use of third party user trackers. The change to clarify influence of U.S. sanctions triggered a question how this might impact Decred contributors - if you know, please comment in [this issue](https://github.com/xaur/decred-issues/issues/125) or [on Reddit](https://old.reddit.com/r/decred/comments/b2xsw3/github_terms_update_has_more_sanctions_stuff/). Some changes might be unpleasant but are pretty common for most companies and give us a good moment to reflect on our beliefs about free stuff. Also, unlike most companies, GitHub has all their policy documents versioned transparently in a Git repo that anybody can clone and inspect. The idea to have a similar repository for Decred was discussed a few times and there is a concept sandbox [repository](https://github.com/RichardRed0x/governance-docs) showing how it might look like.

Stellar (XLM) [experienced](https://messari.io/article/messari-research-stellar-suffered-and-quietly-patched-a-2-2-billion-xlm-inflation-bug-in-2017) an inflation bug which was exploited to print 2.25 billion XLM (worth $10 million at the time, and nearly 25% of the circulating supply) in April 2017. This bug was lightly reported at the time, it was fixed by the Stellar Development Foundation (SDF) who burned an equal amount from its community reserve. That the SDF could identify, fix and mitigate such a major exploit so quietly says something about how decentralized Stellar is.

PIVX experienced an inflation bug which was [exploited](https://medium.com/@dev.pivx/report-wrapped-serials-attack-5f4bf7b51701) in March. The bug concerned the network's zerocoin protocol (zPIV), and allowed an attacker to fake serial numbers and spend zerocoins that had never been minted. Over the course of five days, transactions creating and spending 568,897 PIV (~$438,000) were made before zPIV the exploit was identified and zPIV transactions were disabled until it could be fixed. Besides regular takeaways like "consensus code is hard" and "cryptography is hard", this case has more food for thought. First, Zerocoin functionality was disabled immediately after the exploit was discovered using one of the "sporks". Someone with the keys for these sporks can affect the whole network. Second, the bug was spotted because some nodes were [switching away](https://github.com/PIVX-Project/PIVX/pull/681) from OpenSSL that let the bug go unnoticed (OpenSSL is long [famous](https://www.peereboom.us/assl/assl/html/openssl.html) for its quality). While those nodes were not full alternative implementations, it still shows how a mismatch between diverse software helps to discover bugs. Third, it is possible to know exactly how many coins were minted because PIVX's Zerocoin protocol allows supply to be [auditable](https://zcoin.io/zcoins-privacy-technology-compares-competition/), unlike some other protocols.

Monero's new [Community Crowdfunding System](https://ccs.getmonero.org/) was [launched](https://www.reddit.com/r/Monero/comments/ay0j5n/the_new_ffs_is_complete_please_use_and_explore_it/), and a number of projects were funded.

Dash held an [election](https://blog.dash.org/announcing-the-dash-dao-irrevocable-trust-election-results-bfe134c113b0) for Trust Protectors, people who will oversee the operation of a legal trust that has been [set up](https://blog.dash.org/dash-network-elected-trust-protectors-closing-the-governance-loop-4f07b46da03e) to own and control Dash Core Group.

Dash also [finished](https://blog.dash.org/deterministic-masternode-list-and-automatic-instantsend-now-live-f2028d833388) the deployment of the Deterministic Masternode List, enabling automatic instant payments for transactions with fewer than 4 inputs.

Dash Core Group further [tightened](https://www.theblockcrypto.com/2019/03/04/corporation-behind-dash-lays-off-senior-staff-as-bear-market-grip-tightens/) its budget with layoffs and salary freezes.

Tezos [concluded](https://www.coindesk.com/welcome-to-athens-tezos-completes-historic-first-blockchain-vote) the first round of voting for its Athens upgrade. In this round bakers were choosing from between two versions of the Athens upgrade which increases the gas limit, and they chose the Athens A version which also decreases the minimum roll size and lowers the barrier to entry for bakers. The process has now moved on to its next phase, where bakers must confirm that the selected proposal should proceed to a subsequent testing and confirmation phase.

Grin developers [voted](https://www.coindesk.com/privacy-cryptocurrency-grin-votes-to-fund-third-full-time-developer) to fund 3rd full time developer in a weekly [governance meeting](https://github.com/mimblewimble/grin-pm/blob/master/notes/20190312-meeting-governance.md). An interesting aspect of Grin is their efforts towards reporting and transparency: multiple versioned documents are published on GitHub, including [decision log](https://github.com/mimblewimble/grin-pm/blob/master/decision_log.md), [meeting notes](https://github.com/mimblewimble/grin-pm/tree/master/notes), income and [expenses](https://github.com/mimblewimble/grin-pm/tree/master/financials).

Jack Dorsey [announced](https://www.coindesk.com/square-hiring-crypto-engineers-bitcoin) Square is looking to fund engineers and a designer to work full-time on Bitcoin and cryptocurrency ecosystem, as a way to give back to the community. One [response](https://twitter.com/martybent/status/1108493263185559552) noted that this shows why "dev fund" embedded in a protocol is not needed, because network participants have enough incentives to fund their infrastructure. In case of Decred, if the Treasury is ever deemed no longer necessary, it is in the power stakeholders to repurpose it for investing into a wider crypto/open source/open hardware ecosystem, or disband it entirely.

Investigation of QuadrigaCX by Ernst & Young [found](https://cointelegraph.com/news/report-quadrigacx-wallets-have-been-empty-unused-since-april) that exchange's cold wallets were empty and unused since April 2018. Kraken [offered](https://blog.kraken.com/post/2155/were-offering-a-100000-reward-for-discovery-of-quadriga-coins/) a $100K reward for tips that best lead to the discovery of the missing $190 million.

New research from @BitwiseInvest [suggests](https://twitter.com/BitwiseInvest/status/1109114656944209921) 95% of reported BTC spot volume is fake, but also notes many good news about the crypto ecosystem.

IMF found an [elegant solution](https://blogs.imf.org/2019/02/05/cashing-in-how-to-make-negative-interest-rates-work/) how to make negative interest rates work as a counter-measure to a possible future crisis. Negative interest rate of -3% is when you deposit $100 to a bank and withdraw $97 a year later. Such rate is currently hard to enforce because people would just withdraw to cash. The "straightforward" solution would be to move into a happy "cashless world" where the bank can set arbitrary negative rate and you simply can't withdraw to cash to save your value from melting. This is expected to "make consumption and investment more attractive, ... jolt lending, boost demand, and stimulate the economy". But getting rid of cash is not easy and is years away. So another solution to sustain a negative interest rate that is easier to roll today is to split a fiat currency into e-money and cash and introduce a floating conversion rate between them. This way, in a -3% interest rate scenario, you either deposit 100 cash dollars into e-dollars and get 97 e-dollars in a year, or hold cash and enjoy a 3% value loss against both goods and the e-dollar. In such a system there is no benefit to hold cash relative to bank deposits. Hasu and Su Zhu argue that crypto can [serve as a hedge](https://uncommoncore.co/bitcoin-is-a-hedge-against-the-cashless-society/) against the cashless society. Disclaimer: this paragraph is written by a layman. Economists are welcome to [comment](https://www.reddit.com/r/decred/) how this is healthy at all.

Poloniex [committed](https://medium.com/circle-blog/poloniex-welcomes-grin-commits-to-share-transaction-fees-for-1-year-d07bc92cc0f8) to share a portion of Grin trading fees with [Grin General Fund](https://grin-tech.org/general_funding). 50% of all fees will be donated during the first month, and 25% for the next 11 months. Pretty rare and generous act in the space.

[Coinbase Custody](https://custody.coinbase.com/) [enabled](https://twitter.com/CoinbaseCustody) deposits and withdrawals for ZIL, KNC, ZEC, XTZ and [claim](https://blog.coinbase.com/coinbase-custody-launches-staking-support-for-tezos-makerdao-governance-to-follow-68f7bc51bc53) to hold $600 million for 60 clients. The service offers regulated, insured and full offline, segregated custodial storage of crypto. The plan is to allow clients to fully participate in crypto networks besides just holding: Tezos baking (staking) is already implemented while voting in Tezos and MakerDAO is planned for Q2 2019.

Coinbase received a backlash for acquiring Neutrino https://news.bitcoin.com/coinbase-severs-ties-with-hacking-team-members-while-data-sharing-backlash-intensifies/ https://www.coindesk.com/bitcoin-delete-coinbase-neutrino-crypto

{other: regulations, security, fun}

Texas {worthy?}

* https://www.chepicap.com/en/news/8035/texas-may-soon-require-id-verification-from-crypto-users.html
* https://twitter.com/propelforward/status/1104745898201042950

vulns patched https://blog.trezor.io/firmware-updates-for-trezor-one-firmware-1-8-0-and-trezor-model-t-firmware-2-1-0-b9df91e048df

https://news.bitcoin.com/bitcoin-cash-developers-launch-privacy-preserving-light-client-neutrino/


## 关于月报
三月为英文第12期 [GitHub](https://xaur.github.io/decred-news/journal/201903) 月报。 点击[这里](https://xaur.github.io/decred-news/)浏览所有往期月报，翻译等。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues) 和 [Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

感谢 (按字母排序):

## 中文社区

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

感谢 (按字母排序):
