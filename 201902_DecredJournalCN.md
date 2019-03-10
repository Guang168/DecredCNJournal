# Decred月报 - 2月 

![abstract art](img/journal-201902-384.jpg "Objective Constructs by @saender")

祝 Decred 生日快乐！自 2016年2月8日的[第一个区块](https://explorer.dcrdata.org/block/1)已经渡过3年了。

二月份里我们在 Politeia 上很活跃，有7个新提案提交，5个提案开始投票及在3月份的前几天里通过了4个提案。总额 490,000 美元的2019年宣传及活动预算已正式投票通过。

网络升级也已经[达到](https://voting.decred.org/)需要支持闪电网络的共识更改投票门槛，共识更改投票预计将在 3月14日 开始。

如果你还没升级，[v1.4.0 发布版本](https://github.com/decred/decred-binaries/releases/tag/v1.4.0)包含了很多改进。如果投票通过了，节点需要这个最新版本继续运行升级后的区块链。同时请务必[验证下载软件](https://docs.decred.org/advanced/verifying-binaries/)并呼吁其他朋友们升级哦。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd):通过允许[少一个](https://github.com/decred/dcrd/pull/1596)选票双重支付和[拒绝](https://github.com/decred/dcrd/pull/1597)同区块的双花来收紧mempool政策。 从dcrd[删除](https://github.com/decred/dcrd/pull/1607)钱包的类型并[迁移](https://github.com/decred/dcrwallet/pull/1394)到dcrwallet，这简化了对dcrwallet的更改，并在dcrd中触发[重构](https://github.com/decred/dcrd/pull/1613)，以提供更强大的模块边界并简化依赖图。[删除](https://github.com/decred/dcrd/pull/1599)非root 的Go模块替换 - 这有助于确保测试中的所有模块为最新代码，并帮用户保持它们独立准确。

[dcrwallet](https://github.com/decred/dcrwallet): v1 自动购票经过数个更新版本后已[被移除](https://github.com/decred/dcrwallet/pull/1396)。

[Decrediton](https://github.com/decred/decrediton): Electron 4 [升级](https://github.com/decred/decrediton/pull/2009)让在 Windows 启动[更稳定](https://github.com/decred/decrediton/pull/2017)。在自动购票运行时增加[退出提醒](https://github.com/decred/decrediton/pull/1989)。多个[响应视图](https://github.com/decred/decrediton/issues?q=is%3Aissue+author%3AMariaPleshkova+created%3A2019-02-01..2019-02-28)已完成设计阶段并准备实施。

[Politeia](https://github.com/decred/politeia): 新功能: 突出显示自上次登陆的新评论及密码更改后邮件[通知](https://github.com/decred/politeia/pull/680)(通过Bug Bounty漏洞报告奖励计划[提议](https://github.com/decred/politeia/issues/673))。

一项大的缓存层工作已被[合并](https://github.com/decred/politeia/pull/660)! 感谢 @lukebp 和所以参与评论/测试的人员。这为许多网页性能改进铺了路。其他已完成的工作包括 CLI 工具[改进](https://github.com/decred/politeia/pull/707) 及 dcrtime 的[文件系统验证工具](https://github.com/decred/dcrtime/pull/46) fsck (file system verification tool)。
进行中:

* 使用 CockroachDB 扩展 www 数据库的工作已经[开始](https://github.com/decred/politeia/pull/689)。 
* 开发员[决定](https://matrix.to/#/!VFRvyndKpzcLrVslQD:decred.org/$15507680085008gMbtf:decred.org)将承包商管理系统的代码移去 politeia 及 politeiagui 代码库以避免维护两个分叉代码并保持两份代码同步的工作。
* 更改默认评论排序算法的[讨论](https://github.com/decred/politeiagui/issues/1022).

[dcrandroid](https://github.com/decred/dcrandroid): 多个漏洞修复及小改进等待整合中，详情请参照[项目告示板](https://github.com/decred/dcrandroid/projects/1)。

[中文](https://github.com/decred/dcrandroid/issues/336) 及 [越南语](https://github.com/decred/dcrandroid/pull/333) 翻译进行中。

[dcrios](https://github.com/raedahgroup/dcrios): 已更新 TestFlight[beta测试版](https://testflight.apple.com/join/dvq51tCh)及正在更新以达到dcrandroid版本水平。在[这里](https://github.com/raedahgroup/dcrios/projects/1)查看进度。

第一测试版预计一个月后发布，同时预计应该也有一个dcrandroid更新发布。

[dcrdata](https://github.com/decred/dcrdata): 增加显示[Politeia proposals](https://github.com/decred/dcrdata/pull/1016)数据功能，增加[法币换算](https://github.com/decred/dcrdata/pull/1049) (供应, 基金会, 选票价格),[重组](https://github.com/decred/dcrdata/pull/982)内存池页面，终端获取[原区块](https://github.com/decred/dcrdata/pull/1032) 及 [原区块头](https://github.com/decred/dcrdata/pull/1035)，增加[缓存](https://github.com/decred/dcrdata/pull/1051) 包.

[关于](https://github.com/decred/dcrdata/issues/1022) 如何计算51%攻击加入到dcrdata的讨论。

[Ticket splitting](https://github.com/matheusd/dcr-split-ticket-matcher): @matheusd [分享](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$1549497567273IPjZq:decred.org) 他关于分票的想法，背景及接下来的计划。@david 录制了设置分票的教程[影片](https://www.youtube.com/watch?v=9L8P7hL5v6w)。

[docs](https://github.com/decred/dcrdocs): 解释 [Politeia 审查](https://docs.decred.org/governance/politeia/politeia-censorship/)及如何证明内容被屏蔽的新页面, 新[升级 Decrediton](https://docs.decred.org/wallets/decrediton/upgrading-decrediton/)页面, 测试网选票矿池列表已列入到[使用测试网 Using Testnet](https://docs.decred.org/advanced/using-testnet/)页面, P2PKH 地址生成流程图列入[地址细节Address Details](https://docs.decred.org/advanced/address-details/)页面。 [恢复](https://github.com/decred/dcrdocs/pull/846)搜索功能。

[decred.org](https://github.com/decred/dcrweb): 内容及翻译更新。[开始](https://github.com/decred/dcrweb/issues/561)筹划实施新闻及文章的页面.

其他:

* @matheusd 的[部落格](https://matheusd.com/post/dcp0004-and-hardforks/)写了关于DCP0004 一些有趣的细节： Decred 的 PoS 部分可以充当意外共识漏洞的多一层保护
* [voting.decred.org](https://voting.decred.org/) 仪表板也显示过去的议案。jQuery 已被[移除](https://github.com/decred/hardforkdemo/pull/213)。
* Google reCAPTCHA 替代自托管方案已[merged](https://github.com/decred/dcrstakepool/pull/281) - 这是增加[用户](https://github.com/xaur/decred-issues/issues/25)的一大步。感谢为这个补丁努力的开发员和测试员。
* 有趣答题: 你是否知道 Decred 非常[不鼓励](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15497657664963CvzUr:decred.org) 微额输出?
* 原子交换的[概念证明PoC UI](https://github.com/xaur/decred-issues/issues/8)开始有点进展。
* 支持QTUM的代码在原子交换[被合并](https://github.com/decred/atomicswap/pull/93), 支持POLIS的代码已被[移除](https://github.com/decred/atomicswap/pull/99).
* 为 dcrseeder 增加 DNSSEC 的工作已经[开始](https://github.com/decred/dcrseeder/pull/19)
* [authit](https://github.com/decred/authit), 即 dcrtime 的 UI 已经在[timestamp.decred.org](https://timestamp.decred.org/)托管。欢迎到[GitHub issues](https://github.com/decred/authit/issues)或新的 [#timestamp](https://matrix.to/#/!gltiHJRZiSJTzvjOEu:decred.org) 聊天室提出反馈。

> 我必须说, Go 真的是一个神奇的编程语言。我想我未试过在一个新的编程语言里感到这么舒服。(@jholdstock 在 [聊天室](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15497080644503VtguR:decred.org))

---

## 人员

欢迎新到来的首次贡献者，代码在 GitHub 上合并：@jozn ([dcrd](https://github.com/decred/dcrd/commits?author=jozn)), JoeGruffins ([dcrwallet](https://github.com/decred/dcrwallet/commits?author=JoeGruffins)), luoshang722 ([atomicswap](https://github.com/decred/atomicswap/commits?author=luoshang722)), rex4539 ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=rex4539)).

恭喜在decred.org上[列出的](https://github.com/decred/dcrweb/issues/562)三位Ditto承包商

* Elizabeth Bagot (@liz_bagot)
* Margaret Huang (@margaret_mei)
* Milvian Prieto (@milvian)

1名贡献者从decred.org中[移除](https://github.com/decred/dcrweb/pull/541)：Jure Kralj (@praxis, Reddit 管理员).

## 治理

在 2月里，[DCR基金会](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了 14,878 DCR，并花了 17,311 DCR，二月份是项目这么久以来第一个月开销多于收入。使用 DCR 在2月份的每日平均美元价格 16.51 美元计算，本月收到 24.6 万 美元以及支出 28.6 万 美元。由于这些付款用于支付 1月完成的工作，因此可以用 1月的平均价格 17.06 美元计算 - 在这种情况下，美元收到的数字是 25.4 万美元以及支出 29.5 万美元。3月9日为止，基金会余额为 605,828 DCR(按 16.6 美元计算相当于 一千零五万 美金)。

于3月9日的提案状态:

* [Baeond 卡牌游戏](https://proposals.decred.org/proposals/f545b359fcf1b40b356e9cb556cb422cc7ff01b628b577f804cdc45ce414f5dd) 由 burst提出，由29%的参与率和97%反对票不通过 _(1月份月报遗漏)_.
* [去中心化交易所的提案邀请 Decentralized exchange RFP](https://proposals.decred.org/proposals/5431da8ff4eda8cdbf8f4f2e08566ffa573464b97ef6d6bae78e749f27800d3a) 由 @jy-p 提出，收到 70 评论。第二版本降低了 MVP 的范围并将成本上限设为 25万美元(之前为100W)。@bee 发布了一份个人的赞成和反对
[分析](https://github.com/xaur/decred-proposals/blob/master/decred-dex-rfp-analysis.md)。改提案也引起了基金会是否资助推广这类提案的[讨论](https://www.reddit.com/r/DCR/comments/awbtbr/should_treasury_funded_marketing_resources_be/)。本提案投票已开始 3月9日 为止参与的 8千票中% 91.4%为同意票。
* [钱包教程提案 Wallet tutorials](https://proposals.decred.org/proposals/a3def199af812b796887f4eae22e11e45f112b50c2e17252c60ed190933ec14f) 由 Cryptocurrency.Market 的 Denni Lovejoy 提出。该提案经历了多个在[聊天室](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154941035930084kFSjY:decred.org)和 [Reddit](https://www.reddit.com/r/decred/comments/anksg2/proposed_statement_of_work_sow_for_decred/) 的反馈及更改。750美元的预算以 24% 参与率和 80% 同意票通过。
* [2019活动资金预算 Events funding for 2019](https://proposals.decred.org/proposals/d3e7f159b9680c059a3d4b398de2c8f6627108f28b7d61a3f10397acb4b5e509) 由 @Dustorf 提出。该提案在[聊天室](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154896889724431Mxlvj:decred.org)和 [Reddit](https://www.reddit.com/r/decred/comments/anhh8n/proposal_to_get_events_spending_approved_via/)预览后提出。20万美元的预算投票以 34% 参与率和 89% 同意票通过。
* [2019宣传预算 Marketing funding for 2019](https://proposals.decred.org/proposals/c84a76685e4437a15760033725044a15ad832f68f9d123eb837337060a09f86e) 由 @Dustorf 提出。收到 68 评论，以及在[聊天室](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154897255124536mFHoo:decred.org)和 [Reddit](https://www.reddit.com/r/decred/comments/aolr79/politeia_proposal_to_fund_marketing_ops_for_2019/) 中讨论。29万美元的预算投票以 36% 参与率和 83% 同意票通过。
* [Decred ATM 集成提案 Decred ATM integration](https://proposals.decred.org/proposals/aea224a561cfed183f514a9ac700d68ba8a6c71dfbee71208fb9bff5fffab51d) 由 @oregonisaac 提交。改提案是从2018年11月份 Bcash ATM [提案](https://proposals.decred.org/proposals/bb7e19283d5c65fed598d5a2f4afcc2b5d2eab187b9cb84fc4304430f80b5ad1)及多个星期的研究，草案，反馈的结果。目前提案要求获取利益相关者意见是否继续筹划 ATM 集成。通过后，另一份提案将提供实施细节投票决定。
* [Decred社区网站 Decred community website](https://proposals.decred.org/proposals/fb8e6ca361c807168ea0bd6ddbfb7e05896b78f2576daf92f07315e6f8b5cd83) 由 @karamble 提出。该提案提出整合各资源Decred 相关内容的网站。内容包括文章，视频，播客，活动报告及商家。该原型已由 @karamble 建造，该提案要求 6,000 美元资助该网站6个月。投票以 33% 参与率和 72.5% 同意票通过。
* [Decred IDAX 交易所整合 Decred integration for IDAX exchange](https://proposals.decred.org/proposals/60adb9c0946482492889e85e9bce05c309665b3438dd85cb1a837df31fbf57fb) 由 acean 提出。该提案要求 1,000 DCR 以上线在蒙古的IDAX交易所 DCR/BTC 交易对。投票以 23.5% 参与率和 25% 同意票不被通过。
* [Trust Wallet 钱包整合提案 Decred integration in Trust Wallet](https://proposals.decred.org/proposals/2ababdea7da2b3d8312a773d477272135a883ed772ba99cdf31eddb5f261d571) 由 @oregonisaac 提出。提案预算 3,300 美元整合“完全去中心化”钱包 Trust Wallet 并提供大概每月 100 美元的维护支出。投票尚未开始。

Politeia 在 2月 1-28日 活动:

* 7 份新提案提交，5 份提案开始投票。
* 来自 46 不同用户(公钥)的 300 个 Politeia 提案评论。
* 来自 56 个不同投票用户(公钥)的评论上 1,006 个 upvote/downvote。
* 748 upvotes (70%) 和 258 downvotes (30%)。

自上线至 Feb 28, 2019 数据:

* 来自 113 不同用户(公钥)的 802 个 Politeia 提案评论。
* 来自 122 个不同投票用户(公钥)的评论上 2,785 个 upvote/downvote。
* 2,336 upvotes (80%) 和 449 downvotes (20%)。
* 共有 32 个投票用户从未留评论，他们合共投出 374 评论票 (总数的13.4%）
* 大约 238 评论 (30%) 被作者本身 upvote。
 
感谢 @richardred 将以上数据生成自动化。

有关修改 Decred 宪法及通过 Politeia 投票批准新版本讨论已经开始进行中。初始目标是通过最少改动先将过期或不相关部分去除并增加缺少的部分。在讨论过程中有人提考虑到宪法并没有约束力，我们是否真正需要宪法。所有讨论及提议修改的内容的链接都收录在[这issue](https://github.com/xaur/decred-issues/issues/107)。

一个新的推特账户 [@pi_crumbs](https://twitter.com/pi_crumbs)将推送提案创建或修改，投票开始及结束消息。目前由 @richardred 手动操作，但讨论将其自动化也在进行中。

另一个推特账户 [@slices_of_pi](https://twitter.com/slices_of_pi) 将推送手动编写有关 Politeia 活动的评论。

更多细节，分析与评论请参考 @richardred 的 Politeia 简报 [第10期](https://medium.com/politeia-digest/issue-10-jan-1-feb-18-2018-202cde71a19d) 及 [第11期](https://medium.com/politeia-digest/issue-11-feb-19-feb-28-2019-46befddb09fe)。以上重点总结于 Politeia 简报。

## 网络

算力: 2 月算力以 ～230 Ph/s 开始，以 ～300 Ph/s 结束，本月中最高 420 Ph/s 及最低 210 Ph/s。在3月5日根据 [dcrstats.com](https://dcrstats.com/pow) 数据显示，矿池算力分布为：BTC.com 31%, Poolin 27%, F2Pool 18%, UUPool 15%, Luxor 4%, CoinMine 1% 及其他 5%。矿池分布数据为大约值无法精确计算。 

投票: 按3月1日 dcrstats.com（数据显示）, 30日 平均票价为 111.6 DCR (+2.2)。价格在 98.4 DCR 至 124.1 DCR之间浮动。锁仓数额为 4.36-4.56 百万 DCR, 大约为总流通量的 46.4-48.7%。


选票价格及选票池大小在二月中经历了不寻常的波动。在2月11日同一个区间内购买的1,265张选票把选票池的选票拉到 ～41，670张选票及后面7次票价调整中涨至 119.4。随后选票池票数下跌至低于4万张选票 （上次发生于2017年11月），导致连续10次调整降至 98.4 DCR。在票价到底时，在同一区间内又卖出最高2，880 张中的2，797 张选票。@ImacallyouJawdy提出在单单这一区间选票就锁定了 282k DCR 或 DCR 流通量的 3%。因此选票价格跳跃至 124.1 DCR，这是自 2017年7月 选票价格算法调整后的新高。选票池最高峰是锁定了 42，174 选票，等同于 DCR 供应的 48.7% - 创新高并且比前一个在2018年6月7日的高峰高出 +0.7%。感谢 charts.dcr.farm 里准确的图表。

节点: 截止于3月1日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 205 public listening Node 及 297 Normal Node。版本分布: v1.5.0 dev builds: 8.6% (+4.3%), v1.4.0 final: 43% (+43%), v1.4.0 dev and rc builds: 7% (-6%), v1.3.0: 23% (-32%), v1.2.0: 10% (-4%), v1.1.2: 4% (-4%), v1.1.0: 2% (-1%)。

PoW 和 PoS 的[升级门槛](https://voting.decred.org/)已经完成，共识投票已经锁定并在大约 3月14日开始。感谢所有通过各种渠道帮忙联系 PoW 矿池及 VSP 运营商（选票矿池）并呼吁他们升级的人员。

The vote did not start yet but block votes already signal their choices for `fixlnseqlocks` agenda. As of Mar 4 there [were](https://matrix.to/#/!wSdymYrEpBhsWlDJuk:decred.org/$155168912215429iStcp:decred.org) 8,503 Yes and 1 No vote. "Dat contrarian... At least it's proof that the no button works." - @jz.


## 整合

选票矿池 VSP 代号 "Bravo" 已从 dcr.stakepool.net [重命名](https://github.com/decred/dcrwebapi/pull/59)为[dcr.blue](https://dcr.blue/)。

交易所整合:

* [Vertbase](https://www.vertbase.com/)已增加 DCR/USD 交易对。Vertbase CEO 兼 联合创始人 Justin 加入 #general 并[回答 Vertbase 相关问题](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155015221011045eRXdT:decred.org)。答案中总结：Vertbase目前支持 50 个美国州中的 39 个，正积极增加 GBP/EUR/AUD 交易，并使用第三方处理身份认证。其中一个 Vertbase 特色为短时间的托管：他们在银行转账过账后将代币直接转入用户钱包。

> 我们也需要您提供钱包地址，因为我们不想托管，也不想你使用我们的平台托管您的加密货币。成为您自己的银行！(@Justin 在[#general](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155017217111507BsAmt:decred.org)说道)

3月 8日为止，卖单并未仍无法使用。请参考这个 [Reddit 帖](https://www.reddit.com/r/decred/comments/aqkl1p/vertbase_lists_decred_dcr_with_us_dollar_usd/).

* [Lykke](https://www.lykke.com/) [已加入](https://twitter.com/lykke/status/1095352586545319937) DCR 与 BTC 和 USD 交易对。
* [ChainRift](https://www.chainrift.com/) 已整合 DCR。
* [Livecoin](https://www.livecoin.net/) [已加入](https://twitter.com/livecoin_net/status/1098151449786118144) DCR 与 BTC, ETH 和 USD 交易对。
* [BitMesh](https://bitmesh.com/) [推出](https://www.reddit.com/r/decred/comments/av8a69/bitmesh_has_launched_dcr_and_opened_dcrbtc/) DCR 与 BTC 和 USDT 交易对。

警告: Decred 月报作者无法确认以上交易所可靠性。请自行进行审核[才](https://twitter.com/yeppoon/status/1095857386709893120)将您的个人信息或财产信托于任何实体。

## Adoption

CoinFund [announced](https://blog.coinfund.io/announcing-grassfed-network-and-decred-staking-pool-with-placeholder-55a32a312710) Grassfed Network, an initiative that uses 'generalized mining' to directly participate in decentralized network. The story was featured in [CoinDesk](https://www.coindesk.com/these-cryptofunds-say-generalized-mining-is-the-new-way-to-invest).

Any activity that is compensated with on-protocol rewards denominated in network assets can be seen as [generalized mining](https://grassfed.network/mining/). Following this approach investors can directly engage in the networks and generate additional returns, compared to just speculating on the value of cryptoassets.

Per the announcement, CoinFund partnered with [Placeholder](https://www.placeholder.vc/) who plans to delegate its own voting tickets to the [Decred VSP](https://dcr.grassfed.network) launched in January. This plan was voiced earlier by Joel Monegro and Chris Burniski during the [panel](https://www.youtube.com/watch?v=tkllaH0Y0ng) at Texas Bitcoin Conference 2018. [CoinFund](https://coinfund.io/) is a cryptoasset-focused investment and research firm founded in 2015 and based in New York, USA.

## 外联活动

In February, @Dustorf proposed his plans for [marketing](https://proposals.decred.org/proposals/c84a76685e4437a15760033725044a15ad832f68f9d123eb837337060a09f86e) and [events](https://proposals.decred.org/proposals/d3e7f159b9680c059a3d4b398de2c8f6627108f28b7d61a3f10397acb4b5e509) for the remainder of 2019 and these were passed by stakeholder voting. This is an exciting development that further decentralizes Decred by shifting more direct control over spending to the stakeholders. There was vigorous discussion and many good questions, but the proposals were approved by 83% and 89% of tickets that voted.

With an approved budget, work began in earnest on the scope of the proposals. Planning is underway on NYC Blockchain Week, which coincides with Consensus. More information should be announced within two weeks on these plans.

The first podcast is underway and scheduled to deliver in March. It will feature Decred Jesus, who will provide a colorful overview discussion of Decred as seen from the ground. Work on the website is underway, with architecture, copy-writing and video scripting already begun.

The Decred Assembly and the newsletter are tactics we hope to deliver by the end of this month.

February update from Ditto:

* Media trained 5 Decred community members.
* Secured media coverage: 15-minute [interview](https://blocktv.com/watch/2019-02-20/5c6d6a2be03e3-chain-breakers-promoting-constant-disruption-) between @jy-p and BlockTV, a feature [article](https://www.forbes.com/sites/leslieankney/2019/02/04/no-more-trading-or-listing-fees-decred-releases-new-dex-proposal/) for the DEX proposal in Forbes, a feature [article](https://breakermag.com/as-decred-turns-three-its-still-set-on-real-decentralization/) in honor of Decred's 3rd anniversary in Breaker Mag, an [article](https://www.theblockcrypto.com/2019/02/13/they-asked-us-for-3-million-an-inside-look-into-getting-listed-on-a-crypto-exchange/) on the Vertbase listing in The Block Crypto featuring quotes by @jz. The journalist, Frank Chaparro, said the story was very popular on Twitter and also internally at The Block
* Facilitated 2 interviews with crypto media outlets.
* Worked with the community to create a repository of media-friendly images that we can share with reporters to add visuals to stories about Decred.
* Helped plan the logistics and content for the event hosted by Decred and OKCoin in San Francisco. Worked with Dustin and OKCoin to draft the Eventbrite copy, coordinate with OKCoin, develop the agenda for the event, and draft a press release.
* Put together a plan to position Decred as a superior store of value among a variety of channels, including initiating long-term conversations with select top tier mainstream reporters.
* Worked with Dustin on a master six-month marketing and communications plan spanning PR, events, content, etc. As part of this strategy, we aim to build Decred's legitimacy and credibility among institutional investors. That entails thinking beyond media relations to span other disciplines as well: owned content, Twitter, influencers, events, etc.

For more detail see Ditto's biweekly updates on [Feb 4](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154930816328395IaXDr:decred.org) and [Feb 15](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$155026927613161McEtC:decred.org).

Long [discussion](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$15498862365982zjzwP:decred.org) about perception and framing was triggered by a question whether to use word "bug" in public messaging for 1.4 release.

## 社区活动

出席：

* [TabConf](https://tabconf.com/) in Atlanta, USA. @joshuam [noted](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15497319564677Cmutw:decred.org): "Tabconf was awesome. Extremely engaged audience - best questions I have received at a conference to date".
* [Campus Party](http://brasil.campus-party.org/cpbr12/patrocinadores/) in Sao Paulo, Brazil. About 60,000 people passed through the event which was running 24 hours a day for 6 days. Decred was the only cryptocurrency participating officially and with an exclusive space to present lectures and classes. All Brazilian developer contractors attended and presented a total of 6 talks and 3 workshops. @jy-p presented [Cryptocurrency Security and Adaptability](https://www.youtube.com/watch?v=SMiHku6GGmI). There were a few problems like Decred's zone moved and reduced (happened to almost all participants) and poor organization of translations - all taken into account for future planning. See [full report](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155200602520229ditLj:decred.org) by @emiliomann and [notes](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155197226472913itWWu:matrix.org) by @matheusd.
* Love Night in Ghana. Organized by @George Pro. Since about 90% of participants knew about Bitcoin, presenters could skip the basics and highlight unique features of Decred. One popular question was where DCR can be exchanged to local currency. ([photos](https://twitter.com/deCRED_Ghana/status/1096714039978266624))
* [How To Keep Your Crypto Secure](https://www.meetup.com/Decred-Australia/events/258211699/) in Melbourne, Australia. Australia's cryptocurrency enthusiasts discussed best security practices and Decred's security standards. @Zohand [noted](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15504942691141LtOxa:decred.org): "Feedback was awesome, and the guys from coinstop and CTRL want to run the event again in a couple of months.". ([photos](https://twitter.com/DecredAustralia/status/1097478053763018752))
* [Decred in 30 minutes](https://www.eventbrite.com/e/decred-en-30-minutos-tickets-55764142050) in Mexico City, Mexico. @elian [reported](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15517155592047249xtYGy:matrix.org): "It was the first meetup where everyone knew about Decred quite well, we were 7 in total. The presentation went faster because attendees knew most of the fundamental content in advance so we went to discuss more complex issues like what are the challenges to decentralized governance, best way to stake tickets and future developments that are happening in the project like LN, payments integration and the most recent events, marketing and community proposals in Politeia. Was very nice to meet proper DCR enthusiasts in Mexico. (...) I think we are far from seeing cc as MoE in Mexico but definitely the space is moving fast. At the moment there are more Mexicans in contact with crypto than with the stocks markets in the country, this is a very good indicator.". ([photos](https://twitter.com/DecredESP/status/1102594478664232960))
* Talk in UAEM University in Ecatepec, Mexico. @elian [shared](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$1551994219193770GeoIk:matrix.org): "I spoke about the history of money, the Internet, Bitcoin's blockchain, Decred's hybrid blockchain and how to work in the cryptocurrency & blockchain industries. They were fascinated by the innovation of cryptocurrencies and blockchain, both students and teachers. The audience was mainly composed by computer science students. The main questions went around what is money, how to value cryptocurrencies and what are the potential work opportunities for fresh grads in the industry. (...) Doing talks in universities is a big deal for me because I know that the next generation of devs, lawyers, accountants, etc, that will be working on the industry is there and they are eager to know more about what opportunities this industry brings. Teachers were very excited to have this subjects presented to their students because is not easy to get such high tech talks to universities that are not in the centre of the city.".
* [Decred Meetup](https://www.eventbrite.com/e/decred-meet-up-tickets-57073786231) in Winneba, Ghana. Organized by @George Pro, who [noted](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155133397211500yxtpJ:decred.org): "Our first meetup in Ghana was successful. We took our time to explain to the participants how to stake DCR, how to get DCR (Coinomi process), using it as remittances, wallet set up, speed and privacy among others.". ([photos](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155133397211500yxtpJ:decred.org))
* Talk at Qingdao University in Qingdao, China. [@wanbihou](https://twitter.com/wanbihou) talked about Decred's community governance model and the upcoming on-chain consensus vote. "The students were very enthusiastic!". ([photos](https://twitter.com/wanbihou/status/1101131545010556928))


即将到来的：

* [Decred & OKCoin Present "The Next 10 Years: Crypto Boom, Bust, or Buidl?"](https://www.eventbrite.com/e/decred-okcoin-present-the-next-10-years-crypto-boom-bust-or-buidl-tickets-57549671617) 美国三藩市，3月12日。OKCoin 的 CEO Tim Byun, Decred 的 Jake Yocom-Piatt, 代表 Placeholder 的 Chris Burniske 和 Alex Evans 将讨论 Decred 和加密货币的未来。
* [Restoring Trust through Blockchain Governance](https://www.meetup.com/DecredCanada/events/259126224/) 加拿大多伦多，3月16日
* [Berlin Blockchain Week](https://www.berlin-blockchain-week.com/) 德国柏林，3月27日 @karamble 将发表演说
* [Jalisco Talent Land](https://www.talent-land.mx/#entradas) 墨西哥瓜达拉哈拉，四月22-26日。细节可联系@elian
 
在治理部分提到，利益相关者通过了价值 200K 美元的[2019年的活动预算](https://proposals.decred.org/proposals/d3e7f159b9680c059a3d4b398de2c8f6627108f28b7d61a3f10397acb4b5e509), 当中包含了参与 3 个大型活动及出席多个小型活动。

## 媒体

部分文章:

* Decred evaluation by TokenGazer (Chinese, [qq.com](https://mp.weixin.qq.com/s/7rMaTYXIhIpO37qiIvJX_A), _missed in Jan issue_) - Decred was rated 4.2
* Which one is the best cryptocurrency next to bitcoin? answer by Pavel Svitek ([quora.com](https://www.quora.com/Which-one-is-the-best-cryptocurrency-next-to-bitcoin/answer/Pavel-Svitek)) - thanks to Pavel for presenting Decred to Quora
* No More Trading Or Listing Fees? Decred Releases New DEX Proposal by Leslie Ankne ([forbes.com](https://www.forbes.com/sites/leslieankney/2019/02/04/no-more-trading-or-listing-fees-decred-releases-new-dex-proposal/))
* How Long Will Crypto Winter Last? We Asked Three Experts by Julia Herbst ([breakermag.com](https://breakermag.com/what-the-longest-ever-bear-market-means-for-crypto/))
* As Decred Turns Three, It's Still Set on Real Decentralization by David Z. Morris ([breakermag.com](https://breakermag.com/as-decred-turns-three-its-still-set-on-real-decentralization/)
* Decred Founder Proposes Building DEX as Alternative to Binance (Interview) by Liam Kelly ([cryptoslate.com](https://cryptoslate.com/decred-founder-proposes-dex-binance-interview/))
* "They asked us for $3 million": an inside look into getting listed on a crypto exchange by Frank Chaparro ([theblockcrypto.com](https://www.theblockcrypto.com/2019/02/13/they-asked-us-for-3-million-an-inside-look-into-getting-listed-on-a-crypto-exchange/))
* Cryptonetwork Governance as Capital by Joel Monegro ([placeholder.vc](https://www.placeholder.vc/blog/2019/2/19/cryptonetwork-governance-as-capital))
* Using Governance To Decide The Future: Is Decred (DCR) Going to Build a Decentralized Exchange? by @richardred ([investinblockchain.com](https://www.investinblockchain.com/is-decred-dcr-building-decentralized-exchange/), also [in Chinese](https://0xzx.com/2019022708166553.html))
* Decred mentioned in [Forbes](https://www.forbes.com/sites/samantharadocchia/2019/02/05/everything-about-the-digital-nomad-lifestyle-sounds-great-except-the-us-tax-system/) and [Breaker Mag](https://breakermag.com/bruce-schneier-is-right-about-blockchains-biggest-flaw-and-completely-wrong-about-its-longterm-significance/) stories.

Videos:

* Decred AMA TruStory - Preethi Kasireddy chats with Isaac J and Matheus of Decred to learn more about the hybrid proof of work/proof of stake consensus mechanism and their governance model ([youtube](https://www.youtube.com/watch?v=OKdaa630YDk))
* Cryptocurrency Security and Adaptability - talk by @jy-p at Campus Party Brazil ([youtube](https://www.youtube.com/watch?v=SMiHku6GGmI))
* The Potential of Decentralization - interview with @jy-p for BlockTV ([blocktv.com](https://blocktv.com/watch/2019-02-20/5c6d6a2be03e3-chain-breakers-promoting-constant-disruption-))

Audio:

* ITK Crypto #8 - Tom White 和 Crypto SI 对 @kozel 关于加密货币治理的访问 ([youtube](https://www.youtube.com/watch?v=H-qZBsQY5BM))

翻译:

* Decred 月报 - 2019年 1月 [中文](https://www.jianshu.com/p/097265621ef6) 来自 @guang (和 Dominic, Hugo 及 Jill), 来自 @elian 的[西班牙语](https://medium.com/@decred_es/revista-decred-enero-2019-549e2b051f5a)。感谢！


## 社区

截止于 Mar 1 的社区数据 :

* Twitter followers: 39,797 (+19)
* Reddit subscribers: 9,365 (+35)
* Matrix users: 266 (+19)
* Slack users: 6,581 (+52)
* Discord users: 2,101, can post: 131
* Telegram users: 4,272 (-231)
* YouTube subscribers: 3,746 (-6)
* Facebook followers: 3,141 (+9), likes: 2,896 (+5)
* LinkedIn followers: Decred page 483 (+17), Politeia page 29 (+2)
* GitHub dcrd stars: 474 (+6), forks: 1,237 (+16)

电报群社区: 中文 866 (+53), 意大利语 160 (+28), 葡萄牙语 642 (+100), 西班牙语 73 (+11).

中文社区在二月非常活跃 ：

* 开启了[#chinese](https://matrix.to/#/!nUWpVrwhlJFyLuMlGw:decred.org)中文聊天室
* 殷国超继续贡献 Decred 文章: 一篇关于 [dcrtime](https://mp.weixin.qq.com/s/ks48Piu3s2zy4btZW0kBDQ)和一篇关于[原子交换](https://mp.weixin.qq.com/s/Lgem_BqFBnLUsY7AzC5x_w)
* Dominic 在青岛大学给部分同学[介绍](https://twitter.com/wanbihou/status/1101122114118184961)区块链和 Decred 。
* 殷国超文章促使另一位社区成员[写更多](https://teakki.com/p/5c774a9ab1029f607605bc76)关于 dcrtime 并制作了将文件及文字时间戳的[网页 UI](http://www.ibitlin.com/dcrtool#/dcrtime)(dcrtime 的 UI在[这里](https://github.com/xaur/decred-issues/issues/9)记载)。

社交系统新闻：

* 非英语聊天室重新根据语言命名，并移除了不再使用的聊天室。目前Matrix上已有中文[#chinese](https://matrix.to/#/!nUWpVrwhlJFyLuMlGw:decred.org), 葡萄牙语[#portuguese](https://matrix.to/#/!FBtUquQLhAvHeBIkac:decred.org), 俄语[#russian](https://matrix.to/#/!TQzfaYsKyxAqQDZQeX:decred.org)及西班牙语[#spanish](https://matrix.to/#/!pkeRzinGCRtjIIhAAK:decred.org)
* [Riot](https://riot.im/app/#/room/#general:decred.org) 客户端配合更新的 UI 已[升级](https://medium.com/@RiotChat/the-big-1-0-68fa7c6050be)至版本 1.0。

Another Reddit thread was [deleted](https://www.reddit.com/r/decred/comments/an4b6z/forbes_no_more_trading_or_listing_fees_decred/) after receiving some discussion. Moderators have no power to forbid this destruction of community knowledge, except the workaround to [resubmit](https://www.reddit.com/r/decred/comments/ar29jd/forbes_no_more_trading_or_listing_fees_decred/) the deleted thread. Ideas for robust replacement for Reddit are collected in [this issue](https://github.com/xaur/decred-issues/issues/38).


## 市场

在二月中 DCR 交易价格为 美金 14.97-18.28 / BTC 0.0042-0.0048。平均日汇率为 {} 美元。

## 相关外部信息

A [study](https://medium.com/@MoneroCrusher/analysis-more-than-85-of-the-current-monero-hashrate-is-asics-and-each-machine-is-doing-128-kh-s-f39e3dca7d78) of Monero nonces documented differing patterns in the nonce distribution when ASICs were mining on the network, it considers the methods ASIC miners may take to disguise their presence and how they can be detected. The study speculates that 85% of the Monero hashrate comes from ASICs at time of writing.

A counterfeiting vulnerability was [discovered](https://z.cash/blog/zcash-counterfeiting-vulnerability-successfully-remediated/) in Zcash in early 2018. "This vulnerability is so subtle that it evaded years of analysis by expert cryptographers focused on zero-knowledge proving systems and zk-SNARKs.". It was silently patched with the Sapling network upgrade that occurred on Oct 28, 2018, and this [post](https://z.cash/blog/zcash-counterfeiting-vulnerability-successfully-remediated/) on Feb 5 explained how the vulnerability had been dealt with within Zcash and how other affected coins (like Horizen and Komodo) were notified. The nature of Zcash cryptography is such that it is difficult to determine if any ZEC was counterfeited while the vulnerability was present. The Zcash team reporting on the bug believes it had not been exploited because "discovery of the vulnerability would have required a high level of technical and cryptographic sophistication that very few people possess."

一个 Grin 开发员在论坛上[发帖](https://www.grin-forum.org/t/solved-early-disappointments/3682) 表示对于一项上线两周要求捐款资助其中一名开发人员而未达成目标表示失望 - 并威胁要取区块奖励的 20% 以支持开发。
消息传出后，该[活动](https://grin-tech.org/yeastplume)在短时间内筹得 EUR 67,580，超出原本 EUR 55,000 的目标。如 Breaker Mag [表示](https://breakermag.com/as-decred-turns-three-its-still-set-on-real-decentralization/)， Grin “吸引[上千万美金](https://www.coindesk.com/grin-launch-crypto-interest-from-deep-pocketed-investors)的挖矿投资，却在筹集 62,000 美元支付主开发人员 6 个月工资上面临难题。

Ethereum holders are holding another [signaling carbonvote](http://www.progpowcarbonvote.com/) about whether they want to change mining algorithm to ProgPoW. The vote started with strong [opposition](https://www.trustnodes.com/2019/02/14/98-of-ethereum-vote-against-progpow) to the change (98% No), but later flipped to strong support (94% Yes) as of 4 March (with 3% of circulating ETH having voted). While carbonvote has no official place in Ethereum's governance, the method is being used because:

> We have noticed a lot of trolling and shills on both sides of the debates from anonymous accounts on forums, youtube, telegram, glitter, reddit and twitter. There is no way to know if these accounts are real people who actually have economic stakes in ethereum, or are simply fake troll or shill accounts funded by one side of the debate.

Tezos started [voting](https://blog.nomadic-labs.com/athens-proposals-injected.html) for the first [amendment](https://blog.nomadic-labs.com/athens-our-proposals-for-the-first-voted-amendment.html) to its protocol on February 25 ([simple guide](https://medium.com/tezos-spotlight/tezos-the-first-amendment-a-laymans-guide-7424ef1d3e13), [detailed guide](https://medium.com/tezos/amending-tezos-b77949d97e1e) to amendment process). The amendment process has 4 phases, each lasting 8 "cycles" (a cycle lasts around 3 days, so each phase lasts for around 24 days). In the first phase bakers submit and upvote proposals. There are 2 proposals being evaluated now in the first phase, they both increase the gas limit but one also decreases the minimum "roll size" (amount of XTZ required to be a baker). It is interesting to note that Kialo is being [used](https://www.kialo.com/tezos-protocol-amendment-1-25295) by some Tezos community members to discuss these proposals. When the first phase ends, the most upvoted proposal will progress to phase 2, where it must be approved by at least 80% of bakers. If the criteria are met, this is followed by a testing phase in which a testnet fork with the changes applied is created and runs for 48 hours (a further testnet matching the proposal may be run for the rest of this phase to allow further testing). After the testing phase, bakers vote on whether the changes should be activated, with an 80% supermajority required. After this 4th phase the changes are activated (or not) and the cycle begins again with new proposals.

Dash v0.13.1 在2月8日发布以“加速 Dash Core v0.13的采用”。Dash Core [v0.13](https://blog.dash.org/dash-core-v0-13-on-mainnet-dc9609b0f6f9) 本打算激活 [DIP3](https://github.com/dashpay/dips/blob/master/dip-0003.md) 但激活门槛为 PoW 矿工及主节点(masternodes)在激活开始前 7 天内达到 80% 的区块支持率。在 24 天左右仍未达成门槛后，门槛要求被视为太严格，并决定可以降低主节点(masternodes)的支持率要求。当足够的 PoW 矿工升级 v0.13.1 后，该变更将于一周后激活。(该[激活](https://blog.dash.org/product-update-february-21-2019-5f067b62df00)已在2月26日左右完成)

0x protocol (ZRX) 在2月18日-2月25日进行了[第一次](https://blog.0xproject.com/how-to-participate-in-the-zeip-23-vote-eaa861298033)持代币者投票。该投票是为了通过 [ZEIP-23](https://blog.0xproject.com/zeip-23-trade-bundles-of-assets-fe69eb3ed960)并启动“交易数个资产“。该提案以 5,061,033 ZRX (流通量的 0.86%)参与率和 99% 同意票通过。

The NEM Foundation's funding proposal [started](https://forum.nem.io/t/nem-foundation-update-vote-for-funding-proposal-2019/22007) voting on Feb 15 and voting was open for 5 days. The funding proposal [passed](https://forum.nem.io/t/vote-for-nem-foundation-funding-proposal-2019-approved-by-the-community/22060) with 90% Yes votes and 10% No votes - with votes from 4.56% of the "Proof of Importance" (NEM's way of weighting holders' influence). The vote was conducted on the basis that a 65% supermajority of Yes votes was required, and at least 3% of the network's POI must vote Yes as a quorum requirement. Voting was conducted from within the NEM wallet by sending 0 XEM transactions to a Yes or No address. Another concurrent proposal to fund "NEM Labs" was also successful, with a similar level of participation and 98.8% approval. The NEM Foundation proposal asked for $8 million in XEM (figure is surprisingly hard to find, could only be found in a [google doc presentation](https://docs.google.com/presentation/d/1nMR_1ajVcpdGW7g8I0p7ZGh88tZ1SL5RzG5TsLW6Qnk/edit#slide=id.p2)), while the NEM Labs proposal asked for $3.27 million.

The Aragon Transparency Report for Q4 2018 was [released](https://blog.aragon.org/aragon-q4-2018-transparency-report/). This report presents a detailed breakdown of spending related to the project. The total spent in Q4 2018 was ~€1,055,484.43 or equivalent in cryptocurrency, with €268k on salaries, €330k on payments to service providers, €45k on sponsoring/tickets for events, €63k on hosting the AraCon conference and €260k on [Nest](https://github.com/aragon/nest) teams (a grants program). This report also describes financial [hedging](https://twitter.com/AragonProject/status/1067349802365739008) steps which have been taken by Aragon Association - exchanging some of the ETH raised during the ICO to buy other assets.

The blacklist issued by the EOS Core Arbitration Forum (ECAF) in Jun 2018 was allowed to [lapse](https://medium.com/@eos42/proposed-solution-for-a-broken-blacklist-ce1c18bdf81c) when a new Block Producer was rotated in which had not configured the blacklist. This allowed one of the blacklisted addresses to move over 2 million EOS. The lapse occurred because the blacklist has been implemented as a list of addresses from which block producers will not process transactions, with each block producer being responsible for maintaining the blacklist manually. If only one top 21 BP does not have an updated blacklist, blacklisted accounts are vulnerable to being emptied. One solution that has been suggested is to "null the keys" until a decision has been made about what to do with the frozen funds. What to do with the blacklisted funds is already an issue for EOS, and the ECAF itself may be disbanded if an open referendum to "Delete the ECAF" passes (currently on 99% Yes with 2.4% of EOS having voted).

Binance is [launching](https://www.theblockcrypto.com/2019/02/07/binance-moves-away-from-ethereum-as-it-prepares-to-launch-dex/) its DEX based on Cosmos' Tendermint protocol and DPoS. The listing fee will "probably be close to $100,000" to "reduce the number of spam or scam projects". In contrast, Decred's DEX design has no listing fees and doesn't require an extra blockchain for its operation.

Canadian exchange QuadrigaCX [owes](https://www.coindesk.com/quadriga-creditor-protection-filing) its customers $190 million. The funds reportedly [cannot be accessed](https://www.coindesk.com/quadrigacx-crypto-exchange-users-say-they-still-cant-get-their-money-out) after its founder died, who had sole control or knowledge of exchange's cold storage solution. Another $500K in BTC were locked "by mistake" per [this story](https://www.coindesk.com/quadriga-inadvertently-sent-btc-to-dead-ceos-cold-wallet-ey-report). The never ending trail of failures by centralized exchanges shows just how challenging the custody of cryptocurrencies is.

Medium showed its power again by [suspending](https://archive.today/iKQlv) the account that [posted](https://medium.com/@zeroresearchproof/quadrigacx-chain-analysis-report-pt-1-bitcoin-wallets-19d3a375d389) chain analysis of QuadrigaCX wallets. Luckily, someone made a [snapshot](https://archive.today/xsztt). The suspension hides all account's content and is implemented as a redirect to a same-for-all page that says "This page is unavailable" and does not state the reason. Medium is a powerful platform, but at its core is a centralized service that can lock in data of those who don't make backups. Earlier behavior like this triggered a [discussion](https://github.com/xaur/decred-issues/issues/70) about migrating from Medium or treating it as just a mirror.

Android malware was [discovered](https://www.welivesecurity.com/2019/02/08/first-clipper-malware-google-play/) on Google Play Store that changes cryptocurrency address in the clipboard. Always double check the address before sending.




## 关于月报
二月为英文第11期 [GitHub](https://xaur.github.io/decred-news/journal/201902) 月报。 点击[这里](https://xaur.github.io/decred-news/)浏览所有往期月报，翻译等。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues) 和 [Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

感谢 (按字母排序): bee, davecgh, degeri, Dustorf, emiliomann, guang, jholdstock, liz_bagot, matheusd, raedah, sambiohazard。特别感谢 richardred 给予加密货币治理课题的深入分析，和 saender 提供的美术图。

## 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

感谢 (按字母排序): 
