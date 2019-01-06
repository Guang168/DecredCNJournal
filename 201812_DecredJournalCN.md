#{DRAFT}# Decred月报 - 12月 

Release candidates of core software v1.4.0 are available for download [on GitHub](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc2). Enthusiasts are free to try them while regular users are advised to wait for the final release. As always, make sure to [verify signatures](https://docs.decred.org/advanced/verifying-binaries/).

## 开发进展总结

除非有版本升级，否则新功能和错误修正都会在项目的主分支。这意味着他们通过了多个开发人员的审核，并且可以由开发人员和爱好者从源代码构建，但在下一个版本升级前没有最终用户的安装程序。

对于像Politeia这样的基于Web的项目，通常新的合并工作会在合并后的deployment才会出现。至于dcrdata区块资源管理器，部署就有点复杂：新功能合并到主分支，部署到alpha，然后到beta，最后才到稳定版。

[dcrd](https://github.com/decred/dcrd): v1.4的RC2已发布。此版本更新包括[智能费用估算器](https://github.com/decred/dcrd/pull/1434)，这功能将允许用户根据需求选择最快交易或最低费率。此功能对于闪电网络非常重要，也是处理网络拥挤的机制。更多详情在[issue](https://github.com/decred/dcrd/issues/1412)中有详细说明。现在支持[允许](https://github.com/decred/dcrd/pull/1516)在任何连接数量下设白名单，这让任何运营端允许自己的SPV客户端。对初始同步，验证和网络操作进行了若干性能改进，选择升级的用户应注意将有一次性的数据库迁移以包含这些更新，平均需时30-60分钟(具体取决于硬件)。完整更改列表可在[发布说明](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc2)查询。

在`go get`工具中发现的允许在使用中毒存储库时远程执行代码[漏洞](https://seclists.org/oss-sec/2018/q4/254)已被修复。dcrd和dcrwallet 因为最近切换到更安全的模块系统所以**并没有受到影响**。 最新版本的依赖项不会像在npm中那样自动获取。另外，dcrd里除了runtime，所有依赖项更改已被审核。这是准备dcrd版本需要那么多努力及为什么依赖数量应该受到限制的部分原因。这些信息在[聊天室](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$154476448242812wqgkf:decred.org)中被讨论。

关于dcrd中实施"父子支付方案"(Child Pays For Parent (CPFP))的讨论[进行中](https://github.com/decred/dcrd/issues/1556)

[dcrwallet](https://github.com/decred/dcrwallet): 发布的v1.4.0 RC2修复了许多关于SPV及错误处理的漏洞，并添加了一系列新的gRPC端点，允许终端用户UI中启动新功能。从钱包到节点的Tor连接已通过支持[代理模式](https://github.com/decred/dcrwallet/pull/1294)解决。足够的网络升级，让修改[将默认交易费用](https://github.com/decred/dcrwallet/pull/1339)降至0.0001 DCR得以完成。更多更改请参考[发布说明](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc2)

[Decrediton](https://github.com/decred/decrediton): v1.4的RC1 (Release Candidate 1)于12月16日[发布](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc1). 初始的Trezor[支持](https://github.com/decred/decrediton/pull/1547)让用户使用Decrediton作为“watch-only” 钱包并通过Trezor验签交易。这功能很可能在获得足够测试前隐藏在设置中。初始版本将不支持投票功能。简单支付验证（SPV-simple payment verification)[选择页面](https://github.com/decred/decrediton/pull/1766)让选择SPV更方便。[Eeter](http://www.eeter.co/) [添加了菜单悬停](https://github.com/decred/decrediton/pull/1816)动画以及其他一些风格改进，包括重新设置[治理页面](https://github.com/decred/decrediton/pull/1844)和合并[颜色主题](https://github.com/decred/decrediton/pull/1749)的要求。经过[MatheusD的努力](https://github.com/decred/decrediton/pull/1904)，Raspberry Pi（和其他ARM处理器设备）的用户将可以访问Decrediton（注意[命令行应用程序(CLI)](https://www.decred.org/downloads/)一直可用于Pi)。[各种设计修复](https://github.com/decred/decrediton/pull/1844)，[大修复](https://github.com/decred/decrediton/pull/1874)和[所需补丁]()也已实施。[更新的发布说明版本](https://github.com/decred/decrediton/pull/1854)允许翻译和包含过去信息。新增的一项新功能针对仅观看(watch only)钱包[构建未签名交易](https://github.com/decred/decrediton/pull/1864)(以便可以在仅观看钱包上创建交易，然后签名并在完整钱包广播)。

许多[设计工作](https://github.com/decred/decrediton/issues?utf8=%E2%9C%93&q=is%3Aissue+author%3Alinnutee+created%3A2018-12-01..2018-12-31)已准备好实施。

[Politeia](https://github.com/decred/politeia)：最新[安全收紧](https://github.com/decred/politeiagui/pull/935){等待合并}将Politeia在[securityheaders.com](https://securityheaders.com/?q=test-proposals.decred.org&followRedirects=on)的评级推至A+，将其列入安全标题前3％和名人堂！投票工具的[投票顺序](https://github.com/decred/politeia/issues/565)隐私增强开发以及[允许Tor的bug修正](https://github.com/decred/politeia/pull/639)已完成。[评论计算跟踪](https://github.com/decred/politeia/pull/610)已标准化并整合到Politeia Web(从Politeia Daemon中删除)和[管理员在提案放弃的限制](https://github.com/decred/politeiagui/pull/936)已整合。[为常用命令添加](https://github.com/decred/politeia/pull/625)帮助信息，然后[所有主要命令](https://github.com/decred/politeia/pull/640)添加。 Politeia bulid指令[进行了大修整](https://github.com/decred/politeia/pull/645)。

* visual diff of old proposal versions https://github.com/decred/politeiagui/pull/949 {is it a full user tangible feature or work towards it?}
* thanks to lemonkabir for discovering couple [security](https://github.com/decred/politeia/issues/647) [issues](https://github.com/decred/politeia/issues/650)

WIP:

* Implementation of admin backups is in progress {link}
* Cache layer https://github.com/decred/politeia/pull/648

[Android wallet安卓钱包](https://github.com/decred/dcrandroid):

* 预发布
  * https://twitter.com/raedahgroup/status/1075903485919428608
  * https://www.reddit.com/r/decred/comments/a846ch/decred_wallet_for_android_release_candidate/

* v1.0.0 release candidates:

https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet
https://play.google.com/store/apps/details?id=com.decred.dcrandroid.testnet
https://github.com/decred/dcrandroid/tree/v1.0.0-rc2
https://github.com/raedahgroup/mobilewallet/tree/v1.0.0-rc1

Limitations of wallet encryption and risks of staking on insecure Android smartphones was discussed in [this chat](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$154533559847474ZIrlD:decred.org).

[iOS wallet苹果钱包](https://github.com/raedahgroup/dcrios): {}

[dcrdata](https://github.com/decred/dcrdata):

* v3.1.0 released and deployed to explorer.dcrdata.org, release notes here https://github.com/decred/dcrdata/releases/tag/v3.1.0 {extract highlights}

Congrats and thanks to dcrdata team!

* refactoring merged https://github.com/decred/dcrdata/pull/839
* fixes for browsers with javascript disabled https://github.com/decred/dcrdata/pull/852 _(special thanks from an anti-js dinosaur)_.
* {elaborate on the version bump from 3.2 4.0}
* Docker image to build and test dcrdata https://github.com/decred/dcrdocker/pull/45
* new FAQ wiki page for developers https://github.com/decred/dcrdata/wiki/FAQ
* CSV data export {wait for merge} https://github.com/decred/dcrdata/pull/894

Public dcrdata Tor service was temporarily shut down after a DDoS attack. After some [discussion](https://matrix.to/#/!YwropUjOvDAjfbVSzi:decred.org/$154480347443065mKiKp:decred.org) it was brought back at [dcrdata2opeenddl.onion](http://dcrdata2opeenddl.onion/).

[Ticket splitting](https://github.com/matheusd/dcr-split-ticket-matcher): {}

[docs](https://github.com/decred/dcrdocs):

* thanks to redirection infrastructure laid out previously, work began to [tidy up URLs](https://github.com/decred/dcrdocs/issues/659) and directory structure:
  * https://github.com/decred/dcrdocs/pull/728
  * {wait for merge} https://github.com/decred/dcrdocs/pull/735
* Agenda Voting is changed to Consensus Rules Voting https://github.com/decred/dcrdocs/pull/733
* translation framework was removed https://github.com/decred/dcrdocs/issues/736

[decred.org](https://github.com/decred/dcrweb):

* Decred Business Brief is now available as a [web page](https://decred.org/brief/) in addition to the PDF download.

Other:

* Raspberry Pi offline tx signer by @matheusd https://www.reddit.com/r/decred/comments/a3bfyi/raspberry_pi_offline_transaction_signer/
* [authit](https://authit.co/), dcrtime UI proof of concept. Source is [here](https://github.com/getset0/authit), discussed [here](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$154454253739832PpXgR:decred.org). Credits to @fernandoabolafio, @tiagoalvesdulce and @vctt.
  * the repository was moved to decred GitHub organization https://github.com/decred/authit
* atomicswap PoC work https://github.com/xaur/decred-issues/issues/8#issuecomment-447220453
* Company 0 does not plan to charge Treasury for the privacy work, as clarified in this thread https://www.reddit.com/r/decred/comments/a6l00i/why_is_the_community_not_voting_on_implementing/
* pull request was submitted that adds QTUM support to atomicswap, feel free to join testing https://github.com/decred/atomicswap/pull/93
* Discord is still the dominant source of spam, help is welcome
* coordinated effort to translate Decred articles https://github.com/artikozel/decred-translations
* Decred CLI tools can be built to run on Alpine Linux that uses [musl](https://www.musl-libc.org/) (cleaner implementation of libc), read [this chat](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15457968071823GYapk:decred.org) for details

12月开发活动数据: 分布于{}个存储库（repositories) 有 {} 有效PRs, {} 主要提交, {} 行添加 及 {} 行删除。每个存储库中有来自{}个开发者的贡献。()

## 人员

{welcome contributors whose work was merged to master branches for the first time}

{welcome new individual and company contractors listed on decred.org, updates from existing}

夏天时，[30000fps](https://twitter.com/30000fps)已成为Decred承包商。他的工作目标之一是通过寻找有意义的方式突显呈现及说明一般情况不起眼的流程和功能。最近的开发视觉呈现及decred.org中子页面标题为示例([v1.4.0 release](https://user-images.githubusercontent.com/17774057/50576201-3e124e80-0e15-11e9-83cd-28b50cfd9357.gif) (4 MB), [Politeia release](https://twitter.com/decredproject/status/1052203697986363392), [v1.3.0 release](https://twitter.com/decredproject/status/1044693349205200896))

decred.org中移除了3名贡献者 https://github.com/decred/dcrweb/pull/472

{interviews about people}

部分承包商在[聊天室](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$154508806344819aIkBV:decred.org)分享了他们的入职经验，这是了解如何加入Decred很好的资料。

https://medium.com/@richardred/working-for-the-decred-dae-a9cfb17686fa

## 治理

{high level recap of decision-making activity, most important events, defer to Politeia Digest for the rest}

{bounty prop passed, interesting fact about pseudonymous contributor https://twitter.com/lukebp_/status/1078691610253250560}

{income and spendings from treasury}

聊天室中[讨论到](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$154502025444491kdLiq:decred.org)了特别在熊市时必须控制节约开销。

https://www.reddit.com/r/decred/comments/aa5jvn/any_updates_on_antonopouloss_veiw_of_decred/ 讨论到一下针对Decred治理体系的讨论点包括：“我们不知道治理体系是否有效，因为它还没有失败” 及 “目前还没有争议性课题”

### 本月完成投票 - {} 份 

{}

### 截止12月6日的新提案如下
{}

## DCR网络

算力: 12月算力开始大约167Ph/s结束约183 Ph/s，本月中最高207Ph/s及最低110Ph/s，而大部分时间平均于150Ph/s左右。BeePool矿池算力份额在1.3%-29%间疯狂跳动，F2Pool也一样2.8%-49%。Luxor1%-6.5%，及Coinmine 1%-2%。未命名算力占全网算力45%-70%，最低33%及最高87%。矿池分布数据为大约值无法精确计算。 

投票: 30日 平均票价为 103 DCR。价格与101.33 DCR 至 107.09 DCR之间浮动。锁仓数额为4.14-4.23 百万 DCR, 大约总流通量的 45.53%-46.23%。

节点: [dcred.eu](https://dcred.eu/nodeStats)显示 Jan 04 为止 共有 211 public listening Node 及 269 Normal Node。版本分部: 5.2% 为 v1.5.0(pre)开发者版本(+100%)，3.3% 是 v1.4.0(rc1)(+100%), 13.4% 为 v1.4.0（pre)(+6.9%), 43% 为 v1.3.0(-7%),28% 为 v1.2.0 (+3%), 16% 为 v1.1.2 (+3%) 及7% 为 v1.1.0(+2%)。

第300,000区块在这个月被挖矿。DCR流通量已超过 9,000,000!恭喜大家!

## 挖矿

Whatsminer D1 的[中文评论](https://www.cybtc.com/forum.php?mod=viewthread&tid=41377&fromuid=6)。

Luxor发布的设置Whatsminer[教程](https://medium.com/luxor/whatsminer-d1-decred-setup-guide-182eeccaed99)

从eBay上购买矿机必须小心，您有可能只获得[重量](https://matrix.to/#/!NNzHoaSdnsbZDQOXJr:decred.org/$154491308943809bYuYs:decred.org)

whatsminer.net [报告](https://twitter.com/whatsminer/status/1075810531838091265) 第一批D1订单已全部发货。

比特大陆的 [Antminer DR5](https://twitter.com/Antminer_main/status/1072435004142182400)在推出是收到推特社区批评。


## 整合

### 交易所

* {is it legit? twitter is too young} https://twitter.com/HuobiRussia/status/1075424271537709058

### 钱包

硬件钱包公司Ledger[发推文](https://twitter.com/LedgerHQ/status/1072446149863329792)说明期待已久的DCR整合到Ledger Nano S及Ledger Blue已完成

> 我们很高兴公布Ledger Nano S及Ledger Blue现已和DCR匹配。Decred已在Ledger Live上发布并成为自推出以来第一个本机Ledger Live集成。这里可以阅读更多: https://www.ledger.fr/2018/12/11/ledger-nano-s-ledger-blue-and-ledger-live-now-support-decred-transactions/

DCR可以通过Ledger Live储存。Ledger Live是自从Ledger在今年早些时候停止使用app后的访问加密资产一站式应用。

{explain:

* what this means: "first native Ledger Live integration since its launch"
* what is Ledger Live? is it a wallet? is it a web wallet? do users control keys?
* does it share data with 3rd party servers?
* is it open source?
* is firmware open source?}

Cobo Wallet [发布](https://twitter.com/cobo_wallet/status/1070805250376900609)新的代管投票服务。请对于谁控制密钥，是否市区共识及Politeia投票权等影响作出研究。[此处](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$154413818735775gNTIq:decred.org)讨论{keep? dig whether the service controls keys and consensus/Pi voting rights}

## 落地应用

{}

## 外展活动

{overview of outreach/communications/marketing activity for past month and any short-term plans}

基于Ditto展开了他们的工作，12月对于Decred来说是个令人兴奋的一个月。第一项就是介绍和确定工作流程。你可以在各Matrix聊天室遇到我们的好友Liz Bagot，Trey Ditto，Margaret Mei，Blain Rethmeier，及Milvian Preito。这些聊天室包括Marketing，Ditto PR 及 DCR Writers。

消息传递方面工作已展开并在这里可以查看，也欢迎持续的意见投入。同时，我们正在与设计团队合作，将新消息传递集成到网站中，并通过新页面扩展内容，进一步解释Decred的重要信息。

传递信息内容应该会在一月份达成一致，并且开启网站上的工作。一个关于活动及其他策略的计划也会在一月份公布。

Ditto团队加入了#marketing，该聊天室在整个月都非常热闹，也有很多关于信息内容的讨论。

@Dustorf及@jy-p和Ditto在纽约开会, 这里可以看到[报告](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154413732235771XIVBH:decred.org) {extract highlights}

@liz_bagot发布了第一期的Ditto双周[更新](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154482468943386bBAIp:decred.org?via=decred.org&via=matrix.org)

Update from Ditto for December:

* Had a 2.5-hour onboarding session with Dustin and Jake in our Brooklyn office in early December.
* Created a foundational messaging platform containing a breakdown of Decred's audiences, an about section, a mission statement, a vision statement, and positioning statements for each unique audience. We [submitted](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154524074346294yVYFR:decred.org) the messaging platform to the Decred community for feedback and intend to do another iteration of the document that incorporates the feedback in January.
* Attended and sent reporters from Breaker Mag, Forbes, and Fortune to Decred's meet up in NYC.
* Arranged and staffed interviews between couple big outlets and Decred community members. No set publication dates yet.
* We pitched Jake's commentary on 2019 crypto predictions with crypto reporters and secured coverage in [NullTX](https://nulltx.com/decred-co-founder-pronounces-2018-as-the-death-of-the-ico-model/), [Crypto Briefing](https://cryptobriefing.com/crypto-2019-institutional-adoption/), [The Daily Hodl](https://dailyhodl.com/2018/12/21/after-bitcoin-rallies-18-industry-insiders-weigh-in-on-a-bull-run-and-cryptos-next-turn/), and [CCN](https://www.ccn.com/2018-in-4-words-icos-and-ethereum-are-dead/).

Murad Mahmudov 建议专注于传递保存价值方面的信息：[](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15459293712709dEJuG:decred.org){keep?}

目前有5位知名社区会员拥有发@decredproject推特账号推文的权利

Targeted advertising report for {month} was posted by @{}. {short recap}. Read more [here]({link}).

## 社区活动
### 过去

Decred于12月5日星期三在纽约市flatiron区的Distributed Global举行了首次聚会。大约80人包括VC，其他项目的开发者，媒体和Decred社区的成员出席。项目负责人Jake Yocom-Piatt发表了Decred概述介绍，然后深入讨论了Politeia提案系统的技术细节，包括它的工作原理和应用的潜在广度。

之后，Iterative Capital的创始人Chris Dannen讨论了工作的发展方式，特别是在免费开源软件的时代。他解释了Decred的资金管理如何与一个巨大的工作趋势相吻合，这种工作趋势为工人提供了所需的自主权，使他们能够做到最好。

最后，Placeholder VC的Chris Burniske和Joel Monegro帮忙举办一个对答环节，从机构投资者的角度解释Decred的价值。 Chris透露了VC的财务推理，包括：

1. 团队 - btcsuite 发布时和BTC Core发布的一样好
2. PoW/PoS混合制度比任何其他网络都安全
3. 基金会资助确保开发的长期资金
4. 抗分叉-Decred是为了达成共识过程中维持社区而设

Joel对Decred的治理系统及其让Decred多态，在社区决定时添加功能的能力表示赞赏。 他们得出结论，Decred是为数十年的时间而建造/设计的。 他们分享了他们为了Decred在托管，交易和机构投票方面所做的一些工作，并总结，目前Decred面临的最大问题是流动性。

创始人之夜于12月6日星期四举行，是Distributed Global的节日派对。他们从各个办公室引进了他们所有的GP，并邀请他们的LP，合作伙伴以及他们投资组合中的各种项目的成员。这是一个很好的机会，可以满足于各个社区见面，并为纽约市未来的活动建立起关系。 我们的目标是在纽约举办下一届Decred活动，期待与更多人会面并发展社区。

### 未来活动:

* [10 lat Bitcoina](https://10latbitcoina.com.pl/)-一月26日，波兰华沙@karamble 将在一个庆祝比特币白皮书和比特币10周年纪念的峰会上发表演说。

## 中文媒体／文章链接
* (1204)[加密货币精选：德信币(DCR)](https://www.weibo.com/ttarticle/p/show?id=2309404313596447316959#_0)

## 英文媒体链接

### Articles:
* https://blog.bbod.io/decred-dcr-fundamental-analysis/ {good? accurate?} ([中文版](https://www.weibo.com/ttarticle/p/show?id=2309404313596447316959)和[日文版](https://cointyo.jp/article/10005567))
* https://medium.com/decred/detailed-analysis-of-decred-fork-resistance-93022e0bcde7
* https://cryptobriefing.com/bitcoin-miners-silent-price-falls/ ([中文版](https://www.jinse.com/bitcoin/288904.html))
* https://nulltx.com/decred-co-founder-pronounces-2018-as-the-death-of-the-ico-model/
* https://coinrivet.com/the-practical-cypherpunk-marco-peereboom-of-decred/
* https://www.ccn.com/2018-in-4-words-icos-and-ethereum-are-dead/
* https://51pct.io/decred-governance-and-funding-reimagined/ (部分需要付费阅读)
* https://medium.com/@richardred/working-for-the-decred-dae-a9cfb17686fa


以上是网络发布中较有趣的文章。[decred-media-tracker](https://github.com/RichardRed0x/decred-media-tracker)项目是为了跟踪所有文章。

### Translations:
* Decred Journal - November 2018 @elian 翻译的[西班牙语](https://medium.com/@decred_es/bolet%C3%ADn-mensual-decred-noviembre-2018-52168692e624), @kozel 翻译的[波兰语](https://github.com/artikozel/DecredJournalPL/blob/master/journal/201811_DecredJournalPL.md)及@DZ 翻译的[俄罗斯语](https://medium.com/decred-russia/decred-journal-%D0%BD%D0%BE%D1%8F%D0%B1%D1%80%D1%8C-2018-d0aceacfd72a)。 11月月报是目前最大一份(59 KiB), 感谢大家翻译工作的努力！
* 您可以在Decred Journal[主页](https://xaur.github.io/decred-news/)找到所有翻译链接
* [Detailed analysis of Decred fork resistance](https://medium.com/decred/detailed-analysis-of-decred-fork-resistance-93022e0bcde7) by @Haon - @kozel 翻译的[波兰语](https://github.com/artikozel/decred-articles/blob/master/Polish/into-polish/decredforkresistance.md)
* [How to Get Hired as a Decred Contractor](https://medium.com/decred/how-to-get-hired-as-a-decred-contractor-e1435842df10) by @Haon - @guang 翻译的[中文](https://www.weibo.com/ttarticle/p/show?id=2309404315589245067163)

### Audio:

* Free Talk Live 2018-10-27 Interview with Marco Peereboom of Decred at the Texas Bitcoin Conference https://soundcloud.com/freetalklive/free-talk-live-2018-10-27#t=40:50 _(missed in Oct issue)_
* Episode 18: Murad Mahmudov on Bitcoin http://didyouknowcrypto.com/episode-18-murad-on-bitcoin/ {extract highlights}

## 社区讨论

{}
## 中文社区讨论
{}


### 通讯系统新闻：

* @dhill hunted down bridge bug https://github.com/42wim/matterbridge/pull/644, but a few more bugs remain related to messages with attachments
* \#smart_contracts channel was archived due to inactivity
* Rocket.Chat is being [retired](https://github.com/decred/dcrweb/pull/460)
* landing page for new matrix users https://github.com/decred/dcrweb/pull/462
* issue tracker PoC, 35 issues
* a few threads were created that spurred useful discussion, and were later removed wasting the effort of all people who bothered to reply. Links to access deleted content were posted later. But generally this incident shows an attack/sabotage vector: trigger the discussion and then delete the thread, wasting community's energy. Reddit has no defence from it since moderators cannot disallow users to delete their content. {important. own paragraph?}

For yet another time, a lot of strange Reddit activity was timed close to our major release. It is either an unusual amount of questions about less relevant things, or "innocent" questions about trivial things, or something similar. All coming from accounts never seen before and that never stay. This notice is to inform people who care about the project to watch for weird activity that can waste yours project's energy. Read [this chat](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$154531182347084ccYxu:decred.org) for more details.

{selected discussed topics, as bullet list or one paragraph per topic}

Reddit: {interesting threads}

Twitter: {interesting threads}

{link to chat index}


## 相关外部信息

{PoW, ASIC resistance, tech}


Vertcoin (VTC) 受到51%[攻击](https://medium.com/coinmonks/vertcoin-vtc-is-currently-being-51-attacked-53ab633c08a4)，在4个事件中发生22次重组及15次双花，受害者损失大约 100,000美元。这再次肯定了某些币种容易受到矿工的攻击。这些币种不是矿机主要挖掘对象(GPU挖矿或抗ASIC，也包括比特币分叉币)，矿工只需要有合适的硬件及没有兴趣维护主链就可进行攻击。这些攻击的影响之一是货币被认为是不安全的，因为它曾经失败了。任何仍愿意接受它的人在确认转移可能有非常多的确认数量要求，使得货币移动缓慢。

[Horizen(之前为zencash)](https://www.horizen.global/)团队最近发布了[战略调整](https://blog.zencash.com/re-strategic-actions-for-horizen-from-rolf-versluis/)调整财政部区块奖励额，从10% 增加到20%，减少矿工的奖励金额。在币价跌了90%，及人员和其他成本大幅减少后，更进一步的削减成本将危机项目运行。由于IOHK开发的财务系统仍然在[原型阶段](https://blog.zencash.com/dao-prototype/)和为准备好使用，团队认为有必要单方面决定更改区块奖励。

EOS区块生产者[开始支付](https://cointelegraph.com/news/eos-node-offers-users-financial-rewards-for-votes-reignites-decentralization-debate)把票投给他们的持币者。

Aragon治理提案(AGPs)第一轮投票由于以太坊君士坦丁堡硬分叉造成潜在网络不稳定原因被[推迟](https://forum.aragon.org/t/agp-vote-delay-announcement/426) - 希望“区块链由于维护原因而关闭”不是Politeia会遇到的Decred问题。Aragon Association(Aragon协会)的CEO在提案提交开启前[发布](https://forum.aragon.org/t/agp-wishlist-and-blacklist/355)了提案的黑名单及愿望清单。在AGP[流程](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-1.md)的第一个提案在99.97%同意票数的[通过](https://blog.aragon.org/final-results-from-the-agp-1-vote/)。总共2.6%的ANT代币，从45个独特地址在第一个提案中投票。在48小时投票期开始前，AGPs通过了Aragon协会董事会及社区审核。

200万枚BTCP通过漏洞被开采并在CoinMetrics注意到供应有问题作出[调查](https://coinmetrics.io/bitcoin-private)前并没有被发现。开发团队[发布]（https://medium.com/@bitcoinprivate/official-statement-on-coinmetrics-report-6f1cef176c05）正式声明确认该漏洞。该漏洞在1月5日一个赏金猎人的补丁中被合并，该赏金猎人在收到工作奖励后离开。一行缺失的代码对网络的价值造成了巨大的破坏。我们可以从这个不幸的经历中学习很多：广泛的测试覆盖率，对共识代码的严格评论，在关键任务部分工作的开发人员建立的声誉，以及协议的多个实现对于构建我们可以投以资金信任的系统非常重要。

比特币的Electrum在基础设施上受到了[攻击](https://www.reddit.com/r/CryptoCurrency/comments/a9yji3/electrum_wallet_hacked_200_btc_stolen_so_far/)。 有人启动了一堆恶意的Electrum服务器，促使用户“升级”到恶意软件版本并窃取200多个BTC。Electrum模型涉及位于客户端和完整节点之间的服务器网络。每个客户端依赖它们连接的服务器，这会损害用户隐私，因为这些服务器的所有者可以推断出用户拥有的钱包。如果Electrum服务器遭到破坏，这将会打开一些额外的攻击。Decred选择不开发类似Electrum的基础设施，而是直接进行客户端过滤。 这延迟了轻客户端的开发，但现在在dcrwallet，Decrediton和drcandroid中工作的SPV模式独立于任何服务提供商，并因此增强了用户的隐私。

安全研究人员[演示](https://media.ccc.de/v/35c3-9563-wallet_fail)如果实际拥有该设备,可以以多种方式破解最流行的硬件钱包，。

{DEX}

最新[blockchaintransparency.org](https://www.blockchaintransparency.org/)的交易量报告得出的结论是，coinmarketcap.com排名前25位的与BTC对中，超过80％的交易量是洗牌交易。另一个难过的发现是，平均项目花费超过50,000美元的上市费用。该报告激发一些了分析DCR的交易量的[想法](https://github.com/xaur/decred-issues/issues/34)。

{related exchanges and websites}

Coinbase通过[注册商标](https://www.coindesk.com/coinbase-wants-to-own-buidl-trademark-filing-reveals
)拥有“BUIDL”一词

https://www.coindesk.com/executives-at-korean-crypto-exchange-upbit-indicted-for-fraud

很多加密货币服务及团队视乎由几个实体拥有或共同拥有 https://twitter.com/tangleblog/status/1068094875533479937

多个中心化交易所在年度[Proof-of-Keys](https://www.proofofkeys.com/)活动中[无法提供提款](https://www.ccn.com/several-exchanges-said-to-be-failing-bitcoin-ownership-event/)  

{other: regulations, security, fun}

如果您[碰巧来自“错误”的国家]，Slack可以[关闭您的帐户](https://twitter.com/a_h_a/status/1075510422617219077)。 Matrix 聊天室可以通过多个服务器联合，因此即使某些参与的服务器关闭，其他管辖区域中的服务器也可以继续运行并保留历史记录。

* https://twitter.com/aaomidi/status/1075621119028314112
* https://www.engadget.com/2018/12/22/iran-sanctions-slack/

{write something on a wave of layoffs in the space that did not affect Decred}

* https://cointelegraph.com/news/reports-bitmain-allegedly-fires-all-bch-developers-in-wave-of-redundancies

[Copernicus](https://github.com/copernet/copernicus) is an implementation of the Bitcoin Cash protocol written in Go that utilizes btcsuite. The authors [acknowledge](https://www.copernicuscore.org/btcd.html) btcsuite's contribution to the Bitcoin ecosystem.

[Copernicus](https://github.com/copernet/copernicus)是用Go编写的比特币现金协议的一个实现，它使用了btcsuite。作者就btcsuite对比特币生态系统的贡献表示[肯定](https://www.copernicuscore.org/btcd.html)。

## 关于月报
12月为英文第9期[GitHub](https://xaur.github.io/decred-news/journal/201812)月报。 点击[这里](https://xaur.github.io/decred-news/)浏览往期月报。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues)和[Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

月报贡献者

## 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)





