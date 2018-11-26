{DRAFT}# Decred月报 - 11月 

### 开发进展总结
* 开发活动 -  {Decred Dev Snapshot}

[dcrd](https://github.com/decred/dcrd):

* UTXO反转的设置语义 https://github.com/decred/dcrd/pull/1471
* UTXO反转的设置语义数据库迁移 https://github.com/decred/dcrd/pull/1520 

[dcrwallet](https://github.com/decred/dcrwallet):

* 修改-使用频繁的钱包观察地址问题 https://github.com/decred/dcrwallet/pull/1320
* 修改-在某些情况下错过交易和双重交易 https://github.com/decred/dcrwallet/pull/1321

[Decrediton](https://github.com/decred/decrediton):

* 更新到 Electron 3 https://github.com/decred/decrediton/pull/1777
* 增加基金会余额显示 https://github.com/decred/decrediton/pull/1764
* 改善大钱包启动性能 https://github.com/decred/decrediton/pull/1727
* 自动购票v2 https://github.com/decred/decrediton/pull/1744

[Politeia](https://github.com/decred/politeia):

* 投票者隐私改进
* 强调新评论 {wait for merge or move to Dec} https://github.com/decred/politeiagui/pull/897
* 评论积分移到poloteiawww https://github.com/decred/politeia/pull/610

未来几个月的增强功能会专注于改进性能

[Android](https://github.com/decred/dcrandroid):

* 增加与其他APP匹配的QR码分享 
* 图像及logo更新
* 增加选项同钱包账户间转账
* 增加隐私账户功能

[iOS](https://github.com/raedahgroup/dcrios):

* 开启QR码交易
* 配合最新设计元素大幅度修改设计
* 交易细节增加

Trezor: Model T 已[发布](https://blog.trezor.io/firmware-updates-2-0-9-and-1-7-1-developed-by-the-community-for-the-community-c4b965741ca3)最新固件 version 2.0.9.最新版本带Decred支持。感谢 @matheusd。现在Decrediton开发员可以开始整合工作了。

[dcrdata](https://github.com/decred/dcrdata):

* Check if "Graphical Block Display" is complete by month end, tests just launched.
* Check work on OPRETURN and "Side Chain" forward compatibility.
* @gozart 重新融入app到 es6 modules #805

[Ticket splitting](https://github.com/matheusd/dcr-split-ticket-matcher):

* 新的分配教程 (英文): https://www.reddit.com/r/decred/comments/9vhpby/decred_ticket_splitting_overview/
* 新分配视频 (葡萄牙语 英文字幕): https://www.youtube.com/watch?v=3RGoUQK0g24&feature=share
* 分票数量增加 {needs volume numbers pulled for verfication}
* 更新让SPV钱包参与分票 (从 dcrd 到 dcrdata 更改 uxtos lookup): https://github.com/matheusd/dcr-split-ticket-matcher/issues/29

[docs](https://github.com/decred/dcrdocs):

* 重命名 "mining" 改成 "voting", "stakepool" 改成 "VSP" {link}
* 增加词汇表[Glossary](https://github.com/decred/dcrdocs/pull/675)
* 重命名 dev fund 成 "Decred Treasury" https://github.com/decred/dcrdocs/pull/690
* 新Politeia数据页面 {link}

[decred.org](https://github.com/decred/dcrweb):

* 重重命名 "mining" 改成 "voting", "stakepool" 改成 "VSP" https://github.com/decred/dcrweb/pull/435

Dev activity stats for {month}: {} active PRs, {} master commits, {} added and {} deleted lines spread across {} repositories. Contributions came from {}-{} developers per repository. ([chart]({}))


### Politeia提案系统总结

#### 本月完成投票 - 6 份 

**1.[Decred Contractor Clearance Process](https://proposals.decred.org/proposals/fa38a3593d9a3f6cb2478a24c25114f5097c572f6dadf24c78bb521ed10992a4)** 

* 投票结束 - 11月21日 **通过**
* 法定票数：13228/8173 票，13206 通过(95.71%) 
* 提案建议设立 Decred Contractor Clearance (DCC) 为承包商作为对项目参与及贡献的条件。获取DCC必需要有 3个合格承包商／贡献者担保有相关工作需要的技能。相同的，撤掉承包商资格也只需要3个合格承包商／贡献者投票撤除。

**2.[Wachsman Communications Proposal for Decred](https://proposals.decred.org/proposals/bc8776180b5ea8f5d19e7d08e9fcc35f0d1e3d16974963e3e5ded65139e7b092)**

* 投票结束 - 11月5日 **不通过**
* 法定票数：13202/8192 票，3646 通过(27.62%) 
* 专业的宣传公司合作提案。要求为期6个月，每月 2万美金的经费。

**3.[Ditto Communications Proposal for Decred](https://proposals.decred.org/proposals/27f87171d98b7923a1bd2bee6affed929fa2d2a6e178b5c80a9971a92a5c7f50)**

* 投票结束 - 11月5日 **通过**
* 法定票数：21191/8192 票，13206 通过(62.32%) 
* 专业的宣传公司合作提案。要求为期6个月，每月 2万5千美金的经费。

**4.[Decred Open Source Research](https://proposals.decred.org/proposals/c68bb790ba0843980bb9695de4628995e75e0d1f36c992951db49eca7b3b4bcd)**

* 投票结束 - 11月5日 **通过**
* 法定票数：13141/8192 票，11854 通过(90.21%) 
* 提案设立一个开源研究项目，要求 一万美金 作为起始经费，投入研究区块链研究并发布文章。提案通过后，第二个提案可以用来决定研究内容／题材。
 
**5.[Change language: PoS Mining to PoS Voting, Stakepool to Voting Service Provider](https://proposals.decred.org/proposals/522652954ea7998f3fca95b9c4ca8907820eb785877dcf7fba92307131818c75)**

* 投票结束 11月5日 **通过**
* 法定票数：12745/8192 票，11991 通过（94.08%）
* 提案建议把一些Decred专用词更替，并提议以后类似大规模转换专用名词可以通过提案系统做决定

**6.[Premium Listing for Decred on Easyrabbit](https://proposals.decred.org/proposals/34707d34b09c3ebcf0d4aa604e8a08244e8f0f082c0af3f33d85778c93c81434)**

* 投票结束 11月23日 **不通过**
* 法定票数：8756/8156 票，444 通过（5.07%）
* Easyrabbit 交易所已于10月底上线DCR交易。
* 提案要求 30 DCR 将项目升级为高级用户，以获得一些宣传福利 包括 DCR 标志放到主页面上，低交易费，自媒体宣传DCR 等等。 



### 社区讨论

*  电报群讨论 - @Dante正编写节点教程，希望鼓励更多人运行DCR节点。全节点完全是义务贡献没有任何短期收益，只是如果大家都能搭建全节点，网络的健壮性强。比特币现有10000多节点，所以抗打击性很强。DCR想变更安全更去中心化必需把节点数也拉起来。 
*  电报群及微信群 讨论 - @Neil 与社区讨论DCR的抗分叉性。翻译文章-[详细分析Decred的分叉抵抗性](https://www.dcr66.com/threads/decred.40/) 重新被分享并讨论。
*  电报群及微信群 分享 - @Guang 分享翻译文章 - [区块链治理：Decred如何迭代比特币](https://www.dcr66.com/threads/decred.992/) 
*  电报群及微信群 分享 - @Guang 分享 [微博](https://weibo.com/DecredProject)链接终于上线到[Decred项目网站社区](https://www.decred.org/community/)页面，正式加入社区行列。 


### 社区活动
#### 过去 {参考英文月报}

* [Web Summit](https://websummit.com/) 葡萄牙里斯本 11月 5-8.社区成员 @heyvj 和 @jholdstock 提交了[会议报告](https://github.com/heyvj/decred-events/blob/master/reports/20181106-Web-Summit-Lisbon.md)
* [PDX Blockchain Summit & Hackathon](https://pdxblockchainsummit.org) 美国 波特兰(Portland)Nov 11. Raedah Group 分享 Decred 和 去中心化治理。
* [Blockmaster](https://www.blockmaster.com.br/eventos/forum-blockmaster-2018-sao-paulo/)巴西 圣保罗Nov 13. @Rhama 分享 Decred 和 Politeia.
* [BlockchainFiesta](http://blockchainfiesta.io/) 波兰 克拉科夫(Krakow) Nov 16. 社区成员 @artikozel & @donmario在会议后整理提交了一份[会议报告](https://github.com/artikozel/decred-events/blob/patch-1/reports/20181116-Blockchain-Fiesta-Krakow.md)
* [Blockchain Melbourne](https://www.meetup.com/BlockchainMelbourne/events/256295215/)澳大利亚 墨尔本 Nov 20. Henrik Andersson, [Apollo Capital](https://www.apollocap.io/) CIO, 分享对Decred的投资分析

#### 未来 {参考英文月报}
* 活动 1 
* 活动 2 

### DCR网络
#### 算力 {截图 https://dcred.eu/powStats}
#### 票价 - {截图 https://dcred.eu/posStats}
#### 锁仓数额 - {截图 https://dcred.eu/posStats}
#### 币价 {截图 USD／BTC - https://dcrstats.com/}
#### 节点数 {数据 https://dcred.eu/nodeStats}

### Decred 相关新闻
* 标题 1 - 链接 1
* 标题 2 - 链接 2

### 中文媒体／文章链接
* [老胡评测：比特币核心团队开发永不分裂的币DCR](https://www.jinse.com/bitcoin/265836.html)
* [区块链治理：Decred如何迭代比特币](https://www.dcr66.com/threads/decred.992/) 
* [DCR 通过混合共识机制平衡权益分配｜标准共识评级](https://www.aicoin.net.cn/article/54939.html)
* [解析评级 — DCR 通过混合共识机制平衡权益分配](https://medium.com/@guang.dcr/%E8%A7%A3%E6%9E%90%E8%AF%84%E7%BA%A7-dcr-%E9%80%9A%E8%BF%87%E6%B7%B7%E5%90%88%E5%85%B1%E8%AF%86%E6%9C%BA%E5%88%B6%E5%B9%B3%E8%A1%A1%E6%9D%83%E7%9B%8A%E5%88%86%E9%85%8D-%E6%A0%87%E5%87%86%E5%85%B1%E8%AF%86%E8%AF%84%E7%BA%A7-5edc6f03dc1c)
* [扫盲-Decred分票](https://medium.com/@guang.dcr/%E6%89%AB%E7%9B%B2-decred%E5%88%86%E7%A5%A8-ffe3eb2de64d)

### 英文媒体链接

Featured articles:

* {1007} Blockchain forks and chain splits: why we should avoid them by @Haon ([medium](https://blog.goodaudience.com/blockchain-forks-and-chain-splits-why-we-should-avoid-them-f54c693a90f1))
* {1105} https://www.coinbureau.com/interview/marco-peereboom-decred/
* {1109} https://www.reddit.com/r/decred/comments/9vhpby/decred_ticket_splitting_overview/
* {1115} https://medium.com/@dlefebvr/pr-in-politeia-process-progress-and-pitching-in-d88771183dd4
* {1115} https://medium.com/decred/blockchain-governance-how-decred-iterates-upon-bitcoin-3cc7030c655e

Articles:

* {1103} https://coiniq.com/decred-review/
* {1112} https://medium.com/@info_5576/staking-coins-part-3-decred-83d73f29038d

Translations:

* @zubairzia0's "Blockchain governance: how Decred iterates upon Bitcoin" ([original](https://medium.com/decred/blockchain-governance-how-decred-iterates-upon-bitcoin-3cc7030c655e)) [in Chinese](https://medium.com/@guang.dcr/%E8%AF%91%E6%96%87-%E5%8C%BA%E5%9D%97%E9%93%BE%E6%B2%BB%E7%90%86-decred%E5%A6%82%E4%BD%95%E8%BF%AD%E4%BB%A3%E6%AF%94%E7%89%B9%E5%B8%81-53f434b26105) by @guang
* @thedecreddigest's "Decred: Where did it all begin?" [in Spanish](https://medium.com/@decred_es/decred-d%C3%B3nde-comenz%C3%B3-todo-767092c90a3e) by @elian

Videos:

* {1105} Decred Semanal 29/10 - 04/11 (Politeia, Votações, Ditto (Marketing Internacional, Exchange) ([youtube](https://www.youtube.com/watch?v=tIvCFk1Prck))
* {1105} https://www.youtube.com/watch?v=MgtBRlAfu2k
* {1106} Decred im Coincheck - Zahlen, Daten und Fakten ([youtube](https://www.youtube.com/watch?v=mHpqDpSd0Fs))
* {1109} Politeia, como funciona Os desenvolvedores Fernando e Tiago Alves explicam ([youtube](https://www.youtube.com/watch?v=usWrs9B2Rm4), featuring @Tiago Alves and @fernandoabolafio)

### 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群 

月报贡献者 @Guang @ @ 

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)
