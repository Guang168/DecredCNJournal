# Decred 月报 – 2023 年 2 月

![](img/202302.1.768.png)

_图片：Decred 生日蛋糕_

二月亮点：

- Decred 达成了运营 7 年的里程碑。
- Decred DEX v0.5.9 进行了bug修复和版本优化，并且有大量关于重大开发进展的报告，v0.6 即将到来。
- Bison Relay v0.1.4 已发布，改进了用户体验，Oprah 打赏机器人现已在 BR 上运行。
- Timestamply 重新设计现已上线。
- 选票价格先是大幅下跌，然后是史诗般的上涨，再创历史新高。

内容：

- [DCRDEX v0.5.9 发布](#dcrdex-v059-release)
- [Bison Relay v0.1.4 发布](#bison-relay-v014-release)
- [开发进展总结](#development)
- [人员](#people)
- [治理](#governance)
- [网络](#network)
- [外展](#outreach)
- [活动](#events)
- [媒体](#media)
- [市场](#markets)
- [相关外部信息](#relevant-external)


## DCRDEX v0.5.9 发布

v0.5.9 随 v0.6 一起发布，为 Umbrel 启用自动部署的 Docker 镜像。但是，此版本中还有许多其它修复是从 v0.6 开发向后移植的：

- 改进客户端数据库压缩以节省磁盘空间。
- 更准确的交易费估算。
- 防止零费用交易。
- 增强性能。
- 清理日志记录。
- 修复了大约十几个边缘错误。

可以在[此处](https://github.com/decred/dcrdex/releases)找到完整的发行说明和独立的 DEX 应用程序下载。包含的散列和签名允许[验证](https://docs.decred.org/advanced/verifying-binaries)下载未被第三方损坏或修改。


## Bison Relay v0.1.4 发布

Bison Relay 在 v0.1.4 中收到了另一个更新：

- 一切都运行得更快。
- 可调字体大小。
- 图片和链接附件。
- 右侧面板可以更轻松地访问对用户和群聊的操作。
- 更强大的密钥交换维护。
- 奖励有价值内容作者的打赏机器人。
- 许多其它用户体验改进。

[此处](https://www.youtube.com/watch?v=Yz-IPu00eDc)提供新功能的简短视频概述。

[在改进的下载页面](https://bisonrelay.org/download/)上获取最新版本。欢迎在[GitHub 问题跟踪器](https://github.com/companyzero/bisonrelay/issues) 和 [#br Matrix 聊天](https://chat.decred.org/#/room/#br:decred.org)中报告错误和反馈。


## 开发进展总结

除非另有说明，否则下面报告的工作为“合并至核心存储库”状态。这意味着该工作已完成、审查并集成到高级用户可以[构建和运行](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c)的源代码中，但普通用户尚不可用。


### dcrd

_[dcrd](https://github.com/decred/dcrd) 是一个完整的节点实现，为 Decred 在全球的点对点网络提供支持。_

大多数更改都集中在使共识部署代码更健壮且更易于理解：

- 重新设计了 [共识部署](https://github.com/decred/dcrd/pull/3056) 验证逻辑和测试，使其更容易修改并使其更符合代码库中使用的更现代的编码实践。 术语“部署”和“议程”指的是[共识投票定义](https://github.com/decred/dcrd/blob/974b1b3ccc7393c5450d75f1f58b75b80020cc3b/chaincfg/mainnetparams.go#L139)，包括描述、投票选择、有效期、 和其他细节。
- 为不同的议程强制执行[全球唯一的投票 ID](https://github.com/decred/dcrd/pull/3057)。 从技术上讲，重复使用投票 ID 并没有错，但是 Decred 生态系统中的各种软件隐含地假设 ID 在所有议程中都是唯一的。 这个不成文的规则现在已经正式化，以防止混淆并简化处理它的代码。
- 跟踪 [共识规则更改](https://github.com/decred/dcrd/pull/3059) 状态的简化代码。
- 添加了一个网络参数以[强制共识投票](https://github.com/decred/dcrd/pull/3060) 到某些结果并相应地激活它们的功能。 这已经被用于测试网络以快速测试功能，而无需经过整个投票过程。 虽然它的工作方式被发现是令人惊讶的行为：“如果在给定网络的参数中找不到部署，则认为它是活动的”。 其他问题包括测试投票过程本身的复杂性，以及这种隐式强制投票在 getblockchaininfo 等命令中是不可见的。 所有这些问题都已修复，现在可以更轻松地在代码中找到强制规则。 还添加了安全检查以确保不能在主网络上使用强制投票选择。

Docker:

- 添加了为特定 Git 版本构建 [Docker 映像](https://github.com/decred/dcrd/pull/3048) 的功能。
- 除了 dcrd 版本之外，还打印 [dcrctl 版本](https://github.com/decred/dcrd/pull/3062)，因为它们现在来自单独的存储库。

其它:

- 由于 Go 1.19，在未导出的模块中切换到新的[原子类型](https://github.com/decred/dcrd/pull/3053)。 这使得代码不太容易出现人为错误，并且不那么冗长。 导出的模块在 [单独的 PR](https://github.com/decred/dcrd/pull/3054) 中升级，稍后将合并到 [主存储库](https://github.com/decred/dcrd/pull/3054#issuecomment-1428189607)到更新的 Go 版本太快了。
- 更新了 [连接请求](https://github.com/decred/dcrd/pull/3055) 跟踪以防止并发错误。
- 修复了基于 [riscv64](https://github.com/decred/dcrd/pull/3049) CPU 架构的 OpenBSD 构建。
- 更新了 [Go 1.20](https://github.com/decred/dcrd/pull/3052) 的构建基础设施和文档，并放弃了对 Go 1.18 的支持。
- 依赖更新。


### dcrwallet

_[dcrwallet](https://github.com/decred/dcrwallet) 是命令行和图形界面钱包应用程序使用的钱包服务器。_

- 修复了 [地址发现](https://github.com/decred/dcrwallet/pull/2204) 中的死锁，该死锁可能由时机不佳的 getnewaddress 命令触发。
- 更新了 dcrd 中的 [`addrmgr` 模块](https://github.com/decred/dcrwallet/pull/2206)，以便在 SPV 模式下可用的质量对等点很少时提高性能。
- 更新了 [golang.org/x 模块](https://github.com/decred/dcrwallet/pull/2209)，包括更新的 `x/sys` 以支持在 [OpenBSD](https://github.com/decred/dcrwallet/pull/2208)上构建在 riscv64 CPU 上运行。


### dcrctl

_[dcrctl](https://github.com/decred/dcrctl) 是 dcrd 和 dcrwallet 的命令行客户端。

- 将 [dependencies](https://github.com/decred/dcrctl/pull/54) 更新为最新模块。 这允许在 OpenBSD riscv64 上构建并且还显着减少了间接依赖性。


### Decrediton

_[Decrediton](https://github.com/decred/decrediton) 是一款功能齐全的桌面钱包应用程序，集成了投票、StakeShuffle 混合、闪电网络、DEX 交易等功能。 它在有或没有完整的区块链（SPV 模式）的情况下运行。_

进行中：

- [更新到 React v18](https://github.com/decred/decrediton/pull/3851)。 它可能需要进行大的更改，但会带来性能改进。


### vspd

_[vspd](https://github.com/decred/vspd) 是用于运行投票服务提供商的服务器软件。 VSP 代表其用户全天候 24/7 投票，不能窃取资金。_

- 检查 [VSP 是否已关闭](https://github.com/decred/vspd/pull/369) 是否更早，在 dcrd/dcrwallet/database 客户端初始化之前。 这样效率更高并且可以防止可能的错误。
- 更新至 [Go 1.20](https://github.com/decred/vspd/pull/368)。
- 测试现在作为 [子测试](https://github.com/decred/vspd/pull/365) 运行，以便更好地报告测试结果和指标。
- 添加了 [错误处理](https://github.com/decred/vspd/pull/363) 的测试，确保 vspd 错误的格式正确，非 vspd 错误包含足够的调试信息。
- 从文档中删除了 [dcrstakepool 说明](https://github.com/decred/vspd/pull/370)，因为它现已失效。


### cspp

_[cspp](https://github.com/decred/cspp) 是一个使用 CoinShuffle++ 协议协调硬币组合的服务器。 它是非托管的，即不持有任何资金。_

- 更新 CI 以使用最新的 [flint2](https://github.com/decred/cspp/pull/69) 数学 [library](http://www.flintlib.org/) 在 Ubuntu 22 上构建。
- 添加了一个 [`solverrpc` 包](https://github.com/decred/cspp/pull/86) 作为现有 `solver` 的直接替代品。 它允许将与 C 代码（flint2 数学库）的交互提取到一个名为“csppsolver”的单独后台进程中，并从更灵活的纯 Go 代码与该进程对话。
- 添加了 [build flags](https://github.com/decred/cspp/pull/87)，允许构建一个完全独立的 `csppsolver` 可执行文件，其中嵌入了 flint2 库。 分发此类可执行文件无需安装 flint2。


### DCRDEX

_[DCRDEX](https://github.com/decred/dcrdex) 是一种非托管的、尊重隐私的交易所，用于去信任交易，由原子交换提供支持。_

[v0.5.9 版本](https://github.com/decred/dcrdex/releases/tag/v0.5.9) 是为了支持 [Umbrel 集成](https://github.com/decred/dcrdex/pull/2153)，但它还包括自 2022 年 12 月左右以来在 `master` 中进行的许多重要修复：

- 调整了哪些 [交换费用](https://github.com/decred/dcrdex/pull/2147) 被认为是 BTC 和 DCR 的“最佳”。 最好的案例费用发生在整个订单在一次匹配中被消耗时，即整个订单的 1 笔交易和 1 次输出。 这会影响下订单时显示的费用预览。
- 自动忽略旧客户端版本生成的非常[旧通知](https://github.com/decred/dcrdex/pull/2144)。
- [更新 Docker 配置](https://github.com/decred/dcrdex/pull/2112)：优化基础镜像，将 DEX 客户端切换为以非 root 用户身份运行，删除不需要的文件，并优化 [Docker 构建](https://github.com/decred/dcrdex/pull/2162)用于生产。 除其他外，它有助于在 [Umbrel 应用商店](https://proposals.decred.org/record/8d83046) 中发布 DEX 客户端。
- 添加了 GitHub 工作流程以构建和发布 [发布 Docker 图像](https://github.com/decred/dcrdex/pull/2127)。
- 更新了 dcrd 的 [地址管理器](https://github.com/decred/dcrdex/pull/2096) 模块以修复在运行测试网 SPV 钱包超过一天时的高 CPU 使用率。
- 修复了存档清理功能报告的已删除[订单和匹配项](https://github.com/decred/dcrdex/pull/2098) 的数量。
- 修复了在某些 macOS 系统上检测到“不符合标准”证书错误时毫无意义的 [重新连接尝试](https://github.com/decred/dcrdex/pull/2130)。
- 修复了客户端在 [账户数据库](https://github.com/decred/dcrdex/pull/2119) 加载失败时尝试运行的问题。
- 依赖更新，包括次要的安全修复。
- 从 12 月至 1 月制作的“master”向后移植了[~14 个其他修复](https://github.com/decred/dcrdex/pull/2153)。

以下所有其他更改都在下一个 [v0.6 版本](https://github.com/decred/dcrdex/milestone/22) 的 `master` 分支中。

客户端更改：

- 在[服务器证书更改](https://github.com/decred/dcrdex/pull/2019) 时处理更多边缘情况。
- 如果不支持资产版本，则隐藏 [order form](https://github.com/decred/dcrdex/pull/2054)。
- 显示代币资产订单的[费用百分比](https://github.com/decred/dcrdex/pull/2110)，如果法定汇率可用于代币及其母资产。
- 允许连接到 DEX 服务器 [仅查看模式](https://github.com/decred/dcrdex/pull/1986) 无需注册，并浏览市场和订单簿。

客户端，忠诚债券进展：

- 为客户实施了主要的[债券生命周期](https://github.com/decred/dcrdex/pull/2036) 机制，包括自动债券轮换。 当当前债券即将到期时，必须在正确的时间用另一个债券替换它才能继续使用 DEX 而不会中断。 添加[图表](https://github.com/decred/dcrdex/blob/7603ead02dc6e040e69b50f8796e3f23aac06e1b/client/core/bond.go#L49)来解释债券的生命周期。
- 实施维护[债券基金储备](https://github.com/decred/dcrdex/pull/2103)。 钱包的一部分资金将保留用于未来的债券以及交易费用的缓冲。 当储备金被强制执行时，钱包提款或交易订单等交易将被限制在较低的可用余额范围内。 钱包余额报告将显示锁定在现有债券中并为未来债券预留的资金。 债券将使用不同于为交易订单提供资金的选币策略。 订单试图消耗更少的输出以最小化费用（可以花费更多的 DCR 并返回多余的零钱），而债券试图将确切的 DCR 数量放入时间锁中（并且不能依赖零钱输出）。 默认情况下，为 DCR 启用掉期交易输入的预先调整大小，因为它有利于债券管理，而且 DCR 费用现在很便宜。 无法禁用未使用债券的帐户。 初始实施仅支持 DCR 债券，但已添加基础以允许其他资产中的债券。
- 将注册 UI 流程更改为 [创建债券](https://github.com/decred/dcrdex/pull/2025) 而不是支付费用。 用户可以选择债券的强度。 如果账户等级低于交易水平并且有未决债券，市场页面将显示用户可以交易之前需要的债券确认。 为手动债券过帐添加了后债券功能。
- 优化[硬币选择](https://github.com/decred/dcrdex/pull/2169) 算法以创建更接近目标 DCR 数量的债券。
- 可以在 [此仪表板](https://github.com/orgs/decred/projects/2/views/1) 上查看债券子系统已完成、正在进行和剩余的任务。
- 在大局中，需要 [fidelity bond](https://en.wikipedia.org/wiki/Fidelity_bond) 从用户*支付费用*到服务器，再到用户在使用服务器时*锁定资金* . 这两种方法都可以保护服务器免受垃圾邮件和其他不良行为的侵害。 债券比费用更复杂，但也有优势。 用户可以在不想交易时返还锁定的资金，债券还支持从独立服务器过渡到去中心化的[服务器网格](https://github.com/decred/dcrdex/issues/1765)（收费 系统不清楚哪些服务器应该收取费用）。

客户端修复：

- 修复了在尚未创建父钱包时创建 [令牌钱包](https://github.com/decred/dcrdex/pull/2121) 的问题。
- 修复了[订单状态](https://github.com/decred/dcrdex/pull/2140) 不同视图的差异。
- 修复了注册页面上令人困惑的 [同步进度](https://github.com/decred/dcrdex/pull/2133) 报告。
- 修复了重复重新获取 [资产图标](https://github.com/decred/dcrdex/pull/2163)。
- 修复了无法从钱包中提取 [all available DCR](https://github.com/decred/dcrdex/pull/2170) 的问题。
- 修复了最近匹配表上的[光标和排序方向](https://github.com/decred/dcrdex/pull/2172)。
- 修复了 [钱包余额](https://github.com/decred/dcrdex/pull/2183) 在为订单提供资金后未更新的问题。
- 修复了 ~4 个并发错误。
- 针对 UI、测试、文档和 Docker 图像优化的其他修复。

以太坊、RPC 数据提供者：

- 添加了 DEX 服务器配置 [多个以太坊数据提供者](https://github.com/decred/dcrdex/pull/2104) 并在活动提供者停止工作时切换到另一个提供者的能力。
- 添加了对 [RPC 提供程序运行状况](https://github.com/decred/dcrdex/pull/2125) 的监控。 以前，只有在所有配置的提供者都可以连接到并具有更新的区块链时，ETH 后端才会启动。 现在，如果至少有一个供应商连接正常并报告一个新区块，ETH 后端将启动。 建立连接后，将持续监控供应商的健康响应，并首先使用最好的供应商。
- 改进了 [已知且合规的 RPC 提供程序](https://github.com/decred/dcrdex/pull/2102) 的管理。
- 修复了尝试使用具有 [太旧的块头](https://github.com/decred/dcrdex/pull/2074) 的 RPC 提供程序的问题，这意味着它们未与网络同步。

以太坊，掉期费优化：

- 使 [交换估计](https://github.com/decred/dcrdex/pull/2129) 了解以太坊区块气体限制。
- 在放弃和因资金不足而失败之前，尝试对 [batched swap](https://github.com/decred/dcrdex/pull/2143)（一次交易中的多次交换）使用较低的 gas 限制。
- 调整 [费用估算](https://github.com/decred/dcrdex/pull/2139) 以降低和更现实的金额。

以太坊，其他变化：

- 阐明了 ETH 及其子代币资产的 API [版本控制](https://github.com/decred/dcrdex/pull/2094)。 目前，令牌资产将使用与父资产相同的版本。 这些版本号将用于确定不同的客户端和服务器是否兼容。
- 从 ETH 和 ERC-20 交换的 Solidity 智能合约中删除了 [`isRedeemable` 方法](https://github.com/decred/dcrdex/pull/2111)，并禁用了 `estimateRedeemGas` 调用。 这两种方法都会在赎回交易之前向以太坊节点揭示一个秘密。 当客户端使用私有节点时，这不是问题，但它成为公共 RPC 提供程序的漏洞，自合并以来 DEX 被迫使用。 Solidity 编译器已更新至 v0.8.18。
- 使用 [go-ethereum](https://github.com/ethereum/go-ethereum) 代码构建 [默认包含](https://github.com/decred/dcrdex/pull/2157)。 go-ethereum 是流行的以太坊软件，支持 DCRDEX 中的 ETH 和 ERC-20 支持。 与 DEX 不同，它是根据 GNU 宽松通用公共许可证 (LGPL) 获得许可的。 对于愿意使用 DCRDEX 的闭源软件来说，此许可证的负担可能是不可接受的，因此添加了一个标志以从构建中排除 go-ethereum。
- 在 [mainnet](https://github.com/decred/dcrdex/pull/2013) 上启用了 ETH 和 USDC 并调整了气体限制。 将兑换交易确认从 10 次减少到 3 次，因为重组 [considered](https://github.com/decred/dcrdex/commit/5c1ff8ab05a43b431f6d8e091692c32ea181e937) 在合并之后非常不可能。 智能合约爱好者可以找到 ETH [此处](https://etherscan.io/address/0x8c17e4968b6903e1601be82ca989c5b5e2c7b400#code) 和 ERC-20 [此处](https://etherscan.io/address/0x1bbd020ddd6dc01f974aa72f223d727) 的新交换合约 ＃代码）。
- @chappjc [tweeted](https://twitter.com/chappjc/status/1623136803661266947) 新合约在主网上与 ETH 和 USDC 执行了许多原子互换。
- Bug修复。

以太坊对权益证明共识的升级（也称为 [The Merge](https://ethereum.org/en/upgrades/merge/)）恰好 [客户端](https://github.com/ethereum/go-ethereum/issues/25623) 被 DCRDEX 使用，尽管有一些[期望](https://blog.ethereum.org/2021/03/24/finalized-no-24) 它会起作用。 这大大延迟了 DCRDEX v0.6，而必须开发解决方法。 在 [轻客户端](https://geth.ethereum.org/docs/fundamentals/les) 固定之前，DEX 用户可以选择运行自己的完整节点或使用像 [Infura](https://www.infura.io/)、[Ankr](https://www.ankr.com/) 和 [其它8个](https://github.com/decred/dcrdex/blob/80b0531a64a806ac8901d812b1e322418118cac1/client/asset/eth/multirpc.go)。

Umbrel 应用商店集成：

- 添加到 Decred GitHub 组织的新存储库用于托管 [Umbrel 集成](https://github.com/decred/umbrel-app-store) 代码。 Umbrel 用户可以按照说明添加此存储库并安装 DCRDEX 包。
- DCRDEX 包已提交至 [官方 Umrel 应用商店](https://github.com/getumbrel/umbrel-apps/pull/430) 进行审核。 与自定义社区应用程序商店不同，它需要集中批准。


### Timestamply

_[Timestamply](https://github.com/decred/dcrtimegui) 是由 Decred 区块链提供支持的免费时间戳文件服务。 时间戳证明某个文件在某个时刻已经存在。 这在保护数据完整性方面有一系列应用。_

- [1 月](202301.md#timestamply) 宣布的完整站点 [重新设计](https://github.com/decred/dcrtimegui/pull/151) 已完成并部署在 [timestamp.decred.org](https //时间戳.decred.org/）。 所有现有数据都已[迁移](https://proposals.decred.org/record/855a506/comments/20)。
- 添加了一个新的 API 方法，该方法返回由 dcrtime 服务器标记的 [last digests](https://github.com/decred/dcrtime/pull/84)。 它由新的 GUI 使用。
- 升级到 [Node v16](https://github.com/decred/dcrtimegui/pull/152)。


### Documentation

_[dcrdocs](https://github.com/decred/dcrdocs) 是 Decred [用户文档](https://docs.decred.org/) 的源代码。_

- 更新到 [MkDocs Material v9](https://github.com/decred/dcrdocs/pull/1214)，改进了搜索。
- 删除了 [Font Awesome](https://github.com/decred/dcrdocs/pull/1216) 图标，因为它们不起作用并且只出现在几页上。


### Bison Relay

_[Bison Relay](https://github.com/companyzero/bisonrelay) 是一个新的社交媒体平台，由 Decred Lightning Network 提供强大的审查、监视和广告保护。_

v0.1.4 版本中 GUI 和 CLI 应用程序的常见更改：

- 添加了支付和发送[多条消息并行](https://github.com/companyzero/bisonrelay/pull/98) 的支持，无需等待服务器确认，这使得发送速度更快。
- 在私人聊天和群聊中添加了对[发送和呈现嵌入](https://github.com/companyzero/bisonrelay/pull/118)（如图像和下载链接）的支持。
- 改进了对加密状态的跟踪和[密钥交换 (KX) 重置](https://github.com/companyzero/bisonrelay/pull/116) 的维护。 添加了半自动工具来检测和重置可能损坏的密钥交换。 重置的候选者是长时间没有收到消息的用户，或者如果自己的客户端已经长时间离线的所有用户。
- 改进了对刚 [连接](https://github.com/companyzero/bisonrelay/pull/130) 到服务器后收到的新群聊消息的处理。 这应该显示按时间正确排序的消息，尤其是在连接速度较慢的情况下。
- 修复了在某些情况下阻止 [clean shutdown](https://github.com/companyzero/bisonrelay/commit/ec5637968937439eb8752aa41200947051b2f8c0) 的错误。
- 修复了由于客户端尝试 [重新使用相同的付款](https://github.com/companyzero/bisonrelay/pull/131) 而导致的可能的重新连接循环。

v0.1.4 版本中的 GUI 应用更改：

- 添加了 [字体大小设置](https://github.com/companyzero/bisonrelay/pull/117)，有 4 种大小可供选择。
- 将用户和群聊的菜单操作（列表帖子、支付小费等）移动到[右侧面板](https://github.com/companyzero/bisonrelay/pull/119)。 这类似于 Element 并且更易于使用。
- 聊天列表的顺序在应用程序重新启动时 [已保存](https://github.com/companyzero/bisonrelay/pull/111)。
- 使用 [emoji 字体](https://github.com/companyzero/bisonrelay/commit/41fd091af874512d7a3d941f094c1615e54ee70b) 渲染更多字符和表情符号。

v0.1.4 版本中的命令行应用更改：

- 删除了 Ctrl+C 作为退出快捷方式。
- 如果视图不在底部，则删除[自动滚动到底部](https://github.com/companyzero/bisonrelay/commit/9324add82f4f7bd5317a31f14c8f78618e79e856)。
- 提醒当前窗口[已完成下载](https://github.com/companyzero/bisonrelay/commit/fdad19d95a140125019daa5bbb929ed6892df2f2)。
- 添加了 [未读消息标记](https://github.com/companyzero/bisonrelay/commit/e03164fcdf3c168cb772bde17310a003de8418f6) 到非活动窗口。
- 其他修复和依赖更新。

服务器和 v0.1.4 中的其他更改：

- 添加了对[同时](https://github.com/companyzero/bisonrelay/pull/97)接受多条消息的支持。 默认情况下，连接的客户端在需要支付之前可以请求最多 8 张消息发送发票。 服务器必须在 24 小时内检测到付款，否则将需要重新付款。 生产服务器可能为此使用不同的参数。
- [存储收到的消息](https://github.com/companyzero/bisonrelay/pull/110) 以便 `clientrpc` 用户可以检索它们。 这可以防止机器人和其他自动化工具中遗漏消息。

GUI 和 CLI 应用程序的常见更改合并到下一个版本 (v0.1.5) 的 `master` 中：

- 添加了 [警告](https://github.com/companyzero/bisonrelay/pull/139) 提醒用户 LN 发票生成失败并建议增加接收容量。
- 添加了[群聊的版本控制](https://github.com/companyzero/bisonrelay/pull/140) 和不支持的群聊版本的警告。
- 添加了向其成员[重新发送群聊信息](https://github.com/companyzero/bisonrelay/commit/dc63dafcad9dad4e1db105418e642ea50349896f) 的命令，以解决用户列表不同步的问题。
- 修复了应用重启后的[群聊消息排序](https://github.com/companyzero/bisonrelay/pull/136)。

`master` 中的 GUI 应用程序更改：

- 添加了一条水平线，用于标记收到的 [未读消息](https://github.com/companyzero/bisonrelay/pull/137) 的开始。 如果后续消息来自同一作者，则删除头像和用户名的显示。
- 添加总 DCR [发送和接收](https://github.com/companyzero/bisonrelay/pull/146) 摘要到支付统计页面。
- 为存款地址添加了[二维码](https://github.com/companyzero/bisonrelay/pull/148)。
- 在提示打开更多LN通道的页面默认隐藏[高级选项](https://github.com/companyzero/bisonrelay/pull/150)。
- 修复了打开聊天部分时 [活动聊天](https://github.com/companyzero/bisonrelay/pull/145) 选择丢失的问题。

`master` 中的 CLI 应用程序更改：

- 打开通道和[请求接收容量](https://github.com/companyzero/bisonrelay/pull/147)的简化代码。
- 允许指定嵌入式 dcrlnd 实例将监听的 [自定义 IP 地址](https://github.com/companyzero/bisonrelay/pull/149)，而不是默认的“127.0.0.1”。
- 改进了[文本换行](https://github.com/companyzero/bisonrelay/pull/132) 和多行元素的渲染。
- 添加了[密钥交换调解](https://github.com/companyzero/bisonrelay/pull/134) 和[作者昵称](https://github.com/companyzero/bisonrelay/pull/151) 到使用的自动化 API 通过机器人和其他工具。

其他的东西：

- 奥普拉出局了！ 这是一个打赏机器人，它会关注用户并奖励他们发表实质性的帖子或评论。 在 [#br Matrix chat](https://chat.decred.org/#/room/#br:decred.org) 中询问如何从 Oprah 那里获得提示。


## People

Community stats as of Mar 1 (compared to Feb 2):

- [Twitter](https://twitter.com/decredproject) followers: 53,064 (-204)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 12,660 (-3)
- [Matrix](https://chat.decred.org/) #general users: 750 (+8)
- [Discord](https://discord.gg/GJ2GXfz) users: 1,557, verified to post: 932 (+6)
- [Telegram](https://t.me/Decred) users: 2,756 (-60)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,630 (-10), views: 224.6K (+2.3K)


## Governance

In February the new [treasury](https://dcrdata.decred.org/treasury) received 7,620 DCR worth $183K at February's average rate of $24.03. 3,389 DCR was spent to pay contractors, worth $81K at February's rate.

The [treasury spend tx](https://explorer.dcrdata.org/tx/e09505dbb877e5efdd184129858be5655a3de235cdac2cfa749442f0ccf7de81) had 27 outputs making payments to contractors, ranging from 3 DCR to 1,084 DCR. Most of this DCR was likely paid for December invoices, there is now a persistent lag between the end of the month and the creation of the TSpend for that month, so that by the time transactions are approved by stakeholders it is typically two months after the month when work was conducted. At December's billing rate of $19.79 the February TSpend is equivalent to $67K.

![](../img/202302.2.720.png)

_Image: Decred Treasury monthly inflows and outflows._

As of Mar 14, combined balance of [legacy](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) and [new treasury](https://dcrdata.decred.org/treasury) is 844,504 DCR (16.8 million USD at $19.88).

![](../img/202302.3.720.png)

_Image: Decred Treasury balance history._

There were no new proposals published in Feb, and the proposals which finished voting in the month were covered in the [January issue](202301.md#governance) of the Journal.


## Network

**Hashrate**: February's [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&scale=linear&bin=day&axis=time) opened at ~73 Ph/s and closed ~71 Ph/s, bottoming at 60 Ph/s and peaking at 83 Ph/s throughout the month.

![](../img/202302.4.720.png)

_Image: Decred hashrate._

Distribution of 66 Ph/s hashrate [reported](https://miningpoolstats.stream/decred) by the pools on Mar 1: Poolin 51%, F2Pool 38%, AntPool 11%, CoinMine 0.4%.

Distribution of 1,000 blocks actually [mined](https://miningpoolstats.stream/decred) by Mar 1: Poolin 54%, F2Pool 36%, AntPool 6%, likely BTC.com 4%.

![](../img/202302.5.720.png)

_Image: Historical pool hashrate distribution._

**Staking**: [Ticket price](https://dcrdata.decred.org/charts?chart=ticket-price&axis=time&visibility=true-true&mode=stepped) varied between 207-496.5 DCR, with 30-day [average](https://dcrstats.com/) at 263.8 DCR (+51.3).

After a dramatic drop to 140 DCR in January ticket price skyrocketed to set a new all-time high of **496.5 DCR**. It returned to normal levels a week later and settled around 230 DCR.

![](../img/202302.6.720.png)

_Image: Ticket price made its biggest swing in history._

The [locked amount](https://dcrdata.decred.org/charts?chart=ticket-pool-value&scale=linear&bin=day&axis=time) was 8.76-9.69 million DCR, meaning that 58.5-64.9% of the circulating supply [participated](https://dcrdata.decred.org/charts?chart=stake-participation&scale=linear&bin=day&axis=time) in Proof of Stake. This was also more volatile than usual.

![](../img/202302.7.720.png)

_Image: Drop and recovery of DCR locked in PoS._

**VSP**: The [16 listed VSPs](https://decred.org/vsp/) collectively managed ~7,410 (-980) live tickets, which was 18.4% of the ticket pool (-0.4%) as of Mar 1.

The only gainers in February were dcrhive.com (+383 tickets or +74%) and vsp.decredcommunity.org (+202 tickets or +38%). The other 14 VSPs lost ~25% tickets on average, but the loss should be considered in context of the ticket pool size correcting from abnormal ~44,880 down to its target of 40,960 tickets.

![](../img/202302.8.720.png)

_Image: Distribution of tickets managed by VSPs._

**Nodes**: [Decred Mapper](https://nodes.jholdstock.uk/user_agents) observed between 175 and 188 dcrd nodes throughout the month. Versions of 176 nodes seen on Mar 1: v1.7.5 - 34%, v1.7.1 - 22%, v1.8.0 dev builds - 13%, v1.7.2 - 11%, v1.7.0 - 10%, v1.7.4 - 3%, other - 7%.

![](../img/202302.9.720.png)

_Image: Historical dcrd version distribution, data from nodes.jholdstock.uk. Data until Jan 2023 was incomplete._

The share of [mixed coins](https://dcrdata.decred.org/charts?chart=coin-supply&zoom=jz3q237o-la8vk000&scale=linear&bin=day&axis=time&visibility=true-true-true) varied between 59.2-60.4%. Daily [mixed volume](https://dcrdata.decred.org/charts?chart=privacy-participation&bin=day&axis=time) varied between 206-865K DCR.

Since a large portion of mixed coins comes from staking, the drop of staked DCR has resulted in a drop of mixed volume as well. It went back to normal towards the end of February as stake participation recovered.

![](../img/202302.10.720.png)

_Image: Drop and recovery of mixed and unspent coin percentage._

![](../img/202302.11.720.png)

_Image: Daily mix volume varied more than usual._

Decred's [Lightning Network](https://ln-map.jholdstock.uk/) explorer has seen 158 nodes (+11), 305 channels (+44) with a total capacity of 115 DCR (+9), as of Mar 1. These stats vary depending on the LN node. For example, @karamble's node reported 172 nodes (+12), 385 channels (+38) and 168 DCR (+9) capacity on same Mar 1.


## Outreach

Monde PR's achievements:

- Secured 1 media interview
- Pitched 3 commentary opportunities
- Pitched 4 media opportunities

Secured the following media placements:

- Bison Relay was featured in [Blockworks](https://blockworks.co/news/web3-social-media-apps-to-watch) as a "Web3 social media app to watch".
- A [Decred Magazine article](https://www.decredmagazine.com/planbs-s2f-model-is-flawed/) featuring commentary from @jz on the flaws in PlanB's S2F model.
- A [Decred Magazine article](https://www.decredmagazine.com/middlemen-need-to-be-eliminated-from-the-cryptocurrency-space/) featuring commentary from @jz on eliminating middlemen from the cryptocurrency space.

Commentary on Decred Magazine was originally drafted for a crypto publication but was not used. Instead of throwing it away it was repurposed and published on DM.


## Events

**Attended:**

- @arij organized a celebration of Decred's 7th anniversary at Technopark Casablanca for around 60 guests. The event began with a presentation of the project and its major milestones over the years, followed by remarks from the project's partners. New version of Decred Cake was spotted at the party. See more details in the [report](https://decredcommunity.github.io/events/index/20230205.1).

![](../img/202302.12.720.jpg)

_Image: Decred 7th birthday cake._


## Media

Nostr users [can now follow](https://twitter.com/decredproject/status/1626112166448271360) Decred announcements at: `npub1decredzl29afqaalgw79kzz7cscrakzul00zgq9qymt4weqg03fsqmmnzd` ([preview](https://iris.to/#/profile/npub1decredzl29afqaalgw79kzz7cscrakzul00zgq9qymt4weqg03fsqmmnzd)). Post your public keys in [this thread](https://www.reddit.com/r/decred/comments/10vnmmo/decred_on_nostr/) to help bootstrap a Decred community on Nostr.

**Selected articles:**

- [Middlemen need to be eliminated from the cryptocurrency space](https://www.decredmagazine.com/middlemen-need-to-be-eliminated-from-the-cryptocurrency-space/) by @HassanMaishera
- [$3.8 billion worth of crypto stolen! What can be done?](https://www.decredmagazine.com/u-3-8-billion-worth-of-crypto-stolen-what-can-be-done/) by @Joao
- [Internet privacy and why it is important](https://www.decredmagazine.com/internet-privacy-and-why-it-is-important/) by @BlockchainJew
- [Decred vs Firo: privacy and governance!](https://www.decredmagazine.com/decred-vs-firo-privacy-and-governance/) by @Joao

Decred Magazine engagement stats for February:

- Total number of articles on DM: 409
- Newsletter subscribers: 88
- New DM posts and newsletters sent: 17
- Active social media campaigns: 32
- Completed social media campaigns: 32
- Social media posts: 143
- Likes: 678
- Re-tweets: 148
- Social media followers across all platforms and accounts (including [@DecredSociety](https://twitter.com/DecredSociety)): 1,220

Decred Magazine has started building an audience on TikTok. Engagement with [@decredmagazine](https://www.tiktok.com/@decredmagazine) is greatly appreciated.

**Videos:**

- [Installing Decrediton in fully validating mode - Decred Fundamentals](https://www.youtube.com/watch?v=JxLMi5fWL80) by @phoenixgreen
- [Decred News - ERC20 pairs on DEX, new ticket price ATH, exciting new proposals for DCR DAO & more](https://www.youtube.com/watch?v=9fJ92YxL_pU) by @Exitus
- [Decrediton SPV mode and importing seed phrase - Decred Fundamentals](https://www.youtube.com/watch?v=K1zUdxsrgJM) by @phoenixgreen
- [Decrediton peer to peer payments - send & receive](https://www.youtube.com/watch?v=DRWJ9Ajh6II) by @phoenixgreen
- [Bison Relay updates to version 0.1.4](https://www.youtube.com/watch?v=Yz-IPu00eDc) by @phoenixgreen

Livestream:

- [Decred Roundtable - The next crypto craze](https://www.youtube.com/watch?v=ntJO1Ckmj4M) feat. @phoenixgreen, @Exitus, @DCR\_Jay, and @Laurent - discussing the [motorsports proposal](https://proposals.decred.org/record/2b19c56) and next big things in crypto.

**Audio:**

Twitter Spaces:

- [Bitcoin.jpg: "We're putting it all on chain!"](https://twitter.com/WasPraxis/status/1620938664879554560) by @Tivra discussing NFT and Ordinals use case on Bitcoin - mirrored on [Anchor](https://anchor.fm/decred-magazine/episodes/Bitcoin-jpg-Were-putting-it-all-on-chain-e1ud6gq)
- [Decred's 7th birthday bash](https://twitter.com/decredproject/status/1622721223913271299) by @Tivra feat. Decred community, discussing seven years of Decred, where it's been, and where it's headed - mirrored on [Anchor](https://anchor.fm/decred-magazine/episodes/Decreds-7th-Birthday-Bash-e1um58e)
- [Fair game or rigged system - On proof-of-work and ASIC production](https://www.decredmagazine.com/fair-game-or-rigged-system-on-proof-of-work-and-asic-production/) by @Tivra feat. David Vorick, discussing his experiences in the ASIC production game and question its fairness - mirrored on [Anchor](https://anchor.fm/decred-magazine/episodes/Fair-Game-or-Rigged-System---On-Proof-of-Work-and-ASIC-Production-e1v382d), plus an edited and condensed version on [YouTube](https://www.youtube.com/watch?v=n8Wz5Zx0MSs)

**Art and fun:**

- [Clay Stakey riding clay bison](https://twitter.com/RichardRed0x/status/1622676008955412480) by @richardred
- @karamble's animations for [Bison Relay](https://twitter.com/karamblez/status/1624099752555032602), more [Bison Relay](https://twitter.com/karamblez/status/1625176367573700615), and [DCRDEX](https://twitter.com/karamblez/status/1629475704088805378) ETH+USDC dev update
- [Bison Relay stickers](https://www.reddit.com/r/decred/comments/10rvh06/join_the_herd_bison_relay_stickers/) - a design by [@TofuPixel](https://twitter.com/TofuPixel) that can be used on social media or printed as a sticker to promote BR
- [Decred a crypto unicorn](https://www.decredmagazine.com/decred-a-crypto-unicorn/) by @OfficialCryptos

> Decred is a true unicorn among the established cryptocurrencies. It's commonly described as an extremely versatile creature, a symbol of crypto purity and grace.

**Translations:**

- [Peer-to-peer electronic corporation](https://www.decredmagazine.com/peer-to-peer-electronic-corporation/) by @Tivra - [in Chinese](https://github.com/DominicTing/decred-ZH-translations/blob/master/Peer-to-Peer%20Electronic%20Corporation.md) by @Dominic
- Decred Journal December-January got a total of 3 new [translations](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic) and Polish (@kozel). Thank you all for spreading Decred's message!

**Non-English content:**

- [Weekly crypto market review & Decred](https://www.youtube.com/watch?v=ZLBrCKKNkPs) by @FIMA (Croatian)
- [Decred overview and price prediction](https://www.youtube.com/watch?v=vmdAarp-Lew) (French)

**Discussions:**

- [360 DCR per ticket, is this a record high?](https://www.reddit.com/r/decred/comments/10qtjtj/360_dcr_per_ticket_is_this_a_record_high/)

**Other:**

- Educational thread about [how Decred DAO is funded](https://twitter.com/toddfmaki/status/1622136960407183360) by @toddfmaki
- Educational thread about [Bison Relay](https://twitter.com/karamblez/status/1623621101027835904) by @karamble


## Markets

In February DCR was trading between USDT 21.71-28.52 and BTC 0.00095-0.00121. The average daily rate was $24.03.

![](../img/202302.13.720.png)

_Image: DCRDEX monthly volume in USD._


## Relevant External

Localbitcoins, the longstanding facilitator of person to person Bitcoin exchanges, is [closing down](https://www.coindesk.com/business/2023/02/09/bitcoin-exchange-localbitcoins-to-close-citing-market-conditions/). After 10 years in action Localbitcoins could not withstand the "ongoing very cold crypto winter", and suspended trading on Feb 16, remaining online only for users to withdraw any balances.

Crypto exchange Kraken has [settled](https://www.sec.gov/news/press-release/2023-25) with the SEC over "Unregistered Offer and Sale of Crypto Asset Staking-As-A-Service Program" and agreed to "Pay $30 Million to Settle SEC Charges". This has been presented as part of a larger [crackdown](https://www.wsj.com/articles/sec-is-cracking-down-on-crypto-staking-heres-what-to-know-f0922151) on exchange provided staking services, where exchanges generate revenue by staking users' tokens and pay some proportion of this to the token holders. The stated motivation for these actions is to provide investors with reliable information about what custodians of their tokens are using them for, but as Kraken CEO Jesse Powell has [tweeted](https://twitter.com/jespow/status/1624177588074848256), this is not as easy as filling in a form, and for companies that have tried to engage with the approval process it has [not gone well](https://twitter.com/lex_node/status/1626609794260803584).

The Oasis DeFi protocol was used to "[counter-exploit](https://www.blockworksresearch.com/research/we-do-a-little-counter-exploit)" the hacker who stole 120,000 ETH from the Wormhole bridge in Feb 2022 and steal back funds they had deposited in the platform, after its developers were [ordered](https://blog.oasis.app/statement-regarding-the-transactions-from-the-oasis-multisig-on-21st-feb-2023/) to by a British High Court. After the Wormhole Bridge was exploited last year, Jump Crypto (its VC backer) stepped in to make users whole and has since been tracking the stolen funds with a view to retrieval. As [reported](https://blockworks.co/news/jump-crypto-wormhole-hack-recovery) by Blockworks, Jump Crypto likely played a key role in the retrieval, they provided funds to reclaim the collateral and close open positions and it is likely they are also the "Whitehat group" referenced in the Oasis blog post who provided a proof of concept on how the assets could be retrieved. The counter-exploit involved an upgradeable contract and adding a new signer to the 4-of-12 multisig that owns the Oasis contracts. It is not clear what the process was to generate the court order to perform the exploit.

Optimism, a layer 2 Ethereum chain, [performed](https://optimism.mirror.xyz/lPZEkFF7LU2ZlrO-dsV3p_LtWQUaknFGfxFMgSz3vGA) its second airdrop, sending 11.7 million OP tokens to over 300,000 addresses. This airdrop rewarded users who delegated their OP for governance, and users who spent more than $6 on gas fees, along with multipliers for delegating more for longer or using more gas. Optimism is committed to distributing 19% of its supply in airdrops, and the first one in May 2022 distributed 5%.

Facebook parent Meta [reported](https://www.coindesk.com/business/2023/02/01/facebook-parent-metas-metaverse-division-lost-137b-in-2022/) losses of $13.7 billion in its Metaverse Division for 2022, and warned that the losses would accelerate further in 2023.

India is [aiming](https://www.coindesk.com/policy/2023/02/08/unpacking-indias-cbdc-pilots-as-country-prepares-for-digital-rupee/) to launch its CBDC by the end of 2023 and has two ongoing trials for a wholesale and retail facing CBDC which have been expanding, but not without difficulty. India already has a ubiquitous Unified Payments Interface (UPI) operated by banks which is widely used and exposes user data to the bank operators - the retail CBDC is seen as a way to offer a more cash-like and privacy respecting means of making payments without bank intermediaries.

The United Arab Emirates (UAE) central bank [announced](https://www.coindesk.com/policy/2023/02/13/uae-plans-to-issue-a-cbdc-to-promote-digital-payments/) plans to issue a CBDC for domestic and cross-border payments as part of a new project to accelerate digital transformation.

In January National Australia Bank [became](https://www.afr.com/companies/financial-services/nab-creates-a-stablecoin-in-boost-for-digital-economy-20230117-p5cd8f) the second major Australian bank to create a stablecoin (AUDN) to allow business customers to settle transactions on blockchain technology in real-time using Australian dollars. They aim to launch mid-year and support transactions including overseas payments and carbon credit trading, and the stated purpose is to boost the digital economy. This comes 9 months after Melbourne based rival ANZ created a similar product (A$DC). The Reserve Bank of Australia is exploring use cases for CBDC and will choose some pilot projects in the first half of 2023.

That's all for February. Share your updates for the next issue in our [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat room.


## About

This is issue 56 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from the source after a minimal sanity check. The authors of the Decred Journal cannot verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing, editing, publishing: bee, bochinchero, Exitus, jz, karamble, l1ndseymm, phoenixgreen, richardred
- reviews and feedback: davecgh, kozel
- title image: arij, Exitus
- funding: Decred stakeholders
