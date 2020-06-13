# Decred月报 – 2020年5月

![abstract art](img/journal-202005-384.png)

_图片: Ascending Bits by @saender_

五月亮点：

- 发布新的vspd软件，它将取代VSP运营商使用的现有dcrstakepool软件，降低VSP注册需求，大大提高了所有VSP用户使用体验。
- Decred DEX软件正在进行公开测试，如果您有冒险精神，为什么尝试一下？
- Politeia新的重要组成部分已经发布，RFP提案以及CMS方面的承包商投票功能。
- 最新的v1.5移动客户端的测试版本现已在相应的APP商店中发布-非常欢迎测试人员在GitHub上提交问题。

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以构建和运行的源代码中，但对于普通用户来说，还不能在发布的二进制文件中使用。

[dcrd](https://github.com/decred/dcrd):

- 重做的HTTPS[种子](https://github.com/decred/dcrd/pull/2188)(作为参考，网络正在[迁移](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$156556717014681nMMAT:decred.org)到HTTPS上的种子，因为它更安全，并且更灵活）
- [禁止](https://github.com/decred/dcrd/pull/2110)不遵循有线协议的节点
- 更多代码迁移到Go 1.13

进行中：

- 去中心化开发基金支付所需的TSPEND操作码已在测试网上[成功测试](https://twitter.com/marco_peereboom/status/1263185839028350976)

[dcrwallet](https://github.com/decred/dcrwallet):

- 为JSON-RPC调用添加了客户端[软件包](https://github.com/decred/dcrwallet/pull/1726)
- 能够[同时](https://github.com/decred/dcrwallet/pull/1730)从同一个对等节点请求多个块（dcrlnd中SPV支持所需的更改之一）
- 能够保存[每张选票](https://github.com/decred/dcrwallet/pull/1737)的投票首选项（基于选票的VSP）

进行中：

- 对基于选票的VSP API的强化帐户[支持](https://github.com/decred/dcrwallet/pull/1743)

[Decrediton](https://github.com/decred/decrediton):

- 代码重构，可从pi-ui重用更多组件
- 能够[同时](https://github.com/decred/decrediton/pull/2481)从同一个对等方请求多个块（dcrlnd中SPV支持所需的更改之一）
- 用户界面调整

进行中：

- [混合](https://twitter.com/_vctt/status/1265397168317366283)交易

[Politeia](https://github.com/decred/politeia):

- 在[后端](https://github.com/decred/politeia/pull/1054)和[GUI](https://github.com/decred/politeiagui/pull/1910)中的RFP流程已经实施并正在测试中
- 用于[更改电子邮件地址](https://github.com/decred/politeia/pull/1178)的管理实用程序
- [简短的URL](https://github.com/decred/politeia/issues/900)
- 图像[导航](https://github.com/decred/politeiagui/pull/1878)模式
- 不启用[javascript](https://github.com/decred/politeiagui/pull/1834)查看Politeia进度
- 为了减轻烦人的注释错误，实施了两种临时的解决方法：一种方法是[每天](https://github.com/decred/politeia/pull/1205)运行一次而不是每小时一次，执行昂贵的文件系统检查；另一种方法是在触发该错误的过程中暂时[阻止](https://github.com/decred/politeiagui/pull/1944)注释
- 许多bug修复

CMS:

- [全体承包商](https://github.com/decred/politeia/pull/1104)对有争议的DCC的投票，由前6个月的计费小时数加权-这是实施DCC流程[提案](https://proposals.decred.org/proposals/fa38a3593d9a3f6cb2478a24c25114f5097c572f6dadf24c78bb521ed10992a4)的最后一部分
- 发布用于测试DCC发行和DCC投票过程的[程序](https://github.com/decred/politeia/pull/1179)

进行中：

- 管理员功能可查询承包商的[代码统计信息](https://github.com/decred/politeia/pull/1185)

[vspd](https://github.com/decred/vspd):

vspd是VSP软件从头开始的实现，它将极大地改善VSP用户的隐私，并进而改善Decred网络的安全性。没有注册，没有电子邮件，没有验证码以及没有要备份的脚本，使用起来也将更加容易。查看[公告](https://blog.decred.org/2020/06/02/A-More-Private-Way-to-Stake/)以获取更多详细信息。

vspd的[MVP](https://en.wikipedia.org/wiki/Minimum_viable_product)即将完成，并且dcrwallet已经开始集成。MVP的杰出的功能是获得跨钱包一致性检查，以确保所有钱包都对正确的选票进行投票，并具有正确的投票选择。

[dcrpool](https://github.com/decred/dcrpool):

v1.1候选发布版已准备好进行测试！此版本包括[重新设计](https://github.com/decred/dcrpool/pull/207)的付款处理，新的UI/UX，通过dcrd的工作通知实现更高的效率以及一系列较小的改进和bug修复。有关详细信息，请查看完整的[发行说明](https://github.com/decred/dcrpool/releases/tag/v1.1.0-rc1)。

[dcrlnd](https://github.com/decred/dcrlnd):

@matheusd发布了一个BTC和DCR发票在其各自的LN之间交换的[演示](https://twitter.com/matheusd_tech/status/1263118566418776065)。这实际上是一种“即时交换”，除了它使用的是LN并且是非托管的。请注意，该原型具有已知的向量，并且需要更多的研发才能解决（理想情况下基于[PTLCs](https://suredbits.com/payment-points-monotone-access-structures/), but it is quite far away in the future)，但将来还很遥远）。在[这个聊天中](https://matrix.to/#/!LtiDnUlfuRJMekjFSx:decred.org/$ILkQ49LXwBrUcMq5R_JRIkTcjR7FG9lxwMWsxDve2K0)更多详细信息。

[dcrdex](https://github.com/decred/dcrdex):

-更安全地加密密码
- 检修客户钱包配置，允许用户指定一个钱包配置文件或手动输入设置 ( [1](https://github.com/decred/dcrdex/pull/311), [2](https://github.com/decred/dcrdex/pull/335), [3](https://github.com/decred/dcrdex/pull/346), [4](https://github.com/decred/dcrdex/pull/352))
- 服务器支持用于计划中的维护和市场重新配置的正常[中止交易](https://github.com/decred/dcrdex/pull/287)和客户通知
- 用户浏览器界面中[扩展](https://github.com/decred/dcrdex/pull/378)的 “您的订单”
- 对用户[余额更新](https://github.com/decred/dcrdex/pull/418)改进，以提供最新的余额值
- 添加[莱特币](https://github.com/decred/dcrdex/pull/372)支持。服务器dcrdex已支持LTC，现在客户可以使用LTC钱包并在LTC市场下订单。
- 允许从[trade命令](https://github.com/decred/dcrdex/pull/315)进行交易
- [exchanges命令](https://github.com/decred/dcrdex/pull/314)允许从命令行列出和配置交换
- 添加用户浏览器界面“市场”页面上的市场[搜索框](https://github.com/decred/dcrdex/pull/426)
- 改进了注册事件的[通知](https://github.com/decred/dcrdex/pull/343)（例如完成费用支付确认）
- 多个bug修复和代码重构

[合并](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-05-01..2020-05-31+sort%3Aupdated-asc)了来自10个贡献者的59个PR ，添加10K行删除了3K行代码。

即将进行的工作包括：服务器支持待机/还原活动交换（交换状态），如果由于服务器或对手方导致服务器驱动的交换协商失败，则更好地支持客户端启动的退款或交换完成（退款）不活动，扩展的客户端RPC，扩展的服务器管理命令，改进的客户端对服务器挂起/恢复消息的处理。

测试网测试[已经开始](https://twitter.com/chappjc/status/1267115398610255874)，欢迎大家[参加](https://github.com/decred/dcrdex/wiki/Testnet-Testing)。主网DEX很有可能在今年夏天启动。

[dcrandroid](https://github.com/decred/dcrandroid):

- 支持[只读](https://github.com/decred/dcrandroid/pull/471)钱包模式
- [加密](https://github.com/raedahgroup/dcrlibwallet/pull/131)钱包种子并加强种子输入的隐私性（有关Google Keyboard的隐私问题）
- 在显示或验证种子之前请求[密码](https://github.com/decred/dcrandroid/pull/467)
- 每1GB R内存限制[限制](https://github.com/decred/dcrandroid/pull/472)1个钱包
- [波兰语](https://github.com/decred/dcrandroid/pull/405)翻译
- 多个bug修复

[Google Play](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.testnet)提供了v1.5版本的Testnet版本。发现Bug欢迎在[GitHub](https://github.com/decred/dcrandroid/issues)上提交。

[dcrios](https://github.com/raedahgroup/dcrios):

- 支持[只读](https://github.com/decred/dcrandroid/pull/471)钱包模式
- 支持区块链重新[扫描](https://github.com/raedahgroup/dcrios/pull/675)
- 添加Decred [logo](https://github.com/raedahgroup/dcrios/pull/674)二维码
- [波兰语](https://github.com/decred/dcrandroid/pull/405)翻译
- 多个bug修复

v1.5的Testnet版本在[Apple TestFlight](https://testflight.apple.com/join/7KL4VnB2)上可用。发现Bug欢迎在[GitHub](https://github.com/raedahgroup/dcrios/issues)上提交。


[dcrdata](https://github.com/decred/dcrdata):

- 攻击成本页面现在[DCR流通总量](https://github.com/decred/dcrdata/pull/1736)条件
- v5.3 Beta[已部署](https://dcrdata.decred.org/)

进行中：

- 基于交易的当前订单簿（在[planetdecred.org](https://explorer.planetdecred.org/attack-cost) for testing)上部署的WIP版本进行测试），在攻击成本页面上的DCR价格[增长](https://github.com/decred/dcrdata/pull/1738)预测
- 添加[原子交换交易](https://github.com/decred/dcrdata/pull/1733)标签
- 新增[网络信息](https://github.com/decred/dcrdata/pull/1753)页面包含减少区块奖励倒计时，以及其它基本信息（一个有趣的入口点，可与了解Decred的人分享）

[tinydecred](https://github.com/decred/tinydecred):

- 基础的[SPV节点](https://github.com/decred/tinydecred/pulls?q=is%3Apr+merged%3A2020-05-01..2020-05-31+sort%3Aupdated-asc+spv)
- 添加了BTC网络[参数](https://github.com/decred/tinydecred/pull/184)（支持多资产的第一步）
- 衡量[测试覆盖率](https://github.com/decred/tinydecred/pull/180)的工具
- [v0.1.0](https://github.com/decred/tinydecred/releases/tag/v0.1.0)是第一个版本（恭喜！）[

[docs](https://github.com/decred/dcrdocs):

- [全面检查](https://github.com/decred/dcrdocs/pull/1090)“[验证二进制文件](https://docs.decred.org/advanced/verifying-binaries/)”页面，该页面现在说明了用户需要执行的操作以及原因，并更新了多个页面以[鼓励](https://github.com/decred/dcrdocs/pull/1094)用户验证二进制文件（您也应该这样做！）
- [添加](https://github.com/decred/dcrdocs/pull/1089)了新的“[赎回脚本](https://docs.decred.org/proof-of-stake/redeem-script/)”页面，该页面解释了怎样备份和恢复

其它:

- @mm发布了[InvalidationGame](https://github.com/mmartins000/invalidationgame)，该脚本可在纯PoW网络或混合的PoW + PoS网络（如Decred）上模拟双花攻击。
- Bug Bounty网站发布了一个[更新](https://bounty.decred.org/2020/05/status-update/)：总共处理了123个提交（+19），其中13个有资格获得付款（+2）
- 随着新内容的推出，一些开发人员在Twitter上更加活跃。您可以关注 [@lukebp_](https://twitter.com/lukebp_), [@marco_peereboom](https://twitter.com/marco_peereboom), [@degeri_crypto](https://twitter.com/degeri_crypto)等，以获取更多信息。如果您是拥有Twitter帐户的开发人员，则可以通过在Twitter上发布此类dev更新来帮助传播Decred的构建者文化（不要犹豫[加入聊天室](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org)!)！）

5月（大约）的开发活动统计：〜300个活动PR，〜340个主提交，〜51K行添加和〜26K行删除的分布在16个存储库中（注意：行数不包括Decrediton [#2481](https://github.com/decred/decrediton/pull/2481)重新格式化了一个大型存储库）。每个存储库贡献2-10个开发人员。


## 人员

欢迎新到来的首次贡献者，他的代码已合并到主代码库中： @blaltarriba ([politeiagui](https://github.com/decred/politeiagui/commits?author=blaltarriba)), @dreacot ([dcrandroid](https://github.com/decred/dcrandroid/commits?author=dreacot)), @Ekeh ([dcrdata](https://github.com/decred/dcrdata/commits?author=Ekeh)), @guilhermemntt ([decrediton](https://github.com/decred/decrediton/commits?author=guilhermemntt)), @rstaudt2 ([dcrd](https://github.com/decred/dcrd/commits?author=rstaudt2)) 和 @song50119 ([dcrdex](https://github.com/decred/dcrdex/commits?author=song50119)).

祝贺新承包商获得了承包商认可的支付证书（DCC）：[@camilolwi](https://twitter.com/Camilolwi)（市场营销），[@itswisdomagain](https://github.com/itswisdomagain)（开发），[@nachito](https://github.com/Reidiojed)（市场营销），[@tomee](https://twitter.com/tomasgroos)（市场营销）。

三个Decred社区成员包含在巴西加密市场Cointelegraph的前50名名单那日：Rafaela Romano在＃35，Gabriel Rhama在＃31和Edilson Osório Jr

截至6月1日的社区统计数据：

- Twitter 关注: 40,492 (-78)
- Reddit 订阅: 9,792 (+31)
- Matrix 用户: 655 (+31)
- Discord 用户: 1,222 (+38)
- Telegram 用户: 2,603 (+46)
- YouTube 订阅: 4,030 (+40), 点赞: 144K (+3.5K since May 8) 
- Facebook 关注: 3,632 (+14), 点赞: 3,291 (+11)
- LinkedIn 关注: 810 (+36)
- GitHub dcrd 星星: 543 (+4), 叉子: 240 (+5)

## 治理

5月份，[社区开发基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)获得了13594 DCR，并花费了19153 DCR。以3月份的每日 DCR/USD 汇率 $14.11计算，这是收到的$192K和花费的$270K。以2月份的每日平均价格$12.34计算，该月完成工作的美元费用为$236K。截至6月5日，库存余额为630983DCR（1140万美元，折合18.12美元）。

5月份共提交了5份提案，其中4份于6月初开始投票。5月份没有Politeia提案投票。

新提案在《Politeia Digest》第[31期](https://blockcommons.red/politeia-digest/issue031/)中进行了描述，投票结果将在下一期中讨论。

## 网络

全网算力: [5月的全网算力](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=k9nb7wvw-kavn2b1a&scale=linear&bin=block&axis=time)以约357 Ph/s 的速度开始，而以约386 Ph/s的速度结束，最低为260 Ph/s，峰值为541 Ph / s。截至6月1日的池哈希率分布（大约）：UUPool 38％，Poolin 18％，lab.antpool.com 12％，F2Pool 1.5％，Luxor 1.3％，BTC.com 1.3％，BeePool 0.1％，CoinMine 0.03％，Suprnova 0.02％，其他〜28％。

Staking: [30天的平均票价](https://dcrstats.com/)为141.5 DCR（+3.7）。[票价](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=k9nb7wvw-kavn2b1a&bin=window&axis=time&visibility=true-false&mode=stepped) 132.9-159.2 DCR之间变化。锁定金额为5.59-5,080,000 DCR，相当于参与 PoS 的占[流通量](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=k9nb7wvw-kavn2b1a&scale=linear&bin=block&axis=time)的48.7-50.3％。

节点: 整个[5月](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1588291200000&to=1590969600000)，平均有144个公共监听节点，总共229个节点。五月份的平均版本分布：48％dcrd v1.5.1、11％dcrd v1.5.0、6％dcrd v1.6开发版本，4％dcrd v1.5开发和RC版本，2％dcrd v1.4、9％dcrwallet v1.5.1、1.4％dcrwallet v1.5、1.4％dcrwallet v1.4和其他13％。

Lewis Harland发表了一篇有关Decred网络的研[研究报告](https://formalverification.substack.com/p/in-the-network-decred)，该研究考虑了许多指标，包括代表矿工风险的算力与美元的比率。报告指出，自2020年1月以来，一些指标有所下降，这表明DCR相对于投入网络的美元处于亏损状态。

@PermabullNino发布了另一个链上[研究文章](https://medium.com/@permabullnino/decred-on-chain-mining-pulse-3b28d5155a04)，他在其中探索Decred块时间并介绍了Mining Pulse指示器。

## 整合

[Transak](https://global.transak.com/)通过与Wyre 的合作，为美国，欧盟和许多其他国家的居民带来了一种通过借记卡购买DCR的新方法。“ Transak使用智能合约将最终用户连接到集中式和分散式交易所的流动性。用户将必须输入简单的KYC信息，但是从头到尾的过程将不到5分钟。” 现在，Transak遍布32个国家/地区，支持14种法定货币和300多种加密资产。

警告：Decred Journal的作者不了解上述任何服务的可信赖性。在将您的个人信息或资产信任给任何实体之前，请先进行自己的研究。

## 外展活动

Decred参加了Consensus2020：分布式线上活动，其中6个社区成员录制4条视频，所有这些现在都在YouTube上。除了该活动位于美国以外，所有其他（已知）活动在5月都针对拉坦/巴西地区。

Decred in Depth 和 Rough Consensus 总共发布了4个新播客。

在4月开始撰写Medium [博客](https://medium.com/@Phoenixgreen)后，Phoenix Green扩展到了YouTube视频创作领域，截至撰写本文时，他的[频道](https://www.youtube.com/channel/UCZSFAqUMp8v58eEQl_bzWYg)中有10篇关于Decred的视频。恭喜发布，并保持原始质量内容！

Monde PR在五月份的成就：

- 创造并向投资，金融和加密出版物发行3个故事创意
- 提交Decred发言人对7个新闻故事的评论
- 通过加密出版物获得了一次媒体采访和一封电子邮件问答

Monde PR保证的新闻报道：

- 《[福布斯](https://www.forbes.com/sites/cbovaird/2020/05/05/is-this-the-perfect-time-for-central-bank-digital-currencies/)》上的一篇文章，重点介绍@ jy-p关于CBDC隐私问题的评论
- [Cointelegraph](https://cointelegraph.com/news/bitcoin-s-halving-incentivizes-miners-to-sell-for-double-decred-co-founder-says)中的一篇文章，重点介绍了@ jy-p对比特币减半的影响的评论，并联合了[FXStreet](https://www.fxstreet.com/cryptocurrencies/news/decred-co-founder-expects-bitcoin-halving-to-spike-btcs-price-202005070208)等 12个新闻媒体。评论还包括在[Zero Hedge](https://www.zerohedge.com/markets/paul-tudor-jones-buys-bitcoin-hedge-against-central-bank-money-printing)文章和[Cointelegraph](https://cointelegraph.com/news/top-experts-make-bitcoin-price-predictions-as-btc-halving-approaches)的第二篇文章中，并联合了12个新闻媒体，包括 [Miami Diario](https://miamidiario.com/bitcoin-a-la-mitad-los-expertos-creen-que-solo-se-debe-comprar-si-se-retiene-a-largo-plazo/)和[Crypto News Australia](https://cryptonews.com.au/story/top-experts-make-bitcoin-price-predictions-as-btc-halving-approaches-121382)。
- [Finance Magnates](https://www.financemagnates.com/cryptocurrency/news/will-the-upcoming-halving-increase-bitcoins-price/) 中的一篇文章，重点介绍@raedah对比特币减半的评论。@raedah的评论也包含在与此主题相关的第二篇《金融大亨》文章中。
- [Cointelegraph](https://cointelegraph.com/news/stairway-to-scarcity-bitcoin-sentiment-to-rise-despite-halving-impact)中的一篇文章，重点介绍了@Checkmate对比特币减半的评论，并联合了5个新闻媒体，包括Investing.com
- [路透社](https://www.reuters.com/article/crypto-currencies-bitcoin/as-pandemic-rages-anything-goes-for-bitcoins-third-halving-idUSL1N2CP13B)的一篇文章，其特色是@ jy-p的评论，并与包括《纽约时报》（现已删除），《商业内幕》和纳斯达克在内的 70个新闻机构联合发布。在随后有关Yahoo Finance，CryptoSlate和msn.com减半的文章中，也引用了 @ jy-p的评论。
- [8btc.com](https://m.8btc.com/article/594407)上的一篇文章，内容来自@ jy-p关于比特币减半的评论 
- [Cointelegraph](https://cointelegraph.com/news/bitcoin-halving-was-not-the-apocalyptic-event-some-in-crypto-feared)中的一篇文章，重点介绍@Checkmate对比特币减半的评论
- [AMB Crypto](https://eng.ambcrypto.com/xrp-trades-wide-as-iota-decred-look-to-make-room/)上的一篇文章，其中介绍了@ jy-p对CBDC的评论
- 通过上述努力，5月在21个国家/地区总共发表了123篇文章，请点击[这里](https://docs.google.com/spreadsheets/d/1oef5U9R_JZ7hxmRRNKDCQNia7u-1lRuGk6w3w3LU-p0/edit?usp=sharing)查看完整列表

## 活动

参加：

- 4月2日 - [Walicj.com](https://twitter.com/DecredCN/status/1245279133082324997) - 互联网。DecredCN和Walicj.com在微信小组中共同组织了AMA，主要介绍Decred的治理模型，原子交换和dcrdex。该记录[已发布](http://walicj.com/#/layout/article_detail/16720)在他们的网站上。（四月错过）
- 4月23日 - [Jueves CryptoDrinks Decred](https://twitter.com/Decred_ES/status/1253427311707213824) 互联网。@elian：“这是一个非常休闲的视频通话，与Blockchain Land的社区成员进行了通话，Decred是通话的主持人之一。我对该项目进行了简短介绍，其余的则回答了有关加密货币的一般问题（在哪里购买，如何存储，如何发现诈骗，对减半的想法，交易策略以及采矿是否有利可图。它持续了一个半小时，并有20-25名参与者。” （四月错过）
- 4月28日 - [Panel on Cryptosecurity](https://twitter.com/elianhuesca/status/1255293877373800448) - 互联网。@elian：“它是由Binance用西班牙语组织的，它是一种AMA，但是在加密安全方面，有关如何存储和OPSEC最佳实践的问题。我有很多机会重点介绍Decred在开放式混合区块链上的工作源软件和抗硬性。AMA的观众和其他来宾都给予了很好的回应。” （四月错过）
- 5月2日 - [Bitconf Live](https://www.eventbrite.com.br/e/bitconf-live-edition-tickets-103094542552) - 互联网。Decred是赞助商。OriginalMy的创建者兼首席执行官小Edilson Osorio Jr发表了题为“大流行期间区块链的影响”的演讲，并介绍了一个新的应用程序来验证和验证开处方的过程，而无需与患者进行身体接触（Decred是4个区块链之一）由应用使用）。JoãoFerreira（@girino）谈到了“权力下放与治理”，DEX，原子交换和Politeia，约有2500人观看了此演讲。这些视频可在Facebook和Decred Brasil YouTube频道上找到。
- 5月6日 - [Crypto Resources Livestream](https://twitter.com/cryptorc_tech/status/1257765517626130433) - 互联网。该视频流长达2小时，约有300人观看。@camilolwi介绍了区块链和比特币，然后@elian谈论了Decred将近一个小时。
- 5月7日 - [Hablemos Decred 5](https://twitter.com/Decred_ES/status/1257774155677630464) - 互联网。
- 5月12日 - [Consensus: Distributed](https://www.coindesk.com/events/consensus-2020) - 互联网。Decred的代表来自@lukebp的Politeia，@ matheusd的LN，@ chappjc和@ buck54321的dcrdex和dcrdata，@ Checkmate的链上见解，最后是@ jy-p的演讲，概述了Decred开发的1年。以下媒体部分中的所有链接。
- 5月13日 - [Digital Governance](https://twitter.com/Decred_ES/status/1260574384667983875) - 互联网。这个与Decred，区块链治理和去中心化数字货币有关的约20人网络研讨会是与Hack por la Paz共同组织的。问题围绕着理解我们日常生活中的治理，如何将其推算到数字货币和财富以及CBDC对加密货币市场的影响。
- 5月14日 - [Decentralized Governance Panel](https://twitter.com/Decred_ES/status/1258905004510973953) - 互联网。@caibarrad和@adcade在“什么是分散式治理和DAO？”小组中代表Decred，该小组与BlockchainEx共同组织，是哥伦比亚Decred生态系统发展的一部分。
- 5月16日 - [Open-Source Funding Webinar](https://twitter.com/Decred_ES/status/1259984598102093828) - 互联网。@victorarubin和@tomee与Hack Space Peru共同组织了该活动，作为该地区推广活动的一部分。@pablito进行了有关开源软件最大挑战之一的演讲，资金筹集，探索了十几种方法，最后介绍了Decred解决方案。
- 5月19日 - [Latoken Blockchain Economic Forum](https://latoken.com/events/Keynote-133) - 互联网。@elian在36分钟的主题演讲中谈到了Decred，项目资金/支出，Politia，LN和隐私实施。
- 5月20日 - Bitcoin and Crypto Panel - 互联网。@elian：“作为Talent Land的Business Land的一部分，我参加了有关比特币和加密货币用例的小组讨论，并重点介绍了Politeia和dcrtime作为FOSS基础设施，包括针对政府和企业的案例，以及DAO如何支付其全球劳动力。有关DCR和支付处理基础设施的汇款市场以提高采用率的信息。” 
- 5月25日 - [BlockConf Digital](https://blockconf.digital/) - 互联网。Decred是铜牌赞助商。与预期相反，无法知道人们是否参加了虚拟展位，也没有与人互动的简便方法。@elian在Latam上发表了关于加密货币的演讲，并简要介绍了Decred，Politeia和Latam提案。

## 媒体

精选文章：

- Decred on-chain: @PermabullNino  ([medium](https://medium.com/@permabullnino/decred-on-chain-mining-pulse-3b28d5155a04))
- Decred price: @OneAnalyst ([medium](https://medium.com/coinmonks/decred-price-a-seasonality-study-414bac98bc99))
- 更隐私的Staking方案 @jholdstock ([blog.decred.org](https://blog.decred.org/2020/06/02/A-More-Private-Way-to-Stake/))
- Decred. 分叉之路 by @mrbulb ([github](https://github.com/monsieurbulb/forksintheroad/blob/master/Decred_forks_in_the_road.md))

翻译:

- 一种新型的DEX - [西班牙语](https://medium.com/decred-es/un-nuevo-tipo-de-dex-8d7b5f8681c9) by @francov\_
- Politeia Digest 31 - [西班牙语](https://medium.com/decred-es/politeia-digest-edici%C3%B3n-31-abril-16-mayo-22-2020-28fc2fc75784) by @pablito. 
- 2020年4月的Decred Journal被翻译成阿拉伯语（@arij），中文（@Dominic），波兰语（@kozel）和西班牙语（@francov_）。值得注意的是，所有四个都在GitHub上。谢谢你们！

视频:

- Decred 双周报 - 2020年5月3日 @Exitus ([youtube](https://www.youtube.com/watch?v=oHqzvN3TMU0))
- Decred Construct 开发人员Luke Powell谈Politeia和Matheus Degiovani谈LN ([youtube](https://www.youtube.com/watch?v=HexsUmqA7-Y))
- Decred Construct DEX 开发人员Brian Stafford和Jon Chappelow0 ([youtube](https://www.youtube.com/watch?v=fS9j7RaawjY))
- Trade Secrets Decred链上分析师Checkmate ([youtube](https://www.youtube.com/watch?v=NOyyAx6Ab_0))
- Decred Changelog 项目负责人Jake Yocom-Piatt ([youtube](https://www.youtube.com/watch?v=OmwI62HZerg)) with Q&A ([youtube](https://www.youtube.com/watch?v=Uzf2ZGXWoss))
- 365 Decred days - CoinDesk ([coindesk.com](https://www.coindesk.com/video/365-decred-days)) - 这是CoinDesk网站上完整的Decred Foundations程序，它们通过Zoom进行广播，因此质量不如YouTube在上面上传的质量 ([youtube](https://www.youtube.com/watch?v=QWfq1tn8xs0))
- Decred 双周报 - 2020年5月22日 @Exitus ([youtube](https://www.youtube.com/watch?v=9i56ly5SS6M))

音频:

- Decred in Depth Ep. 24 - @chappjc和@ buck54321谈论dcrdex ([libsyn](https://decredindepth.libsyn.com/chappj-buck-the-decred-dex))
- Decred in Depth Ep. 25 - @raedah谈论了Decred的开发工作，从为DCP-0001和dcrdata做贡献到移动钱包等新项目，与非洲和亚洲开发者组成了一个小组，以及新的Planet Decred提案 ([libsyn](https://decredindepth.libsyn.com/raedah-planet-decred-development), [soundcloud](https://soundcloud.com/decredindepth/raedah-planet-decred-dcr))
- Rough Consensus Ep. 5 - 通货紧缩，美元和贬值。@ mr.black，@ Checkmate和@PermabullNino讨论了比特币减半，传统市场的救济集会，通货紧缩和通货膨胀对经济的现实，以及Decred如何被低估为SoV竞争者。 ([libsyn](https://roughconsensus.libsyn.com/episode-5-deflation-dollars-decred))
- Rough Consensus Ep. 6 - Seth Simmons和间谍团队一起谈论叙事如何驱动加密货币。 ([libsyn](https://roughconsensus.libsyn.com/episode-6-narratives-with-seth-simmons))

## 社区讨论

通讯系统新闻：

- Riot发布了一个巨大的更新，该更新已部署到chat.decred.org。默认情况下，新DM启用端到端加密。确保备份密钥，以免丢失对加密聊天记录的访问权限。

精选Reddit帖子：:

- @mrbulb 关于他的“ Forks in the road”文章的帖子有19条评论，大多数是来自表示对此表示感谢的人，但是有一位用户删除了他们的评论
- 在伊朗进行宣传的预案
- [时间锁](https://www.reddit.com/r/decred/comments/gcyquz/decred_timelocks/)的应用

精选Twitter讨论:

- 在比特币减半的那天，@ ammarooni 提醒奥地利经济学家建议不要突然改变货币发行
- @lukebp在Twitter上表达了更多有关[Politeia](https://twitter.com/lukebp_/status/1258139602516193280)工作的声音
- @lukebp 在一些简短的推文中解释了 Politeia，CMS和DCC流程
- @chappjc makes the dcrdex testnet pre-alpha [official](https://twitter.com/chappjc/status/1267115398610255874)
- @chappjc使dcrdex testnet pre-alpha 正式
- @elian揭露了有关银行账户即将发生的严酷现实

## 市场表现

5月DCR交易价格在12.62-15.66美元，BTC 0.0014-0.00167之间。每日平均价格为$14.11。

OneAnalyst进行的一项[季节性研究](https://medium.com/coinmonks/decred-price-a-seasonality-study-414bac98bc99)探讨了DCR的每日、每周和每月的收益影响（DCR似乎更倾向于星期六）。

[总结](https://blockcommons.red/publication/mm-phase1-wrapup/)第一阶段做市商行为由@richardred分析订单簿的深度随着时间DCR和其它资产，他认为没有看到有机增长超出I2维护的订单。

## 相关外部信息

比特币一直期待已久的减半发生在5月11日，它占据了加密新闻的主导地位，甚至渗透了更多的 主流 消息来源 -其中大部分集中在对价格可能产生的影响上。

Cointelegraph组织的长达7个小时的现场直播是为纪念这一事件而进行的几项现场活动之一，因此中途毫不客气地暂停了播放，并因YouTube是“有害内容”而被YouTube删除。

达世币投资基金会（Dash Investment Foundation）宣布将不再寻求决策自主权，并将减少其对达世币司令部的要求，从而应对了一些摩擦（主节点拒绝了提案和私人批评），并在第二季度提出了新的风险投资策略2020年。

Reddit引入了新的基于区块链的令牌，将在/ r / cryptocurrency（Moons）和/ r / FortNiteBR（Bricks）上进行试用。相对于业力分数（50％），主持人10％，Reddit 20％和“更广泛的Reddit社区” 20％，subreddit的用户将获得令牌。除了充当subreddit点上的声誉徽章之外，还可以用于解锁功能，例如在评论中发布gif。还描述了民意测验的点加权变体。

科技巨头和数十个政府已经决定，智能手机的后门能力还不够，并发起了前所未有的大规模监视计划（归因于COVID-19）。许多技术的标题中都添加了“保留隐私”，这一次可能真的很安全。一旦大流行“结束”，甚至有可能终止跟踪系统。除了讽刺，对于加密货币用户来说，这意味着他们的移动设备上存在许多新的隐私和安全风险，并且是考虑使用替代操作系统甚至硬件的强烈动机。

## 关于月报

这是Decred Journal的第26期。有关所有问题，镜像和翻译的索引，请参见此处。

在经过最少的健全性检查之后，来自第三方的大多数信息都会直接从来源中继。Decred Journal的作者无权验证所有声明。请当心诈骗，并自行进行调查。

我们随时欢迎您的反馈和贡献。

感谢 (字母排列):

- 写作和编辑: bee, chappjc, degeri, elian, Exitus, l1ndseymm, richardred
- 评论和反馈: davecgh, dnldd, Dominic, emiliomann, jholdstock, jrick, lukebp, matheusd, raedah
- 封面图片:  saender

## 中文社区

* [社区网址](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [优酷频道](https://i.youku.com/decredproject)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

