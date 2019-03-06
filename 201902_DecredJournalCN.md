# Decred月报 - 2月 

![Decred Journal - February 2018]()




## 开发进展总结

[dcrd](https://github.com/decred/dcrd):通过允许[少一个](https://github.com/decred/dcrd/pull/1596)选票双重支付和[拒绝](https://github.com/decred/dcrd/pull/1597)同区块的双花来收紧mempool政策。 从dcrd[删除](https://github.com/decred/dcrd/pull/1607)钱包的类型并[迁移](https://github.com/decred/dcrwallet/pull/1394)到dcrwallet，这简化了对dcrwallet的更改，并在dcrd中触发[重构](https://github.com/decred/dcrd/pull/1613)，以提供更强大的模块边界并简化依赖图。[删除](https://github.com/decred/dcrd/pull/1599)非root 的Go模块替换 - 这有助于确保测试中的所有模块为最新代码，并帮用户保持它们独立准确。

[dcrwallet](https://github.com/decred/dcrwallet): v1 自动购票经过数个更新版本后已[被移除](https://github.com/decred/dcrwallet/pull/1396)。

[Decrediton](https://github.com/decred/decrediton): Electron 4 [升级](https://github.com/decred/decrediton/pull/2009)让在 Windows 启动[更稳定](https://github.com/decred/decrediton/pull/2017)。在自动购票运行是增加[退出提醒](https://github.com/decred/decrediton/pull/1989)。

多个[响应视图](https://github.com/decred/decrediton/issues?q=is%3Aissue+author%3AMariaPleshkova+created%3A2019-02-01..2019-02-28)已完成设计阶段并准备实施。

[Politeia](https://github.com/decred/politeia): 新功能: 突出显示自上次登陆的新评论及密码更改后邮件[通知](https://github.com/decred/politeia/pull/680)(通过Bug Bounty漏洞报告奖励计划[提议](https://github.com/decred/politeia/issues/673))。

Epic cache layer work was [merged](https://github.com/decred/politeia/pull/660)! Thanks @lukebp and all reviewers/testers. This paves the way for a lot of site performance improvements. Among other completed work are CLI tool [improvements](https://github.com/decred/politeia/pull/707) and [fsck](https://github.com/decred/dcrtime/pull/46) (file system verification tool) for dcrtime.

In progress:

* Work [started](https://github.com/decred/politeia/pull/689) to scale www database using CockroachDB.
* A decision [was made](https://matrix.to/#/!VFRvyndKpzcLrVslQD:decred.org/$15507680085008gMbtf:decred.org) to move the code for contractor management system in politeia and politeiagui repositories to avoid the overhead of maintaining two codebase forks and keeping them in sync.
* Change of the default comment sorting algorithm is being [discussed](https://github.com/decred/politeiagui/issues/1022).

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

* [voting.decred.org](https://voting.decred.org/) dashboard now shows past agendas too. jQuery was [removed](https://github.com/decred/hardforkdemo/pull/213) to the delight of those who understand.
* Replacement of Google reCAPTCHA with self-hosted solution was [merged](https://github.com/decred/dcrstakepool/pull/281) - huge step in improving [stakeholder's privacy](https://github.com/xaur/decred-issues/issues/25). Thanks to all developers and testers of this patch.
* Trivia: did you know that Decred heavily [discourages](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15497657664963CvzUr:decred.org) creation of dust outputs?
* [PoC UI](https://github.com/xaur/decred-issues/issues/8) for atomic swaps made a few steps.
* QTUM support [merged](https://github.com/decred/atomicswap/pull/93) in atomicswap, POLIS support [removed](https://github.com/decred/atomicswap/pull/99).
* Work [started](https://github.com/decred/dcrseeder/pull/19) to add DNSSEC support to dcrseeder.
* [authit](https://github.com/decred/authit), the UI for dcrtime is now hosted at [timestamp.decred.org](https://timestamp.decred.org/). Feedback is welcome in [GitHub issues](https://github.com/decred/authit/issues) or in the new [#timestamp](https://matrix.to/#/!gltiHJRZiSJTzvjOEu:decred.org) chat room.

> I must say, Go really is an amazing language. I don't think I have felt so comfortable in a new language so quickly. (@jholdstock in [chat](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15497080644503VtguR:decred.org))

2月开发活动数据: 分布于 {} 个存储库（repositories) 有 {} 有效 PRs, {} 主要提交, {} 行添加 及 {} 行删除。每个存储库中有来自 {}-{} 个开发者的贡献。

---

## 人员

欢迎新到来的首次贡献者，代码在 GitHub 上合并：@jozn ([dcrd](https://github.com/decred/dcrd/commits?author=jozn)), JoeGruffins ([dcrwallet](https://github.com/decred/dcrwallet/commits?author=JoeGruffins)), luoshang722 ([atomicswap](https://github.com/decred/atomicswap/commits?author=luoshang722)), rex4539 ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=rex4539)).

恭喜在decred.org上[列出的](https://github.com/decred/dcrweb/issues/562)三位Ditto承包商

* Elizabeth Bagot (@liz_bagot)
* Margaret Huang (@margaret_mei)
* Milvian Prieto (@milvian)

1名贡献者从decred.org中[移除](https://github.com/decred/dcrweb/pull/541)：Jure Kralj (@praxis, Reddit 管理员).

## 治理

{} 月，[DCR基金会](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了 {} DCR，并花了 {} DCR。使用 DCR {} 月份的每日平均美元价格 {} 美元计算，本月收到 {} 万 美元以及支出 {} 万 美元。由于这些付款用于支付 {} 月完成的工作，因此可以用 {} 月的平均价格 {} 美元计算 - 在这种情况下，美元收到的数字是 {} 万美元以及支出 {} 万美元。

## 网络

算力: {} 月算力以 ～{} Ph/s 开始，以 ～{} Ph/s 结束，本月中最高 {} Ph/s 及最低 {} Ph/s。在{}月{}日根据 [dcrstats.com](https://dcrstats.com/pow) 数据显示，矿池算力分布为：Poolin {}%, F2pool {}%, BTC.com {}%, UUPool {}%, Luxor {}%, CoinMine {}% 及 其他 {}%。矿池分布数据为大约值无法精确计算。 

投票: 按{}月{}日 dcrstats.com（数据显示）, 30日 平均票价为 {} DCR (+{})。价格在 {} DCR 至 {} DCR之间浮动。锁仓数额为 {}-{} 百万 DCR, 大约为总流通量的 {}-{}%。

在2月11日同一个区间内购买的1,265张选票使得在后面7次票价调整中涨至 119.4。随后选票池票数下跌至低于4万张选票 （上次发生于2017年11月），导致连续10次调整降至 98.4 DCR。在票价到底时，在同一区间内又卖出最高2，880 张中的2，797 张选票，

节点: 截止于{}月{}日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 {} public listening Node 及 {} Normal Node。版本分布: 

## 挖矿



## 整合


## Adoption


## 外联活动


## 社区活动

出席：

* {}

即将到来的：

* {}

## 媒体



## 社区讨论

截止于 Feb 4 的社区数据 :

* Twitter followers: {} (-106)
* Reddit subscribers: {} (+89)
* Matrix users: {} (+26)
* Slack users: {} (+110)
* Telegram users: {} (-231)
* YouTube subscribers: {} (+14)
* Facebook followers: {} (+11), likes: {} (+11)
* LinkedIn followers: Decred page {} (+{}), Politeia page {} (+3)
* GitHub dcrd stars: {} (+{}), forks: {} (+{})

社交系统新闻：


## 市场

在二月中 DCR 交易价格为 美金 {}-{} / BTC {}-{}。平均日汇率为 {} 美元。

## 相关外部信息





## 关于月报
二月为英文第11期 [GitHub](https://xaur.github.io/decred-news/journal/201902) 月报。 点击[这里](https://xaur.github.io/decred-news/)浏览所有往期月报，翻译等。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues) 和 [Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

感谢 (按字母排序): 


## 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

感谢 (按字母排序): 
