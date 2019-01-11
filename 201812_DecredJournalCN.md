# Decred月报 - 12月 

![Decred Journal - December 2018](img/DEC18_journal-201812-384.png)

12月份中，项目发展的不错，为2018年划上了一个圆满的句点。Politeia前期中通过的一些提案正如火如荼进行中，Ditto人员已加入我们并与广大的社区合作，为Decred制定2019年的拓展计划。

软件版本v1.4.0预发布版可在[GitHub](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc2)下载。欢迎爱好者使用，普通用户建议耐心等待最终版。为确保下载的是官方开发版本，请下载后务必进行[验证软件签名](https://docs.decred.org/advanced/verifying-binaries/)。

[安卓钱包](https://github.com/decred/dcrandroid)预发布版也在[Google Play store](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet)上线了。这是Decred SPV模式带来的好处。SPV模式允许用户避开中心化服务器，直接从P2P网络下载区块信息，从而增强隐私功能-这样的设计在手机钱包里是少见的。除了注意这是预发布版本，请用户了解手机的环境会带来一下安全隐患，不建议储存大量DCR。

虽然在币圈的价格和资金收缩来说，12月是难过的一个月，但Decred并未收到影响，并已准备好在2019年冲刺扩展。

Decred月报团队祝愿所有读者新年快乐！

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): v1.4的RC2已发布。此版本更新包括[智能费用估算器](https://github.com/decred/dcrd/pull/1434)，一个将允许用户根据需求选择最快交易或最低费率的选项。此功能对于闪电网络非常重要，同时也是个处理网络拥挤的机制。更多详情在[issue](https://github.com/decred/dcrd/issues/1412)中有详细说明。现在支持[设置白名单](https://github.com/decred/dcrd/pull/1516), 在白名单下允许无限连接，这让运营者允许自己的SPV客户端连接。此外我们对初始同步，验证和网络操作进行了若干性能改进，选择升级的用户请注意，这会有一次数据库迁移，平均用时大概30-60分钟(具体取决于硬件)。完整更改列表可在[发布说明](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc2)查询。

在`go get`工具中使用恶意仓库时存在远程代码执行的[漏洞](https://seclists.org/oss-sec/2018/q4/254)已被修复。Decred软件并没有受到影响。另外，dcrd里除了Go runtime以外，所有依赖项的更改都已被审核。这也是在发布dcrd版本时需要那么多努力及为什么依赖数量应该受到限制的部分原因。更多细节在[聊天室](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$154476448242812wqgkf:decred.org)中讨论。

关于dcrd中实施"父子支付方案"(Child Pays For Parent (CPFP))的讨论也正[进行中](https://github.com/decred/dcrd/issues/1556)。

[dcrwallet](https://github.com/decred/dcrwallet): 刚发布的v1.4.0 RC2修复了许多关于SPV及错误处理的漏洞，并添加了一系列新的gRPC端点，以允许终端用户在UI中启动新功能。从钱包到节点的Tor连接已通过支持[代理模式](https://github.com/decred/dcrwallet/pull/1294)解决。有了足够的网络节点升级，这让[默认交易费用](https://github.com/decred/dcrwallet/pull/1339)降至0.0001 DCR得以完成。更多更改请参考[发布说明](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc2)。

[Decrediton](https://github.com/decred/decrediton): v1.4.0 RC2 预发布版更新功能包括对Trezor初步支持，设计改进及漏洞修复。初步的Trezor[支持](https://github.com/decred/decrediton/pull/1547)让用户可以使用Decrediton作为“watch-only”钱包并通过Trezor验签交易。这功能很可能在获得足够测试前隐藏在设置中。该版本暂不支持投票功能。另外“watch-only”钱包可以[创建未验签交易](https://github.com/decred/decrediton/pull/1864)，然后把数据传输到另一台设备签名验证及广播。治理页面也获得一些较大的改动，其中一个增加的重要功能包括在有新提案及投票活动时[通知](https://github.com/decred/decrediton/pull/1835)用户。[开启SPV模式](https://github.com/decred/decrediton/pull/1766)的新页面也会在钱包开启页面显示。初始的暗色主题也可以在设定中启用(最终颜色还待确认)。更多相关改进信息请参考[发布说明](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc2)。

在主分支中（未包含在1.4发布版），现在可以为[Raspberry Pi(树莓派)](https://github.com/decred/decrediton/pull/1904)打包Decrediton。

许多[设计工作](https://github.com/decred/decrediton/issues?utf8=%E2%9C%93&q=is%3Aissue+author%3Alinnutee+created%3A2018-12-01..2018-12-31)也已完成，正等待整合实施。

[Politeia](https://github.com/decred/politeia): 最新的[安全收紧](https://github.com/decred/politeiagui/pull/935)为Politeia在[securityheaders.com](https://securityheaders.com/?q=test-proposals.decred.org&followRedirects=on)争取了A+评价，这项荣誉让Politeia成为该网站中的最优秀的3%并登上荣誉榜。另外也加入了查看[旧提案版本](https://github.com/decred/politeiagui/pull/949)版本功能。这是另一份比较[版本区别](https://github.com/decred/politeiagui/issues/973)的一部分。politeiavoter将[自动重试失败的请求](https://github.com/decred/politeia/pull/639),这也修复了Tor的使用。评论评分计算通过从politeiad[迁移](https://github.com/decred/politeia/pull/610)到politeiawww完成了修复。提案在批准启动投票后不可转成[被放弃](https://github.com/decred/politeiagui/pull/936)。上述及其他一些小更动将在下一次部署后更新到[提案系统](https://proposals.decred.org/)页面。

后台管理[数据备份](https://github.com/decred/politeia/issues/605)及另外两项服务器扩展的更改正进行中。这两项更改包括[缓存层](https://github.com/decred/politeia/issues/546)及[websockets 支持](https://github.com/decred/politeia/issues/547)。

[安卓钱包](https://github.com/decred/dcrandroid): v1.0.0 [主网](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet)及[测试网](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.testnet)的第二预发布版可在Google Play下载。更新包括完全重做种子确认及恢复种子界面，修复漏洞等。
完整改进事项列表可参照[GitHub](https://github.com/decred/dcrandroid/tree/v1.0.0-rc2)。在[这里](https://www.reddit.com/r/decred/comments/a846ch/decred_wallet_for_android_release_candidate/)有更多的讨论和评论。

即将更新的下个预发布版将修复一些小漏洞，以及少数人要求的初始同步时更友好的状态显示。

目前的更新专注于简化新用户的设置体验，毕竟这是新用户第一接触而且过程有点繁琐。

我们讨论了钱包加密的局限性以及在不安全的Android智能手机上投票的风险, 请见[讨论](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$154533559847474ZIrlD:decred.org).

[iOS钱包](https://github.com/raedahgroup/dcrios): 开发正努力跟进安卓钱包功能。iOS测试将在安卓1.0完成后发布。

[dcrdata](https://github.com/decred/dcrdata): v3.1.1 已上线到 [主页面](https://explorer.dcrdata.org/)。更新内容包括[侧链](https://explorer.dcrdata.org/side)及[不合格区块](https://explorer.dcrdata.org/rejects)，重大的性能改进，Go模块的支持，非javescript模式的[改进](https://github.com/decred/dcrdata/pull/852) _(抗拒js的恐龙对此表示感谢!)_ 。完整发布说明请[查看](https://github.com/decred/dcrdata/releases/tag/v3.1.0)。这次发布是4个月里面，16位代码贡献者的129提交的成果。恭喜dcrdata团队！

在主分支上，[CSV格式](https://github.com/decred/dcrdata/pull/894)下载一个地址的交易信息的新功能已完成。合并了几个大型重构(采用当前前端的最佳实践)。

在受到DDoS攻击后，公共dcrdata的Tor服务暂时关闭。经过一番[讨论](https://matrix.to/#/!YwropUjOvDAjfbVSzi:decred.org/$154480347443065mKiKp:decred.org)后也重新上线于[dcrdata2opeenddl.onion](http://dcrdata2opeenddl.onion/)。

开发人员可以使用新的[Docker image](https://github.com/decred/dcrdocker/pull/45)来开发及测试dcrdata和wiki上新的[FAQ页面](https://github.com/decred/dcrdata/wiki/FAQ)

[分票(Ticket splitting)](https://github.com/matheusd/dcr-split-ticket-matcher): [v0.7.0](https://github.com/matheusd/dcr-split-ticket-matcher/releases/tag/v0.7.0)和[v0.7.2](https://github.com/matheusd/dcr-split-ticket-matcher/releases/tag/v0.7.2)已发布。更新包括: SPV客户端的支持(请阅读[隐私协议](https://github.com/matheusd/dcr-split-ticket-matcher/releases/tag/v0.7.0))，通过使用session令牌提高安全性能，OpenBSD的支持及更好的汇报。[请在GitHub](https://github.com/matheusd/dcr-split-ticket-matcher/releases)下载。为确保下载版本为@matheusd提供，请下载后验证软件签名。

[docs](https://github.com/decred/dcrdocs): 基于之前设定的重定向基础设施，[整理网址](https://github.com/decred/dcrdocs/issues/659)及目录结构的工作已经开始。议程投票“Agenda Voting” 一词[改成](https://github.com/decred/dcrdocs/pull/733)共识规则投票“Consensus Rules Voting”。有关翻译的架构已经被[移除](https://github.com/decred/dcrdocs/issues/736)。词汇表也增加了更多的术语。新的[SPV指南](https://docs.decred.org/wallets/spv/)
已被[收录](https://github.com/decred/dcrdocs/pull/726)到文档中。Politeia文档的[更新](https://github.com/decred/dcrdocs/pull/758)把Politeia相关页面整理到一起，同时增加了[提案指引](https://docs.decred.org/governance/politeia/proposal-guidelines/)页面及[提案例子](https://docs.decred.org/governance/politeia/example-proposals/).

[decred.org](https://github.com/decred/dcrweb): 页眉从javascript[改成](https://github.com/decred/dcrweb/pull/457)视频，Rocket.Chat也从社区页面被[移除了](https://github.com/decred/dcrweb/pull/460)，Decred的商业简报除了PDF下载外也增加了[网页版](https://decred.org/brief/)。

其他:

* @matheusd 提出[Raspberry Pi离线交易签名工具](https://www.reddit.com/r/decred/comments/a3bfyi/raspberry_pi_offline_transaction_signer/)并制作了一个[现场演戏](https://www.youtube.com/watch?v=xbSoZ7GH1_k&t=7s)影片。如果您觉得这是值得更详细开发的功能[请联系他](https://www.reddit.com/r/decred/comments/a3bfyi/raspberry_pi_offline_transaction_signer/)。
* [authit](https://authit.co/)是dcrtime的UI概念证明。[这里](https://github.com/getset0/authit)可以找到该代码库，并在[这里](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$154454253739832PpXgR:decred.org)热烈讨论。这要归功于@fernandoabolafio, @tiagoalvesdulce和@vctt。该代码库也已移入到 Decred [GitHub组织](https://github.com/decred/authit)的一部分。
* @devwarrior正开发[原子交换](https://github.com/xaur/decred-issues/issues/8#issuecomment-447220453)的UI概念证明。欢迎到[聊天室](https://decred.slack.com/team/U6056C1NE)联系讨论合作并把这项功能带到Decred。
* 原子交换中添加[支持QTUM](https://github.com/decred/atomicswap/pull/93)的PR已被提交，欢迎社区加入评论和测试。前段时间的[支持Ethereum](https://github.com/decred/atomicswap/pull/76)PR也是一个重要的亮点。
* 为了更有效的向非英语社区推广Decred核心概念，协调重要Decred文章的[翻译工作](https://github.com/artikozel/decred-translations)正在进行中。
* Decred命令行界面工具可在使用[musl](https://www.musl-libc.org/)(更干净的libc实施)的Alpine Linux运行。详情参阅[聊天室记录](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15457968071823GYapk:decred.org)。

12月开发活动数据: 分布于8个存储库（repositories) 有 230 有效PRs, 196 主要提交, 33k 行添加 及 106k 行删除。每个存储库中有来自3-9个开发者的贡献。

## 人员

欢迎首次代码贡献者：[aerth](https://github.com/decred/dcrwallet/commits?author=aerth)(dcrwallet)，[@guang](https://github.com/decred/decrediton/commits?author=Guang168)(decrediton)及[tpkeeper](https://github.com/decred/politeia/commits?author=tpkeeper)(politeia)。

[30000fps](http://30000fps.com)从2018夏天已成为Decred贡献者。他的工作的目标之一是通过找到有意义的方式来实现可视化和说明一些隐晦的过程和特征，从而带来启发性的发展。最近的开发视觉呈现(包括接下来的[v1.4.0的发布](https://user-images.githubusercontent.com/17774057/50576201-3e124e80-0e15-11e9-83cd-28b50cfd9357.gif) (4 MB)，[Politeia的发布](https://twitter.com/decredproject/status/1052203697986363392)，[v1.3.0的发布](https://twitter.com/decredproject/status/1044693349205200896))，还有decred.org中子页面的页眉动画[改动](https://github.com/decred/dcrdesign/issues/27)都是他的一些作品示例。

decred.org中移除了3名贡献者 https://github.com/decred/dcrweb/pull/472

部分贡献者在[聊天室](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$154508806344819aIkBV:decred.org)分享了他们的入职经验，对于有兴趣加入Decred成为献者的朋友们是了解这过程很好的资料。@richardred 也发布了一篇很好的文章 [“为Decred去中心化自治实体工作(Working for the Decred DAE)”](https://medium.com/@richardred/working-for-the-decred-dae-a9cfb17686fa)来详细描述他参与Decred的经历。

另外还有些独立贡献者正把他们2019的一些计划整合成一份社区[路线图](https://github.com/degeri/decred_independent_contractor_roadmap)

## 治理

在整个12月中，[基金会](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收取了17,016 DCR并花费了其中 12,570 DCR。按12月平均DCR价格17.5美元计算，这分别代表29.8万美元和22万美元。由于这是用于支付11月的工作开销，所以同时也可以考虑这数额如果以11月均价为32.50美元来计算的话分别是55.3万和40.9万美元。

以下是1月10日为止的粗略提案更新。请阅读在[Politeia](https://proposals.decred.org/)网页的提案原文及讨论。

* [开源研究项目2(Open Source Research2)](https://proposals.decred.org/proposals/5d9cfb07aefb338ba1b74f97de16ee651beabc851c7f2b5f790bd88aea23b3cb): 目前正进行Politeia的数据研究及Git贡献者分析，4个新的研究提议也在提案评论中提出。请到讨论区评论并对于提议发出投票，让研究团队了解那一项是重要的。
* [稳定币提案](https://proposals.decred.org/proposals/85fc65cef080cfc3564906fd3d488b827d74fc99bb29143ed8aa6c400b765be9)被大部分人批评后，提案者取消了提案。
* [Coffee钱包整合](https://proposals.decred.org/proposals/45de9806c952c5ffc2fc6782fddbc74c852c26e3fb0e950144b92d75082c4731): 提案者建议降低要求数额但社区对于支付整合费用反应并不热烈。提案沉默了一段时间后被移到被放弃状态。后来提案者回来[说明](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15467875879232uBQcG:decred.org) 他们并不打算放弃。
* 不通过的提案: [电台广告](https://proposals.decred.org/proposals/7fe5d07a4ffff7dc6a83383018823d880b1c1db0a29305e74934817cf2b4e2ce) (69% 反对), [Decredex](https://proposals.decred.org/proposals/e78bc28631d0e682912e3ece25944481bf978b906ea44b1ed36470c0f48b27fc) (96% 反对), Bcash的[ATM 整合](https://proposals.decred.org/proposals/bb7e19283d5c65fed598d5a2f4afcc2b5d2eab187b9cb84fc4304430f80b5ad1) (89% 反对); 参与率介于总票的24-31%。
* [Baeond](https://proposals.decred.org/proposals/f545b359fcf1b40b356e9cb556cb422cc7ff01b628b577f804cdc45ce414f5dd)自治卡牌游戏: 讨论仍然在进行中，提案者在评论和聊天室中和社区进行讨论并根据反馈修改提案，很多社区成员对于这个提案将如何对Decred项目有帮助感到困惑。
* [Smart Reach合作提案](https://proposals.decred.org/proposals/cf7143c93d35f886be03d749396e9202c7837a3d3cbbe876f93c3a7d18ec2028): 讨论仍然在进行中。

[漏洞悬赏提案](https://proposals.decred.org/proposals/d33a2667469b56942adf42453def6cc2292325251e4cf791e806939ea9efc9e1)以90%同意及30%的参与率通过了提案。@degeri展示了经历所有阶段的一个很好的例子：参与社区展示出执行有用的工作的能力，鉴定社区缺乏项目，起草方案主意，推向社区获取多轮反馈，提交提案，最终获取支持。这里[值得一提](https://twitter.com/lukebp_/status/1078691610253250560)的是，一位匿名贡献者通过提交高质量工作成果建立起记录并获取信任。Decred是少数可以这样获得支持的项目。

为了避免常见错误和建立一个成功的提案，请阅读@s_ben的新[提案指引](https://docs.decred.org/governance/politeia/proposal-guidelines/)(灵感来自于@nnnko56非常好的[评论](https://proposals.decred.org/proposals/85fc65cef080cfc3564906fd3d488b827d74fc99bb29143ed8aa6c400b765be9/comments/2))

Company 0将不会为匿名的工作向基金会收取费用。相关解释参考[reddit帖](https://www.reddit.com/r/decred/comments/a6l00i/why_is_the_community_not_voting_on_implementing/)

讨论: [聊天室](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$154502025444491kdLiq:decred.org)里讨论到特别在熊市时必须谨慎控制节约基金会开销。[在reddit帖中](https://www.reddit.com/r/decred/comments/aa5jvn/any_updates_on_antonopouloss_veiw_of_decred/)讨论到几个针对Decred治理体系常提到的论点包括：“我们不知道治理体系是否有效，因为它还没有失败” 及 “目前还没有争议性课题”。事实证明建立一个系统过程中完全避免争议是非常困难的。

@richardred在Politeia[第8期](https://medium.com/politeia-digest/issue-8-dec-5-dec-11-2018-23bb061a08a0)和[第9期](https://medium.com/politeia-digest/issue-9-dec-12-dec-31-2018-67b65b5bf30)简报中提供了更详细的Politeia活动报告。简报抓住了每项提案的一些有趣的细节。第9期也包含了特别2018年终Politeia从上线以来的数据统计。你也可以到[这里](https://github.com/RichardRed0x/politeia-digest)阅读所有发布过的简报并留言反馈。

## 网络

算力: 12月算力开始大约167Ph/s结束约183 Ph/s，本月中最高207Ph/s及最低110Ph/s，而大部分时间平均于150Ph/s左右。在一月10日根据[dcrstats.com](https://dcrstats.com/pow)，矿池算力分布为：poolin 34%，F2pool 27%, UUPool 7.4%, btc.com 7%, Luxor 3.8%, BeePool 2.6%， coinmine 1.1%, 其他为17%。矿池分布数据为大约值无法精确计算。 

投票: 按dcrstats.com, 30日 平均票价为 103（+0）DCR。价格与101 DCR 至 107 DCR之间浮动。锁仓数额为4.14-4.23 百万 DCR, 大约总流通量的 46.3%-47.1%。

节点: 截止于1月1日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 192 public listening Node 及 253 Normal Node。版本分部: 1.5% 为 v1.5.0(pre)开发者版本，1.8% 为 v1.4.0(rc1)，5.3% 为 v1.4.0（pre)(-1.2%)，55% 为 v1.3.0(+5%)，20% 为 v1.2.0 (-5%)，10% 为 v1.1.2 (-1%) 及 4% 为 v1.1.0(-1%)。

我们希望在这一部分提供更多[有趣的数据](https://github.com/xaur/decred-news/issues/41)，如果您可以帮上忙请您联系我们。

第300,000区块在这个月被挖矿。DCR流通量已超过 9,000,000!恭喜大家!

## 挖矿

Whatsminer D1:

* [中文评论](https://www.cybtc.com/forum.php?mod=viewthread&tid=41377&fromuid=6)
* Luxor发布了[设置教程](https://medium.com/luxor/whatsminer-d1-decred-setup-guide-182eeccaed99)
* Whatsminer.net[报告](https://twitter.com/whatsminer/status/1075810531838091265)指出第一批D1订单已全部发货。

比特大陆的 [Antminer DR5](https://twitter.com/Antminer_main/status/1072435004142182400)在推出是收到推特社区批评。[参数](https://www.asicminervalue.com/miners/bitmain/antminer-dr5-34th): 34 Th/s，1,800 W, 价格[从1,400美元](https://www.asicminervalue.com/miners/bitmain/antminer-dr5-34th)开始。[Reddit](https://www.reddit.com/r/decred/comments/a9iqbl/got_voted_to_0_in_rcryptocurrency_maybe_ill_get/)帖子里也有关于这台矿机和一些小户爱好者挖矿的挑战性。

从eBay上购买矿机必须小心，您有可能只获得[重量](https://matrix.to/#/!NNzHoaSdnsbZDQOXJr:decred.org/$154491308943809bYuYs:decred.org)

## 整合

硬件钱包公司Ledger宣布期待已久的DCR整合已经完成：

> 我们很高兴公布Ledger Nano S及Ledger Blue现已和DCR匹配。Decred已在Ledger Live上发布并成为自推出以来第一个本机Ledger Live集成。[这里](https://www.ledger.fr/2018/12/11/ledger-nano-s-ledger-blue-and-ledger-live-now-support-decred-transactions/)阅读更多.([@LedgerHQ](https://twitter.com/LedgerHQ/status/1072446149863329792))

DCR可以通过Ledger Live储存。Ledger Live是自从Ledger在今年早些时候停止使用app后的访问加密资产一站式应用。

Cobo Wallet [发布](https://twitter.com/cobo_wallet/status/1070805250376900609)新的代管投票服务。请对于谁控制密钥，是否市区共识及Politeia投票权等影响作出研究。更多讨论在[这里](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$154413818735775gNTIq:decred.org)。

对于软件和硬件钱包，请务必研究并了解具体如何操作。你是否掌控私钥？你是否失去共识投票权和Politeia投票权？钱包是直接连接Decred全节点还是通过中介连接？该服务是否会和第三方分享您的资料？代码是否开源可审计？
 
## 外展活动

> 基于Ditto展开了他们的工作，12月对于Decred来说是个令人兴奋的一个月。第一项就是介绍和确定工作流程。你可以在各Matrix聊天室遇到我们的好友Liz Bagot(@liz\_bagot)，Trey Ditto(@treydpr)，Margaret Mei(@margaret\_mei)，Blain Rethmeier(@blainr)，及Milvian Preito(@milvian)。这些聊天室包括#marketing, #ditto\_pr, and #writers\_room。
> 
> 消息传递方面工作已展开并可在[这里](https://docs.google.com/document/d/1BCah1EKLHpwgkvVcWRWJTRC68iWeGPdbGSrhEw35XhU/edit)查看，也欢迎持续的意见投入。同时，我们正在与设计团队合作，将新消息传递集成到网站中，并通过新页面扩展内容，进一步解释Decred的重要信息。
> 
> 传递信息内容应该会在一月份达成一致，并且开启网站上的工作。一个关于活动及其他策略的计划也会在一月份公布。(@Dustorf)

Ditto团队加入了#marketing，该聊天室在整个月都非常热闹，也有很多关于信息内容的讨论。

@Dustorf及@jy-p和Ditto在纽约开会, 这里可以看到[报告](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154413732235771XIVBH:decred.org)。会议中讨论的包括吸引新开发人员及贡献者的挑战，对内行的投资者，机构或政府机构解释及宣传Decred长期愿景。

Trey[发布](https://medium.com/decred/decred-and-ditto-in-2019-c9063a6bca06)了Ditto在2019的大局方向和Decred的策略。后来还在Reddit加上了一个[问卷](https://www.reddit.com/r/decred/comments/a7cul1/decred_and_ditto_in_2019_share_your_ideas/)尝试了解社区如何形容Decred，平时阅读什么媒体，及应该如何吸引更多开发人员。

@liz_bagot在12中旬发布了第一期的Ditto双周[更新](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154482468943386bBAIp:decred.org?via=decred.org&via=matrix.org)并对12月的工作作出总结：

* 与Dustin和Jake在12月初，在我们Brooklyn办公室进行2.5小时的入职会议
* 创建了一个基础信息传递平台，其中包含Decred的受众细分，关于项目章节，使命陈述，愿景陈述，及针对每类用户的定位陈述。我们把这些[提交](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154524074346294yVYFR:decred.org)给社区并将在一月根据反馈进行再一轮修改。
* 出席并邀请Breaker Mag, Forbes, 及Fortune记者参与Decred在纽约市的meetup。
* 安排并配备Decred社区成员与数个大媒体进行采访暂时还没有发布日期。
* 我们把Jake对于2019加密货币的预测评论推广给加密货币记者并成功获得在[NullTX](https://nulltx.com/decred-co-founder-pronounces-2018-as-the-death-of-the-ico-model/)，[Crypto Briefing](https://cryptobriefing.com/crypto-2019-institutional-adoption/)，[The Daily Hodl](https://dailyhodl.com/2018/12/21/after-bitcoin-rallies-18-industry-insiders-weigh-in-on-a-bull-run-and-cryptos-next-turn/)及[CCN](https://www.ccn.com/2018-in-4-words-icos-and-ethereum-are-dead/)获得报导。

目前有5位知名社区会员拥有发@decredproject推特账号推文的权力，[这里](https://medium.com/@richardred/working-for-the-decred-dae-a9cfb17686fa#bd70)可以了解这具体是怎么操作的。

## 社区活动

Decred于12月5日星期三在纽约市flatiron区的Distributed Global举行了首次聚会。大约80人包括VC，其他项目的开发者，媒体和Decred社区的成员出席。项目负责人Jake Yocom-Piatt发表了Decred概述介绍([照片](https://twitter.com/CryptoLeslie/status/1070769160878219266))，然后深入讨论了Politeia提案系统的技术细节，包括它的工作原理和应用的潜在广度。

之后，Iterative Capital的创始人Chris Dannen讨论了在免费开源软件时代的工作方式改变发展。Iterative Capital的[论文](https://iterative.capital/thesis/)详细的阐述他们在这方面的想法。他解释了Decred的资金管理如何与一个巨大的工作趋势相吻合，而这种工作趋势为工人提供了所需的自主权，使他们能够做到最好。

最后，Placeholder VC的Chris Burniske和Joel Monegro帮忙举办一个对答环节，从机构投资者的角度解释Decred的价值。 Chris透露了VC的财务推理，包括：

1. 团队 - btcsuite 发布时和BTC Core发布的一样好
2. PoW/PoS混合制度比任何其他网络都安全
3. 基金会资助确保开发的长期资金
4. 抗分叉-Decred是为了达成共识过程中维持社区而设

Joel对Decred的治理系统及其让Decred多态，在社区决定时添加功能的能力表示赞赏。 他们得出结论，Decred是为数十年的时间而建造/设计的。 他们分享了他们为了Decred在托管，交易和机构投票方面所做的一些工作，并总结，目前Decred面临的最大问题是流动性。

创始人之夜于12月6日星期四举行，是Distributed Global的节日派对。他们从各个办公室引进了他们所有的GP，并邀请他们的LP，合作伙伴以及他们投资组合中的各种项目的成员。这是一个很好的机会，可以满足于各个社区见面，并为纽约市未来的活动建立起关系。下一轮纽约的Decred活动计划在春天举行。

其他出席的活动:

* 在墨西哥Amozoc科技大学中@elian向学生介绍未来需要的技能并[分享](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15466174667748MPUAY:decred.org): “作为我经验分享的一部分，我粗略的介绍了Decred作为一个创新项目，数字技能（digital skills）成为协作的重要工具。这并不是加密货币活动，反而是个商业管理学生的激励讲座，鼓励他们去学习一些数字电子方面的技能。这是郊外的一所较小的大学，所以这类内容非常受欢迎。作为网络企业带来的新机会分享，我也分享了我在Decred开源项目中的工作。我认为让他们了解到在无限可能的互联网中庞大的经济对他们来说非常有趣。”([照片](https://twitter.com/Decred_MX/status/1071230180398641154))
* [Decred入门](https://cryptocanucks.com/events/an-introduction-to-decred-toronto/)-多伦多，加拿大。@michae2xl和@zubairzia0举办了活动并[分享](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15464604416182ZLeNH:decred.org) 虽然出席率很低，大家对于和本地Decred社区见面感到期待并愿意帮忙组织下次活动。([照片](https://twitter.com/Decred_CA/status/1079191530362101760))

未来活动:

* [OKEx Taiwan MeetUp](https://www.eventbrite.hk/e/okex-global-meetup-tour-2019-taiwan-tickets-54689867867)-台北，台湾，1月17日活动前部分介绍3个项目(Decred, EOS和NEM,各20分钟)，另一部分是关于链上投票（30分钟）的小组讨论。@morphymore 将参与介绍。
* [Binance Blockchain Week](https://www.binancefair.com/)新加坡，1月21-22日 @guang将代表Decred出席。
* [10 lat Bitcoina](https://10latbitcoina.com.pl/)-1月26日，波兰华沙@karamble 将在一个庆祝比特币白皮书和比特币10周年纪念的峰会上发表演说。
* [TabConf](https://tabconf.com/)美国亚特兰大，2月8-10日. @moo31337 将在2月9日介绍“Decred 101:Decred入门”
* [北美比特币峰会The North American Bitcoin Conference](https://btcmiami.com/) 迈亚密美国，1月16-18日. @jy-p将介绍Politeia及探讨Politeia更广的潜在应用。如果您有兴趣在峰会中帮忙请联系@Dustorf。
* [Campus Party](http://brasil.campus-party.org/cpbr12/patrocinadores/)圣保罗巴西，2月12-17。Decred将会有演讲人及专属的黑客马拉松区域。
* [Jalisco Talent Land](https://www.talent-land.mx/#entradas)瓜达拉哈拉，墨西哥，4月22-26日。Decred将有个展位。@elian将介绍Decred概览和Q&A，同时也会有如何使用软件及投票的教程。如果您有兴趣出席或帮忙请联系@elian。

任何有关活动的问题欢迎到[#event_planning](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org)聊天室提问。

## 媒体链接

部分文章:

* Bitcoin Miners Go Silent As Price Falls ([英文版cryptobriefing.com](https://cryptobriefing.com/bitcoin-miners-silent-price-falls/)，[中文版](https://www.jinse.com/bitcoin/288904.html))
* Detailed analysis of Decred fork resistance by @Haon ([medium](https://medium.com/decred/detailed-analysis-of-decred-fork-resistance-93022e0bcde7))
* Decred and Ditto in 2019 by Trey Ditto ([medium](https://medium.com/decred/decred-and-ditto-in-2019-c9063a6bca06)，社区问卷和[讨论](https://www.reddit.com/r/decred/comments/a7cul1/decred_and_ditto_in_2019_share_your_ideas/))
* Fundamental Pick: Decred by BBOD Research ([英文版blog.bbod.io](https://blog.bbod.io/decred-dcr-fundamental-analysis/)，[中文版](https://www.weibo.com/ttarticle/p/show?id=2309404313596447316959)及[日文版](https://cointyo.jp/article/10005567))
* Decred Co-founder Pronounces 2018 as the "Death of the ICO Model" ([nulltx.com](https://nulltx.com/decred-co-founder-pronounces-2018-as-the-death-of-the-ico-model/))
* 2018 in 4 Words - ICOs and Ethereum Died ([ccn.com](https://www.ccn.com/2018-in-4-words-icos-and-ethereum-are-dead/))
* The practical cypherpunk: Marco Peereboom of Decred ([coinrivet.com](https://coinrivet.com/the-practical-cypherpunk-marco-peereboom-of-decred/))
* Decred: Governance and Funding Reimagined ([51pct.io](https://51pct.io/decred-governance-and-funding-reimagined/))
* Working for the Decred DAE by @richardred ([medium](https://medium.com/@richardred/working-for-the-decred-dae-a9cfb17686fa))

翻译:

* Decred Journal - November 2018 @elian 翻译的[西班牙语](https://medium.com/@decred_es/bolet%C3%ADn-mensual-decred-noviembre-2018-52168692e624), @kozel 翻译的[波兰语](https://github.com/artikozel/DecredJournalPL/blob/master/journal/201811_DecredJournalPL.md)及@DZ 翻译的[俄罗斯语](https://medium.com/decred-russia/decred-journal-%D0%BD%D0%BE%D1%8F%D0%B1%D1%80%D1%8C-2018-d0aceacfd72a)， @guang 翻译的[中文](https://medium.com/@guang.dcr/decred%E6%9C%88%E6%8A%A5-11%E6%9C%88-1ddac6598830)。11月月报是目前最大一份(59 KiB), 感谢大家翻译工作的努力！
* 您可以在Decred Journal[主页](https://xaur.github.io/decred-news/)找到所有翻译链接。
* [Detailed analysis of Decred fork resistance](https://medium.com/decred/detailed-analysis-of-decred-fork-resistance-93022e0bcde7) by @Haon - @kozel 翻译的[波兰语](https://github.com/artikozel/decred-articles/blob/master/Polish/into-polish/decredforkresistance.md)
* [How to Get Hired as a Decred Contractor](https://medium.com/decred/how-to-get-hired-as-a-decred-contractor-e1435842df10) by @Haon - @guang 翻译的[中文](https://www.weibo.com/ttarticle/p/show?id=2309404315589245067163)

录像:

* On The Record w/ Murad Mahmudov - Bitcoin for 2019 on Tone Vays show ([youtube](https://www.youtube.com/watch?v=pjXzrAOhAPo), Decred介绍在影片大约1小时点开始)

录音:

* Free Talk Live 2018-10-27 Interview with Marco Peereboom of Decred at the Texas Bitcoin Conference https://soundcloud.com/freetalklive/free-talk-live-2018-10-27#t=40:50 _(missed in Oct issue)_
* Episode 18: Murad Mahmudov on Bitcoin http://didyouknowcrypto.com/episode-18-murad-on-bitcoin/ {extract highlights}

## 社区讨论

社区数据（Jan 1）:

* Twitter followers: 39,884 (-120)
* Reddit subscribers: 9,241 (+110)
* Matrix users: 221 (+18)
* Slack users: 6419 (+66)
* Telegram users: 4734 (+92)
* YouTube subscribers: 3738 (+2)
* Facebook followers: 3121 (+16), likes: 2880 (+13)
* LinkedIn followers: Decred page 450 (+17), Politeia page 24 (+4)
* GitHub dcrd stars: 458 (+11), forks: 1192 (+33)

另外还有电报群社区 中文(661, +119), 葡萄牙语 (435, +99) 及意大利语 (120)。还有@michae2xl运行Instagram中@decredproject账号1月6日为止有396关注。

通讯系统新闻：

* @dhill继续修复连接聊天软件的漏洞 https://github.com/42wim/matterbridge/pull/644, 仍有些有关带附件信息的漏洞有待解决。
* 由于活跃度低的关系，\#smart_contracts频道将被存档
* Rocket.Chat被[移除](https://github.com/decred/dcrweb/pull/460)

社区启用[issue跟踪](https://github.com/xaur/decred-issues)模型，试图以更结构化的格式讨论可执行的想法。任何对项目有益的想法都可以加入讨论。截至1月10日为止，有[73个issues](https://github.com/xaur/decred-issues/issues)包括[文章主题想法](https://github.com/xaur/decred-issues/labels/article), [PR](https://github.com/xaur/decred-issues/labels/PR), [存档](https://github.com/xaur/decred-issues/labels/archiving)及保存数据，或[通信平台](https://github.com/xaur/decred-issues/labels/comms)的讨论。例如[这项issue](https://github.com/xaur/decred-issues/issues/54)就是关于要给Decred的混合PoW/PoS共识算法取个好名字的艰难任务。目前所有提出的选项都已经在issue中记录下来。您可以使用顶部的“watch”按钮订阅所有内容，也可以使用右侧面板上的“订阅”按钮订阅个别issue。人们普遍认为“GitHub适合开发人员” - 事实并非如此。发布issue和评论以及'+1'并不比使用Reddit或聊天软件难用，而事实上，很多非开发人员已经通过这样做出了贡献。

Reddit事件展示了平台的另一个弱点。用户开了多个帖子并激发了讨论，但后来却把帖子删除了。这件事浪费了所有社区回复的人的努力。被删除的帖虽然以另一种形式[保存](https://www.reddit.com/r/decred/comments/a6ywpj/deleted_threads_with_valuable_discussion/)了下来，但此事件显示了另一种攻击/破坏维度：触发讨论然后删除帖子，浪费社区的资源。由于版主无法禁止用户删除内容，因此在Reddit其实并无法阻止这问题的发生。该事件也引发了探讨基于Politeia的[Reddit替代产品](https://github.com/xaur/decred-issues/issues/38)的讨论，。

再一次的，在临近软件新版本发布时Reddit出现了很多不寻常活动。这包括许多较不相关问题的出现，或看似无意的问题等等，并且这些问题都是从一些从来不活跃，短暂出现的帐号问出。这起事希望让关心项目的社区成员注意这些有可能浪费项目资源的怪异活动。详情请看[讨论](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$154531182347084ccYxu:decred.org)。

## 市场

12月中DCR在 USD 14.2-21.4/BTC 0.0042-0.0058 区间交易。平均DCR/USD 价格为 USD17.50。5-6百万的交易量短暂的把价格拉升到 USD 20.9 / BTC 0.0058，平日交易量一般为0.8-1.2百万。注意交易量数据并不是可靠的指标。

## 相关外部信息

Vertcoin (VTC) 受到51%[攻击](https://medium.com/coinmonks/vertcoin-vtc-is-currently-being-51-attacked-53ab633c08a4)，在4个事件中发生22次重组及15次双花，受害者损失大约 100,000美元。这再次肯定了某些币种容易受到矿工的攻击。这些币种不是矿机主要挖掘对象(GPU挖矿或抗ASIC，也包括比特币分叉币)，矿工只需要有合适的硬件及没有兴趣维护主链就可进行攻击。这些攻击的影响之一是货币被认为是不安全的，因为它曾经失败了。任何仍愿意接受它的人在确认转移可能有非常多的确认数量要求，使得货币交易缓慢。

[Horizen(之前为zencash)](https://www.horizen.global/)团队最近发布了[战略调整](https://blog.zencash.com/re-strategic-actions-for-horizen-from-rolf-versluis/)调整财政部区块奖励额，从10% 增加到20%，减少矿工的奖励金额。在币价跌了90%，及人员和其他成本大幅减少后，更进一步的削减成本将危机项目运行。由于IOHK开发的财务系统仍然在[原型阶段](https://blog.zencash.com/dao-prototype/)和为准备好使用，团队认为有必要单方面决定更改区块奖励。

EOS区块生产者[开始支付](https://cointelegraph.com/news/eos-node-offers-users-financial-rewards-for-votes-reignites-decentralization-debate)把票投给他们的持币者。

Aragon治理提案(AGPs)第一轮投票由于以太坊君士坦丁堡硬分叉造成潜在网络不稳定原因被[推迟](https://forum.aragon.org/t/agp-vote-delay-announcement/426) - 希望“区块链由于维护原因而关闭”不是Politeia会遇到的Decred问题。Aragon Association(Aragon协会)的CEO在提案提交开启前[发布](https://forum.aragon.org/t/agp-wishlist-and-blacklist/355)了提案的黑名单及愿望清单。在AGP[流程](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-1.md)的第一个提案在99.97%同意票数的[通过](https://blog.aragon.org/final-results-from-the-agp-1-vote/)。总共2.6%的ANT代币，从45个独特地址在第一个提案中投票。在48小时投票期开始前，AGPs通过了Aragon协会董事会及社区审核。

200万枚BTCP通过漏洞被开采并在CoinMetrics注意到供应有问题作出[调查](https://coinmetrics.io/bitcoin-private)前并没有被发现。开发团队[发布]（https://medium.com/@bitcoinprivate/official-statement-on-coinmetrics-report-6f1cef176c05) 正式声明确认该漏洞。该漏洞在1月5日一个赏金猎人的补丁中被合并，该赏金猎人在收到工作奖励后离开。一行缺失的代码对网络的价值造成了巨大的破坏。我们可以从这个不幸的经历中学习很多：广泛的测试覆盖率，对共识代码的严格审查，在关键任务部分工作的开发人员建立的声誉，以及协议的多个实现对于构建我们可以投以资金信任的系统非常重要。

比特币的Electrum在基础设施上受到了[攻击](https://www.reddit.com/r/CryptoCurrency/comments/a9yji3/electrum_wallet_hacked_200_btc_stolen_so_far/)。 有人启动了一堆恶意的Electrum服务器，促使用户“升级”到恶意软件版本并窃取200多个BTC。Electrum模型涉及位于客户端和完整节点之间的服务器网络。每个客户端依赖它们连接的服务器，这会损害用户隐私，因为这些服务器的所有者可以推断出用户拥有的钱包。如果Electrum服务器遭到破坏，这将会打开一些额外的攻击。Decred选择不开发类似Electrum的基础设施，而是直接进行客户端过滤。 这延迟了轻客户端的开发，但现在在dcrwallet，Decrediton和drcandroid中工作的SPV模式独立于任何服务提供商，并因此增强了用户的隐私。

安全研究人员[演示](https://media.ccc.de/v/35c3-9563-wallet_fail)如果实际拥有该设备，可以以多种方式破解最流行的硬件钱包。

最新[blockchaintransparency.org](https://www.blockchaintransparency.org/)的交易量报告得出的结论是，coinmarketcap.com排名前25位的与BTC对中，超过80％的交易量是洗牌交易。另一个难过的发现是，平均项目花费超过50,000美元的上市费用。该报告激发一些了分析DCR的交易量的[想法](https://github.com/xaur/decred-issues/issues/34)。

Coinbase通过[注册商标](https://www.coindesk.com/coinbase-wants-to-own-buidl-trademark-filing-reveals
)拥有“BUIDL”一词。

很多加密货币服务及团队似乎由几个实体拥有或共同拥有 https://twitter.com/tangleblog/status/1068094875533479937

多个中心化交易所在年度[Proof-of-Keys](https://www.proofofkeys.com/)活动中[无法提供提款](https://www.ccn.com/several-exchanges-said-to-be-failing-bitcoin-ownership-event/)  

Slack不小心[屏蔽](https://www.engadget.com/2018/12/22/iran-sanctions-slack/)了一些到过伊朗的用户。后来Slack对此[道歉](https://slackhq.com/an-apology-and-an-update)并作出了澄清。但这并不意外而且非常明显Slack 科技是个([风投资助](https://en.wikipedia.org/wiki/Slack_Technologies))符合美国法律的公司。相反的Matrix 聊天室可以通过多个服务器联合，因此即使某些参与的服务器关闭，其他管辖区域中的服务器也可以继续运行并保留历史记录。

12月中媒体报道了[多篇](https://www.wsj.com/articles/layoffs-become-the-latest-thing-in-cryptocurrency-1544471449)关于[加密货币行业](https://www.newsbtc.com/2019/01/09/cryptocurrency-shapeshift-layoffs/)的[裁员](https://www.businessinsider.com/bitmain-layoffs-2018-12)新闻。(也有报道指出相比其他行业并[没有这么严重](https://cointelegraph.com/news/better-than-corporations-layoffs-in-crypto-are-on-the-rise-still-lower-than-in-other-industries))。从上述Horizen的情况及一些Dash[社区讨论](https://www.reddit.com/r/dashpay/comments/ac9ca4/dash_nigeria_defunding_statement_and_path_forward/)看出其他拥有基金会的项目也同样正渡过难关。我们必须对在Politeia出现前管理基金会并保持健康的余额的团队表示感激，这是Decred在其他项目萎缩的时候仍然在发展扩大团队。12月的DCR价格以 17.50美元计算，将是基金会第一次花费大于收纳的月份。就算DCR/USD 汇率保持低迷，基金会仍然有能力可以保持目前的美金开销金额（略算为8年）。

[据称](https://cointelegraph.com/news/reports-bitmain-allegedly-fires-all-bch-developers-in-wave-of-redundancies)在这波加密领域大裁员中，比特大陆裁退了所有比特现金的开发团队，当中也包括了Copernicus团队。

[Copernicus](https://github.com/copernet/copernicus)用Go编写了比特币现金协议的一个实现，当中也使用了btcsuite。软件预发布版本在12月[发布](https://news.bitcoin.com/an-alternative-client-has-mined-bitcoin-cash-block-558847/)并挖采了首个区块。作者在网站中[感谢](https://www.copernicuscore.org/btcd.html)btcsuite开发者并对他们在比特币生态系统的贡献表示[肯定](https://www.copernicuscore.org/btcd.html)。Copernicus团队在博客里[表示](https://medium.com/@copernicusbit/the-copernicus-project-launched-the-pre-release-v0-0-6-dc572a924214)该软件“把原本的客户端软件架构重新组合和设计，以让整体架构更简洁，降低开发人员的学习难度并增加了多样的客户端以确保BCH网络的安全”。

Copernicus并不是第一个尝试多样化比特现金网络的团队。比特币现金已经有多个C++，Rust及JavaScript实现在开发过程中。在9月份，另外也[宣布](https://news.bitcoin.com/developers-unveil-two-new-bitcoin-cash-full-node-clients-written-in-go/)了两个用Go写的比特现金实现。[Gocoin-cash](https://github.com/CounterpartyXCPC/gocoin-cash)是[counterparty.cash](http://counterparty.cash/)团队基于[gocoin](https://github.com/piotrnar/gocoin) (另一个Go语言的比特币全节点实现)开发的。而[bchd](https://github.com/gcash/bchd)则是由OpenBazaar开发人员 [Chris Pacia](https://github.com/cpacia)主领。在bchd的最初[公告](https://www.yours.org/content/introducing-bchd-aee6a07feb00)中Chris表示btcsuite“是设计和写的最好的比特币代码之一”并解释相比C++的实现，他允许更多开发人员参与及更快速的开发新功能。同时这也给了他们“免费”的客户端隐私SPV。beta在11月[公布](https://medium.com/@bchd.cash/bchd-beta-release-46f89c677c47)，并从btcd分叉两个月内把贡献人数增加到9人和实现了多项btcd改进。

对于Decred的相关性和好消息是，更多的开发人员开始研究btcsuite代码库，而Decred同样基于该代码库也可以从中受益。

## 关于月报
12月为英文第9期[GitHub](https://xaur.github.io/decred-news/journal/201812)月报。 点击[这里](https://xaur.github.io/decred-news/)浏览往期月报。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues)和[Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

## 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)
