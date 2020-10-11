# Decred月报 – 2020年9月

![abstract art](img/journal-202009-384.png)

_图片: by @saender_

九月重点:

- 经过全面审查后，去中心化国库支付代码已完成合并。
- dcrdex正在解决早期测试中发现的许多复杂去信任交易方案，第一次主网交换在十月初完成，正式发行版应该很快就可以投入使用。
- 第一个关于Politeia的RFP提案（更改decred.org上的消息传递）获得批准，并收到了4个候选提案。不久将开始投票。
- 6月份批准的提案dcronchain.com 链上指标网站现已启动。
- withdecred.org门户网站已经启动，已提交相关提案以资助奖品，该提案已于10月初获得批准。

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以构建和运行的源代码中，但对于普通用户来说，还不能在发布的二进制文件中使用。

[dcrd](https://github.com/decred/dcrd):

去中心化国库支付被[合并](https://github.com/decred/dcrd/pull/2170)到主数据库中。自初始计划发布以来，获得了576条评论意见，更改了115个文件，添加了1.5万行代码，花费了5个月的时间。目前已从其它项目中撤出了几名开发人员，以彻底检查和测试新共识的关键代码。感谢大家为这一重大变化所做的辛勤工作！

DCP0006共识变化的描述文件正在[审查中](https://github.com/decred/dcps/pull/17)。

国库代码合并的后的工作:

- 单向[迁移](https://github.com/decred/dcrd/pull/2336)数据库以支持新的国库支付代码部署
- [跟踪](https://github.com/decred/dcrd/pull/2350)内存池中的tspend（国库支出）交易
- 在节点启动时[中继](https://github.com/decred/dcrd/pull/2349)tspend交易（这是为了帮助挖矿节点和投票钱包及时发现tspends）
- 新的RPC命令来[统计](https://github.com/decred/dcrd/pull/2351)tspend交易的投票计数（初步实现内存池中的tspend或已挖掘的tspend查询）
- 从代码中删除了[footguns](https://github.com/decred/dcrd/pull/2389)以计算tspend窗口值
- 重新设计封装了`standalone`的[一致性](https://github.com/decred/dcrd/pull/2394)，并使测试覆盖率恢复到100％

其它合并工作:

- 优化的[签名缓存](https://github.com/decred/dcrd/pull/2358)
- 合并[禁用/白名单](https://github.com/decred/dcrd/pull/2363)逻辑
- 更严格的[系统服务](https://github.com/decred/dcrd/pull/2357)
- 为即将发布的版本更新了[检查点](https://github.com/decred/dcrd/pull/2370) 和已知的最低链工作
- 在测试范围，日志记录，bug处理等方面进行了许多较小的改进

@matheusd编写了一个独立的工具来生成tspend[工具](https://github.com/matheusd/tspend)，该交易可用于无间隙设置（无需与基础dcrd建立网络连接）。它与@jrick的ss工具结合使用，用于后量子文件和流加密。

[dcrwallet](https://github.com/decred/dcrwallet):

- 增加去中心化国库支出的[支持](https://github.com/decred/dcrwallet/pull/1714)，包括网络运营商生成国库密钥新工具
- 转储扩展的公共密钥时[发出警告](https://github.com/decred/dcrwallet/pull/1822)（如果xpub与任何帐户私钥组合泄漏，则将显示该帐户的所有私钥）
- [变更](https://github.com/decred/dcrwallet/pull/1830)零散购票
- 将[未发布](https://github.com/decred/dcrwallet/pull/1838)的交易保存到数据库中（有必要防止以前的某些钱包输出在重新启动期间被双重花费，或保持部分签名的TX；这将由vspd客户端使用）
- 新标记，仅[手动](https://github.com/decred/dcrwallet/pull/1833)添加故障单，而不通过网络同步发现故障单（vspd管理员将使用此标记，以防止用户通过重复使用其投票地址来获得免费投票。设置此标记后，只能通过以下方式将故障码添加到vspd中：适当的API）
- 为P2SH [listunspent](https://github.com/decred/dcrwallet/pull/1842)结果添加兑换脚本（这是针对dcrdex的）
- 支持[vspd](https://github.com/decred/dcrwallet/pull/1840)
- 实现的[sendrawtransaction](https://github.com/decred/dcrwallet/pull/1846)
- 对vspd和dcrdex客户端进行的广泛测试有助于发现并修复bug

[Decrediton](https://github.com/decred/decrediton):

- 从pi-ui引用[复选框](https://github.com/decred/decrediton/pull/2663)组件
- 继续重构功能组件和CSS模块
- 多个bug修复

进行中：

- 支持闪电网络 [守望台](https://github.com/decred/decrediton/pull/2638) 
- 闪电网络 [UI/UX](https://github.com/decred/decrediton/pull/2641)改进

[Politeia](https://github.com/decred/politeia):

- 添加用户数据库 [测试](https://github.com/decred/politeia/pull/1296)
- 通过[分页](https://github.com/decred/politeia/pull/1306)优化内存使用
- admin TOTP [重置](https://github.com/decred/politeia/pull/1298)命令

CMS:

- 添加的用户[搜索](https://github.com/decred/politeiagui/pull/2131)返回按钮
- 替换了剩余的[缓存](https://github.com/decred/politeia/pull/1300)使用量，以清除tlog迁移的方式
- 添加了用于测试基础架构的[LevelDB](https://github.com/decred/politeia/pull/1302)

进行中：

- 2FA使用[TOTP](https://github.com/decred/politeia/pull/1212)登录（基于时间的代码）
- 查询CMS管理员的承包商[代码](https://github.com/decred/politeia/pull/1185)统计信息
- [后端](https://github.com/decred/politeia/pull/1180)和[GUI](https://github.com/decred/politeiagui/pull/2142)上的tlog实现

来自@lukebp的状态更新：

> 在过去的一个月中，大多数的Politeia开发都集中在tlog上。与现有politeia功能匹配的前端和后端工作已完成。接下来的几周主要关注测试日志，解决bug，编写文档以及将测试覆盖范围。尚待实现的功能是能够检索特定Politeia数据的包含证明。politeiad后端目前支持此功能，但是需要添加相应的politeiawww路由，以及在GUI中显示/下载包含证明的方式。此功能将在启动前添加。

[vspd](https://github.com/decred/vspd):

- 存储每张票最多10个投票选择[更改](https://github.com/decred/vspd/pull/180)的记录，以实现双向问责
- 要求dcrwallet在[手动购票](https://github.com/decred/vspd/pull/187)模式下运行

[dcrpool](https://github.com/decred/dcrpool):

- 将代码库更新为Go 1.13
- 修复重新连接 [错误](https://github.com/decred/dcrpool/pull/247)

[dcrlnd](https://github.com/decred/dcrlnd):

- [移植](https://github.com/decred/dcrlnd/pull/103)上游工作的PR已更新，所有工作已完成至[v0.11.1-beta](https://github.com/lightningnetwork/lnd/releases/tag/v0.11.1-beta)版本。这将使我们与当前最新的lnd版本保持一致。

[dcrdex](https://github.com/decred/dcrdex):

- 增加带有过滤器和无限滚动的[订单历史](https://github.com/decred/dcrdex/pull/644)视图，以及具有所有匹配项和相关交易输出的订单详细信息视图
- 显示[锁定](https://github.com/decred/dcrdex/pull/683)在合约中的金额并更新余额
- 添加[`match_status`](https://github.com/decred/dcrdex/issues/643)和[`order_status`](https://github.com/decred/dcrdex/pull/687)路线不寻常的情况下恢复的测试，如笔记本电脑中止或连通性差导致的客户错过了发现的revoke_match步骤（重新启动dexc程序固定它，但它是UX差）
- 改进的[重新连接](https://github.com/decred/dcrdex/pull/663)处理
- 更强大的[丢失](https://github.com/decred/dcrdex/pull/661)匹配处理
- 返回[活动订单](https://github.com/decred/dcrdex/pull/677)的`connect`响应
- 在不再需要的更多情况下[解锁](https://github.com/decred/dcrdex/pull/648)硬币（阅读此随机注释以了解在不信任交换协议中必须考虑多少个情况）
- 用户[惩罚](https://github.com/decred/dcrdex/pull/649)通知
- 更好地[赎回交易](https://github.com/decred/dcrdex/pull/513)处理
- 多个[操作失灵](https://github.com/decred/dcrdex/pull/680)检查修复
- 需要客户端RPC[密码](https://github.com/decred/dcrdex/pull/621)
- 在用户界面中可[启用](https://github.com/decred/dcrdex/pull/654)调试日志记录
- 许多内部更改和bug修复

[合并](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2020-09-01..2020-09-30+sort%3Aupdated-asc)了来自4个贡献者的35个PR ，添加了9K行代码以及删除了2.6K行代码。

Twitter[民意调查](https://twitter.com/chappjc/status/1302795835248439296)显示了大家希望在DCRDEX主网上支持LTC交易对。

> 由#dcrdex协调的首次DCR-BTC主网原子交换在昨天进行。测试和开发仍在继续，但讨论内容已经转移到软件分发和教程上。@decredproject的精彩时刻。（@chappjc[10月9日](https://twitter.com/chappjc/status/1314436781891301376)）

[dcrandroid](https://github.com/planetdecred/dcrandroid):

- 更新 [中文](https://github.com/planetdecred/dcrandroid/pull/515) 翻译
- bug 修复

进行中：

- 显示Politeia [提案](https://github.com/planetdecred/dcrandroid/pull/503)

[dcrios](https://github.com/planetdecred/dcrios):

- bug 修复

进行中：

- 显示Politeia [提案](https://github.com/planetdecred/dcrios/pull/715)
- 添加XC UI [测试](https://github.com/planetdecred/dcrios/pull/707)

[dcrros](https://github.com/decred/dcrros):

- [已更新](https://github.com/decred/dcrros/pull/6)至Rosetta规范的v1.4.4，其中包括构建，签名和发布交易的功能。该`check:construction`规范对应的rosetta-cli的测试套件正在通过此PR。

Rosetta v1.4发布了用于以标准格式构造交易的[Construction API](https://www.rosetta-api.org/docs/construction_api_introduction.html)（以前称为Wallet API），当我们在[6月](202006.md)宣布Decred的Rosetta实现时，该API尚未完成。最新的dcrros支持此API，并且正在努力使其与规范保持一致，以及Decred即将到来的共识更改。


[docs](https://github.com/decred/dcrdocs):

- 用更大的比例替换示例开发[建议](https://github.com/decred/dcrdocs/pull/1127)
- 用适当的选项卡替换特定于操作系统的[可折叠](https://github.com/decred/dcrdocs/pull/1129)部分

[dev docs](https://github.com/decred/dcrdevdocs):

- [Ticket Selection](https://devdocs.decred.org/developer-guides/ticket-selection/) 页面 [移动到](https://github.com/decred/dcrdocs/pull/1126)dcrdocs
- 为Decred中使用的txscript系统[添加](https://github.com/decred/dcrdevdocs/pull/86)了[概述](https://devdocs.decred.org/developer-guides/transactions/txscript/overview/)和[操作码](https://devdocs.decred.org/developer-guides/transactions/txscript/opcodes/)参考（这是一种简单的，基于堆栈的，类似于Forth的编程语言）

[decred.org](https://github.com/decred/dcrweb):

- 增加 [Latam](https://github.com/decred/dcrweb/pull/909) 贡献者
- 后端更新

其他：

- Bug赏金计划发布了新的[内容](https://bounty.decred.org/2020/09/status-update/)，并根据最近提交的经验对规则和范围进行了[更改](https://github.com/decred/dcrbounty/pull/71/files)

## 人员

截至10月1日的社区统计数据：

- Twitter 粉丝:: 40,790 (-26)
- Reddit 订阅: 9,929 (+23)
- Matrix #general 用户: 197 (+23)
- Discord 用户: 1,396 (+2)
- Telegram 用户: 2,434 (-34)
- YouTube 订阅: 4,210 (+30), 浏览: 156K (+1.7K)
- LinkedIn 粉丝: 891 (+16)
- GitHub dcrd 星: 563 (+6), forks: 248 (+2)

这些统计信息的图表可在[社交媒体统计信息](https://github.com/decredcommunity/social-media-stats/blob/graphs/graphs/index.md)存储库（跟踪更多帐户）和Planet Decred的[dcrextdata](https://dcrextdata.planetdecred.org/community)（高分辨率的动态图表）中找到。


## 治理

九月[国库](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到12300 DCR，花费5740 DCR。按照9月份的每日平均DCR/USD汇率13.26美元计算，这是16.3万美元的收入和7.6万美元的支出。按8月平均汇率17.02美元计算，当月完成工程的美元账单金额为9.8万美元。截至10月3日，社区开发基金余额为640000 DCR（750万美元，11.69美元）。

- @Exitus有关视频制作的[提案](https://proposals.decred.org/proposals/1e55a41)以94.6％的赞成票和31％的投票率获得批准。
- 9月提交了一项[提案](https://proposals.decred.org/proposals/2bf72e6)，以DCR赠品推广新的withDecred.org网站，并于10月初获得批准，赞成票率为62％，投票率为37％。
- 支付@alexsolo的2016-18年工作报酬的[提案](https://proposals.decred.org/proposals/f279ed5)以8％的赞成票和28％的投票率被拒绝。
- 更改decred.org上消息传递的RFP[提案](https://proposals.decred.org/proposals/91becea)已获得批准，批准率为85％，投票率为29％。在9月28日截止日期之前提交了4项提案，一旦准备就绪，将开始进行决赛投票。这些提案中只有一个可以被批准，并且仍然必须满足通常的批准和法定人数要求

有关提案的详细说明，请参见《Politeia Digest》第[36](https://blockcommons.red/politeia-digest/issue036/)期和第[37](https://blockcommons.red/politeia-digest/issue037/)期。

@bee根据过去提案的经验，发布了一份成功的Politeia提案的[全面清单](https://github.com/decredcommunity/guidelines/blob/master/proposals.md)。

## 网络

全网算力: 9月哈希率 以460 Ph/s开启并以 450 Ph/s结束。月内，最低为338 Ph/s，峰值为609 Ph/s。哈希率分布 截至10月1日：UUPool 35%, Poolin 27%, Huobipool 11%, easy2mine 10%, Antpool 9%, BTC.com 3%, Luxor 0.9%, F2Pool 0.5%, okex 0.2%, CoinMine 0.02%,，其他~3%。

Staking: [30天的平均票价](https://dcrstats.com/)为148.6 DCR（-2.8）。[价格](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kegbelov-kfrbnmg7&bin=window&axis=time&visibility=true-false&mode=stepped)在144.7-152.5 DCR之间变化。[锁定金额](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kegbelov-kfrbnmg7&bin=block&axis=time)为6066-612万DCR，相当于参与PoS的占[可用供应量](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kegbelov-kfrbnmg7&bin=block&axis=time)的50.38-51.04％。

节点: 整个[9月](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1598918400000&to=1601510400000)，每个dcr.farm平均有108个公共侦听节点和133个节点。9月的平均版本分布：26％dcrd v1.5.1、22％dcrd v1.5.2、7％dcrd v1.6开发人员版本，7％dcrd v1.5.0、4％dcrd v1.5开发人员和RC版本，0.8％dcrd v1.4、17％dcrwallet v1.5.1、1.6％dcrwallet v1.5、1.1％dcrwallet v1.4，其它15％。

[dcronchain.com](https://dcronchain.com/) 是在六月批准的[提案](https://proposals.decred.org/proposals/0230918)。初始版本包括5个交互式图表，这些图表是根据@Checkmate和@PermabullNino的研究从Decred的链上数据得出的。小组欢迎有关 [Reddit](https://www.reddit.com/r/decred/comments/j3589s/release_dcronchaincom_onchain_researchgraphs_in/)的任何反馈。源代码可在[GitHub](https://github.com/Decred-Bulls/dcronchain)上获得。恭喜发布！

## 整合

六月巴西NovaDAX交易所现在在其借记卡上增加了DCR支持。这将允许访问全国23,000多个ATM和POS终端。

> NovaDAX是BR市场的前三名。使用新的借记卡，可以在接受Elo的地方支付任何账单，而Elo在巴西与Visa和Mastercard的采用相同。此外，还可以用BRL进行银行转帐，从您的帐户中扣除DCR，而无需支付转帐费，这是巴西所有银行都收取的费用。也可以在Banco24horas ATM中用DCR交换BRL，在巴西大约有23000台机器。NovaDAX正在葡萄牙开设分公司，并打算在欧洲市场做同样的事情。（@emiliomann）

澳大利亚Swyftx已添加到decred.org，尽管它具有DCR已有一段时间。该交易所具有许多功能，并允许用户使用AUD购买DCR。

警告：Decred Journal的作者不了解上述任何服务的可信赖性。在将您的个人信息或资产信任给任何实体之前，请先进行自己的研究。

## 外展活动

@Exitus' second [proposal](https://proposals.decred.org/proposals/1e55a41) for making video content for another 6 months was approved with very high support. @Checkmate will join in the second phase to help with scripts and feedback. The proposal shared some stats for the last 6 months: 21K views gained with 98% like rate, ~500 subscribers gained and ~250 lost, 170 comments received. The most popular video was [DCR 101 - How to Stake Decred 2020](https://www.youtube.com/watch?v=m5lcm6yttEk) with 1.6K views. Various videos uploaded to Twitter gained ~18K views.

@pavel, @pablito, and @el\_capitan [launched](https://www.reddit.com/r/decred/comments/it9mkf/withdecredorg_new_portal_to_onboard_newcomers_to/) a new website [withdecred.org](https://withdecred.org/) to find a new scalable approach for how to onboard new users to Decred community. The website contains a series of articles that form a structured "funnel" that leads the person to purchase a few DCR. A [proposal](https://proposals.decred.org/proposals/2bf72e6) followed to fund the operations and a distribution of $5,000 worth of DCR to drive initial engagement, approved in early October. Historically, some community members have been skeptical about giveaways and this project will finally bring some empirical data and gauge the ROI of that model. Companion Twitter handle is [@withdecred](https://twitter.com/withdecred).

A few community members [organized](https://www.reddit.com/r/decred/comments/it0idm/decred_on_quora/) to answer a stash of questions about Decred on Quora.

@pavel started experimenting with publishing [Decred](https://www.publish0x.com/withdecred/why-we-need-decred-an-inclusive-approach-to-sound-money-xgdwkjl) [content](https://www.publish0x.com/crypto-as-an-agent-for-change/monero-and-decred-are-the-new-bitcoin-xlldpze) on Publish0x since it is a [promising](https://github.com/Decred-Bulls/decred-marketing#why-to-invest-time-into-publish0xcom) crypto portal.

@pablito and @caibarrad launched the first episode of Decred en Español podcast, available on [YouTube](https://twitter.com/Decred_ES/status/1310654270056923136) and [Spotify](https://twitter.com/Decred_ES/status/1310055071200292869).

@jazzah posted a [contest](https://www.reddit.com/r/decred/comments/ifyb03/contest/) themed "KYC vs Shuffle++" where participants need to complete non-trivial tasks by inspecting a crazy hilarious image. Prize #1 has been claimed but prizes 2-4 are still open for anyone.

Monde PR's achievements for September:

- created/pitched 2 story ideas to the finance and crypto publications
- responded to 3 requests for comments
- responded to 2 news stories about DCR

News coverage secured by Monde PR:

- an article in [Authority Magazine](https://medium.com/authority-magazine/meet-the-disruptors-how-jake-yocom-piatt-of-decred-aims-to-redefine-governance-with-blockchain-5c3724f20e74) featuring commentary by @jy-p on how Decred aims to redefine governance with blockchain technology
- an article in [AMB Crypto](https://eng.ambcrypto.com/will-defi-crash-the-crypto-economy-the-same-way-cdos-did/) featuring commentary by @richardred on the 'DeFi bubble', syndicated to 12 news outlets including [Crypto Fund Report](https://www.cryptofundreport.com/articles/will-defi-crash-the-crypto-economy-the-same-way-cdos-did/) and [Coingenius.news](https://coingenius.news/will-defi-crash-the-crypto-economy-the-same-way)
- an article in [The Daily Chain](https://thedailychain.com/decred-clarify-details-of-reported-vulnerability/) featuring commentary by @davecgh clarifying details of a reported vulnerability

## 活动

Attended:

- Sep 4 - [Hablemos Decred 11](https://twitter.com/Decred_ES/status/1301583356644282368) - Internet. @elian and guest Jose Zarate from Stamping.io discussed timestamping on blockchains. ([video](https://www.youtube.com/watch?v=QwsWiJ8v5qE))
- Sep 10 - [Hablemos Decred 12](https://twitter.com/Decred_ES/status/1304153821631791104) - Internet. @caibarrad and @elian invited David Riascos from @cLabs to talk about the importance of the community in the development of open protocols and the challenges of adoption in the cryptocurrency industry. ([video](https://www.youtube.com/watch?v=QC5_1PqJb_4))
- Sep 17 - [Hablemos Decred 13](https://twitter.com/Decred_ES/status/1305595709257846785) - Internet. @adcade and @elian talked with guest Nancy Salazar from Platzi about how to start a career in technology and how to overcome the challenges of complex areas such as blockchains. ([video](https://www.youtube.com/watch?v=f_ppC-GVDk8))
- Sep 25 - [Hablemos Decred 14](https://twitter.com/Decred_ES/status/1308582624772927494) - Internet. @elian and guest Eloisa Cadenas from CryptoFintech explored the origins of [maximalism](https://es.cointelegraph.com/news/wild-crypto-maximalism), the risks of such lines of thought, the future of interoperable blockchains and what are the challenges for adoption and innovation in the cryptocurrency space. The event was [announced](https://es.cointelegraph.com/news/virtual-talk-where-does-the-concept-of-maximalist-come-from) on Cointelegraph Spanish. ([video](https://www.youtube.com/watch?v=EGaMhQX3Wd4))

Upcoming:

- Oct 15 - Hablemos Decred 17 - Internet. @elian and Gus Grilliesca will explore the future of art and cryptocurrencies.
- Oct 17 - [Introduction to blockchain API](https://www.eventbrite.com/e/open-source-workshop-introduccion-a-blockchain-api-de-decred-dcrdata-tickets-124107662359) - Internet. A workshop to explore Decred blockchain with dcrdata API.
- Oct 19 - [Open Source Software Summit](https://www.eventbrite.com.mx/e/cumbre-de-contribuidores-de-open-source-software-ccoss-2020-tickets-91491063233) - Internet. @adcade will present Decred with the talk "open source contractor model in the cryptocurrency industry".

## 媒体

Decred was mentioned in a long [report](https://medium.com/greenfield-one/the-state-of-blockchain-governance-governance-by-and-of-blockchains-f6418c46077) on blockchain governance. Full 115-page PDF is [here](https://65eocu3ftlpiygeym3g5kply6zy2dtdjyrhbm4m26cb6bt3msyla.arweave.net/90jhU2Wa3owYmGbN1T149nGhzGnEThZxmvCD4M9slhY) (Decred on pages 64-66).

Selected articles:

- Why I Decred by Decred Citizen ([medium](https://medium.com/@decred.citizen/why-i-decred-8d83081b6fb8))
- Decred on-chain: DAO + Treasury accounting by @permabullnino ([medium](https://medium.com/@permabullnino/decred-on-chain-dao-treasury-accounting-afb1ed989b0a))
- Blockchain governance - Part 2 by @mm ([stakey.club](https://stakey.club/en/blockchain-gov-part2/))
- Meet the Disruptors: How Jake Yocom-Piatt of Decred aims to redefine governance, with blockchain technology by Tyler Gallagher ([medium](https://medium.com/authority-magazine/meet-the-disruptors-how-jake-yocom-piatt-of-decred-aims-to-redefine-governance-with-blockchain-5c3724f20e74))
- Monero and Decred are the new Bitcoin by John Dennehy ([medium](https://medium.com/@john_dennehy/monero-and-decred-are-the-new-bitcoin-34a8c1fb2515))

> Since decentralization is a founding principle of the crypto-space it gets a lot of lip-service but one of the oldest problems with power is that it is extremely rare that once someone has it, they will give it up voluntarily. Decred is a rare exception and notable in the progress its developers have made in converting the project's resources into this autonomous system. Monero is another outlier here, as its development is completely funded by community donations.

Crypto media has picked up the [INVDoS](https://invdos.net/) vulnerability disclosed on Sep 9, which brought some mixed press for Decred. [CoinDesk](https://www.coindesk.com/high-severity-bug-in-bitcoin-software-revealed-2-years-after-fix) release was the first and didn't mention Decred at all. Notably, it was published just 45 min after the PDF was last updated at invdos.net and 28 min _before_ the email on [bitcoin-dev](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2020-September/018164.html) mailing list. [ZDNet](https://www.zdnet.com/article/researcher-kept-a-major-bitcoin-bug-secret-for-two-years-to-prevent-attacks/) briefly mentioned Decred's bug bounty program. [Decrypt](https://decrypt.co/41685/developers-reveal-2018-bitcoin-bug-used-to-crash-entire-networks) has overblown the issue and posted some inaccuracies. [The Daily Chain](https://thedailychain.com/bitcoin-engineers-identify-and-patch-vulnerability-in-decred-btcd-blockchains/) went as far as to say that "Bitcoin engineers patched vulnerability in Decred". A common pattern is that these outlets didn't reach out for comments from the experts most familiar with the software (Decred developers). @l1ndseymm contacted The Daily Chain and they posted a follow-up [clarification](https://thedailychain.com/decred-clarify-details-of-reported-vulnerability/) with a comment from @davecgh. @degeri addressed the misinformation in a tweet [thread](https://twitter.com/degeri_crypto/status/1305591774698786821). A detailed account of media coverage, misinformation, timeline of events and reflection is available [here](https://github.com/xaur/notes/blob/master/invdos.md).

Translations:

- Meet the Disruptors: How Jake Yocom-Piatt of Decred aims to redefine governance, with blockchain technology - [in Chinese](https://github.com/Decred-CN/articles/blob/master/Meet%20The%20Disruptors.md) by @Dominic
- Politeia Digest issues 36-37 - [in Arabic](https://insaf01.github.io/politeia-digest-ar/) by @arij and @abdulrahman4
- Decred Journal August 2020 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic) and Spanish (@francov\_). Thank you all for spreading the word!

A list of all known translations of Decred content has been compiled [here](https://github.com/decredcommunity/translations/blob/master/index.md). If you enjoy DJ for reading about all the work being done for Decred, open this ~280 item list and scroll it for a minute to get a similar injection.

If you translate content, join the new public [#translations](https://chat.decred.org/#/room/#translations:decred.org) chat room to coordinate with others.

Videos:

- The Cost of attacking Decred by Decred Society ([youtube](https://www.youtube.com/watch?v=yv2wzRsK6zc))
- Security and coin supply by Decred Society ([youtube](https://www.youtube.com/watch?v=M5HWV_a1gj8))
- Going down the Decred rabbit hole by Decred Society ([youtube](https://www.youtube.com/watch?v=cI1jbIAe4YE))
- Decred price analysis - 6th September 2020 by Brave New Coin ([youtube](https://www.youtube.com/watch?v=ABjp9RYnDrk))

Audio:

- Decred in Depth 30 with @eSizeDave and @zohand of the Decred Australia team talking about their experiences presenting Decred to various audiences - what sticks, and what misses ([libsyn](https://decredindepth.libsyn.com/zohand-dave-decred-australia), [player.fm](https://player.fm/series/decred-in-depth/zohand-dave-decred-australia))
- Decred in Depth 31 with @l1ndseymm giving her take on the role of PR, her experience of working with Decred's community and going through the proposal process, and strategies for raising the project's profile. ([libsyn](https://decredindepth.libsyn.com/lindsey-mcconaghy-dcr-pr-marketing-2020), [anchor.fm](https://anchor.fm/staked-podcast/episodes/Staked-Podcast-Episode-0-0-3-ejq685/a-a38c12o))
- Cyber Hacker podcast: Crypto-Security and blockchain innovations featuring @jy-p ([player.fm](https://player.fm/series/cyber-hacker/crypto-security-and-block-chain-innovations), [apple](https://podcasts.apple.com/au/podcast/cyber-hacker/id1462830605?i=1000489977562))

The Decred dork has been busy this month, with 4 episodes of the new Staked Podcast:

- Episode 0.0.1 - History of Decred
- Episode 0.0.2 - Decred Constitution
- Staked podcast interview with @pavel
- Episode 0.0.3 - Decred investment thesis

Staked Podcast is available on [YouTube](https://www.youtube.com/channel/UCWoknbkENz-W4pg18p57rNA) (with video), [anchor.fm](https://anchor.fm/staked-podcast), [Spotify](https://open.spotify.com/show/4KWpxBXn26Ek4VVeNg8D3S) and [Google](https://podcasts.google.com/feed/aHR0cHM6Ly9hbmNob3IuZm0vcy8xNDY5ZjRlYy9wb2RjYXN0L3Jzcw==).

## 社区讨论

Comm systems news:

- traders rejoice, #trading chat is now available via [Telegram](https://t.me/DecredTrading) and is bridged to Matrix and Discord

Selected Reddit posts:

- everyone's favorite Wall Street CEO, u/jamie-demon, has been busy publishing [dcrdocs](https://www.reddit.com/r/decred/comments/j1ia6k/dcrdocs_on_ipfs_and_zeronet/), [decredpower](https://www.reddit.com/r/decred/comments/iu9f31/decredpower_on_the_ipfs/), and [DCRComic](https://www.reddit.com/r/decred/comments/iw333o/dcr_comic_on_ipfs/) to IPFS and ZeroNet distributed web networks
- a [post](https://www.reddit.com/r/decred/comments/iwu75w/bch_has_some_funding_and_governance_issues/) about BCH funding and governance issues attracted 45 comments, mostly in response to someone complaining about DCR
- @pavel is arranging an AMA interview and submitted a [post](https://www.reddit.com/r/decred/comments/j2gz5f/ask_me_anything_ama_what_would_you_ask_decreds/) to collect questions at the end of the month
- in-depth [discussion](https://www.reddit.com/r/decred/comments/i11tjv/porting_cloak_coins_enigma_protocol_and/g4psjpr/) about the merits of CloakCoin's Enigma privacy protocol with one of that project's developers

Selected Twitter discussions:

- @richardred [tweeted](https://twitter.com/RichardRed0x/status/1310700935216271360) an animated painting, titled "Ticket Price All Time Highs Again"
- latest development news breaking on twitter from [@moo31337](https://twitter.com/marco_peereboom/status/1308125042149134336) (Decentralize Treasury Spending) and [@chappjc](https://twitter.com/chappjc/status/1302798545439817730) (dcrdex)
- @jz asserts that Decred is a [#ChadCoin](https://twitter.com/jz_bz/status/1310639727477915648)

## 市场

In September DCR was trading between USD 11.03-17.30 / BTC 0.00106-0.00148. The average daily rate was $13.26.

## 相关外部信息

The Wasabi wallet was subject to a DoS [vulnerability](https://blog.wasabiwallet.io/responsible-disclosure-v4-hard-fork/) which would have allowed an attacker to halt the CoinJoin process for all participants without revealing themselves - fixed before it could be exploited.

Bitcoin Cash's current situation was [summarised](https://read.cash/@Cain/the-current-bch-drama-for-outsiders-50b4dbb8) nicely by Cain. The BCH (aka BCH ABC) chain looks set to fork over a dispute about developer funding. The Bitcoin ABC developers are adding a rule from Nov 15 that 8% of the block reward must go to an address controlled by them, to fund infrastructure development. This idea has been controversial in the BCH community for some time, and an alternative BCHN implementation is planned. This sets up an interesting hash war scenario, where ABC miners will not mine on BCHN blocks without a developers' reward, whereas the BCHN miners will mine on anything - if the BCHN chain does not have a significant majority of hashpower, BCHN miners would be likely to see a lot of orphaned blocks. BCH has a checkpointing system, which adds some further intrigue around the possibility of chain splits and new nodes ending up on different chains. So far around 50% of PoW mining power is signalling for BCHN, and the rest is not signalling for anything.

BitShares has a [forthcoming](https://finbold.com/binance-huobi-announces-support-for-upcoming-bitshares-hardfork/) hardfork which is being supported by Binance and Huobi, after the BitShares China Association alleged that one of the BitShares developers had tampered with voting system code without community approval.

The SushiSwap saga provided peak DeFi drama in September. SushiSwap is a "decentralized exchange" running on Ethereum which copied the open source smart contracts of an established (VC-funded) decentralized exchange, UniSwap. When the SushiSwap developer, Chef Nomi, announced that SushiSwap would do a "fair launch" and grant almost all the SUSHI tokens to liquidity providers, SushiSwap began to draw a lot of liquidity away from UniSwap, and SUSHI gained considerable value in a short space of time. 10% of all the SUSHI tokens go into a development fund, and when the hype was peaking Chef Nomi [liquidated](https://www.coindesk.com/sushiswap-liquidation-weekend) the dev SUSHI (worth over $10 million at the time) for ETH and announced that he was not exit scamming because he would still be around to do development, but he had sold all the dev SUSHI. This was not well received by the SUSHI community, who sought to replace Nomi in short order, with Nomi then handing the reigns (keys?) to Sam Bankman-Fried of the FTX exchange. SushiSwap then went on to elect a set of multi-sig governors with a token vote. Subsequently, Chef Nomi [returned](https://www.coindesk.com/sushiswap-creator-chef-nomi-returns-dev-fund) along with the ETH they had obtained by selling dev SUSHI, offering that the community determine how much they should be rewarded for their part. There was some speculation that Chef Nomi had been effectively unmasked and did not want to live with the stigma of their hasty exit.

UniSwap [launched](https://uniswap.org/blog/uni/) their own token, UNI, in response to SUSHI's success and the amount of liquidity it was attracting. 60% of the genesis tokens (intended to cover the first four years) are available to liquidity providers, with an initial 15% being allocated to people who had used UniSwap before a cut-off of early Sep. The remaining 40% of UNI is allocated to investors and employees.

Ethereum Classic Labs have [teamed](https://medium.com/etc-core/ethereum-classic-labs-teams-up-with-openrelay-and-chainsafe-8248d1182612) up with Chainsafe and OpenRelay to develop a solution which prevents further 51% attacks. 3 days after the teaming up announcement there is already a comprehensive [MESS](https://medium.com/etc-core/agreeing-to-disagree-proposing-a-weakly-subjective-finality-solution-for-ethereum-classic-7daad47efc0e) plan for weakly-subjective finality.

The KuCoin exchange (which lists DCR) was hacked, and a [reported](https://www.coindesk.com/hackers-drain-kucoin-crypto-exchanges-funds) $150 million was stolen, later [upgraded](https://www.coindesk.com/kucoin-ceo-says-perpetrators-of-281m-hack-identified-authorities-on-the-case) to $281 million, although $204 million was subsequently [recovered](https://www.coindesk.com/kucoin-ceo-says-perpetrators-of-281m-hack-identified-authorities-on-the-case) (with help from the operators of centralized stablecoins), and KuCoin claims to have identified the suspects and reported them to law enforcement authorities.

Coinbase Pro [announced](https://twitter.com/CoinbasePro/status/1306641678506360832) that fees for crypto withdrawals would now be passed on to customers (Coinbase had previously covered these to provide "free" withdrawals).

The bZxHQ DeFi lender was subjected to another [exploit](https://www.coindesk.com/defi-lender-bzx-third-attack), this time for $8 million, which is larger than the previous two exploits earlier this year. They have an insurance fund which is covering the damage. According to CoinDesk, "the bug managed to remain undetected in two extensive code audits from cybersecurity firms Certik and Peckshield".

Square [formed](https://www.coindesk.com/square-alliance-patents-crypto) the Cryptocurrency Open Patent Alliance (COPA), where members pledge to never assert patent rights for offensive purposes, and in turn can use the patents of any member organization defensively if required. Blockstream [tweeted](https://twitter.com/Blockstream/status/1304529416131940352) about joining COPA as the next step in their defensive patent strategy.

The Polkadot Treasury received its first [proposals](https://polkadot.network/writing-history-the-first-teams-submit-their-proposal-to-the-polkadot-treasury-2/). Polkadot's Treasury is funded by transaction fees, slashing and staking inefficiencies - and every 24 days if these funds are not used 1% of the balance is burned. The funds are presently administered by the Polkadot Council, and the first four teams to be funded this way are working on a development environment for pallet-contracts, a Go Substrate RPC Client, Polkascan, and a platform for local community currencies and self-issued universal basic income.

This [article](https://decrypt.co/41024/researchers-find-new-way-for-criminals-to-launder-money-using-bitcoin) about "private mining", where a user gives their transaction to a specific miner, who collects the associated reward whenever they mine it in a block, sees it as a possible tool for money laundering, and in the future potentially also a legitimate source of miner income.

The United States Internal Revenue Service are [offering](https://cointelegraph.com/news/the-irs-offers-a-625-000-bounty-to-anyone-who-can-break-monero-and-lightning) a bounty of $625,000 to anyone who can provide a working prototype of technology to trace Monero or Lightning Network transactions. The deadline was Sep 16, so unfortunately it is now too late to cash in on that privacy-breaking prototype, if you happen to have one to hand.

Relevant External fans will likely enjoy the [@Scams_alarms](https://twitter.com/Scams_alarms) Twitter account for more horrifying stories.

## 关于月报

这是Decred Journal的第30期。有关所有问题，镜像和翻译的索引，请参见 [此处](https://xaur.github.io/decred-news/).

在经过最少的健全性检查之后，来自第三方的大多数信息都会直接从来源中继。Decred Journal的作者无权验证所有声明。请当心诈骗，并自行进行调查。

我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。您可以在[这里](https://github.com/xaur/decred-news/labels/next%20release)提交故事。

感谢 (字母排列):

- 写作和编辑: bee, degeri, elian, l1ndseymm, lukebp, matheusd, richardred
- 评论和反馈: Checkmate, davecgh, jazzah, jholdstock, pavel
- 封面图片: saender

## 中文社区

* [社区网址](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [优酷频道](https://i.youku.com/decredproject)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息
