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

- 来自@raedah的GoDCR[提案](https://proposals.decred.org/proposals/e5c8051)要求预算为6万美元，以使用[Gio](https://gioui.org/)库进一步开发（8个月）Go-native桌面钱包。该提案包括每月$ 1,000的Gio赞助，GoDCR已成为该项目的先驱。批准获得92％的支持和38％的投票率。
- @raedah提出的相关移动钱包[提案](https://proposals.decred.org/proposals/bc499c9)要求$ 44K，用于在Android和iOS钱包上再工作8个月。移动钱包和GoDCR都共享[dcrlibwallet](https://github.com/planetdecred/dcrlibwallet)组件，该组件允许所有三个组件访问添加到该组件的新功能。获得93％的支持和38％的投票率。
- 一个[提案](https://proposals.decred.org/proposals/3943bff)来自@joegruff进一步制定Decred地址扫描Android应用程序请求已经完成的工作，$ 3,000（应用程序已经开源，并在谷歌Play商店一年）和$ 6000名最大的必要的更新和新功能。出于评论的普遍需求，Joe同意添加紧凑的过滤器支持以提高隐私性，甚至在需要时可以自愿工作（因为使用此功能编辑提案为时已晚）。投票很紧张，因为大多数情况下支持率保持在60％以下，但最终提案以67％的支持和34％的投票率获得批准。
- 一个[提案](https://proposals.decred.org/proposals/8a09324)来自@paris_smithson到基金的艺术品的生产和销售为WhyDecred.com最初请求$ 16,800到基金16件作品，被编辑由$ 10K（至$ 6,800个），前最终被抛弃的想法，该网站将完成下降请求在提交另一个提案之前。

《Politeia Digest》[第39期](https://blockcommons.red/politeia-digest/issue039/)提供了有关本月提案的更多详细信息。

[decredcommunity/proposals](https://github.com/decredcommunity/proposals)存储库已经过重组，以保持结构的一致性。回购协议当前包含13个投标的52个更新。请提交建议，因为它有助于将建议收集到一个地方（与在聊天室和Reddit中进行搜索相比）并防止丢失。（如果您不想独自面对GitHub，请召唤@bee）

## 网络

全网算力: 11月[哈希率](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kgw9asu9-ki79jtll&scale=linear&bin=block&axis=time) 以226 Ph/s开启并以 293 Ph/s结束。月内，最低为215 Ph/s，峰值为566 Ph/s。[哈希率分布](https://miningpoolstats.stream/decred) 截至11月1日：UUPool 44%, Poolin 35%, easy2mine 13%, Huobipool 2.6%, Antpool 2%, F2Pool 1.6%, BTC.com 1.2%, Luxor 1%, CoinMine 0.02%.

Staking: [30天平均票价](https://dcrstats.com/)为 158.66 DCR (+6.96). [票价](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kgw9asu9-ki79jtll&bin=window&axis=time&visibility=true-false&mode=stepped)139.3-188.9 DCR之间变化。[锁定金额](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kgw9asu9-ki79jtll&scale=linear&bin=block&axis=time)为609-661万DCR，相当于参与PoS的可用供应量的49.88-53.64%。

选票价格再次达到188.85 DCR的新高，而Staking参与（DCR锁定在门票中）达到了历史新高53.6％。

节点: 整个[11月](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1604188800000&to=1606780800000)份，每个dcr.farm平均有114个公共侦听节点，总共166个节点。11月的平均版本分布：dcrd v1.5.2、28％dcrd v1.5.1、13％dcrd v1.6开发版本，5％dcrd v1.5.0、3.4％dcrd v1.7开发版本，3％dcrd v1。 5个开发和RC版本，1.1％dcrd v1.4、12％dcrwallet v1.5.1、2.5％dcrwallet v1.6开发和RC版本，1.3％dcrwallet v1.5、0.8％dcrwallet v1.4、9％其他。

其它新闻中：

- Decred网络已处理了[500,000](https://twitter.com/decredproject/status/1324674240268898304)个区块！
- 有一个[新的](https://twitter.com/CoinShuffle_BOT/status/1324444980308594689) [@CoinShuffle_BOT](https://twitter.com/CoinShuffle_BOT)帐户通报Decred的每日混币统计信息
- Coin Metrics的财富分布[研究](https://coinmetrics.io/bitcoin-an-unprecedented-experiment-in-fair-distribution/)发现，按其网络分布因子度量，Decred在比特币之后仅次于比特币（注意：NDF基于地址，许多地址可能由同一个人控制，请在[此处](https://www.reddit.com/r/decred/comments/jrsrbk/network_distribution_factor_ndf_btc_has_the/)进行讨论）

## 整合

欢迎新[vsp.decredcommunity.org](https://vsp.decredcommunity.org/)运行新VSPD软件的主网选票托管服务。在撰写本文时，它有70张现场选票和30张已投票的票。

现有提供商 [decredbrasil.com](https://vspd.decredbrasil.com/), [99split.com](https://vspd.99split.com/), 和 [stakeminer.com](https://vsp.stakeminer.com/)除了在[decred.org/vsp](https://decred.org/vsp/) 中列出的现有dcrstakepool服务器之外，还都启动了vspd实例。

在撰写本文时，我们总共有5种主网vspd服务可供选择。谢谢大家支持以[更私密](https://blog.decred.org/2020/06/02/A-More-Private-Way-to-Stake/)的方式进行抵押。

[Stakey.net](https://stakey.net/) VSP现在在[Mastodon](https://citadel.stakey.net/@support)上发布状态和支持更新。

Staked[宣布](https://twitter.com/staked_us/status/1329173484598124546)其Decred VSP的关闭缺乏经济可行性。截至12月8日，该网站上仍显示Decred ，VSP的统计信息页面显示133个活跃用户，308个总用户和31张实时门票。

Hotbit Korea[宣布](https://twitter.com/Hotbit_Korea/status/1331412789416534017)将于11月26日在DCR / KRW市场上市。

警告：Decred Journal的作者不了解上述任何服务的可信赖性。在将您的个人信息或资产信任给任何实体之前，请先进行自己的研究。

## 采用

VotoLegal使用dcrtime记录并为巴西2020年市政选举活动捐赠。据[Geek Insider](https://geekinsider.com/decred-blockchain-for-brazil-municipal-elections/)，超过24K的捐款已追踪总额超过$ 600K

## 外展活动

为了应对[传播内容和新闻](https://www.reddit.com/r/decred/comments/jz0bq1/decred_skepticism_sunday_22_november_2020/gd9auhx/)的长期挑战，@ Exitus和其他人已经在Telegram中组建了一个营销工作组来帮助协调：

> 迄今为止，已证明这是一种生产力和积极力量。如果有人想参与并增加价值，请与我联系。

Stakey.net VSP为[支持](https://citadel.stakey.net/@support)帐户启动的Mastodon服务器通过[此邀请链接](https://citadel.stakey.net/invite/tZ2Cm5FX)向Decred社区开放。[Mastodon](https://docs.joinmastodon.org/)是Twitter的一种开源，自托管的微博替代品，并且是[Fediverse](https://en.wikipedia.org/wiki/Fediverse)的一部分。

Decred现在在[gioui.org](https://gioui.org/)上被列为赞助商。

以西班牙语发表的第二份提案的活动和费用第5个月度[报告](https://github.com/decredcommunity/proposals/blob/master/proposals/3c02b67/updates/20201120.md)已于12月结束。出版了一份涵盖6月至12月的重大最终报告以及[第3项提案](https://proposals.decred.org/proposals/350f64b)，以继续努力。

区块链学习挑战赛（由Decred在西班牙和Talent Land Network共同组织）有6个项目进入了决赛。参与者在GitHub上发布了源代码，并以简短的视频演示了他们的项目。5名法官对5个领域的每个项目进行了评分（使用了多少数据，如何使用Decred创意，与创意相关性如何，使用该应用程序有多容易，该应用程序的完成程度如何，以及文件的记录情况如何） 。决赛的摘要和所有的评分和链接都在[这里](https://github.com/DecredES/Challenge/blob/main/Proyectos-Finalistas.md)，最终的颁奖视频在[这里](https://www.youtube.com/watch?v=CQTitBVUMMY)。

@ michae2xl发布了他11月份针对“巴西营销”提案的活动的[报告](https://github.com/decredcommunity/proposals/blob/master/proposals/bc20f98/updates/20201203.md)。

Monde PR 11月份的成就：

- 创建并提出了一个故事的想法，以资助和加密出版物
- 回应了3条评论
- 获得2次媒体采访

Monde PR保证的新闻报道：

- @richardred出现在[Hitechies播客](https://www.hitechies.com/richard-red-at-decred-talks-to-pramod-dhakal/)中，谈论去中心化和DeFi的未来
- @ jy-p出现在[加密对话播客](https://bravenewcoin.com/insights/podcasts/how-the-decred-dex-plans-to-disrupt-the-crypto-exchange-market)中，谈论DCRDEX的发布
- [Crypto Briefing](https://cryptobriefing.com/politicians-brazil-use-decred-record-political-donations/)中的一篇文章，重点介绍了@ jy-p对Decred在巴西大选中的使用的评论，并联合了6个新闻媒体，包括Coin Market Cap
- [Cryptonomist](https://en.cryptonomist.ch/2020/11/19/elections-in-brazil-donations-on-blockchain/)中的一篇文章，重点介绍@ jy-p对Decred在巴西大选中的使用的评论，并联合了3个新闻媒体，包括[比特币以太坊新闻](https://ms.bitcoinethereumnews.com/blockchain/elections-in-brazil-donations-on-blockchain-the-cryptonomist/
- [Geek Insider](https://geekinsider.com/decred-blockchain-for-brazil-municipal-elections/)中的一篇文章，重点介绍@ jy-p对Decred在巴西大选中的使用的评论
- [Blockchain Latino America](https://blockchainlatinoamerica.com/blockchain/blockchain-para-donaciones-transparentes/)上的一篇文章，重点介绍@ jy-p对Decred在巴西大选中的使用的评论
- [Explica.co](https://www.explica.co/ripples-waves-and-xrp-ahead-on-weekly-top-with-more-than-50-hikes/)中有关Decred在巴西大选中使用的文章
- [Cointelegraph](https://cointelegraph.com/news/friendliest-of-them-all-these-could-be-the-best-countries-for-crypto)中的一篇文章，收录了@ jy-p关于美国是加密货币最友好国家的评论，并联合了33个新闻媒体，包括Cointelegraph Italy和Investing.com
- [Master of Nodes](https://mastersofnodes.com/decred-blockchain-system-implemented-in-brazil-municipal-elections)中的一篇文章，重点介绍@ jy-p对Decred在巴西大选中的使用的评论
- @lukebp出现在[Digital Cash Network](https://odysee.com/@DigitalCashNetwork:c/Decred:6)播客中，谈论Decred的治理模型
- [Cointelegraph](https://cointelegraph.com/news/decred-co-founder-explains-rationale-behind-bitcoin-bull-and-bear-cycles)中的一篇文章，重点介绍@ jy-p对比特币的牛市和熊市周期的评论，并联合了17个新闻媒体，包括Cointelegraph德国，Cointelegraph巴西和Cointelegraph意大利

## 活动

参加：

- 11月2日 - [Blockchain Summit Latam](https://www.blockchainsummit.la/) - 互联网。@elian在“公共协议中的治理”演讲中谈到了几个公共区块链之间的异同以及Decred如何从中脱颖而出。([视频](https://www.youtube.com/watch?v=SiMoxHS8AAk&list=PLiJAJqCfjxwIR6q1W0bidE9W4369KMjzz))
- 11月5日 - [Hablemos Decred 20](https://twitter.com/Decred_ES/status/1323671501212684288) - 互联网。西班牙Cointelegraph的@elian和Fernando Quiros谈到了新闻业，传播业和广告业中区块链技术和加密货币的可能用例。([视频](https://www.youtube.com/watch?v=V1tl600djBA))
- 11月9日 - [Talent Land Latinoamerica](https://www.talentland.talent-republic.tv/) - 互联网。@ adcade，@ elian，@ francov_和@pablito谈到了“我们的金钱，我们的规则：抛弃本国货币”。([视频](https://www.youtube.com/watch?v=B0tEYQ2l_RM))
- 11月12日 - [Hablemos Decred 21](https://twitter.com/Decred_ES/status/1326279642169348096) - 互联网。与来宾Cristobal Pereira（LatAmTech首席执行官）一起回顾了Latam区块链峰会，并讨论了Latam生态系统的观点。([视频](https://www.youtube.com/watch?v=sTaghDgY5k8))
- 11月19日 - [Hablemos Decred 22](https://twitter.com/Decred_ES/status/1328819770876162049) - 互联网。邀请嘉宾华金·莫雷诺（Joaquin Moreno）一起讨论主题“购买比特币的公司，您准备好了吗？”。([视频](https://www.youtube.com/watch?v=N2hxP8I6hbM))
- 11月19日 - [University of El Salvador](https://twitter.com/addcade/status/1329605293081288709) - 互联网。@adcade与经济学系的学生讨论了加密货币，Decred，治理和贡献机会。这是一个有2人参加的2小时会议，而有45人参加的会议延长到+1小时。
- 11月27日 - [Hablemos Decred 23](https://twitter.com/Decred_ES/status/1331372082354130946) - 互联网。来自Decred（西班牙语）的@caibarrad和来宾Felipe Montoya参加了会议，讨论了“ DLT”和加密货币之间的异同。([视频](https://www.youtube.com/watch?v=tu5OqKQhSbk))
- 11月28日 - [Partnership agreement with OMJD](https://decredcommunity.github.io/events/index/20201128.1) - 摩洛哥卡萨布兰卡。在7月与摩洛哥青年决策者组织（OMJD）举行在线聚会之后，@ arij与他们签署了为期2年的协议，以举办有关Decred和区块链技术的聚会，研讨会和会议，以造福年轻人。

西班牙Decred活动不断在西班牙语[Cointelegraph](https://es.cointelegraph.com/tags/decred)上登出。

我们用作以上事件数据主数据源的[事件存储库](https://github.com/decredcommunity/events)已使用新的“技术”进行了升级。现在，有关事件的关键信息被保存在（大多数是人类可读的）[YAML文件](https://github.com/decredcommunity/events/tree/master/index)中，并且与完整的[报告](https://github.com/decredcommunity/events/tree/master/reports)相比，编写的散文要少得多。这样的结构使我们可以生成一个[漂亮的网站](https://decredcommunity.github.io/events/index/)，每个事件在此网站上都具有与其相关的所有链接。这应该有助于报告和知识共享。要列出您的活动，请按照以下步骤操作。

## 媒体

精选文章：

- @richardred([blockcommons.red](https://blockcommons.red/crypto-governance-research/overviews/polkadot/))的Polkadot治理概述
- @richardred的Uniswap / SushiSwap治理概述([blockcommons.red](https://blockcommons.red/crypto-governance-research/overviews/uniswap/))


影片：

- Decred双周报v1.6 和DEX最新进展 @Exitus ([youtube](https://www.youtube.com/watch?v=mYfOr4e9MZ8))
- Decred双周报 开发进展概要 社区参与度 @Exitus ([youtube](https://www.youtube.com/watch?v=13YGyb27z5E))
- Decred - 混合区块链 Decred Society ([youtube](https://www.youtube.com/watch?v=dszDzH0OlEo))
- Luke Powell谈数字现金网络 Decred治理，混合共识和新的去中心化国库 ([youtube](https://www.youtube.com/watch?v=4_EafyDcJvk), [odysee.com](https://odysee.com/@DigitalCashNetwork:c/Decred:6), [anchor.fm](https://anchor.fm/digitalcashnetwork))
- 对PermabullNiño(@PermabullNino)的采访 Staked Podcast ([youtube](https://www.youtube.com/watch?v=nRryWFk_l7k))
- 对Le_Hibou_（@Frenchy_LeDegen）的采访 Staked Podcast ([youtube](https://www.youtube.com/watch?v=N5BnEB6MDLs))
- 对LOL DEFI（@loldefi）的采访 by Staked Podcast ([youtube](https://www.youtube.com/watch?v=eqpafR0E1SA))
- 加密货币Convo-播客壮举的Eduardo Lima。DubDigital ([youtube](https://www.youtube.com/watch?v=ErezLZ-SG5o))

Staked Podcast的纯音频版本可在[anchor.fm](https://anchor.fm/staked-podcast)上获取。恭喜您获得1000次下载/流！

音频:

- Hitechies播客-Richard Red和Pramod Dhakalrr讨论了DeFi挑战，ETH，银行业，支付系统的未来等等。 ([hitechies.com](https://www.hitechies.com/richard-red-at-decred-talks-to-pramod-dhakal/))
- 加密对话074-Decred DEX如何计划使用@ jy-p破坏加密交易市场 ([bravenewcoin.com](https://bravenewcoin.com/insights/podcasts/how-the-decred-dex-plans-to-disrupt-the-crypto-exchange-market), [youtube](https://www.youtube.com/watch?v=i3LQza2sYNQ))
- Decred in Depth 33: Seth Simmons谈DCR + Monero隐私 ([libsyn](https://decredindepth.libsyn.com/seth-simmons-dcr-monero-privacy))
- Rough Consensus 12: 比特币已进入中国市场。伙计们与@POVCryptoPod和比特币杂志的共同主持人@ck_SNARKs一起讨论了比特币的采用，山寨币繁荣与萧条的教训，价格在加密货币领域的作用等等。 ([libsyn](https://roughconsensus.libsyn.com/episode-12-bitcoin-has-entered-the-china-shop-w-ck_snarks))
- Rough Consensus 13: 数字自治与自由。蜘蛛侠与Frank Braun（@thefrankbraun）进行了广泛的对话，涉及范围包括：数码朋克数字社会，数字时代的隐私和自由，BTC，DCR，Scrit等在更光明的未来中的作用。 ([libsyn](https://roughconsensus.libsyn.com/episode-13-digital-autonomy-and-freedom-with-frank-braun))

艺术和段子:

- Decred DAO空间邀请[海报](https://twitter.com/coveryfire7777/status/1324430999212744704)由@Exitus 
- [Swiss Army Knife](https://twitter.com/_Checkmatey_/status/1324835192100413441) 的声音金钱@Checkmate
- [Hidden Hydra](https://twitter.com/New_Copernicus/status/1333518011861372928)预告片剪辑by @New_Copernicus
- 在[Redbubble](https://officialcryptos.redbubble.com/)上 查看OfficialCrypto的商品设计（您知道Decred徽标与“ [Real Defi](https://twitter.com/OfficialCryptos/status/1325421754777526272) ”完美匹配）吗？

翻译：

- 我如何学会停止担忧和爱Decred DEX - [西班牙语](https://medium.com/decred-es/c%C3%B3mo-aprend%C3%AD-a-dejar-de-preocuparme-y-amar-el-dcrdex-74e4ecf7bf70) @francov\_
- 门罗币和Decred是新的比特币 - [西班牙语](https://github.com/DecredES/traducciones/blob/master/Monero-y-Decred-son-el-nuevo-Bitcoin.md) @francov\_
- cryptoassets的实用程序 - [西班牙语](https://github.com/DecredES/traducciones/blob/master/La-utilidad-de-los-criptoactivos.md) @francov\_
- 2020年10月的Decred Journal被[翻译成](https://xaur.github.io/decred-news/)阿拉伯语（@arij，@ abdulrahman4），中文（@Dominic），西班牙语（@francov_）和越南语（@duyenemdo）。越南读者还可以赶上八月的活动。谢谢大家的不懈努力！
- 如果您翻译Decred内容，请在[#translations](https://chat.decred.org/#/room/#translations:decred.org)聊天室打个招呼。

## 社区讨论

精选的Reddit帖子：

- 前瞻性思考11月14日星期六开始时，建议选择“ Decred正在重新定价”作为新的[叙述](https://www.reddit.com/r/decred/comments/jtx4y2/forward_thinkingsaturday_14_november/)
- 创建[多重签名](https://www.reddit.com/r/decred/comments/jvhxea/how_to_create_a_decred_multisig_wallet/)地址
- u / oiezz等人的原创[营销思想](https://www.reddit.com/r/decred/comments/jx989d/tiny_marketing_ideas/)集合
- 为什么[混淆](https://www.reddit.com/r/decred/comments/k39r3v/not_showing_result_of_a_votation_before_it_ends/)选票是一个坏主意
- Miniscript，Minsc或RGB等高级[脚本语言](https://www.reddit.com/r/decred/comments/k3ioxi/how_feasible_is_to_implement_a_scripting_language/)对Decred的适用性=

精选的Twitter讨论：

- @PermabullNino在dcrdex上的[价值流](https://twitter.com/PermabullNino/status/1323330573444632576)图显示了为什么无需在交易过程中注入代币
- @withdecred的事实丰富的Decred螺距[螺纹](https://twitter.com/withdecred/status/1325147231935098880)

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
