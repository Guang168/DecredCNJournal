# Decred月报 – 2021年5月

![abstract art by @saender](img/202105.1.github.png)

_图片:@saender_

五月亮点：

- 新国库已经开始接收区块奖励，并且已经批准和释放了第一笔交易进行了测试。
- 节点和钱包软件版本 1.6.3 已发布，以修补 VSP 质押的一些问题以及添加了一些最新功能。
- DCRDEX v0.2.0 发布，包含超过 3 个月的工作，并且实验性的将 DCRDEX 集成到 Decrediton v1.6.3中。

内容:

- [v1.6.3 补丁发布](#v163-patch-release)
- [新国库启动](#new-treasury-activated)
- [开发仅占总结](#development)
- [人员](#people)
- [治理](#governance)
- [网络](#network)
- [生态系统](#ecosystem)
- [外展](#outreach)
- [媒体](#media)
- [社区讨论](#discussions)
- [市场](#markets)
- [相关外部信息](#relevant-external)

## v1.6.3 补丁发布

最新版本的 GUI 钱包 Decrediton 修复了 VSP 质押问题，并集成了新版本的[DCRDEX](#dcrdex)。命令行 dcrwallet 也随着 VSP 修复和改进而更新。

Decrediton 用户请注意：

- DEX 选项卡仅在全节点模式下显示，在 SPV 模式下隐藏
- 需要运行 Bitcoin Core 并使其完全同步才能使用 DEX 
- Windows版本已更新以修复默认比特币目录的[错误](https://github.com/decred/decrediton/pull/3469)，如果您在 5 月 25 日之前获得安装程序，请重新下载并重新安装

请在[此处](https://github.com/decred/decred-binaries/releases/tag/v1.6.3)查看完整的发行说明和下载。与往常一样，请验证[程序签名](https://docs.decred.org/advanced/verifying-binaries/)以确保你运行的是未被篡改的二进制文件。

## 新国库启动

新共识规则于 5 月 8 日启动。从区块[552,448](https://explorer.dcrdata.org/block/00000000000000001c6fc262b2673d94827f87daa329b0bdeb7866562ef919cf)开始，10% 的区块奖励流向新的[国库账户](https://explorer.dcrdata.org/treasury)，不再流向[旧地址](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)。

主要区别在于新国库账户由 Decred 利益相关者控制。来自旧地址的支出只需要由 Decred Holdings Group LLC（“DHG”）签署交易，这是一家为引导 Decred 而创建的传统公司实体。新国库只有当利益相关者投票批准一项特殊的“国库支出”交易（“tspend”）时，支出才有可能。

[Decred Change Proposal 6](https://github.com/decred/dcps/blob/master/dcp-0006/dcp-0006.mediawiki) （Decred共识变更DCP） 中指定了一个复杂的投票过程来支持它，并在软件版本 v1.6 中实现。简单来说的步骤是：

- Politeia 创建符合某些要求的 tspend 交易
- 交易被发布到内存池，投票钱包开始对其进行投票
- 投票最多持续 12 天，但如果结果无法被任何剩余投票改变，则可以在大约 7 天内通过
- 在此期间被召集最多 17,280 张票可以进行 tspend 投票（以及正常的区块批准和共识升级投票）
- 如果投票通过，交易将被包含在一个区块中（最多1天后），并支付给承包商

新的国库系统在激活后很快就在主网上成功测试。5 月 10 日，利益相关者被[通知](https://twitter.com/decredproject/status/1391877816292151296)配置他们的投票钱包。然后在 5 月 12 日，一个小的测试 tspend [交易](https://explorer.dcrdata.org/tx/7507bcc72bfde895065034e12e6d462f2360163cd0c879f0db35514f9456b2c1)被广播到网络。最近的投票窗口是 5 月 13 日至 24 日，但在 9 天内累积 6,755 票赞成和 1 票反对后，投票支付。在此期间有机会投票的 12,550 张选票中，54% 的人积极投票。tspend 是在区块[556,416](https://explorer.dcrdata.org/block/000000000000000000b8bed4b8511e3c5197d3eee6372db2ba199481e14d5376)中开采的。

从软件版本 v1.6.3 开始，tspend 投票仅支持 24/7 全天候运行投票钱包的“solo投票者”（截至 6 月 1 日，约占所有利益相关者的 77%）。

国库支出投票将成为支付构建 Decred 人员的重要月度流程。[建议](https://twitter.com/decredproject/status/1391877959410233344)solo选民通过使用以下命令配置他们的投票钱包来为即将到来的 tspend 投票做准备：

    dcrctl --wallet settreasurypolicy "03f6e7041f1cf51ee10e0a01cd2b0385ce3cd9debaabb2296f7e9dee9329da946c" "yes or no"

此命令表示您对当前03f6e704...资金管理及其密钥的信任，并设置您的钱包将投票支持由其签名的 tspend。您可以在[DCP-0006](https://github.com/decred/dcps/blob/master/dcp-0006/dcp-0006.mediawiki)或[源代码](https://github.com/decred/dcrd/blob/master/chaincfg/mainnetparams.go#L389)中验证此密钥。通过这种一次性配置，投票是半自动的，但是当需要更精细的控制时，可以对单个 tspend 交易进行投票。

祝贺所有拥有这一里程碑的利益相关者，并感谢所有[贡献者](https://twitter.com/matheusd_tech/status/1390981711736053760)使其成为现实！

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以[构建和运行](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c)的源代码中，但对于普通用户来说，还不能使用。

<a id="dcrd" />

**[dcrd](https://github.com/decred/dcrd)**

- 将用于处理[签名](https://github.com/decred/dcrd/pull/2642)标准脚本的代码移动到其自己的子代码中，以便为将来将标准脚本处理与共识关键代码分开做准备
- 更新了 OpenBSD [rc 脚本](https://github.com/decred/dcrd/pull/2646)
- 重新设计应用程序[版本](https://github.com/decred/dcrd/pull/2651)处理以从单个字符串解析它，这更易于管理且更防错
- 收到[SIGHUP](https://github.com/decred/dcrd/pull/2645)信号时执行正常关机
- 将脚本[版本](https://github.com/decred/dcrd/pull/2650)添加到gettxoutRPC的结果中。将来引入新版本时，脚本版本将变得更加重要。
- 在 UTXO 数据库之前将块数据库[刷新](https://github.com/decred/dcrd/pull/2649)到磁盘，以确保后者在非正常关机后可以恢复
- 重新设计[UTXO](https://github.com/decred/dcrd/pull/2652)相关逻辑以更好地分离关注点。这使得流程更容易遵循，并为优化 UTXO 数据库铺平了道路。

<a id="dcrwallet" />

**[dcrwallet](https://github.com/decred/dcrwallet)**

合并在 master 和 v1.6.3 版本中：

- 改进了用于创建额外[拆分交易](https://github.com/decred/dcrwallet/pull/2034)的方法，以修复购买选票时的余额不足错误
- 修复了支付 VSP 费用时的[输入选择](https://github.com/decred/dcrwallet/pull/2035)，解决了两个错误：一个是未使用预期输入并可能保持锁定状态，另一个是 VSP 费用可能从错误的帐户中支付，这可能会降低混币钱包的隐私性
- 确保预期的钱包[帐户](https://github.com/decred/dcrwallet/pull/2037)用于支付 VSP 费用并在同步失败的 VSP 选票时接收找零
- 多个修复程序，用于跟踪有关费用支付安排、错误处理、撤销和过期费用交易的 VSP 管理的选票
- 确保[没有重复](https://github.com/decred/dcrwallet/pull/2042)的费用支付，并且所有费用都由 VSP 客户端跟踪
- 收到[SIGHUP](https://github.com/decred/dcrwallet/pull/2039)信号时执行正常关机
- 添加了一个新的 gRPC 端点，用于公开VSP 客户端[跟踪](https://github.com/decred/dcrwallet/pull/2040)的选票和费用（由 Decrediton 使用）

合并到 master:

- 已实现的[`gettxout`](https://github.com/decred/dcrwallet/pull/1903)方法返回有关未花费交易输出的信息，这是 DCRDEX 在SPV 模式下操作 DCR 钱包所必需的
- 实现cfilters([紧凑块过滤器](https://bitcoinops.org/en/topics/compact-block-filters/))。这些类似于 dcrd 的实现，并且还使 DCRDEX 能够在 SPV 模式下管理 DCR。

<a id="decrediton" />

**[Decrediton](https://github.com/decred/decrediton)**

合并在 master 和 v1.6.3 版本中：

- 允许在隐私钱包中的账户之间[发送](https://github.com/decred/decrediton/pull/3446)资金（混合账户除外）
- 仅在[需要](https://github.com/decred/decrediton/pull/3457)时显示“处理托管选票”视图
- 修复了启动时显示的空白页面而不是[加载栏](https://github.com/decred/decrediton/pull/3449)
- 修复了错误的密码短语，允许[跳过](https://github.com/decred/decrediton/pull/3454)帐户安全迁移
- 固定钱包帐户锁定以防止锁定正在处理 VSP 选票的帐户，但也锁定任何不再需要[解锁](https://github.com/decred/decrediton/pull/3453)的帐户
- 始终使用 Lodash 进行[类型检查](https://github.com/decred/decrediton/pull/3135)
- 修复了当自动购票处于隐私模式时[未解锁](https://github.com/decred/decrediton/pull/3476)的未混合和更改帐户
- 修复了 Windows 上的默认比特币[目录](https://github.com/decred/decrediton/pull/3469)

合并到 master:

- 固定处理[零](https://github.com/decred/decrediton/pull/3468)“要维持的余额”值
- 引入了[预加载脚本](https://github.com/decred/decrediton/pull/3397)，并使用`invoke/handle`. 这是隔离所有 Node 相关调用的第一步，以便可以关闭主 UI 代码的 Node 集成。

![DEX in Decrediton](img/202105.2.380.png)

<a id="politeia" />

**[Politeia](https://github.com/decred/politeia)**

在对新存储后端和新 API 进行大规模升级后，大部分工作都致力于更新 UI 代码、测试和修复错误。

- 更新了[关于Politeia](https://github.com/decred/politeiagui/pull/2378)副本
- 将提案令牌放入电子邮件通知[主题](https://github.com/decred/politeia/pull/1417)
- 在整个 UI 代码库中始终如一地处理[简短](https://github.com/decred/politeiagui/pull/2365)的提案令牌
- 修复了多条[评论](https://github.com/decred/politeiagui/pull/2384)相关的 UI 错误
- 修复了初始 UI 加载期间的[闪烁](https://github.com/decred/politeiagui/pull/2395)
- ~2 个其它后端和 ~14 个 UI 错误修复
- 修复了[单元](https://github.com/decred/politeiagui/pull/2364)测试和[端到端](https://github.com/decred/politeiagui/pull/2383)测试以使用新的后端 API
- 依赖升级、代码清理、API 增强

承包商管理系统（CMS）：

- 将发票同行评审[可见性](https://github.com/decred/politeia/pull/1351)从基于作者的域更改为基于发票的行项目域。这将允许承包商审查其域中的所有计费工作，即使它来自其它域的承包商。当前的领域是开发、研究、设计和营销。
- 添加了更多电子邮件[通知](https://github.com/decred/politeia/pull/1353)：“一旦国库的支出完全自动化，及时提交发票将变得更加重要，因此需要进一步唠叨。”
- 文档更新和代码清理
- ~4 个后端和 ~1 个 UI 错误修复

Politeia v1.0.1 [已发布](https://github.com/decred/politeia/releases/tag/v1.0.1)，包括上述所有后端修复和改进。

现在可以在[里程碑](https://github.com/decred/politeia/milestones)页面上跟踪 v1.1.0 的进度。

<a id="vspd" />

**[vspd](https://github.com/decred/vspd)**

- 将选票和费用交易的区块浏览器[链接](https://github.com/decred/vspd/pull/247)添加到 UI
- 为状态响应添加了最佳块[高度](https://github.com/decred/vspd/pull/254)（用于检测停滞的 VSP）
- 为所有已确认的选票填充[购买高度](https://github.com/decred/vspd/pull/250)并将其显示在管理页面上
- 改进的管理页面[视觉](https://github.com/decred/vspd/pull/263)效果
- 添加了数据库[升级](https://github.com/decred/vspd/pull/242)框架
- 从请求处理失败中[恢复](https://github.com/decred/vspd/pull/255)时改进日志记录
- 添加了最大日志大小和最大日志文件的[配置](https://github.com/decred/vspd/pull/249)参数以保留
- 从数据库中[删除](https://github.com/decred/vspd/pull/260)确认的费用交易，将磁盘使用量减少约 2 倍
- 将每张票存储在其自己的[数据库存储桶](https://github.com/decred/vspd/pull/243)中。结合之前的优化，它允许将大约 40% 的磁盘使用率提高大约 50% 的插入速度和大约 85% 的票证迭代速度。

<a id="dcrstakepool" />

**[dcrstakepool](https://github.com/decred/dcrstakepool)**

- 修复了 dcrstakepool（旧版 VSP 软件）和 dcrwallet v1.6.3 在一些罕见配置中的[不兼容](https://github.com/decred/dcrstakepool/pull/636)问题

<a id="dcrpool" />

**[dcrpool](https://github.com/decred/dcrpool)**

- 不要尝试使用比预期[新的](https://github.com/decred/dcrpool/pull/326)数据库版本运行
- 处理`SIGTERM` 和 `SIGHUP`关闭信号

第三个 v1.2.0 发布[候选](https://github.com/decred/dcrpool/releases/tag/v1.2.0-rc3)修复了自 RC2 以来发现的问题，但 coinbase 确认失败仍未解决。当团队正在探索解决方案时，发布被推迟到另行通知。

<a id="dcrdex" />

**[DCRDEX](https://github.com/decred/dcrdex)**

DCRDEX v0.2.0 has been released! It incorporates more than 3 months of work since the v0.1.5 release. The most notable changes are:

- UI and usability enhancements including responsive design and interactive depth chart
- support for client control by Decrediton and use of its accounts
- account import/export
- experimental Bitcoin Cash (BCH) support

Check Important Notices and the full list of changes in the [release notes](https://github.com/decred/decred-binaries/releases/tag/v1.6.3#dcrdex-v020). The [DEX page](https://dex.decred.org/) guides through simplified installation steps. More advanced users can get the binaries [here](https://github.com/decred/decred-binaries/releases/tag/v1.6.3#downloads-v163) and install them manually. Don't forget to [verify](https://docs.decred.org/advanced/verifying-binaries/) the downloads to ensure they came unmodified.

Merged in master:

- initial server-side [Ethereum](https://github.com/decred/dcrdex/pull/979) asset support
- disallow [changing](https://github.com/decred/dcrdex/pull/1055) to a wallet that cannot settle user's active trades
- fixed an elusive and long-standing issue with updating [score](https://github.com/decred/dcrdex/pull/1083) for offline users
- updated to [latest](https://github.com/decred/dcrdex/pull/953) dcrd and dcrwallet packages

A lot of exciting work towards the [0.3 milestone](https://github.com/decred/dcrdex/milestone/12) is in progress, most notably Ethereum and SPV.

<a id="dcrandroid" />

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

- disallow sending from [unmixed](https://github.com/planetdecred/dcrandroid/pull/541) accounts
- added password input [delays](https://github.com/planetdecred/dcrandroid/pull/542) to resist brute-force attacks
- show [staking](https://github.com/planetdecred/dcrandroid/pull/543)-related transactions on the Overview page
- updated [dependencies](https://github.com/planetdecred/dcrandroid/pull/546) and replaced usages of "CoinShuffle++" with "StakeShuffle"
- keep the [display on](https://github.com/planetdecred/dcrandroid/pull/553) until the mixing is completed or canceled
- show rich text [formatting](https://github.com/planetdecred/dcrandroid/pull/557) for Politeia proposals (without using WebView)
- updated Chinese and French translations
- fixed [watch-only](https://github.com/planetdecred/dcrandroid/pull/560) wallet being listed as a source when sending funds

Merged in [dcrlibwallet](https://github.com/planetdecred/dcrlibwallet) shared library:

- added code for fetching proposal [description](https://github.com/planetdecred/dcrlibwallet/pull/192) and switched from saving proposal files to loading them on demand
- integrated a signed TLS [certificate](https://github.com/planetdecred/dcrlibwallet/pull/193) for [cspp.decred.org](https://cspp.decred.org/) which is required when using mainnet
- fixed bugs with balance and Politeia integration

<a id="dcrios" />

**[dcrios](https://github.com/planetdecred/dcrios)**

- implemented [Privacy mode](https://github.com/planetdecred/dcrios/pull/727) with guided setup of the mixer
- show [USD equivalent](https://github.com/planetdecred/dcrios/pull/746) of wallet's DCR balance on the Overview page
- added password input [delays](https://github.com/planetdecred/dcrios/pull/749) to resist brute-force attacks
- when there is more than one wallet on the Overview page, show [which wallet](https://github.com/planetdecred/dcrios/pull/776) the transactions belong to
- show more specific [notifications](https://github.com/planetdecred/dcrios/pull/766) for staking transactions (ticket voted or revoked)
- show rich text [formatting](https://github.com/planetdecred/dcrios/pull/773) for Politeia proposals (without using UIWebView)
- fixed incorrect list of [accounts](https://github.com/planetdecred/dcrios/pull/765) to send from
- added support for iOS 11
- ~17 bug fixes and UI tweaks

<a id="godcr" />

**[godcr](https://github.com/planetdecred/godcr)**

- implemented pages: [Tickets](https://github.com/planetdecred/godcr/pull/395) overview, [Tickets list](https://github.com/planetdecred/godcr/pull/406), and [Restore wallet](https://github.com/planetdecred/godcr/pull/386)
- implemented the [Max](https://github.com/planetdecred/godcr/pull/396) button for setting the maximum DCR amount that can be sent
- added the submission of input fields with pressing [Enter](https://github.com/planetdecred/godcr/pull/414)
- added [loading](https://github.com/planetdecred/godcr/pull/400) animations to some modals
- initial [dark mode](https://github.com/planetdecred/godcr/pull/401) support
- added language [translation](https://github.com/planetdecred/godcr/pull/426) infrastructure
- ~14 bug fixes

Elias Naur (creator of the Gio library that powers godcr) has kindly reviewed the UI code and shared his [recommendations](https://paste.sr.ht/~eliasnaur/cea1d29d6a5f96668b5e166c2f39ef596974574f). Issues were created to address them, and some are already completed (e.g. [#409](https://github.com/planetdecred/godcr/issues/409), [#411](https://github.com/planetdecred/godcr/issues/411), [#416](https://github.com/planetdecred/godcr/issues/416)).

![godcr](img/202105.3.628.png)

<a id="dcrdata" />

**[dcrdata](https://github.com/decred/dcrdata)**

- [initial version](https://github.com/decred/dcrdata/pull/1824) of the new [`/treasury`](https://dcrdata.decred.org/treasury) page
- [show](https://github.com/decred/dcrdata/pull/1827) treasury spend transactions on the [mempool](https://dcrdata.decred.org/mempool) page, tspend Yes/No votes on the ticket vote transaction page, and vote tally on tspend's own transaction page
- added a simpler endpoint to query [exchange rates](https://github.com/decred/dcrdata/pull/1826)
- added the share of [mixed](https://github.com/decred/dcrdata/pull/1825) coins to the [homepage](https://dcrdata.decred.org/) (under Distribution)

<a id="dcrdocs" />

**[docs](https://github.com/decred/dcrdocs)**

- removed [inline HTML](https://github.com/decred/dcrdocs/pull/1168) for images - a step towards packaging all docs as a single [PDF file](https://github.com/decred/dcrdocs/issues/923)
- several updates regarding [vspd](https://github.com/decred/dcrdocs/pull/1171) staking

<a id="dcrweb" />

**[decred.org](https://github.com/decred/dcrweb)**

- [`/release`](https://decred.org/release/) page [updated](https://github.com/decred/dcrweb/pull/982) for v1.6.3
- improved [SEO tags](https://github.com/decred/dcrweb/pull/979)
- removed [inactive](https://github.com/decred/dcrweb/pull/990) contributors
- [updated](https://github.com/decred/dcrweb/pull/957) [`/exchanges`](https://decred.org/exchanges/) page
- added [hardware wallets](https://github.com/decred/dcrweb/pull/989) section on the [`/wallets`](https://decred.org/wallets/) page

Other:

- Bug Bounty Program [update](https://bounty.decred.org/2021/05/status-update/): a total of 180 submissions processed so far, with 16 of them being eligible for a payout
- a lightweight Jekyll [theme config](https://github.com/decredcommunity/jekyll-themes) was extracted into its own repo for reuse. It allows to publish a few Markdown pages without third party tracking scripts. You can see it in action on mini-websites for [events](https://decredcommunity.github.io/events/index/), [proposals](https://decredcommunity.github.io/proposals/) and [social-media-stats](https://decredcommunity.github.io/social-media-stats/) projects.
- translations require continuous maintenance. Join the [#translations](https://chat.decred.org/#/room/#translations:decred.org) chat room to coordinate with the other translators and developers.

## People

Welcome to new first time contributors with code merged to master: @LasTshaMAN ([politeia](https://github.com/decred/politeia/commits?author=LasTshaMAN))!

Community stats as of Jun 1:

- [Twitter](https://twitter.com/decredproject) followers: 45,724 (+1,333)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 11,190 (+203)
- [Matrix](https://chat.decred.org/) #general users: 467 (+33)
- [Discord](https://discord.gg/GJ2GXfz) users: 1,787 (+221)
- [Telegram](https://t.me/Decred) users: 2,705 (+60)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,540 (+40), views: 186K (+4K)
- GitHub [dcrd](https://github.com/decred/dcrd) stars: 598 (+7), forks: 255 (+1)

May's recap of interesting social media dynamics [is out](https://decredcommunity.github.io/social-media-stats/posts/20210604.1), now with tables for easier reading. Feedback is appreciated to understand how valuable these reports are.

All-time community growth charts have been tweaked, updated, and moved to a new location [here](https://decredcommunity.github.io/social-media-stats/docs/charts).

## Governance

In May Decred Treasury received 11,342 DCR (2,564 to the [old address](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx), and 8,778 to the [new system](https://explorer.dcrdata.org/treasury)) worth $1.97M at May's average rate of $173.47. No DCR was spent in May. On Jun 2, 698 DCR was spent from the legacy address for April invoices, worth $121K at May's rate, or $139K at April's billing rate of $198.60. As of Jun 3, combined Treasury balance is 683,438 DCR (107 million USD at $156).

May saw 1 proposal submitted and approved, the proposal for continued development of Politeia (detailed [last month](202104.md)) had 98.4% approval and turnout of 44%.

Treasury charts have been [added](https://twitter.com/_Checkmatey_/status/1392266971228430338) on [checkonchain.com](http://checkonchain.com/) to assist with governance decisions around expenses.

## Network

**Hashrate**: May's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=ko2vefoc-kpf16yhd&scale=linear&bin=block&axis=time) opened at ~418 Ph/s and closed ~351 Ph/s, bottoming at 234 Ph/s and peaking at 497 Ph/s throughout the month.

There appears to be a correlation between the Dec-Apr price rally from ~25 to ~200 USD and the hashrate rise from ~350 to 450-550 Ph/s. Then in the opposite direction, Apr 17-23 price correction happened along hashrate drop from ~450 to ~250 Ph/s. Most recently, May 10-23 hashrate decline correlated with price drop from ~200 to ~110 USD.

Distribution of hashrate [reported](https://miningpoolstats.stream/decred) by the pools on Jun 1: Poolin 39%, F2Pool 17%, Antpool 3%, BTC.com 1.6%, Luxor 1.3%, Huobipool 0.4%, UUPool 0.1%, Coinmine 0.05%, okex 0.01%, others 38%.

Distribution of 1,000 actually [mined blocks](https://miningpoolstats.stream/decred) almost matches the reported hashrate. Unidentified mined blocks are split between 4 addresses: [Dsacz](https://explorer.dcrdata.org/address/DsaczRtjC31N6XVV69qcBoyR2BEEmjRDay3) 25%, [DsR4G](https://explorer.dcrdata.org/address/DsR4GSVsMxShvk6dpod9DBTbX7DuZhE2jjs) 7%, [DsbNN](https://explorer.dcrdata.org/address/DsbNNnupnCWd9MrHycs1NvwrtfhSYKF6ZGB) 4%, and [DsaWD](https://explorer.dcrdata.org/address/DsaWDBxVjxtV1ugqXsV3PGmAD4jLwryvSX3) 0.2%.

**Staking**: [Ticket price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=ko2vefoc-kpf16yhd&axis=time&visibility=true-true&mode=stepped) varied between 173-198 DCR, with 30-day [average](https://dcrstats.com/) at 183.7 DCR (-2.1).

The [locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=ko2vefoc-kpf16yhd&scale=linear&bin=block&axis=time) was 7.39-7.62 million DCR, meaning that 57.2-58.7% of the circulating supply [participated](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=ko2vefoc-kpf16yhd&scale=linear&bin=block&axis=time) in proof-of-stake.

**VSP**: On Jun 1, 8.2K (+1.1K) live tickets were managed by vspd servers and 1.1K (-1.1K) by the [still listed](https://decred.org/vsp/) legacy dcrstakepool servers. Collectively the 12 legacy and 13 new VSPs managed 22.5% of the ticket pool. The recently delisted but still active legacy VSPs managed 61 live tickets.

On May 14 it was [discovered](https://github.com/decred/dcrwebapi/issues/138) that 4 legacy VSPs have not upgraded to the new consensus rules and got forked off the network on May 8, while holding ~350 tickets of their clients. All but one have eventually upgraded to continue serving their tickets, while [stakepool.dcrstats.com](https://stakepool.dcrstats.com) changed to maintenance mode and stopped reporting the stats. The status of its 77 live tickets is unknown as of Jun 8.

**Nodes**: Throughout May there were around 215 reachable nodes according to [dcrextdata](https://dcrextdata.planetdecred.org/nodes).

Node versions as of Jun 1 [snapshot](https://nodes.jholdstock.uk/user_agents) (252 total, dcrd only): v1.6.2 - 42%, v1.6.0 - 21%, v1.6.1 - 17%, v1.7 dev builds - 8%, v1.6 dev builds 4%, v1.5.2 - 3%, v1.5.1 - 2.7%, v1.5.0 - 0.8%.

## Ecosystem

Welcome the new [vspd](https://github.com/decred/vspd) instance [123.dcr.rocks](https://123.dcr.rocks/) from [@thefrankbraun](https://twitter.com/thefrankbraun). Service fee is 0.49% and voting wallets are [located](https://twitter.com/thefrankbraun/status/1389014142095437825) in 3 data centers on 2 continents. Since it was listed on May 1, the service has already voted ~430 tickets and manages ~650 live tickets as of Jun 8.

Legacy VSP [dcrpool.dittrex.com](https://dcrpool.dittrex.com) was [removed](https://github.com/decred/dcrwebapi/pull/140) from the [listing](https://decred.org/vsp/) but is still online watching its last 1 live ticket. The service has voted 800+ tickets since [Nov 2018](https://github.com/decred/dcrwebapi/pull/48). The replacement vspd instance from Dittrex is up, [waiting](https://github.com/decred/dcrwebapi/pull/133) its first voted ticket to get added to the list.

Not all exchanges handled Decred's 6th consensus upgrade smoothly:

- Binance has upgraded in advance and was not affected by the fork when it happened
- Bittrex got stuck at block [552,447](https://explorer.dcrdata.org/block/552447) - last block adhering to the old consensus rules. Their [status page](https://global.bittrex.com/Status) reported that DCR wallet was disabled and under "Wallet Maintenance", which changed to "Normal" on around May 13.
- Poloniex [tweeted](https://twitter.com/PoloSupport/status/1390916088397852675) that their DCR wallet was disabled for "maintenance" (~4 hours after the consensus upgrade), and [tweeted](https://twitter.com/PoloSupport/status/1395727656251973639) again on May 21 that it was re-enabled

Since around May 17, Ledger Live users have been reporting issues with syncing and sending their DCR. Last update on Ledger's [incident page](https://status.ledger.com/incidents/j1sypv88pgs6) says the fix was being tested on May 20, but their Jun 3 [tweet](https://twitter.com/Ledger_Support/status/1400429510827388929) confirms the issue is still unresolved. As of Jun 8, the [status page](https://status.ledger.com/) reports an outage for DCR and a 75% uptime over the past 90 days.

The following services have been [removed](https://github.com/decred/dcrweb/pull/957) from [decred.org](https://decred.org/exchanges/):

- [instaex.io](https://instaex.io/) - website is down
- [fexpro.net](https://fexpro.net/) - certificate errors
- [changenow.io](https://changenow.io) - DCR trading pair [unavailable](https://github.com/decred/dcrweb/pull/988) for 3+ months
- [transak.com](https://global.transak.com/) - [no longer](https://github.com/decred/dcrweb/issues/984) seems to support buying DCR
- 6 OTC desks [removed](https://github.com/decred/dcrweb/issues/983) as none of them were actively quoting DCR

[MarketplaceGOLD](https://marketplacegold.com/) has compiled a list of merchants [accepting DCR](https://marketplacegold.com/crypto/186-decred-dcr) globally and [announced](https://www.reddit.com/r/decred/comments/nbcvob/where_decred_dcr_is_accepted_locally_and_globally/) it on r/decred.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

Join our [#services](https://chat.decred.org/#/room/#services:decred.org) chat to follow Decred ecosystem updates.

## Outreach

Monde PR's achievements for May:

- pitched 2 stories to finance and crypto publications
- responded to 12 requests for comments/PR opportunities
- secured 2 media interviews

News coverage secured by Monde PR:

- an article in [Brave New Coin](https://bravenewcoin.com/insights/crypto-market-forecast-week-of-may-3rd-2021) featuring news about the decentralized treasury activation
- an article in [CoinDesk](https://www.coindesk.com/bitcoiners-future-consensus-2018-2021) featuring commentary by @lukebp about his experience at Consensus. The piece was syndicated to [Yahoo! Finance](https://finance.yahoo.com/news/8-400-bitcoiners-went-hilton-200356039.html)
- The DCRDEX integration announcement was covered by [Bankless Times](https://www.banklesstimes.com/2021/05/27/decred-announces-initial-dcrdex-integration-into-decrediton-wallet/) and [Crowdfund Insider](https://www.crowdfundinsider.com/2021/05/175918-digital-currency-project-decred-announces-initial-integration-of-its-decentralized-exchange-into-decrediton-wallet/). The Crowdfund Insider article was syndicated to [Crypto News BTC](https://cryptonewsbtc.org/2021/05/28/digital-currency-project-decred-announces-initial-integration-of-its-decentralized-exchange-into-decrediton-wallet/), [MCC Exchange](https://mcc.exchange/2021/05/27/digital-currency-project-decred-announces-initial-integration-of-its-decentralized-exchange-into-decrediton-wallet/) and [MoneyNow](https://moneynow.cc/decreds-virtual-currency-allocation-announces-initial-integration-of-its-decentralized-wallet-into-decrediton-wallet/). The announcement was also covered by [CryptoNEXA](https://www.cryptonexa.com/2021/06/02/decred-and-zcash-lead-the-weekly-top/), [CriptoNoticias](https://www.criptonoticias.com/mercados/decred-zcash-lideran-top-semanal-mercado-halla-plena-recuperacion/) and [Crypto News](https://cryptonews.com/news/polygon-enjin-decred-uniswap-and-horizen-led-the-market-last-10514.htm). The Crypto News article was syndicated to [IQ Stock Market](https://www.iqstockmarket.com/n/polygon-enjin-decred-uniswap-horizen-led-market-last-week-2325136/).

## Media

Selected articles:

- Big Tech on steroids: why the 2020s will be the "decade of the DAO" by [Dominic Frisby](https://en.wikipedia.org/wiki/Dominic_Frisby) ([MoneyWeek](https://moneyweek.com/investments/alternative-finance/bitcoin-crypto/603213/decade-of-the-dao-decentralised-autonomous-organisation))
- Thinking Out Loud #2: Decred charting spree by @PermabullNino ([substack.com](https://permabullnino.substack.com/p/thinking-out-loud-2-decred-charting))

Videos:

- Finite coin supply - Decred Fundamentals by @phoenixgreen ([youtube](https://www.youtube.com/watch?v=pRIEiCvBYPE))
- Why is governance important - Decred Fundamentals by @phoenixgreen ([youtube](https://www.youtube.com/watch?v=hrL4sS8HuXg))
- Decred News Update - $150M stakeholder-driven DAO now live, DCRDEX coming to wallet, v1.6.2 & more by @Exitus ([youtube](https://www.youtube.com/watch?v=S_asvjm4lFI))
- Why this will be the decade of the DAO - Big Tech on steroids by Dominic Frisby ([youtube](https://www.youtube.com/watch?v=dQLN-DNnVKU))
- Decred 2021: DCR coin (Decred explained) by Layah Heilpern of Exodus ([youtube](https://www.youtube.com/watch?v=Kkb4BWmth7k))
- Decred Price Analysis - 26th May 2021 by Josh Olszewicz of Brave New Coin ([youtube](https://www.youtube.com/watch?v=LUg_DXUHdmg))
- Talking Decred with Jake Yocom-Piatt by Dominic Frisby ([youtube](https://www.youtube.com/watch?v=ZCfIM8IHurU)) - @jy-p hinted at upgrading the mixing tech with post-quantum crypto

Art and fun:

- The games are rigged - the revolution will not be centralized by @karamble ([twitter](https://twitter.com/karamblez/status/1398087058892148740))
- [Lego Stakey](https://twitter.com/Talha_Habib/status/1398268623572111362) made by young hodlers
- @jz has been busy with the [#RealDecredMemes](https://twitter.com/hashtag/RealDecredMemes) hashtag: DCR marrow [chart/menu](https://twitter.com/jz_bz/status/1391442849808408580), [freedom eagle](https://twitter.com/jz_bz/status/1392177374008053760), levels of voter [enlightenment](https://twitter.com/jz_bz/status/1395560884433473537), [shower thoughts](https://twitter.com/jz_bz/status/1396211915098136578)
- CoinDesk sending [mixed signals](https://twitter.com/CoinDesk/status/1395432897834848256) on their sympathy for Stakey

Translations:

- Decred Journal April 2021 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4) and Chinese (@Dominic). Thank you all!

Other non-English content:

- Decred's new Treasury covered by [CriptoNoticias](https://www.criptonoticias.com/comunidad/protocolo-decred-esta-5-dias-descentralizar-tesoreria/)
- looks like @Dominic secretly runs a new Decred podcast in Chinese with 3 episodes already out: [first](https://twitter.com/wanbihou/status/1383625001098649602) with an anon hardware engineer about events in the community, [second](https://twitter.com/wanbihou/status/1388412787076984832) on governance with decreder, and [third](https://twitter.com/wanbihou/status/1393825045902807041) with Mable Jiang of 51% Podcast (where @Dominic was a [guest](https://podcasts.apple.com/cn/podcast/51-with-mable-jiang-presented-by-multicoin-capital/id1540917284?l=en&i=1000515571194) recently)

![Lego Stakey](img/202105.4.384.jpg)

## Discussions

Selected Reddit threads:

- Chia's [Proof of Space and Time](https://www.reddit.com/r/decred/comments/n2sdwq/thoughts_on_alternatives_to_proof_of_work/) (PoST) as a replacement of PoW
- My GF made this deliciously looking [cake](https://www.reddit.com/r/decred/comments/n7l6ca/my_gf_made_this_deliciously_looking_cake_full_of/) full of Decred
- Decred: a [moonshot](https://www.reddit.com/r/decred/comments/ncnmca/decred_a_moonshot_and_the_continuity_of_proof_of/), and the continuity of proof of work consensus
- Do we [still need](https://www.reddit.com/r/decred/comments/njdrw6/do_we_still_need_centralized_exchanges/) centralized exchanges?
- Why Decred is worth a [non-zero percentage](https://www.reddit.com/r/decred/comments/nors4z/why_decred_is_worth_a_nonzero_percentage_of/) of Bitcoin's market cap

Selected Twitter discussions:

- a long [debate](https://twitter.com/lukebp_/status/1388987670832074758) between @lukebp and @BuckPerley on formal vs informal governance

> The Decred DAO has achieved a new milestone for the entire crypto space: A Digital Sovereign Wealth Fund.
> 
> The Decred network is the closest thing to a Digital Nation state.
> 
> A Layer 1 DAO with its own treasury, its own exchange, its own currency, and its own wallet. ([@ammarooni](https://twitter.com/Ammarooni/status/1390869248910794753))

![space cake exterior](img/202105.5.384.jpg) ![space cake interior](img/202105.6.384.jpg)

_And its own cakes!_

## Markets

In May DCR was trading between USD 90.4-229.4 / BTC 0.0027-0.0047. The average daily rate was $173.47.

@PermabullNino posted a ["charting spree"](https://permabullnino.substack.com/p/thinking-out-loud-2-decred-charting) with lots of metrics unique to Decred and succint commentary. USD 40 and BTC 0.004 seem to be important levels for many miners and stakers.

@PermabullNino's non-Decred series ["Permabullish Banter"](https://permabullnino.substack.com/) [reports](https://permabullnino.substack.com/p/pb-banter-5-7-2021) that the stablecoin printer is in full "brr" mode, and some [insights](https://permabullnino.substack.com/p/pb-banter-5-25-2021) on USDC.

@Checkmate has updated [checkonchain.com](https://checkonchain.com/) with new charts tracking [Decred Treasury](https://www.reddit.com/r/decred/comments/nakdpc/new_decred_onchain_metric_charts_live/) and DCRDEX trading [volume](https://twitter.com/_Checkmatey_/status/1391743198242885634).

[DCRDEX](https://dex.decred.org/) has traded 383K DCR and 1.4K BTC in May, averaging to 12K DCR and 46 BTC daily trading volume.

## Relevant External

[Signalling](https://taproot.watch/) for Taproot activation on Bitcoin has hit a level exceeding 90% (as of early Jun at ~97%) and is set to be locked in some time in June when the current signalling window ends.

Iran's Central Bank has [reportedly](https://www.coindesk.com/iran-central-bank-ban-trading-crypto-mined-abroad) banned trading of cryptocurrency which is "mined abroad", in an effort to stop capital flight. Iranian businesses are still permitted to obtain cryptocurrency from registered Iranian miners, for use in international payments.

Bitcoin mining pool Marathon Mining has [mined](https://www.coindesk.com/marathon-miners-censor-bitcoin-transactions-ofac-compliant) a block which it describes as "fully compliant with U.S. regulations", having censored transactions from entities it believes are sanctioned by the US Department of Treasury or have been involved in dark web activity. Despite their efforts some darknet market transactions made it into this block which was intended as a milestone for Bitcoin censorship.

After Elon Musk criticized Bitcoin's environmental characteristics and Tesla [stopped](https://twitter.com/elonmusk/status/1392602041025843203) accepting it as payment, he joined with Michael Saylor and others to [promote](https://www.forbes.com/sites/ninabambysheva/2021/05/24/elon-musk-and-michael-saylor-lead-effort-by-bitcoin-miners-to-address-environmental-concerns/) a new "Bitcoin Mining Council to promote energy usage transparency and accelerate sustainability initiatives worldwide".

Ark's Cathie Wood also [remarked](https://www.coindesk.com/ark-cathie-wood-crash-esg-movement) at Consensus that ESG (Environmental Social and Governance) concerns with Bitcoin meant "A lot of institutional buying went on pause", crediting Elon Musk with a role in this movement.

The PoolTogether DAO, associated with the Pool Together lottery and controlling over 50% of all POOL tokens, has [voted](https://snapshot.org/#/poolpool.pooltogether.eth/proposal/QmfDcwyhMyhiTmszt8EX1a2vGfJzAN5TcXGMUwm7W7G7rq) to [diversify](https://gov.pooltogether.com/t/ptip-11-treasury-diversification/963) the holdings by selling 5.38% of all POOL tokens, currently controlled by the DAO, to a selection of VCs for the agreed sum of 7 million USDC. The POOL tokens bought by the VCs will have a lock-up period of 1 year, vesting over a 1 year period following that.

This is part of an apparent recent [trend](https://www.coindesk.com/synthetix-baderdao-sushiswap-lido-dao-treasuries) for DAOs to diversify their holdings.

May's big Ethereum flash loan fail victim was xToken, where an attacker [exploited](https://www.theblockcrypto.com/post/104667/defi-protocol-xtoken-exploit-attack) bugs in two different contracts within the same transaction, netting a profit of $24.5 million after paying a $21,900 transaction fee to obtain the flash loan.

Binance Smart Chain is now providing [competition](https://www.crowdfundinsider.com/2021/05/175611-defi-hack-analysis-project-pancakebunny-attacked-via-major-200-million-flash-loan-vulnerability/) for Ethereum in the DeFi dumpster fire stakes, after BUNNY tokens were hit for a notional $200 million in misprinted tokens following an economic exploit with, you guessed it, flash loans.

Coinbase is [expanding](https://decrypt.co/72109/coinbase-says-its-a-media-company-really) its remit to also become a media company, going direct to their audience with "fact check" type content that is approved by its marketing department.

That's all for May. Share your stories for the next issue in our declassified [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat.

## About

This is issue 38 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, richardred
- reviews and feedback: chappjc, davecgh, dnldd, jholdstock, karamble, lukebp, matheusd, oshorefueled
- title image: saender
- funding: Decred stakeholders
