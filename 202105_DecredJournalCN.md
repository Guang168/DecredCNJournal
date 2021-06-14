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

DCRDEX v0.2.0 已经发布！它包含了自 v0.1.5 发布以来超过 3 个月的工作。最显着的变化是：

- UI 和可用性增强，包括响应式设计和交互式深度图
- 支持 Decrediton 的客户控制及其账户的使用
- 帐户导入/导出
- 比特币现金 (BCH) 支持

查看重要通知和[发行说明](https://github.com/decred/decred-binaries/releases/tag/v1.6.3#dcrdex-v020)中的完整更改列表。在[DEX页面](https://dex.decred.org/)通过简化安装步骤指南。更高级的用户可以在[此处](https://github.com/decred/decred-binaries/releases/tag/v1.6.3#downloads-v163)获取二进制文件并手动安装它们。不要忘记[验证](https://docs.decred.org/advanced/verifying-binaries/)下载以确保它们未被篡改。

合并到 master:

- 初始服务器端[以太坊](https://github.com/decred/dcrdex/pull/979)资产支持
- 不允许[更改](https://github.com/decred/dcrdex/pull/1055)为无法结算用户的钱包
- 更新到[最新](https://github.com/decred/dcrdex/pull/953)的dcrd 和 dcrwallet

许多朝着[0.3](https://github.com/decred/dcrdex/milestone/12) 里程碑迈进的工作正在进行中，最重要的是以太坊和SPV。

<a id="dcrandroid" />

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

- 禁止从[非混合](https://github.com/planetdecred/dcrandroid/pull/541)帐户发送
- 添加密码输入[延迟](https://github.com/planetdecred/dcrandroid/pull/542)以抵抗暴力攻击
- 在概览页面显示[质押](https://github.com/planetdecred/dcrandroid/pull/543)相关交易
- 更新[依赖项](https://github.com/planetdecred/dcrandroid/pull/546)并用“StakeShuffle”替换“CoinShuffle++”
- 保持[显示](https://github.com/planetdecred/dcrandroid/pull/553)直到混合完成或取消
- 显示Politeia 提案的富文本[格式](https://github.com/planetdecred/dcrandroid/pull/557)（不使用 WebView）
- 更新了中文和法语翻译
- 修复[观察钱包](https://github.com/planetdecred/dcrandroid/pull/560)列出发送资金

合并到 [dcrlibwallet](https://github.com/planetdecred/dcrlibwallet):

- 添加了用于获取提案[描述](https://github.com/planetdecred/dcrlibwallet/pull/192)的代码，并从保存提案文件切换为按需加载
- 为[cspp.decred.org](https://cspp.decred.org/)集成了一个签名的 TLS [证书](https://github.com/planetdecred/dcrlibwallet/pull/193)，这是使用主网时所必需的
- 修复了平衡和 Politeia 集成的错误

<a id="dcrios" />

**[dcrios](https://github.com/planetdecred/dcrios)**

- 通过混币器的引导设置实施[隐私模式](https://github.com/planetdecred/dcrios/pull/727)
- 在概览页面上显示钱包的 DCR 余额[等值的美元](https://github.com/planetdecred/dcrios/pull/746)
- 添加密码输入[延迟](https://github.com/planetdecred/dcrios/pull/749)以抵抗暴力攻击
- 当概览页面有多个钱包时，显示交易属于哪个[钱包](https://github.com/planetdecred/dcrios/pull/776)
- 显示更具体的质押交易[通知](https://github.com/planetdecred/dcrios/pull/766)（票已投票或撤销）
- 显示Politeia 提案的富文本[格式](https://github.com/planetdecred/dcrios/pull/773)（不使用 UIWebView）
- 添加了对 iOS 11 的支持
- ~17 个错误修复和 UI 调整

<a id="godcr" />

**[godcr](https://github.com/planetdecred/godcr)**

- 实现的页面：[选票](https://github.com/planetdecred/godcr/pull/395)概览、[选票列表](https://github.com/planetdecred/godcr/pull/406)和[恢复钱包](https://github.com/planetdecred/godcr/pull/386)
- 实现了[Max](https://github.com/planetdecred/godcr/pull/396)按钮，用于设置可以发送的最大 DCR 数量
- 添加了按[Enter](https://github.com/planetdecred/godcr/pull/414)提交输入字段的功能
- 向一些模态添加了[加载](https://github.com/planetdecred/godcr/pull/400)动画
- 初始[暗模式](https://github.com/planetdecred/godcr/pull/401)支持
- 添加语言[翻译](https://github.com/planetdecred/godcr/pull/426)基础设施
- ~14 个错误修复

Elias Naur（为 Godcr 提供支持的 Gio 库的创建者）友好地审查了 UI 代码并分享了他的[建议](https://paste.sr.ht/~eliasnaur/cea1d29d6a5f96668b5e166c2f39ef596974574f)。问题是为了解决这些问题而创建的，有些问题已经完成（例如[#409](https://github.com/planetdecred/godcr/issues/409), [#411](https://github.com/planetdecred/godcr/issues/411), [#416](https://github.com/planetdecred/godcr/issues/416)）。

![godcr](img/202105.3.628.png)

<a id="dcrdata" />

**[dcrdata](https://github.com/decred/dcrdata)**

- 新[`/treasury`](https://dcrdata.decred.org/treasury)页面的[初始版本](https://github.com/decred/dcrdata/pull/1824)
- 在[mempool](https://dcrdata.decred.org/mempool)页面上[显示](https://github.com/decred/dcrdata/pull/1827)资金支出交易，在投票交易页面上显示 tspend Yes/No 投票，在 tspend 自己的交易页面上进行投票统计
- 添加了一个更简单的端点来查询[汇率](https://github.com/decred/dcrdata/pull/1826)
- 将混合币的份额添加到[主页](https://dcrdata.decred.org/)（在Distribution下）

<a id="dcrdocs" />

**[docs](https://github.com/decred/dcrdocs)**

- 删除了图像的[内联HTML](https://github.com/decred/dcrdocs/pull/1168) - 将所有文档打包为单个[PDF](https://github.com/decred/dcrdocs/issues/923)文件
- 更新多个[vspd](https://github.com/decred/dcrdocs/pull/1171)描述

<a id="dcrweb" />

**[decred.org](https://github.com/decred/dcrweb)**

- [`/release`](https://decred.org/release/)页面[更新为](https://github.com/decred/dcrweb/pull/982) v1.6.3
- 改进的[SEO标签](https://github.com/decred/dcrweb/pull/979)
- 删除[不活跃](https://github.com/decred/dcrweb/pull/990)的贡献者
- [更新](https://github.com/decred/dcrweb/pull/957)[`/exchanges`](https://decred.org/exchanges/)页面
- 在页面上添加了[硬件钱包](https://github.com/decred/dcrweb/pull/989)部分[`/wallets`](https://decred.org/wallets/)

其它:

- 漏洞赏金计划[更新](https://bounty.decred.org/2021/05/status-update/)：目前共处理了 180 份提交，其中 16 份符合支付条件
- 一个轻量级的 Jekyll[主题配置](https://github.com/decredcommunity/jekyll-themes)被提取到它自己的 repo 中以供重用。它允许在没有第三方跟踪脚本的情况下发布一些 Markdown 页面。您可以在活动、提案和社交媒体统计项目的迷你网站上看到它的作用。
- 翻译需要持续维护。加入[#translations](https://chat.decred.org/#/room/#translations:decred.org)聊天室，与其它翻译和开发人员进行协调。

## 人员

欢迎到来首次贡献者，他们的代码已合并到主存储库中： @LasTshaMAN ([politeia](https://github.com/decred/politeia/commits?author=LasTshaMAN))!

截至 6 月 1 日的社区统计数据：

- [Twitter](https://twitter.com/decredproject) 粉丝: 45,724 (+1,333)
- [Reddit](https://www.reddit.com/r/decred/) 订阅s: 11,190 (+203)
- [Matrix](https://chat.decred.org/) #general 用户: 467 (+33)
- [Discord](https://discord.gg/GJ2GXfz) 用户: 1,787 (+221)
- [Telegram](https://t.me/Decred) 用户: 2,705 (+60)
- [YouTube](https://www.youtube.com/decredchannel) 订阅: 4,540 (+40), 观看: 186K (+4K)
- GitHub [dcrd](https://github.com/decred/dcrd) 星: 598 (+7), 叉: 255 (+1)

历史社区增长图表已经过调整、更新，并移至[此处](https://decredcommunity.github.io/social-media-stats/docs/charts)的新位置。

## 治理

5月，Decred 国库收到了 11,342 DCR（[旧地址](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)为2,564 ，[新账户](https://explorer.dcrdata.org/treasury)为8,778 ），价值 197 万美元，5 月份的平均汇率为 173.47 美元。5 月份没有花费 DCR。6 月 2 日，698 DCR 从旧地址用于 4 月发票，按 5 月的费率计算价值 121,000 美元，或按 4 月的结算费率 198.60 美元计算价值 139,000 美元。截至 6 月 3 日，合并的国库余额为 683,438 DCR（1.07 亿美元，合 156 美元）。

5 月份提交并通过了 1 个提案，Politeia 的持续发展提案（[上月](202104.md)详述）获得了 98.4% 的批准和 44% 的投票率。

在[checkonchain.com](http://checkonchain.com/)上[添加](https://twitter.com/_Checkmatey_/status/1392266971228430338)了国库图表，以协助围绕费用进行治理决策。

## 网络

**全网算力**: 5 月份[算力](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=ko2vefoc-kpf16yhd&scale=linear&bin=block&axis=time)为~418 Ph/s开始，结束为~351 Ph/s，全月最低为234 Ph/s，最高为497 Ph/s。

12 月至 4 月的价格从约 25 美元上涨至约 200 美元与算力从约 350 上涨至 450-550 Ph/s 之间似乎存在相关性。然后在相反的方向上，4 月 17 日至 23 日的价格调整发生在算力从 ~450 下降到 ~250 Ph/s 的过程中。最近，5 月 10 日至 23 日算力下降与价格从约 200 美元跌至约 110 美元相关。

6 月 1 日矿池[报告](https://miningpoolstats.stream/decred)的算力分布：Poolin矿池 39%，F2Pool 17%，蚂蚁矿池 3%，BTC.com 1.6%，卢克索 1.3%，火币矿池 0.4%，UUPool 0.1%，Coinmine 0.05%，okex 0.01%，其他38%。

1,000 个实际[开采区块](https://miningpoolstats.stream/decred)的分布几乎与报告的哈希率相符。未识别的开采块被分成 4 个地址：[Dsacz](https://explorer.dcrdata.org/address/DsaczRtjC31N6XVV69qcBoyR2BEEmjRDay3) 25%, [DsR4G](https://explorer.dcrdata.org/address/DsR4GSVsMxShvk6dpod9DBTbX7DuZhE2jjs) 7%, [DsbNN](https://explorer.dcrdata.org/address/DsbNNnupnCWd9MrHycs1NvwrtfhSYKF6ZGB) 4%, 和 [DsaWD](https://explorer.dcrdata.org/address/DsaWDBxVjxtV1ugqXsV3PGmAD4jLwryvSX3) 0.2%。

**Staking**: [票价](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=ko2vefoc-kpf16yhd&axis=time&visibility=true-true&mode=stepped)173-198 DCR之间变化，具有30天的平均在183.7 DCR（-2.1）。

[锁定量](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=ko2vefoc-kpf16yhd&scale=linear&bin=block&axis=time)为7.39-7.62亿DCR，这意味着循环供应的57.2-58.7％参加PoS。

**VSP**: 6 月 1 日，8.2K (+1.1K) 现场票由 vspd 服务器管理，1.1K (-1.1K) 由仍在列出的旧版 dcrstakepool 服务器管理。12 个传统 VSP 和 13 个新 VSP 总共管理着 22.5% 的票池。最近退市但仍然活跃的旧版 VSP 管理着 61 张现场门票。

5 月 14 日，[发现](https://github.com/decred/dcrwebapi/issues/138) 4 个传统 VSP 没有升级到新的共识规则，并于 5 月 8 日从网络中分叉，同时持有约 350 张客户的票。除了一个之外，其他所有人最终都升级，而[stakepool.dcrstats.com](https://stakepool.dcrstats.com)更改为维护模式并停止报告统计信息。截至 6 月 8 日，其 77 张现场门票的状态尚不清楚。

**Nodes**: 根据[dcrextdata](https://dcrextdata.planetdecred.org/nodes)，整个 5 月大约有 215 个可访问节点。

截至 6 月 1 日[快照](https://nodes.jholdstock.uk/user_agents)的节点版本（共 252 个，仅 dcrd）：v1.6.2 - 42%、v1.6.0 - 21%、v1.6.1 - 17%、v1.7 dev builds - 8%、v1.6 dev builds 4%，v1.5.2 - 3%，v1.5.1 - 2.7%，v1.5.0 - 0.8%。

## 生态系统

欢迎新[vspd](https://github.com/decred/vspd)实例[123.dcr.rocks](https://123.dcr.rocks/)来自[@thefrankbraun](https://twitter.com/thefrankbraun)。服务费为 0.49%，投票钱包位于两大洲的 3 个数据中心。自 5 月 1 日上市以来，截至 6 月 8 日，该服务已投票约 430 张票并管理约 650 张现场票。

旧版 VSP [dcrpool.dittrex.com](https://dcrpool.dittrex.com)已从列表中[删除](https://github.com/decred/dcrwebapi/pull/140)，但仍在在线观看其最后 1 个现场门票。自2018年11 月以来，该服务已对 800 多张票进行了投票。来自 Dittrex 的替换 vspd 实例已启动，等待其第一个投票票被添加到列表中。

并非所有交易所都顺利处理了 Decred 的第 6 次共识升级：

- 币安已提前升级，分叉发生时未受影响
- Bittrex 卡在第552,447个区块——最后一个区块遵守旧的共识规则。他们的状态页面报告说 DCR 钱包被禁用，并且在“钱包维护”下，在 5 月 13 日左右更改为“正常”。
- Poloniex发推文称他们的 DCR 钱包因“维护”而被禁用（共识升级后约 4 小时），并于 5 月 21 日再次发推文称已重新启用

自 5 月 17 日左右以来，Ledger Live 用户一直在报告同步和发送 DCR 的问题。Ledger[事件页面](https://status.ledger.com/incidents/j1sypv88pgs6)上的最新更新称，该修复程序已在 5 月 20 日进行测试，但他们 6 月 3 日的[推文](https://twitter.com/Ledger_Support/status/1400429510827388929) 证实该问题仍未解决。截至 6 月 8 日，状态页面报告 DCR 中断，并且在过去 90 天内正常运行时间为 75%。

以下服务已从[decred.org](https://decred.org/exchanges/) 中[删除](https://github.com/decred/dcrweb/pull/957)：

- [instaex.io](https://instaex.io/) - 网站已关闭
- [fexpro.net](https://fexpro.net/) - 证书错误
- [changenow.io](https://changenow.io) - DCR 交易对3 个月以上不可用
- [transak.com](https://global.transak.com/) - 似乎不再支持购买 DCR

[MarketplaceGOLD](https://marketplacegold.com/) 编制了一份全球接受 [DCR](https://marketplacegold.com/crypto/186-decred-dcr) 的商家名单，并在 r/decred 上公布。

警告：Decred 月报的作者不知道上述任何服务的可信度。在将您的个人信息或资产信任给任何实体之前，请自行研究。

加入我们的[#services](https://chat.decred.org/#/room/#services:decred.org)聊天室，关注 Decred 生态系统更新。

## 外展

Monde PR 五月份的成绩：

- 向金融和加密出版物投放了 2 个故事
- 回应了 12 项评论/公关机会请求
- 获得2次媒体采访

Monde PR 新闻报道：

- [Brave New Coin](https://bravenewcoin.com/insights/crypto-market-forecast-week-of-may-3rd-2021) 上的一篇文章，介绍了去中心化国库激活的新闻
- [CoinDesk](https://www.coindesk.com/bitcoiners-future-consensus-2018-2021) 上的一篇文章，其中评论了@lukebp 关于他在 Consensus 的经历。这篇文章被联合给[Yahoo! Finance](https://finance.yahoo.com/news/8-400-bitcoiners-went-hilton-200356039.html)
- DCRDEX 整合公告由[Bankless Times](https://www.banklesstimes.com/2021/05/27/decred-announces-initial-dcrdex-integration-into-decrediton-wallet/)和[Crowdfund Insider](https://www.crowdfundinsider.com/2021/05/175918-digital-currency-project-decred-announces-initial-integration-of-its-decentralized-exchange-into-decrediton-wallet/)报道。Crowdfund Insider 文章被联合给[Crypto News BTC](https://cryptonewsbtc.org/2021/05/28/digital-currency-project-decred-announces-initial-integration-of-its-decentralized-exchange-into-decrediton-wallet/), [MCC Exchange](https://mcc.exchange/2021/05/27/digital-currency-project-decred-announces-initial-integration-of-its-decentralized-exchange-into-decrediton-wallet/) 和 [MoneyNow](https://moneynow.cc/decreds-virtual-currency-allocation-announces-initial-integration-of-its-decentralized-wallet-into-decrediton-wallet/)。[CryptoNEXA](https://www.cryptonexa.com/2021/06/02/decred-and-zcash-lead-the-weekly-top/), [CriptoNoticias](https://www.criptonoticias.com/mercados/decred-zcash-lideran-top-semanal-mercado-halla-plena-recuperacion/) 和 [Crypto News](https://cryptonews.com/news/polygon-enjin-decred-uniswap-and-horizen-led-the-market-last-10514.htm)也报道了该公告。加密新闻文章被联合到IQ Stock Market。

## 媒体

精选文章：

- Big Tech on steroids: 为什么 2020 年代将成为“DAO 的十年” 作者：[Dominic Frisby](https://en.wikipedia.org/wiki/Dominic_Frisby) ([MoneyWeek](https://moneyweek.com/investments/alternative-finance/bitcoin-crypto/603213/decade-of-the-dao-decentralised-autonomous-organisation))
- Thinking Out Loud #2: @PermabullNino Decred图表大礼包 ([substack.com](https://permabullnino.substack.com/p/thinking-out-loud-2-decred-charting))

视频:

- 有限的货币供应 - Decred Fundamentals 来自 @phoenixgreen ([youtube](https://www.youtube.com/watch?v=pRIEiCvBYPE))
- 为什么治理很重要 - Decred Fundamentals 来自 @phoenixgreen ([youtube](https://www.youtube.com/watch?v=hrL4sS8HuXg))
- Decred 双周报 - 价值 1.5 亿美元的利益相关者驱动的 DAO 现已上线，DCRDEX 进入钱包，v1.6.2 及更多 @Exitus ([youtube](https://www.youtube.com/watch?v=S_asvjm4lFI))
- 为什么这将是 DAO 的十年 - Dominic Frisby ([youtube](https://www.youtube.com/watch?v=dQLN-DNnVKU))
- Decred 价格分析 -  Josh Olszewicz ([youtube](https://www.youtube.com/watch?v=LUg_DXUHdmg))
- 与 Jake Yocom-Piatt 讨论 Decred Dominic Frisby ([youtube](https://www.youtube.com/watch?v=ZCfIM8IHurU)) - @jy-p 暗示用后量子加密升级混合技术

艺术与娱乐：

- 游戏被操纵 - 革命不会集中 @karamble ([twitter](https://twitter.com/karamblez/status/1398087058892148740))
- [乐高Stakey](https://twitter.com/Talha_Habib/status/1398268623572111362) 由年轻的 hodlers 制作
- @jz 一直忙于#RealDecredMemes标签：[chart/menu](https://twitter.com/jz_bz/status/1391442849808408580), [freedom eagle](https://twitter.com/jz_bz/status/1392177374008053760), levels of voter [enlightenment](https://twitter.com/jz_bz/status/1395560884433473537), [shower thoughts](https://twitter.com/jz_bz/status/1396211915098136578)

翻译:

- Decred 4月报被[翻译成](https://xaur.github.io/decred-news/)阿拉伯语（@arij、@abdulrahman4）和中文（@Dominic）。谢谢你们！

其它非英语内容：

- Decred的新国库覆盖[CriptoNoticias](https://www.criptonoticias.com/comunidad/protocolo-decred-esta-5-dias-descentralizar-tesoreria/)
- 看起来@Dominic 秘密运行了一个新的中文版 Decred 播客，已经发布了 3 集：[首先](https://twitter.com/wanbihou/status/1383625001098649602)是一位匿名硬件工程师关于社区中的事件，[其次](https://twitter.com/wanbihou/status/1388412787076984832)是与 decreder 讨论进行治理，[第三](https://twitter.com/wanbihou/status/1393825045902807041)是 Mable Jiang 的 51% 播客（@Dominic 所在的位置）最近有客人）

![Lego Stakey](img/202105.4.384.jpg)

## 讨论

选定的 Reddit 主题：

- Chia 的[时空证明](https://www.reddit.com/r/decred/comments/n2sdwq/thoughts_on_alternatives_to_proof_of_work/)(PoST) 作为 PoW 的替代品
- 我的 GF 做了一个充满 Decred 的美味[蛋糕](https://www.reddit.com/r/decred/comments/n7l6ca/my_gf_made_this_deliciously_looking_cake_full_of/)
- Decred：[moonshot](https://www.reddit.com/r/decred/comments/ncnmca/decred_a_moonshot_and_the_continuity_of_proof_of/)，以及工作共识证明的连续性
- 我们还[需要](https://www.reddit.com/r/decred/comments/njdrw6/do_we_still_need_centralized_exchanges/)中心化交易所吗？

选定的 Twitter 讨论：

- @lukebp 和 @BuckPerley 之间关于正式与非正式治理的[长期辩论](https://twitter.com/lukebp_/status/1388987670832074758)

> Decred DAO 为整个加密领域实现了一个新的里程碑：数字主权财富基金。
> 
> Decred 网络是最接近数字国家状态的网络。
> 
> 第 1 层的DAO，有自己的金库、自己的交易所、自己的货币和自己的钱包。 ([@ammarooni](https://twitter.com/Ammarooni/status/1390869248910794753))

![space cake exterior](img/202105.5.384.jpg) ![space cake interior](img/202105.6.384.jpg)

_还要有自己的蛋糕！_

## 市场

5 月 DCR 的交易价格在 90.4-229.4 美元 / BTC 0.0027-0.0047 之间。平均每日价格为 173.47 美元。

@PermabullNino 发布了一个["图表狂欢"](https://permabullnino.substack.com/p/thinking-out-loud-2-decred-charting)，其中包含许多 Decred 独有的指标和简洁的评论。40 美元和 BTC 0.004 似乎是许多矿工和利益相关者的重要价格。

@Checkmate 更新了[checkonchain.com](https://checkonchain.com/)，其中包含跟踪[Decred 国库](https://www.reddit.com/r/decred/comments/nakdpc/new_decred_onchain_metric_charts_live/) 和 DCRDEX 交易量的[新图表](https://twitter.com/_Checkmatey_/status/1391743198242885634)。


[DCRDEX](https://dex.decred.org/) 5月交易量为383K DCR和1.4K BTC，日均交易量为12K DCR和46 BTC。

## 相关外部信息

比特币上的 Taproot 激活信号已达到超过 90% 的水平（截至 6 月初约为 97%），并且将在当前信号窗口结束时锁定在 6 月的某个时间。

据报道，伊朗中央银行已禁止“在国外开采”的加密货币交易，以阻止资本外逃。伊朗企业仍然可以从注册的伊朗矿工那里获得加密货币，用于国际支付。

比特币矿池 Marathon Mining开采了一个区块，该区块被描述为“完全符合美国法规”，审查了其认为受到美国财政部制裁或参与暗网活动的实体的交易。尽管他们付出了努力，但还是有一些暗网市场交易进入了这个区块，这旨在成为比特币审查的里程碑。

在 Elon Musk 批评比特币的环境特性并且特斯拉停止接受它作为支付之后，他与 Michael Saylor 等人一起推动了一个新的“比特币矿业委员会，以促进能源使用透明度并加速全球可持续发展计划”。

Ark 的 Cathie Wood在 Consensus 上还表示，对比特币的 ESG（环境社会和治理）担忧意味着“许多机构购买暂停”，并认为 Elon Musk 在这场运动中发挥了作用。

该PoolTogether DAO，与池一起彩票和控制所有POOL令牌超过50％的关联，已投来分散出售的所有POOL令牌，目前由DAO控制的5.38％的持股，以选择风险投资的协议金额700 万美元。VC 购买的 POOL 代币将有 1 年的锁定期，之后的归属期为 1 年。

这是DAO最近实现资产多元化的明显趋势的一部分。

5 月份以太坊闪贷失败的最大受害者是 xToken，攻击者在同一笔交易中利用了两个不同合约中的漏洞，在支付 21,900 美元的交易费以获得闪贷后净赚2450 万美元。

Binance Smart Chain 现在在 DeFi 垃圾箱火灾赌注中为以太坊提供竞争，在 BUNNY 代币因经济剥削而遭受名义上 2 亿美元的错误印刷代币之后，你猜对了，闪电贷款。

Coinbase 正在扩大其职权范围，也成为一家媒体公司，通过其营销部门批准的“事实核查”类型的内容直接面向受众。

这就是五月的全部。在我们解密的#journal聊天中分享您下一期的故事。

## 关于月报

这是Decred Journal的第38期。有关所有问题，镜像和翻译的索引，请参见[这里](https://xaur.github.io/decred-news/)。

在经过最少的健全性检查之后，来自第三方的大多数信息都会直接从来源中继。Decred Journal的作者无权验证所有声明。请当心诈骗，并自行进行调查。

您可以在[此处](https://github.com/xaur/decred-news/labels/next%20release)提交内容，以供撰写下一期月报内容。我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢 (字母排列):

- 写作和编辑: bee, degeri, l1ndseymm, richardred
- 评论和反馈: chappjc, davecgh, dnldd, jholdstock, karamble, lukebp, matheusd, oshorefueled
- 封面图片: saender
- 资助: Decred stakeholders

## 中文社区

* [社区网址](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [bilibili频道](https://space.bilibili.com/425519478)
* QQ群号-258412796
