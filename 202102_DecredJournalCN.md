# Decred月报 – 2021年2月

![abstract art](img/202102.1.github.png)

_图片：@saender

二月亮点：

- v1.6.1软件已发布，相较于1.6版本进行了bug修复和UX改进
- 在强制矿工升级的政策发布之后，PoW和PoS达到升级阈值
- PoS参与度达到新高，混合DCR的比例从31％上升到38％
- 推出并发布了面向专业用户的dcrwallet前端Kohola
- 利益相关者在Politeia投票批准了Decred月报和开源研究2021制作的提案

内容：

- [v1.6.1补丁发布](#补丁发布)
- [为新共识规则投票!](#为新共识规则投票)
- [开发进展总结](#开发进展总结)
- [人员](#人员)
- [治理](#治理)
- [网络](#网络)
- [整合](#整合)
- [外展](#外展)
- [活动](#活动)
- [媒体](#媒体)
- [社区讨论](#社区讨论)
- [市场](#市场)
- [相关外部信息](#相关外部信息)

## v1.6.1补丁发布

新[版本](https://twitter.com/decredproject/status/1364636813168693252)对dcrd，dcrwallet，Decrediton和dcrdex的bug进行了修复以及UX改进。大多数更改都在解决新VSP的问题。重要的是，它允许Decrediton用户使用旧版VSP和新版VSP设置共识投票偏好。

在[此处](https://github.com/decred/decred-binaries/releases/tag/v1.6.1)获取完整的发行说明和下载，或在下面的部分中阅读压缩的变更概述。与往常一样，请[验证](https://docs.decred.org/advanced/verifying-binaries/)软件签名，以确保您可以完全运行开发人员打包的内容。

新的VSP +混合组合中仍然存在一些粗糙的地方，请通过u / mowmowbeans撰写的此[文章](https://www.reddit.com/r/decred/comments/m3k31o/161_things_ive_learned/)以了解解决方法。

为了快速了解Decrediton更新，请查看@Exitus的[混币](https://www.youtube.com/watch?v=QC65PBNwAK4)和[staking](https://www.youtube.com/watch?v=olWfTqw16OQ)视频教程。

## 为新共识规则投票!

3月12日开始进行投票，以激活去中心化国库，投票将一直持续到4月9日。

要了解详情，请阅读原始[提案](https://proposals.decred.org/proposals/c96290a)，技术[规格](https://github.com/decred/dcps/blob/master/dcp-0006/dcp-0006.mediawiki)或观看@matheusd的[视频解析](https://www.youtube.com/watch?v=BdTLKAassvc)（大约14分钟开始）。

如果您尚未设置投票偏好，请[进行设置](https://www.reddit.com/r/decred/comments/lu1af0/psa_upcoming_decentralized_treasury_consensus/)，以便在您的任何票证投票时投出所需的票数。新提案的正确编号为`treasury`。

要查看投票如何进行，请查看投票[仪表板](https://voting.decred.org/)或dcrdata的[可视化](https://explorer.dcrdata.org/agenda/treasury)文件。

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以[构建和运行](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c)的源代码中，但对于普通用户来说，还不能使用。

**[dcrd](https://github.com/decred/dcrd)**

v1.6.1修补程序版本进行了以下更改：

- [修改了](https://github.com/decred/dcrd/pull/2597)通知逻辑，迫使工作量证明矿工进行升级，以便可以开始对新的共识更改进行投票
- 修复了网络中断后可能无法重新建立连接的罕见[问题](https://github.com/decred/dcrd/pull/2582)

在面向[下一个发行版](https://github.com/decred/dcrd/milestone/26)的开发中，本月的重点是增加了[UTXO缓存](https://github.com/decred/dcrd/pull/2591)，该缓存将初始区块链同步时间减少了约33％，但需要一些额外的内存。通过允许在刷新间隔之间创建和使用条目以完全避免写入，它还可以显著加速正常操作期间的块处理，并减少存储介质上的磨损。UTXO缓存是迈向多[对等](https://github.com/decred/dcrd/issues/1145)并行区块下载的必需步骤。

另一个亮点是[引入了](https://github.com/decred/dcrd/pull/2579)按高度划分的Bloom过滤器。APBF是一种查找设备，可以快速判断它是否包含某些元素。它可以使用很少的内存来跟踪大量数据，但以可控的误报率为代价。与经典的Bloom过滤器不同，它可以通过老化和丢弃旧项来处理无限量的数据。向Decred添加APBF的动机是替换LRU（最近最少使用）高速缓存，该高速缓存用于连续跟踪已知其它对等方拥有的数据。举一个具体的例子，使用APBF时，用于跟踪125个对等节点已知地址的内存从〜200 MiB减少到〜5 MiB。而且，该过滤器将对其它项目有很大[帮助](https://matrix.to/#/!zefvTnlxYHPKvJMThI:decred.org/$ulmCeMPuDSSmt3KTB09fJpypa4fpooFILTXKtQNWUCg)，例如钱包，DEX，移动钱包等。请在[PR](https://github.com/decred/dcrd/pull/2579) 和 [README](https://github.com/decred/dcrd/tree/master/container/apbf)中全面阅读详细信息。

其它工作：

- 借助智能位级数学，apbf程序包中的主要[运算速度](https://github.com/decred/dcrd/pull/2584)提高了两倍以上
- 跟踪最近[确认](https://github.com/decred/dcrd/pull/2580)的交易和交换给使用APBF的对等方已知的[地址](https://github.com/decred/dcrd/pull/2583)
- 跟踪最近[被拒绝](https://github.com/decred/dcrd/pull/2590)的交易也切换到了APBF，具有在高拒绝情况下降低带宽使用率。
- `reject`信息弃用朝着未来版本迁移

**[dcrwallet](https://github.com/decred/dcrwallet)**

v1.6.1修补程序附带的更改：

- 新的gRPC方法可通过新的vspd协议（由Decrediton使用）在关联的VSP上设置[投票选择](https://github.com/decred/dcrwallet/pull/1981)
- 当帐户只有一个输出时，创建一个额外的交易以为购买VSP票证提供足够的[输出](https://github.com/decred/dcrwallet/pull/1980)，并使用产生的[费用](https://github.com/decred/dcrwallet/pull/2005)输出（修正“ utxos不足”的[错误](https://www.reddit.com/r/decred/comments/lebx71/error_when_trying_to_purchase_tickets_with/)）
- 选择输出时跳过[未发布](https://github.com/decred/dcrwallet/pull/1985)的交易，并在挖掘tx时清除未发布状态（修复某些重复支出的情况）
- 混币时考虑[交易费](https://github.com/decred/dcrwallet/pull/1992)以避免混合输出
- 修复了在混币期间支付[非常高费用](https://github.com/decred/dcrwallet/pull/2002)的可能性
- 更新了salsa20和blake2b[依赖项](https://github.com/decred/dcrwallet/pull/1998)以防止可能出现的内存损坏
- 如果交易没有输入，则返回[错误](https://github.com/decred/dcrwallet/pull/1990)`signrawtransaction`
- 保存[混合](https://github.com/decred/dcrwallet/pull/1989)输出交易并观察输出

**[Decrediton](https://github.com/decred/decrediton)**

v1.6.1修补程序附带的更改：

- 对vspd选票实施的共识投票[偏好](https://github.com/decred/decrediton/pull/3200)选择
- 在混币器，自动购票正在运行时，[禁用](https://github.com/decred/decrediton/pull/3231)一些按钮，以避免可能出现的问题
- 在传统模式和vspd模式之间切换时，请禁用[自动购买](https://github.com/decred/decrediton/pull/3182)，以防止意外购票
- 为购票添加[健全性](https://github.com/decred/decrediton/pull/3230)检查，以防止遗留格式错误的旧版VSP票
- 支持通过多个[条件](https://github.com/decred/decrediton/pull/3194)过滤交易
- 改进了小屏幕上的[staking统计数据](https://github.com/decred/decrediton/pull/3205)和[交易记录](https://github.com/decred/decrediton/pull/3195)的布局
- 显示混合和未混合[帐户](https://github.com/decred/decrediton/pull/3225)的不同图标
- 显示一条[信息](https://github.com/decred/decrediton/pull/3252)，解释为什么有时购买的选票少于所要求的数量
- 在5秒钟内未收到VSP状态响应时显示[超时](https://github.com/decred/decrediton/pull/3199)错误
- 在总览上显示[未确认](https://github.com/decred/decrediton/pull/3254)的余额
- 更好的标签[名称](https://github.com/decred/decrediton/pull/3219)
- 添加了繁体中文[翻译](https://github.com/decred/decrediton/pull/3086)
- 使用挂钩和CSS模块继续迁移到功能组件
- 增加自动化测试范围
- 22个bug修复

合并中：

- 迁移到[grpc-js](https://github.com/decred/decrediton/pull/2936)依赖项以减少构建时间和二进制文件大小
- 将UI[语言](https://github.com/decred/decrediton/pull/3134)更改应用到菜单栏和上下文菜单，而无需重新启动Decrediton
- 修复“隐私”页面上占用大量[CPU](https://github.com/decred/decrediton/pull/3123)的动画
- 其他3个bug修复

**[Politeia](https://github.com/decred/politeia)**

- 管理员帐户的端到端[测试](https://github.com/decred/politeiagui/pull/2297)

CMS:

- 发票中列出的分包商的[代码统计信息](https://github.com/decred/politeiagui/pull/2299)
- 默认显示[更多数据](https://github.com/decred/politeiagui/pull/2298)，以防止丢失新发票
- 用户界面修复

大部分工作再次集中在新的存储后端上。为了将Decred的实现与原始的tlog区别开来，引入了一个新的术语“ tstore”，这意味着将Trillian透明日志和保存实际数据的键值存储结合起来。自2020年4月以来，tstore[拉取请求](https://github.com/decred/politeia/pull/1180)已累计438次提交，并且正在更改超过4万行代码。

最近的后端更改涉及如何在未经审查和经过审查的状态下存储数据。在前端，开发人员正在调整 [GUI](https://github.com/decred/politeiagui/pull/2306)以适应后端API的更改。

> 我对新的插件架构感到非常兴奋。仅使用config选项，就可以启动不同的Politeia应用程序而无需编写任何代码。将相同的插件体系结构添加到politeiawww中以提供用户功能后，整个过程就可以配置了。([@lukebp](https://matrix.to/#/!ueeciPqvqEsPyPCJkp:decred.org/$fDljYk8O9Wac_LFh9W-k7PRuPJdVk-bz4OTVfTw6sdY))

**[dcrpool](https://github.com/decred/dcrpool)**

- 支持[反向代理](https://github.com/decred/dcrpool/pull/301)部署
- [Stratum](https://github.com/decred/dcrpool/pull/304)挖矿协议的各种改进
- 固定的哈希计算跨越多个[周期](https://github.com/decred/dcrpool/pull/305)

**[dcrlnd](https://github.com/decred/dcrlnd)**

- 检查[解锁时](https://github.com/decred/dcrlnd/pull/106)是否使用了正确的钱包帐户（这可以在Decrediton中显示有意义的消息）
- 
**[cspp](https://github.com/decred/cspp)**

- 验证客户是否支付了足够的交易[费用](https://github.com/decred/cspp/pull/58)（并关闭了DoS向量）
- 删除[超时](https://github.com/decred/cspp/pull/60)的客户端
- 隔离不同[运行](https://github.com/decred/cspp/pull/61)的状态，以防止可能出现的混币中止

**[dcrdex](https://github.com/decred/dcrdex)**

v0.1.5修复一下问题：

- 处理因某种原因[丢失](https://github.com/decred/dcrdex/pull/967)了资金的订单
- 使客户端初始化和兑换请求[异步](https://github.com/decred/dcrdex/pull/911)以阻止可能并行发生的操作
- 在[恢复](https://github.com/decred/dcrdex/pull/965)启动和登录时的交易时重试合同审核，以防止匹配被错误地吊销
- blake2依赖关系[已更新](https://github.com/decred/dcrdex/pull/982)，以防止静默内存损坏

在[此处](https://github.com/decred/decred-binaries/releases/tag/v1.6.1#dcrdex-v015)获取发行说明和下载，或跟踪[dcrinstall](https://github.com/decred/decred-release/releases)并运行`dcrinstall --dcrdex`以自动下载，验证和配置程序。无论如何，请[验证](https://docs.decred.org/advanced/verifying-binaries/)下载的文件以确保它们没有被修改。

合并到v0.2版本的主版本中：

- 估算[估算](https://github.com/decred/dcrdex/pull/958)和赎回交易期间的最低，最高和最大费用，以提供更多的费用明晰度，而不是仅仅显示最坏的情况
- 在升级数据库[之前](https://github.com/decred/dcrdex/pull/949)写一个备份文件
- 将客户端从btcsuite的客户端切换到Decred的[rpcclient](https://github.com/decred/dcrdex/pull/938)客户端，因为后者[支持](https://github.com/decred/dcrdex/issues/841)取消请求
- 在[关机](https://github.com/decred/dcrdex/pull/928)期间将钱包锁定代码移到更好的位置

您可以针对[0.2](https://github.com/decred/dcrdex/milestone/6)（服务器市场数据，UI +后端改进）和[0.3](https://github.com/decred/dcrdex/milestone/12)（SPV支持，BCH对，Decred 1.7）跟踪里程碑页面上的内容。

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

- 更新[法语](https://github.com/planetdecred/dcrandroid/pull/535)翻译
- 代码库[清理](https://github.com/planetdecred/dcrandroid/pull/533)
- 用户界面调整

[dcrlibwallet](https://github.com/planetdecred/dcrlibwallet)基础库已更新，以在必要时[重新启动](https://github.com/planetdecred/dcrlibwallet/pull/156)同步并支持外部记录器（以便更轻松地嵌入其他软件）。

**[dcrios](https://github.com/planetdecred/dcrios)**

- 允许用户从初始屏幕创建[仅观查](https://github.com/planetdecred/dcrios/pull/734)的钱包（无需先创建新的常规钱包）
- 添加了调试页面以查看连接的[对等节点](https://github.com/planetdecred/dcrios/pull/730)的详细信息
- 用户界面和翻译调整

**[godcr](https://github.com/planetdecred/godcr)**

- 添加了用于验证消息和验证地址工具的[安全工具](https://github.com/planetdecred/godcr/pull/299)UI和[逻辑](https://github.com/planetdecred/godcr/pull/315)
- [设置](https://github.com/planetdecred/godcr/pull/307)页面的已实现逻辑
- 已实施[vspd](https://github.com/planetdecred/godcr/pull/263)的购票支持
- 实施了StakeShuffle帐户[混合](https://github.com/planetdecred/godcr/pull/312)
- 实施了仅[观察钱包](https://github.com/planetdecred/godcr/pull/318)导入

**[dcrros](https://github.com/decred/dcrros)**

- [已更新](https://github.com/decred/dcrros/pull/19)，以符合Rosetta规范版本1.4.10
- 添加了完整的端到端[测试套件](https://github.com/decred/dcrros/pull/18)以判断正确的dcrros行为，包括在本地simnet上运行所需的Data and Construction API测试，该测试可解决链上发现的许多情况

**[docs](https://github.com/decred/dcrdocs)**

- 命令行“[购票](https://docs.decred.org/wallets/cli/dcrwallet-tickets/)”页面[已更新](https://github.com/decred/dcrdocs/pull/1148)为v1.6的步骤

**Kohola**

@peter\_zen [分享了](https://matrix.to/#/!aNnAOHkWUdNcEXRGjJ:decred.org/$uc4-7jDq7LehB55bK3sAjq9qL-g2WDJ8wOW5HZTvknI):

> 宣布我和@bgptr去年一直在从事的项目: [kohola](https://github.com/peterzen/kohola)
> 
> Kohola是我为满足自己的需求而开发的dcrwallet前端，Decrediton并未涵盖这些需求。它的功能尚未完成，但我一直在将其用作常用钱包。几个月前，由于其它优先事项，它的研究工作停滞了，但我依然会分享它的当前状态，因为其它用户可能会发现它有用。万一证明它有用，那么完成它会很棒。

从[自述文件](https://github.com/peterzen/kohola)来看，此钱包专用于专业用户，并提供诸如加密配置，独立抵押支持，硬币控制等功能。该应用程序是使用React和Redux框架以Go和TypeScript编写的。值得注意的是，Kohola在夏威夷语中的意思是“鲸鱼”。

其它:

- u / interfux发布了Debian / Ubuntu [软件包](https://www.reddit.com/r/decred/comments/lr8kut/debianubuntu_packages_for_decred_software/)和一个非官方的APT存储库，可轻松安装和更新Decred命令行程序。欢迎反馈，特别是经验丰富的包装人员的反馈意见，以推动其进一步发展并最终在Debian / Ubuntu官方repos中发布。
- @dezryth共享了一个Python[程序](https://github.com/dezryth/VotedTicketNotifier)，当您的票被挑中时，该程序会向您的移动设备发送推送通知
- 现在大多数项目正在使用Go 1.16进行构建和测试

## 人员

欢迎新到来的首次贡献者，他们的代码已合并到主代码库中： @bochinchero ([dcrlnd](https://github.com/decred/dcrlnd/commits?author=bochinchero)) 和 @fintechtrades ([dcrdocs](https://github.com/decred/dcrdocs/pull/1150))!

@arij在Decred in Depth播客中接受了采访，请参阅[媒体部分](#媒体)。

截至3月1日的社区统计数据：

- [Twitter](https://twitter.com/decredproject) 粉丝: 42,922 (+1,121)
- [Reddit](https://www.reddit.com/r/decred/) 订阅: 10,559 (+358)
- [Matrix](https://chat.decred.org/) #general 用户: 382 (+38)
- [Discord](https://discord.gg/GJ2GXfz) 用户: 1,444 (-473) - 观看次数
- [Telegram](https://t.me/Decred) 用户: 2,518 (+90)
- [YouTube](https://www.youtube.com/decredchannel) 订阅: 4,420 (+100), views: 175K (+6K)
- [LinkedIn](https://www.linkedin.com/company/decredproject) 粉丝: 978 (+16)
- GitHub [dcrd](https://github.com/decred/dcrd) 星: 584 (+9), 叉: 252 (+3)

检测到跟踪帐户的显着[变化](https://github.com/decredcommunity/social-media-stats)：

- 上面列出的Twitter，Reddit和YouTube的关注度和观看次数均比往常更多
- [CoinMarketCap](https://coinmarketcap.com/currencies/decred/) 页面又增加了3K观查者至29K
- 1月出现了[DecredKorea](https://twitter.com/DecredKorea) 和 [DecredNederland](https://twitter.com/DecredNederland) 账户，并开始用韩语和荷兰语发布推文
- [DecredDEX](https://twitter.com/DecredDEX)已加入[decredexplorer](https://twitter.com/decredexplorer)，现在我们有两个以产品为中心的Twitter帐户
- [@Checkmate](https://twitter.com/_Checkmatey_) 吸引了30％的关注者（达到5K），并以每天约41个疯狂的速度发布了1.2K条推文
- [ConsensusRough](https://twitter.com/ConsensusRough)获得了18％的关注者，到438

## 治理

二月[国库](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到10444 DCR，花费3010 DCR。按照1月份的每日平均DCR/USD汇率113.76美元计算，这是1200万美元的收入和34.2万美元的支出。按2月平均汇率54.25美元计算，当月完成工程的美元账单金额为16.3万美元。截至3月3日，社区开发基金余额为653,000 DCR（9,720万美元，148.86美元）。

在2月初创下两个提案的破纪录投票率（在上一期中发现）之后，本月的剩余时间相对平静，另外两个提案被批准。

- Decred Journal 2021[提案](https://proposals.decred.org/proposals/1d74b88)以92.4％的赞成票和51％的投票率获得批准。该年度申请的最高资助金额为39,000美元，其中还包括《 Politeia Digest》和所有相关的设计工作。感谢所有投票支持《华尔街日报》首项个人提案的利益相关者！不要犹豫，分享您对[Reddit](https://www.reddit.com/r/decred/search?q=decred+journal&restrict_sr=on&t=all&sort=new), [GitHub](https://github.com/xaur/decred-news/issues) 或 [Matrix](https://chat.decred.org/#/room/#writers:decred.org)的想法，尤其是如果您[投票否](https://explorer.dcrdata.org/proposal/decred-journal-2021)（我们可以在批评中幸存）。

- @ richard-red提出的“开放源研究2021”[提案](https://proposals.decred.org/proposals/020b8b0)获得了75.4％的赞成票和60％的投票赞成。请求的预算已增加到40,000美元，其中9,150美元留给了@bee的开放数据收集计划。

@ammarooni发表了对他的书的计划[反思](https://twitter.com/Ammarooni/status/1359352089714061313)，并正在寻求一些诚实的反馈。

## 网络

**全网算力**: 2月份的[哈希率](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kkf13di6-kltwy2po&scale=linear&bin=block&axis=time)以〜428 Ph/s的速度打开，以〜420 Ph/s的速度关闭，在278 Ph/s的谷底，并在整个月达到537 Ph/s的峰值。

截至3月1日的池哈希率[分布](https://miningpoolstats.stream/decred)：Poolin 36％，Antpool 34％，F2Pool 8％，Luxor 2％，BTC.com 1.5％，Huobipool 0.8％，Coinmine 0.08％，UUPool 0.03％，未知18％。

即时快照非常不稳定，因此，与3月1日之前分配的1,000个区块（3.5天）相比，分布情况是：Antpool 41％，Poolin 29％，easy2mine 11％，F2Pool 6％，Luxor 1.5％，Huobipool 0.4％，未知11％。

UUPool的报告哈希率已从最高点下降到了最低点，看起来其矿工已经迁移到Antpool和F2Pool。新的身份不明的地址也出现了。

**Staking**: [票价](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kkf13di6-kltwy2po&axis=time&visibility=true-true&mode=stepped)154.3-220.4 DCR之间变化，具有30天的[平均](https://dcrstats.com/)在181.7 DCR（8.5）。该锁定量为6.74-7.30亿DCR，这意味着循环供应的53.6-57.7％参加在验证的股权。

看来我们每个月的选票价格和参与度都[打破](https://twitter.com/michae2xl/status/1359609723541213186)了纪录！

**节点**: 根据[dcrextdata](https://dcrextdata.planetdecred.org/nodes)，在整个2月份，大约有220个可访问节点。dcr.farm的平均版本分布：35％dcrd v1.6.0、10％dcrd v1.6.1、10％dcrd v1.5.2、7％dcrd v1.5.1、5％dcrd v1.6 dev和RC内部版本，4％dcrd v1.7开发人员版本，2％dcrd v1.5.0、1.5％dcrd v1.5开发人员和RC版本，9％dcrwallet v1.6.0、4％dcrwallet v1.6.1、3％dcrwallet v1.5.1，约9％。

由于需求低，运营成本高，[charts.dcr.farm](https://charts.dcr.farm/)已被关闭，以使其可持续地运行。我们感谢运营商多年来分享的所有网络见解。dcr.farm的旧版和新[VSP](https://dcr.farm/)仍在运行。

仅在2月份，[混合硬币](https://explorer.dcrdata.org/charts?chart=coin-supply&zoom=jzk7rn6n-kmfblq6m&bin=day&axis=time&visibility=true-true-true)的份额就从31％增长到38％，这可能要归功于v1.6中添加了GUI。[@CoinShuffle_BOT](https://twitter.com/CoinShuffle_BOT)每天发布混合统计信息。

截至3月1日，Decred的[闪电网络](https://ln-map.jholdstock.uk/)已经拥有30个节点（+2），56个通道（+9），总容量为16.8 DCR（+8.5）。

@matheusd分享了一些票务拆分[统计数据](https://www.reddit.com/r/decred/comments/lj2her/og_ticket/gnj3zqq/)：在近3年的时间里，平均以81 /月的速度购买了2679张票证，这意味着大约有0.2％的票证被拆分了。在v1.6和不支持票证拆分的新vspd放样中对此进行了讨论。要使其与vspd一起使用，需要新的拆分/匹配协议以及服务器和客户端的重写，鉴于需求低，目前不太可能发生这种情况。

## 整合

三个VSP启用了对新vspd的支持：[decredvoting.com](https://decredvoting.com/), [ibitlin.com](https://dcrpool.ibitlin.com/), 和 [coinmine.pl](https://vsp.coinmine.pl)。现在，我们总共有11个vspd实例和17个旧版VSP实例。

该[VSP上市](https://decred.org/vsp/)了更新，以显示沿着传统的人VSPD门票。截至3月1日，vspd服务器持有4.4K实时票证，占目标票证池的11％。旧版VSP服务器持有6.5K实时票证，占目标的16％。

[SwapSwop.io](https://swapswop.io/)交换平台来打招呼的R / decred并回答了关于流动性来源，管辖，他们的KYC过程的一些问题。DCR于2020年9月上市。

一个新的[#services](https://chat.decred.org/#/room/#services:decred.org)公共聊天室欢迎每个人收集有关不断增长的Decred生态系统的信息（交易所，付款处理方，VSP等）。

警告：Decred Journal的作者不了解上述任何服务的可信赖性。在将您的个人信息或资产信任给任何实体之前，请先进行自己的研究。

## 活动

几个Decred的贡献者在Decred AMA中回答了有关[r/CryptoCurrency](https://www.reddit.com/r/CryptoCurrency/comments/lqlone/decred_ama_ask_us_about_privacy_daos_lightning/)的各种问题。该话题获得171条评论和140票赞成。

@elima_iii已开始“Decred in Depth”系列的第二季，吸引了新来宾和更多的社区参与。到宾客的问题在[Twitter](https://twitter.com/elima_iii/status/1363280047059132417)上收集（[@matheusd](https://twitter.com/elima_iii/status/1365424755906670595)情节甚至更多），可以观看主持人和宾客的视频，而YouTube现在是主要地点。

@pavel分享了withDecred提案的[更新](https://github.com/decredcommunity/proposals/blob/master/proposals/2bf72e/updates/20210208.md)：

> 由于过去几周的大规模价格行动，我暂停了赠品活动，因为似乎不再需要引起社会关注。在活动时，[@withDecred](https://twitter.com/withdecred) Twitter帐户每月有大约10万次展示，并引发了一些良好的对话（也有一些先令）。（...）我现在正在考虑如何使用WithDecred活动（Web + Twitter）从这里开始，目前我正在支持社区创建的内容。如果您有任何建议，请随时在[这里](https://chat.decred.org/#/room/#proposals:decred.org)或在[Twitter](https://twitter.com/paveldcr)上ping我。

Monde PR在二月份的成就：

- 创建/整理了3个故事，以资助和加密出版物
- 回应了3条评论请求
- 获得2次媒体采访

## 活动

参加:

- 2月3日 - [Decred 5 Years Giveaway](https://decredcommunity.github.io/events/index/20210203.1) - 互联网。Decred的西班牙团队组织了一场精致的赠品，以纪念Decred成立5周年。DCR总共获得了130美元的DCR奖励，用于诸如转推，回答问题（在挖掘了一些dcrdata之后），回答“您喜欢Decred怎么样？”或争夺模因一代等各种任务。这项活动吸引了60多人，在Twitter上产生了超过57,000的印象，并吸引了100多个Twitter关注者和40多个[Telegram](https://t.me/DecredES)用户。[报告](https://decredcommunity.github.io/events/index/20210203.1)中的详细信息。
- 2月6日 - [Blockchain, AI, and Big Data](https://decredcommunity.github.io/events/index/20210206.1) - 摩洛哥卡萨布兰卡。@arij和OMJD组织了一个活动来纪念Decred成立5周年。关于机器学习，大数据和区块链的3个讲座。在后者中，@ arij讨论了如何在巴西市政选举中使用Decred区块链。预计会有20个人，但有40个人出现，约有500人观看了现场直播。最后，举行了一个小型的周年庆典（涉及...举行）。
- 2月9日 - [Decred intro and features](https://decredcommunity.github.io/events/index/20210209.1) - 互联网。@ michae2xl受Monnos（一月份在DCR上市的巴西交易所）的邀请，在Instagram直播中介绍Decred。他们与Rodrigo Soeiro（首席执行官）一起向该领域的新人们致辞，展示了Decred的产品，并讨论了他们的潜力。
- 2月20日 - [Alternative Consensus: Let’s Talk PoS](https://decredcommunity.github.io/events/index/20210220.1) - 互联网。@elian曾与Decred万物[Criptodemia](https://twitter.com/criptodemia)和[Kevin Negocios](https://twitter.com/KevinNegocios)从Veinte交易所委内瑞拉在1+小时的视频直播。

![Decred Cake 3](../img/202102.3.github.jpg)

即将来临：

- 3月12日至14日 - [Hackathon Nayarit 2021](https://www.facebook.com/EduNayarit/posts/2982126628674008) - 互联网。以西班牙语表示的将赞助由纳亚里特教育部组织的黑客马拉松。为了准备参与者，西班牙团队举办了由5个网络研讨会组成的“区块链教育”培训周

## 媒体

所选文章：

- 与联合创始人兼项目负责人Jake Yocom-Piatt([coinscrum.com](https://www.coinscrum.com/decred-with-jake-yocom-piatt/))一起发布了Decred v1.6-1月的视频改编成一篇文章，将新的库务代码与“最小复杂的有线智能联系人”进行了比较，并解释了v1的主要功能。
- Xangle在1月的研究[报告](https://xangle.io/research/600a3251b7cb8c849dfa26b9)中将DCRDEX列为2021年值得关注的顶级DEX之一

影片：

- Decred新闻更新-2月14日-Massive 1.6版本发布，投票获得7500万美元的DAO，LN，隐私和更多内容！由@Exitus([youtube](https://www.youtube.com/watch?v=f2ooNJXpR7I))
- Decred隐私教程：通过@Exitus([youtube](https://www.youtube.com/watch?v=QC65PBNwAK4))混合硬币
- Insaf Nori采访@elima_iii([youtube](https://www.youtube.com/watch?v=hUXk1GWhE-0))深入探讨（实时）
- 成为社会分散组织([youtube](https://www.youtube.com/watch?v=Vb-9vvU0fDU))的自己的银行
- Decred的价格分析-2021年2月24日，作者Brave New Coin([youtube](https://www.youtube.com/watch?v=O6iTIABl2Lw))

音频:

- Rough Consensus 17: 失散已久的联合主持人@ mr.black重新加入了Pod，谈论加密和金融。 ([libsyn](https://roughconsensus.libsyn.com/episode-17-spidey-reunion))

艺术与乐趣：

- @karamble的Decred v1.6数字公告[剪辑](https://twitter.com/karamblez/status/1356921573647745024) （尝试发现“ taco”！）
- @richardred关于[原子交换](https://twitter.com/RichardRed0x/status/1356719226724220930)如何工作的最终解释

![Decred doughnuts](../img/202102.2.github.jpg)

翻译：

- Decred新闻更新1月24日- @francov_提供[西班牙](https://www.youtube.com/watch?v=Quf8u1Ksm4M)语字幕
- 使用Decred区块链构建透明的未来- @arij和@ abdulrahman4用[阿拉伯语](https://insaf01.github.io/decred-arabic/articles/building-a-transparent-future-with-decred-blockchain.html)撰写
- Decred Journal 2021年1月被[翻译](https://xaur.github.io/decred-news/)成阿拉伯文（@arij，@ abdulrahman4），中文（@Dominic）和西班牙文（@francov_）。谢谢大家传播Decred新闻！

## 社区讨论

最近有更多尝试骗人。请记住，真正的开发人员和管理员绝对不会向您提供免费资金或技术帮助。密切注意与您聊天的用户显示名称和用户ID，以避免冒充用户的聪明方法。告诉您的朋友也要保持警惕。

精选的Reddit帖子：

- 将选票重命名为["OG选票"](https://www.reddit.com/r/decred/comments/lj2her/og_ticket/)并将其1/10部分称为常规“票证”的想法
- 在一个[价格的讨论](https://www.reddit.com/r/decred/comments/llnzvu/dcr_breaking_through_all_time_high_price_usd/)变得异常智能摸招聘的主题（我们一直在说的：不仅开发商都希望）
- DCRDEX vs [Bisq](https://www.reddit.com/r/decred/comments/ln7co5/dcrdex_vs_bisq/)
- 有关[种子词](https://www.reddit.com/r/decred/comments/lo72lf/discussion_around_33_word_seed_vs_bip_39/)和金属钱包的一些有趣事实

精选的Twitter讨论：

- @ jy-p提醒我们[为什么](https://twitter.com/behindtext/status/1363118198749597698)仍在这里
- 另一个伟大的[线程](https://twitter.com/cburniske/status/1362146220123201536)从@cburniske

> 作为自2016年以来一直关注@decredproject的人，其社区的实力，基本面以及迄今为止在2021年的市场吸引力都令我感到惊讶。 ([@cburniske](https://twitter.com/cburniske/status/1362146231116460032))

## 市场

2月DCR交易价格在66.95-169.90美元/ BTC 0.0018-0.0030之间。每日平均费用为113.76美元。

@Checkmate发布了一个大型链上线程，其中许多（全部？）指示器都进入了ATH状态。2月9日的预测：“如果火车从这里减速下来，我会很惊讶，这根本不符合要求！” 是正确的。

在币安上观察到异常高的出价。

[DCRDEX](https://dex.decred.org/)在二月份交易了390K DCR和1K BTC，平均每天交易为14K DCR和36 BTC。价格在0.0019-0.0030之间变化，平均为0.0026。

## 相关外部信息

Yearn Finance是2月份最大的DeFi Fail案例，它的用户遭受了一笔1,100万美元的小额贷款攻击。在这种攻击的一个有趣的发展，大部分的开发资金中支付了费用，以各种流动性游泳池和跑马圈地的服务，只有270万$的攻击者的钱包结束了，剩下的可能助长了DEFI经济。攻击的受害者已从最近建立的新的YFI国库资金中获得了补偿-在遭受攻击的4天之内，Yearn团队就能够动员970万DAI进行分发，并且不需要进行代币投票。YFI和财政部目前在Multisig持有人的直接控制下，并且“授权”正在扩展 直到5月24日。

Yearn Finance还正在显着改变其库务和治理融资模式，主要变化包括由于其不具竞争力的收益率而取消YFI股权，而转而采用回购模式，并允许将其代币部署在流动性池中的YFI持有人也可以将其用于投票。

比特币的开发者在过程中决定如何主根升级应该被激活，随着竞争的存在点的比特币核心更新是否应该有它在信令期末激活无论绝对多数阈值是否设置出货遇到问题（例如用户激活的软叉），或者采取更为谨慎的方法，并避免在一开始就强制执行此问题。根据矿池的哈希率，截至3月2日的一个月的矿工信号显示对矿池对Taproot的支持率为89％。此外，Poolin做出了共识性努力，汇集了池的情绪和首选的激活方法。

纽约总检察长就Tether和Bitfinex的指控达成和解，该公司支付了1850万美元的罚款，但避免承认任何不当行为。

尼日利亚中央银行已采取行动提醒银行“禁止交易加密货币或便利支付加密货币交易所的费用”，并指示其关闭所有从事加密货币交易的人和实体的帐户。

美国联邦储备委员会经历了一个问题，与几个小时障服务的跨行转账系统。在美国财政部长珍妮特·耶伦（Janet Yellen）警告比特币“效率极低”并对投资者构成风险之后不久，这种情况就发生了。

@notsofast敦促每个人从错误中吸取教训，这些错误已导致在安全漏洞中损失约100,000美元的加密货币：获得一个好的密码管理器，使用硬件钱包，在单独的浏览器配置文件或设备中隔离诸如Metamask之类的危险浏览器扩展。

## 关于月报

这是Decred Journal的第35期。有关所有问题，镜像和翻译的索引，请参见[这里](https://xaur.github.io/decred-news/)。

在经过最少的健全性检查之后，来自第三方的大多数信息都会直接从来源中继。Decred Journal的作者无权验证所有声明。请当心诈骗，并自行进行调查。

您可以在[此处](https://github.com/xaur/decred-news/labels/next%20release)提交内容，以供撰写下一期月报内容。我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢 (字母排列):

- 写作和编辑: bee, degeri, l1ndseymm, richardred
- 评论和反馈: davecgh, jholdstock, peter\_zen
- 封面图片: saender
- 资助: Decred stakeholders

## 中文社区

* [社区网址](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [bilibili频道](https://space.bilibili.com/425519478)
* QQ群号-258412796
