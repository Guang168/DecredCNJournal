# Decred月报 - 2月 

![abstract art](img/FEB19_journal-201902-384.png "Objective Constructs by @saender")

祝 Decred 生日快乐！自 2016年2月8日 的[第一个区块](https://explorer.dcrdata.org/block/1)已经渡过3年了。

二月份里我们在 Politeia 上很活跃，有 7 个新提案提交，5 个提案开始投票及在 3 月份的前几天里通过了 4 个提案。总额 490,000 美元的 2019 年宣传及活动预算已正式投票通过。

网络升级也已经[达到](https://voting.decred.org/)需要支持闪电网络的共识更改投票门槛，共识更改投票预计将在 3月14日 开始。

如果你还没升级，[v1.4.0 发布版本](https://github.com/decred/decred-binaries/releases/tag/v1.4.0)包含了很多改进。如果投票通过了，节点需要这个最新版本继续运行升级后的区块链。同时请务必[验证下载软件](https://docs.decred.org/advanced/verifying-binaries/)并呼吁其他朋友们升级哦。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd):通过最[大限制](https://github.com/decred/dcrd/pull/1596)一票双投和[拒绝](https://github.com/decred/dcrd/pull/1597)同区块双投来完善内存池制度。从dcrd[删除](https://github.com/decred/dcrd/pull/1607)钱包的类型并[迁移](https://github.com/decred/dcrwallet/pull/1394)到dcrwallet，这简化了对dcrwallet的更改，并在dcrd中触发[重构](https://github.com/decred/dcrd/pull/1613)，以提供更强大的模块边界并简化依赖图。[删除](https://github.com/decred/dcrd/pull/1599)非root 的Go模块替换 - 这有助于确保测试中的所有模块为最新代码，并帮用户保持它们独立准确。

[dcrwallet](https://github.com/decred/dcrwallet): v1 自动购票经过数个更新版本后已[被移除](https://github.com/decred/dcrwallet/pull/1396)。

[Decrediton](https://github.com/decred/decrediton): [升级](https://github.com/decred/decrediton/pull/2009)到 Electron 4，让 Windows 启动时[更稳定](https://github.com/decred/decrediton/pull/2017)。在自动购票运行时增加[退出提醒](https://github.com/decred/decrediton/pull/1989)。多个[响应视图](https://github.com/decred/decrediton/issues?q=is%3Aissue+author%3AMariaPleshkova+created%3A2019-02-01..2019-02-28)已完成设计阶段并准备实施。

[Politeia](https://github.com/decred/politeia): 增加了突出显示自上次登陆后的新评论以及邮件[通知](https://github.com/decred/politeia/pull/680)密码更改的功能。(通过 Bug Bounty 漏洞报告奖励计划[提议](https://github.com/decred/politeia/issues/673))。

一项大的缓存层工作已被[合并](https://github.com/decred/politeia/pull/660)! 感谢 @lukebp 和所有参与评论/测试的人员。这为许多网页性能改进铺了路。其他已完成的工作包括 CLI 工具[改进](https://github.com/decred/politeia/pull/707) 及 dcrtime 的[文件系统验证工具](https://github.com/decred/dcrtime/pull/46) fsck (file system verification tool)。

进行中:

* 使用 CockroachDB 扩展 www 数据库的工作已经[开始](https://github.com/decred/politeia/pull/689)。 
* 开发员[决定](https://matrix.to/#/!VFRvyndKpzcLrVslQD:decred.org/$15507680085008gMbtf:decred.org)将承包商管理系统的代码移去 politeia 及 politeiagui 代码库以避免维护两个分叉代码并保持两份代码同步的工作。
* 更改默认评论排序算法的[讨论](https://github.com/decred/politeiagui/issues/1022).

[dcrandroid](https://github.com/decred/dcrandroid): 多个漏洞修复及小改进等待整合中，详情请参照[项目告示板](https://github.com/decred/dcrandroid/projects/1)。

[中文](https://github.com/decred/dcrandroid/issues/336)及[越南语](https://github.com/decred/dcrandroid/pull/333)翻译进行中。

[dcrios](https://github.com/raedahgroup/dcrios): 已更新 TestFlight [beta测试版](https://testflight.apple.com/join/dvq51tCh)及正在更新以达到dcrandroid版本水平。在[这里](https://github.com/raedahgroup/dcrios/projects/1)查看进度。

第一测试版预计一个月后发布，同时预计应该也有一个 dcrandroid 更新发布。

[dcrdata](https://github.com/decred/dcrdata): 增加显示 [Politeia proposals](https://github.com/decred/dcrdata/pull/1016) 数据功能，增加[法币换算](https://github.com/decred/dcrdata/pull/1049) (供应, 基金会, 选票价格),[重组](https://github.com/decred/dcrdata/pull/982)内存池页面，终端获取[原区块](https://github.com/decred/dcrdata/pull/1032)及[原区块头](https://github.com/decred/dcrdata/pull/1035)，增加[缓存](https://github.com/decred/dcrdata/pull/1051) 包.

[关于](https://github.com/decred/dcrdata/issues/1022)如何计算 51% 攻击成本加入到dcrdata的讨论。

[Ticket splitting](https://github.com/matheusd/dcr-split-ticket-matcher): @matheusd [分享](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$1549497567273IPjZq:decred.org)他关于分票的想法，背景及接下来的计划。@david 录制了设置分票的教程[影片](https://www.youtube.com/watch?v=9L8P7hL5v6w)。

[docs](https://github.com/decred/dcrdocs): 解释 [Politeia 审查](https://docs.decred.org/governance/politeia/politeia-censorship/)及如何证明内容被屏蔽的新页面, 新[升级 Decrediton](https://docs.decred.org/wallets/decrediton/upgrading-decrediton/) 页面, 测试网选票矿池列表已列入到[使用测试网 Using Testnet](https://docs.decred.org/advanced/using-testnet/) 页面, P2PKH 地址生成流程图列入[地址细节 Address Details](https://docs.decred.org/advanced/address-details/) 页面。 [恢复](https://github.com/decred/dcrdocs/pull/846)搜索功能。

[decred.org](https://github.com/decred/dcrweb): 内容及翻译更新。[开始](https://github.com/decred/dcrweb/issues/561)筹划实施新闻及文章的页面.

其他:

* @matheusd 的[博客](https://matheusd.com/post/dcp0004-and-hardforks/)写了关于 DCP0004 一些有趣的细节： Decred 的 PoS 部分可以充当意外共识漏洞的多一层保护
* [voting.decred.org](https://voting.decred.org/) 仪表板也显示过去的议案。jQuery 已被[移除](https://github.com/decred/hardforkdemo/pull/213)。
* Google reCAPTCHA 替代自托管方案已 [merged](https://github.com/decred/dcrstakepool/pull/281) - 这是增加[用户](https://github.com/xaur/decred-issues/issues/25)的一大步。感谢为这个补丁努力的开发员和测试员。
* 有趣答题: 你是否知道 Decred 非常[不鼓励](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15497657664963CvzUr:decred.org) 微额输出?
* 原子交换的[概念证明 PoC UI](https://github.com/xaur/decred-issues/issues/8) 开始有点进展。
* 支持QTUM的代码在原子交换[被合并](https://github.com/decred/atomicswap/pull/93), 支持POLIS的代码已被[移除](https://github.com/decred/atomicswap/pull/99).
* 为 dcrseeder 增加 DNSSEC 的工作已经[开始](https://github.com/decred/dcrseeder/pull/19)
* [authit](https://github.com/decred/authit), 即 dcrtime 的 UI 已经在[timestamp.decred.org](https://timestamp.decred.org/)托管。欢迎到[GitHub issues](https://github.com/decred/authit/issues)或新的 [#timestamp](https://matrix.to/#/!gltiHJRZiSJTzvjOEu:decred.org) 聊天室提出反馈。

> 我必须说, Go 真的是一个神奇的编程语言。我想我未试过在一个新的编程语言里感到这么舒服。(@jholdstock 在 [聊天室](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15497080644503VtguR:decred.org))

---

## 人员

欢迎新到来的首次贡献者，代码在 GitHub 上合并：@jozn ([dcrd](https://github.com/decred/dcrd/commits?author=jozn)), JoeGruffins ([dcrwallet](https://github.com/decred/dcrwallet/commits?author=JoeGruffins)), luoshang722 ([atomicswap](https://github.com/decred/atomicswap/commits?author=luoshang722)), rex4539 ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=rex4539)).

恭喜在 decred.org 上[列出的](https://github.com/decred/dcrweb/issues/562)三位 Ditto 承包商

* Elizabeth Bagot (@liz_bagot)
* Margaret Huang (@margaret_mei)
* Milvian Prieto (@milvian)

1名贡献者从 decred.org 中[移除](https://github.com/decred/dcrweb/pull/541)：Jure Kralj (@praxis, Reddit 管理员).

## 治理

在 2月里，[DCR 基金会](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了 14,878 DCR，并花了 17,311 DCR，二月份是项目这么久以来第一个月开销多于收入。使用 DCR 在 2 月份的每日平均美元价格 16.51 美元计算，本月收到 24.6 万 美元以及支出 28.6 万 美元。由于这些付款用于支付 1 月份完成的工作，因此可以用 1月份的平均价格 17.06 美元计算 - 在这种情况下，美元收到的数字是 25.4 万美元以及支出 29.5 万美元。3月9日 为止，基金会余额为 605,828 DCR (按 16.6 美元计算相当于 1005万 美金)。

于 3月9日 的提案状态:

* [Baeond 卡牌游戏](https://proposals.decred.org/proposals/f545b359fcf1b40b356e9cb556cb422cc7ff01b628b577f804cdc45ce414f5dd) 由 burst 提出，由 29% 的参与率和 97% 反对票不通过 _(1月份月报遗漏)_.
* [去中心化交易所的请求提案 Decentralized exchange RFP](https://proposals.decred.org/proposals/5431da8ff4eda8cdbf8f4f2e08566ffa573464b97ef6d6bae78e749f27800d3a) 由 @jy-p 提出，收到 70 评论。第二版本降低了 MVP 的范围并将成本上限设为 25万美元(之前为 100 万)。@bee 发布了一份个人的赞成和反对[分析](https://github.com/xaur/decred-proposals/blob/master/decred-dex-rfp-analysis.md)。改提案也引起了基金会是否资助推广这类提案的[讨论](https://www.reddit.com/r/DCR/comments/awbtbr/should_treasury_funded_marketing_resources_be/)。本提案已于 3月9日 开启投票，8000 票中有 91.4% 的人投了赞成票。
* [钱包教程提案 Wallet tutorials](https://proposals.decred.org/proposals/a3def199af812b796887f4eae22e11e45f112b50c2e17252c60ed190933ec14f) 由 Cryptocurrency.Market 的 Denni Lovejoy 提出。该提案经历了多个在[聊天室](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154941035930084kFSjY:decred.org)和 [Reddit](https://www.reddit.com/r/decred/comments/anksg2/proposed_statement_of_work_sow_for_decred/) 的反馈及更改。750 美元的预算以 24% 参与率和 80% 同意票通过。
* [2019活动资金预算 Events funding for 2019](https://proposals.decred.org/proposals/d3e7f159b9680c059a3d4b398de2c8f6627108f28b7d61a3f10397acb4b5e509) 由 @Dustorf 提出。该提案在[聊天室](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154896889724431Mxlvj:decred.org)和 [Reddit](https://www.reddit.com/r/decred/comments/anhh8n/proposal_to_get_events_spending_approved_via/) 预览后提出。20万 美元的预算投票以 34% 参与率和 89% 同意票通过。
* [2019宣传预算 Marketing funding for 2019](https://proposals.decred.org/proposals/c84a76685e4437a15760033725044a15ad832f68f9d123eb837337060a09f86e) 由 @Dustorf 提出。收到 68 评论，以及在[聊天室](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154897255124536mFHoo:decred.org)和 [Reddit](https://www.reddit.com/r/decred/comments/aolr79/politeia_proposal_to_fund_marketing_ops_for_2019/) 中讨论。29万 美元的预算投票以 36% 参与率和 83% 同意票通过。
* [Decred ATM 集成提案 Decred ATM integration](https://proposals.decred.org/proposals/aea224a561cfed183f514a9ac700d68ba8a6c71dfbee71208fb9bff5fffab51d) 由 @oregonisaac 提交。改提案是从 2018年11月 份 Bcash ATM [提案](https://proposals.decred.org/proposals/bb7e19283d5c65fed598d5a2f4afcc2b5d2eab187b9cb84fc4304430f80b5ad1)及多个星期的研究，草案，反馈的结果。目前提案要求获取利益相关者意见是否继续筹划 ATM 集成。通过后，另一份提案将提供实施细节投票决定。
* [Decred社区网站 Decred community website](https://proposals.decred.org/proposals/fb8e6ca361c807168ea0bd6ddbfb7e05896b78f2576daf92f07315e6f8b5cd83) 由 @karamble 提出。该提案提出整合各资源Decred 相关内容的网站。内容包括文章，视频，播客，活动报告及商家。该原型已由 @karamble 建造，该提案要求 6,000 美元资助该网站6个月。投票以 33% 参与率和 72.5% 同意票通过。
* [Decred IDAX 交易所整合 Decred integration for IDAX exchange](https://proposals.decred.org/proposals/60adb9c0946482492889e85e9bce05c309665b3438dd85cb1a837df31fbf57fb) 由 acean 提出。该提案要求 1,000 DCR 以上线在蒙古的IDAX交易所 DCR/BTC 交易对。投票以 23.5% 参与率和 25% 同意票不被通过。
* [Trust Wallet 钱包整合提案 Decred integration in Trust Wallet](https://proposals.decred.org/proposals/2ababdea7da2b3d8312a773d477272135a883ed772ba99cdf31eddb5f261d571) 由 @oregonisaac 提出。提案预算 3,300 美元整合 “完全去中心化” 钱包 Trust Wallet 并提供大概每月 100 美元的维护支出。投票尚未开始。

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

一个新的推特账户 [@pi_crumbs](https://twitter.com/pi_crumbs) 将推送提案创建或修改，投票开始及结束消息。目前由 @richardred 手动操作，但讨论将其自动化也在进行中。

另一个推特账户 [@slices_of\_pi](https://twitter.com/slices_of_pi) 将推送手动编写有关 Politeia 活动的评论。

更多细节，分析与评论请参考 @richardred 的 Politeia 简报 [第10期](https://medium.com/politeia-digest/issue-10-jan-1-feb-18-2018-202cde71a19d) 及 [第11期](https://medium.com/politeia-digest/issue-11-feb-19-feb-28-2019-46befddb09fe)。以上重点总结于 Politeia 简报。

## 网络

算力: 2 月算力以 ～230 Ph/s 开始，以 ～300 Ph/s 结束，本月中最高 420 Ph/s 及最低 210 Ph/s。在 3月5日 根据 [dcrstats.com](https://dcrstats.com/pow) 数据显示，矿池算力分布为：BTC.com 31%, Poolin 27%, F2Pool 18%, UUPool 15%, Luxor 4%, CoinMine 1% 及其他 5%。矿池分布数据为大约值无法精确计算。 

投票: 按 3月1日 dcrstats.com（数据显示）, 30日 平均票价为 111.6 DCR (+2.2)。价格在 98.4 DCR 至 124.1 DCR之间浮动。锁仓数额为 4.36-4.56 百万 DCR, 大约为总流通量的 46.4-48.7%。


选票价格及选票池大小在二月份中经历了不寻常的波动。在 2月11日 同一个区间内购买的 1,265 张选票把选票池的选票拉到 ～41，670 张选票及后面 7 次票价调整中涨至 119.4。随后选票池票数下跌至低于 4 万张选票 （上次发生于 2017年11月 ），导致连续 10 次调整降至 98.4 DCR。在票价到底时，在同一区间内又卖出最高 2，880 张中的 2，797 张选票。@ImacallyouJawdy 提出在单单这一区间选票就锁定了 282k DCR 或 DCR 流通量的 3%。因此选票价格跳跃至 124.1 DCR，这是自 2017年7月 选票价格算法调整后的新高。选票池最高峰是锁定了 42，174 选票，等同于 DCR 供应的 48.7% - 创新高并且比前一个在2018年6月7日的高峰高出 +0.7%。感谢 charts.dcr.farm 里准确的图表。

节点: 截止于 3月1日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 205 public listening Node 及 297 Normal Node。版本分布: v1.5.0 dev builds: 8.6% (+4.3%), v1.4.0 final: 43% (+43%), v1.4.0 dev and rc builds: 7% (-6%), v1.3.0: 23% (-32%), v1.2.0: 10% (-4%), v1.1.2: 4% (-4%), v1.1.0: 2% (-1%)。

PoW 和 PoS 的[升级门槛](https://voting.decred.org/)已经完成，共识投票已经锁定并在大约  3月14日 开始。感谢所有通过各种渠道帮忙联系 PoW 矿池及 VSP 运营商（选票矿池）并呼吁他们升级的人员。

投票还未开始但是区块投票已经开始发出对于 `fixlnseqlocks` 议程的选择信号。截止于 3月4日 [共有](https://matrix.to/#/!wSdymYrEpBhsWlDJuk:decred.org/$155168912215429iStcp:decred.org) 8,503 票赞成和 1 票不赞成。“这逆向投票。。。至少证明反对票是有效的吧。” @jz

## 整合

选票矿池 VSP 代号 "Bravo" 已从 dcr.stakepool.net [重命名](https://github.com/decred/dcrwebapi/pull/59)为 [dcr.blue](https://dcr.blue/)。

交易所整合:

* [Vertbase](https://www.vertbase.com/) 已增加 DCR/USD 交易对。Vertbase CEO 兼 联合创始人 Justin 加入 #general 并[回答 Vertbase 相关问题](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155015221011045eRXdT:decred.org)。答案中总结：Vertbase 目前支持 50 个美国州中的 39 个，正积极增加 GBP/EUR/AUD 交易，并使用第三方处理身份认证。其中一个 Vertbase 特色为短时间的托管：他们在银行转账过账后将代币直接转入用户钱包。

> 我们也需要您提供钱包地址，因为我们不想托管，也不想你使用我们的平台托管您的加密货币。成为您自己的银行！(@Justin 在 [#general](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$155017217111507BsAmt:decred.org) 说道)

截止到 3月8日，Vertbase 卖单路径仍不可用，请参考这个 [Reddit 帖](https://www.reddit.com/r/decred/comments/aqkl1p/vertbase_lists_decred_dcr_with_us_dollar_usd/).

* [Lykke](https://www.lykke.com/) [已加入](https://twitter.com/lykke/status/1095352586545319937) DCR 与 BTC 和 USD 交易对。
* [ChainRift](https://www.chainrift.com/) 已整合 DCR。
* [Livecoin](https://www.livecoin.net/) [已加入](https://twitter.com/livecoin_net/status/1098151449786118144) DCR 与 BTC, ETH 和 USD 交易对。
* [BitMesh](https://bitmesh.com/) [推出](https://www.reddit.com/r/decred/comments/av8a69/bitmesh_has_launched_dcr_and_opened_dcrbtc/) DCR 与 BTC 和 USDT 交易对。

警告: Decred 月报作者无法确认以上交易所可靠性。请自行进行审核[才](https://twitter.com/yeppoon/status/1095857386709893120)将您的个人信息或财产信托于任何实体。

## 落地应用

CoinFund [已宣布](https://blog.coinfund.io/announcing-grassfed-network-and-decred-staking-pool-with-placeholder-55a32a312710)Grassfed Network，一项使用“通用采矿”参与去中心化网络的计划。相关文章发表在[CoinDesk](https://www.coindesk.com/these-cryptofunds-say-generalized-mining-is-the-new-way-to-invest)。

任何以网络资产计价的协议奖励都可以被视为[通用采矿](https://grassfed.network/mining/)。采用这种方法，在资产增值外，投资者可以直接参与网络并产生额外的回报。

根据公告，CoinFund与创投[Placeholder](https://www.placeholder.vc/)合作，他们计划将拥有的票委托给1月份推出的[Decred VSP](https://dcr.grassfed.network) 。 Joel Monegro和Chris Burniski在德克萨斯比特币会议2018年的[小组讨论](https://www.youtube.com/watch?v=tkllaH0Y0ng)期间提出了这个计划。[CoinFund](https://coinfund.io/)是一家专注于加密货币投资和研究的公司，成立于2015年，总部位于美国纽约。

## 外联活动

在 2 月，@Dustorf 提出了在 2019 年剩余日子里[营销](https://proposals.decred.org/proposals/c84a76685e4437a15760033725044a15ad832f68f9d123eb837337060a09f86e)和[活动](https://proposals.decred.org/proposals/d3e7f159b9680c059a3d4b398de2c8f6627108f28b7d61a3f10397acb4b5e509)的计划 。利益相关者投票通过了这两个提案。这是一个令人兴奋的发展，通过将支出的直接控制权转移给利益相关者，使 Decred 更加去中心化。经过激烈的讨论，提案分别得到了83％和89％的票批准。

在批准预算后，工作在提案的范围下已经开始。正在规划纽约市区块链周，时间与 2019 共识大会相吻合。预计在两周内公布更多计划信息。

第一个 Decred 播客正在录制并计划在 3月份 发布。采访目标为 Decred Jesus。作为项目贡献者，他将会真实并丰富多彩地概述 Decred 。网站相关工作，架构，文案和视频脚本已经开始。

我们希望在本月底之前发布 Decred Assembly 和定期通报。

Ditto 2月 工作总结:

* 媒体培训了 5 名 Decred 社区成员。
* 获得媒体报道：@ jy-p 和 BlockTV 的 15 分钟[访谈](https://blocktv.com/watch/2019-02-20/5c6d6a2be03e3-chain-breakers-promoting-constant-disruption-); 在福布斯发布去中心化交易所 DEX 的焦点[文章](https://www.forbes.com/sites/leslieankney/2019/02/04/no-more-trading-or-listing-fees-decred-releases-new-dex-proposal/)。 在 Breaker Mag 发布的焦点[文章](https://breakermag.com/as-decred-turns-three-its-still-set-on-real-decentralization/)，以纪念 Decred 的三周年庆典。在 Block Crypto 发布 Vertbase 交易所提供法币 DCR 交易对的[文章](https://www.theblockcrypto.com/2019/02/13/they-asked-us-for-3-million-an-inside-look-into-getting-listed-on-a-crypto-exchange/)其中包含 @jz 的访问。记者弗兰克查帕罗说，这个故事在 Twitter 上很受欢迎，而且在 The Block 内部也很受欢迎。
* 促进了 2 次媒体采访。 
* 与社区合作创建了一个对媒体友好的图像存储库，我们可以与记者分享，为 Decred 的故事添加视觉色彩。
* 帮助计划旧金山 Decred 和 OKCoin 主办活动的后勤和内容。与 Dustin 和 OKCoin 合作起草 Eventbrite 副本，与 OKCoin 协调，制定活动议程，并起草新闻稿。
* 制定一项计划，在不同渠道中，将 Decred 定位为优质储值货币 SoV ，包括与顶级主流记者展开长期对话。
* 与 Dustin 合作，制定了为期 六个月 的营销和传播计划，涵盖公关，活动，内容等。作为战略的一部分，我们的目标是令机构投资者认可 Decred 的合法性和可信度。需要超越媒体关系，并配合其他营销媒体，包括项目研究内容，推特，影响者，活动等。

如需了解详细信息，请参阅 [2月4日](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154930816328395IaXDr:decred.org)和[2月15日](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$155026927613161McEtC:decred.org) 的 Ditto 双周更新。

讨论：

* [关于](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$15498862365982zjzwP:decred.org)是否在 1.4 的公共消息中使用词语 “bug”。
* 对于将 Decred 的市场代码从 DCR 更改为 CRED 的[意见](https://www.reddit.com/r/decred/comments/ans7lg/what_do_we_think_of_converting_decreds_ticker/)。
* [批评](https://www.reddit.com/r/decred/comments/asg6kf/update_on_the_decred_14_release/)在公告中使用 “毫无生气的公司” 模式。

## 社区活动

出席：

* 在中国的青岛大学，谈到了 Decred 的社区治理模型和即将进行的链上共识投票。 [@wanbihou](https://twitter.com/wanbihou) “学生们非常热情！” （[照片](https://twitter.com/wanbihou/status/1101131545010556928)）
* 美国亚特兰大的 [TabConf](https://tabconf.com/)。 @joshuam [提到](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15497319564677Cmutw:decred.org)）：“Tabconf非常棒。会议者参与度非常高 - 我在迄今为止的会议中被问到了最有深度的问题”。
* [校园派对](http://brasil.campus-party.org/cpbr12/patrocinadores/) 在巴西圣保罗。大约有 6 万人参与了这项 24 小时，为期 6 天的活动。Decred 是唯一正式参与的加密货币，并有专门的空间来展示讲座和课程。所有巴西开发承包商参于并举办了 6 次讲座和 3 次研讨会。 @jy-p 介绍了[加密货币安全性和适应性](https://www.youtube.com/watch?v=SMiHku6GGmI)）。当中遇到一些问题，如 Decred 的区域移动和减少（几乎所有会议参与者都遇到了）和翻译不良 - 所有这些都考虑到未来的计划中。请参阅 @emiliomann 的[完整报告](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155200602520229ditLj:decred.org)和 @matheusd 的[笔记](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155197226472913itWWu:matrix.org)。
* 加纳爱之夜。由 @George Pro 组织。由于约 90％ 的参与者已经了解比特币，演示者可以跳过基础知识并突出显示 Decred 的独特功能。一个常见的问题是在哪里可以把 DCR 兑换成当地货币。（[照片](https://twitter.com/deCRED_Ghana/status/1096714039978266624)）
* [如何保护您的加密货币安全](https://www.meetup.com/Decred-Australia/events/258211699/) - 澳大利亚墨尔本。澳大利亚的加密货币爱好者讨论了最佳安全措施和 Decred 的安全标准。@Zohand [注释](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15504942691141LtOxa:decred.org)）：“反馈很棒，来自 coinstop 和 CTRL 的人想在几个月后再次参加活动。”。（[照片](https://twitter.com/DecredAustralia/status/1097478053763018752)）
* [Decred 30分钟](https://www.eventbrite.com/e/decred-en-30-minutos-tickets-55764142050)在墨西哥城举办。 @elian [报道](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15517155592047249xtYGy:matrix.org)：“这是第一次见面会内所有人（7 个人）都了解 Decred。因此我们可以讨论更复杂的问题，例如去中心化治理面临的挑战，最佳的投票方式以及项目中发生的未来发展，如 LN，支付，Politeia 的整合和最近的活动，营销和社区建议。很高兴在墨西哥遇到 DCR 爱好者。我认为在墨西哥，我们还没有到用加密货币作为货币的地步，但这一块正在快速发展。目前有更多的墨西哥人与加密货币接触，而不是与该国的股票市场接触，这是一个非常好的指标。“ （[照片](https://twitter.com/DecredESP/status/1102594478664232960)）
* 在墨西哥埃卡特佩克的UAEM大学讲话。 @elian [分享](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$1551994219193770GeoIk:matrix.org)：“我谈到了货币的历史，互联网，比特币区块链，Decred 的混合区块链和如何在加密货币和区块链行业工作。学生和教师对加密货币和区块链的创新着迷。观众主要由计算机科学学生组成。主要问题围绕什么是金钱，如何估值加密​​货币，和这个行业中大学毕业生的潜在工作机会。（...）在大学里进行谈判对我来说是一件大事，因为我知道下一代开发人员，律师，会计师等将会在不同行业里工作，他们渴望了解这个行业带来的机会。教师们非常高兴我们能够将这些知识传授给他们的学生，因为不容易在非市中心的大学进行这样的高科技讲座。“
* 加纳 Winneba 的 [Decred 聚会](https://www.eventbrite.com/e/decred-meet-up-tickets-57073786231)。由 @George Pro 组织，[提到](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155133397211500yxtpJ:decred.org)：“我们在加纳的第一次聚会是成功的。我们花时间去向参与者解释如何投资 DCR，如何获得 DCR（Coinomi流程），将其用作汇款，钱包设置，速度和隐私等。“（[照片](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$155133397211500yxtpJ:decred.org)）


即将到来的：

* [Decred & OKCoin Present "The Next 10 Years: Crypto Boom, Bust, or Buidl?"](https://www.eventbrite.com/e/decred-okcoin-present-the-next-10-years-crypto-boom-bust-or-buidl-tickets-57549671617) 美国三藩市，3月12日。OKCoin 的 CEO Tim Byun, Decred 的 Jake Yocom-Piatt, 代表 Placeholder 的 Chris Burniske 和 Alex Evans 将讨论 Decred 和加密货币的未来。
* [Restoring Trust through Blockchain Governance](https://www.meetup.com/DecredCanada/events/259126224/) 加拿大多伦多，3月16日
* [Berlin Blockchain Week](https://www.berlin-blockchain-week.com/) 德国柏林，3月27日 @karamble 将发表演说
* [Jalisco Talent Land](https://www.talent-land.mx/#entradas) 墨西哥瓜达拉哈拉，四月22-26日。细节可联系@elian
 
在治理部分提到，利益相关者通过了价值 200K 美元的 [2019 年的活动预算](https://proposals.decred.org/proposals/d3e7f159b9680c059a3d4b398de2c8f6627108f28b7d61a3f10397acb4b5e509), 当中包含了参与 3 个大型活动及出席多个小型活动。

## 媒体

部分文章:

* TokenGazer 评级 Decred (中文[qq.com](https://mp.weixin.qq.com/s/7rMaTYXIhIpO37qiIvJX_A)) - Decred 被评4.2/5
* 比特币之外最好的加密货币？Pavel Svitek在 ([quora.com](https://www.quora.com/Which-one-is-the-best-cryptocurrency-next-to-bitcoin/answer/Pavel-Svitek))上回答 - 感谢 Pavel 在 Quora 平台上以 Decred 回答了这个问题
* 没有交易或上币费用？ Decred 发布新的DEX提案 by Leslie Ankne ([福布斯](https://www.forbes.com/sites/leslieankney/2019/02/04/no-more-trading-or-listing-fees-decred-releases-new-dex-proposal/))
* Crypto 冬天会持续多久？Julia Herbst 问了三位专家 ([breakermag.com](https://breakermag.com/what-the-longest-ever-bear-market-means-for-crypto/))
* 随着 Decred 成立3周年，它在继续实现真正的去中心化 by David Z. Morris ([breakermag.com](https://breakermag.com/as-decred-turns-three-its-still-set-on-real-decentralization/)
* Decred 创始人提议建立 DEX 作为 Binance 的替代交易所（采访）by Liam Kelly ([cryptoslate.com](https://cryptoslate.com/decred-founder-proposes-dex-binance-interview/))
* “他们向我们要 300 万美元” 作为加密货币上交易所的费用 by Frank Chaparro ([theblockcrypto.com](https://www.theblockcrypto.com/2019/02/13/they-asked-us-for-3-million-an-inside-look-into-getting-listed-on-a-crypto-exchange/))
* 加密货币网络治理作为资本 by Joel Monegro ([placeholder.vc](https://www.placeholder.vc/blog/2019/2/19/cryptonetwork-governance-as-capital))
* 利用治理决定项目未来：Decred 会建造去中心化交易所吗？ by @richardred ([investinblockchain.com](https://www.investinblockchain.com/is-decred-dcr-building-decentralized-exchange/), [中文翻译](https://0xzx.com/2019022708166553.html))
* Decred 在 [福布斯](https://www.forbes.com/sites/samantharadocchia/2019/02/05/everything-about-the-digital-nomad-lifestyle-sounds-great-except-the-us-tax-system/) 和 [Breaker Mag](https://breakermag.com/bruce-schneier-is-right-about-blockchains-biggest-flaw-and-completely-wrong-about-its-longterm-significance/) 文章中被提到.

视频:

* Decred 问答环节 TruStory - Preethi Kasireddy 跟 Decred 社区成员 Isaac J 和 Matheus 了解了 PoS / PoW 共识运作和治理模型 ([youtube](https://www.youtube.com/watch?v=OKdaa630YDk))
* 加密货币的安全性与伸展性 -  @jy-p 在巴西校园派对的演讲 ([youtube](https://www.youtube.com/watch?v=SMiHku6GGmI))
* 去中心化的潜力 - BlockTV 和 @jy-p 的采访 ([blocktv.com](https://blocktv.com/watch/2019-02-20/5c6d6a2be03e3-chain-breakers-promoting-constant-disruption-))

音频:

* ITK Crypto #8 - Tom White 和 Crypto SI 对 @kozel 关于加密货币治理的访问 ([youtube](https://www.youtube.com/watch?v=H-qZBsQY5BM))

翻译:

* Decred 月报 - 2019年 1月 [中文](https://www.jianshu.com/p/097265621ef6) 来自 @guang (和 Dominic, Hugo 及 Jill), 来自 @elian 的[西班牙语](https://medium.com/@decred_es/revista-decred-enero-2019-549e2b051f5a)。感谢！


## 社区

截止于 Mar 1 的社区数据 :

* Twitter 关注量: 39,797 (+19)
* Reddit 关注用户: 9,365 (+35)
* Matrix 用户: 266 (+19)
* Slack 用户: 6,581 (+52)
* Discord 用户: 2,101, 发帖数: 131
* Telegram 用户: 4,272 (-231)
* YouTube 关注量: 3,746 (-6)
* Facebook 关注: 3,141 (+9), likes: 2,896 (+5)
* LinkedIn 关注: Decred page 483 (+17), Politeia page 29 (+2)
* GitHub dcrd : 474 (+6), fork人数: 1,237 (+16)

电报群社区: 中文 866 (+53), 意大利语 160 (+28), 葡萄牙语 642 (+100), 西班牙语 73 (+11).

中文社区在二月非常活跃 ：

* 开启了[#chinese](https://matrix.to/#/!nUWpVrwhlJFyLuMlGw:decred.org)中文聊天室
* 殷国超继续贡献 Decred 文章: 一篇关于 [dcrtime](https://mp.weixin.qq.com/s/ks48Piu3s2zy4btZW0kBDQ)和一篇关于[原子交换](https://mp.weixin.qq.com/s/Lgem_BqFBnLUsY7AzC5x_w)
* Dominic 在青岛大学给部分同学[介绍](https://twitter.com/wanbihou/status/1101122114118184961)区块链和 Decred 。
* 殷国超文章促使另一位社区成员[写更多](https://teakki.com/p/5c774a9ab1029f607605bc76)关于 dcrtime 并制作了将文件及文字时间戳的[网页 UI](http://www.ibitlin.com/dcrtool#/dcrtime) (dcrtime 的 UI在[这里](https://github.com/xaur/decred-issues/issues/9)记载)。

社交系统新闻：

* 非英语聊天室重新根据语言命名，并移除了不再使用的聊天室。目前 Matrix 上已有中文 [#chinese](https://matrix.to/#/!nUWpVrwhlJFyLuMlGw:decred.org), 葡萄牙语[#portuguese](https://matrix.to/#/!FBtUquQLhAvHeBIkac:decred.org), 俄语[#russian](https://matrix.to/#/!TQzfaYsKyxAqQDZQeX:decred.org)及西班牙语[#spanish](https://matrix.to/#/!pkeRzinGCRtjIIhAAK:decred.org)
* [Riot](https://riot.im/app/#/room/#general:decred.org) 客户端配合更新的 UI 已[升级](https://medium.com/@RiotChat/the-big-1-0-68fa7c6050be)至版本 1.0。

另一个 reddit 帖子在收到一些讨论后被[删除](https://www.reddit.com/r/decred/comments/an4b6z/forbes_no_more_trading_or_listing_fees_decred/)
。版主没有权力阻止删除社区信息的破坏性行为，只能[重新提交](https://www.reddit.com/r/decred/comments/ar29jd/forbes_no_more_trading_or_listing_fees_decred/)已删除帖。本 issue 收集了替代 Reddit 的[解决方案](https://github.com/xaur/decred-issues/issues/38)。


## 市场

在二月中 DCR 交易价格为 美金 14.97-18.28 / BTC 0.0042-0.0048。平均日汇率为 {} 美元。

## 相关外部信息

一项关于 Monero nonces 的[研究](https://medium.com/@MoneroCrusher/analysis-more-than-85-of-the-current-monero-hashrate-is-asics-and-each-machine-is-doing-128-kh-s-f39e3dca7d78)记录了 ASIC 矿机在网络上挖掘时的不同模式，其中记录了 ASIC 矿工怎样采取隐藏的方法以防止被检测。 在撰写本文时，该研究推测85％的 Monero 哈希值来自 ASIC 矿机。

2018年初，Zcash [发现了](https://z.cash/blog/zcash-counterfeiting-vulnerability-successfully-remediated/)一个漏洞。“这个漏洞非常的微妙，以至于它躲避了密码学专家多年对于零知识证明系统和 zk-SNARKs 的分析。”它在 2018年10月28日 Sapling 网络升级中默默被[修补](https://z.cash/blog/zcash-counterfeiting-vulnerability-successfully-remediated/)，2月5日 的这篇文章解释了 Zcash 如何处理漏洞以及通知其他受影响的加密货币（如Horizen和Komodo）。Zcash 加密算法的性质使得其存在漏洞时很难确认是否有其他伪造 ZEC。报告该漏洞的 Zcash 团队认为它没有被利用，因为 “发现漏洞需要高水平的计算机技术和加密技术，只有极少数的人才能符合这条件。”

一个 Grin 开发员在论坛上[发帖](https://www.grin-forum.org/t/solved-early-disappointments/3682) 表示对于一项上线两周要求捐款资助其中一名开发人员而未达成目标表示失望 - 并威胁要取区块奖励的 20% 以支持开发。消息传出后，该[活动](https://grin-tech.org/yeastplume)在短时间内筹得 EUR 67,580，超出原本 EUR 55,000 的目标。如 Breaker Mag [表示](https://breakermag.com/as-decred-turns-three-its-still-set-on-real-decentralization/)， Grin “吸引[上千万美金](https://www.coindesk.com/grin-launch-crypto-interest-from-deep-pocketed-investors)的挖矿投资，却在筹集 62,000 美元支付主开发人员 6 个月工资上面临难题。

以太坊持有者正在举行一个社区是否想要将挖矿算法改为 ProgPoW 的[投票活动](http://www.progpowcarbonvote.com/)。投票开始时社区强烈[反对](https://www.trustnodes.com/2019/02/14/98-of-ethereum-vote-against-progpow)这一变化（98％否定），但后来在 3月4日（有 3％ 的流通 ETH 投票）转向强力支持（94％赞成）。虽然持币人投票在以太坊的治理中没有官方地位，但还是需要使用该方法，因为：

> 我们已经注意到论坛，youtube，telegram，glitter，reddit 和 twitter 上匿名账户的争论双方都有很多拖沓和嘘声。没有办法知道这些账户是否是真实的人或他们实际上拥有以太坊的的权益者，或许他们只是由辩论的一方资助的虚假账号或杠精。

Tezos 于 2月25日 开始对其协议的第一次修订[投票](https://blog.nomadic-labs.com/athens-proposals-injected.html)（[简单指南](https://medium.com/tezos-spotlight/tezos-the-first-amendment-a-laymans-guide-7424ef1d3e13)，[修订过程的详细指南](https://medium.com/tezos/amending-tezos-b77949d97e1e)）。[修订](https://blog.nomadic-labs.com/athens-our-proposals-for-the-first-voted-amendment.html)过程分为 4 个阶段，每个阶段持续 8 个“周期”（一个周期持续约 3 天，因此每个阶段持续约 24 天）。在第一阶段，bakers 提交并提出建议。现在在第一阶段有 2 个建议被评估，它们都增加了气体限制但是也减少了最小“滚动尺寸”（需要作为 bakers 的 XTZ 的量）。值得注意的是，一些 Tezos 社区成员[正在使用](https://www.kialo.com/tezos-protocol-amendment-1-25295) Kialo 来讨论这些提议。当第一阶段结束时，最受欢迎的提案将进入第 2 阶段，必须得到至少 80％ 的 bakers 的批准。如果满足标准，则接下来是测试阶段，其中创建了应用了更改的测试网络分支并运行了 48 小时（可以在此阶段的其余部分运行与该提案匹配的另一个测试网以允许进一步测试） 。在测试阶段之后，bakers 投票决定是否激活更改，需要80％的参与者。在第4阶段之后，激活（或不激活）更改或再次以新提议开始。

Dash v0.13.1 在 2月8日 发布以“加速 Dash Core v0.13 的采用”。Dash Core [v0.13](https://blog.dash.org/dash-core-v0-13-on-mainnet-dc9609b0f6f9) 本打算激活 [DIP3](https://github.com/dashpay/dips/blob/master/dip-0003.md) 但激活门槛为 PoW 矿工及主节点 (masternodes) 在激活开始前 7 天内达到 80% 的区块支持率。在 24 天左右仍未达成门槛后，门槛要求被视为太严格，并决定可以降低主节点(masternodes)的支持率要求。当足够的 PoW 矿工升级 v0.13.1 后，该变更将于一周后激活。(该[激活](https://blog.dash.org/product-update-february-21-2019-5f067b62df00)已在 2月26日 左右完成)

0x protocol (ZRX) 在 2月18日-2月25日 进行了[第一次](https://blog.0xproject.com/how-to-participate-in-the-zeip-23-vote-eaa861298033)代币持有者投票。该投票是为了通过 [ZEIP-23](https://blog.0xproject.com/zeip-23-trade-bundles-of-assets-fe69eb3ed960)并启动“交易数个资产“。该提案以 5,061,033 ZRX (流通量的 0.86%)参与率和 99% 同意票通过。

NEM基金会的资金提案于 2月15日 [开始](https://forum.nem.io/t/nem-foundation-update-vote-for-funding-proposal-2019/22007)投票，投票开放 5 天。 资助提案以 90％ 赞成票和 10％ 的弃权[通过](https://forum.nem.io/t/vote-for-nem-foundation-funding-proposal-2019-approved-by-the-community/22060) - 获得 “重要证明”（NEM加权持有人影响力的方式）4.56％ 的投票。 投票的基础是，需要 65％ 的赞成票，并且至少 3％ 的网络 POI 必须达到法定人数的要求。 通过将 0 XEM交易发送到是或否地址，在 NEM 钱包内进行投票。 同时为 “NEM实验室” 提供资金的另一项建议也取得了成功，参与程度相似，批准率为 98.8％。NEM基金会的提案要求在XEM 中获得 800万 美元（这个数据令人惊讶地难以找到，只能在[google文档](https://docs.google.com/presentation/d/1nMR_1ajVcpdGW7g8I0p7ZGh88tZ1SL5RzG5TsLW6Qnk/edit#slide=id.p2)演示文稿中找到），而 NEM 实验室的提案要求获得 327万 美元。

2018年第四季度 Aragon 透明度报告[发布](https://blog.aragon.org/aragon-q4-2018-transparency-report/)。本报告详细列出了与项目相关的支出。 2018 年第四季度的总支出为1,055,484.43 欧元或等值的加密货币，工资为 26.8万 欧元，向服务提供商支付的金额为 33万 欧元，赞助/活动门票为 45,000 欧元，托管 AraCon 会议的金额为 63,000 欧元，[Nest](https://github.com/aragon/nest)团队为 260,000 欧元（补助计划）。该报告还[描述了](https://twitter.com/AragonProject/status/1067349802365739008) Aragon 协会采取的财务对冲步骤 - 交换 ICO 期间筹集的一些 ETH 以购买其他资产。

EOS 核心仲裁论坛（ECAF）于 2018年6月 发布在[新的](https://medium.com/@eos42/proposed-solution-for-a-broken-blacklist-ce1c18bdf81c) Block Producer 轮换时没有配置黑名单时失效的情况。这使得一个列入黑名单的地址可以移动超过 200 万个 EOS。 失效的原因是黑名单已被实施为地址列表，区块生产者不会处理交易，每个区块生产者负责手动维护黑名单。 如果只有一个前21名 BP 没有更新的黑名单，则黑名单账户很容易被清空。目前已经提出的一个解决方案是在做出关于如何处理冻结资金的决定前一直 “对私钥无效”。如何处理列入黑名单的资金问题一直存在，如果公开投票 “删除 ECAF” 被通过，那么ECAF本身就会被解散（目前 99％ 通过，2.4％ 的 EOS 已经投票 ）。

Binance 目前[推出](https://www.theblockcrypto.com/2019/02/07/binance-moves-away-from-ethereum-as-it-prepares-to-launch-dex/)了基于 Cosmos 的 Tendermint 协议和 DPoS 的 DEX。 上币费用 “可能接近 10万 美元” 以 “减少垃圾项目或诈骗项目的数量”。相比之下，Decred 的 DEX 设计没有上币费用，也不需要额外的区块链来进行操作。

加拿大交易所 QuadrigaCX [欠](https://www.coindesk.com/quadriga-creditor-protection-filing)其客户 1.9亿 美元。据报道，这些资金在其创始人去世后[无法操作](https://www.coindesk.com/quadrigacx-crypto-exchange-users-say-they-still-cant-get-their-money-out)，他对交易所的冷钱包拥有唯一的控制权。还有一个[故事](https://www.coindesk.com/quadriga-inadvertently-sent-btc-to-dead-ceos-cold-wallet-ey-report)，BTC 的另一个 50万 美元被 “错误地” 锁定。中心化交易所无休止的失败表明加密货币的保管是多么的具有挑战性。

Medium [暂停](https://archive.today/iKQlv)了[发布](https://medium.com/@zeroresearchproof/quadrigacx-chain-analysis-report-pt-1-bitcoin-wallets-19d3a375d389) QuadrigaCX 钱包分析的账户，再次显示了它的力量。 幸运的是，有人制作了[快照](https://archive.today/xsztt)。暂停隐藏了所有帐户的内容，并导向为 “此页面不可用” 页面，并且没有说明原因。 Medium 是一个功能强大的平台，但其核心是一个中心化服务提供商，可以锁定那些不进行备份的人的数据。像这样的早期行为引发了关于从 Medium 迁移或将其视为镜像的[讨论](https://github.com/xaur/decred-issues/issues/70)。

在 Google Play 商店中发现有 Android 恶意软件[更改](https://www.welivesecurity.com/2019/02/08/first-clipper-malware-google-play/)剪贴板中的加密货币地址。在发送之前，请务必仔细检查地址。


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

感谢 (按字母排序): Dominic, guang, hugo, Jill
