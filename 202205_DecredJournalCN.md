# Decred月报 – 2022 年 5 月

![abstract art by @saender](img/202205.1.github.png)

_图片: @saender_

对于 Decred 来说，5月是一个史诗般的月份：

- 获得选民批准的四项共识变更（DCP0007-10）已在主网上激活。
- 核心软件有两个临时bug修复版本，v1.7.2 和 v1.7.3。
- GoDCR v1.7.0 已经发布，这是第一个供主网使用的版本 - 并且已经发布了新的资金提案。
- Decred 杂志推出，这是一个托管和共享 Decred 新闻和其它内容的新平台，由 @phoenixgreen 带头。
- 由于激活了 DCP-0009，所有撤销miss票错误的都已被撤销。
- Politeia 上发布了四项新提案。

内容：

- [激活了四个共识变更](#four-consensus-changes-activated)
- [发布核心软件 v1.7.2 和 v1.7.3](#core-software-v172-and-v173-released)
- [GoDCR v1.7.0 发布](#godcr-v170-released)
- [安卓和iOS钱包v1.7.0发布](#android-and-ios-wallets-v170-released)
- [发展](#development)
- [人员](#people)
- [治理](#governance)
- [网络](#network)
- [生态系统](#ecosystem)
- [外展](#outreach)
- [活动](#events)
- [媒体](#media)
- [讨论](#discussions)
- [市场](#markets)
- [相关外部](#relevant-external)


## 激活了四个共识变更

在 v1.7中添加并经利益相关者批准的所有四个[共识升级](https://docs.decred.org/governance/consensus-rule-voting/consensus-vote-archive/)已于 5 月 8 日在[区块657,280](https://dcrdata.decred.org/block/657280)中激活：

- [DCP-0007](https://github.com/decred/dcps/blob/master/dcp-0007/dcp-0007.mediawiki) - 确定新国库每月最大支出的算法已修复。

- [DCP-0008](https://github.com/decred/dcps/blob/master/dcp-0008/dcp-0008.mediawiki) - 现在需要明确的共识升级来定义和允许更新版本。对于 Decred 生态系统中的所有参与者来说，与未来的共识变化整合将更加容易且不易出错。一些工程师甚至会说，完全验证节点拒绝他们无法完全验证的数据是唯一明智的操作方式。通过这次升级，Decred 将硬分叉作为升级共识的最安全和可靠的方式加倍下注，“因为我们可以”。

- [DCP-0009](https://github.com/decred/dcps/blob/master/dcp-0009/dcp-0009.mediawiki) - 矿工现在自动撤销错过和过期的选票。这消除了用户处理撤销的巨大挫败感，尤其是丢失（未备份）赎回脚本的痛苦。钱包代码和 GUI 变得更简单，质押变得更容易。

- [DCP-0010](https://github.com/decred/dcps/blob/master/dcp-0010/dcp-0010.mediawiki) - 每个区块奖励的 50% 从 PoW 矿工重定向到 PoS 选民，将 PoW/PoS/国库的分配比例从 60/30/10 更改为 10/80/10。这有望重新平衡 DCR 的供需，并降低恶意行为者操纵市场的能力。作为副产品，更高的 PoS 奖励使质押 DCR 更具吸引力。

这可能是 Decred 历史上最大的共识升级。


## 发布核心软件 v1.7.2 和 v1.7.3

dcrd 和 dcrwallet v1.7.2于 5 月 11 日[发布](https://twitter.com/decredproject/status/1524430609543831553)- 撰写本文时的最新版本。当启用可选索引时，dcrd 修复了一个罕见且难以命中的情况。dcrwallet 收到了一个修复verifymessage，启用了公共钱包密码的更改，以及一些内部/开发人员的更改。[发行说明](https://github.com/decred/decred-binaries/releases/tag/v1.7.2)。

[Decrediton v1.7.2](https://github.com/decred/decred-binaries/releases/tag/v1.7.2#decrediton-v172)增加了对国库支出投票的支持、更多关于 VSP 质押的信息、更新的 DEX 模块和几个错误修复。v1.7.3于 5 月 18 日紧随其后，修复了 macOS 10.15 并设置了国库支出投票选项。[发行说明](https://github.com/decred/decred-binaries/releases/tag/v1.7.3)。

[验证下载](https://docs.decred.org/advanced/verifying-binaries/)以确保它们未被修改。`6DF634AA7608AF04`这些文件使用以（主键以）结尾的 Decred Release 子密钥进行签名`6DF634AA7608AF04`。

## GoDCR v1.7.0 发布

自 v0.9.0 测试网发布以来，经过近 8 个月的开发，GoDCR 的首次主网版本于 5 月 23 日[宣布](https://www.reddit.com/r/decred/comments/uwa6w2/godcr_desktop_wallet_for_decred_written_purely_in/)。

支持以下功能：

- 基本钱包发送/接收
- 质押（自动购票）
- 通过 StakeShuffle 的钱包隐私
- 提案投票
- 共识规则变更投票
- 消息签名
- 钱包恢复
- 在 Linux、macOS、Windows 和 FreeBSD 上运行

[在此处下载](https://github.com/planetdecred/godcr/releases/tag/v1.7.0)`release@planetdecred.org` 并验证来自（密钥以 结尾）的签名`A3C9EB3218CCC3E8`。

这只是 GoDCR 的开始。接下来是 DEX 交易、硬币选择、国库支出投票，以及从一个统一的代码库构建桌面和移动应用程序的雄心勃勃的目标。检查寻求在 2022-2023 年资助这项工作的提案。

![](img/202205.3.full.png)

_图片：显示每个子系统摘要的 GoDCR 概览。_


## 安卓和iOS钱包v1.7.0发布

Android 和 iOS 钱包 v1.7.0于 5 月 11 日[发布](https://www.reddit.com/r/decred/comments/umye1t/decred_mobile_wallet_v170_has_been_released_for/)。

自 v1.6.1 以来的更改包括：

- 将 Decred 模块更新到 v1.7.0
- 更新混币服务器证书
- 手动隐私设置改进
- 错误修复和其它小改进

主网 iOS 应用在[App Store](https://apps.apple.com/us/app/decred-wallet/id1462247643)和 [TestFlight](https://testflight.apple.com/join/7KL4VnB2) 上提供测试网版本。

Android 应用程序可在 [Play Store](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet) 商店中找到。对于高级用户，有一个由 Planet Decred Release 密钥签名的新[APK下载](https://github.com/planetdecred/dcrandroid/releases/tag/v1.7.0)。

## 发展

除非另有说明，否则下面报告的工作具有“合并为主”状态。这意味着该工作已完成、审查并集成到高级用户可以[构建和运行](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c)的源代码中，但在普通用户的发布二进制文件中尚不可用。

<a id="dcrd" />

**[dcrd](https://github.com/decred/dcrd)**

_dcrd 是一个完整的节点实现，为 Decred 在全球的点对点网络提供支持。_

5 月份的总体方向是通过添加优化和删除不需要的代码来进一步利用最近激活的共识更改。

- 通过使用块头而不是检查点来优化[权益节点修剪](https://github.com/decred/dcrd/pull/2943)（减少对后者的依赖）。基于标头的同步操作更有效，并为多对等块下载铺平了道路。
- 追溯修复了撤销[费用限制错误](https://github.com/decred/dcrd/pull/2948)，该错误允许一方在拆分交易中为另一方增加支付给矿工的费用。由于自动撤销议程已激活，因此从未被利用过`mainnet`，也无法被利用。
- 重新设计了[旧块拒绝逻辑](https://github.com/decred/dcrd/pull/2945)，以用块替换检查点的使用assumevalid（在每个版本中都硬编码）。语义已被澄清，以反映“检查点”现在仅用于处理旧分叉，不再用于优化（现在依赖于其他方法）。CLI 选项已--nocheckpoints替换为--allowoldforks. 通过此更改，检查点的作用降至最低，这是可取的，因为它们是一种解决方法。
- 删除了不推荐使用的[地址索引](https://github.com/decred/dcrd/pull/2930)以及相关的 CLI 标志 (--addrindex和--dropaddrindex) 和searchrawtransactionsJSON-RPC。从开发的角度来看，地址索引需要大量维护，它没有被任何值得注意的东西使用，而且无论如何它也不容易提供大多数人想要的地址，这是一个完全平衡，而不是所有个别交易。它提供的所有信息以及更多信息都可以通过 dcrdata 获得。
- 添加了一个对模块进行[基本事务完整性](https://github.com/decred/dcrd/pull/2949)检查的功能blockchain/standalone，这对消费者（例如 DCRDEX）非常有用，因为该模块几乎没有依赖关系。
- 实施了[标头证明存储](https://github.com/decred/dcrd/pull/2938)以及单向数据库升级。这将通过从磁盘存储/加载它们来避免重新计算提交哈希。“区块头承诺”的概念听起来很吓人，但它是一项值得学习的强大技术。提案中对此进行了很好的描述，但简而言之，这些承诺是区块链数据的微小指纹，允许构建快速且安全的轻量级应用程序。目前只有一种类型的承诺——“紧凑型区块过滤器”，它允许轻钱包快速安全地找到用户的交易。未来可能会增加对其他用例的更多承诺。
- 在内部制作[`blockchain`](https://github.com/decred/dcrd/pull/2952)包而不是导出。这是减少导出的包和模块的总数以减少维护负担的持续整体努力的一部分，并最终达到可以遵循根模块的语义版本控制的程度。
- 最近的共识更改启用了持续的[代码](https://github.com/decred/dcrd/pull/2922)[清理](https://github.com/decred/dcrd/pull/2954)。

<a id="dcrwallet" />

**[dcrwallet](https://github.com/decred/dcrwallet)**

随 v1.7.2 补丁发布：

- [修复](https://github.com/decred/dcrwallet/pull/2150) 了签名消息的验证。
- [添加](https://github.com/decred/dcrwallet/pull/2148) `walletpubpassphrasechange`到 JSON-RPC 方法。它允许更改钱包的公共密码。
- 在返回的工单信息中[添加](https://github.com/decred/dcrwallet/pull/2146)了 VSP 主机，使钱包应用可以知道工单是由哪个 VSP 管理的。
- [删除](https://github.com/decred/dcrwallet/pull/2153)了所有选票撤销功能。现在撤销是自动创建的，不需要钱包来处理它。

合并`master`：

- 有关错过和过期票证的最新 dcrd 更改的[兼容性更新](https://github.com/decred/dcrwallet/pull/2158)。
- [修复](https://github.com/decred/dcrwallet/pull/2164)了getstakeinfo命令中的错误（由过期选票的更改引起）。

<a id="decrediton" />

**[Decrediton](https://github.com/decred/decrediton)**

_Decrediton 是一款功能齐全的桌面钱包应用程序，集成了投票、StakeShuffle 混合、闪电网络、DEX 交易等。它在有或没有完整区块链（SPV 模式）的情况下运行。_

v1.7.2 和 v1.7.3 补丁合并并发布：

- 用户现在可以在交易详情中获取[VSP费用交易哈希和费用状态](https://github.com/decred/decrediton/pull/3752)。如果收到的费用交易显示未使用票证的确认状态，但 dcrwallet 认为它尚未确认，则应用程序会在后台处理并更新状态。
- 对[工单状态和工单历史视图进行了改进](https://github.com/decred/decrediton/pull/3751)。现在选项卡在从交易详细信息页面返回后会记住它们的滚动位置。使用无限滚动功能逐渐加载行。
- [删除了撤销](https://github.com/decred/decrediton/pull/3754)选票功能。现在撤销是自动创建的，不需要钱包来处理它。
- 删除了撤销票证功能。现在撤销是自动创建的，不需要钱包来处理它。
- 删除了撤销票证功能。现在撤销是自动创建的，不需要钱包来处理它。
- Electron（Decredtion 所基于的框架）已[升级到 v17.4.2](https://github.com/decred/decrediton/pull/3765)，以修复阻止 dcrwallet/dcrd 在 macOS 10.15 (Catalina) 上启动的问题。
- ~7 个bug修复

![](img/202205.5.github.png)

_图片：Decrediton 显示每张票的附加 VSP 信息。_

<a id="politeia" />

**[Politeia](https://github.com/decred/politeia)**

_Politeia 是 Decred 的提案系统。它用于向 Decred 国库请求资金。_

后端更改：

- tlog 客户端现在有它[自己的包](https://github.com/decred/politeia/pull/1636)（用于导入遗留提案）。
- Trillian 版本[更新](https://github.com/decred/politeia/pull/1642)到 1.4.1。
- 修复了最小提案[开始日期错误](https://github.com/decred/politeia/pull/1637)。
- 修复[CSRF 错误检查](https://github.com/decred/politeia/pull/1638)。
- 修复了与开始和结束日期相关的[错误消息](https://github.com/decred/politeia/pull/1640)。
- 评论插件[fsck 函数重写](https://github.com/decred/politeia/pull/1641)以修复几个错误。“fsck”是“文件系统检查”的缩写，负责验证数据完整性和重建缓存。

图形用户界面更改：

- 通过替换为修复了[评论表单组件](https://github.com/decred/politeiagui/pull/2760)。formik react-hook-form
- 修复了与[提案开始/结束日期](https://github.com/decred/politeiagui/pull/2771)相关的几个错误。 

pi-ui 库中的更改（Politeia 和 Decrediton 的常见 UI 元素）：

- 支持小部件中的[键盘导航](https://github.com/decred/pi-ui/pull/446)。`DatePicker`
- 在文本输入字段中添加了带有工具提示的[信息图标](https://github.com/decred/pi-ui/pull/447)。

<a id="vspd" />

**[vspd](https://github.com/decred/vspd)**

_vspd 是用于运行投票服务提供商的服务器软件。VSP 24/7 代表其用户投票，不能窃取资金。_

- 12 个提交，代表各种代码优化和重构。

<a id="dcrlnlpd" />

**[dcrlnlpd](https://github.com/decred/dcrlnlpd)**

_dcrlnlpd 代表“DCR LN 流动性提供者守护程序”。_

了解 Decred LN 生态系统中的最新项目：

> 该服务允许在 Decred 网络中运行闪电网络流动性提供者。
> 
> 此 LP 允许远程客户端请求与 LP 关联的节点打开返回请求客户端的 LN 通道。这允许请求客户端有一些入站带宽来接收 LN 付款。
> 
> 为了创建通道，LP 会收取一定的费用，指定为所需通道大小的百分比。 \[[自述文件](https://github.com/decred/dcrlnlpd/blob/941743f09e2d01d5bae36b492de38e49c9565510/README.md)\]

<a id="dcrdex" />

**[DCRDEX](https://github.com/decred/dcrdex)**

_DCRDEX 是由原子交换提供支持的去信任交易的非托管交易所。_

面向用户的变化：

- 添加了对使用[accelerating BTC transactions](https://github.com/decred/dcrdex/pull/1555)收费技术[加速 BTC 交易](https://bitcoinops.org/en/topics/cpfp/)的支持。如果订单能够加速，订单页面将显示一个按钮。单击按钮时，会出现一个弹出窗口，允许用户选择更高的费用。
- 钱包页面添加了一个按钮来[重新创建 BTC SPV 钱包](https://github.com/decred/dcrdex/pull/1507)，因为它仍然有很多可能被破坏的方式。
- 支持使用用户提供的证书更新服务器的[TLS证书](https://github.com/decred/dcrdex/pull/1602)。

内部和开发人员更改：

- Allow [harness testing](https://github.com/decred/dcrdex/pull/1550) on testnet for the ETH client.
- Simnet harness tests [generalized](https://github.com/decred/dcrdex/pull/1603) to work with all currently supported assets.
- Implemented [stage 3](https://github.com/decred/dcrdex/pull/1530) of the signature message truncation fix. It is tricky to fix a bug when it is "deployed" on many co-dependent servers and clients, but the devs have a smart [4-stage plan](https://github.com/decred/dcrdex/pull/1526) for it.
- Switched to Bitcoin Cash [testnet4](https://github.com/decred/dcrdex/pull/1606) now that it is first class in bchd. Also, added a custom encoder for BCH's [CashAddr](https://www.reference.cash/protocol/blockchain/encoding/cashaddr/) addresses.
- Added methods for [calculating the median fee](https://github.com/decred/dcrdex/pull/1597) of the most recent block(s) in BTC/DOGE/LTC/BCH. Implemented a cache to prevent repeated scans between blocks, and a fallback if there is not enough data to estimate the fee.
- Updates to newer modules from [btcsuite and go-ethereum](https://github.com/decred/dcrdex/pull/1542).
- Dependency updates to build with [Node.js 18](https://github.com/decred/dcrdex/pull/1617).
- Encoding now allows for transaction [data longer](https://github.com/decred/dcrdex/pull/1620) than 65,535 bytes.
- Generic [wait and retry function](https://github.com/decred/dcrdex/pull/1623) reworked to gradually "taper off" (slow down) after a few initial frequent attempts.
- Various bug fixes, dependency upgrades, and optimizations.

While working on DCRDEX the developers have made [various contributions](https://twitter.com/blockchainbuck/status/1532146821300101120) to upstream projects: [btcd](https://github.com/btcsuite/btcd/commits?author=chappjc), [btcwallet](https://github.com/btcsuite/btcwallet/commits?author=chappjc), [go-ethereum](https://github.com/ethereum/go-ethereum/pull/24533), [neutrino](https://github.com/lightninglabs/neutrino/commits?author=chappjc), [zcash](https://github.com/zcash/zcash/commits?author=buck54321), and others.

Dev team has started a discussion on [renaming DCRDEX](https://www.reddit.com/r/decred/comments/v3gxa8/should_we_rebrand_decred_dex/) and are accepting name and logo ideas.

> Probably found a vendor to perform an audit of our Solidity atomic swap contracts. Notably, our contracts are so simple, we're under their minimum order size. That's what happens when you're not trying to extract trading fees and there's no admin functionality. \[[@blockchainbuck](https://twitter.com/blockchainbuck/status/1527105721724190722)\]

![](../img/202205.6.github.png)

_Image: DCRDEX allows to accelerate swaps when the network is busy but you want that trade ASAP._

<a id="dcrios" />

**[Decred Wallet (iOS)](https://github.com/planetdecred/dcrios)**

- GitHub build [workflow added](https://github.com/planetdecred/dcrios/pull/907) to ensure dcrios builds without any errors.
- [Updated](https://github.com/planetdecred/dcrios/pull/899) automated UI tests.

<a id="godcr" />

**[GoDCR](https://github.com/planetdecred/godcr)**

_GoDCR is a lightweight desktop GUI wallet with integrated staking, privacy, Politeia voting, consensus voting, and more._

- [Default account](https://github.com/planetdecred/godcr/pull/910) is now filtered out when privacy is enabled.
- All [signed messages](https://github.com/planetdecred/godcr/pull/918) can be verified, the restriction to just personal wallet addresses has been removed.
- Redirect modals [added](https://github.com/planetdecred/godcr/pull/923) to debug page (sending to docs.decred.org) and transaction details page (sending to the block explorer).
- Reworked [key event](https://github.com/planetdecred/godcr/pull/907) handling to be less error-prone and more efficient.
- Option to [import watch-only](https://github.com/planetdecred/godcr/pull/943) wallet added to the splash screen.
- Privacy is [enabled by default](https://github.com/planetdecred/godcr/pull/936) when a new wallet is created.
- Gio [updated](https://github.com/planetdecred/godcr/pull/934) to latest stable version.
- A bottom [navigation bar](https://github.com/planetdecred/godcr/pull/948) has replaced the side bar on screen-sizes below 479px (mobile devices).
- [Fixes](https://github.com/planetdecred/godcr/pull/957) to wallet crashes and proposal titles.
- Bug fixed where [incorrect locked balance](https://github.com/planetdecred/godcr/pull/956) was displayed in the Staking tab.
- Fixed builds on [Android](https://github.com/planetdecred/godcr/pull/924) and [FreeBSD](https://github.com/planetdecred/godcr/pull/914).
- ~6 other bug fixes and some optimizations.

Android and iOS builds of GoDCR [already function](https://proposals.decred.org/record/0ef42e5/comments/31) in some capacity, although there remains a lot of work to polish the mobile/touch UX.

![](../img/202205.7.github.png)

_Image: First look of GoDCR running on an emulated mobile OS._

<a id="dcrdata" />

**[dcrdata](https://github.com/decred/dcrdata)**

_dcrdata is an explorer for Decred blockchain and off-chain data like Politeia proposals, markets, and more._

- Updated [dependencies](https://github.com/decred/dcrdata/pull/1913) to build with Node.js 16 and 18.

<a id="dcrweb" />

**[decred.org](https://github.com/decred/dcrweb)**

_dcrweb is the source code for the decred.org website._

- [Updated chat room](https://github.com/decred/dcrweb/pull/1033) links.
- [Added](https://github.com/decred/dcrweb/pull/1035) PoW/PoS reward consensus change [press release](https://decred.org/press/2022-05-09-decred_shifts_to_majority_pos/).
- [Removed defunct](https://github.com/decred/dcrweb/pull/1037) exchanges.

**Other**

- dcrseeder: DNS seeding was finally [removed](https://github.com/decred/dcrseeder/pull/50), and a small fix to [prune dead peers](https://github.com/decred/dcrseeder/pull/47) more aggressively.


## People

Welcome to new first-time contributors with code merged to master in January-March:

- arjundashrath ([dcrd](https://github.com/decred/dcrd/commits?author=arjundashrath))
- liukun ([dcrd](https://github.com/decred/dcrd/commits?author=liukun))
- monsa00 ([godcr](https://github.com/planetdecred/godcr/commits?author=monsa00))
- ukane-philemon ([dcrdata](https://github.com/decred/dcrdata/commits?author=ukane-philemon), [dcrdex](https://github.com/decred/dcrdex/commits?author=ukane-philemon), [vspd](https://github.com/decred/vspd/commits?author=ukane-philemon))

We had no Decred Journal for these months but it's never too late to greet new contributors. Welcome onboard guys!

Community stats as of Jun 1 (compared to May 2):

- [Twitter](https://twitter.com/decredproject) followers: 54,474 (-388)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 12,631 (+10)
- [Matrix](https://chat.decred.org/) #general users: 677 (+15)
- [Discord](https://discord.gg/GJ2GXfz) users: 2,305 (+12)
- [Telegram](https://t.me/Decred) users: 2,858 (+30)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: ~4,630 (-9), views: 209K (+2K)

See [June 2022](https://decredcommunity.github.io/social-media-stats/posts/20220604.1) report on Decred SM performance for a more in-depth look at Feb vs Jun numbers.


## Governance

In May the new [treasury](https://dcrdata.decred.org/treasury) received 9,407 DCR worth $390K at this month's average rate of $41.46. 2,950 DCR was spent from the legacy treasury to pay contractors, worth $122K at May's rate, or $179K at April's billing rate of $60.62. These payments were to cover both March and April's contractor invoices.

As of Jun 12, combined balance of [legacy](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) and [new treasury](https://dcrdata.decred.org/treasury) is 795,673 DCR ($23.9 million USD at $30.09).

A new [proposal](https://proposals.decred.org/record/0ef42e5) was submitted by Raedah Group to fund GoDCR, the desktop GUI wallet built in pure Go which will also replace existing mobile wallets as development continues. This proposal requests $250K for 12 months of funding, a greater amount than the [previous proposal](https://proposals.decred.org/record/f7d9fc8) which was narrowly rejected in October 2021. The extra budget is due to larger number of workers, a longer duration and covering the maintenance of existing Android/iOS wallets. The budget was reduced from the initial $300K in response to some comments.

Four proposals were published on Politeia in May:

- The [proposal](https://proposals.decred.org/record/4fdef29) from @Exitus to fund Decred Journal and Politeia Digest until December 2022. DJ was inactive for 3 months since [@bee announced the halt](202112.md#the-future-of-decred-journal), until @Exitus took over the lead of the April issue and eventually a full new proposal. A detailed report on the 2021 proposal's deliverables and finances was published [here](https://github.com/decredcommunity/proposals/blob/master/proposals/1d74b88/updates/20220521.md), with key stats being $24,800 spent out of $39,000 to release 12 issues of DJ and 10 issues of PD. The new budget is capped at $33,000.

- The [proposal](https://proposals.decred.org/record/7057e0b) from @kozel to fund Decred content and asset translations throughout 2022. A report on Phase 2 informed that only $8,180 out of $33,000 was spent, so Phase 3 will have a lower limit of $20,000.

- The [proposal](https://proposals.decred.org/record/da2f32d) to fund continuation of the Bug Bounty program until December 2023. For the last 12 months the operating costs were ~$2,100 and ~$1,000 were paid as bounty rewards. The new proposal has duration increased from 12 to 18 months, the budget is split between $5,000 for operating costs and up to $100,000 for reward payments. The leadership was transferred from @degeri to @jholdstock.

- The [proposal](https://proposals.decred.org/record/6bdffcb) from @juliana requested $3,575 to run 3 events at universities in Uganda in 2022, with 30 people expected at each event.

See Politeia Digest [issue 51](https://blockcommons.red/politeia-digest/issue051/) to catch up on proposal activity between January and May.


## Network

**Hashrate**: May's [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&zoom=l2im68kw-l3x1522f&bin=block&axis=time) opened at ~345 Ph/s and closed ~115 Ph/s, bottoming at 74 Ph/s and peaking at 381 Ph/s throughout the month.

![](../img/202205.8.github.png)

_Image: Anticipated hashrate drop after the mining reward reduction._

Distribution of hashrate [reported](https://miningpoolstats.stream/decred) by the pools on Jun 1: Poolin 55%, ViaBTC 21%, F2Pool 7%, AntPool 7%, Luxor 5%, BTC.com 4%, CoinMine 0.3%.

Distribution of 1,000 blocks actually [mined](https://miningpoolstats.stream/decred) before Jun 1: Poolin 55%, ViaBTC 20%, F2Pool 8%, DsV1GF7 6.5%, BTC.com 6%, Luxor 4%, CoinMin2 0.2%, DsmLNFC 0.1%.

**Staking**: [Ticket price](https://dcrdata.decred.org/charts?chart=ticket-price&zoom=l2im68kw-l3x1522f&axis=time&visibility=true-true&mode=stepped) varied between 217-231 DCR, with 30-day [average](https://dcrstats.com/) at 223.6 DCR (+9.4).

The [locked amount](https://dcrdata.decred.org/charts?chart=ticket-pool-value&zoom=l2im68kw-l3x1522f&scale=linear&bin=block&axis=time) was 8.78-9.07 million DCR, meaning that 62.6-63.9% of the circulating supply [participated](https://dcrdata.decred.org/charts?chart=stake-participation&zoom=l2im68kw-l3x1522f&scale=linear&bin=block&axis=time) in Proof of Stake. Both DCR and percentage values are the new ATHs for Decred.

All missed and expired tickets [have been revoked](https://github.com/decred/dcrd/pull/2861#issuecomment-1144049589), unlocking a total 175,957 DCR from 1,719 tickets (average price 103 DCR per ticket). ~45K of that DCR have moved already, while the remaining ~131K DCR are likely lost due to lost seeds and other reasons. One of the revoked tickets was from an old block 767, around the time when first complaints about [the high ticket price](https://forum.decred.org/threads/are-you-still-purchasing-at-current-price-4-55-dcr.840/) appeared.

All new missed votes are revoked automatically, the first one revoked in block [657295](https://dcrdata.decred.org/block/657295).

**VSP**: On Jun 1, ~6,900 (+120) live tickets were managed by 16 [listed](https://decred.org/vsp/) vspd servers, or 16.8% of the ticket pool (+0.2%).

Legacy (dcrstakepool) tickets can no longer be voted since May 8 when the chain forked to the new rules. Unlike all other shutdown/stalled legacy VSPs, on Jun 1 coinmine.pl and decredbrasil.com reported that they're on a current block height and collectively hold 19 live tickets. We are not sure how this is possible and these tickets are not included in the above stats.

**Nodes**: Throughout May there were around ~185 reachable nodes according to [PD Analytics](https://analytics.planetdecred.org/nodes).

Node versions as of Jun 1 [snapshot](https://nodes.jholdstock.uk/user_agents) (160 total, dcrd only): v1.7.1 - 41%, v1.7.2 - 20%, v1.7.0 - 12%, v1.7.0 dev builds - 9%, v1.8.0 dev builds - 4%, v1.6.x - 6%, v1.5.x - 4%.

![](../img/202205.10.github.png)

_Image: Mixed and unspent % crawling up._


## Ecosystem

- [big.decred.energy VSP](https://github.com/decred/dcrwebapi/pull/161) from [@DCR_Uncle](https://twitter.com/DCR_Uncle) is now [available](https://twitter.com/DCR_Uncle/status/1527138204175847424) on the VSP list with a 1% fee.

- A second instance of Decred Lightning Network Visualizer was discovered at [decred.lighting](https://decred.lighting/), running same code as [ln-map.jholdstock.uk](https://ln-map.jholdstock.uk/).

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.


## Outreach

Monde PR's achievements:

- Pitched 2 news updates to crypto and finance media.
- Pitched 1 newsjack.
- Responded to 3 requests for comments.
- Secured 2 media interviews.

Secured the following news articles:

- Decred's shift to a majority PoS consensus model was covered by [Invezz](https://invezz.com/news/2022/05/09/decred-shifts-to-majority-proof-of-stake-consensus-model/), featuring commentary from @jy-p. Invezz posted the story in 9 other languages including [French](https://invezz.com/fr/actualites/2022/05/09/decred-passe-au-modele-de-consensus-majoritaire-proof-of-stake/) and [Italian](https://invezz.com/it/notizie/2022/05/10/decred-passa-al-modello-proof-of-stake/). The story was syndicated to 4 publications including [Bitcoin Insider](https://www.bitcoininsider.org/article/164786/decred-shifts-majority-proof-stake-consensus-model) and [Crypto News](https://cryptonews.net/news/altcoins/6288659/).
- The GoDCR release was covered by [CryptoNinjas](https://www.cryptoninjas.net/2022/05/23/decred-blockchain-introduces-new-cross-chain-spv-based-wallet-godcr/) and [E-Crypto News](https://e-cryptonews.com/decred-launches-godcr-wallet-with-enhanced-privacy-features/). The CryptoNinjas article was syndicated to 3 publications including [BitcoinEthereumNews](https://bitcoinethereumnews.com/blockchain/decred-blockchain-introduces-new-cross-chain-spv-based-wallet-godcr-cryptoninjas/) and [Global Online Money](https://globalonlinemony.com/decred-blockchain-introduces-new-cross-chain-spv-based-wallet-godcr-cryptoninjas/).


## Events

**Attended:**

- @arij and @khalidesi hosted a Decred booth during the two days of [EMEC EXPO](https://twitter.com/in_insaf/status/1526979202951655425) (International Exhibition of Digital Transformation) in Casablanca, Morocco, and answered many questions about how Decred works and what problems it solves.

- Edson Neto [talked about](https://twitter.com/Decred_BR/status/1529089788199976960) Decred at [Bitconf](https://www.instagram.com/p/Cd6sL2wLHU7/) in Sao Paulo, Brazil.

**Upcoming:**

- Jun 30 - [Decred Social Meetup](https://www.meetup.com/chicago-decred-meetup/events/286491971/) in Chicago, USA. There will be at least one Decred Jacket, sources say.

![](../img/202205.9.github.jpg)

_Image: Edson Neto presenting at Bitconf._


## Media

[Decred Magazine](https://www.decredmagazine.com/) has been [launched](https://twitter.com/DecredSociety/status/1530562659006939136) by @phoenixgreen to collect all Decred content in one place, give new writers a platform, and archive great past content ([Decred Journal](https://www.decredmagazine.com/tag/decred-journal/) included). The latter is valuable since websites and blogs commonly "evaporate" their content over time and it becomes hard or impossible to recover. As of writing, around 300 posts have been imported and 8 authors have explicitly agreed to add their content. Decred Magazine is intended as a replacement for [decredsociety.com](https://www.decredsociety.com/) launched earlier as a pilot project.

**Selected articles:**

- [Decred Lightning node setup guide](https://gist.github.com/dcr-uncle/11b30f44e73b55cc31fb75881f9b4643) by @DCR\_Uncle
- [The biggest blockchain consensus vote in history goes live!](https://www.decredmagazine.com/the-bigest-blockchain-consensus-vote-in-history-goes-live/) by @phoenixgreen
- [The PoW rebellion](https://www.decredmagazine.com/the-pow-rebellion/) by @phoenixgreen

**Videos:**

- [Peer to Peer Exchange - Decred and the state of the market](https://www.youtube.com/watch?v=vqzaEdtmCsI) by @phoenixgreen and @Exitus
- [Decred Monthly Recap - 2.66x increase in staking rewards, dev updates, big hard-fork inbound!](https://www.youtube.com/watch?v=uOHiDTj9Prs) by @Exitus and @DajanaDcr
- [DCRDATA Looking into a block - Decred Fundamentals](https://www.youtube.com/watch?v=nsMrdK45cK8) by @phoenixgreen - also as a [blog post](https://www.decredmagazine.com/dcrdata-looking-into-a-block/)
- [DCRDATA Proof of Work charts - Decred Fundamentals](https://www.youtube.com/watch?v=t_pcHfJS0uw) by @phoenixgreen - also as a [blog post](https://www.decredmagazine.com/dcrdata-proof-of-work-charts/)
- [DCRDATA Proof of Stake charts - Decred Fundamentals](https://www.youtube.com/watch?v=eRtogHA_2_w) by @phoenixgreen - also as a [blog post](https://www.decredmagazine.com/dcrdata-proof-of-stake-charts/)
- [This miner is QUIET, PROFITABLE, and BROKEN WTF?!](https://www.youtube.com/watch?v=skv8RehpaaU) (DR5 Miner and Subsidy Change) by @VoskCoin
- [Decred staking rewards just increased 2.6x! Let's spread the word!](https://twitter.com/DajanaDcr/status/1526306473051045892) (TikTok) by @DajanaDcr and @Exitus
- [Decred code history visualized](https://twitter.com/karamblez/status/1528173850642505728) by @karamble

**Audio**:

- Videos by @phoenixgreen (aka Decred Society) are also available in the [podcast format on anchor.fm](https://anchor.fm/decred-society/).


## Discussions

Selected Reddit posts:

- [Weekly Contribution Streaks](https://www.reddit.com/r/decred/comments/v0eus3/weekly_contribution_streaks_tards_unite/) is a new weekly activity from u/ersfbddfgwe that seeks to break the common mental barrier "I can't contribute anything because I'm not a developer :(". The "rules" are simple: just show up and write about _anything_ you did, big or small, with an optional DCR address for tips. There is an ongoing discussion about how to better rank and reward contributions.

- In [Decred Mining Thread](https://www.reddit.com/r/decred/comments/unh7nn/decred_mining/) miners have been sharing the challenges of mining DCR after their block reward share was reduced from 60% to 10%.

Selected Twitter discussions:

- Implementing [SPV trading wallets](https://twitter.com/blockchainbuck/status/1531156971759575040) for the DCRDEX. What it means and why the devs are focused on SPV. - by @buck54321
- Implementing a custom workflow for creating [Ethereum ERC-20 wallets](https://twitter.com/blockchainbuck/status/1527105720285552641). What tokens should we do and why? - by @buck54321


## Markets

In May DCR was trading between USD 30.00-58.68 / BTC 0.00103-0.00190. The average daily rate was $41.46.

@Applesaucesome is posting technical analysis of DCR, crypto, and the broader market on the new [Decred Magazine](https://www.decredmagazine.com/author/applesaucesome/) website, about once a week.

In May, DCRDEX has facilitated the trading of [~74K DCR](https://github.com/bochinchero/dcrsnapshots/tree/main/2022-05/700), equivalent of ~3M USD.


## Relevant External

Insider trading in the crypto space is increasingly in the spotlight. The Wall Street Journal featured an [article](https://www.wsj.com/articles/crypto-might-have-an-insider-trading-problem-11653084398) about suspected insider trading around exchange listings on Binance, Coinbase and FTX. The analysis was conducted by Argus Inc based on public blockchain records.

The former OpenSea product manager Nathaniel Chastain, who lost their job over profiting from the listing of NFTs on the OpenSea front page in September, has now been [arrested](https://www.cnbc.com/2022/06/01/former-opensea-employee-charged-in-first-ever-nft-insider-trading-case.html) and charged with insider trading by prosecutors in New York's Southern District. Although the NFTs in question are not the usual securities which insider trading laws apply to, the DA is alleging that Chastain injured his employer (OpenSea) by misappropriating information.

Actor Seth Green [lost](https://www.buzzfeednews.com/article/sarahemerson/seth-green-bored-ape-stolen-tv-show) his Bored Ape NFT in a phishing incident, made even more consequential by the fact that the ape had been set to star in a new show he was developing, *White Horse Tavern*. In June Green paid a $260,000 [ransom](https://www.businessinsider.com/seth-green-pays-260000-return-stolen-bored-ape-ethereum-nft-2022-6) to secure the return of the ape, so that the show could go on (without raising a lot of copyright questions over whether the stolen ape's image could be used).

That's all for May. Share your updates for the next issue in our [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat room.


## About

This is issue 47 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from the source after a minimal sanity check. The authors of the Decred Journal cannot verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing and editing: bee, bochinchero, Exitus, l1ndseymm, richardred
- reviews and feedback: davecgh, matheusd, phoenixgreen
- title image: saender
- funding: Decred stakeholders
