# Decred月报 - 3月 

![](img/)


## 开发进展总结

[dcrd](https://github.com/decred/dcrd): Huge [refactoring](https://github.com/decred/dcrd/pull/1656) makes initial full sync [20-25%](https://twitter.com/davecgh/status/1110649183185317889) faster, down to around 45 mins on typical hardware. Another benefit is reduced vote propagation latency:

> \[latency is affected by\] many factors, but per node average from ~70ms to sub 5ms on my nodes. Need more data for better values. Good alone, but real gains will come with majority network upgrade since savings are multiplied by number of nodes votes traverse (log_8(tot)). Full deployment ~90% overall improvement. ([@davecgh](https://twitter.com/davecgh/status/1110721000172384256))

As part of the optimization `txscript` module was completely refactored to use a new zero-allocation script tokenizer.

> Initial sync is a big factor of course, but the real gains are in the ongoing transaction processing for mempool. The other really nice facet is the exported tokenizer which means it's possible to do zero-allocation analysis on scripts outside of txscript which is great for building apps (e.g. atomic swaps, taproot, etc) on top. ([@davecgh](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$155249146926580yNJqU:decred.org))

Because a critical and error prone area of consensus code was changed, significant effort has been put into making these changes easier to reason about and review by carefully crafting a series of 122 individual commits such that every commit message thoroughly describes its purpose, maintains consensus, and therefore passes all tests.

Bonus: the refactoring slashed some 2K lines of code. Less code, less bugs!

There is an opportunity to remove another 10-15 min of initial block download but it requires months of solid work _(hint to contributors)_.

Other merged work:

* Initial Bech32 ([BIP 173](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki)) support [ported](https://github.com/decred/dcrd/pull/1646) from btcsuite.
* Introduced reusable [LRU cache](https://github.com/decred/dcrd/pull/1683) module.
* Module `hdkeychain` [refactored](https://github.com/decred/dcrd/pull/1696) to make code less brittle and more testable.
* [Added](https://github.com/decred/dcrd/pull/1424) new background block template generators.
* Lots of refactoring and testing improvements to harden the codebase against unintended changes.

A total of [209 commits](https://github.com/decred/dcrd/compare/4e7f080b7b2cb11a8680d54dc5fb9ce735119d15...8f5019e083e92f31b2799f9d23809e0c0692d465) from 9 contributors were merged in March.

In progress:

* Another large refactor [started](https://github.com/decred/dcrd/pull/1698) to address multiple issues in `chaincfg` module.
* Discussion [started](https://github.com/decred/dcrd/issues/1645) to protect node seeding process from DNS based attacks.

In the big picture, changes like background block template generator and part of `txscript` optimization aim to improve scalability and reduce the number of missed votes on the network through improvements to the mining infrastructure and reduction of voting propagation latencies. The other part of `txscript` and `chaincfg` refactoring are infrastructure work to properly introduce a new script engine version for future desirable consensus changes such as the decentralized treasury spending. Even if that proposal doesn't pass, the infrastructure is still needed for a wide variety of future script-related consensus changes.

[dcrwallet](https://github.com/decred/dcrwallet): bug fixes and code maintenance. Merged [12 commits](https://github.com/decred/dcrwallet/compare/9f5f1163d8bf8037138f07734002470d4100de21...9450c9183e71231065dc0ea25087a47e8e5bb38e) from 6 contributors.

[Decrediton](https://github.com/decred/decrediton): Ticket activity heatmap visualization merged among smaller fixes - total [5 commits](https://github.com/decred/decrediton/compare/35ab6e216dde0bc90d76334e25eb5174bf62e623...f80e832e55231a8f4cb7b1aa69f6e2faea2709df) from 2 contributors.

[Politeia](https://github.com/decred/politeia): Added tab to [preview](https://github.com/decred/politeiagui/pull/1018) proposal text, completed feature to [view difference](https://github.com/decred/politeiagui/pull/1004) between proposal versions. {is the differ complete or needs more work? is it deployed?}, default comment sort option [set to](https://github.com/decred/politeiagui/pull/1034) Top, added feature to set sort in the URL. Many bugs were fixed.

In terms of code infrastructure, several parts of contractor management system landed in master, completed several steps of refactoring to fix accumulated layer violations and better support contractor management system, test coverage [increased](https://github.com/decred/politeia/pull/727) from 13% to 19%.

A bug was detected that allowed advanced users to cast votes beyond the end of the voting period. The fix was deployed on Mar 13.

> The reassuring part about Politeia is that all of the data is publicly available and is periodically timestamped onto the Decred blockchain. This means that anyone can pull the data down from github and cryptographically verify which votes were cast within the voting period (+/- 1 hour) and which ones were cast after the voting period had ended. (@lukebp in [Politeia Digest 12](https://richardred0x.github.io/politeia-digest/issue-012.html))

{where is the issue or PR for the fix? is it [#742](https://github.com/decred/politeia/pull/742)?}

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

* [Trust Wallet 钱包整合提案 Decred integration in Trust Wallet](https://proposals.decred.org/proposals/2ababdea7da2b3d8312a773d477272135a883ed772ba99cdf31eddb5f261d571) approved by 67% Yes of the 9.3K tickets that voted. Ahead of the vote, Trust Wallet developers [moved forward](https://github.com/TrustWallet/wallet-core/issues/43) to integrate Decred on their end.
* [Decred ATM 集成提案 Decred ATM integration](https://proposals.decred.org/proposals/aea224a561cfed183f514a9ac700d68ba8a6c71dfbee71208fb9bff5fffab51d) rejected with 52.5% Yes among 12.7K voting tickets. Possibility of a second attempt was discussed [here](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15542882616188dHEHP:decred.org).
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

--

> ## 社区

截止于 {} 的社区数据 :

* Twitter 关注量: 39,797 (+19)
* Reddit 关注用户: 9,365 (+35)
* Matrix 用户: 266 (+19)
* Slack 用户: 6,581 (+52)
* Discord 用户: 2,101, 发帖数: 131
* Telegram 用户: 4,272 (-231)
* YouTube 关注量: 3,746 (-6)
* Facebook 关注: 3,141 (+9), likes: 2,896 (+5)
* LinkedIn 关注: Decred page 483 (+17), Politeia page 29 (+2)
* GitHub dcrd : 474 (+6), fork人数: 1,237 (+16)

电报群社区: 中文 866 (+53), 意大利语 160 (+28), 葡萄牙语 642 (+100), 西班牙语 73 (+11).


社交系统新闻：



> ## 市场

在二月中 DCR 交易价格为 美金 14.97-18.28 / BTC 0.0042-0.0048。平均日汇率为 {} 美元。

## 相关外部信息



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
