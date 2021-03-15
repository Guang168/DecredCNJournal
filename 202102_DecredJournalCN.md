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

- [v1.6.1补丁发布](#v1.6.1补丁发布)
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
- implemented [vspd](https://github.com/planetdecred/godcr/pull/263) staking support
- implemented StakeShuffle account [mixing](https://github.com/planetdecred/godcr/pull/312)
- implemented [watch-only](https://github.com/planetdecred/godcr/pull/318) wallet import

**[dcrros](https://github.com/decred/dcrros)**

- [updated](https://github.com/decred/dcrros/pull/19) to comply with the Rosetta spec version 1.4.10
- added a full end-to-end [test suite](https://github.com/decred/dcrros/pull/18) to assert correct dcrros behavior, including running the required Data and Construction API tests on a local simnet that exercises a large number of situations actually found on chain

**[docs](https://github.com/decred/dcrdocs)**

- command-line [Buying Tickets](https://docs.decred.org/wallets/cli/dcrwallet-tickets/) page [updated](https://github.com/decred/dcrdocs/pull/1148) with steps for v1.6

**Kohola**

@peter\_zen [shared](https://matrix.to/#/!aNnAOHkWUdNcEXRGjJ:decred.org/$uc4-7jDq7LehB55bK3sAjq9qL-g2WDJ8wOW5HZTvknI):

> Announcing a project I and @bgptr have been working on last year: [kohola](https://github.com/peterzen/kohola)
> 
> Kohola is a dcrwallet frontend I started for my own needs which weren't covered by Decrediton. It's not feature complete yet but I've been using it as my production wallet. Work on it stalled some months ago due to other priorities but I thought I'd share it in its present state as other peeps may find it useful. In case it proves some usefulness it would be great to finish it.

From the [readme](https://github.com/peterzen/kohola), this wallet is intended for expert users and offers features like encrypted configuration, solo staking support, coin control, and more. The app is written in Go and TypeScript using React and Redux frameworks. Notably, Kohola means "whale" in Hawaiian.

Other:

- u/interfux announced Debian/Ubuntu [packages](https://www.reddit.com/r/decred/comments/lr8kut/debianubuntu_packages_for_decred_software/) and an unofficial APT repo for easy installation and updating of Decred command-line programs. Feedback is welcome, especially from experienced packagers to push it further and ultimately publish in official Debian/Ubuntu repos.
- @dezryth shared a Python [program](https://github.com/dezryth/VotedTicketNotifier) that will send push notifications to your mobile device when your tickets vote
- most projects are now building and testing with Go 1.16

## People

Welcome to new first time contributors with code merged to master: @bochinchero ([dcrlnd](https://github.com/decred/dcrlnd/commits?author=bochinchero)) and @fintechtrades ([dcrdocs](https://github.com/decred/dcrdocs/pull/1150))!

@arij was interviewed on the Decred in Depth podcast, see [Media](#media).

Community stats as of Mar 1:

- [Twitter](https://twitter.com/decredproject) followers: 42,922 (+1,121)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 10,559 (+358)
- [Matrix](https://chat.decred.org/) #general users: 382 (+38)
- [Discord](https://discord.gg/GJ2GXfz) users: 1,444 (-473) - pruned inactive users
- [Telegram](https://t.me/Decred) users: 2,518 (+90)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,420 (+100), views: 175K (+6K)
- [LinkedIn](https://www.linkedin.com/company/decredproject) followers: 978 (+16)
- GitHub [dcrd](https://github.com/decred/dcrd) stars: 584 (+9), forks: 252 (+3)

Notable changes detected for the [tracked](https://github.com/decredcommunity/social-media-stats) accounts:

- Twitter, Reddit, and YouTube listed above all got a higher than usual increase in following and views
- [CoinMarketCap](https://coinmarketcap.com/currencies/decred/) page got another +3K watchers to 29K
- [DecredKorea](https://twitter.com/DecredKorea) and [DecredNederland](https://twitter.com/DecredNederland) Twitter accounts have emerged in Jan and started tweeting in Korean and Dutch
- [DecredDEX](https://twitter.com/DecredDEX) has joined [decredexplorer](https://twitter.com/decredexplorer) and now we have two product-focused Twitter accounts
- [@Checkmate](https://twitter.com/_Checkmatey_) gained +30% followers (to 5K) and posted 1.2K tweets at a crazy rate of ~41/day
- [ConsensusRough](https://twitter.com/ConsensusRough) got +18% followers, to 438

## Governance

In February the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 10,444 DCR and spent 3,010 DCR (actually payments didn't go out until Mar 2). Using February's daily average DCR/USD rate of $113.76, this is $1.2M received and $342K spent. At January's average daily rate of $54.25, the USD figure billed for past work is $163K. As of Mar 3, the Treasury balance is 653,000 DCR (97.2 million USD at $148.86).

After the record-breaking turnout for two proposals at the start of Feb (covered in the [last issue](202101.md#governance)), the rest of the month was relatively quiet, with two further proposals being approved.

- The Decred Journal 2021 [proposal](https://proposals.decred.org/proposals/1d74b88) was approved with 92.4% Yes votes and turnout of 51%. The max amount of funding requested for the year is $39,000, and it also covers Politeia Digest and all of the associated design work. Thanks to all the stakeholders who voted for the Journal's first solo proposal! Don't hesitate to share your thoughts on [Reddit](https://www.reddit.com/r/decred/search?q=decred+journal&restrict_sr=on&t=all&sort=new), [GitHub](https://github.com/xaur/decred-news/issues) or [Matrix](https://chat.decred.org/#/room/#writers:decred.org), especially if you [voted No](https://explorer.dcrdata.org/proposal/decred-journal-2021) (we can survive the criticism).

- The Open Source Research 2021 [proposal](https://proposals.decred.org/proposals/020b8b0) from @richard-red was approved with 75.4% Yes votes and turnout of 60%. The requested budget has increased to $40,000, and $9,150 of this is set aside for the expansion of @bee's open data collection initiative. 

@ammarooni posted a [reflection](https://twitter.com/Ammarooni/status/1359352089714061313) on his book [proposal](https://proposals.decred.org/proposals/9e1d644) and is looking for some honest feedback.

## Network

**Hashrate**: February's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kkf13di6-kltwy2po&scale=linear&bin=block&axis=time) opened at ~428 Ph/s and closed ~420 Ph/s, bottoming at 278 Ph/s and peaking at 537 Ph/s throughout the month.

Pool hashrate [distribution](https://miningpoolstats.stream/decred) as of Mar 1: Poolin 36%, Antpool 34%, F2Pool 8%, Luxor 2%, BTC.com 1.5%, Huobipool 0.8%, Coinmine 0.08%, UUPool 0.03%, unknown 18%.

Instant snapshots are too volatile, so compare that to how 1,000 blocks (3.5 days) mined before Mar 1 have been distributed: Antpool 41%, Poolin 29%, easy2mine 11%, F2Pool 6%, Luxor 1.5%, Huobipool 0.4%, unknown 11%.

UUPool's reported hashrate has dropped from the top spot to the bottom and it looks like its miners have migrated to Antpool and F2Pool. New unidentified addresses are also showing up.

**Staking**: [Ticket price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kkf13di6-kltwy2po&axis=time&visibility=true-true&mode=stepped) varied between 154.3-220.4 DCR, with 30-day [average](https://dcrstats.com/) at 181.7 DCR (+8.5). The [locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kkf13di6-kltwy2po&scale=linear&bin=block&axis=time) was 6.74-7.30 million DCR, meaning that 53.6-57.7% of the circulating supply [participated](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kkf13di6-kltwy2po&scale=linear&bin=block&axis=time) in proof-of-stake.

It looks like we are [breaking](https://twitter.com/michae2xl/status/1359609723541213186) a record every month in terms of both ticket price and participation!

**Nodes**: Throughout February there were around 220 reachable nodes according to [dcrextdata](https://dcrextdata.planetdecred.org/nodes). Average version distribution from dcr.farm: 35% dcrd v1.6.0, 10% dcrd v1.6.1, 10% dcrd v1.5.2, 7% dcrd v1.5.1, 5% dcrd v1.6 dev and RC builds, 4% dcrd v1.7 dev builds, 2% dcrd v1.5.0, 1.5% dcrd v1.5 dev and RC builds, 9% dcrwallet v1.6.0, 4% dcrwallet v1.6.1, 3% dcrwallet v1.5.1, ~9% others.

[charts.dcr.farm](https://charts.dcr.farm/) has been shut down due to low demand and high operating costs to keep it running in a sustainable way. We thank the operators for all the network insights shared over the years. dcr.farm's legacy and new [VSP](https://dcr.farm/) are still operational.

The share of [mixed coins](https://explorer.dcrdata.org/charts?chart=coin-supply&zoom=jzk7rn6n-kmfblq6m&bin=day&axis=time&visibility=true-true-true) has grown from 31% to 38% in Feb alone, possibly thanks to the GUI for it added in v1.6. [@CoinShuffle_BOT](https://twitter.com/CoinShuffle_BOT) posts mixing stats daily.

Decred's [Lightning Network](https://ln-map.jholdstock.uk/) has seen 30 nodes (+2), 56 channels (+9) with a total capacity of 16.8 DCR (+8.5), as of Mar 1.

@matheusd shared some ticket splitting [stats](https://www.reddit.com/r/decred/comments/lj2her/og_ticket/gnj3zqq/): over almost 3 years 2,679 split tickets were purchased at an average rate of 81/month, meaning that roughly 0.2% of tickets are being split. This was discussed in the context of v1.6 and the new vspd staking where ticket splitting is not supported. A new splitting/matching protocol and a rewrite of both server and client are required to make it work with vspd, which is unlikely to happen at this time given the low demand.

## Integrations

Three VSPs have enabled support for the new vspd staking: [decredvoting.com](https://decredvoting.com/), [ibitlin.com](https://dcrpool.ibitlin.com/), and [coinmine.pl](https://vsp.coinmine.pl). We now have a total of 11 vspd instances and 17 legacy VSP instances.

The [VSP listing](https://decred.org/vsp/) was updated to show vspd tickets along the legacy ones. As of Mar 1, vspd servers held 4.4K live tickets, or 11% of the target ticket pool. Legacy VSP servers held 6.5K live tickets, or 16% of the target.

[SwapSwop.io](https://swapswop.io/) exchange platform came to [say hi](https://www.reddit.com/r/decred/comments/lfgr64/buy_dcr_at_swapswopio_a_crypto_exchange_platform/) on r/decred and answered a few questions about liquidity sources, jurisdiction, and their KYC processes. DCR was [listed](https://twitter.com/swapswopio/status/1308107303032369152) in Sep 2020.

A new [#services](https://chat.decred.org/#/room/#services:decred.org) public chat room welcomes everyone to collect information about the growing Decred ecosystem (exchanges, payment processors, VSPs - anything).

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Several Decred contributors answered all kinds of questions in Decred AMA on [r/CryptoCurrency](https://www.reddit.com/r/CryptoCurrency/comments/lqlone/decred_ama_ask_us_about_privacy_daos_lightning/). The thread got 171 comment and 140 upvotes.

@elima\_iii has started the second season of the Decred in Depth series, featuring new guests and more community engagement. Questions to guests are collected [on Twitter](https://twitter.com/elima_iii/status/1363280047059132417) (even more for the [@matheusd](https://twitter.com/elima_iii/status/1365424755906670595) episode), video of both host and guest is available and YouTube is the primary location now.

@pavel shared an [update](https://github.com/decredcommunity/proposals/blob/master/proposals/2bf72e/updates/20210208.md) for the withDecred [proposal](https://proposals.decred.org/proposals/2bf72e6):

> Due to the massive price action in last weeks, I've suspended the giveaways as it seems no longer necessary to generate social buzz. At the time of activity, [@withDecred](https://twitter.com/withdecred) Twitter account had around 100K impressions monthly and generated some good conversations (and some shilling as well). (...) I'm now thinking how to go forward from here with WithDecred activities (web + Twitter), for the moment I'm supporting community-created content. If you have some suggestions, feel free to ping me [here](https://chat.decred.org/#/room/#proposals:decred.org) or on [Twitter](https://twitter.com/paveldcr).


Monde PR's achievements for February:

- created/pitched 3 stories to finance and crypto publications
- responded to 3 requests for comments
- secured 2 media interviews

## Events

Attended:

- Feb 3 - [Decred 5 Years Giveaway](https://decredcommunity.github.io/events/index/20210203.1) - Internet. Decred in Spanish team organized a sophisticated giveaway to mark Decred's 5th anniversary. A total of $130 in DCR was awarded for various tasks like retweets, answering questions (after digging some [dcrdata](https://explorer.dcrdata.org/)), answering "what do you like about Decred?", or competing in a meme generation. This activity engaged more than 60 people, generated over 57K Twitter impressions, and onboarded 100+ Twitter followers and 40+ [Telegram](https://t.me/DecredES) users. Details in the [report](https://decredcommunity.github.io/events/index/20210203.1).
- Feb 6 - [Blockchain, AI, and Big Data](https://decredcommunity.github.io/events/index/20210206.1) - Casablanca, Morocco. @arij and OMJD organized an event to mark Decred's 5th anniversary. There were 3 talks on machine learning, big data, and blockchains. In the latter, @arij talked about how Decred blockchain was used in Brazil municipal elections. 20 people were expected but 40 showed up, and ~500 watched it live. In the end, there was a small celebration of the anniversary _(involving... hold on)_.
- Feb 9 - [Decred intro and features](https://decredcommunity.github.io/events/index/20210209.1) - Internet. @michae2xl was invited by Monnos (Brazilian exchange that listed DCR in [January](202101.md#integrations)) to introduce Decred in an Instagram live. Together with Rodrigo Soeiro (CEO) they have addressed new people in the space, showed Decred's products, and discussed their potential.
- Feb 20 - [Alternative Consensus: Let’s Talk PoS](https://decredcommunity.github.io/events/index/20210220.1) - Internet. @elian talked all things Decred with [Criptodemia](https://twitter.com/criptodemia) and [Kevin Negocios](https://twitter.com/KevinNegocios) from [Veinte Exchange](https://twitter.com/Veinte_ven) of Venezuela in a 1+ hour livestream.

![Decred Cake 3](../img/202102.3.github.jpg)

Upcoming:

- Mar 12-14 - [Hackathon Nayarit 2021](https://www.facebook.com/EduNayarit/posts/2982126628674008) - Internet. Decred in Spanish will sponsor the hackathon organized by the Ministry of Education of Nayarit. To prepare participants, the Spanish team hosted Blockchain Education training week, consisting of 5 webinars.

## Media

Selected articles:

- Decred v1.6 with co-founder & project lead, Jake Yocom-Piatt ([coinscrum.com](https://www.coinscrum.com/decred-with-jake-yocom-piatt/)) - a Jan video reworked into an article, compares the new treasury code to "minimally complex hardwired smart contact" and explains key features of v1.6 in simple terms
- DCRDEX was listed among the top DEXes to watch in 2021 in the January research [report](https://xangle.io/research/600a3251b7cb8c849dfa26b9) by Xangle

Videos:

- Decred News Update - Feb 14th - Massive 1.6 release, vote for $75M DAO, LN, privacy, & more! by @Exitus ([youtube](https://www.youtube.com/watch?v=f2ooNJXpR7I))
- Decred Privacy Tutorial: Mix your coins by @Exitus ([youtube](https://www.youtube.com/watch?v=QC65PBNwAK4))
- Insaf Nori interview Decred in Depth (live) by @elima\_iii ([youtube](https://www.youtube.com/watch?v=hUXk1GWhE-0))
- Being your own bank by Society Decentralised ([youtube](https://www.youtube.com/watch?v=Vb-9vvU0fDU))
- Decred Price Analysis - 24th February 2021 by Brave New Coin ([youtube](https://www.youtube.com/watch?v=O6iTIABl2Lw))

Audio:

- Rough Consensus 17: Spidey reunion. The long lost co-host @mr.black rejoins the pod to talk about crypto and finance. ([libsyn](https://roughconsensus.libsyn.com/episode-17-spidey-reunion))
- past Decred in Depth episodes (up to 33rd) have been uploaded to the main YouTube [channel](https://www.youtube.com/decredchannel)

Art and fun:

- @karamble's Decred v1.6 digital announcement [clip](https://twitter.com/karamblez/status/1356921573647745024) _(try spotting "taco"!)_
- glitchy and loud 5th anniversary [clip](https://twitter.com/New_Copernicus/status/1357574854535487488) by @New\_Copernicus
- the ultimate explanation of how [atomic swaps](https://twitter.com/RichardRed0x/status/1356719226724220930) work by @richardred
- [The Rewards](https://www.reddit.com/r/decred/comments/lfxqef/the_rewards/) by @AGNFAB1
- "I wish to be [irrisistible](https://twitter.com/Decred_ES/status/1358855083396653062) to men!"
- introducing [Decred Pączki](https://twitter.com/LolekBolek74/status/1359866192538787843) (doughnuts)

![Decred doughnuts](../img/202102.2.github.jpg)

Translations:

- Decred News Update Jan 24 - with [Spanish](https://www.youtube.com/watch?v=Quf8u1Ksm4M) subtitles by @francov\_
- Building a transparent future with the Decred blockchain - [in Arabic](https://insaf01.github.io/decred-arabic/articles/building-a-transparent-future-with-decred-blockchain.html) by @arij and @abdulrahman4
- Decred Journal January 2021 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), and Spanish (@francov\_). Thank you all for spreading Decred news!

## Community Discussions

There have been more attempts to scam people recently. Please remember that real developers and admins will never DM you with offers of free money or technical assistance. Pay close attention to _user display name_ and _user ID_ you chat with to avoid smart ways to [impersonate](https://twitter.com/GrapheneOS/status/1365881076229488641). Tell your friends to stay vigilant, too.

Selected Reddit posts:

- an idea to rename tickets to ["OG tickets"](https://www.reddit.com/r/decred/comments/lj2her/og_ticket/) and call its 1/10th part a regular "ticket"
- one of the [price discussions](https://www.reddit.com/r/decred/comments/llnzvu/dcr_breaking_through_all_time_high_price_usd/) became unusually intelligent and touched the topic of recruiting (we keep saying it: not only developers are [wanted](https://www.reddit.com/r/decred/comments/llnzvu/dcr_breaking_through_all_time_high_price_usd/gnr3kpf/))
- DCRDEX vs [Bisq](https://www.reddit.com/r/decred/comments/ln7co5/dcrdex_vs_bisq/)
- a few interesting facts about [seed words](https://www.reddit.com/r/decred/comments/lo72lf/discussion_around_33_word_seed_vs_bip_39/) and metal wallets

Selected Twitter discussions:

- @jy-p reminds [why](https://twitter.com/behindtext/status/1363118198749597698) we are still here
- another great [thread](https://twitter.com/cburniske/status/1362146220123201536) from @cburniske

> As someone who's followed @decredproject since 2016, the strength of its community, fundamentals, and market traction thus far in 2021 has surprised even me. ([@cburniske](https://twitter.com/cburniske/status/1362146231116460032))

## Markets

In February DCR was trading between USD 66.95-169.90 / BTC 0.0018-0.0030. The average daily rate was $113.76.

@Checkmate posted a [mega](https://twitter.com/_Checkmatey_/status/1358968202898755584) on-chain thread with many (all?) indicators going ATH. Feb 9 prediction "I would be surprised if the train slows down from here, it's just not in character!" was correct.

Unusually large bids have been [observed](https://twitter.com/_Checkmatey_/status/1363709306885922826) on Binance.

[DCRDEX](https://dex.decred.org/) has traded 390K DCR and 1K BTC in February, averaging to 14K DCR and 36 BTC daily. The price varied between 0.0019-0.0030 with an average of 0.0026.

## Relevant External

Yearn Finance was February's largest DeFi [Fail](https://cryptobriefing.com/hacker-spends-8-3-million-fees-attack-yearn-finance/), with a flash loan attack exploiting its users for $11 million. In an interesting development for this kind of attack, most of the exploited funds were paid in [fees](https://twitter.com/FrankResearcher/status/1357639434380992512) to various liquidity pools and staking services, with just $2.7 million ending up in the attacker's wallet, and the rest presumably fuelling the DeFi economy. The victims of the attack have been [compensated](https://twitter.com/iearnfinance/status/1359108691677614080) from the new pool of YFI Treasury funds that were recently minted - within 4 days of the hack the Yearn team were able to mobilize 9.7 million DAI to distribute, and no token voting was required. YFI and the Treasury are currently under the direct control of the Multisig holders, and that "empowerment" is being [extended](https://gov.yearn.finance/t/yip-59-temporarily-extend-multisig-empowerment/9746) until May 24.

Yearn Finance is also [changing](https://gov.yearn.finance/t/yip-56-buyback-and-build/8929) up its Treasury and governance funding model [significantly](https://gov.yearn.finance/t/yip-56-buyback-and-build/8929), major changes include scrapping YFI staking because of its uncompetitive yield and instead switching to a buyback model and allowing YFI holders who have deployed their tokens in a liquidity pool to also use them to vote. 

Bitcoin developers are in the [process](https://twitter.com/AndreCronjeTech/status/1359934584612212738) of deciding how the [Taproot](https://bitcoinmagazine.com/technical/taproot-coming-what-it-and-how-it-will-benefit-bitcoin) upgrade should be activated, with the point of contention being whether the Bitcoin Core update should ship with a setting that has it activating at the end of the signalling period regardless of whether the supermajority threshold is met (like the User Activated Soft Fork) or take a more cautious approach and avoid forcing the issue initially. Miner signalling for the month to Mar 2 showed 89% support for Taproot from pools according to their hashrate. Additionally, Poolin contributed a consensus effort [compiling](https://taprootactivation.com/) pools' sentiment and preferred activation methods.

The New York Attorney General reached a [settlement](https://www.reuters.com/article/new-york-ifinex-settlement/bitfinex-tether-owner-pays-18-5-mln-fine-to-settle-nyag-cryptocurrency-cover-up-charges-idUSL1N2KT16E) on charges against Tether and Bitfinex which saw the company pay $18.5 million fine but avoid having to admit to any wrongdoing.

The Central Bank of Nigeria has moved to remind banks that "dealing in cryptocurrencies or facilitating payments for cryptocurrency exchanges is prohibited" and [instructed](https://www.coindesk.com/nigerias-central-bank-orders-banks-to-close-accounts-of-all-crypto-users) them to close the accounts of all people and entities who trade in cryptocurrencies.

The US Federal Reserve experienced an [issue](https://www.theregister.com/2021/02/24/federal_reserve_outage/) with its inter-bank transfer system which impaired service for hours. This happened soon after US Treasury Secretary Janet Yellen had [warned](https://www.cnbc.com/2021/02/22/yellen-sounds-warning-about-extremely-inefficient-bitcoin.html) that Bitcoin is "extremely inefficient" and poses risk to investors.

@notsofast urges everyone to learn from his [mistakes](https://cryptonews.com/news/trader-s-lesson-why-you-shouldn-t-keep-large-amounts-of-cry-9302.htm) that have led to losing ~$100,000 in crypto in a security breach: get a good password manager, use a hardware wallet, isolate dangerous browser extensions like Metamask in separate browser profiles or devices.

## About This Issue

This is issue 35 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

You can submit a story [here](https://github.com/xaur/decred-news/labels/next%20release) to be considered for the next release. [Feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, richardred
- reviews and feedback: davecgh, jholdstock, peter\_zen
- title image: saender
- funding: Decred stakeholders
