# Decred月报 – 2020年11月

![abstract art](img/journal-202011-384.png)

_图片: @saender_

十一月热门:

- v1.6 经过了4个候选版本的测试，进行了许多bug修复和用户体验的改进后暂时没有发现其它问题，这也意味着即将发布正式版本。
- dcrdex发布了修补程序，其中包含重要的案例修复程序以及对下一个版本的UI和后端改进。
- 用于继续开发移动钱包的资金和一个新的GoDCR PC钱包提案已经获得批准，用于GoDCR的资金还包括赞助用于接口的Gio库。
- 已经有四个VSP服务商进行了vspd升级，用以支持在Decrediton v1.6中提供的新的无注册帐户选票购买和匿名选票购买。

## v1.6 候选版本4

新的v1.6 候选版本4修复了许多前三个版本发现的bug。在[此处](https://github.com/decred/decred-binaries/releases)获取最新的RC二进制文件（单击`Assets`），并确保对其[进行验证](https://docs.decred.org/advanced/verifying-binaries/)。

感谢每个帮助测试的人让我们史诗般的 v1.6正式版得以尽快发布。

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以构建和运行的源代码中，但对于普通用户来说，还不能使用。

**[dcrd](https://github.com/decred/dcrd)**

去中心化国库支付共识规则已在测试网上[激活](https://twitter.com/degeri_crypto/status/1329980732110819331)，激活过程没有任何问题。

合并到主存储库（朝v1.7迈进）并反向移植到v1.6版本分支：

- 限制内存池不能追踪太多未确认[交易](https://github.com/decred/dcrd/pull/2458)的统计信息。这样可以避免发生复杂性攻击的可能性，并加快了未确认交易的区块模板的生成。
- 更正了RPC命令中的国库投票[状态处理](https://github.com/decred/dcrd/pull/2469)
- 在某些RPC命令的输出中添加了新字段，以指示[国库](https://github.com/decred/dcrd/pull/2470)基础和[国库支出](https://github.com/decred/dcrd/pull/2472)输入（资金来自新国库）并更新了文档
- 修复了在测试网上发现的国库代码中的[同步问题](https://github.com/decred/dcrd/pull/2474)
- 生成RPC证书的默认曲线更改为P-256，因为Chromium（由Decrediton使用）[取消了](https://security.stackexchange.com/questions/100991/why-is-secp521r1-no-longer-supported-in-chrome-others)对更强P-521的支持。

其它合并：

- gencerts工具获得了生成由本地CA证书和密钥签名的证书的功能，这有助于降低配置复杂性
- 固定并发问题
- [rpcserver](https://github.com/decred/dcrd/issues/2069)的更多测试
- 重构数据库[升级](https://github.com/decred/dcrd/pull/2457)逻辑以消除重复数据，并使其更快地编写将来的升级

**[dcrwallet](https://github.com/decred/dcrwallet)**

- 对所有常规发送使用[随机硬币](https://github.com/decred/dcrwallet/pull/1914)选择
- 保存未发布的[VSP费用](https://github.com/decred/dcrwallet/pull/1915)交易，以防止在重新启动钱包期间产生双花
- 沿VSP费用地址请求发送选票的父交易（以更快地注册选票，VSP需要知道选票的输出资金，这通常来自同一区块中开采的“拆分交易”，但并不总是被即时可见） VSP）
- 为了避免在混币帐户中使用未混币的更改，请使用正确的[更改帐户](https://github.com/decred/dcrwallet/pull/1919)支付VSP费用，以防止混币帐户使用未混币的更改（没有隐私泄漏，因为尚未发布混币VSPStaking，solo隐私购票没有这样的问题）
- 最大VSP费用可[配置](https://github.com/decred/dcrwallet/pull/1933)
- bug修复和文档更新

**[Decrediton](https://github.com/decred/decrediton)**

- 更新Trezor[固件](https://github.com/decred/decrediton/pull/2932)（迈向[Trezor买票](https://github.com/decred/decrediton/issues/2681)支持的一步）
- 按照更新的设计，[隐私](https://github.com/decred/decrediton/pull/2987)标签页经过重新[设计](https://github.com/decred/decrediton/issues/2965)以简化操作
- [帮助页面](https://github.com/decred/decrediton/pull/2885)介绍了隐私功能
- 在“隐私”标签页上显示[日志](https://github.com/decred/decrediton/pull/2888)
- 允许从混币账户以外的[其它账户](https://github.com/decred/decrediton/pull/2909)发送交易的能力
- 显示[混合](https://github.com/decred/decrediton/pull/2926)交易的过滤器
- 修复了隐私钱包的[错误](https://github.com/decred/decrediton/pull/2889)
- 根据批准或拒绝状态[过滤](https://github.com/decred/decrediton/pull/2854)完成投票的提案
- 在执行某些操作时不允许[关闭](https://github.com/decred/decrediton/pull/3005)Decrediton
- [AppImage](https://github.com/decred/decrediton/pull/2864)打包，其中Decrediton作为单个可执行文件出现（作为副作用，这使GNOME用户避免了必须通过命令行启动它）
- 删除了[最大钱包](https://github.com/decred/decrediton/pull/2886)数量限制
- 更新[中文](https://github.com/decred/decrediton/pull/2927)翻译
- 增加了阿拉伯语，意大利语和波兰语的部分新[翻译](https://github.com/decred/decrediton/pull/2974)
- 许多UI调整

10月修复了约60个bug，11月修复了约65个bug。Decrediton功能的清单越来越多，需要更多的测试。非常感谢帮助改进Decrediton的所有测试人员！

进行中：

- 迁移到[grpc-js](https://github.com/decred/decrediton/pull/2936)以显着减少构建时间和二进制文件大小
- [入门](https://github.com/decred/decrediton/pull/2659)和[设置](https://github.com/decred/decrediton/pull/2957)页面的自动化测试
- [Trezor](https://github.com/decred/decrediton/pull/2869)上测试网购票

**[Politeia](https://github.com/decred/politeia)**

- 登录时检查[TOTP代码](https://github.com/decred/politeia/pull/1212)（用于2FA的6位数字代码）
- 草稿中的嵌入式[图像](https://github.com/decred/politeiagui/pull/2201)
- 大量[设计修复](https://github.com/decred/politeiagui/pull/2197)
- 使用[cypress](https://www.cypress.io/)进行自动[UI测试](https://github.com/decred/politeiagui/pull/2151)
- bug修复

CMS:

- 跟踪GitHub[开发活动统计信息](https://github.com/decred/politeia/pull/1185)的基础架构，将用于确保开发人员的进度与其计费时间相符
- 发票页面上过去发票和GitHub贡献的统计信息，以帮助管理员进行审阅
- 多种修复

进行中：

- 前端支持[TOTP登录](https://github.com/decred/politeiagui/pull/2127)

**[vspd](https://github.com/decred/vspd)**

- 不拒绝具有[无效](https://github.com/decred/vspd/pull/199)投票选择的选票（这是可取的，这样可以在客户端或服务器不是最新时，不停止票证的注册，在此进行说明）
- 在费用地址请求中接受可选的[父交易](https://github.com/decred/vspd/pull/205)（请参见上面的dcrwallet部分）
- bug修复和代码清除

**[dcrpool](https://github.com/decred/dcrpool)**

- 完成[Postgres](https://github.com/decred/dcrpool/pull/282)实施。现在，所有数据库测试都针对Bolt和Postgres运行。BoltDB由于是嵌入式键/值数据库，因此仅允许部署dcrpool的单个实例。使用Postgres，可以针对同一个Postgres数据库部署多个dcrpool实例。
- 提取[错误](https://github.com/decred/dcrpool/pull/284)包以支持将数据库提取到其自己的包中
- bug修复和代码清除

**[dcrlnd](https://github.com/decred/dcrlnd)**

- 添加了[IPC](https://en.wikipedia.org/wiki/Inter-process_communication) 工具以允许[父进程](https://github.com/decred/dcrlnd/pull/117)（例如Decrediton）控制dcrlnd进程

10月份从上游版本[0.11.1](https://github.com/lightningnetwork/lnd/releases/tag/v0.11.1-beta)移植变更，其中包括对[两个](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002858.html) [漏洞](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002857.html)的修复，这些漏洞可能导致资金损失。发现者的更多背景在[这里](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002859.html)和[这里](https://lists.linuxfoundation.org/pipermail/lightning-dev/2020-October/002855.html)。

建议升级到最新的dcrlnd主或候选[标记](https://github.com/decred/dcrlnd/tags)。

**[dcrdex](https://github.com/decred/dcrdex)**

修补程序[v0.1.3](https://github.com/decred/dcrdex/releases/tag/v0.1.3)已发布，修复了可能的客户端挂起和一些较小的问题。二进制文件作为[v1.6 RC4](https://github.com/decred/decred-binaries/releases/tag/v1.6.0-rc4)的一部分提供。

合并在主存储库中：

- 模态对话框上的[关闭按钮](https://github.com/decred/dcrdex/pull/800)
- 订单明细页上的[确认](https://github.com/decred/dcrdex/pull/805)计数
- [批量](https://github.com/decred/dcrdex/pull/797)赎回交易可能节省一些交易费用
- 订单[撤销](https://github.com/decred/dcrdex/pull/798)时的可见通知
- 更多的图表[交互性](https://github.com/decred/dcrdex/pull/837)（在深度图上突出显示悬停的订单等等）
- TUI[已删除](https://github.com/decred/dcrdex/pull/827) （：终端生命形式滴下了些许泪水：）
- 区块链[同步时](https://github.com/decred/dcrdex/pull/785)不允许交易
- [异步](https://github.com/decred/dcrdex/pull/819)运行合约审核以不阻止传入消息和其他交易活动
- 改善[关机](https://github.com/decred/dcrdex/pull/787)顺序
- 避免钱包[锁定](https://github.com/decred/dcrdex/pull/817)错误
- 优化订单簿的[内存](https://github.com/decred/dcrdex/pull/794)使用
- 新用户和具有良好掉期历史的用户的可配置手数[限制](https://github.com/decred/dcrdex/pull/815)
- 管理功能以检索[市场数据](https://github.com/decred/dcrdex/pull/771)
- 更快，更丰富的[测试工具](https://github.com/decred/dcrdex/pull/820)
- 带有可自定义“程序”的[负载测试](https://github.com/decred/dcrdex/pull/717)机器人，以向系统施加压力
- dexc [Dockerized](https://github.com/decred/dcrdex/pull/836)
- DEX客户端的[RPC协议](https://github.com/decred/dcrdex/pull/702)的规范，以帮助除dexctl之外的其他程序（例如Decrediton）使用DEX客户端
- 修复了几种边缘情况

[合并了](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-11-01..2020-11-30+sort%3Aupdated-asc)来自6个贡献者的37个PR ，添加了7K行代码并删除了4K行代码。

进行中：

- [最大订单](https://github.com/decred/dcrdex/pull/842)估计
- 用户[信誉](https://github.com/decred/dcrdex/pull/848)
- 从数据库[恢复](https://github.com/decred/dcrdex/pull/856)交换
- 市场数据[API端点](https://github.com/decred/dcrdex/pull/796)，以允许第三方和网站从DEX提取数据

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

合并到dcrlibwallet共享库中：

- 能够发送[自定义输入](https://github.com/planetdecred/dcrlibwallet/pull/165)（以支持[硬币控制](https://nopara73.medium.com/coin-control-is-must-learn-if-you-care-about-your-privacy-in-bitcoin-33b9a5f224a2)功能）
- 防止多个钱包使用[同一种子](https://github.com/planetdecred/dcrlibwallet/pull/138)

进行中：

- 显示Politeia [提案](https://github.com/planetdecred/dcrandroid/pull/503)
- [vspd](https://github.com/planetdecred/dcrlibwallet/pull/163)支持

**[dcrios](https://github.com/planetdecred/dcrios)**

- [法语](https://github.com/planetdecred/dcrios/pull/726) 翻译
- bug修复和用户界面调整

进行中：

- Politeia [提案](https://github.com/planetdecred/dcrios/pull/715)
- [隐私](https://github.com/planetdecred/dcrios/pull/727)模式

**[godcr](https://github.com/planetdecred/godcr)**

- [UI大幅修整](https://github.com/planetdecred/godcr/pull/262)

进行中：

- [vspd](https://github.com/planetdecred/godcr/pull/263) 支持
- Politeia [提案](https://github.com/planetdecred/godcr/pull/254)

**[dcrdata](https://github.com/decred/dcrdata)**

- 市场页面的bug修复

**[dcrros](https://github.com/decred/dcrros)**

- 更新为Rosetta spec [v1.4.5](https://github.com/coinbase/rosetta-specifications/releases/tag/v1.4.5)
- 后端的每个服务调用和大多数代码路径的[单元测试](https://github.com/decred/dcrros/pull/9)覆盖率
- 改进了与dcrd的[连接](https://github.com/decred/dcrros/pull/11)处理
- 返回[对等节点列表](https://github.com/decred/dcrros/pull/12)和同步状态
- 使规范要求的构造API方法可用于[脱机](https://github.com/decred/dcrros/pull/13)实例

**[decred.org](https://github.com/decred/dcrweb)**

- 新闻稿转换为[单独的](https://github.com/decred/dcrweb/pull/931)页面
- 内容更新

其它：

- [发布](https://github.com/decred/release) 工具进行了大量升级，自动化发布过程

## 人员

欢迎新到来的首次贡献者，他们的代码已合并到主代码库中： @HlloWrld ([dcrweb](https://github.com/decred/dcrweb/commits?author=HlloWrld)).

截至12月1日的社区统计数据：

- Twitter 粉丝: 40,897 (+79)
- Reddit 订阅: 9,982 (+45)
- Matrix #general 用户: 253 (+31)
- Discord 用户: 1,501
- Telegram 用户: 2,339 (-55)
- YouTube 订阅: 4,250 (+40), 观看量: 162K (+3K)
- LinkedIn 粉丝: 932 (+8)
- GitHub dcrd 星: 567 (+1), 叉: 246 (+0)

## 治理

十月[国库](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到11975 DCR，花费13846 DCR。按照9月份的每日平均DCR/USD汇率18.19美元计算，这是21.8万美元的收入和25.2万美元的支出。按10月平均汇率12.01美元计算，当月完成工程的美元账单金额为16.6万美元。截至12月4日，社区开发基金余额为636385 DCR（1640万美元，25.69美元）。

10月发布了4项建议，其中3项已被批准，1项已被放弃。

- GoDCR [proposal](https://proposals.decred.org/proposals/e5c8051) from @raedah requested a budget of $60K to further develop (8 months) a Go-native desktop wallet using [Gio](https://gioui.org/) library. This proposal includes a $1,000/month sponsorship of Gio, for which GoDCR has become a pioneering project. Approved with 92% support and 38% turnout.
- A related mobile wallets [proposal](https://proposals.decred.org/proposals/bc499c9) from @raedah requested $44K for a further 8 months of work on the Android and iOS wallets. Both mobile wallets and GoDCR share the [dcrlibwallet](https://github.com/planetdecred/dcrlibwallet) component, which allows all three to access new features added to it. Approved with 93% support and 38% turnout.
- A [proposal](https://proposals.decred.org/proposals/3943bff) from @joegruff to further develop a Decred Address Scanner Android app requested $3,000 for work already completed (app has been open source and in the Google Play store for a year) and $6,000 maximum for necessary updates and new features. By popular demand in comments Joe [agreed](https://proposals.decred.org/proposals/3943bff/comments/15) to add compact filters support to improve privacy, and even work voluntarily if needed (because it was too late to edit the proposal with this feature). The vote was tense as the support stayed [below](https://explorer.dcrdata.org/proposal/decred-address-scanner) 60% most of the time, but eventually the proposal was approved with 67% support and 34% turnout.
- A [proposal](https://proposals.decred.org/proposals/8a09324) from @paris\_smithson to fund artwork production and marketing for [WhyDecred.com](https://www.whydecred.com/) originally requested $16,800 to fund 16 artworks, was edited to drop the request by $10K (to $6,800), before ultimately being abandoned with the idea that the site will be completed before another proposal is submitted.

Politeia Digest [issue 39](https://blockcommons.red/politeia-digest/issue039/) has more details on the month's proposals.

[decredcommunity/proposals](https://github.com/decredcommunity/proposals) repository has been reorganized for consistent structure. The repo currently holds 52 updates for 13 proposals. Please submit updates for your proposals as it helps to collect them in one place (vs searching across chats and Reddit) and protect from loss. _(summon @bee if you don't want to face GitHub alone)_

## 网络

Hashrate: November's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kgw9asu9-ki79jtll&scale=linear&bin=block&axis=time) opened at ~226 Ph/s and closed ~293 Ph/s, bottoming at 215 Ph/s and peaking at 566 Ph/s throughout the month. Pool hashrate [distribution](https://miningpoolstats.stream/decred) as of Dec 1: UUPool 44%, Poolin 35%, easy2mine 13%, Huobipool 2.6%, Antpool 2%, F2Pool 1.6%, BTC.com 1.2%, Luxor 1%, CoinMine 0.02%.

Staking: [30-day average](https://dcrstats.com/) ticket price was 158.66 DCR (+6.96). The [price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kgw9asu9-ki79jtll&bin=window&axis=time&visibility=true-false&mode=stepped) varied between 139.3-188.9 DCR. [Locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kgw9asu9-ki79jtll&scale=linear&bin=block&axis=time) was 6.09-6.61 million DCR, which corresponded to 49.88-53.64% of the available supply [participating](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kgw9asu9-ki79jtll&scale=linear&bin=block&axis=time) in PoS.

The ticket price once again reached new high of 188.85 DCR while stake participation (DCR locked in tickets) has hit an _all-time high_ of 53.6%.

Nodes: Throughout [November](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1604188800000&to=1606780800000) there was an average of 114 public listening nodes and 166 total nodes per dcr.farm. Average version distribution for November: 28% dcrd v1.5.2, 20% dcrd v1.5.1, 13% dcrd v1.6 dev builds, 5% dcrd v1.5.0, 3.4% dcrd v1.7 dev builds, 3% dcrd v1.5 dev and RC builds, 1.1% dcrd v1.4, 12% dcrwallet v1.5.1, 2.5% dcrwallet v1.6 dev and RC builds, 1.3% dcrwallet v1.5, 0.8% dcrwallet v1.4, 9% others.

In other news:

- Decred network has processed [500,000](https://twitter.com/decredproject/status/1324674240268898304) blocks!
- there's a [new](https://twitter.com/CoinShuffle_BOT/status/1324444980308594689) [@CoinShuffle_BOT](https://twitter.com/CoinShuffle_BOT) account that tweets Decred's daily mixing stats
- wealth distribution [study](https://coinmetrics.io/bitcoin-an-unprecedented-experiment-in-fair-distribution/) by Coin Metrics has found that Decred is second after Bitcoin by their Network Distribution Factor metric (note: NDF is based on addresses and many addresses may be controlled by the same person, discussion [here](https://www.reddit.com/r/decred/comments/jrsrbk/network_distribution_factor_ndf_btc_has_the/))

## 整合

Welcome the new [vsp.decredcommunity.org](https://vsp.decredcommunity.org/) service that is running a mainnet instance of the new vspd software. As of writing it has ~70 live and ~30 voted tickets.

Existing providers [decredbrasil.com](https://vspd.decredbrasil.com/), [99split.com](https://vspd.99split.com/), and [stakeminer.com](https://vsp.stakeminer.com/) have all launched vspd instances in addition to their existing dcrstakepool servers listed at [decred.org/vsp](https://decred.org/vsp/).

As of writing we have a total of 5 mainnet vspd services to choose from. Thank you all for supporting [a more private](https://blog.decred.org/2020/06/02/A-More-Private-Way-to-Stake/) way to stake.

[Stakey.net](https://stakey.net/) VSP is now posting status and support updates on [Mastodon](https://citadel.stakey.net/@support).

Staked [announced](https://twitter.com/staked_us/status/1329173484598124546) the closure of their Decred VSP for lack of economic viability. As of Dec 8, Decred is still featured on the [site](https://staked.us/) and VSP [stats](https://decred.staked.us/stats) page shows 133 active users, 308 total users and 31 live tickets.

Hotbit Korea [announced](https://twitter.com/Hotbit_Korea/status/1331412789416534017) that they would list DCR/KRW market on Nov 26.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## 采用

dcrtime was [used](https://twitter.com/Decred_BR/status/1328848031832215553) by VotoLegal to record and timestamp donations to Brazil's 2020 municipal elections campaign. According to [Geek Insider](https://geekinsider.com/decred-blockchain-for-brazil-municipal-elections/), more than 24K donations have been tracked totalling more than $600K as of Nov 19. ([discussion](https://www.reddit.com/r/decred/comments/jw4l9o/decred_blockchain_used_in_brazil_election/))

## 外展活动

To address the longstanding challenge of [spreading content and news](https://www.reddit.com/r/decred/comments/jz0bq1/decred_skepticism_sunday_22_november_2020/gd9auhx/), @Exitus and others have assembled a Marketing Workgroup in Telegram to help coordinate:

> Thus far, it has proven to be a productive and a positive force. If anyone would like to participate and add value, please DM me.

Mastodon server launched by Stakey.net VSP for their [support](https://citadel.stakey.net/@support) account is open to the Decred community via this [invite link](https://citadel.stakey.net/invite/tZ2Cm5FX). [Mastodon](https://docs.joinmastodon.org/) is an open-source, self-hosted microblogging alternative to Twitter and is part of the [Fediverse](https://en.wikipedia.org/wiki/Fediverse).

Decred is now listed as a sponsor at [gioui.org](https://gioui.org/).

Decred in Spanish published 5th monthly [report](https://github.com/decredcommunity/proposals/blob/master/proposals/3c02b67/updates/20201120.md) of activities and expenses for their second proposal that is ending in December. A big final [report](https://github.com/DecredES/Monthly_reports/blob/master/Final_Report_June_December_2020.md) covering June-December was published together with the [3rd proposal](https://proposals.decred.org/proposals/350f64b) to continue the effort.

Blockchain Learning Challenge (co-organized by Decred in Spanish and Talent Land Network) had 6 projects that made it to the finals. Participants published source code on GitHub and presented their projects in short video pitches. 5 judges have rated each project in 5 areas (how much data was used and how, how original and relevant for Decred the idea is, how easy it is to use the app, how finished the app is, and how well things are documented). Summary of the finals with all ratings and links is [here](https://github.com/DecredES/Challenge/blob/main/Proyectos-Finalistas.md), and the final award video is [here](https://www.youtube.com/watch?v=CQTitBVUMMY).

@michae2xl published a [report](https://github.com/decredcommunity/proposals/blob/master/proposals/bc20f98/updates/20201203.md) of his November activities for the Brazil Marketing proposal.

Monde PR's achievements for November:

- created and pitched one story idea to finance and crypto publications
- responded to 3 requests for comments
- secured 2 media interviews

News coverage secured by Monde PR:

- @richardred appeared on the [Hitechies podcast](https://www.hitechies.com/richard-red-at-decred-talks-to-pramod-dhakal/) talking about decentralization and the future of DeFi
- @jy-p appeared on the [Crypto Conversation podcast](https://bravenewcoin.com/insights/podcasts/how-the-decred-dex-plans-to-disrupt-the-crypto-exchange-market) talking about the DCRDEX launch
- an article in [Crypto Briefing](https://cryptobriefing.com/politicians-brazil-use-decred-record-political-donations/) featuring commentary from @jy-p on Decred's use in Brazil's election, syndicated to 6 news outlets including [Coin Market Cap](https://coinmarketcap.com/fr/headlines/news/politicians-brazil-use-decred-record-political-donations/)
- an article in [Cryptonomist](https://en.cryptonomist.ch/2020/11/19/elections-in-brazil-donations-on-blockchain/) featuring commentary from @jy-p on Decred's use in Brazil's election, syndicated to 3 news outlets including [Bitcoin Ethereum News](https://ms.bitcoinethereumnews.com/blockchain/elections-in-brazil-donations-on-blockchain-the-cryptonomist/)
- an article in [Geek Insider](https://geekinsider.com/decred-blockchain-for-brazil-municipal-elections/) featuring commentary from @jy-p on Decred's use in Brazil's election
- an article in [Blockchain Latino America](https://blockchainlatinoamerica.com/blockchain/blockchain-para-donaciones-transparentes/) featuring commentary from @jy-p on Decred's use in Brazil's election
- an article in [Explica.co](https://www.explica.co/ripples-waves-and-xrp-ahead-on-weekly-top-with-more-than-50-hikes/) about Decred's use in Brazilian election
- an article in [Cointelegraph](https://cointelegraph.com/news/friendliest-of-them-all-these-could-be-the-best-countries-for-crypto) featuring commentary from @jy-p on the U.S. being the most crypto-friendly country, syndicated to 33 news outlets including [Cointelegraph Italy](https://it.cointelegraph.com/news/friendliest-of-them-all-these-could-be-the-best-countries-for-crypto) and [Investing.com](https://www.investing.com/news/cryptocurrency-news/friendliest-of-them-all-these-could-be-the-best-countries-for-crypto-2353744)
- an article in [Master of Nodes](https://mastersofnodes.com/decred-blockchain-system-implemented-in-brazil-municipal-elections) featuring commentary from @jy-p on Decred's use in Brazil's election
- @lukebp appeared on the [Digital Cash Network podcast](https://odysee.com/@DigitalCashNetwork:c/Decred:6) talking about Decred's governance model
- an article in [Cointelegraph](https://cointelegraph.com/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles) featuring commentary from @jy-p on Bitcoin's bull and bear cycles, syndicated to 17 news outlets including [Cointelegraph Germany](https://de.cointelegraph.com/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles), [Cointelegraph Brazil](https://cointelegraph.com.br/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles) and [Cointelegraph Italy](https://it.cointelegraph.com/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles)

## 活动

Attended:

- Nov 2 - [Blockchain Summit Latam](https://www.blockchainsummit.la/) - Internet. @elian gave a talk "Governance in public protocols" about the similarities and differences between several public blockchains and how does Decred stand out from these. ([video](https://www.youtube.com/watch?v=SiMoxHS8AAk&list=PLiJAJqCfjxwIR6q1W0bidE9W4369KMjzz))
- Nov 5 - [Hablemos Decred 20](https://twitter.com/Decred_ES/status/1323671501212684288) - Internet. @elian and Fernando Quiros of Cointelegraph in Spanish talked about the possible use cases for blockchain technology and cryptocurrencies in the context of journalism, communication and advertising. ([video](https://www.youtube.com/watch?v=V1tl600djBA))
- Nov 9 - [Talent Land Latinoamerica](https://www.talentland.talent-republic.tv/) - Internet. @adcade, @elian, @francov\_ and @pablito talked about "Our money, our rules: Leaving behind the national currencies". ([video](https://www.youtube.com/watch?v=B0tEYQ2l_RM))
- Nov 12 - [Hablemos Decred 21](https://twitter.com/Decred_ES/status/1326279642169348096) - Internet. Joined by guest Cristobal Pereira (CEO LatAmTech) to recap Blockchain Summit Latam and discuss perspectives for the Latam ecosystem. ([video](https://www.youtube.com/watch?v=sTaghDgY5k8))
- Nov 19 - [Hablemos Decred 22](https://twitter.com/Decred_ES/status/1328819770876162049) - Internet. Joined by guest Joaquin Moreno to discuss the topic "Companies buying Bitcoin, are you ready?". ([video](https://www.youtube.com/watch?v=N2hxP8I6hbM))
- Nov 19 - [University of El Salvador](https://twitter.com/addcade/status/1329605293081288709) - Internet. @adcade talked to students of the economics faculty about cryptocurrencies, Decred, governance and contribution opportunities. It was a 2 hour conference with 77 people, extended to +1 hour with ~45 people.
- Nov 27 - [Hablemos Decred 23](https://twitter.com/Decred_ES/status/1331372082354130946) - Internet. Joined by @caibarrad from Decred in Spanish and guest Felipe Montoya to discuss similarities and differences between "DLTs" and crypto. ([video](https://www.youtube.com/watch?v=tu5OqKQhSbk))
- Nov 28 - [Partnership agreement with OMJD](https://decredcommunity.github.io/events/index/20201128.1) - Casablanca, Morocco. Following an online meetup with The Moroccan Organization of Young Decision Makers (OMJD) in July, @arij signed a 2-year agreement with them in order to hold meetups, workshops and conferences about Decred and blockchain technology for the benefit of the young.

Spanish Decred events keep getting announcements at [Cointelegraph in Spanish](https://es.cointelegraph.com/tags/decred).

Our [events repository](https://github.com/decredcommunity/events) that serves as a master source for event data above was upgraded with new "tech". Now key info about events is saved in (mostly human-readable) [YAML files](https://github.com/decredcommunity/events/tree/master/index), and requires writing less prose than full [reports](https://github.com/decredcommunity/events/tree/master/reports). Such structure allows us to generate a [pretty website](https://decredcommunity.github.io/events/index/) where each event gets a nice link with everything about it. This should help with reporting and knowledge sharing. To get your event listed please follow [these steps](https://github.com/decredcommunity/events/blob/master/docs/submit-index.md).

## 媒体

Selected articles:

- Polkadot governance overview by @richardred ([blockcommons.red](https://blockcommons.red/crypto-governance-research/overviews/polkadot/))
- Uniswap/SushiSwap governance overview by @richardred ([blockcommons.red](https://blockcommons.red/crypto-governance-research/overviews/uniswap/))

Videos:

- Decred bi-weekly news update - New 1.6 release is inbound & DEX is live! by @Exitus ([youtube](https://www.youtube.com/watch?v=mYfOr4e9MZ8))
- Decred bi-weekly news update - Development progress, staking participation all-time high - and more! by @Exitus ([youtube](https://www.youtube.com/watch?v=13YGyb27z5E))
- Decred - The hybrid blockchain by Decred Society ([youtube](https://www.youtube.com/watch?v=dszDzH0OlEo))
- Luke Powell on Decred governance, hybrid consensus, and new decentralized treasury on the Digital Cash Network ([youtube](https://www.youtube.com/watch?v=4_EafyDcJvk), [odysee.com](https://odysee.com/@DigitalCashNetwork:c/Decred:6), [anchor.fm](https://anchor.fm/digitalcashnetwork))
- Interview with Permabull Niño (@PermabullNino) by Staked Podcast ([youtube](https://www.youtube.com/watch?v=nRryWFk_l7k))
- Interview with Le\_Hibou\_ (@Frenchy\_LeDegen) by Staked Podcast ([youtube](https://www.youtube.com/watch?v=N5BnEB6MDLs))
- Interview with L.O.L. DEFI (@loldefi) by Staked Podcast ([youtube](https://www.youtube.com/watch?v=eqpafR0E1SA))
- Crypto Convo - Eduardo Lima of the Staked Podcast feat. DubDigital ([youtube](https://www.youtube.com/watch?v=ErezLZ-SG5o))

Audio-only version of Staked Podcast is available on [anchor.fm](https://anchor.fm/staked-podcast). Congrats on hitting [1,000](https://twitter.com/stakedpodcast/status/1326856050465792008) downloads/streams!

Audio:

- Hitechies Podcast - Richard Red and Pramod Dhakalrr talk about DeFi challenges, ETH, banking industry, future of payment systems and more. ([hitechies.com](https://www.hitechies.com/richard-red-at-decred-talks-to-pramod-dhakal/))
- Crypto Conversation 074 - How the Decred DEX plans to disrupt the crypto exchange market with @jy-p ([bravenewcoin.com](https://bravenewcoin.com/insights/podcasts/how-the-decred-dex-plans-to-disrupt-the-crypto-exchange-market), [youtube](https://www.youtube.com/watch?v=i3LQza2sYNQ))
- Decred in Depth 33: Seth Simmons on DCR + Monero privacy ([libsyn](https://decredindepth.libsyn.com/seth-simmons-dcr-monero-privacy))
- Rough Consensus 12: Bitcoin has entered the China shop. The lads are joined by @ck\_SNARKs, co-host of @POVCryptoPod and Bitcoin Magazine, to discuss Bitcoin adoption, lessons from altcoin boom and bust cycles, the role of price within the cryptocurrency space, and more. ([libsyn](https://roughconsensus.libsyn.com/episode-12-bitcoin-has-entered-the-china-shop-w-ck_snarks))
- Rough Consensus 13: Digital autonomy and freedom. The spidermen are joined by Frank Braun (@thefrankbraun) in a wide ranging conversation covering: cypherpunk digital societies, privacy and freedom in the digital age, role of BTC, DCR, Scrit and others in a brighter future. ([libsyn](https://roughconsensus.libsyn.com/episode-13-digital-autonomy-and-freedom-with-frank-braun))

Art and memes:

- Decred DAO space invitation [poster](https://twitter.com/coveryfire7777/status/1324430999212744704) by @Exitus
- [Swiss Army Knife](https://twitter.com/_Checkmatey_/status/1324835192100413441) of sound money by @Checkmate
- [Hidden Hydra](https://twitter.com/New_Copernicus/status/1333518011861372928) teaser clip by @New\_Copernicus
- check out OfficialCrypto's merch designs at [Redbubble](https://officialcryptos.redbubble.com/) _(did you know Decred logo matches perfectly to "[Real Defi](https://twitter.com/OfficialCryptos/status/1325421754777526272)")_?

Translations:

- How I learned to stop worrying and love the Decred DEX - [in Spanish](https://medium.com/decred-es/c%C3%B3mo-aprend%C3%AD-a-dejar-de-preocuparme-y-amar-el-dcrdex-74e4ecf7bf70) by @francov\_
- Monero and Decred are the new Bitcoin - [in Spanish](https://github.com/DecredES/traducciones/blob/master/Monero-y-Decred-son-el-nuevo-Bitcoin.md) by @francov\_
- Utility of cryptoassets - [in Spanish](https://github.com/DecredES/traducciones/blob/master/La-utilidad-de-los-criptoactivos.md) by @francov\_
- Decred Journal October 2020 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), Spanish (@francov\_) and Vietnamese (@duyenemdo). Vietnamese readers can also catch up on August events. Thank you all for your continued work!
- If you translate Decred content, come say hi in the [#translations](https://chat.decred.org/#/room/#translations:decred.org) chat room.

## 社区讨论

Selected Reddit posts:

- Forward Thinking _Saturday_ Nov 14 started with the suggestion to pick "Decred is being repriced" as the new [narrative](https://www.reddit.com/r/decred/comments/jtx4y2/forward_thinkingsaturday_14_november/)
- creating [multisig](https://www.reddit.com/r/decred/comments/jvhxea/how_to_create_a_decred_multisig_wallet/) addresses
- a collection of original [marketing ideas](https://www.reddit.com/r/decred/comments/jx989d/tiny_marketing_ideas/) by u/oiezz and others
- why [obfuscating](https://www.reddit.com/r/decred/comments/k39r3v/not_showing_result_of_a_votation_before_it_ends/) votes is a bad idea
- applicability of higher-level [script languages](https://www.reddit.com/r/decred/comments/k3ioxi/how_feasible_is_to_implement_a_scripting_language/) like Miniscript, Minsc or RGB to Decred

Selected Twitter discussions:

- @PermabullNino's diagram of [value flows](https://twitter.com/PermabullNino/status/1323330573444632576) on dcrdex shows why injecting a token into the trade process is not necessary
- @withdecred's fact-packed Decred pitch [thread](https://twitter.com/withdecred/status/1325147231935098880)

## 市场

11月DCR美元交易价格在11.71-24.78 USD / BTC交易价格 0.00086-0.00135之间。每日平均价格为$18.19。

TIE已证明DCR/USD[攀升](https://twitter.com/TheTIEIO/status/1334586246606319623)与30天平均推文量之间存在相关性。

在币安上[观察到](https://twitter.com/Mr_DEX89/status/1326602830053068802)一个奇怪的恐慌峰值，降至0.00075 BTC 。

11月12日，@ jy-p [说到](https://matrix.to/#/!mlRZqBtfWHrcmgdTWB:decred.org/$ZPdL5sG-IwT034pc7FldzbijUOjAe3u0ja1OkcabU_g)DEX总共交易了191K DCR。平均每天10 BTC。

那些希望在不安装任何内容的情况下窥视DCRDEX的人可以查看YouTube上的24/7[直播](https://www.youtube.com/channel/UCSxEsULY1DUBsjdkZTbkKRA)。

## 相关外部信息

发现从根本上破坏了BSV Electrum钱包中P2SH的替代物，使任何人都可以将Bs链上以多重签名哈希保存的硬币花费掉。

Value DeFi协议被黑客盗取了700万美元，尽管攻击者出于未知原因将200万美元退还给了合同地址。该漏洞利用Flash借贷执行，在Value DeFi发推文（现已删除）不到24小时后，吹嘘“ Flash借贷攻击预防”的强大安全性。

OUSD稳定币遭到一笔用于进行再入攻击的快速贷款的黑客攻击，以打印和重置（降级）几乎相当于整个流通供应量的OUSD，从而使黑客能够提取700万美元的价值。

通过借入价值700万美元的MKR代币并在立即还清贷款之前对其进行投票，还利用了一笔快速贷款来开发MakerDAO的治理系统。MakerDAO的响应是禁用某些执行功能，以防攻击者能够访问它们，并延长冷静期，在此期间，社区可以应对意外的建议通过。如果要求MKR持有者锁定令牌一段时间以进行投票-或可借用的MKR数量少于合法参与治理系统的数量，则不会暴露这种弱点。

Schnorr签名和Taproot的软叉实现在10月被合并到Bitcoin Core，但是到目前为止，在网络上激活更改的方法尚未达成协议。还有一个不受欢迎的论点，即Taproot通过引入另一种地址方案，将使普通用户的比特币隐私状况更加恶化。Taproot将添加新的Schnorr签名类型，这将为多签名钱包提供更大的灵活性，并使这些交易看起来与常规交易相同。

以太坊2.0信标链存款合同于11月初发布，并于11月24日达到了目标540,000 ETH，最终的150,000 ETH将在12月1日启动截止日期前的几个小时内到来。信标链是启动和迁移到以太坊2.0的四个阶段中的第一阶段，以这种初始形式，链的唯一目的是确保PoS验证程序可以保持共识。

最新的Bitcoin Cash硬分叉发生在11月，这次争议的焦点是为ABC开发人员筹集资金。这场哈希战争显然是赢家，BCHN链（无开发资金）吸引了几乎所有的采矿能力。在分叉之前，观察到超过100万个生物安全信息交换所正在转移到交易所（出售有风险的资产和接收拆分硬币是这样做的两个常见原因）。

以太坊网络在11月11日经历了一次中断。最新版本的Geth节点软件默默地修复了一个休眠状态已超过一年的共识错误。由于更改了共识代码，因此存在意外硬分叉的风险。一家供应商独立发现了该错误，并看到大多数节点已升级，因此决定在生产中对其进行测试。看看会发生什么。令所有人惊讶的是，运行旧软件的少数节点中有Infura，Infura是流行的服务提供商，被“ dapps”用来与以太坊网络同步。触发漏洞的交易使Infura和依赖它的一堆“去中心化”财务应用程序停止了运行，包括Metamask，MakerDAO，Uniswap，Compound等。币安和其他交易所在注意到相互矛盾的交易历史后也暂停了交易。Infura在几个小时内解决了该问题，并发布了验尸报告，解释了为何不进行升级，并指出了无提示共识修复的危险。以太坊开发人员还发布了验尸报告对盖斯（Geth）的解释是，该修复程序是静默完成的，不会引起攻击者的不必要关注。除其他事项外，该事件还告诉我们，部署关键修复程序具有挑战性，因为这是在告知好角色而不通知坏角色之间的权衡。

阿拉贡项目是在过程退役记号的引入一年前的令牌“阿拉贡苑”，阿拉贡DAO的争议解决服务使用ANJ的。现在，ANJ代币被视为Aragon Court成功的障碍，将由ANT持有者通过向ANJ持有者发行约1-5％的通货膨胀而被买断。

美国当局没收了价值约10亿美元的69,370 BTC（和叉子），显然是在2013年从丝路窃取资金的一位不愿透露姓名的黑客的同意下进行的。

## 关于月报

这是Decred Journal的第32期。有关所有问题，镜像和翻译的索引，请参见[这里](https://xaur.github.io/decred-news/)。

在经过最少的健全性检查之后，来自第三方的大多数信息都会直接从来源中继。Decred Journal的作者无权验证所有声明。请当心诈骗，并自行进行调查。

您可以在[此处](https://github.com/xaur/decred-news/labels/next%20release)提交内容，以供撰写下一期月报内容。我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢 (字母排列):

- 写作和编辑:  adcade, bee, degeri, elian, l1ndseymm, richardred
- 评论和反馈: davecgh, dnldd, jholdstock, JoeGruff, lukebp
- 封面图片: saender
- 资助： Decred国库

## 中文社区

* [社区网址](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [bilibili频道](https://space.bilibili.com/425519478)
* QQ群号-258412796
