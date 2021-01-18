# Decred月报 – 2020年12月

![abstract art](img/journal-202012-384.png)

_图片: @saender_

祝大家新年快乐！

十二月的亮点：

- 经过一个月的完善，v1.6确实看起来更棒了。候选版本5准备发行。
- 链上数据在12月变得很疯狂，包括选票价格大幅上涨至191 DCR。
- 社交媒体指标也在迅速发展，推特@decredproject追踪数突破了关键阻力位。
- DCR从Upbit退市，导致价格飙升，保证金交易被添加到其它几家交易所。

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以构建和运行的源代码中，但对于普通用户来说，还不能使用。

**[dcrd](https://github.com/decred/dcrd)**

合并在主版本中，并反向移植到v1.6：

- 更正了[费用计算](https://github.com/decred/dcrd/pull/2530)，以修复某些交易在某些重组方案中被视为较低优先级的交易
- 将DCP-5[违规](https://github.com/decred/dcrd/pull/2533)列入白名单。由于已修复了bug，当大多数网络已升级到版本7时，旧版本6会接受5个块。这些块原本是有效的，现在已列入白名单，以允许完全同步链而无需检查点

合并到主存储库：

- 将[上下文检查](https://github.com/decred/dcrd/pull/2481)从健全性/位置功能移动到适当的位置，以恢复在去中心化国库支出工作之前的预期限制。这些将是必要的解耦块处理顺序从下载顺序。
- 改变了主链[区块缓存](https://github.com/decred/dcrd/pull/2488)语义，减少了对块数据显示顺序的依赖
- 将数据块管理器提取到其自己的[`netsync`](https://github.com/decred/dcrd/pull/2500)程序包中，以提高其可测试性，并从共识验证中更清晰地拆分与网络的同步
- 对[对等](https://github.com/decred/dcrd/issues/1145)区块下载的其它一些更改
- 添加了挖矿[测试工具](https://github.com/decred/dcrd/pull/2480)，可以更轻松地添加测试范围并帮助优化块模板生成代码
- 更改了RPC服务器[身份验证](https://github.com/decred/dcrd/pull/2486)，以使用HMAC-SHA256以及每次启动时唯一的随机密钥来加强对某些类的内存转储攻击的能力
- 更多[rpcserver](https://github.com/decred/dcrd/issues/2069)测试范围
- 更新了多个位置以遵循错误处理[最佳试验](https://github.com/decred/dcrd/issues/2181)
- 全面的代码更改和测试更新

总共[合并了](https://github.com/decred/dcrd/pulls?q=is%3Apr+merged%3A2020-12-01..2020-12-31+sort%3Aupdated-asc)来自6个贡献者的51个PR和92个提交，添加了10K行和删除了8K行代码。

**[dcrwallet](https://github.com/decred/dcrwallet)**

- [随机选择](https://github.com/decred/dcrwallet/pull/1937)硬币以支付VSP费用（这也可以重试并完成一些以前总是失败的VSP票证购买）
- 固定的[未发布](https://github.com/decred/dcrwallet/pull/1941)输出用于为其他交易提供资金（与VSP费用保持一致，直到票证与VSP一起提交时才处于未发布状态）
- 代码重构

进行中：

- 能够[导入](https://github.com/decred/dcrwallet/pull/1945)来自其他种子的投票帐户（支持Trezor赌注）

**[Decrediton](https://github.com/decred/decrediton)**

- 添加了混合[所有资金](https://github.com/decred/decrediton/pull/3041)的按钮
- 添加了v1.6的[版本说明](https://github.com/decred/decrediton/pull/3048)和动画图像
- 更新翻译（阿拉伯语，中文，德语，日语，意大利语，波兰语，西班牙语）
- 〜23个修复和UI调整

发布rc5很可能解决一些剩余的问题。

**[Politeia](https://github.com/decred/politeia)**

- 删除了公共路线上的[CSRF](https://github.com/decred/politeia/pull/1356)，以防止CSRF令牌链接点滴投票的可能性。对隐私的影响最小：将CSRF令牌链接到点滴投票将需要编写其他代码，因为所使用的CSRF库不会自动完成。
- 用于提案[编辑](https://github.com/decred/politeiagui/pull/2227)的端到端UI测试
- 删除了烦人的注销模式，并将很少使用的“永久注销”功能移至“帐户”选项卡
- [验证](https://github.com/decred/politeia/pull/1355)选票的新`politeiavoter`命令
- CMS发票处理和查看的UX改进
- Politeia和CMS的bug修复

来自@lukebp的tlog集成更新：

> 添加了检索用户提交的任何数据的完整时间戳（包含证明）的功能。为此的前端工作仍在进行中。后端tlog分支现已完成功能，我们将开始代码审查过程。

**[vspd](https://github.com/decred/vspd)**

- 拒绝重用或旧[时间戳](https://github.com/decred/vspd/pull/215)
- 数据库代码的更多测试范围
- v1.0版本的较小修复程序和其它准备工作

**[dcrpool](https://github.com/decred/dcrpool)**

- [单独挖矿](https://github.com/decred/dcrpool/pull/274)节点
- 将[客户端信息](https://github.com/decred/dcrpool/pull/293)保存在数据库中，并使其在任何dcrpool实例上可用
- 支持NiceHash池[验证器](https://github.com/decred/dcrpool/pull/294)（允许它连接到dcrpool并查询基本统计信息）

**[dcrdex](https://github.com/decred/dcrdex)**

- 新的[最大订单](https://github.com/decred/dcrdex/pull/842)按钮，可根据市场，市场面和钱包余额以最大数量填充数量字段
- 通过HTTP和WebSockets公开[市场数据](https://github.com/decred/dcrdex/pull/796)API端点
- 显示每个DEX服务器的[帐户ID](https://github.com/decred/dcrdex/pull/825)
- 支持为BTC订单提供资金的[已确认](https://github.com/decred/dcrdex/pull/865)产出
- 从数据库中[恢复](https://github.com/decred/dcrdex/pull/856)交换程序（比以前的方法更好，代码更少）
- 允许应用监听[IPv6](https://github.com/decred/dcrdex/pull/899)地址
- 改善颜色以区分买卖订单
- 许多bug修复和依赖项升级

来自7个贡献者的28个PR进行了[合并](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-12-01..2020-12-31+sort%3Aupdated-asc)，增加了8K行以及删除了5K行代码。

修补程序版本[v0.1.4](https://github.com/decred/dcrdex/milestone/10)即将关闭。

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

- [提取](https://github.com/planetdecred/dcrandroid/pull/523)cfilter时的通知
- bug修复

合并到dcrlibwallet共享库中：

- [vspd](https://github.com/planetdecred/dcrlibwallet/pull/163)支持
- 查询有关已连接的SPV[对等节点](https://github.com/planetdecred/dcrlibwallet/pull/160)的信息的方法
- 依赖项升级和bug修复

请注意，假设这些应用程序添加了必要的UI，添加到dcrlibwallet的功能将可供dcrandroid，dcrios和godcr使用。

**[dcrios](https://github.com/planetdecred/dcrios)**

- XCUI在某些情况下[自动](https://github.com/planetdecred/dcrios/pull/707)进行UI测试

**[godcr](https://github.com/planetdecred/godcr)**

- [投币](https://github.com/planetdecred/godcr/pull/261)选择界面
- 复制文本或创建交易时的[通知](https://github.com/planetdecred/godcr/pull/274)
- [钱包](https://github.com/planetdecred/godcr/pull/276)主页面的新UI设计
- 用户界面调整
- bug修复和优化

需要使用用于覆盖小部件的API才能完全实现Godcr的预期设计。这引起了Gio团队的注意，并被视为优先事项。

**[dcrros](https://github.com/decred/dcrros)**

- [脱机模式](https://github.com/decred/dcrros/pull/14)支持以完全满足[Construction API](https://www.rosetta-api.org/docs/construction_api_introduction.html)的规范，其中某些操作仅在脱机实例中执行

**[decred.org](https://github.com/decred/dcrweb)**

- 删除[无效](https://github.com/decred/dcrweb/pull/935)的贡献者
- 依赖升级

其他：

- Electric Capital的研究人员已在Decred生态系统中绘制了大多数[存储库](https://www.reddit.com/r/decred/comments/k9g76v/decred_developer_ecosystem_repositories/)，并构建了可视化其活动的工具

## 人员

欢迎新到来的首次贡献者，他们的代码已合并到主代码库中： @piotrdelikat ([decrediton](https://github.com/decred/decrediton/commits?author=piotrdelikat))!

截至1月2日的社区统计数据：

- Twitter 粉丝: 41,320 (+423)
- Reddit 订阅: 10,051 (+69)
- Matrix #general 用户: 287 (+34)
- Discord 用户: 1,723 (+222)
- Telegram 用户: 2,338 (-1)
- YouTube 订阅: 4,300 (+50), 观看量: 165K (+3K)
- LinkedIn 粉丝: 944 (+12)
- GitHub dcrd 星星: 570 (+3), 叉: 247 (+1)

我们[跟踪](https://github.com/decredcommunity/social-media-stats)的统计数据有几个要点：

- [@decredproject](https://twitter.com/decredproject) Twitter打破了41K的粉丝，增加了+423
- [Reddit](https://www.reddit.com/r/decred/)突破1万个订阅
- [Discord](https://discord.gg/GJ2GXfz)提高14％
- [DecredTrading](https://t.me/DecredTrading) Telegram的用户数增加了72％，达到158位（上帝帮助我们）
- [@Checkmate](https://twitter.com/_Checkmatey_)得到了+ 11％的关注者（达到3.5K）并发出了1K的推文（〜34 /天）
- [DecredES](https://t.me/DecredES) 上涨+ 18％（至245）
- [CoinMarketCap](https://coinmarketcap.com/currencies/decred/)有17.8K的关注量

感谢Decred在所有平台上的贡献者提高了对该项目的认识！

## 治理

十一月[国库](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到12099 DCR，花费7466 DCR。按照9月份的每日平均DCR/USD汇率31.07美元计算，这是37.6万美元的收入和23.2万美元的支出。按11月平均汇率18.19美元计算，当月完成工程的美元账单金额为13.6万美元。截至1月5日，社区开发基金余额为641260 DCR（3020万美元，47.16美元）。

在12月提交了两个提案并进行了投票：

- Decred ES团队的第三项[提案](https://proposals.decred.org/proposals/350f64b)要求14,800美元用于资助六个月的工作，从最初的要价42,000美元缩减到与Talent Land Blockchain Challenge和Codigo Decred有关的项目。该提案以54.5％的赞成票被否决，但未能达到60％的门槛-投票率为37％。
- 在削减了LATAM市场营销[提案](https://proposals.decred.org/proposals/5ce1636)的hackathons元素之后，提交了Decred Hackathons和LATAM Initial Chapter提案，其背后的人是ES团队的成员。该提案要求最高预算为17,000美元，用于创建黑客马拉松的材料并运行两次黑客马拉松，其中3,500美元的预算用于奖励奖品。该提案以50.2％的赞成票和36％的投票率被拒绝。

12月是美国，拉美和巴西市场营销提案的最后一个可计费月份。为他们工作的承包商将需要提交续约提案以保持资金。

@JoeGruff为他的地址扫描器建议发布了三个简短的进度和费用[更新](https://github.com/decredcommunity/proposals/tree/master/proposals/3943bff/updates)。

尽管12月对于提案来说是一个安静的月份，但是1月已经有两个新的提案，用于[DCRDEX](https://proposals.decred.org/proposals/d462ac3)和[Decred in Depth](https://proposals.decred.org/proposals/391108e)的新资金（在新的管理下）。

Politeia Digest在12月休息了一段时间，但很快就会回来。

## 网络

全网算力: 11月[哈希率](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=ki3ivfpm-kjej4ggy&scale=linear&bin=block&axis=time) 以292 Ph/s开启并以 340 Ph/s结束。月内，最低为240 Ph/s，峰值为452 Ph/s。[哈希率分布](https://miningpoolstats.stream/decred) 截至1月1日：UUPool 42%, Poolin 35%, easy2mine 12%, F2Pool 3.9%, Antpool 2.7%, Huobipool 2.6%, BTC.com 1.3%, Luxor 1.2%, CoinMine 0.02%。

Staking: [30天平均票价](https://dcrstats.com/)为 163.9 DCR (+5.2). [票价](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=ki3ivfpm-kjej4ggy&axis=time&visibility=true-false&mode=stepped)在150.6-190.99 DCR之间变化。[锁定金额](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=ki3ivfpm-kjej4ggy&scale=linear&bin=block&axis=time)为642-668万DCR，相当于参与PoS的[可用供应量](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=ki3ivfpm-kjej4ggy&scale=linear&bin=block&axis=time)的52.01-54.20%。

又高了。门票价格达到DCR 190.9的峰值，锁仓比例达到54.2％。

节点：整个12月，每个dcr.farm平均有87个公共侦听节点，总共200个节点。12月的平均版本分布：27％dcrd v1.5.2、21％dcrd v1.6开发人员和RC版本，16％dcrd v1.5.1、5％dcrd v1.7开发人员版本，5％dcrd v1.5.0、3％dcrd v1.5开发人员和RC版本，0.7％dcrd v1.4、10％dcrwallet v1.5.1、1.3％dcrwallet v1.6开发人员和RC版本，1％dcrwallet v1.5、0.7％dcrwallet v1.4、9％其它。

@Checkmate通过[我们的网络](https://ournetwork.substack.com/p/our-network-issue-50-part-2)新闻报道说，许多链上指标都达到了历史新高。

@PermabullNino报告说，在28天内，票池余额的DCR[增加](https://twitter.com/PermabullNino/status/1338497116864438273)了约500K 。

Mainnet闪电网络正在缓慢增长。整个2020年，平均有15个节点，30个通道和6个DCR容量。截至1月8日，根据@jholdstock的[LN地图](https://ln-map.jamieholdstock.com/)，共有24个节点，42个通道，总容量为8.7 DCR 。

## 整合

[Ultravsp](https://ultravsp.uk/)（以前是Ultrapool）和[Ubiq](https://dcrvsp.ubiqsmart.com/) VSP都已启动了新的[vspd](https://github.com/decred/vspd)投票软件的主网实例。他们的[dcrstakepool](https://github.com/decred/dcrstakepool)服务器将分别继续在[legacy.ultravsp.uk](https://legacy.ultravsp.uk/)和 [dcr.ubiqsmart.com](https://dcr.ubiqsmart.com/)上运行。

请注意，由于英国脱欧造成域名混乱，Ultravsp必须从ultrapool.eu迁移到英国域[ultravsp.uk](https://ultravsp.uk/)，并且由于设置它的过程过于繁琐，因此不会进行自动重定向。最近通过电子邮件通知了购买票的VSP用户。

Bittrex[添加](https://twitter.com/BittrexExchange/status/1341801493964308482)了即时交换功能，该功能使用户可以使用借记卡或交易所的法定余额快速购买资产。据报道DCR交易可以进行。

Binance已启用DCR / BTC和DCR / USDT的保证金交易，并宣布了为期1周的“借入DCR的零利率促销”。([讨论](https://www.reddit.com/r/decred/comments/k8gy0d/margin_trading_for_dcr_enabled_on_binance/))


[MXC交易所](https://www.mxc.com/)  在2019年列出的常规DCR / USDT对之外，MXC Exchange还[增加](https://twitter.com/MXC_Exchange/status/1334707659900035075)了5倍杠杆保证金交易DCR / USDT对。

土耳其交易所[Bitexen](https://www.bitexen.com/) 宣布DCR在其他11种资产中[上市](https://destek.bitexen.com/portal/tr/kb/articles/bitexen-11-adet-yeni-coin)。

总部位于马耳他的即时交换聚合服务商[Swapzone](https://swapzone.io/)自5月或更早就开始提供DCR支持，但是在12月，它受到了我们的关注，并添加到decred.org[交换](https://decred.org/exchanges/)页面。

Korean Upbit已将DCR[移除](https://www.reddit.com/r/decred/comments/kfu4sb/whats_going_on_in_korea_upbit/)，显然与Decred保护个人隐私的使命背道而驰。

警告：Decred Journal的作者不了解上述任何服务的可信赖性。在将您的个人信息或资产信任给任何实体之前，请先进行自己的研究。

## 外展活动

Decred西班牙团队发布了他们的第二份提案的最终[第六份报告](https://github.com/decredcommunity/proposals/blob/master/proposals/3c02b67/updates/20201211.md)。第3项提案的投票以54.5％和50.2％的赞成票结束，但未达到要求的60％门槛。该团队正在收集有关Reddit的[反馈](https://www.reddit.com/r/decred/comments/kkb97s/what_are_your_thoughts_on_the_decred_in_spanish/)，并计划下一步的工作。

@ michae2xl发布了最终[报告](https://github.com/decredcommunity/proposals/blob/master/proposals/bc20f98/updates/20210105.md)，该报告涵盖了巴西市场营销提案的12月活动。

Monde PR在12月成就：

- 创造并推销了两个故事创意，以资助和加密出版物

Monde PR保证的新闻报道：

- [NASDAQ Trade Talks](https://www.nasdaq.com/videos/tradetalks:-how-can-blockchain-can-be-used-in-elections)对@ jy-p进行了采访，谈到Decred在巴西大选中的用途。随后的[Coin Journal](https://coinjournal.net/news/decred-bounces-off-42-after-spiking-50/), [Crypto Potato](https://cryptopotato.com/decred-dcr-pumps-50-as-social-sentiment-surges/), [Coin Market Cap](https://coinmarketcap.com/headlines/signals/decred-co-founder-on-nasdaq-tradetalks-decred/)和[CryptoMode](https://cryptomode.com/5-reasons-why-you-shouldnt-overlook-decred-dcr/)中提到了采访。
- 在DCRDEX发布和Decred在巴西选举使用的细节在功能[Cointelegraph](https://cointelegraph.com/news/bitcoin-bull-market-pulls-kusama-ksm-decred-dcr-and-qtum-price-higher)
- @ jy-p受到[Geek Insider播客](https://www.youtube.com/watch?v=mYK_Awn1wTk)的采访，谈论Decred的起源，DCRDEX的发布以及Decred在巴西大选中的使用
- [Brave New Coin](https://bravenewcoin.com/insights/decred-price-analysis-active-addresses-hit-all-time-highs-as-trend-metrics)介绍了DCRDEX发布的详细信息
- @ jy-p的Cointelegraph访谈中有关比特币牛市和熊市周期的评论在[Forex Academy](https://www.forex.academy/how-to-spot-bitcoin-bull-bear-cycles-beginners-edition/)和[Inside Bitcoin](https://insidebitcoins.com/news/bitcoin-btc-price-prediction-november-29-2020-2)发表
- @ jy-p对Ledger的安全挑战的评论发表在[The Union Journal](https://www.theunionjournal.com/ledger-cto-discusses-wallets-safety-after-multiple-security-setbacks/)
上

## 活动

参加：

- 12月3日 - [Hablemos Decred 24](https://decredcommunity.github.io/events/index/20201203.1) - 互联网。@elian和@pablito讨论了私有加密货币的情况。
- 12月5日 - [World Blockchain Conference](https://decredcommunity.github.io/events/index/20201205.1) - 中国武汉。没有正式的Decred活动，但@Dominic在Cobo Wallet，F2Pool等网站与老朋友会面，向他们介绍即将推出的v1.6和新的共识规则。
- 12月10日 - [Hablemos Decred 25](https://decredcommunity.github.io/events/index/20201210.1) - 互联网。西班牙团队的代表聚集一堂，对在DAO工作1年进行了回顾，总结了DAO的好，坏，挑战以及2021年的未来。
- 12月11日 - [Cripto Latin Fest Online 2020](https://decredcommunity.github.io/events/index/20201211.1) - 互联网。Paxful Latam协办。Decred是VIP赞助商。@elian介绍了Decred和即将推出的Hidden Hydra的常见话题，在Facebook上的观看次数为1.6千，在YouTube上的观看次数约为800。在另一个小组中，他谈到了如何防止加密骗局。
- 12月16日 - [UAM Xochimilco](https://twitter.com/addcade/status/1338544856344317953) - 墨西哥墨西哥城。@adcade在UAM霍奇米尔科大学的Aula多媒体实验室中讨论了Decred的组织和礼节。
- 12月18日 - [New Year at CR!](https://decredcommunity.github.io/events/index/20201218.1) - 互联网。加密资源学院组织了一次年终活动，邀请了Decred，Bitso，Prime XBT DAI，Binance等合作伙伴。在治理小组会议上，@ elian介绍了Decred治理的工作方式，POLITEIA的作用和财政部的权力下放。
- 12月24日 - [Decred AMA](https://decredcommunity.github.io/events/index/20201224.1) - 互联网。西班牙社区中的OKEx AMA在其Telegram上进行了约500位用户。有关Decred的治理，隐私，未来发展，历史和DEX的问题超过30个。还有一个DCR赠品（OKEx提供20美元，西班牙语Decred提供30美元）。超过30个新成员加入了@DecredES频道。
- 12月30日 - [Decred in Spanish New Year Giveaway](https://decredcommunity.github.io/events/index/20201230.1) - 互联网中有所下降。要参与，人们需要加入@DecredES Telegram，并告诉他们他们对Decred的看法。在28条评论中，根据对项目的了解和理解，选择了9条最佳评论，总共获得了3条DCR。

上面的信息可在我们的[活动跟踪器](https://decredcommunity.github.io/events/index/)中更详细地获取，该事件跟踪器旨在了解有效的方法并改进营销工作的报告。感谢大家提交和审阅活动。

## 媒体

@mm完成了他的有关区块链治理的7部分系列文章：

- [1](https://stakey.club/en/blockchain-gov-part1/) 介绍加密货币，货币印刷和比特币
- [2](https://stakey.club/en/blockchain-gov-part2/) 介绍了加密货币，工作量证明安全性，激励措施和通货膨胀背后的技术
- [3](https://stakey.club/en/blockchain-gov-part3/) 介绍了基本架构类型（免许可/许可，公共/私有），比特币治理，隐私和可替代性以及数字货币以外的区块链应用（尤其是电子投票）
- [4](https://stakey.club/en/blockchain-gov-part4/) 介绍Decred Project的基础知识（安全性，共识性，资金，游戏中的皮肤）并将其与纯PoW和PoS方法进行比较
- [5](https://stakey.club/en/blockchain-gov-part5/) 使用@mm的InvalidationGame攻击模拟器评估了比特币与Decred的区块链安全性和治理，并考虑了外部和内部攻击。除其他细节外，它提供了攻击比特币和Decred所需的资本支出和运营支出的单独估算。
- [6](https://stakey.club/en/blockchain-gov-part6/) 测试了针对真实数据的许多假设（主题包括链上指标与价格，选民投票率，OLS模型等的相关性）
- [7](https://stakey.club/en/blockchain-gov-part7/) 通过总结模拟结果，有关安全性的发现以及Decred可以为世界提供的内容来总结该系列

> Decred Project不仅旨在为依赖可信赖的第三方的金融系统和依赖大型金融机构的善意的人们提供替代方案，而且还展示了如何以安全透明的方式进行电子投票。

研究中使用的Python / R / SQL代码可在[GitHub](https://github.com/mmartins000?tab=repositories)上获得。

精选文章：

- Decred价格分析 - 活跃指标创下历史新高，因为趋势指标被Josh Olszewicz([bravenewcoin.com](https://bravenewcoin.com/insights/decred-price-analysis-active-addresses-hit-all-time-highs-as-trend-metrics))）看涨-带有[视频](https://www.youtube.com/watch?v=oCYZS_qJ7us)版本

视频:

- Decred 双周报 - 修改了隐私页面，大量开发人员更新，1.6入站等等！@Exitus ([youtube](https://www.youtube.com/watch?v=-3s9_jMWNuA))
- 价格年度新高 Decred Society ([youtube](https://www.youtube.com/watch?v=qw-ohbTObeo))
- Decred 非常适合储蓄用户 Decred Society ([youtube](https://www.youtube.com/watch?v=zYDT0n59C7k))
- Decred加密分析 DubDigital ([youtube](https://www.youtube.com/watch?v=kqAD_PSgyME))
- ake Yocom-Piatt在Geek Insider上谈论Decred和区块链 ([youtube](https://www.youtube.com/watch?v=mYK_Awn1wTk))
-区块链如何在选举中使用？与纳斯达克TradeTalks的Jake Yocom-Piatt和Jill Malandrino ([youtube](https://www.youtube.com/watch?v=pBSn_CdQYts))
- Staked Podcast对@BTC_Uncle的采访 ([youtube](https://www.youtube.com/watch?v=__7LTz3nQKk))
- Staked Podcast对Ammar Naseer（@Ammarooni）的采访([youtube](https://www.youtube.com/watch?v=g0bFMuHXrkU))
- @Checkmate的2020年onchain封闭会议BTC + DCR([youtube](https://www.youtube.com/watch?v=g60ovCl54OA))
- Decred Deep Dive：隐藏的hydra释放即将到来！由@Checkmate([youtube](https://www.youtube.com/watch?v=3AxBa-EE8RM), [discussion](https://www.reddit.com/r/decred/comments/klz8ue/decred_deep_dive_hidden_hydra/))

音频:

- Rough Consensus 14: 重塑牛市。@Checkmate和@PermabullNino分享了他们对比特币ATH，ETH 2.0，DCR 1.6等的想法。 ([libsyn](https://roughconsensus.libsyn.com/episode-14-rehashing-bull-market-happenings))

艺术/娱乐：

- 爆笑Decred [GOT cover](https://streamable.com/iam635) @degeri
- @ aithzakaria1的“他们[不知道](https://twitter.com/aithzakaria1/status/1335706207395450880)我已经拒绝了”
- 现在是Decred的[时间](https://twitter.com/aithzakaria1/status/1330999761634258948)了，Ben！@ aithzakaria1
- 适应生存- @OfficialCryptos设计的[商品](https://twitter.com/OfficialCryptos/status/1338551937818562561)
- DCR[暴力切断](https://twitter.com/exitusdcr/status/1343774006344880130)CMC@Exitus
- @AGNFAB的[数字国家状态](https://twitter.com/AGNFAB1/status/1338963085537718275)
- @New_Copernicus在[Hidden Hydra](https://twitter.com/New_Copernicus/status/1336044535370092546), [Decred Rabbit Hole](https://twitter.com/New_Copernicus/status/1339649654842126337), cheerful [Happy Holidays!](https://twitter.com/New_Copernicus/status/1341665478935076865)和[Happy New Year!](https://twitter.com/New_Copernicus/status/1344509258176622593)上分享了更多预告片！和新年快乐！

翻译：

- 阿拉伯语翻译：“ decred：一切从哪里开始？” 发布在[satoshiat.com](https://www.satoshiat.com/2020/12/%d8%a7%d9%84%d8%af%d9%8a%d9%83%d8%b1%d9%8a%d8%af-%d9%85%d9%86-%d8%a3%d9%8a%d9%86-%d8%a8%d8%af%d8%a3%d8%aa%d8%9f/)加密专用网站上。
- 一般的“加密资产的实用性”和更技术性的“数字钱包的安全性增强”和“验证数字签名：拒绝”，由@francov_译成西班牙文（请参见西班牙语[翻译库](https://github.com/DecredES/traducciones)及其媒介）
- 2020年11月的Decred月报被[翻译成](https://xaur.github.io/decred-news/)阿拉伯文（@ arij，@ abdulrahman4），中文（@Dominic）和西班牙文（@francov_）。谢谢大家传播Decred月报！
- 截至撰写时，[该索引中](https://github.com/decredcommunity/translations/blob/master/index.md)已跟踪305项所有已知译文

其它非英语内容：

- “Decred的加密货币增加了50％，超过了DeFi硬币” ([es.cointelegraph.com](https://es.cointelegraph.com/news/the-decred-cryptocurrency-increased-by-50-and-surpassed-defi-coins))
- @arij用阿拉伯语大大改进的Decred简介([youtube](https://www.youtube.com/watch?v=k6xXL_ttSDI))

## 社区讨论

精选Reddit帖子：

- 在DCRDEX上添加[ERC-20](https://www.reddit.com/r/decred/comments/khnc35/adding_erc20_to_the_dex/)
- 权衡隐私权功能的[取舍](https://www.reddit.com/r/decred/comments/k6dn93/what_are_the_trade_offs_for_decreds_privacy/)
- 从[VSP运营商](https://www.reddit.com/r/decred/comments/k9hegy/upcoming_changes_in_16_for_proofofstake_using_vsps/)的角度来看，即将对VSP系统进行更改的好处

精选的Twitter讨论：

- @Ammarooni提醒您，12月15日是Decred在bitcointalk论坛上首次[宣布成立5周年](https://twitter.com/Ammarooni/status/1338898342722605057)。
- 简短的[历史](https://twitter.com/lefebvre_dustin/status/1333816694922485761)记录，Decred如何在不使用Oracle的情况下进行编码@Dustorf

## 市场

12月DCR美元交易价格为24.01-41.59 USD，BTC价格为0.0012-0.002之间。每日平均价格为$31.07。

DCR的交易异常的Upbit高达$ 3,500，直到它被下架。

在DCRDEX[开启交易](https://ournetwork.substack.com/p/our-network-issue-50-part-2)的48天中，DCR的交易量约为60万，相当于同期Binance交易量的30％。但是，与任何集中式交易所不同的是，该交易量更加真实可靠。

@bochinchero在Decred上[发布](https://twitter.com/TheBochinchero/status/1339202616153284608)了他的第一篇链上分析文章，提出了新的评估指标：

> 抵押的已实现价值是一种类似于已实现价值的度量标准，但仅适用于选票池中流通的硬币，本质上将每张选票视为UTXO。[它]提供对锁定在网络安全性和治理中的资金的更准确评估。在过去的急剧抛售中，它充当了心理触底-最大痛苦的点，最后的买家介入其中。

@Checkmate宣布[启动](https://twitter.com/_Checkmatey_/status/1338418991212052485)[checkonchain.com](https://checkonchain.com/)，其中包含许多图表（许多图表）：

> 这是我已经从事很长时间的工作了。如果您想在这个市场上占据优势，请关注它。不久之后，将全面讨论如何正确应用每个指标。

## 相关外部信息

Cover Protocol是一个DeFi保险项目，旨在“保护DeFi用户免受智能合约风险的侵害”，遭到黑客攻击，攻击者铸造了40亿个COVER代币，以400万美元的价格清算了这些代币，但随后将资金返还给了智能合约。该团队现在正在考虑使用快照创建一个新版本的COVER令牌，以退还COVER持有人，因为否则，那多余的40亿个令牌会破坏令牌系统。

攻击者诱使Nexus Mutual的首席执行官欺骗了他，使其签署了一笔交易，将他所有的NXM都发送到了攻击者的钱包中，从而遭到830万美元的黑客攻击。攻击者向BTC洗了270万美元，这使NXM的价格降低了，然后他们在以太坊区块链产品上发送了一条消息，要求归还其余部分（以便NXM避免进一步的痛苦），以280万美元的ETH赎金。

去年12月，DeFi融资最多的是Compounder finance，后者的开发人员在合同中利用了一个隐藏的后门，因此潜逃了1,080万美元的投资者资金。

去年12月最大的快速贷款攻击受害者是Warp Finance，该漏洞的损失为770万美元，但585万美元将退还给持有人。可以说，这也是12月份DeFi黑客最多的退款，但是COVER是该头衔的竞争者，因为尽管返回的美元金额较小，但它却占COVER供应的可笑比例。

Gitcoin结束了强劲的2020年，其第8轮以太坊资金看到了45万美元的匹配资金，并且第一轮非以太坊资金也为Zcash项目完成了，从Zcash基金会分配了2.5万美元的匹配资金，但仅吸引了156笔捐款总计$ 2,137。

美国国会提出了一项法案，要求稳定币发行人获得银行宪章，在流通任何硬币之前，必须先获得美联储和其他机构的批准。

然后，加密货币法规的第一线转移到“自托管钱包”（即任何自托管的加密货币），并要求交易所对涉及这些可疑实体的交易进行尽职调查的程度。

Bittrex宣布将于1月15日将隐私币Monero，Zcash和Dash退市，但未说明具体原因。在此之前一个月左右，ShapeShift已将这些硬币除名。

在美国证券交易委员会指控Ripple Labs通过出售未注册证券销售的代币来筹集13亿美元之后一周，Bittrex也成为第11家将XRP退市的交易所。这提醒我们，筹集资金是一项长期的系统性风险，可能会在ICO之后的数年内适得其反。

为了摆脱监管机构的压力，Facebook的天秤座更名为Diem，放弃了获得一篮子货币支持的愿望，转而支持美元的直接支持。

Ledger最初在7月份报告的客户数据泄漏，现已公开转储。在原来的公告莱杰表示，更详细的信息，如物理地址已经为9.5K的客户访问，但似乎现在这部分信息已收获272K客户。

## 请在互联网上支持月报

100多个Twitter喜欢平均60个，1K+Medium的掌声，在12月10日在“Medium”上标记为“DEX”的帖子，在Publish0x上的良好观看率等等。

感谢您的支持！请继续为最好的加密货币项目带来更多知名度。

## About This Issue

这是Decred Journal的第33期。有关所有问题，镜像和翻译的索引，请参见[这里](https://xaur.github.io/decred-news/)。

在经过最少的健全性检查之后，来自第三方的大多数信息都会直接从来源中继。Decred Journal的作者无权验证所有声明。请当心诈骗，并自行进行调查。

您可以在[此处](https://github.com/xaur/decred-news/labels/next%20release)提交内容，以供撰写下一期月报内容。我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢 (字母排列):

- 写作和编辑: bee, degeri, l1ndseymm, lukebp, richardred
- 评论和反馈: davecgh, elian, JoeGruff, oshorefueled
- 封面图片: saender
- 资助： Decred Treasury

## 中文社区

* [社区网址](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [bilibili频道](https://space.bilibili.com/425519478)
* QQ群号-258412796
