# Decred月报 - 4月

![abstract art](img/APR19_journal-201904-384.jpg "Blue Dragon by @saender. Dragon resembles power/fear/terror/chaos. Blue dragon is calm and intelligent, but nevertheless powerful. It resembles a balance of power and wisdom.")

在四月份我们在 Decred 测试网上推出了闪电网络！欢迎[查看](https://hackernoon.com/decred-wants-you-be-one-of-the-first-to-test-the-dcr-lightning-network-dd9ecf14d95e)，测试，并开始在 Decred 的 LN 上开始构建。

LN 将在 DCP0004 在 5月9日（第342，784区块）激活时上线主网，但它将需要一段时间才能建立起来并且稳定至可以在主网上使用 - 现在是在 Decred 测试网上尝试 LN 的时候。同时提醒所有节点很重要的是必须在 **5月9日前升级以避免被分叉出网络！**

Politeia 软件在上线的提案网站上部署了大量性能改进和新功能（如提案版本的差异查看）。承包商管理系统也已准备好以基本形式进行，并将用于收集和处理4月份的承包商发票。

本月的 Decred 月报版本比平时更加分散，@bee 退下了他一直以来在月报里扮演的重要角色（但依然积极提供指导），其他贡献者也比平常做得更多。

## 请马上升级节点!

成功通过[投票](https://voting.decred.org/)的规则更改 [DCP0004](https://github.com/decred/dcps/blob/master/dcp-0004/dcp-0004.mediawiki) (为启用 LN 更新序列锁定规则)将于 5月9日（第342，784区块）激活。一旦有人根据新规则进行交易事务，任何仍遵循旧规则的节点（即v1.4.0之前的任何软件版本）将被视为停止遵循合规的 Decred 主链。因此，非常重要的是所有节点（矿工，选民，用户，商家，服务提供商）必须在 5月9日 之前将其 Decred 软件升级到v1.4.0。**别在5月9日被分叉出网络！**


## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 重构继续进行，未使用函数和条件清理，改进挖掘代码并修改`chaincfg`模块。由于之前对版本化模块的工作现已可用并且已完全使用，因此现在可以进行仔细的代码升级并确保不会在其他环节造成破坏。

[dcrwallet](https://github.com/decred/dcrwallet): 代码的清理和购票代码的改进。开始为 gRPC API 添加[可选身份验证](https://github.com/decred/dcrwallet/pull/1437)，允许用户省略需要解锁钱包的 API 调用中的密码。这将缓解通过物理和网络分段隔离未锁定钱包时出现的问题。

[Decrediton](https://github.com/decred/decrediton): 使 Decrediton 设计更具响应性（使其在更小的屏幕上可用）的工作继续进行，为此[主题](https://github.com/decred/decrediton/issues/1820)中的几乎所有视图完成了响应式设计。新的响应式设计在创建新的钱包视图中[已实施](https://github.com/decred/decrediton/pull/2094)。用于向 Decrediton 添加嵌入式 LN 钱包 UI 的[提交](https://github.com/decred/decrediton/pull/2107)也已打开; 此初始版本将允许Decrediton用户执行开/关频道，存/取款，创建发票和发送付款等操作。

[Politeia](https://github.com/decred/politeia): 在提案网站上进行了项升级[部署](https://twitter.com/marco_peereboom/status/1120398754216062978)，这带来了显着的性能改进，为提案版本历史记录查看器下拉菜单添加了差异查看器，并更改了评论的排序默认设置首先显示评分最高的评论。承包商管理系统也已上线，承包商将使用它来提交 4月份 的发票。

[dcrlnd](https://github.com/decred/dcrlnd): Decred 的 闪电网络(LN)已在测试网上运行！经过几个月的努力和整个软件的几次更改，Decred 原始 [lnd 守护程序](https://github.com/lightningnetwork/lnd)的官方端口，[dcrlnd](https://github.com/decred/dcrlnd) 已经[发布](https://matheusd.com/post/announcing-dcrlnd/) 并可在测试网使用。来自上游闪电网络项目的所有单元和集成测试都正在通过，并且在 Decrediton 的初始[集成](https://github.com/decred/decrediton/pull/2107) 即将完成。

一个 lnd 水龙头 (faucet) 已经被[设计](https://github.com/matheusd/lightning-faucet/pull/4)成符合 Decred 的外观和感觉。[这里](https://testnet-dcrln-01.davec.name/)查看几个测试网水龙头中的一个。

目前正在准备主网的 LN，并在 5月9日 左右的第 342,784 个区块中，在“fixlnseqlock”议程[激活](https://explorer.dcrdata.org/agendas)之后，在主网上可以实现 Lightning。但这需要时间建立网络及改善用户体验。目前使用 Decred 的 LN 应该被认为是实验性质的，并且不应涉及大量的 DCR。 测试网将是 LN 活动一段时间的地方。您可以通过此[网络图表](http://ln-map.jamieholdstock.com/)跟踪测试网 LN 的增长情况。


[dcrandroid](https://github.com/decred/dcrandroid): 小错误修复和语言优化继续进行中。可选的生物识别身份验证选项也在[进行中](https://github.com/decred/dcrandroid/pull/343)，并将在下一版本中发布，在输入钱包密码短语时添加额外的安全层。

[dcrios](https://github.com/raedahgroup/dcrios): dcrios beta 版本在社区成员继续测试下改进了 UI。 目前只剩下数个未解决的漏洞，开发人员也正继续通过正式的 Apple Store 申请批准应用程序。

[dcrdata](https://github.com/decred/dcrdata): v4.1.0 已发布并部署于 [explorer.dcrdata.org](https://explorer.dcrdata.org/)。此版本增添[实时追踪](https://explorer.dcrdata.org/agendas)共识规则更改的链上投票进度，以及在[发布笔记](https://github.com/decred/dcrdata/releases/tag/release-v4.1.0)中列出的一些性能和开发改进。[Politeia提案](https://alpha.dcrdata.org/proposals)的投票图表也已添加到alpha网站上并正在进行迭代。

[docs](https://github.com/decred/dcrdocs): 新页面: [预挖](https://docs.decred.org/advanced/premine/) 描述了 Decred 的空投和推出（常见误解），[验证投票](https://docs.decred.org/governance/consensus-rule-voting/verifying-votes/) 描述如何验证选票投票, [硬件钱包](https://docs.decred.org/wallets/hardware-wallets/) 则提供支持 DCR 的硬件钱包基本信息。[Decred 的治理入门](https://docs.decred.org/governance/overview/)页面则被重新翻修以更好的介绍选票投票和 Politeia 提案系统在决策过程扮演的角色。

[dcrtimestamptweet](https://github.com/tiagoalvesdulce/dcrtimestamptweet): 在三月底推出了一个新的推特机器人。只要在评论中提到 [@dcrtimestampbot](https://twitter.com/dcrtimestampbot),机器人将把帖子收录到 IPFS，然后使用 dcrtime 将数据时间戳到 Decred 区块链中，并向用户发出确认消息。

4 月开发活动数据: 分布于 10 个最活跃存储库（repositories) 有 326 个有效 PRs, 509 个主要提交, 96K 行添加 及 55K 行删除。每个存储库中有来自 1-9 位开发者的贡献。

## 人员

欢迎新到来的首次贡献者，代码在 GitHub 上合并：@devwarrior ([atomicswap](https://github.com/decred/atomicswap/commits?author=devwarrior-cool)) 及 DominicTing ([dcrweb](https://github.com/decred/dcrweb/pull/588)).


恭喜 5 位新的贡献者列入官网[decred.org](https://decred.org/contributors/):

* Angel Dominguez (@anshawblack, 市场)
* Thiago de Freitas Figueiredo (@thi4go, 开发)
* Hugo Chang (@changhugo, 社区经理 - 中国)
* Dominic Ting (@dominic.d, 社区经理 - 中国)
* Michael Guimaraes (@michae2xl, 社区经理)

1 位不活跃设计人员从 decred.org 被移除: Kärt Koosa (@kart, 插画者)

## 治理

实施 DCP0004 的[共识投票](https://voting.decred.org/) 在4月11日完成，几乎100％批准，54.5％ 的选票通过投票积极参与。新规则将于 5月9日 生效，请参阅上面有关升级节点软件的说明。

在 4月里，[DCR 基金会](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了 15,460 DCR，并花了 13,943 DCR，使用 DCR 在 4 月份的每日平均美元价格 24.22 美元计算，本月收到 37.4 万 美元以及支出 33.8 万 美元。由于这些付款用于支付 3 月份完成的工作，因此可以用 3 月份的平均价格 18.14 美元计算 - 在这种情况下，美元收到的数字是 28.0 万美元以及支出 25.3 万美元。5月3日 为止，基金会余额为 608,069 DCR (按 26.20 美元计算相当于 1600万 美金)。

于 5月7日 的提案状态:

4 项新提案提交:

* [去中心化社区基金开销 Decentralize Treasury Spending](https://proposals.decred.org/proposals/c96290a2478d0a1916284438ea2c59a1215fe768a87648d04d45f6b7ecb82c3f) 由 @moo31337 提出, 提案提议每个月进行链上投票核批社区基金会开销。这项提案吸引了很多讨论并在新闻中报导。其中一些实现细节故意被省略：

  > 原因是在我们多年的软件开发经验中学到的是只计划未来两步并在达到目标后再进行评估。规划太遥远几乎总是以现实与计划相冲突而告终。所以，没错，目前计划是有意含糊的。一旦技术实现变得明显，我们就可以再决定这个过程细节。([@moo31337](https://proposals.decred.org/proposals/c96290a2478d0a1916284438ea2c59a1215fe768a87648d04d45f6b7ecb82c3f/comments/6))

  很多提问已获得解答并且投票已经在 5月6日 [开始](https://twitter.com/marco_peereboom/status/1125497388041494528)。

* [EXMO交易所的法币交易对整合 Fiat Pairs integration on EXMO Exchange](https://proposals.decred.org/proposals/950e8149e594b01c010c1199233ab11e82c9da39174ba375d286dc72bb0a54d7) 由 @vadymprykhodko 提出，要求 ~23,800 美元 将 DCR 与 BTC 和 两个法币交易对（DCR/RUB，DCR/UAH）整合到 EXMO 交易所。这项提案以 62.6% 同意 通过了投票。

* [Decred 的宪法更改 Amendment to Decred Constitution](https://proposals.decred.org/proposals/fd56bb79e0383f40fc2d92f4473634c59f1aa0abda7aabe29079216202c83114) 由 @richard-red 提出，提议对 Decred 宪法作出一系列更改，以将其更新，并澄清宪法在项目里的状态。投票以 12K 选票参与率 99% 同意通过。感谢所有在过程中参与提过意见的人们。


* [通过提案系统宣传 DCR 故事 A Journey to the Future of Work- Telling the DCR story through Politeia](https://proposals.decred.org/proposals/b9f342a0f917abb7a2ab25d5ed0aca63c06fe6dcc9d09565a9cde3b6fe7e6737) 由 @jer979 提出，要求 40 DCR 编写一篇关于提交提案，经历评论和投票阶段经验的文章 - 以及另外，如果该文章被纳入“一级”媒体的 60 DCR 支付。

另外 3 份 提案的投票也在本月结束： 

* 提案资助 [Trust 钱包整合 Trust Wallet integration](https://proposals.decred.org/proposals/2ababdea7da2b3d8312a773d477272135a883ed772ba99cdf31eddb5f261d571) (预算 3，300 美金 以及长期的 每月100美金)以 67% 同意票通过。
* 类似于 RFP 流程的 [ATM 整合提案](https://proposals.decred.org/proposals/aea224a561cfed183f514a9ac700d68ba8a6c71dfbee71208fb9bff5fffab51d)以 52.5％ 的票数被拒绝 - 这是第一个拥有 >50％ 同意票但被拒绝的提案。在 #proposals 聊天室的一项[讨论](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15542882616188dHEHP:decred.org)中,由于投票结果接近，讨论的共识为可以以另一版本提案重新尝试投票。
* 由 @georgepro 提交的非洲宣传提案 bring Decred to Africa (Ghana) 以 5.4% 同意票被拒绝。在投票结果出来后（提案系统Politeia已关闭评论），@jet\_user 在 reddit 发表了一篇有关此提案长而周到的[评论](https://www.reddit.com/r/decred/comments/b9vhee/voting_has_started_for_the_bring_decred_to_africa/eks6578/)。

更多更详细的提案系统 Politeia 相关的消息请关注[第 14 期](https://medium.com/politeia-digest/issue-14-apr-1-apr-16-2019-1ad873ccafb) Politeia 简报。

dcrdata 的 alpha 版现在提供[图表](https://alpha.dcrdata.org/proposals)，显示随时间推移的投票结果，包括正在进行的投票的实时更新。这使得存储在 Git [存储库](https://github.com/decred-proposals/mainnet)中的 Politeia 数据更易于访问。

## 网络

算力: 4 月算力开始 ～377 Ph/s 及 ～530 Ph/s 浮动。低点为 276 Ph/s 高点为 676 Ph/s。在 5月1日 根据 [dcrstats.com](https://dcrstats.com/pow) 数据显示，矿池算力分布为：Poolin 21%, lab.antpool.com 20%, F2Pool 18%, BTC.com 10%, UUPool 9%, Luxor 2.9%, CoinMine 0.37%, BeePool 0.09%, suprnova 0.04% 及其他 18.8%。矿池分布数据为大约值无法精确计算。

投票: 按 5月1日 dcrstats.com（数据显示）, 30日 平均票价为 117.2 DCR (+ 4.9)。价格在 105.4 DCR 至 127.7 DCR之间浮动。锁仓数额为 4.51-4.76 百万 DCR, 大约占总流通量的 47.0-49.1%。

节点: 截止于 5月7日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 180 public listening Node 及 201 Normal Node。版本分布: v1.5.0 dev builds: 6.9% (+0.6%), v1.4.0: 61% (+6%), v1.4.0 dev and rc builds: 6.1% (+1.1%), v1.3.0: 11% (-6%), v1.2.0: 7.9% (-1.6%), v1.1.2: 4.3% (+0.3%), v1.1.0: 1.4% (-0.3%)。

[DCP0004](https://github.com/decred/dcps/blob/master/dcp-0004/dcp-0004.mediawiki) 以几乎100% 通过的同意率通过。新规则将于 5月9日（第342，784区块）激活。请确保软件升级到[最新版本](https://decred.org/downloads/)。

## 整合

CoinZark [添加](https://twitter.com/coinzark/status/1114888240857849862) Decred 对超过 25+ 支持的货币兑换。

Vertbase [公布](https://twitter.com/vertbase/status/1119226866311757829) 他们将为 DCR 增加 GBP 和 EUR 交易。在 UK 使用 GBP 交易对的注册及购买将在 5月2日 [开启](https://twitter.com/vertbase/status/1123998203689484291)。

警告: Decred 月报作者无法确认以上交易所可靠性。请自行进行审核才将您的个人信息或财产信托于任何实体。

## 外联活动

四月是一个非常忙碌的月份，协调外展，计划聚会和活动，并在各种平台上设置开始执行营销计划。@anshawblack在电报群中获得了 Decred DCR 的管理权，并通过共享优质 Decred 内容促进了出色的讨论。以下是 Politeia 批准的[营销计划](https://proposals.decred.org/proposals/c84a76685e4437a15760033725044a15ad832f68f9d123eb837337060a09f86e)的最新进度更新。

Decred Assembly 视频: @Dustorf & @jy-p 做了练习，然后在两周后回来录制 Decred Assembly (DA) 改版的第一集。 同时也决定了不是录制单个节目，而是单独录制片段以生成更多更易消化的视频。四月份中，我们将与 @jy-p 深度讨论 DEX，Decred 分布式的与 @elian 谈论墨西哥和南美洲，以及与 @richardred 分析 Decred 利益相关者无法作出好决定的这项误解。为了每周发布这些视频，目前仍然有一些管理工作。我们希望在月报发布时这些视频能顺利完成。五月版已经安排好了。

Decred 通讯简报 Decred Newsletter: 我们决定使用开源服务[phpList](https://www.phplist.org/)，这造成了一些延迟。现已设置好构造并已成功发送测试。目前，设计团队正在构建一个模板，使其看起来很漂亮，他们也正在努力将注册链接合并到decred.org 中。完成后，我们将分享以便让人们注册，我们希望在5月份内发送第一封电子邮件。

网站更新 Website Updates: 体系结构设置已完成，并为大多数附加子页面编写了初稿。此外，还为新的介绍性视频编写了第二版稿，该视频将分为三部分：安全。适应性强。自资。

Decred 深度播客 Decred in Depth Podcast: @anshawblack 将在 5月11日前往纽约参与 Blockchain Week 并计划与 @jy-p, @jz, Murad Mahmudov, Joel Monegro, Permabull Niño, 和 Trey Ditto 录制播客。他将在之后的几个星期和月份进行剪辑。

社区组织 Community Organizers: Decred 聚会的数量和参加活动的数量突显了我们在世界各地动员社区的成功。会议指南和执行聚会的工具将成为网站更新的一部分。在此完成前，可以在 GitHub 上的 [Design Repository](https://github.com/decred/dcrdesign/releases) 中找到资源。提醒一下，如果你想在你附近办聚会，那就开始吧！ Decred 社区成员在所有事情上都处于领导地位，没有人需要决定在哪里发生什么事，所有事情都是社区主导。

Decred 已在币安获得 [V Label 认证](https://medium.com/binanceexchange/binance-infos-v-label-verification-f3506f64b292)。通过认真需要一名项目的官方成员（拥有Decred 邮箱地址并已通过币安认证的成员 - @s\_ben)审核并确认 Decred 的[资料页面](https://info.binance.com/en/currencies/decred)。这使我们有机会更新项目描述以更准确，并结合最新的营销信息，以及纠正有关Decred发布的一些错误信息（一项常见任务）。

## 社区活动

已出席:

* Apr 4-5 - [BitcoinDay Argentina](https://www.eventbrite.com.ar/e/bitcoinday-cor-ciudad-de-cordoba-tickets-57550681638) - Cordoba, Argentina. @elian presented a keynote "Decred in 20 minutes" introduction to the project, and also a "How to become a Decred contractor" talk as part of the workshop. See report [here](https://decredcommunity.org/events/bitcoinday-argentina). ([photos](https://twitter.com/elianhuesca/status/1114571807649148928))
* Apr 8 - [Decred: Tools, Use and Contribution](https://www.meetup.com/decredpdx/events/260098916/) - Portland, USA. 17 attendees heard @oregonisaac give an in depth talk on Decred tools, use and contribution, and development updates from @raedah, @oregonisaac and @s\_ben. The community is growing in numbers and engagement. Everyone is excited and looking forward to the next meetup. ([photos](https://twitter.com/DecredPdx/status/1115734111174291456))
* Apr 18 - [Coordinating Open Source: Today and Tomorrow](https://www.meetup.com/San-Francisco-Decred-Meetup/events/260046546/) - Coinbase HQ, San Francisco, USA. The event was held at Coinbase HQ in partnership with Coinbase Custody. @lukebp spoke about Decred's unique governance and self-funding model. There was then a moderated discussion about tradeoffs of different funding models, and Luke answered questions for over an hour. Approximately 70 people attended. (photos: [1](https://twitter.com/liz_bagot/status/1119098216165695495) [2](https://twitter.com/LarissaBundziak/status/1119340380187529216))
* Apr 18 - [Binance LATAM AMA](https://twitter.com/binance/status/1118883131799400449) - online. @elian participated in a Spanish language AMA with members of the Binance Latam community, receiving and answering question from users on Facebook and Telegram.
* Apr 22-26 - [Talent Land](https://www.talent-land.mx/) - Guadalajara, Mexico. @elian provided a [summary](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155690701035573YcsMH:matrix.org) of the event and Decred's participation. The event was attended by over 60,000 people, and Decred was the only major cryptocurrency represented in "Blockchain Land". A talk titled "Decred: The money of the future" was attended by around 35 people, and hundreds more stopped by to talk to the Decred representatives at the booth. Attendees responded well to the idea of "be your own bank", and also the concept of Decred as self-funding open source software production. (photos: [1](https://twitter.com/elianhuesca/status/1121243105276125184) [2](https://twitter.com/victorarubin/status/1121169425011494913))
* Apr 24-25 - [Blockchain Summit](http://blockchainsummit.ma/) - Rabat, Morocco. @arij (@butterfly in Slack) presented Decred and exhibited. Mainly students and professors from Morocco and France attended. (photos: [1](https://twitter.com/DecredArabia/status/1121011670808240128) [2](https://twitter.com/DecredArabia/status/1121160292333965313) [3](https://twitter.com/DecredArabia/status/1121695331253673984))
* Apr 25 - [Decred Chicago meetup](https://www.meetup.com/Chicago-Decred-Meetup/events/260653330/) - Chicago, USA. Jack Miller hosted the inaugural meetup in Chicago.
* Apr 29 - [AMA for Chinese Community](https://www.chainnode.com/ama/317174) - online. @Haon and @guang conducted an AMA with members of the Chinese Decred community, receiving and answering over 30 questions.
* Apr 30 - [Crypto Governance - It is a matter of survival](https://www.meetup.com/BlockchainMelbourne/events/260266298/) - Melbourne, Australia. Decred facilitated this panel discussion about crypto governance. ([photos](https://twitter.com/DecredAustralia/status/1123396115003392000))

即将到来的:

* May 10-17 - NYC Blockchain Week - New York, USA. A team of 7 Decred community members will attend events at various locations. Ditto has been working to make [AtomicSwap](https://twitter.com/TheBlock__/status/1123339626616360962) (the event formerly known as BreakerCon) as successful as possible on May 15. You may have seen the [news](https://twitter.com/BreakerMag/status/1123259686516592642) that Breaker Mag is shutting down, so Ditto is now co-hosting this event with the top crypto outlet, The Block. During Blockchain Week NYC, Decred will take the main stage as @jy-p speaks on a panel called "The Idealist's Dilemma", where he'll debate what it means to be decentralized with other project leads: Ryan Taylor of Dash, Alexander Zaidelson of Beam, and Tal Kol of Orbs.
* May 18 - [Criptolatinfest](https://criptolatinfest.com/) - Bogota, Colombia. Decred will have a speaking slot.
* May 20-21 - [La Conexion](https://www.la-conexion.com/) - Medellin, Colombia. @elian will give a keynote on governance.
* May 23-24 - [BitcoinDay Uy](https://bitcoinday.tv/) - Montevideo, Uruguay. Speaking slot to present Decred at BitcoinDay Uruguay. This event is organized by the same group as BitcoinDay Argentina, and the invitation to present Decred comes from the project's strong showing in Argentina.
* Jun 5 - Decred Meetup - Berlin, Germany. @jholdstock will present an overview of Decred and Philipp Banhardt of BlueYard will discuss their investment thesis. Hosted by BlueYard Capital.
* Jun 12 - [Decred: A Decentralized Autonomous Entity](https://www.meetup.com/Decred-Washington-DC-Meetup-Group/events/261144707/) - Arlington, VA, USA. Organized by Akin Sawyerr.
* Jun 19-23 - [Campus Party Brasil](https://brasil.campus-party.org/campus-party-brasilia/) - Brasilia, Brazil. Decred [will](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15568861633013AEoGy:decred.org) be well represented, as it always is at Campus Party.
* Early June, date TBD - Decred meetup NYC, being launched by Cole Kennelly of Staked. Planning the first three events through the summer, then will involve Decred in events that incorporate the wider ecosystem.
* The SF Meetup group will share details soon about their next event, likely to be held in early June. The working topic is Lightning Network.

## 媒体

Ditto 概览:

* @jz spoke with [The Block](https://www.theblockcrypto.com/2019/04/17/binance-wants-crypto-projects-to-migrate-to-its-chain-from-ethereum-and-the-firms-massive-trading-business-could-help/) about Decred's listing experience on Binance.
* Ticket-voter [messaging](https://pastebin.com/7SvuVyyY) document was created as a tool for educating people on how Decred's voting system works. Input from the community was incorporated, with second version currently under review.
* An [article](https://www.investinblockchain.com/put-your-money-where-your-mouth-is-decreds-treasury-proposal-closer-true-dae/) on the proposal to decentralize the Treasury appeared on InvestInBlockchain.com.
* @matheusd drafted a [blogpost](https://hackernoon.com/decred-wants-you-be-one-of-the-first-to-test-the-dcr-lightning-network-dd9ecf14d95e) on the Lightning Network Testnet on Medium and it was published on HackerNoon.
* AMA with @jy-p [took place](https://www.reddit.com/r/CryptoCurrency/comments/bjubwv/ama_decred_project_lead_jake_yocompiatt/) on r/cryptocurrency, which has more than 870K readers. @lukebp generated this opportunity when he presented at Coinbase in SF.
* Ditto and @Dustorf will have an AMA for the Decred community to ask anything about PR and marketing via Reddit, Matrix, and YouTube. Target date is May 17 at noon EST (UTC-5).

部分文章:

* Unpacking Decred's Social Contract by @Haon ([medium](https://medium.com/@NoahPierau/unpacking-decreds-social-contract-69c413aa652))
* Be one of the first to test the DCR Lightning Network by @matheusd ([medium](https://hackernoon.com/decred-wants-you-be-one-of-the-first-to-test-the-dcr-lightning-network-dd9ecf14d95e))
* Crypto Briefing reviewed Decred and [rated](https://cryptobriefing.com/decred-digital-asset-report-dcr-token-review/) it C+ (6.4), citing "... Decred has a smaller merchant network and less active ecosystem compared to its rivals. In addition, the massive inflation rate discourages users to utilize DCR as a means of payment"
* Blockchain Voter Apathy by Roy Learner ([medium](https://medium.com/wave-financial/blockchain-voter-apathy-69a1570e2af3)) - considers voter participation in a selection of blockchain projects (including Decred)
* Blockchain proposal voting notes by @richardred ([github](https://github.com/RichardRed0x/crypto-governance-research/blob/master/governance-proposals/proposal-data-notes.md)) - a review of proposal voting datasets added for Decred, Dash and Aragon
* What Types of Organizations Should Be Autonomous? by Amentum Capital ([medium](https://medium.com/amentum/what-types-of-organizations-should-be-autonomous-6f9dff3c5691)).
* Past, Present, Future: From Co-ops to Cryptonetworks by Jesse Walden ([a16z.com](https://a16z.com/2019/03/02/cooperatives-cryptonetworks/), _missed in Mar issue_)

翻译:

* Guides to solo staking and ticket splitting have been [translated](https://mp.weixin.qq.com/s/lAxmWYItifQldGgwTVOWHw) to Chinese by @wanbihou. Check out [dcrclub.org](https://blog.dcrclub.org/) for a collection of Chinese translations of Decred articles.
* @akinsawyerr translated a Decred review by iBotics Research from [Spanish](http://ibotics.es/reports/iBotics_Research_DCR.pdf) to [English](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$1556338959151873UVFAF:matrix.org).

视频:

* @jy-p's Decred overview [keynote speech](https://www.youtube.com/watch?v=l2Vu0JX7Xbc) at OKCoin + Decred San Francisco [event](https://www.eventbrite.com/e/decred-okcoin-present-the-next-10-years-crypto-boom-bust-or-buidl-tickets-57549671617).
* @joshuam [presentation](https://www.youtube.com/watch?v=QeNfs7lUV38) at TABConf 2019, giving an introduction to the Decred cryptocurrency, community and economy/organization.

音频:

* Old Decred Assembly was [uploaded](https://podcasts.apple.com/podcast/decred-assembly-1-0/id1459062074) to Apple Podcast. Thanks to Ryan.


## 社区

截止于 5月2日 的社区数据 :

* Politeia 用户: 167
* Twitter 关注量: 40,456 (+147)
* Reddit 关注用户: 9,425 (+20)
* Matrix 用户: 312 (+28)
* Slack 用户: 6,685 (+46)
* Discord 用户: 2194 (+70), Verified to Post: 199 (+38)
* Telegram 用户: 3,668 (-374)
* YouTube 关注量: 3,771 (+7)
* Facebook 关注: 3,218 (+53), likes: 2,956 (+40)
* LinkedIn 关注: Decred page 515 (+20)
* GitHub dcrd 关注量: 486 (+7), forks: 1,285 (+28)

社交系统新闻：

* Servers hosting matrix.org and riot.im were compromised and taken down on Apr 11 for emergency security maintenance. If your homeserver is matrix.org, change your password. See incident report [here](https://matrix.org/blog/2019/04/11/security-incident/) and tweet timeline [here](https://twitter.com/matrixdotorg/status/1116304867683905537). Interestingly, the hacker [posted](https://github.com/matrix-org/matrix.org/issues/371) generous and somewhat humorous recommendations to the admins on GitHub. Decred's homeserver (matrix.decred.org) was not affected. A good moment to say thanks to our admins who work every day to keep a lot of self-hosted infrastructure running. The incident disrupted our comms for many hours because many people use the browser version of Riot.im client, which was taken offline. To be resilient against such issues, users should consider installing standalone clients (desktop or mobile). Another idea is to [self-host Riot](https://github.com/xaur/decred-issues/issues/62).
* There were multiple interruptions in the chat bridge and many messages were not delivered across the bridge.
* Matrix federation is [moving](https://github.com/matrix-org/matrix-doc/blob/master/proposals/1711-x509-for-federation.md) to stop supporting self-signed certificates and to rely on [Certificate Authorities](https://en.wikipedia.org/wiki/Certificate_authority) to behave.
* Fake account impersonating as "Decred" was detected running giveaways on Facebook. Stay vigilant.
* @degeri joined as a new Reddit moderator to keep r/decred clean from everyday spam. Welcome!

Selected Reddit discussions:

* Does 48% of coins locked in staking result in lower [volatility](https://www.reddit.com/r/decred/comments/bh1erw/decred_has_48_of_coins_lockedup_in_staking/)?
* Decred was [added](https://www.reddit.com/r/decred/comments/bgiqh0/bullish_bitwise_has_updated_their_top_20_mid_cap/) to Bitwise Top 20 Mid Cap Crypto Index
* fintechprof is going '[all-in](https://www.reddit.com/r/decred/comments/biipw3/im_going_allin_on_decred_here_is_why/)' on Decred (with their energy, not by irresponsibly investing their savings/loans), and outlined the reasons for this enthusiastic embrace.
* Decred enthusiasts are heartily [invited](https://www.reddit.com/r/decred/comments/bi387g/new_sub_for_all_things_crypto_staking_decred/) to a new subreddit about crypto staking.
* [Details](https://www.reddit.com/r/decred/comments/b8k2i0/where_can_i_read_about_the_pseudo_random_number/) about the pseudorandom number generator used to select tickets in Decred.
* [Pre-proposal](https://www.reddit.com/r/decred/comments/b84t6b/preproposal_second_constitutional_amendment_to/) suggesting a second constitutional amendment to declare Feb 8 International day of Stakey.
* Perspective on scalability and [blockchain size](https://www.reddit.com/r/decred/comments/bi366i/blockchain_storage_over_time/) over time.
* @jy-p did an [AMA](https://www.reddit.com/r/CryptoCurrency/comments/bjubwv/ama_decred_project_lead_jake_yocompiatt/) on /r/cryptocurrency on May 2 that received 69 total comments.

## 市场

在 4月中 DCR 交易价格为 美金 19.97-26.68 / BTC 0.0045-0.0052。平均日汇率为 24.22 美元。

比特币于 4月3日 突破 5000 美元的关口，大多数其他加密资产像往常一样对美元价格上升，但对BTC价格降低。比特币在本月多次试探 5,500 美元，但最终徘徊在 5,000-5,500 美元之间。

## 相关外部信息

@richardred has collected and [shared](https://github.com/RichardRed0x/crypto-governance-research/tree/master/governance-proposals) comprehensive proposal voting datasets for Decred, Dash and Aragon, and [tweeted](https://twitter.com/RichardRed0x/status/1114552602237313024) some basic statistics like average voter participation for each project. At the time of writing (Apr 6), based on proposals that had finished voting, Decred had an average ticket participation of 76% for on-chain votes and 31% for Politeia proposals; Dash had an average masternode participation of 19% in its Treasury proposals; Aragon had an average ANT token participation of 4.5% voting on Aragon Governance Proposals (this is not directly comparable to Decred/Dash where only tickets/masternodes can vote).

The second round of Aragon AGP voting concluded its 2 day voting window on Apr 27. Nine proposals were voted on, with a mean participation rate of 3.8% of circulating ANT tokens. 6 proposals were accepted, 3 rejected.

Three of the Aragon's proposals concerned Polkadot in some way, after the leaders of Aragon One had stated that they are considering developing a second Aragon application on Polkadot. A proposal to buy some DOTs with the Aragon Association's ETH (with a view to maintaining a parachain and participating in Polkadot governance) was firmly rejected by ANT voters, with just 7% Yes votes. A proposal to affirm Aragon's commitment to Ethereum and stop Aragon One working on Polkadot related development was more narrowly defeated (with 31% Yes votes). This proposal would have caused significant friction between Aragon One and the ANT holder community had it passed, with Luis Cuende stating in an [interview](https://www.coindesk.com/aragon-vote-aims-to-restrict-ethereum-app-from-funding-polkadot-blockchain) that he would have submitted a counter-proposal in the following round of AGP voting. In the third Polkadot-related proposal, 72% of voting ANT approved the Aragon Association to participate in a "lockdrop" for tokens on the forthcoming Edgeware parachain, leaving considerable discretion for the AA to decide how many tokens to lock and how long to lock them for. Another interesting proposal saw the Aragon Association asking for authority to arrange security audits directly (rather than going through the AGP process to vote on these decisions). This was approved with 93% Yes votes, while a proposal from the group that currently performs security audits for continued funding was rejected with 35% Yes votes.

It has been [noted](https://www.evanvanness.com/post/184616403861/aragon-vote-shows-the-perils-of-onchain-governance) that the outcome of several AGP votes was altered by one whale (7th largest ANT wallet, holding 2% of tokens) voting very close to the end of the voting period.

The Dash sporking upgrade process [completed](https://blog.dash.org/product-update-april-5-2019-71344591a5e1) to enable Deterministic Masternode List (which is a requirement for chain locks that will deter PoW majority attacks) and Auto InstantSend. The activation of this spork caused Treasury proposal votes to be reset, and for most of the month it looked as though only a few proposals would reach the required level of votes to be funded. When superblock voting closed on Apr 29 voter participation rates were back to within their normal range and 15 proposals met the requirement. 660 DASH remained to be spent in the superblock, and is now lost to the Dash Treasury, but this level of underspend is not particularly uncommon. Among the [proposals](https://github.com/RichardRed0x/crypto-governance-research/blob/master/governance-proposals/dash-proposals.csv) were two from rival PR firms, Wachsman and Shift; until this point Dash Core Group had arranged such services directly at their discretion, and had been retaining the services of Wachsman. The Shift proposal, costing $10K per month as a retainer, passed with 536 Yes votes (90% Yes, but only 52 votes over the quorum requirement), while the Wachsman proposal was rejected with a score of -206 (more No votes than Yes votes).

The EOS constitution has been replaced with a new [user agreement](https://github.com/eosnewyork/eosuseragreement/blob/master/README.md), proposed on chain by [EOS New York](https://medium.com/eos-new-york/the-eos-user-agreement-has-been-proposed-on-chain-61bf3760b604) and [approved](https://eosauthority.com/approval/view?scope=eosnewyorkio&name=eosuseragree&lnc=en) by the 21 Block Producers. This change had been put to EOS holders in a [referendum](https://eosauthority.com/polls_details?proposal=eosuseragree_20190207&lnc=en). The referendum has a long duration (3 months) and is not due to finish until May 8, there is strong support for the proposal (98% Yes) but voter participation is very low (1.7%). EOS referendums had a notional quorum requirement of 15%, but in light of the fact that none of the polls are even close to reaching that level of participation, it seems like the BPs have decided to bypass the formal referendum process and move forward with some of the proposed changes. The EOS BPs also [approved](https://twitter.com/zeroxeos/status/1118833569118466048) the deployment of REX (Resource Exchange), but it [failed](https://www.reddit.com/r/eos/comments/bekd4f/rex_is_here_status_approved_by_15_bp/) execution on chain and will have to be re-proposed.

Aeternity is [planning](https://blog.aeternity.com/aeternity-first-on-chain-governance-vote-decentralization-2-0-5e0c8a01891a) to hold its first on-chain governance vote May 7-14. The proposal to be voted on is establishing a "Block Reward Initiative (BRI), through which ~0-20% of miner rewards will be allocated to development". The announcement post references Aeternity's ICO funds as being sufficient to fund development for years to come, and positions the BRI as a transition to a self-sustaining platform. BRI funds would be given to a charitable foundation registered in Liechtenstein, and administered by a technical council. AE token holders will vote for 0, 5, 10, 15 or 20% of the block rewards to go to this foundation - as long as more than 50% of AE votes for a share greater than 0%, the percentage will be set using a weighted average of the votes for options greater than 0%. This will leave some AE holders who don't want the block reward funding with a difficult choice of whether to vote for 0% and hope to be in the majority (and otherwise be ignored) or to vote for 5% to lower the weighted average in the case that the proposal is approved.

Ycash, a "friendly fork" of Zcash, was [announced](https://forum.zcashcommunity.com/t/announcing-ycash-the-first-friendly-fork-of-the-zcash-blockchain/33162). Ycash will build off a snapshot of the Zcash chain, and will diverge in two ways (replacing the current 20% Founders Reward with a perpetual 5% reward going to a newly created Ycash foundation, and switching the PoW mining algorithm to something more conducive to mining on commodity hardware) while aiming to incorporate future improvements from Zcash. Zooko Wilcox wrote a [blog post](https://z.cash/blog/future-friendly-fork/) about "A Future Friendly Fork" in 2017, and this appears to have inspired the positioning of Ycash as a friendly fork. Zooko has also commented on the Ycash post to say that he sees Ycash as a positive development for Zcash.

The Zcash Foundation [announced](https://www.zfnd.org/blog/kzen-multisig/) funding for a research project with KZen Networks to enable private n-of-n multisig transactions for Sapling Zcash without requiring a consensus change. The effort is related to KZen's work on [threshold signatures](https://www.kzencorp.com/post/threshold-signatures-private-key-the-next-generation), which are similar to multisig but are indistinguishable from regular signatures.

"Maker DAO" was the subject of some controversy this month, initially with an ongoing [issue](https://www.coindesk.com/makerdao-set-to-increase-dai-fees-above-15-in-bid-to-stabilize-stablecoin) with the DAI peg to USD (with frequent stability increases lately failing to restore the peg) and then with some leaked information about [conflict](https://www.coindesk.com/darkest-days-yet-purple-pill-tell-all-details-years-long-rift-at-heart-of-makerdao-stablecoin-project) within the Maker team. [Zandy's story](https://www.scribd.com/document/407743542/Zandy-s-Story#from_embed) provides an interesting look into the history of Maker and the origins of the Maker Foundation as a last-minute move to avoid a hefty tax bill, and a subsequent falling out of the parties involved, with secret communications channels, a "purple pill" roadmap to try and resolve the conflict, board members being fired and having to relinquish their private multisig keys, and a [leaked letter](https://www.coindesk.com/leaked-letter-exposes-infighting-atop-flagship-ethereum-project-makerdao) that exposed the whole thing.

Zcoin [announced](https://zcoin.io/further-disclosure-on-zerocoin-vulnerability/) a vulnerability with the Zerocoin protocol that allowed forged coins to be created ("not exceeding 1% of the circulating supply"). Details are to be released later, once other projects exposed to a flaw with the cryptography of Zerocoin (PIVX, Veil and Gravity Coin) have had a chance to mitigate the issue. The Zcoin team called for Zerocoin spends to be disabled on Apr 9 when they detected the issue, and in this post on Apr 26 confirmed that it will remain disabled for Zcoin as they are working on a replacement (Sigma) which is nearly ready.

In [part 4](https://blog.0xproject.com/0x-roadmap-2019-part-4-proposal-for-stake-based-liquidity-incentive-52c16558df29) of the 0x Roadmap [ZEIP-31](https://github.com/0xProject/ZEIPs/issues/31) was proposed, which would add incentives for market makers to hold the ZRX token. This is in response to a lack of correlation between users of 0x and ZRX token holders. ZRX is designed to be used to govern the protocol, which is unlikely to work well in a scenario where the main users do not hold any ZRX. The proposal is at the start of a long process to develop and audit the new smart contracts then hold a tokenholder vote to approve/reject the integration of the changes.

Bitcoin (Cash) Satoshi's Vision (BSV) has been [delisted](https://www.coindesk.com/kraken-exchange-joins-binance-shapeshift-in-delisting-bitcoin-sv) by a number of exchanges as part of an ongoing feud between Craig S Wright and some members of the Bitcoin community. Ironic that the poor behavior of a very visible front man is causing so much trouble for BSV.

Bitfinex encountered some [trouble](https://bitcoinmagazine.com/articles/bitfinex-faces-legal-action-from-ny-attorney-general-heres-what-this-means/) from the New York Attorney General's office, in the form of a request for a court order to investigate transactions between certain legal entities relating to Bitfinex and Tether. Specifically, the NY AG alleges that Bitfinex lost some $850 million held by Crypto Capital (they claim it has been frozen), and borrowed from Tether reserves in order to keep Bitfinex operational. Tether [updated](https://news.bitcoin.com/while-tether-withdraws-claim-of-usd-backing-rival-stablecoins-provide-monthly-attestations/) their terms on [Feb 26](https://archive.today/yw7nb), adding that it may now back USDT by assets other than USD and delay the redemption or withdrawal because of poor liquidity or unavailability of the assets.

QuadrigaCX declared [bankrupt](https://cointelegraph.com/news/canadian-crypto-exchange-quadrigacx-officially-declared-bankrupt) after months of uncertainty.

A critical flaw was [discovered](https://motherboard.vice.com/en_us/article/zmakk3/researchers-find-critical-backdoor-in-swiss-online-voting-system) in Switzerland's Internet Voting System (missed from March), which is scheduled to be used in elections this year. The flaw would allow someone to alter votes undetected. Cory Doctorow [wrote](https://boingboing.net/2019/03/13/principal-agent-problems.html) about this as exposing issues with Internet voting around the auditing process and NDAs which cover code and silence criticizm from security researchers.

The G20 members will [meet](https://cointelegraph.com/news/g20-to-establish-crypto-aml-and-counter-terrorism-financing-regulations-in-june-report) in Japan in June and plan to agree on a framework to combat crypto-enabled money laundering and terrorism financing - with the main aim being anti-anonymity and the identification of individuals transacting in crypto-assets at the moment of transaction.

Researchers have [shown](https://gadgets.ndtv.com/laptops/news/intel-visa-sa-00086-exploit-researchers-computer-data-access-2014854) that a testing utility bundled with Intel chips (Intel VISA) can allow an attacker to capture data from the CPU.

Former Mozilla exec [accused](https://www.zdnet.com/article/former-mozilla-exec-google-has-sabotaged-firefox-for-years/) Google of sabotaging Firefox for years - through a long series of "mistakes" which led Google products to have issues in Firefox browser.

When it comes to privacy, New York Times has a good [sense of humor](https://twitter.com/Pinboard/status/1116354502032932865) - stuffing the "Privacy Project" homepage to the gills with third-party tracking scripts.


## 关于月报
四月为英文第13期 [GitHub](https://xaur.github.io/decred-news/journal/201903) 月报。点击[这里](https://xaur.github.io/decred-news/)浏览所有往期月报，翻译等。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues) 和 [Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

感谢 (按字母排序): bee, degeri, Dustorf, elian, guang, Haon, issedjur, liz\_bagot, lukebp, lustosa, matheusd, richardred, s\_ben, saender, sambiohazard.

## 中文社区

* [微博](https://www.weibo.com/DecredProject)
* 微信公众号：Decred中文社区
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

感谢 (按字母排序): 
