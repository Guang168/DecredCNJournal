# Decred月报 - 2020年3月

![abstract art](img/journal-202003-384.png)

_图片: Expand Vector by @saender_

三月重点:

- DCP-0005已激活, 这为Decred网络的轻量级客户端（SPV）用户带来史无前例的安全性和隐私保护。同时，任何仍在运行v1.4版本的客户端将被分叉，请尽快升级到最新版本。
- Decred DEX撮合了测试网上的第一笔由原子交换驱动的交易。
- 本月几乎所有关键的代码库都取得了惊人的进展，请在下面查看。
- 利益相关者批准的美国(英语内容创作)和巴西营销的年度预算为28.6万美元，其中的一些资金，用来继续制作《Decred月报》。
- 本期是Decred月报的第24期，标志着Decred项目的每月报道持续了两年时间！

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以构建和运行的源代码中，但对于普通用户来说，还不能在发布的二进制文件中使用。

[dcrd](https://github.com/decred/dcrd):

- ECDSA签名 与 secp256k1 软件包[分离](https://github.com/decred/dcrd/pull/2139)，从而清楚表明ECDSA只是一种可能的数字签名算法，并使Schnorr签名成为代码库的一级签名
- 导出的[字段值类](https://github.com/decred/dcrd/pull/2134)，以允许外部调用者执行优化的数学字段
- 通过谨慎精简化的操作来进一步优化签名验证
- 添加了从内存中[清除](https://github.com/decred/dcrd/pull/2117)私钥的方法，并[减少](https://github.com/decred/dcrd/pull/2131)了私钥的内部副本数量，从而增强了防止内存刮取的安全性
- 从签名解析和签名操作中完全[删除](https://github.com/decred/dcrd/pull/2107)大整数，而使用专门的mod n标量代码
- 对schnorr验证重新设计以解决多个问题
- 防止在几个方面滥用代码
- 删除未使用的多余代码

[披露](https://bounty.decred.org/2020/03/status-update/)了一个漏洞，该漏洞允许多天内存耗尽攻击，可能导致dcrd v1.4.0中的节点崩溃。3月13日，网络分叉了dcrd v1.5.0中实现了新共识规则，这意味着网络上的所有节点都必须以最新版本运行。由于此版本和更高版本包含该漏洞的修复程序，因此现已解决

根据CoinCode.sh 的[分析](https://coincode.sh/c/dcr/)，dcrd 与 btcd 的代码重叠少于16％，这意味着84％是新的开发工作。经过 @davecgh [确认](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15862843869377LGlSK:decred.org)，鉴于已编写的新代码，数字似乎合理，并指出dcrwallet中的差异甚至更为明显（尚未分析）

[dcrwallet](https://github.com/decred/dcrwallet):

- `fundrawtransaction`[实现的](https://github.com/decred/dcrwallet/pull/1706)命令可添加未签名的输入并将输出更改为原始交易
- 钱包操作已[切换](https://github.com/decred/dcrwallet/pull/1648)为使用版本2的过滤器（不建议使用v1过滤器，但仍由网络提供并由dcrwallet使用，下一版本将使用v2过滤器）
- `getaddressesbyaccount`固定的命令也[返回](https://github.com/decred/dcrwallet/pull/1695)该imported帐户的导入地址
- 未加密的P2SH兑换脚本已[移至](https://github.com/decred/dcrwallet/pull/1688)地址管理器存储中（这简化了存储并消除了解锁钱包以查看或存储脚本的要求）
- 对效率和语义的进行改进
- 清除不推荐使用的和未使用的代码

[Decrediton](https://github.com/decred/decrediton):

- 支持[冷Staking](https://github.com/decred/decrediton/pull/2424)（使用硬件钱包链接也需要）
- 支持在观察钱包中[导入脚本](https://github.com/decred/decrediton/pull/2423)
- 从dcrdata 检索已通过的[议程](https://github.com/decred/decrediton/pull/2442)
- 在“治理”选项卡上检查[新提案](https://github.com/decred/decrediton/pull/2420)
- 新的[投票视图](https://github.com/decred/decrediton/pull/2444)，[地址](https://github.com/decred/decrediton/pull/2416)显示在概述和事务视图上以及其他UI调整

正在开发中:

- [CoinShuffle++](https://github.com/decred/decrediton/pull/2452)隐私保护的集成

[Politeia](https://github.com/decred/politeia):

- 更改密码使种子[无效](https://github.com/decred/politeia/pull/1159)
- 测试改进和bug修复

tlog集成已经开始，[预计](https://github.com/decred/politeia/issues/1112#issuecomment-606147106)需要2个月的时间。在[2019年7月的月报中](201907.md#development)，我们不准确地报告了tlog集成的开始，但该工作实际上仅是开始研究，旨在作为概念验证并证明Google的[Trillian](https://github.com/google/trillian)数据存储可以替代现有的Git后端。它在八月份进行了[合并](https://github.com/decred/politeia/pull/951)，并包含一个具有基本功能的[客户端/服务器](https://github.com/decred/politeia/tree/master/tlog)，用于存储文档。这项工作经验提供了足够的见解，知道它会起作用。下一步是编写使用Trillian的Politeia后端。

tlog后端的主要优点是它将使Politeia具有更高的可延展性，并允许在公开内容之后审查内容，同时保留对所有已提交数据的审核记录。它还将允许正确解决重复注释的bug。

CMS:

- 分配提案[所有权](https://github.com/decred/politeia/pull/1135)的功能，该功能将在即将进行的更改中使用，以使提案所有者查看针对他们的提案收取的费用
- 可以[停用](https://github.com/decred/politeia/pull/1154)已付款发票上的临时承包商帐户并需要获得管理员批准才能允许其他发票
- 十月开始的重新设计工作终于[合并](https://github.com/decred/politeiagui/pull/1828)了。较大的更改将增加9K行代码和删除24K行代码

视觉更新的背后，重新设计的CMS总结了迁移politeiagui代码 [snew经典的UI](https://github.com/decred/snew-classic-ui)[过程](https://matrix.to/#/!VFRvyndKpzcLrVslQD:decred.org/$158644942810878cUwaw:decred.org)，以[pi-ui](https://github.com/decred/pi-ui)库。早在2018年，snew允许Redite风格的外观和感觉迅速使Politeia脱颖而出，但很快就变得难以开发。构建pi-ui并切换到它可以改善代码模块化，并提供了灵活的方式来组成和样式化UI组件，以使其符合设计规范，并提高性能。

[dcrstakepool](https://github.com/decred/dcrstakepool):

- 代码维护，bug处理和消除，增加文档，升级依赖关系和增加测试

[dcrpool](https://github.com/decred/dcrpool):

- 支持[方尖碑DCR1](https://github.com/decred/dcrpool/issues/110)
- [关闭](https://github.com/decred/dcrpool/pull/164)之前备份池数据库
- [重构](https://github.com/decred/dcrpool/pull/171)连接代码以简化测试
- 增加测试范围
- 对UX，配置的较小改进，并修复了一些错误
- 这项工作是为即将发布的1.1.0版本做的准备

[dcrlnd](https://github.com/decred/dcrlnd):

- 对系统进行[改进](https://github.com/decred/dcrlnd/pull/84)

正在开发:

- 新的[chainscan](https://github.com/decred/dcrlnd/pull/83)软件包，它使用提交的筛选器来更有效地检测与LN节点相关的事务，并且还可以在SPV模式下运行
- 使用嵌入式和远程dcrwallet作为事件源的chainntnfs软件包的[实现](https://github.com/decred/dcrlnd/pull/92)。这允许将dcrlnd与基础dcrd进一步解耦，这是让dcrlnd实例以SPV模式运行的要求
- 在上面的基础上，为远程钱包启用和测试[SPV模式](https://github.com/decred/dcrlnd/pull/95)（“远程钱包”是dcrlnd连接到已经运行的dcrwallet实例的连接模式，即不需要带有单独种子的自己的嵌入式钱包）

> 移动LN钱包需要SPV模式。即使在台式机钱包中，SPV可能仍将是主导的同步模式，因此dcrlnd支持SPV模式至关重要。这也是我在LN的[公告中](https://matheusd.com/post/announcing-dcrlnd/)概述的“路线图”中“立即工作”部分的最后一项，因此，总结了从lnd到dcrlnd的大部分移植工作。结束此次SPV的任务意味着我们可以开始探索Decred中可用的更多奇特更改（例如[PTLCs](https://suredbits.com/payment-points-monotone-access-structures/)依赖@davecgh也得出结论的Schnorr工作）。（@matheusd）

[dcrdex](https://github.com/decred/dcrdex):

- DEX客户端的命令行[控制应用程序](https://github.com/decred/dcrdex/pull/181)
- 通过客户端浏览器GUI[下订单](https://github.com/decred/dcrdex/pull/195)的能力
- [备份和还原](https://github.com/decred/dcrdex/pull/210)客户端密钥和其他帐户数据（较早的[#183](https://github.com/decred/dcrdex/pull/183)添加了客户端订单数据的备份）
- 客户跟踪[纪元订单](https://github.com/decred/dcrdex/pull/188)，并在纪元结束时验证订单[改组和匹配](https://github.com/decred/dcrdex/pull/189)
- [取消比率计算](https://github.com/decred/dcrdex/pull/206)，使服务器能够可靠地跟踪用户的已完成订单与已取消订单，并能够从数据库中重建任何用户最近的订单历史记录。这是社区行为执法的重要组成部分。
- 代码库重构和清理

一个重要的里程碑是[撮合交易](https://github.com/decred/dcrdex/pull/213)的完成。这是客户端的最后一个重要部分，它能够执行交换。使客户经历整个交换过程（撮合交易），与服务器进行通信，对交易对手交易进行必要的审计，并根据交换过程的要求创建和广播自己的合同和赎回交易。

6个贡献者总共合并了19个拉取请求，添加了11K行代码并删除了3K行代码（在[此处](https://github.com/decred/dcrdex/compare/94310f66c06fdf5ca31eeb80c9f6af7aecf4c31d...d3bd07f822200041092bdc85f5c1b752b3c9ee24)提交摘要）。

祝贺dcrdex团队在testnet上[完成](https://twitter.com/chappjc/status/1245075450625511425)了第一个由订单驱动的原子交换！

[dcrandroid](https://github.com/decred/dcrandroid):

- 添加[统计信息页面](https://github.com/decred/dcrandroid/pull/440)
- UI调整和修复

下一个版本的测试网版本可在[此处](https://play.google.com/apps/testing/com.decred.dcrandroid.testnet)获得。

[dcrios](https://github.com/raedahgroup/dcrios):

- 修改[发送页面](https://github.com/raedahgroup/dcrios/pull/557)
- 新的“[更多](https://github.com/raedahgroup/dcrios/pull/559)”菜单用户界面
- 交易页面的[新钱包](https://github.com/raedahgroup/dcrios/pull/600)选择器小部件
- 从[二维码](https://github.com/raedahgroup/dcrios/pull/581)读取DCR数量
- 多项bug修复和UI调整

下一个版本的测试网版本可在[此处](https://testflight.apple.com/join/7KL4VnB2)获得。

[dcrdata](https://github.com/decred/dcrdata):

- [原始JSON](https://github.com/decred/dcrdata/pull/1716)图表数据的通用URL 已添加到图表页面
- 小调整和bug修复

[tinydecred](https://github.com/decred/tinydecred):

- [Staking视图](https://github.com/decred/tinydecred/pull/53)显示已完成，未完成和正在等待被选的门票
- 简单[帐户视图](https://github.com/decred/tinydecred/pull/94)
- 创建帐户并发送DCR的简单[视图](https://github.com/decred/tinydecred/pull/125)
- [帐户发现](https://github.com/decred/tinydecred/pull/124)
- 更改测试以使用内存[数据库](https://github.com/decred/tinydecred/pull/116)
- 将整体测试覆盖率提高到[98%](https://github.com/decred/tinydecred/issues/70#issuecomment-606669036)，并修复了此过程中发现的一些错误，现在所有文件的覆盖率至少为94％

3个贡献者合并了总共56个拉取请求，添加了11K行代码和6K行代码（请在[此处](https://github.com/decred/tinydecred/compare/fa081e7f17d303f0eea31e9f07499db4e0acc53a...e1ef1ff72cb924d27098f9df151f6805d5db3e90)提交摘要）。

[docs](https://github.com/decred/dcrdocs):

- [dcrlnd](https://docs.decred.org/lightning-network/overview/)文档[已更新](https://github.com/decred/dcrdocs/pull/1083)为最新版本0.2.1，将命令分为几类
- [添加](https://github.com/decred/dcrdocs/pull/1081)了有关[如何](https://docs.decred.org/getting-started/joining-matrix-channels/)加入Matrix的指南
- 通货膨胀页已[重命名](https://github.com/decred/dcrdocs/issues/1074)为“[发行](https://docs.decred.org/advanced/issuance/)”以消除歧义
- [记录了](https://github.com/decred/dcrdocs/pull/1073)作为[Tor隐藏服务](https://docs.decred.org/privacy/cspp/how-to-cspp/#tor-hidden-service)访问CoinShuffle ++服务器

[decred.org](https://github.com/decred/dcrweb):

- 大幅度清理，修复了新网站中的小问题
- 更新的VSP[页面](https://github.com/decred/dcrweb/pull/853)
- 招聘页面已删除，decred.org/recruiting 现在重[定向](https://docs.decred.org/contributing/overview/)到“贡献”页面
- 路线图页面已[删除](https://github.com/decred/dcrweb/pull/857)

其他：

- 大多数项目升级为使用Go 1.14构建，并放弃了对Go 1.12的支持
- @mm发布了DigiSign Oracle，这是一个免费的开源Web应用程序，可帮助最终用户验证数字签名。它的创建是为了帮助Decred用户验证软件包签名，而不必使用复杂的命令行程序。您可以在[stakey.club](https://stakey.club/digisign-oracle/)上访问它，或将[源代码](https://github.com/mmartins000/digisign-oracle)下载到您的计算机上并使用网络浏览器打开。

## v1.6版本计划

> v1.6的粗略计划是在第二季度末发布。我们计划包括：去中心化的社区开发基金共识变更，Decrediton的Staking和非Staking CSPP支持，基于选票的VSP支持以及无数dcrd改进。(@jy-p 在[2020-03-20](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15855719584400kpyNr:decred.org))

## 人员

欢迎新的首次贡献者，他的代码已合并到主代码库中： @unimere ([decrediton](https://github.com/decred/decrediton/commits?author=unimere)).

社区统计：

- Twitter 粉丝: 40,694 (-207)
- Reddit 订阅: 9,760 (+22)
- Matrix 用户: 601 (+36)
- Discord 用户: 1,160 (+73), 已验证发布: 479 (+29)
- Telegram 用户: 2,607 (-71)
- YouTube 订阅: 3,980 (-10)
- Facebook 粉丝: 3,606 (+26), 喜欢: 3,273 (+24)
- LinkedIn 粉丝: 744 (+25)
- GitHub dcrd 星星: 536 (+1), 分叉: 1,507 (+11)

## 治理

3月份，[社区开发基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)获得了13,713 DCR，并花费了17,153 DCR。以3月份的每日 DCR/USD 汇率 $ 13.40计算，这是收到的$ 184K和花费的$ 230K。以2月份的每日平均价格$ 20.48计算，该月完成工作的美元费用为$ 281K。截至4月3日，库存余额为640K DCR（741万美元，折合11.58美元）。

本月发布了4个新提案。

DCRComic团队提出的新[提案](https://proposals.decred.org/proposals/2f08f8518bc7672069a10ac6461fd9ab341d4a9e4c343fd4a7ec426250f3896f)要求预算16,200美元，以制作12部漫画以及其它活动，并为每部漫画额外增加150美元，以花费更多时间调整产品以供社交媒体使用。在有人批评Stakey被过度使用来代表Decred生态系统中的许多不同角色之后，该提案被[搁置](https://twitter.com/DCRComic/status/1243197581104041984)以重新设计角色。4月6日对提案进行了修改，以添加新角色，这些[角色](https://github.com/pLabarta/dcrwebcomic/blob/master/Proposal2/NewChars.md)将与Stakey一起加入阵容，并于4月9日开始投票。

在社区根据COVID-19削减到177,800美元后，美国市场营销[提案](https://proposals.decred.org/proposals/c830ea5afea45a0aabf4092d1bea51fb10b8bfa2d8474aac03224f0f94d3d1af)被批准，获得74％的支持和31％的投票率。

巴西的营销[提案](https://proposals.decred.org/proposals/bc20f986c3ea2fed2ea074c377a89f1a4b956ea0d527a8b6c099a5a8f175beb5)也获得了批准，该提案要求在今年余下时间提供$ 108K，获得65％的支持，投票率达到34％。编辑该提案的目的是，在COVID-19局势持续存在的情况下，不会组织活动或为活动付费，但该项目并未从预算中删除，某些活动可能会在今年晚些时候进行。

提交了另外两个提案，正在讨论中。PolisPay App的一项[提案](https://proposals.decred.org/proposals/d3b16861a7e555db2fdd25b589123f4b6c4289c857fbdff329a4ffb1cb60c4d9)寻求5,000美元以支持DCR。还有一个建议为Decred Daily Twitter 帐户提供资金6个月并为其建立一个网站（总预算$ 5,280）。Decred Daily[提案](https://proposals.decred.org/proposals/7d42c6f4bf3059b64789185af615c1df97cb61a379425933be5ff01d074ed4d5)于4月9日开始投票。

i2 Trading的做市提案已经历六个月的做市活动，该活动于2019年10月下旬开始，因此将在2020年4月下旬结束.i2的交易日志由Company 0 审查，发现性能令人满意。i2计划提交一份提案，以继续进行做市活动，但将按比例缩小以反映当前的市场状况。

有关本月“Politeia活动”的更多详细信息，请参见《Politeia摘要》第[29期](https://blockcommons.red/politeia-digest/issue029/)。

## 网络

Hashrate: [March's hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=k73pwcch-k8jayo3s&bin=block&axis=time) opened at ~359 Ph/s and closed ~309 Ph/s, bottoming at 274 Ph/s and peaking at 556 Ph/s throughout the month. Pool [hashrate distribution](https://dcrstats.com/pow) as of Apr 1: UUPool 55%, Poolin 18%, lab.antpool.com 17%, Luxor 2.5%, BTC.com 2.2%, F2Pool 1.5%, BeePool 0.13%, CoinMine 0.08%, Suprnova 0.02% and others ~3.8%. Pool distribution numbers are approximate and cannot be accurately determined.

Staking: [30-day average](https://dcrstats.com/) ticket price was 141.9 DCR (+9.8). The [price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=k73pwcch-k8jayo3s&bin=window&axis=time) varied between 130.9-166.8 DCR. [Locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=k73pwcch-k8jayo3s&bin=block&axis=time) was 5.50-5.75 million DCR, which corresponded to 49.05-51.27% of the available supply [participating](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=k73pwcch-k8jayo3s&bin=block&axis=time) in PoS.

The ticket price topped at 166.82 which is again a new high since the stake difficulty algorithm change.

Block size: This month, the blockchain size grew by 129 MB. Blocks had an average [size](https://explorer.dcrdata.org/charts?chart=block-size&zoom=k73pwcch-k8jayo3s&bin=block&axis=time) of 14.5 KB. The smallest block had a size of 1.62 KB and the largest one, 374.98 KB. So far the major source of nearly full blocks is the Treasury: this month the payouts created a range of 9 full blocks on [Mar 16](https://explorer.dcrdata.org/blocks?height=432590&rows=20).

Transactions: In March, Decred users made 49,078 regular transactions and bought 44,149 tickets. 43,791 tickets were rewarded for voting and 728 were revoked. On average, there were 1,583 regular DCR transactions and 1,424 new tickets per day.

Nodes: Throughout [March](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1583020800000&to=1585699200000) there was an average of 146 public listening nodes and 246 total nodes per dcr.farm. Average version distribution for Mar: 28% dcrd v1.5.1, 20% dcrd v1.4, 15% dcrd v1.5, 8% dcrd v1.5 dev and RC builds, 5% dcrd v1.6 dev builds, 5% dcrwallet v1.5.1, 5% dcrwallet v1.4, 2% dcrwallet v1.5. On Mar 13 the new consensus rules activated and after that dcrd v1.4 can no longer follow the chain.

## Integrations

Probit [added](https://twitter.com/ProBit_Exchange/status/1235450770100649986) support for DCR/KRW and DCR/USDT pairs to their exchange.

Exmo.com had a sudden DCR [outage](https://twitter.com/Exmo_Com/status/1240255377507303431) a few days after the Mar 13 fork, the services [resumed](https://twitter.com/Exmo_Com/status/1240627750005870592) the next day. Currently, Exmo is the only integration [funded](https://proposals.decred.org/proposals/950e8149e594b01c010c1199233ab11e82c9da39174ba375d286dc72bb0a54d7) by stakeholders.

[NOWPayments](https://nowpayments.io/) payment processor that was launched in 2019 by ChangeNOW supports DCR among [40+](https://nowpayments.io/supported-coins/) other assets.

ChainRift [announced](https://twitter.com/ChainRift/status/1228010062163202049) in Feb that they will be shutting down exchange operations and pivoting to a software development company.

DCR was [added](https://twitter.com/Checkmatey/status/1244030247558729729) to FTX PRIV-PERP index future contract that tracks a basket of 9 privacy coins. Index calculation can be found [here](https://help.ftx.com/hc/en-us/articles/360027668812-Index-Calculation).

User AGspearo was not able to access their [funds](https://www.reddit.com/r/decred/comments/fim5j2/stakepool_failure_caused_me_to_lose_all_my/) due to the VSP d1pool.com shutting down without notice and them not having access to their redeem script. AGspearo spent a lot of time on support trying to resolve this issue but ultimately they were unable to get their funds. @davecgh broke down the issue as a [comment](https://www.reddit.com/r/decred/comments/fim5j2/stakepool_failure_caused_me_to_lose_all_my/fkiac45) and also said a possible consensus change might solve these [issues](https://www.reddit.com/r/decred/comments/fim5j2/stakepool_failure_caused_me_to_lose_all_my/fkku35k). If you are reading this and do not have your redeem scripts backed up please take this a warning and do a [backup](https://docs.decred.org/wallets/decrediton/using-decrediton/#backup-redeem-script) and store then along with your seed.

Some VSPs that had broken signup pages/out of date/returning errors had been [put on notice](https://github.com/decred/dcrwebapi/pulls?q=is%3Apr+author%3Ajholdstock+created%3A2020-03-01..2020-03-31) that they will be removed from the [listing](https://decred.org/vsp/). Some of them have responded and fixed the issues. raqamiya.net, tokensmart.io, and dcrpos.idcray.com have been removed since they failed to respond.

Warning: the authors of Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

[Decred in Depth](https://decredindepth.libsyn.com) released two new episodes in March and one in early April, while [Rough Consensus](https://roughconsensus.libsyn.com/) also released 2 episodes (see [Media](#media) below).

@Dustorf [posted](https://proposals.decred.org/proposals/c830ea5afea45a0aabf4092d1bea51fb10b8bfa2d8474aac03224f0f94d3d1af/comments/56) that he will be operating in a reduced capacity for the next couple months and that the cost of the proposal will be reduced accordingly. The executions affected include: newsletter, original content generation, Decred Assembly, PR, and release coordination, and update work. This specifically means that the DEX release will have to be managed by the developers and the community at large.

@dezryth [posted](https://scottrchristian.com/2020/03/15/dezryth-proposal-updates/) a second update about his operation of Decred's Facebook account for the month of February. This one is more detailed and includes stats for each post, comparison to competitors, and shares some ideas about next steps. @dezryth acknowledges that current stats are not great and that organic following is hard to build, but on the good side active posting brought a 30% increase in daily views.

@bee has extensively (really) [commented](https://www.reddit.com/r/decred/comments/fa70c3/decred_2019_marketing_report/) on the 2019 Marketing Report and shared his vision for moving forward.

A comprehensive compilation of [common misconceptions](https://github.com/decredcommunity/wiki/blob/master/wiki/misconceptions.md) and criticism of Decred was added to decredcommunity wiki, along with responses to them. Feedback/contributions welcome, discussion is [here](https://www.reddit.com/r/decred/comments/frqkt0/your_favorite_misconceptions_about_decred_in_one/).

Monde PR's achievements for March:

- outreach and introductions to target journalists
- pitched reactive comments to current news stories
- submitted comments from Decred spokespeople to 7 news stories
- pitched Decred to 3 upcoming features
- submitted thought leadership piece written by @richardred to ValueWalk
- secured 2 media interviews

News coverage secured by Monde PR:

- an [article](https://cointelegraph.com/news/proof-of-stake-vs-proof-of-work-which-one-is-fairer) in Cointelegraph featuring commentary from @jy-p on consensus models
- an [article](https://www.financemagnates.com/cryptocurrency/news/fintech-experts-share-tips-for-remote-work-during-coronavirus-quarantine/) in Finance Magnates featuring commentary from @richardred on remote working
- an [article](https://www.coindesk.com/remote-working-proves-unexpected-hero-as-half-of-us-economy-shifts-to-home-offices) in CoinDesk featuring commentary from @jy-p on rapid scaling which was also syndicated to Yahoo Finance

## Events

Attended:

- Mar 4 - [Decred Meetup](https://www.eventbrite.com/e/decred-meetup-la-plata-tickets-95666770887) - La Plata, Argentina. It was an introduction to Decred project in which @camilolwi, @tomee, and @pablito talked about the fundamentals of Decred, its security and hybrid consensus model, governance, voting and how to become a contractor for the project. There were around 20 attendees to the meetup and a session of networking. ([photos](https://twitter.com/cryptorc_tech/status/1238180910513733634))
- Mar 4 - [Decred Meetup](https://www.eventbrite.com/e/decred-en-uninet-business-school-caracas-venezuela-tickets-97157792573) - Caracas, Venezuela. The meetup was co-hosted by Uninet Business School and Innova Consultants. There were 15 attendees to the meetup, there was an introduction to Decred, its security and hybrid model, privacy, how to contribute, followed by a session of Q&A and networking. ([photos](https://twitter.com/Decred_ES/status/1235324847338795009))
- Mar 4 - [Crypto and Blockchain 2020 and Beyond](https://www.meetup.com/BC-Aus/events/268793182/) - Melbourne, Australia. This 80+ person event directed entry fees to Crypto Fire Alliance to help with the bushfire emergency (the event raised $1K while the entire program [raised](https://www.finder.com.au/crypto-bushfire-fundraiser) $27K in crypto). @eSizeDave joined an hour-long panel discussion, [noting](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158381267934685XUpiS:decred.org): "the audience had more questions for me than anyone else, and got a lot of follow-up meetings as a result of it". ([report](https://github.com/decredcommunity/events/blob/master/reports/20200304-crypto-and-blockchain-2020-and-beyond-melbourne-australia.md), [video](https://twitter.com/DecredAustralia/status/1235390840307978245))
- Mar 5 - [Decred Meetup](https://www.eventbrite.com/e/decred-meetup-en-valencia-venezuela-tickets-97804334397) - Valencia, Venezuela. Co-hosted by ClicTechNova y CoWorking Lab. The meetup was an introduction to the Decred ecosystem, hybrid blockchain, governance mechanism, privacy, and elements that make Decred a DAO. There were ~50 attendees that asked interesting questions about social attacks on the network, how to contribute and the incentive model of DCR. ([photos](https://twitter.com/Decred_ES/status/1236079742643773440), [video](https://twitter.com/Decred_ES/status/1236080559752916998))
- Mar 6 - [Impact Hub](https://www.eventbrite.com/e/decred-meetup-impact-hub-caracas-venezuela-tickets-97159680219) - Caracas, Venezuela. Co-hosted by El Dorado y Cointigo. The meetup was an introduction to the Decred ecosystem, its governance structure and what makes it a different cryptocurrency from the rest. Around 30 people attended, several entrepreneurs and developers but also several new users of cryptocurrencies looking for more information about the technology and investment opportunities. ([photos](https://twitter.com/Decred_ES/status/1236337867095343104), [video](https://twitter.com/Decred_ES/status/1236340242698752001))
- Mar 8 - [International Women's Day](https://www.meetup.com/GDGCasablanca/events/268661463/) - Casablanca, Morocco. The event was held at ENSAM, a University of Science. Most of the 70 attendees were data science students and developers. @arij gave a 1-hour talk about blockchains and Decred and a workshop afterwards: "What I've learned from my experiences talking and explaining blockchain technology and Decred, is that people are more interested when you show them how things really work with demo and videos, especially when it is their first time learning about it". ([notes](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$158374584733992NOIMZ:decred.org), [photos](https://www.flickr.com/photos/187387360@N04/albums/72157713440754483))
- Mar 12 - [Bitcoin Woman to Woman](https://twitter.com/bitcoinemb/status/1233500964566523911) - Mexico City, Mexico. Co-hosted by the Bitcoin Embassy, the ~30 person meetup was to discuss women's involvement in the cryptocurrency industry and how to empower women to use crypto. @francov\_ did a presentation on how to contribute to the Decred project and her experience working in the industry. "The highlight of the talk was to express that we do not need your title, gender, nationality, age, even your real name, we only need your talent and your aspiration to help the Decred ecosystem grow". The meetup was followed by a networking session. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200312-bitcoin-woman-to-woman-mexico-city-mexico.md))
- Mar 12 - [Decred Meetup](https://www.meetup.com/es-ES/BitcoinBlockchainUruguay/events/269160706/) - Montevideo, Uruguay. Around 25 people attended the meetup. @tomee presented an introduction to Decred and its security, adaptability, and sustainability, Politeia, governance and how to contribute. The meetup was also a networking session and some of the people knew the project from Labitconf. (photos: [1](https://twitter.com/ivarese/status/1238628854379536389), [2](https://twitter.com/cryptorc_tech/status/1241081659669315585))
- Mar 12 - [Blockchain Summit Latam](https://twitter.com/Decred_ES/status/1237552322596593665) - Panama City, Panama. The event was rescheduled to Oct 15-16, but this change occurred 24 hours before the event when some speakers were already in the area (~35 people). The event staff took the opportunity and hosted a small meetup where presenters got the chance to network and to know about the projects from close up. @adcade and @elian talked with a few representatives and secured an [interview](https://es.cointelegraph.com/news/decred-how-does-your-development-continue-during-the-bear-market) for Spanish Cointelegraph. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200312-blockchain-summit-latam-meetup-panama-city-panama.md))
- Mar 12 - [Hablemos Decred 01](https://twitter.com/Decred_ES/status/1238242352306614273) - Internet. "Let's Talk Decred", the first Spanish online meeting used Decred's Discord server. Most questions were about Decred's PoS voting system. Those who had some prior knowledge of crypto asked how to stake, and those who didn't wanted to know more about voting rights and what can stakeholders do with their tickets. About a third of ~15 people were new to the project. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200312-hablemosdecred-01-internet.md))
- Mar 18 - [Exchanges in LATAM](https://twitter.com/Decred_ES/status/1240428280756310018) - Internet. @elian talked about centralized and decentralized exchanges in a virtual meetup with people from [@AvaLatam](https://twitter.com/AvaLatam), [@blockchain_land](https://twitter.com/blockchain_land) and virica.io Mexico. Around 16 people attended and one lesson learned was that online talks should be 30 min or less.
- Mar 24 - [Decred Webinar](https://www.meetup.com/es-ES/blockacademycl/events/269108758/) - Internet. @tomee and @camilolwi talked all things Decred and the challenges of decentralized blockchain governance in a webinar co-organized with Blockchain Academy Chile. ([video](https://www.youtube.com/watch?v=U07ZL_qFAQM))
- Mar 27 - [Hablemos Decred 02](https://twitter.com/Decred_ES/status/1243214184793485314) - Internet. Second Spanish online meetup explored Jitsi to connect 13 participants from Argentina, Mexico, Bolivia, Chile, of which 7 were new to the project. This time the call started with an intro talk about Decred, a demo of Decrediton, and an open mic for questions and comments. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200327-hablemosdecred-02-internet.md))
- Mar 29 - [Binance AMA](https://twitter.com/Decred_ES/status/1244360357843533825) - Internet. The event was hosted in the Binance Spanish Telegram group with 8,000+ members and received a high level of engagement. @adcade, @elian, and @pablito got 155 questions from 73 participants and gifted 0.333 DCR to the best questions. A good amount of knowledge was gathered that can signal where prospect Decred users lack information. This was the second Decred AMA with the Binance Spanish community and the longest AMA they had so far (~2.5 hours). ([report](https://github.com/decredcommunity/events/blob/master/reports/20200329-decred-ama-binance-spanish-community-internet.md))
- Mar 30 - [Decred and Sound Money Virtual Meetup](https://www.meetup.com/Decred-Australia/events/269640276/) - Internet. The event was hosted by @eSizeDave and @zohand and joined by @Checkmate to discuss key topics such as sound money, the macroeconomic environment, gold, and Decred. Participants were quite impressed by the quality and left good feedback, one of them enjoying that it was "mentally stimulating". ([report](https://github.com/decredcommunity/events/blob/master/reports/20200330-decred-and-sound-money-internet.md))

Cancelled:

- Apr 5 - [Toronto Blockchain Week](https://www.eventbrite.ca/e/discover-decred-an-autonomous-digital-currency-toronto-blockchain-week-tickets-91562362491) - Toronto, Canada.

Upcoming:

- Apr 13-17 - [Jalisco Talent Land @ Home](https://www.talent-land.tv/) - Internet. In a panel called "Decred, crypto and the future of money" Decred LATAM team will give a brief on Decred and explore how crypto will transform remote work and our interaction with money. The panel will be streamed on [talent-land.tv](https://www.talent-land.tv/) on Apr 15, 21:00 (CST, UTC-5).
- Apr 16 - [Decred Webinar](https://twitter.com/Decred_ES/status/1245452957417684992) - Internet. The topic will be "Let's talk about cryptocurrencies and the future of money" - a webinar hosted by Ibero (university) to discuss crypto and give an overview of Decred.
- May 14 - [BlockConf](https://blockconf.digital/) - Internet. Decred LATAM team will run a virtual booth for Decred to answer questions from the attendees. If anyone wants to help with keeping the booth active in several time zones during the 48-hour event, please contact @elian.
- May 30-31 - [Bitconf](https://www.bitconf.com.br/portal/) - São Paulo, Brazil. Decred will have multiple talks on various subjects.
- June or later - [Campus Party Amazonia](https://brasil.campus-party.org/campus-party-amazonia-2020/) - Manaus, Brazil. Moved from March.
- June or later - [Jalisco Talent Land](https://www.talent-land.mx/en/home/) - Guadalajara, Mexico. Moved from April.
- End of 2020 - [DevOpsDays](https://devopsdays.org/events/2020-natal/welcome/) - Natal, Brazil. Moved from March.

Postponed until further notice:

- [CIBTC Blockchain Summit](http://cibtc.es/) - Motril, Spain.
- Decred Meetup - La Paz, Bolivia.
- [Bitcoinference](https://www.eventbrite.com/e/bitcoinference-where-the-blockchain-meets-you-tickets-94598812595) - Cancún, Mexico.

## Media

[decredpower.info](https://decredpower.info/) is a new single-page directory to explore all things Decred. Suggestions are welcome [here](https://github.com/raedahgroup/decredpower/issues).

Selected articles:

- Observing Ethereum governance during the ProgPoW debate by @Checkmate ([medium](https://medium.com/@_Checkmatey_/observing-ethereum-governance-during-the-progpow-debate-9bf1aec724ad))
- Crypto risk is not what you think by @Dustorf ([medium](https://medium.com/@dlefebvr/crypto-risk-is-not-what-you-think-8a2662840b70))
- Theory of three pillars in the cypherpunk social contract by @Cato\_io ([medium](https://medium.com/@cato_io/threepillarstheory-cd6b57c5d88a))
- Public service, pandemics and crypto networks by @mrbulb ([medium](https://medium.com/@decentpartners/public-service-pandemics-and-crypto-networks-379dce1594d1))
- Decred: how does your development continue during the bear market? by @adcade (in Spanish, [es.cointelegraph.com](https://es.cointelegraph.com/news/decred-how-does-your-development-continue-during-the-bear-market))

The Brazil Marketing and Events [proposal](https://proposals.decred.org/proposals/bc20f986c3ea2fed2ea074c377a89f1a4b956ea0d527a8b6c099a5a8f175beb5) was covered in the media from an interesting "investment in Brazil" perspective (in Portuguese):

- "Decred's community allows more than 500,000 BRL to be invested in Brazil" ([criptofacil.com](https://www.criptofacil.com/comunidade-decred-permite-que-mais-r-500-mil-sejam-investidos-brasil/))
- "Cryptocurrency will invest more than half a million in Brazil" ([livecoins.com.br](https://livecoins.com.br/criptomoeda-vai-investir-mais-meio-milhao-brasil/))
- "'Whales' approve and Decred can invest more than 500,000BRL to promote cryptocurrency in Brazil" ([cointelegraph.com.br](https://cointelegraph.com.br/news/decred-pode-investir-ate-us-500-mil-para-promover-criptomoeda-no-brasil)) - this one is poorly written and is based on another interview (@emiliomann)
- "The cryptocurrencies that invest the most in Brazil" ([cointimes.com.br](https://cointimes.com.br/as-criptomoedas-que-mais-investem-no-brasil/))

Translations:

- Theory of three pillars in the cypherpunk social contract - [in Spanish](https://medium.com/decred-es/teor%C3%ADa-de-los-tres-pilares-en-el-contrato-social-del-cypherpunk-40f569836b6a) by @francov\_
- Decred Technical Brief - [in Arabic](https://insaf01.github.io/decred-arabic/articles/decred-technical-brief-ar.html) by @arij
- Decred Journal February 2020 was translated to Arabic (@arij), Chinese (@Dominic) and Spanish (@francov\_). All three are stored [in Git](https://github.com/xaur/decred-news/blob/docs/guidelines.md#why-git) which helps to preserve the work long-term and protect it from censorship. Thank you all for spreading the word!

Videos:

- Decred's 2020 marketing and publishing proposals for the USA & Brazil breakdown by @Exitus ([youtube](https://www.youtube.com/watch?v=Liol1lLCinQ))
- Decred bi-Weekly news update - March 12, 2020 by @Exitus ([youtube](https://www.youtube.com/watch?v=N4U1FwYUaKA))
- Decred bi-Weekly news update - March 31, 2020 by @Exitus ([youtube](https://www.youtube.com/watch?v=MBi7d263HvE))
- Top 5 staking coins in 2020 by Coin Bureau ([youtube](https://www.youtube.com/watch?v=znx7H7JWtfg))

Audio:

- Decred in Depth Ep. 19 - Leo Zhang of Iterative Capital talks about Proof of Work mining, gives a first-hand account of mining economics, and considers the benefits of a hybrid PoS component and formal stakeholder decision-making. ([libsyn](https://decredindepth.libsyn.com/leo-zhang-dcr-mining), [youtube](https://www.youtube.com/watch?v=iWi3nK0HIHE), [soundcloud](https://soundcloud.com/decredindepth/leo-zhang-dcr-mining))
- Decred in Depth Ep. 21 - @Exitus talks about producing video content for the Decred DAO, becoming a contractor and the challenges crypto marketing faces during the bear market. ([libsyn](https://decredindepth.libsyn.com/-exitus-dcr-community-managment-media), [youtube](https://www.youtube.com/watch?v=oGi3NA14CZU))
- Rough Consensus Ep. 2 - Distributed consensus. @mr.black, @Checkmate, and @permabullnino discuss the concept of triple entry accounting and how it provides a framework for analyzing consensus mechanisms. The theory is that PoW, PoS and hybrid security systems provide different security and ledger assurances. ([libsyn](https://roughconsensus.libsyn.com/rough-consensus-2-distributed-consensus))
- Rough Consensus Ep. 3 - The long road ahead. @mr.black, @Checkmate, and @permabullnino discuss the latest macro shift triggered by COVID-19, the popping of the longest equities bull market in history, and how cryptocurrencies can play a role in the future. ([libsyn](https://roughconsensus.libsyn.com/rough-consensus-3-the-long-road-ahead))
- POV Crypto Podcast Ep. 127 - Hard money in the time of brrr with @permabullnino ([libsyn](https://povcryptopod.libsyn.com/127-hard-money-in-the-time-of-brrr-with-permabullnino), Decred mentioned around 30 min mark)
- What is Decred? by @elian (in Spanish, [criptotendencias.com](https://www.criptotendencias.com/podcast/episodio-30-que-es-decred-entrevista-con-elian-huesca-community-builder-business-dev-del-proyecto/))
- Decred Brief by @elian (in Spanish, [Territorio Bitcoin](https://www.ivoox.com/episodio-111-especial-comunidad-blockchain-cuarentena-audios-mp3_rf_49382826_1.html))

## Community Discussions

Comm systems news:

- A guide on how to join the Decred Matrix community was published at [docs.decred.org](https://docs.decred.org/getting-started/joining-matrix-channels/). If you prefer to be guided by Stakey, a slightly different version is available at [dcrcomic.org](https://dcrcomic.org/guide-enter-the-matrix.html).
- FYI you can watch the [r/decred comment feed](https://www.reddit.com/r/decred/comments/) to never miss a new comment.

Selected Reddit posts:

- u/oiezz has suggested using the monthly Journal posts as discussion spaces, and last month's [post](https://www.reddit.com/r/decred/comments/fgo0p4/decred_journal_february_2020/) has accumulated 18 comments.
- A [post](https://www.reddit.com/r/decred/comments/fhrsqn/austerity_mindset/fkd6nrn/) from u/Corp-Por asking whether Decred should adopt an austerity mindset with Treasury funds had 22 comments and a score of 7. Most of the commenters were not as keen as the OP to make drastic changes, citing the Treasury's ample reserves and capacity to maintain funding at current rates for 5 years.
- A [post](https://www.reddit.com/r/decred/comments/frb863/next_privacy_iteration_how_private_and_fungible/) asking about Decred's next privacy iteration had @jy-p respond to say that the approach is to pick the low-hanging fruit (Decrediton support, post-quantum security), continue to increase mixing uptake, then revisit questions about how to enhance privacy further.
- @davecgh [responded](https://www.reddit.com/r/decred/comments/fim5j2/stakepool_failure_caused_me_to_lose_all_my/) to the unfortunate story of a Decred stakeholder who has lost access to their staked DCR because the VSP they were using went offline, their Decrediton machine was destroyed, and they had not saved the redeem script (see details [here](https://docs.decred.org/wallets/decrediton/using-decrediton/#backup-redeem-script)). @davecgh explained that the redeem script is shared with the VSP as a multi-sig where either the user or VSP can redeem locked DCR and revoke tickets. As redeem scripts are reused and revealed when the first ticket is redeemed, this stuck DCR scenario can only occur when the wallet of the user or VSP has never been online to redeem any of the tickets that used it. Once a single ticket has been redeemed by that wallet/VSP combination, the script is effectively stored in the blockchain.
- @bee [thinks](https://www.reddit.com/r/decred/comments/frqvmc/checkmate_on_twitter_ftx_has_finally_listed_dcr/flxb7s0/) that derivatives are evil and is hoping to get enlightened about their benefit for the public.
- @bee made a [point](https://www.reddit.com/r/decred/comments/frqkt0/your_favorite_misconceptions_about_decred_in_one/fm1jrmc/?context=3) that not all consensus changes are as undesirable as frequent PoW algorithm changes necessary to maintain ASIC resistance.

Selected Twitter discussions:

- @swack lost his hammer and tweeted this [thread](https://twitter.com/swack0/status/1239674494526111747) about Decred as the only non-Bitcoin cryptoasset that deserves consideration as SoV and fiat alternative, citing adaptability, sustainability, and lack of associated leveraged financial products.
- DCP-0006 Social Media Governance, [announced](https://twitter.com/decredproject/status/1245399765489254400?s=20) Apr 1, is in doubt with an unexpectedly large proportion of respondents (66%) to the Twitter poll voting to give Twitter the greatest weighting - this raises serious questions about the sampling methodology.
- @chappjc [tweets](https://twitter.com/chappjc/status/1245075450625511425) about the first dcrdex order-driven atomic swap being coordinated.
- @davecgh comes out of twitter retirement with a popular [tweet](https://twitter.com/davecgh/status/1238309416270790658?s=20) about the activation of DCP0005 Block Header Commitments.

## Markets

In March DCR was trading between USD 8.68-19.78 / BTC 0.0017-0.0021. The average daily rate was $13.40.

On Mar 7 BTC/USD started its decline from $9,100 mark down to $7,800 on Mar 11. On Mar 12 it joined the global COVID-19 panic and tanked below ~$4,500 (and [even lower](https://twitter.com/HsakaTrades/status/1239227306863820801) in some markets). Most cryptoassets lost around 40% that day, demonstrating their mostly speculative price levels and persisting dependence on BTC. This dump took DCR/USD with it down to ~$8.

Fred Wilson [noted](https://avc.com/2020/03/correlation-and-market-meltdowns/) that "in panics, all assets are correlated", but when the panic settles cryptocurrency fundamentals might start kicking in.

## Relevant External

Markets everywhere had a [very bad time](https://www.bloomberg.com/news/articles/2020-03-08/yen-slides-as-oil-price-war-adds-to-global-worries-markets-wrap) as the severity of the COVID-19 situation became clear and nations began to lock down. Cryptocurrency prices declined as much or more than most other assets, all Decred meetups and events are canceled or moving online, and some contributors have more childcare to do than before, but those seem to be the only changes that are directly relevant to Decred. Nevertheless, the situation obviously has an effect on all of us and the broader macroeconomic environment and outlook. Stay safe.

It was a challenging month for DeFi, as a sharp drop in the price of ETH strained the stability of the DAI stablecoin. When ETH price moves too much some DAI loans will be liquidated in auctions if their holders do not add more ETH to reach the required collateralization, but on this occasion, the price appears to have moved too quickly for the liquidation auctions to keep up. This [article](https://medium.com/@whiterabbit_hq/black-thursday-for-makerdao-8-32-million-was-liquidated-for-0-dai-36b83cac56b6) explains how $8.32 million worth of DAI was liquidated for $0, as unforeseen conditions in the auction process (including ETH chain congestion) resulted in 36% of all liquidation auctions going to the highest bidder at $0.00. "The greatest Vault has lost ~35,000 ETH whereas the most successful liquidator has had a profit of 30,000 ETH". This left the Maker Foundation and community in a difficult [position](https://www.coindesk.com/defi-leader-makerdao-weighs-emergency-shutdown-following-eth-price-drop), considering changing the rules on the fly or triggering an emergency shutdown. The Foundation [decided](https://www.coindesk.com/makerdao-debts-grow-as-defi-leader-moves-to-stabilize-protocol) not to use its power to intervene directly by triggering a shutdown, and moved to introduce proposals that modified risk parameters and set up an auction of newly printed MKR tokens to pay the protocol debt and "refund CDPs that lost funds".

The Steem-Sun conflict began last month when the Steemit company (and its "ninja mined" STEEM tokens) was acquired by Justin Sun - Steem (DPoS) witnesses adopted a hard fork to nullify those tokens, then Sun mobilized exchange support to oust the established witnesses and replace them with puppets that would not adopt the fork, preserving his STEEM tokens. In March the strategy of the Steem community changed, as an influential group decided to [migrate](https://www.coindesk.com/steem-will-hard-fork-in-just-hours-over-community-fears-of-justin-sun-power-grab) away from the Steem blockchain to a new one called Hive. Exchanges Binance and Huobi are said to be supportive of this move, in a remarkable turnaround from their actions last month when they voted with Sun. Prominent members of the Steem community thanked community members for withdrawing their STEEM from exchanges, to put pressure on exchanges to backtrack on supporting the Sun-powered witnesses. It seems the exchange operators were also misled about the significance of their votes in that context, believing that they were voting for a regular protocol upgrade.

Hive is the same as Steem in most regards, with 1 STEEM being exchangeable for 1 HIVE - the main difference is that Sun's Steemit STEEM tokens will not be redeemable on the HIVE chain, effectively cutting them out of the ecosystem. When this [story](https://www.coindesk.com/splinter-cryptocurrency-hive-outperforms-justin-suns-steem-after-one-week-trading) was written the price of HIVE was almost double that of STEEM, but as of Apr 4, the two tokens are trading for similar prices. This case should be of interest to those who say coin voting is plutocratic, as it shows what can happen when whales try to use their coins to impose their will on an unwilling community.

It has been a good month for people who like to buy, hold or sell cryptocurrency without being considered a criminal. The governments in [South Korea](https://thenews.asia/amendment-to-special-reporting-act-passes-cryptocurrency-trading-now-legal-in-south-korea/) and supreme court in [India](https://news.bitcoin.com/bitcoin-legal-india-supreme-court-verdict-cryptocurrency/) made moves to nullify previously imposed restrictions on cryptocurrency trading.

Since Mar 18 Tether has issued over $400M USDT in batches of $60M and surpassed the [$6 billion](https://beincrypto.com/tether-usdt-quietly-surpasses-the-6-billion-mark/) mark. On Mar 25 USDT held on exchanges has set a new ATH of [$1.2 billion](https://twitter.com/glassnodealerts/status/1242849119456157699). The timing is interesting as it comes quickly after the market crash of Mar 12. Use USDT with caution, because even its co-founder believes ["it doesn't really matter"](https://beincrypto.com/tether-co-founder-it-doesnt-really-matter-if-usdt-backed-by-equal-amount-of-dollars/) if it's backed by an equal amount of dollars.

U.S. government approved an exceptionally large [$2 trillion](https://www.zerohedge.com/economics/anatomy-2-trillion-covid-19-stimulus-bill) "stimulus" plan attributed to COVID-19. Discussion of the source of funds is still rare in the media. One politician [argued](https://twitter.com/RepThomasMassie/status/1243565651391897603) that the bill creates even more secrecy around the Fed that is already not auditable.

U.S. Fed made multiple unprecedented moves attributed to COVID-19, succinctly [summarized](https://www.bloomberg.com/news/articles/2020-03-25/fed-unbound-all-the-u-s-central-bank-s-corona-related-moves) by Bloomberg. Most of that means [creating money](https://seekingalpha.com/article/4335693-inflation-alert-money-supply-expanding-26x-rate-of-qe1) out of thin air without any labor, and then loaning out that money to people and businesses who will need to _work_ to pay it back. Among the measures are swap lines built to "pump USD out across the world to ease access to the world's most important currency".

President of one of the 12 Federal Reserve Banks openly admitted in an [interview](https://www.zerohedge.com/markets/kashkari-says-fed-has-infinite-amount-cash-we-create-it-electronically) that "there's an infinite amount of cash at the Federal Reserve".

ECB [announced](https://www.ecb.europa.eu/press/pr/date/2020/html/ecb.pr200318_1~3949d6f266.en.html) a EUR 750 billion "Pandemic Emergency Purchase Programme" and [noted](https://twitter.com/Lagarde/status/1240414918966480896) "There are no limits to our commitment to the euro. We are determined to use the full potential of our tools, within our mandate". The bank is ready to further increase the size of asset purchase programmes and revise any self-imposed limits.

## Happy Birthday DJ!

24th issue marks the second anniversary of Decred Journal.

Retrospective and a bit of trivia from @bee:

- The DJ team has grown from 2 to ~5 stable contributors, ~3-8 translators, and ~7-11 people reviewing and sharing feedback.
- The byte size of an issue has grown from 20 KB to ~50 KB. The biggest issue was [64.5 K](https://xaur.github.io/decred-news/journal/201908.html) (7.5K words).
- Our production process has evolved significantly and is now extensively [documented](https://github.com/xaur/decred-news/blob/docs/guidelines.md).
- You may have noticed that [Decred](https://xaur.github.io/decred-news/journal/201805.html) [Cakes](https://xaur.github.io/decred-news/journal/202002.html) have a special meaning for me.
- To publish the very [first](https://xaur.github.io/decred-news/journal/201804.html) issue we needed a title. Among the candidates considered were "Monthly Stakeholder Entertainment Session" and "Deep in Decred". The latter was rejected for its sexual connotations.
- In March 2019 I got somewhat exhausted and [announced](https://xaur.github.io/decred-news/journal/201903.html#psa-decred-journal-takes-a-break) that the production of future issues is uncertain. Luckily, a few more people have [stepped in](https://github.com/xaur/decred-news/issues/65) and we continued.
- Problem of the first year: when starting every issue I worried that I wouldn't collect enough content and that it would look poor compared to previous months that had so much. I was wrong every single time. Problem of the second year: when finishing every issue I worried that it is too big and it got hard to track everything that is happening.
- I couldn't imagine what the [index](https://xaur.github.io/decred-news/) of all issues and translations would look like in 2 years!
- After pioneering the use of Git and GitHub for DJ I began to annoy pretty much everyone in the community to do the same for other documents. I believe that knowledge preservation is [important](https://github.com/xaur/decred-news/blob/docs/guidelines.md#why-git) and will keep annoying you guys. Thank you for your patience.
- About 6 months after starting DJ I got upset about declining Reddit upvotes. Then I talked to people and learned two things. First is that people who've been here for years say it is common: humans get less sensitive to any stimulus over time, even a good one. Second is that I took upvotes seriously without even knowing who is behind those numbers. But people I do know, talk to every day, people of highest intelligence and wisdom who are the reason why I'm still here, keep telling me I'm doing a good job. And they keep doing an amazing job for years without chasing the likes. So I asked myself, why do I care about these numbers more than I care what the best people around me think? It makes no sense! So I stopped worrying about that. (No offense to our dear readers, we value your feedback greatly, just not the number of clicks! I'm sharing this for anyone who gets too focused on stats).
- Thanks to Decred stakeholders for funding this work and helping us deliver the scale and quality of this production.
- We received a lot of positive [feedback](https://xaur.github.io/decred-news/testimonials.html) over these two years. Praise is not the goal, but kind words let us know that we're still on the right track. Thank you for all the support!

## About This Issue

This is issue 24 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, elian, degeri, l1ndseymm, kozel, pablito, richardred, s\_ben
- reviews and feedback: adcade, ammarooni, chappjc, davecgh, emiliomann, guisso, jholdstock, jrick, lukebp, matheusd, michae2xl, raedah
- title image: saender
