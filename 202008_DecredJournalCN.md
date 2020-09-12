# Decred Journal – 2020年8月

![abstract art](img/journal-202008-384.png)

_图片: Bidirectional @saender_

八月重点:

- 发布v1.5.2以修补潜在的拒绝矢量服务。
- dcrdex团队最多有6位活跃成员，每月合并50多个PR(键盘在燃烧)，以清除通过测试发现的bug。
- 去中心化国库支付代码的审查已经结束，收尾工作正在进行中。
- vspd得到了一些提升，现在工作已转移到Decrediton和dcrwallet的集成中。
- Politeia转换为tlog已经准备实施，重构达到适应需求就将开始测试。

## v1.5.2补丁发布

此版本修补了潜在的拒绝矢量服务。建议自己运行节点的人以及PoW矿工进行升级。

dcrd和Decrediton的新二进制文件在[此处](https://github.com/decred/decred-binaries/releases/tag/v1.5.2)提供。使用前请确保对其进行[验证](https://docs.decred.org/advanced/verifying-binaries/) -现在的说明更加详细和友好。

该漏洞[CVE-2018-17145](https://nvd.nist.gov/vuln/detail/CVE-2018-17145)于9月10日在NIST(美国国家标准与技术研究院)披露。Decred团队已于7月7日发布了补丁并于7月8日对其进行了修补。v1.5.2二进制版本于8月27日发布。

截至9月10日，根据[dcr.farm](https://charts.dcr.farm/d/000000014/nodes)，超过20％的节点已升级。

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以构建和运行的源代码中，但对于普通用户来说，还不能在发布的二进制文件中使用。

说到从源代码构建，v1.5.2中的更改实际上是从master分支上的[早期修复程序](https://github.com/decred/dcrd/pull/2253)中向后移植的。这意味着使用源代码构建的人在二进制发布之前1.5个月就收到了这些修复程序。如果您想尝试使用源代码构建，可以查看@kozel 制作的[教程](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c)以获取帮助。

> @davecgh:通过从源代码编译Decred软件，您可以利用代码升级体验最新版本带来的舒适体验，而不必等待正式版本的发布，这是最先进的。

[dcrd](https://github.com/decred/dcrd):

- 向存储库添加了一些历史[发行说明](https://github.com/decred/dcrd/pull/2314)。与仅使用GitHub的发行页面相比，这可以更好地保护这些文档不丢失，减少对GitHub的依赖，并允许人们在标准工作流程中做出改
- 添加了[simnet](https://github.com/decred/dcrd/pull/2315)环境文档和设置脚本。这可以提高开发人员在测试时的工作效率，还有助于使用通用设置编写可重现的bug报告。
- 引入的[contrib](https://github.com/decred/dcrd/pull/2317)目录中包含可选工具，这些可选工具在使用dcrd和相关软件时可能会很有用。当前，这包括操作系统服务配置和新的simnet设置脚本。
- 添加了数据库[迁移](https://github.com/decred/dcrd/pull/2321)，以删除所有最近优化后不再需要的区块索引数据。这使dcrd内存占用率减少了约19.5％。
- 已更新为Go 1.15，带来了可观的链接程序提升，使二进制文件减小了5％。
- 改进了文档和测试范围

值得注意的是，`notfound`触发v1.5.2发行版的消息处理很快又被[移植](https://github.com/btcsuite/btcd/pull/1603)到btcd，并且是其8月[发行版](https://github.com/btcsuite/btcd/releases/tag/v0.21.0-beta)的一部分。

进行中：

- 大部分的时间都用在了去[中心化国库支付](https://github.com/decred/dcrd/pull/2170)测试工作。

[dcrwallet](https://github.com/decred/dcrwallet):

- 已部署的基本VSP v3（vspd）[基础结构](https://github.com/decred/dcrwallet/pull/1785)
- 增加了检索[混合帐户](https://github.com/decred/dcrwallet/pull/1773)，以恢复钱包与CoinJoin交易
- 在`listlockunspent`命令中添加了可选的[account](https://github.com/decred/dcrwallet/pull/1787)参数（最初由dcrdex请求，但通常也很有用）
- [允许](https://github.com/decred/dcrwallet/pull/1807)从标准输入创建钱包（对于自动化测试很有用，这有助于多个其他项目）
- 优化[数据库](https://github.com/decred/dcrwallet/pull/1817)布局可实现更快的访问速度和更少的读/写
- [修复](https://github.com/decred/dcrwallet/pull/1806)了一个bug，其中`listunspent`在锁定时报告收益

[Decrediton](https://github.com/decred/decrediton):

- 添加了对使用[SPV](https://github.com/decred/decrediton/pull/2629)模式运行LN钱包的支持，并默认启用SPV
- 增加了对使用[混合帐户](https://github.com/decred/decrediton/pull/2565)还原钱包的支持
- [还原](https://github.com/decred/decrediton/pull/2604)重构的遗留代码以支持旧的和新的staking模型
- 继续升级为使用功能组件，自定义挂钩和CSS模块
- 为侧边栏组件添加了第一个[自动化测试](https://github.com/decred/decrediton/pull/2606)
- 大量bug修复

关于使用硬件钱包进行购票有很多问题。@jz [总结了](https://www.reddit.com/r/decred/comments/imbv74/staking_decred_with_ledger/)截至9月4日的最新动态：

- @JoeGruff 与Trezor 一起为在Decrediton的simnet上进行选票购买[工作](https://matrix.to/#/!frQxfmcoOmtseMqzby:decred.org/$D02jsxFbrVDCXsdbMx71fy6wluJfIaw-en-GwEAyj9E)，并且即将提交固件的PR。
- 在常规人员可以使用该固件之前，Trezor人员需要审查固件将其合并到上游。
- 据我所知，目前没人在Ledger的支持上工作，Trezor完成后可能会解决该问题。
- 期望在Ledger Live（他们的软件钱包）中支持Staking是不合理的，这不是我们可以为他们做的事情。

[Politeia](https://github.com/decred/politeia):

- 后端支持[TOTP](https://github.com/decred/politeia/pull/1210)（2FA的基于时间的代码）
- [改进了](https://github.com/decred/politeia/pull/1274)Politeia和[CMS](https://github.com/decred/politeia/pull/1232)中与dcrdata的重新连接的处理
- 通过有限状态机优化 RFP提案 [获取](https://github.com/decred/politeiagui/pull/2084)
- 大量bug修复

承包商管理系统（CMS）稳步发展，将提高问责制和支出效率:

- 用户界面，用于[查看](https://github.com/decred/politeiagui/pull/2051)相同的域发票
- 为那些已被提案批准但尚未通过DCC批准的承包商添加了新的承包商[类型](https://github.com/decred/politeia/pull/1276)，并且规定了此类承包商无法查看域发票的规则
- 增加了一个[限制](https://github.com/decred/politeia/pull/1275)，即相同域的承包商只能查看彼此过去6个月的发票
- 删除了使用[缓存](https://github.com/decred/politeia/pull/1282)为tlog迁移做准备

从@lukebp处获取的迁移tlog的更新进度：

> politeiad tlog后端和politeiad插件的工作已经完成。当前的焦点是重构礼貌。rockroachdb缓存依赖关系已经被删除，而politeiawww以前对其依赖很大，因此重构politeiawww路由涉及到本质上的完全重写。我们从来没有为git后端敲定一个合适的插件架构，导致我们过度依赖缓存。现在我们已经有了正确的tlog插件架构，我们必须把politeiawww逻辑的大部分分离出来，并将其移入插件层。过度依赖缓存也意味着不构建politeiad API，因为对缓存运行相同的查询更快更容易。所有这些现在都必须得到解决。
> 
> 一旦politieawww重构完成，我们就可以运行性能测试。如果性能测试顺利进行，我们就可以将tlog放到testnet上，并开始为发布做准备。

[vspd](https://github.com/decred/vspd):

- 管理员状态端点的基本HTTP [身份验证](https://github.com/decred/vspd/pull/167)（用于自动监视）
- 在关闭数据库[之后](https://github.com/decred/vspd/pull/169)写入备份
- 多个小型更新

感谢 @isuldor ([test.stakey.net](https://test.stakey.net/))和 @sethsimmons ([vspd.realprivacy.cc](https://vspd.realprivacy.cc/))）帮助测试了vspd。

最小可行的vspd最终更改已合并，下一步是完成dcrwallet和Decrediton集成。

[dcrpool](https://github.com/decred/dcrpool):

- 测试工具 [改进](https://github.com/decred/dcrpool/pull/243)

[dcrlnd](https://github.com/decred/dcrlnd):

- 使配置选项更[智能](https://github.com/decred/dcrlnd/pull/107)

[dcrdex](https://github.com/decred/dcrdex):

- 合约的接受者/创建者，[锁定时间](https://github.com/decred/dcrdex/pull/612)从24/48小时更改为8/20小时
- 允许[缩小](https://github.com/decred/dcrdex/pull/573)深度图上查看更多订单
- 添加了["拆分"](https://github.com/decred/dcrdex/pull/562)交易以适应大小多笔输出。以一笔额外交易为代价，使用户可以更好地控制锁定了多少资金，并释放更多订单的资金，从而创建更健康的订单簿和更好的用户体验。
- 指示市场视图上用户订单的即时[生效时间](https://github.com/decred/dcrdex/pull/586)
- [罚款账户](https://github.com/decred/dcrdex/pull/537)通知
- [异步](https://github.com/decred/dcrdex/pull/565)请求/通知处理和并行新匹配协商，以修复长期运行的客户端`init`和`redeem`请求以及其他一些问题
- 如果服务器无法识别，请在客户端[禁用](https://github.com/decred/dcrdex/pull/519)帐户
- 在[myorders](https://github.com/decred/dcrdex/pull/581)端点中添加了一些预先计算的有用信息，例如订单的期限和结算的金额
- 重复数据删除的[websocket](https://github.com/decred/dcrdex/pull/585)代码
- 更新并锁定了npm [依赖项](https://github.com/decred/dcrdex/pull/584)
- 固定[余额](https://github.com/decred/dcrdex/pull/548)计算
- 修复了多个并发bug
- 许多其他后端和UI更改

[合并了](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-08-01..2020-08-31+sort%3Aupdated-asc)来自6个贡献者的51个PR ，添加了19K并删除了4K行代码。

感谢所有[参加](https://twitter.com/stakeynet/status/1291960465904435200) alpha测试的人。

[dcrandroid](https://github.com/planetdecred/dcrandroid):

- added [rebroadcast](https://github.com/planetdecred/dcrandroid/pull/495) button to pending transaction dialog
- UI tweaks and translation updates

[dcrios](https://github.com/planetdecred/dcrios):

- 在交易列表页面上显示票券[奖励](https://github.com/planetdecred/dcrios/pull/706)和投票所需的天数
- 在未决交易对话框中添加了[重播](https://github.com/planetdecred/dcrios/pull/709)按钮
- 添加了按钮以[切换](https://github.com/planetdecred/dcrios/pull/714)金额输入字段的货币

[godcr](https://github.com/planetdecred/godcr):

- 帐户[重命名](https://github.com/planetdecred/godcr/pull/247)功能
- 在窗口标题中显示[网络](https://github.com/planetdecred/godcr/pull/248)
- 具有圆角的自定义[编辑器](https://github.com/planetdecred/godcr/pull/223)
- bug修复

[dcrdata](https://github.com/decred/dcrdata):

- 在“阻止”页面上显示哈希和[其它](https://github.com/decred/dcrdata/pull/1735)（侧链）阻止的链接
- [国库](https://github.com/decred/dcrdata/pull/1752)地址页面的简短URL
- 过滤器仅在“地址”页面上列[出未使用](https://github.com/decred/dcrdata/pull/1724)的输出

[docs](https://github.com/decred/dcrdocs):

- [添加](https://github.com/decred/dcrdocs/pull/1118)了描述LN [守望台](https://docs.decred.org/lightning-network/watchtowers/)的页面
- [重新添加](https://github.com/decred/dcrdocs/pull/1120) PoS FAQ
- 如何充分节点添加信息的成熟可能需要数天接受入站连接之前（配置 FAQ）
- 添加了有关承包商[工资率](https://github.com/decred/dcrdocs/pull/1123)的信息（[捐助方补偿](https://docs.decred.org/contributing/contributor-compensation/#pay-rates)页面）
- 为[移动钱包](https://docs.decred.org/wallets/mobile-wallets/)[添加](https://github.com/decred/dcrdocs/pull/1121)了页面

[decred.org](https://github.com/decred/dcrweb):

- 图标更新和bug修复

Other:

- most projects build and test with Go [1.15](https://github.com/decred/dcrd/pull/2334), which [came out](https://golang.org/doc/go1.15) in August
- multiple developers used the [release](https://github.com/decred/release) tool to [reproduce](https://matrix.to/#/!zefvTnlxYHPKvJMThI:decred.org/$l62fxKNyrDN_RhzY93vopaCLwh0Y9aulr6j7DjbFVd0) the v1.5.2 build and computed the same manifest hash

## People

Welcome to new first time contributors with code merged to master: @hsyia ([dcrdocs](https://github.com/decred/dcrdocs/pull/1122)), @brandoncurtis ([decred-release](https://github.com/decred/decred-release/pull/173)), @isuldor ([dcrwebapi](https://github.com/decred/dcrwebapi/pull/107)), @JustinBeBoy ([dcrios](https://github.com/planetdecred/dcrios/commits?author=JustinBeBoy)).

Community stats as of Sep 1:

- Twitter followers: 40,816 (+179)
- Reddit subscribers: 9,906 (+31), online: 320
- Matrix #general users: 174 (+50) \*
- Discord users: 1,394 (+22)
- Telegram users: 2,468 (-52)
- YouTube subscribers: 4,180 (+30), views: 154K (+3K)
- LinkedIn followers: 875 (+13)
- GitHub dcrd stars: 557 (+7), forks: 246 (+6)

\* reminder: Matrix had a big "purge" [in July](202007.md#people).

Some observations from other accounts tracked by the [social-media-data](https://github.com/decredcommunity/social-media-stats) repository:

- Facebook: [decredbrasil](https://www.facebook.com/groups/decredbrasil/) 5,799 members (-36) and 57 posts in 30 days, [decredinternational](https://www.facebook.com/groups/decredinternational/) 802 members and 20 posts in 30 days
- Instagram: [decred_es](https://www.instagram.com/decred_es/) 390 followers (+15), [decredbr](https://www.instagram.com/decredbr/) 767 followers (+50), [decredproject](https://www.instagram.com/decredproject/) 578 followers (+2). Unlike the other two, English account has no active maintainer (_hint_).
- Twitter: [DecredArabia](https://twitter.com/DecredArabia) 218 followers (+5), [DecredAustralia](https://twitter.com/DecredAustralia) 436 followers, [Decred_BR](https://twitter.com/Decred_BR) 540 followers (+13), [Decred_CA](https://twitter.com/Decred_CA) 334 followers, [Decred_ES](https://twitter.com/Decred_ES) 909 followers (+49), [Decred_PL](https://twitter.com/Decred_PL) 226 followers (+3)
- YouTube: [Decred Arabia](https://www.youtube.com/channel/UCCtB2BfsA2VdT0FJXpsYICA) 29 subscribers and 0.6K views, [Decred Brasil](https://www.youtube.com/channel/UC73wa2ddXuPWsmenVfeFTYg) 369 subscribers (+108) and 13K views (+4K), [Decred en Español](https://www.youtube.com/channel/UCCprOo4gR1vsjJTAzv8BMBQ) 74 subscribers (+28) and 1.3K views (+0.4K)
- #planetdecred Matrix room at the planetdecred.org homeserver has 151 users

## Governance

In August the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 12,961 DCR and spent 10,787 DCR. Using August's daily average DCR/USD rate of $17.02, this is $221K received and $184K spent. At July's average daily rate of $15.13, the USD figure billed for work completed in that month is $163K. As of Sep 6, Treasury balance is 634,747 DCR (8.5 million USD at $13.37).

New and concluded proposals:

- [proposal](https://proposals.decred.org/proposals/1dc1571) for design domain funding to cover 6 months of work in subdomains for UI/UX ($35K), Identity ($16K), and Visual Comms ($14K) - was approved with 80% yes votes and 25% turnout
- [proposal](https://proposals.decred.org/proposals/32cba00) to continue paying the moderators of Politeia, Matrix, Discord, and Telegram (max $9K over 6 months) was approved with 73% yes votes and a voter turnout of 29%
- [proposal](https://proposals.decred.org/proposals/2dcbc3e) to pay $50K for integration and promotional campaigns on two travel booking sites was rejected with 15% approval and a voter turnout of 24%
- a new [proposal](https://proposals.decred.org/proposals/1e55a41) for video production from @Exitus was published in early September
- early September also saw the first RFP [proposal](https://proposals.decred.org/proposals/91becea) published, it aims to change the messaging on decred.org and is inviting proposals for which changes to make

Four proposals have been abandoned: [augmented reality posters](https://proposals.decred.org/proposals/dedf452), [marketing by @fst_nml](https://proposals.decred.org/proposals/3372cfc), [social media memes](https://proposals.decred.org/proposals/4f81031) and [Decred poker series](https://proposals.decred.org/proposals/7a67ed5) (@darthcrypto plans to return with a more developed proposal).

@pavel shared a [screenshot](https://twitter.com/_Checkmatey_/status/1295858198260248576) and an update on the development of the [Decred OnChain](https://proposals.decred.org/proposals/0230918) website:

> Chart subpages are almost done. From UX/UI perspective, we are working on homepage. I would say we are ±75% done. ([chat](https://matrix.to/#/!qYpAAClAYrHaUIGkLs:decred.org/$3FcfGt9YIOR81fM5CnqEFib4d7HYJPqGe_2oE3Q4JL4?via=decred.org&via=matrix.org&via=planetdecred.org))

Pre-proposals:

- @kozel is shepherding a [pre-proposal](https://www.reddit.com/r/decred/comments/igfqjc/decred_content_and_asset_translation_proposal_an/) for content translation
- @lewildbeast is gathering feedback on a [pre-proposal](https://github.com/decredcommunity/proposals/pull/6) to offer awards to developers and researchers who pioneered new technology that Decred benefits from (e.g. HD wallets)

@bee is testing GitHub-based "proposal drafting infrastructure" that allows multiple people to edit the draft, get feedback and formatting help, track revisions, and post comments. Keeping drafts in a well-known place makes them discoverable and allows to save any progress for others to pick up even if the original author stops developing the proposal. Currently @lewildbeast's [awards](https://github.com/decredcommunity/proposals/pull/6) and @elian's [BTCPay](https://github.com/decredcommunity/proposals/pull/7) integration pre-proposals are hosted. To use this, submit a pull request to [proposals](https://github.com/decredcommunity/proposals/pulls) repo or ping @bee in [Matrix](https://decred.org/matrix/) #proposals room.

Check Politeia Digest [issue 34](https://blockcommons.red/politeia-digest/issue034/) and [issue 35](https://blockcommons.red/politeia-digest/issue035/) for a more detailed review of the governance activity.

## Network

Hashrate: [August's hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kd8zvp86-kek04pzi&scale=linear&bin=block&axis=time) opened at ~313 Ph/s and closed ~486 Ph/s, bottoming at 248 Ph/s and peaking at 557 Ph/s throughout the month. Pool [hashrate distribution](https://dcrstats.com/pow) as of Sep 1: UUPool 39%, Poolin 30%, lab.antpool.com 9%, BTC.com 2.3%, Luxor 0.8%, F2Pool 0.6%, BeePool 0.09%, CoinMine 0.03%, Suprnova 0.02% and others ~19%.

Staking: [30-day average](https://dcrstats.com/) ticket price was 151.4 DCR (+7.1). The [price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kd8zvp86-kek04pzi&axis=time&visibility=true-false&mode=stepped) varied between 141.2-168.1 DCR. [Locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kd8zvp86-kek04pzi&bin=block&axis=time) was 5.82-6.09 million DCR, which corresponded to 49.11-51.03% of the available supply [participating](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kd8zvp86-kek04pzi&bin=block&axis=time) in PoS.

Ticket price hit 168.12 DCR, which is a new high since the change of the price algorithm in 2017.

Nodes: Throughout [August](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1596240000000&to=1598918400000) there was an average of 141 public listening nodes and 139 total nodes per dcr.farm (the total was ~250 before a sharp drop on Aug 10, some data might have been missed). Average version distribution for August: 41% dcrd v1.5.1, 11% dcrd v1.5.0, 7% dcrd v1.5.2, 6% dcrd v1.6 dev builds, 5% dcrd v1.5 dev and RC builds, 0.9% dcrd v1.4, 10% dcrwallet v1.5.1, 1.1% dcrwallet v1.5, 1% dcrwallet v1.4, 16% others.

Our Network [update](https://ournetwork.substack.com/p/our-network-issue-34) by @Checkmate shares observations about an average of 100K DCR mixed daily making a significant part of the on-chain volume, hashrate boost following some market recovery above the "thermocap", and changes in three Decred-specific metrics.

New [research piece](https://medium.com/@_Checkmatey_/decred-mining-market-mechanics-fd26b921dc46) by @Checkmate gives a comprehensive overview of Decred mining market mechanics. For those preferring video/audio format, a summary overview of the paper and charts is available on [YouTube](https://www.youtube.com/watch?v=TJn6qTko0Xw). A full read is highly recommended.

> Understanding the incentives, mechanics, and performance metrics of the Decred chain's largest natural seller sheds light on both market pricing, and the strength of network security. This research should provide a sound basis for interpreting the context and performance of the Decred mining market.

## Integrations

Transak [tweeted](https://twitter.com/transak_finance/status/1294322399031316480) that DCR can be bought in 32 countries via its service.

BitcoinToYou now [allows](https://twitter.com/bitcointoyou/status/1291473453812535301) to buy and sell DCR for the Brazilian fiat currency BRL. @michae2xl presented Decred in a [livestream](https://www.youtube.com/watch?v=dk_2WYZ4EDU) on their channel.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Decentralized Treasury work is making some well-deserved [noise](https://twitter.com/marco_peereboom/status/1293364590399512577) on Twitter. Thanks to all developers for posting dev updates and everyone [amplifying](https://twitter.com/_Checkmatey_/status/1293370599977361409) [them](https://twitter.com/jz_bz/status/1295447838843908098).

Decred Latam team published [second](https://www.reddit.com/r/decred/comments/i7ue8h/activities_report_decred_en_espa%C3%B1ol_proposal_2/) and [third](https://www.reddit.com/r/decred/comments/ip0uke/activities_report_3_decred_en_espa%C3%B1ol_proposal_2/) activities reports for their marketing [proposal](https://proposals.decred.org/proposals/3c02b67). All three reports are polished and archived in the [proposals](https://github.com/decredcommunity/proposals/tree/master/proposals/3c02b67/updates) knowledge base.

@michae2xl [reported](https://www.reddit.com/r/decred/comments/ijhxzn/august_report_for_brazil_proposal/) on his August activities for the Brazil marketing [proposal](https://proposals.decred.org/proposals/bc20f98) ([archived](https://github.com/decredcommunity/proposals/blob/master/proposals/bc20f98/updates/20200830.md)).

Monde PR's achievements for August:

- updated the PR Calendar with suggested pitches and story ideas for the next 6 months
- created and pitched 2 story ideas to the media
- secured two email Q&As with crypto and mainstream publications
- submitted comments from Decred spokespeople to one news story

News coverage secured by Monde PR:

- an article in [AMB Crypto](https://eng.ambcrypto.com/bitcoin-on-chain-solutions-are-punching-above-its-weight-again/) featuring commentary by @jy-p on Bitcoin scaling, syndicated to 4 news outlets including [Fintech Zoom](https://fintechzoom.com/fintech_news_bitcoin-news/bitcoin-on-chain-solutions-are-punching-above-its-weight-again/) and [Sunrise Reads](https://sunriseread.com/bitcoin-on-chain-solutions-are-punching-above-its-weight-again/109311/)
- an article in [Finance Magnates](https://www.financemagnates.com/cryptocurrency/news/are-crypto-platforms-taking-personal-data-protection-seriously-enough/) featuring commentary by @jy-p on personal data protection
- an article in [Cointelegraph](https://cointelegraph.com/news/ledger-cto-discusses-wallet-s-safety-after-multiple-security-setbacks) featuring commentary by @jy-p on Ledger's security setbacks, syndicated to 7 media outlets including [The Union Journal](https://theunionjournal.com/ledger-cto-discusses-wallets-safety-after-multiple-security-setbacks/) and [Armenian Reporter](https://www.reporter.am/ledger-cto-discusses-wallets-safety-after-multiple-security-setbacks/)

## Events

Attended:

- Aug 5 - [Governance and blockchain](https://twitter.com/BlockSummitLA/status/1291029494065778689) in Latin America - Internet. @elian joined Cristobal Pereira and Ernesto Contreras of Dash to discuss blockchain governance of Decred in comparison to Dash, mechanics of Decred Treasury, Politeia, and the proposal process. The event was announced on [Spanish Cointelegraph](https://es.cointelegraph.com/news/online-seminar-on-governance-in-the-blockchain-and-its-contributions-to-latin-america). ([video](https://www.youtube.com/watch?v=Sh3obx4Mx_0))
- Aug 8 - [Hablemos Decred 8](https://twitter.com/Decred_ES/status/1288633074050306052) - Internet. @elian and guest José Manuel Da Silva from [criptolugares.io](https://www.criptolugares.io/) talked about cryptocurrencies and commerce, particularly in Venezuela, and the prospects of adoption from a medium of exchange perspective. ([video](https://www.youtube.com/watch?v=z-6a_tgE89E))
- Aug 11 - [Decred Talk 1](https://twitter.com/Decred_BR/status/1292842513846460417) - Internet. In this first episode of the Brazilian version of Decred Talk, @michae2xl and André Horta (CEO BitcoinToYou) talked about Decred DAO and autonomous ecosystems. The event was streamed on BitcoinToYou's channel. ([video](https://www.youtube.com/watch?v=dk_2WYZ4EDU))
- Aug 17 - Decred Talk 2 - Internet. Second edition of Decred Talk was hosted on Instagram. The goal was to engage with new/unknown community members and answer their questions. ([video](https://www.instagram.com/tv/CEAenAhF7m0/))
- Aug 20 - [Hablemos Decred 9](https://twitter.com/Decred_ES/status/1294416104723488769) - Internet. @adcade and guest Mauricio Ocampo of [technolawgeek.com](https://www.technolawgeek.com/) discussed legal perspectives of cryptocurrencies. ([video](https://www.youtube.com/watch?v=VzELuWRqCo4))
- Aug 28 - [Legal status of Bitcoin](https://twitter.com/paxful_LATAM/status/1297912240511881216) - Internet. Organized by [Paxful Latam](https://twitter.com/paxful_LATAM).
- Aug 28 - [Hablemos Decred 10](https://twitter.com/Decred_ES/status/1298432664245084161) - Internet. @adcade, @elian and guest [Carlos Ramirez](https://twitter.com/Ciberagente) discussed cybersecurity, privacy and cybercrime. ([video](https://www.youtube.com/watch?v=GosMlhxWK3M))
- Aug 29 - [From laws to protocols](https://twitter.com/Decred_ES/status/1299506004607094784) - Internet. Hosted by [Students for Liberty](https://twitter.com/SFLMexico) Mexico. ([video](https://www.facebook.com/894983097182840/videos/312801089791414))
- Aug 31 - [Future of organizational structures](https://twitter.com/Decred_ES/status/1298275771333705728): Centralized vs decentralized - Internet. @elian joined a panel with John DeVadoss (Neo) and Ernesto Contreras (Dash) to discuss governance in decentralized organizations. ([video](https://www.youtube.com/watch?v=yIlVTSObIzU)) Organized by [Fintech Advisory Services](https://www.fintech-advisory.com/). ([video](https://www.youtube.com/watch?v=yIlVTSObIzU))

In other news, @eSizeDave is facilitating a webinar to help academics from the Australian RMIT university to learn about Decred as part of their research.

## Media

Selected articles:

- Decred, mining market mechanics by @Checkmate ([medium](https://medium.com/@_Checkmatey_/decred-mining-market-mechanics-fd26b921dc46))
- Utility of cryptoassets by @mm ([stakey.club](https://stakey.club/en/utility-of-cryptoassets/))
- Blockchain governance - Part 1 by @mm ([stakey.club](https://stakey.club/en/blockchain-gov-part1/))
- Our Network #34 features another Decred update from @Checkmate ([substack.com](https://ournetwork.substack.com/p/our-network-issue-34))

Translations:

- @mm's own new and old articles are available [in Portuguese](https://stakey.club/pt/articles/)
- Decred, Mining Market Mechanics - [in Spanish](https://territorioblockchain.com/decred-mecanica-del-mercado-minero/) by territorioblockchain.com
- Politeia Digest issues 33-35 - [in Arabic](https://insaf01.github.io/politeia-digest-ar/) (@arij, @abdulrahman4) and [in Spanish](https://medium.com/decred-es/politeia-digest-spanish/home) (@pablito)
- Decred Journal - July 2020 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), Portuguese (@mm) and Spanish (@francov\_). Polish May and June by @kozel are now available too. Thank you all!

In other non-English content:

- We totally missed the creation of [Decred Arabia](https://www.youtube.com/channel/UCCtB2BfsA2VdT0FJXpsYICA) YouTube channel back in [May](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$15908512441460kIGQx:decred.org) (_seriously folks, [submit your stories](https://github.com/xaur/decred-news/blob/docs/contributing.md)!_). The channel now has 7 videos: 2 original on the [history of money](https://www.youtube.com/watch?v=OFONdBbYbBc) and [history of Decred](https://www.youtube.com/watch?v=_7Ae_Klwqo0), and 5 strategic English videos with Arabic subtitles such as [How Decred is Unique](https://www.youtube.com/watch?v=N0DmpjhuD38) and [How to Stake Decred](https://www.youtube.com/watch?v=JuKw3BHO0v0). The same subtitles are also available in original English videos. Source files are [on GitHub](https://github.com/Insaf01/Decred-Videos-Ar) for collaboration and reuse. If you would like to submit your translated subtitles to Decred's videos please contact @Exitus.
- @elian was featured in Spanish Territorio Bitcoin podcast in [Feb](https://www.ivoox.com/episodio-105-entrevista-jesus-sanchez-bermejo-audios-mp3_rf_47751087_1.html) and [Jun](https://www.ivoox.com/que-es-decred-entrevista-profundidad-elian-audios-mp3_rf_52242080_1.html), which got 7K and 5K views, respectively.
- @elian was [quoted](https://es.cointelegraph.com/news/cryptology-and-marketing-the-challenges-of-organic-growth) in Spanish Cointelegraph on marketing and challenges of organic growth.

Videos:

- Decred bi-weekly news update - August 18th, 2020 by @Exitus ([youtube](https://www.youtube.com/watch?v=hjOi4sfvdNU))
- Top 5 bullish signals for Decred by LiteLiger ([youtube](https://www.youtube.com/watch?v=186jzRRJ-80))
- Mining market mechanics - Decred research read-through by @Checkmate ([youtube](https://www.youtube.com/watch?v=TJn6qTko0Xw))
- Did you know Decred has Governance by Decred Society ([youtube](https://www.youtube.com/watch?v=1BNW60RE0rQ)) - a quick overview of the Politeia proposal process

Audio:

- Staked Podcast Episode 0.0. "It [took](https://twitter.com/elima_iii/status/1299306383146471426) me over a year to build up the bravery to do this". Congrats to Eduardo for launching the podcast! ([anchor.fm](https://anchor.fm/staked-podcast/episodes/Staked-Podcast-Episode-0-0-eimmd6/a-a31v0tg), [tweet](https://twitter.com/stakedpodcast/status/1299305564258938880))
- Rough Consensus 10. In this episode, the spidermen are joined by @notsofast - a cryptocurrency OG with wide ranging expertise, and pick his brain surrounding: Bitcoin vs altcoins, why Decred, mining, investment/trading approach, and much more. ([libsyn](https://roughconsensus.libsyn.com/episode-10-bitcoin-decred-altcoins-with-notsofast))

Even though the memes [proposal](https://proposals.decred.org/proposals/4f81031) was abandoned, people started generating memes independently:

- [contributing](https://twitter.com/coveryfire7777/status/1292966872560918529) to the DAO
- [attacking](https://twitter.com/coveryfire7777/status/1293719678985146369) Decred
- [strong doge](https://twitter.com/coveryfire7777/status/1293984002349699072)
- [attack cost](https://twitter.com/svitekpavel/status/1289793785669484544)
- Decred chilling with some [features](https://twitter.com/lukebp_/status/1292622538560872448) while Bitcoin and Ethereum wrestle

## Community Discussions

Selected Reddit posts:

- newcomer [wonders](https://www.reddit.com/r/decred/comments/i5jcjp/dcrdex_seems_like_the_greatest_thing_ever_why_is/) why the wider crypto community is not paying attention to DCRDEX
- [question](https://www.reddit.com/r/decred/comments/i9ufxy/decred_team_and_treasury_fund_management/) about Treasury fund management had several in depth answers
- Jul 31 Forward Thinking Friday focused on [Contrarian Messaging](https://www.reddit.com/r/decred/comments/i1gumi/forward_thinking_friday_contrarian_messaging_31/) where @Checkmate suggested two potential areas for Decred marketing to rally around, "Decred is Ready" and "Own the Name, Decentralised Credits, in the face of 'De'Fi"
- Aug 7 [Forward](https://www.reddit.com/r/decred/comments/i5cy0y/forward_thinking_friday_7_aug_2020/) Thinking Friday mostly concerned marketing ideas, and it's where the idea to reward Bitcoin developers who produced work that is useful to Decred was first discussed
- Aug 14 Forward [Thinking](https://www.reddit.com/r/decred/comments/i9w54z/forward_thinking_friday_14_aug_2020/) Friday's top comment was about building private DAEs on Decred
- Aug 28 Forward Thinking [Friday](https://www.reddit.com/r/decred/comments/iip7ap/forward_thinking_friday_28_aug_2020/)'s top comment was about creating a crypto index using DCRDEX

Selected Twitter discussions:

- Reluctant Raccoon just cannot find that "DeFi governance token" [satisfaction](https://twitter.com/ypical_/status/1292439057168060416) anywhere outside Decred
- @DecredSociety [noted](https://twitter.com/DecredSociety/status/1292039718679580673) Decred's "market maturity" component of the FCAS rating is down, but overall the project is still A-grade
- @degeri [reminds](https://twitter.com/degeri_crypto/status/1293729682584674304) that Decred is always hiring (and tagging some company that was "restructured" recently)
- @CATO\_io [explored](https://twitter.com/CATO_io/status/1299756617722925056) how Decred's ethics and risk-sharing lead to a more robust system. Good example of creative outreach that exposes new sides of the project.

## Markets

In August DCR was trading between USD 15.25-23.49 / BTC 0.00134-0.00202. The average daily rate was $17.02.

After hitting a new high of ~$12,100 on Aug 2, BTC/USD crashed to $10,550 within minutes and triggered a spectacular liquidation of more than $1 billion worth of futures. ZeroHedge [wrote](https://www.zerohedge.com/markets/bitcoin-hits-1-year-high-then-plummets-after-someone-liquidates-1-billion-seconds-hammer) that price manipulation is likely since it's not in the best interest of the seller to "take out the entire bidstack in one transaction".

In a Twitter convo, @Checkmate shared his [model](https://twitter.com/_Checkmatey_/status/1293652411316281344) where DCR's bear market was hugely affected by compulsory selling by ASIC miners that invested in hardware at the peak bull market.

## Relevant External

Bitcoin Cash is warming up for another community splitting hard fork. The developers of the BitcoinABC client [announced](https://www.bitcoinabc.org/2020-08-24-celebrating-bchd-slp/) that the next bi-annual hard fork on Nov 15 will add a requirement that a portion of each block reward goes to an address controlled by the developers. Roger Ver and others have [tweeted](https://twitter.com/rogerkver/status/1300908197113458688) this is not acceptable and they won't be joining the fork.

Ethereum Classic has suffered [another](https://cryptobriefing.com/after-second-double-spend-attack-ethereum-classics-future-is-question/) [two](https://www.coindesk.com/ethereum-classic-attacker-successfully-double-spends-1-68m-in-second-attack-report) double spend reorg attacks, with the attacker gaining $5.6 million from the first attack, which was executed with $204,000 worth of rented hashpower. The attacks reorged so many blocks that some implementations ignored them and the network [partitioned](https://blog.coinbase.com/coinbases-perspective-on-the-recent-ethereum-classic-etc-double-spend-incidents-1fd19ef215f3).

Charles Hoskinson of IOHK and Cardano has [proposed](https://cointelegraph.com/news/charles-hoskinson-s-iohk-submitted-a-decentralized-treasury-proposal-to-the-ethereum-classic-community) two ECIPs for ETC, one to add checkpointing which would stop the long reorgs, and a second to add a development fund which receives 20% of block rewards. The block reward proposal seems highly controversial in the community, with ETC labs rejecting the idea.

The YAM token and protocol was [born](https://medium.com/@yamfinance/yam-finance-d0ad577250c7) and [died](https://coingeek.com/defi-strikes-again-yam-protocol-bug-leads-to-750000-loss/) in August, its cycle lasted for about 3 days, which is fast even for DeFi. The token was billed as a "governance token" for the YAM protocol, but as soon as the system started it became clear it was fundamentally broken. There was a short window where YAM farmers were mobilized to act and save the protocol but there was a bug in the solution as well so it's dead now. YAM was covered in disclaimers about being experimental, unaudited, and was produced in a 10 day period by smashing other smart contracts together - one hour after launch, $76 million was invested, rising to $300 million the next day before the fatal flaw was announced.

MakerDAO activated an executive "spell" contract which was supposed to raise the ceiling for WBTC but [instead](https://twitter.com/nanexcool/status/1292287024767082496) set it to zero. It seems no harm was done on this occasion other than delaying the availability of more WBTC.

Zcash Foundation is [selecting](https://decrypt.co/39105/a-five-member-board-to-control-36-million-treasury-for-zcash) a 5 member board to control the share of block reward funding which it is due to begin receiving. The board will be selected by votes of the Community Advisory Panel, which currently has 62 members, but each member can now invite one additional member.

Coinbase CEO [confirmed](https://www.theblockcrypto.com/linked/76588/coinbase-ceo-interview-token-service) that the company is developing a platform to join in the initial exchange offering (IEO) business, provisionally titled Coinbase Launch.

Cryptocurrency adoption is most widespread in Nigeria and Vietnam according to Statista Global [Consumer Survey](https://www.zerohedge.com/crypto/youll-never-guess-which-country-has-most-widespread-adoption-crypto-world).

The fintech company Plaid (as [used by](https://enegnei.github.io/This-Month-In-Bitcoin-Privacy/July_2020/#july-1st---class-action-lawsuit-against-plaid-inc) Coinbase, Gemini, and others) has been hit with a $5M+ class action [lawsuit](https://www.natlawreview.com/article/fintech-startup-plaid-inc-hit-5m-class-action-lawsuit).

> 1\. Imagine there is a company that knows every dollar you deposit or withdraw, every dollar you charge or pay to your credit card, and every dollar you put away for retirement, within hours after you make the transaction. Imagine this includes every book or movie ticket or meal you purchase, every bill you pay to a doctor or hospital, and every payment you make (or miss) on your mortgage, student loan or credit card bill. Imagine this company maintains a file on you containing all of this information going back five years. Imagine that this company uses your username and password to log into the online account you maintain with your bank and updates that file multiple times a day to stay up to date on every financial move you make.
> 
> 2\. Imagine this company is not your bank. Imagine that, as far as you know, you never provided your username and password to this company or otherwise authorized it to access your online accounts. Imagine you never heard of this company at all.

Imagine someone got a hold of their database and used it to identify cryptocurrency holders.

Top cryptocurrency exchanges are [drafting](https://www.coindesk.com/crypto-exchange-group-eyes-bulletin-board-system-for-fatf-compliance-coinbase-exec) a white paper on sharing customer data to comply with FATF's "travel route" requirements.

Class action [lawsuit](https://cointelegraph.com/news/600m-crypto-ad-ban-class-action-filed-in-australian-courts) against Google and Facebook was filed in Australia. Tech giants are accused of anti-competitive behavior for banning crypto ads in 2018, which allegedly killed the ICO market, damaging the wider crypto industry while not efficiently blocking impersonation scams.

A bipartisan group of members of US Congress have [written](https://www.coincenter.org/congress-to-irs-proof-of-stake-block-rewards-should-not-be-taxed-as-income/) to the IRS to urge a clarification on how PoS rewards are treated for tax purposes - and asking that these be treated not as income but as a good produced by the validator, to be taxed when it is sold.

The United States Postal Service [filed]( https://www.zerohedge.com/crypto/usps-just-filed-patent-blockchain-based-secure-voting-system) a patent for a blockchain-based secure voting system.

## About This Issue

This is issue 29 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

You can submit a story [here](https://github.com/xaur/decred-news/labels/next%20release) to be considered for the next release. [Feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, lukebp, richardred
- reviews and feedback: davecgh, jholdstock, jrick, jz, Exitus, michae2xl
- title image: saender
