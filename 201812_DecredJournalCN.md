#{DRAFT}# Decred月报 - 12月 

## 开发进展总结

除非有版本升级，否则新功能和错误修正都会在项目的主分支。这意味着他们通过了多个开发人员的审核，并且可以由开发人员和爱好者从源代码构建，但在下一个版本升级前没有最终用户的安装程序。

对于像Politeia这样的基于Web的项目，通常新的合并工作会在合并后的deployment才会出现。至于dcrdata区块资源管理器，部署就有点复杂：新功能合并到主分支，部署到alpha，然后到beta，最后才到稳定版。

[dcrd](https://github.com/decred/dcrd): v1.4的RC1(Release Candidate 1)版本于12月15日[发布](https://www.reddit.com/r/decred/comments/a6a5fz/dcrd_version_140_release_candidate_1/)。这版本更新包括[智能费用估算器](https://github.com/decred/dcrd/pull/1434)，这是个期待已久的功能，允许用户根据需求选择最快交易或最低费率。该功能在[issue](https://github.com/decred/dcrd/issues/1412)中有详细说明。现在支持在任何[无论连接数量](https://github.com/decred/dcrd/pull/1516)下设白名单，允许dcrd连接到哪些节点方面得以更好地控制，这包括配置为使用SPV模式的钱包。对初始同步，验证和网络操作进行了若干性能改进，选择升级的用户应注意将有一次性的数据库迁移以包含这些更新，平均需时30-60分钟(具体取决于硬件)。团队准备v1.4版本时也[完成版本更新模块](https://github.com/decred/dcrd/pull/1541)。


在`go get`工具中发现了一个允许在使用中毒存储库时远程执行代码的漏洞{link}。dcrd和dcrwallet 因为最近切换到更安全的模块系统所以**并没有受到影响**。 最新版本的依赖项不会像在npm中那样自动获取。另外，dcrd里除了runtime，所有依赖项更改已被审核。这是准备dcrd版本需要那么多努力及为什么依赖数量应该受到限制的部分原因。这些信息在[聊天室](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$154476448242812wqgkf:decred.org)中被讨论。

关于dcrd中实施"父子支付方案"(Child Pays For Parent (CPFP))的讨论[进行中](https://github.com/decred/dcrd/issues/1556)

[dcrwallet](https://github.com/decred/dcrwallet): 从钱包到节点的Tor连接将在下一个版本中提供，开发解决了代理支持问题-[阻止通过Tor从dcrwallet到dcrd的连接](https://github.com/decred/dcrwallet/pull/1294)。足够的网络升级，让修改[将默认交易费用](https://github.com/decred/dcrwallet/pull/1339)降至0.0001 DCR得以完成。


[Decrediton](https://github.com/decred/decrediton): v1.4的RC1 (Release Candidate 1)于12月16日[发布](https://github.com/decred/decred-binaries/releases/tag/v1.4.0-rc1). 初始的Trezor[支持](https://github.com/decred/decrediton/pull/1547)让用户使用Decrediton作为“watch-only” 钱包并通过Trezor验签交易。这功能很可能在获得足够测试前隐藏在设置中。初始版本将不支持投票功能。简单支付验证（SPV-simple payment verification)[选择页面](https://github.com/decred/decrediton/pull/1766)让选择SPV更方便。


[Eeter](http://www.eeter.co/) [添加了菜单悬停](https://github.com/decred/decrediton/pull/1816)动画以及其他一些风格改进，包括重新设置[治理页面](https://github.com/decred/decrediton/pull/1844)和合并[颜色主题](https://github.com/decred/decrediton/pull/1749)的要求。经过[MatheusD的努力](https://github.com/decred/decrediton/pull/1904)，Raspberry Pi（和其他ARM处理器设备）的用户将可以访问Decrediton（注意[命令行应用程序(CLI)](https://www.decred.org/downloads/)一直可用于Pi)。[各种设计修复](https://github.com/decred/decrediton/pull/1844)，[大修复](https://github.com/decred/decrediton/pull/1874)和[所需补丁]()也已实施。[更新的发布说明版本](https://github.com/decred/decrediton/pull/1854)允许翻译和包含过去信息。
新增的一项新功能针对仅观看(watch only)钱包[构建未签名交易](https://github.com/decred/decrediton/pull/1864)(以便可以在仅观看钱包上创建交易，然后签名并在完整钱包广播)。

许多[设计工作](https://github.com/decred/decrediton/issues?utf8=%E2%9C%93&q=is%3Aissue+author%3Alinnutee+created%3A2018-12-01..2018-12-31)已准备好实施。

[Politeia](https://github.com/decred/politeia)：最新[安全收紧](https://github.com/decred/politeiagui/pull/935){等待合并}将Politeia在[securityheaders.com](https://securityheaders.com/?q=test-proposals.decred.org&followRedirects=on)的评级推至A+，将其列入安全标题前3％和名人堂！

投票工具的[投票顺序](https://github.com/decred/politeia/issues/565)隐私增强开发以及[允许Tor的bug修正](https://github.com/decred/politeia/pull/639)已完成。[评论计算跟踪](https://github.com/decred/politeia/pull/610)已标准化并整合到Politeia Web(从Politeia Daemon中删除)和[管理员在提案放弃的限制](https://github.com/decred/politeiagui/pull/936)已整合。[为常用命令添加](https://github.com/decred/politeia/pull/625)帮助信息，然后[所有主要命令](https://github.com/decred/politeia/pull/640)添加。 Politeia bulid指令[进行了大修整](https://github.com/decred/politeia/pull/645)。

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

夏天时[@30000fps](https://twitter.com/30000fps)开始对Decred identity的动画及图形设计作出贡献

decred.org中移除了3名贡献者 https://github.com/decred/dcrweb/pull/472

{interviews about people}

部分承包商在[聊天室](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$154508806344819aIkBV:decred.org)分享了他们的入职经验，这是了解如何加入Decred很好的资料。

## 治理

{high level recap of decision-making activity, most important events, defer to Politeia Digest for the rest}

{bounty prop passed, interesting fact about pseudonymous contributor https://twitter.com/lukebp_/status/1078691610253250560}

{income and spendings from treasury}

聊天室中[讨论到](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org/$154502025444491kdLiq:decred.org)了特别在熊市时必须控制节约开销。

### 本月完成投票 - {} 份 

{}

### 截止12月6日的新提案如下
{}

## DCR网络
第300,000区块在这个月被挖矿。DCR流通量已超过 9,000,000!恭喜大家!

### 算力 

{}

### 票价

{}

### 锁仓数额 

{}

### 币价

{}

### 节点数

{}

## 挖矿

Whatsminer D1 的[中文评论](https://www.cybtc.com/forum.php?mod=viewthread&tid=41377&fromuid=6)。

Luxor发布的设置Whatsminer[教程](https://medium.com/luxor/whatsminer-d1-decred-setup-guide-182eeccaed99)

从eBay上购买矿机必须小心，您有可能只获得[重量](https://matrix.to/#/!NNzHoaSdnsbZDQOXJr:decred.org/$154491308943809bYuYs:decred.org)

whatsminer.net [报告](https://twitter.com/whatsminer/status/1075810531838091265) 第一批D1订单已全部发货。

比特大陆的 [Antminer DR5](https://twitter.com/Antminer_main/status/1072435004142182400)


## 整合

### 交易所

* {is it legit? twitter is too young} https://twitter.com/HuobiRussia/status/1075424271537709058

### 钱包

https://twitter.com/LedgerHQ/status/1072446149863329792

> We are excited to announce that the Ledger Nano S and Ledger Blue are now compatible with Decred. Decred is now available on Ledger Live and marks the first native Ledger Live integration since its launch. Read more here: https://www.ledger.fr/2018/12/11/ledger-nano-s-ledger-blue-and-ledger-live-now-support-decred-transactions/

{explain:

* what this means: "first native Ledger Live integration since its launch"
* what is Ledger Live? is it a wallet? is it a web wallet? do users control keys?
* does it share data with 3rd party servers?
* is it open source?
* is firmware open source?}

Cobo Wallet [announced](https://twitter.com/cobo_wallet/status/1070805250376900609) a custodial staking service. Please do your research to understand the implications like who controls the keys, whether you lose consensus and Politeia voting rights, and so on. Discussed [here](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$154413818735775gNTIq:decred.org){keep? dig whether the service controls keys and consensus/Pi voting rights}

## 落地应用

{}

## 外展活动

{overview of outreach/communications/marketing activity for past month and any short-term plans}

Ditto people joined #marketing and the room was very hot throughout the month. There was a lot of brainstorming and deciding on messaging.

@Dustorf, @jy-p and Ditto met in New York, report [here](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154413732235771XIVBH:decred.org) {extract highlights}

@liz_bagot gave the inaugural Ditto Bi-Weekly Update [here](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154482468943386bBAIp:decred.org?via=decred.org&via=matrix.org)

Update from Ditto for December:

* Had a 2.5-hour onboarding session with Dustin and Jake in our Brooklyn office in early December.
* Created a foundational messaging platform containing a breakdown of Decred's audiences, an about section, a mission statement, a vision statement, and positioning statements for each unique audience. We [submitted](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154524074346294yVYFR:decred.org) the messaging platform to the Decred community for feedback and intend to do another iteration of the document that incorporates the feedback in January.
* Attended and sent reporters from Breaker Mag, Forbes, and Fortune to Decred's meet up in NYC.
* Arranged and staffed interviews between couple big outlets and Decred community members. No set publication dates yet.
* We pitched Jake's commentary on 2019 crypto predictions with crypto reporters and secured coverage in [NullTX](https://nulltx.com/decred-co-founder-pronounces-2018-as-the-death-of-the-ico-model/), [Crypto Briefing](https://cryptobriefing.com/crypto-2019-institutional-adoption/), [The Daily Hodl](https://dailyhodl.com/2018/12/21/after-bitcoin-rallies-18-industry-insiders-weigh-in-on-a-bull-run-and-cryptos-next-turn/), and [CCN](https://www.ccn.com/2018-in-4-words-icos-and-ethereum-are-dead/).

Now a total of 5 well known community members have the rights to tweet via @decredproject Twitter account.

Targeted advertising report for {month} was posted by @{}. {short recap}. Read more [here]({link}).



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

## 社区活动
### 过去

{}

### 未来活动:
{}

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


## 相关外部信息

{PoW, ASIC resistance, tech}

VTC 51% attack:

* https://medium.com/coinmonks/vertcoin-vtc-is-currently-being-51-attacked-53ab633c08a4
* https://coingeek.com/vertcoin-loses-over-100000-in-51-attack-report/
* https://www.theblockcrypto.com/2018/12/03/long-tail-cryptocurrency-is-51-attacked-vertcoin-edition/
* {explain the impact}

{governance, forks, chain splits, controversy}

[Horizen(previously zencash)](https://www.horizen.global/) recently announced a [strategic action](https://blog.zencash.com/re-strategic-actions-for-horizen-from-rolf-versluis/) in a blog post to increase the Treasury block rewards from 10% to 20% claiming a difficult choice was made by the team to reduce the amount of rewards for the miners.Consider they have planned a DAO treasury and voting system, with [prototype delivered](https://blog.zencash.com/dao-prototype/), this decision to change rewards without consensus voting from the whole community came a little surprising. {need polishing and improve writing}

EOS block producer [began paying](https://cointelegraph.com/news/eos-node-offers-users-financial-rewards-for-votes-reignites-decentralization-debate) holders that voted for it.

The Growing Focus on Blockchain Governance [article](https://www.tokendaily.co/blog/the-growing-focus-on-blockchain-governance) by Chris McCoy was discussed [in #governance](https://matrix.to/#/!tIDEIWechmqCLjPiui:decred.org/$154466528741798eoKOQ:decred.org) for it's strange interpretation of Decred's vote to choose a PR firm. It claims that the decision is called _"very basic"_ and _"day-to-day"_, that it distracts _developers_ and makes _the protocol_ susceptible to mob rule. The article comes for a founder of another project active in the governance domain.

2 million BTCP were mined via an exploit and went unnoticed for months until CoinMetrics noticed something is wrong with the supply and [investigated](https://coinmetrics.io/bitcoin-private) it. Developer team [posted](https://medium.com/@bitcoinprivate/official-statement-on-coinmetrics-report-6f1cef176c05) an official statement confirming the inflation exploit. The bug was merged on Jan 5 together with a patch from a bounty hunter that disengaged after receiving the reward for his work. Just one missing line of code made a huge damange to the network's value proposition. We can take a lot from this unfortunate experience: extensive test coverage, super critical review of consensus code, established reputation of developers working on mission critical parts, and having multiple implementations of the protocol are all very important to build a system we can trust money to.

There was an [attack](https://github.com/spesmilo/electrum/issues/4968) on Bitcoin's Electrum infrastructure. Someone started a bunch of bad Electrum servers that prompted the user to "upgrade" to a malware version. Electrum model involves a network of servers that sit between clients and full nodes, which is bad for client's privacy but can also go wrong if the network of Electrum servers is not as strong as the network of more mission critical full nodes. Decred was reluctant to build Electrum infrastructure for these very problems and decided to go straight to client-side filtering approach, at the cost of postponing the release of light clients. Now that it is done, dcrwallet and Decrediton in SPV mode connect directly to full nodes.

{DEX}

Latest exchanges volumes report by [blockchaintransparency.org](https://www.blockchaintransparency.org/) concluded that of the coinmarketcap.com top 25 BTC pairs over 80% of volume is wash traded. Another unhappy finding is that the average project spent over $50,000 on listing fees. The report has spurred [the idea](https://github.com/xaur/decred-issues/issues/34) to analyze the trading volume of DCR.

{related exchanges and websites}

Coinbase seeks to own term "BUIDL" https://www.coindesk.com/coinbase-wants-to-own-buidl-trademark-filing-reveals

https://www.coindesk.com/executives-at-korean-crypto-exchange-upbit-indicted-for-fraud

Many cryptocurrency services and projects seem to be owned or co-owned by a couple of entities https://twitter.com/tangleblog/status/1068094875533479937

{other: regulations, security, fun}

Slack can close your account if you happen to be from a wrong country https://twitter.com/a_h_a/status/1075510422617219077 . Matrix rooms can be federated over multiple servers, so even if some participating servers are shut down, servers in other jurisdictions can keep running and keep the history.

* https://twitter.com/aaomidi/status/1075621119028314112
* https://www.engadget.com/2018/12/22/iran-sanctions-slack/

{write something on a wave of layoffs in the space that did not affect Decred}

* https://cointelegraph.com/news/reports-bitmain-allegedly-fires-all-bch-developers-in-wave-of-redundancies

[Copernicus](https://github.com/copernet/copernicus) is an implementation of the Bitcoin Cash protocol written in Go that utilizes btcsuite. The authors [acknowledges](https://www.copernicuscore.org/btcd.html) btcsuite's contribution to Bitcoin ecosystem.

## 关于月报
12月为英文第9期[GitHub](https://xaur.github.io/decred-news/journal/201812)月报。 点击[这里](https://xaur.github.io/decred-news/)浏览往期月报。

大部分来自第三方的信息在基本检查后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues)和[Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

月报贡献者

## 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)





