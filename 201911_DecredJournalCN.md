# Decred月报 - 2019年11月

![abstract art](img/journal-201911-384.png)

_图片: Powermove by @saender

11月的主要内容：

- v1.5.0的最终测试版本2和3已经发布，并且两个版本都已确定存在问题（RC3中的问题影响到Windows中的Decrediton）。感谢所有通过下载这些发行候选版本并报告他们遇到BUG的贡献者。
- Decred DEX基础设施项目本月取得了重大进展，增加了Decred钱包的初始版本，身份验证管理和Epoch时间处理。
- @elian的拉美营销和活动提案已获得批准，这是其批准的第一个区域性营销工作，其预算不占用主要营销预算。
- @matheusd删除了大量博客文章，列出了在Lightning Network上进行票务拆分的计划，以这种方式进行分票的优势（最低参与量低，更好的用户体验），需要进行共识的变更以促进其顺利实施。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 性能增强和代码清除。

在等待v1.5最终版本的同时，开发正在朝着[1.6.0](https://github.com/decred/dcrd/milestone/24)迈进。

[`regentemplate`](https://github.com/decred/dcrd/pull/1979) 引入命令以强制使用新事务生成最新模板。

对内存池进行了更改，以在从对等方断开连接时[退出](https://github.com/decred/dcrd/pull/1982)所有剩余的孤立进程，并根据最近的改进来修改 [孤立](https://github.com/decred/dcrd/pull/1984)的TX策略。

[添加](https://github.com/decred/dcrd/pull/2000)了新的区块链参数，用于指定区块链的最小已知总工作量。检查链条是否最新的代码已更新为使用总工作量而不是最终检查点的高度。此方法不依赖于受信任的已知检查点，无论区块的接收和处理顺序如何，该方法都是有效的，并且通常是链重组无法使之无效的更客观的值。

`lru` [扩展](https://github.com/decred/dcrd/pull/2002)了程序包，以允许插入和检索键值对（除了值之外）。

[dcrwallet](https://github.com/decred/dcrwallet): Bug修复，代码清除。

添加了用于检测[重用地址](https://github.com/decred/dcrwallet/pull/1616)及其相应出站的方法。

[Decrediton](https://github.com/decred/decrediton): 大量错误修复和UI调整，代码清除。

首次初始化闪电网络钱包时，添加Toggle以[创建](https://github.com/decred/decrediton/pull/2310)特定于闪电网络的钱包帐户。这激励用户不要使用他们的大部分资金的默认钱包帐户，如果选择了自动开启功能，这可能会导致许多渠道自动打开。

部署了新一批的[响应视图](https://github.com/decred/decrediton/pulls?q=is%3Apr+merged%3A2019-11-01..2019-11-30+responsive)。

修复了在RC1和RC2测试期间发现的多个错误。

十一月总共[合并](https://github.com/decred/decrediton/pulls?q=is%3Apr+merged%3A2019-11-01..2019-11-30)了54个拉取请求。

[Politeia](https://github.com/decred/politeia): 付款信息已[添加](https://github.com/decred/politeia/pull/1051)到后端，使CMS可以完全恢复基于politeiad的发票信息。

现在支持在[Windows](https://github.com/decred/politeia/pull/1046)上构建politeiavoter 。

CMS的前端重新设计正在进行中。

[RFP流程](https://github.com/decred/politeia/pull/1054)流程的实施已开始。

[dcrstakepool](https://github.com/decred/dcrstakepool): 开始工作对服务器具有私钥的投票权的选票[进行](https://github.com/decred/dcrstakepool/pull/571)任意投票。工作继续实施[每张选票](https://github.com/decred/dcrstakepool/issues/568)认证和选票购买，以删除用户帐户，投票地址重用和电子邮件要求。

[dcrpool](https://github.com/decred/dcrpool): 正在增加广泛的[测试范围](https://github.com/decred/dcrpool/pull/141)。

[dcrlnd](https://github.com/decred/dcrlnd): BUG修复，改进测试和构建基础结构。Dockerfile 已[更新](https://github.com/decred/dcrlnd/pull/56)为dcrlnd。

[cspp](https://github.com/decred/cspp): 加了RPC超时，改进了客户端-服务器错误处理，允许使用LetsEncrypt登台服务器。

[dcrdex](https://github.com/decred/dcrdex): 进度很快！11月实施的新组件包括：[身份验证管理器](https://github.com/decred/dcrdex/pull/50), [帐户注册商](https://github.com/decred/dcrdex/pull/58), initial version of [Decred钱包](https://github.com/decred/dcrdex/pull/49)客户端的初始版本，客户端[websocket](https://github.com/decred/dcrdex/pull/55)连接性，[初始时期处理](https://github.com/decred/dcrdex/pull/66)和匹配存储以及过渡。识别未用资金的方式已从txid / vout更改为更抽象的[coin ID](https://github.com/decred/dcrdex/issues/75)，以在将来可能支持基于非UTXO的资产。

[dcrandroid](https://github.com/decred/dcrandroid):继续增加[多钱包支持](https://github.com/decred/dcrandroid/pull/401)。

[dcrios](https://github.com/raedahgroup/dcrios): 重新设计，UI调整，BUG修复。

导航菜单重新[设计](https://github.com/raedahgroup/dcrios/pull/524)。当应用程序处于后台模式时，添加了通知以显示[同步状态](https://github.com/raedahgroup/dcrios/pull/529)。

继续对该书进行[修改](https://github.com/raedahgroup/dcrios/issues/506)，[钱包还原](https://github.com/raedahgroup/dcrios/pull/527)和[验证种子](https://github.com/raedahgroup/dcrios/pull/530)视图的工作。

[dcrdata](https://github.com/decred/dcrdata): v5.2现已发布！

前端亮点：更新的标题和块页面，改进的图表，用于将文本复制到剪贴板上的地址和哈希值的按钮。后端：添加dcrd v1.5支持，删除了对PostgreSQL的SQLite支持，Insight API修复，性能改进。查看[发行说明](https://github.com/decred/dcrdata/releases/tag/v5.2.0)以查看所有更改。该版本在4个月内由9位贡献者进行了83次提交。祝贺dcrdata团队！

将添加[CSPP匿名混合](https://github.com/decred/dcrdata/pull/1610)（实时显示在[block](https://alpha.dcrdata.org/block/403513)页面的alpha上），计算攻击成本的工作正在进行中。

[docs](https://github.com/decred/dcrdocs): 新的[隐私指南](https://github.com/decred/dcrdocs/pull/1029)，[治理概述](https://github.com/decred/dcrdocs/pull/1030)的检修，新的[开发者文档](https://github.com/decred/dcrdocs/pull/1017)的链接，次要更新和清理。

[decred.org](https://github.com/decred/dcrweb): 较小的更新和清理。

[删除了](https://github.com/decred/dcrweb/pull/745) Cobo 托管钱包，认为不应推广其资产托管的解决方案。交易页面已[更新](https://github.com/decred/dcrweb/pull/746) （Nanex，OOOBTC已删除）。

其它:

- @matheusd [概述](https://blog.decred.org/2019/11/11/LN-Multi-Owner-Tickets/)了在Lightning Network上实施多所有者票证（“票据拆分”）的方法。正确地进行操作需要一些渐进的改进和共识中的一些新操作码。该博客是技术性很强的文章，但是链接到4个更深的[帖子](https://www.reddit.com/r/decred/comments/duzv3m/ln_multiowner_tickets_blog_post_from_matheus/)，这些链接对我们强大的社区成员来说是最重要的。Reddit的讨论对帖子进行了补充，并解决了@bee提出的一系列问题（tl; dr：这不仅仅是对共享门票的史诗性投资，因为大多数建议的更改本身都是有用的改进）。
- @karamble [发布了](https://twitter.com/karamblez/status/1197676296240861186)带有EPaper显示屏的Raspberry Pi Decred [仪表板](https://github.com/karamble/dcraspaper) 。
- 开发者正在使用Go 1.13和@jrick的发布工具（在[这里](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$157308464734953aRCth:decred.org)讨论）[测试](https://github.com/jrick/release)可复制的内部版本。希望有更多的人来验证构建，为您提供帮助。

11月的开发活动统计：分布在12个存储库中的173个活动PR，342个主提交，添加72K和删除19K的行。每个存储库的贡献来自1-7个开发者。

## 人员

欢迎新到来的首次贡献者，他们的代码已合并到主库中：zeoio ([dcrdex](https://github.com/decred/dcrdex/commits?author=zeoio)), githubsands ([dcrlnd](https://github.com/decred/dcrlnd/commits?author=githubsands)), eharris128 ([dcrweb](https://github.com/decred/dcrweb/commits?author=eharris128))。

我们检测早期遗漏的两个新贡献者：neddoz（[dcrios](https://github.com/raedahgroup/dcrios/commits?author=neddoz) （自6月）和quacklabs [dcrios](https://github.com/raedahgroup/dcrios/commits?author=quacklabs)自9月）。欢迎上车！

社区统计：

- Twitter 粉丝: 40,641 (+9)
- Reddit 订阅: 9,703 (+47)
- Matrix 用户: 474 (+18)
- Slack 用户: 6,872 (+14)
- Discord 用户: 2,592 (+40), 已验证发布: 379 (+21)
- Telegram 用户: 2,903 (-63)
- YouTube 订阅: 3,920 (+60)
- Facebook 粉丝: 3,307 (+11), 喜欢: 3,027 (+8)
- LinkedIn 粉丝: 662 (+24)
- GitHub dcrd 星星: 520 (+3), 分叉: 1,400 (+0)

## 治理

十一月份，[社区开发基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)获得了14,096 DCR，并花费了17,889 DCR。按照11月份的每日DCR / USD汇率$ 19.97计算，这是收到的$ 281K和花费的$ 357K。以10月份的每日平均汇率$ 15.59计算，该月完成工作的美元费用为$ 279K。截至12月2日，库存余额为640201 DCR（12.40百万美元，$ 19.44）。

提交了两份新提案，一份是DCR版本的Point of Sale应用程序[PlusBit](https://proposals.decred.org/proposals/e559188b0febcab29c49c1f7dd5c66645e31be00894a150ef7d0b8ceb6486605)，售价为650美元，另一份是@ buck54321，要求30,000美元来继续开发[TinyDecred](https://proposals.decred.org/proposals/ad0f9688b3467734e2581604914b2cc32c6eb7991dff460eff41d21f66d88451)。对这两个提案的投票于12月3日开始。

拉丁美洲市场营销[提案](https://proposals.decred.org/proposals/5af0ce1cd325be6be39109c2750f34095c4e8feeea962ede058a1e4f4a61473e)由@elian提出，已获得75％赞成票，29％的参与获得批准，研究和教育的提案通过@ammarooni用80％赞成票，29％的参与获得批准。Dota2奖金提案被拒绝，获得5％的批准和29％的参与。

@richardred 在10月中旬至11月中旬向DCR订单簿中生成了一份[报告](https://www.blockcommons.red/publication/mm-tracking-1/)，因为i2 Trading开始使DCR市场符合其批准[提案](https://proposals.decred.org/proposals/2eb7ddb29f151691ba14ac8c54d53f6692c1f5e8fe06244edf7d3c33fb440bd9)。可以增加额外的流动性，尽管根据在此时间范围内测量的方式（价格波动造成困难的条件），可能无法在所有交易所和货币对中使用90％的正常运行时间。

有关Politeia活动的更深入报道，请参见Politeia Digest [第25期](https://blockcommons.red/politeia-digest/issue025/)。

## 网络

全网算力：11月份的哈希率以约442 Ph/s的速度开始，而以约381 Ph/s的速度结束，在整个月触底达到322 Ph/s的谷值。截至12月4日的池哈希率分布：Poolin 35％，UUPool 32％，F2Pool 11.6％，lab.antpool.com 6.8％，BTC.com 2.8％，Luxor 2.3％，Coinmine 0.11％，BeePool 0.10％，suprnova 0.01％和其他[dcrstats.com](https://dcrstats.com/pow)的 9.45％。池分配数是近似值，无法准确确定。

Staking: 每个dcrstats.com的30天平均票价为134.8 DCR（+2.5）。价格在123.9-150.4 DCR之间变化。锁定金额为5.29-54.9百万DCR，相当于可用供应量的49.50-51.17％。

自从sdiff算法更改以来，门票价格创下了新高，而51.17％是新的历史[最高参与率](https://explorer.dcrdata.org/charts?chart=stake-participation)。

[11月29日](https://explorer.dcrdata.org/charts?chart=missed-votes&zoom=k0x6wa44-k3ucpasw&bin=window&axis=time)又发生了一次投票失败的事件。

节点：整个[11月](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1572566400000&to=1575158400000)，每个dcr.farm平均有189个公共侦听节点和398个普通节点。版本分发：73％使用dcrd v1.4，9.6％使用dcrd v1.5开发版本和RC，2％使用dcrd v1.6开发版本，而8.8％使用dcrwallet v1.4。

截至12月4日，根据[dcrdata](https://explorer.dcrdata.org/agendas)，大约有24％的PoS选民表示他们已经升级并准备投票赞成共识规则更改。

11月24日，有[400,000](https://www.reddit.com/r/decred/comments/e0yvyb/block_400000/)个区块被利益相关者挖出并审核。

## 整合

Bittrex 在其交易所中[添加](https://twitter.com/BittrexExchange/status/1194330471385186316)了DCR / USD [交易对](https://global.bittrex.com/Market/Index?MarketName=USD-DCR)。@jz提供了一些[背景信息](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$157358651139766wUsaK:decred.org)，并解释说i2trading将为该市场提供流动性。

Abra钱包/交易所[增加](https://support.abra.com/hc/en-us/articles/360001777271-We-ve-added-new-cryptocurrencies-)了 Decred对美国和国际客户的支持。根据[此页面](https://www.abra.com/cryptocurrency/investing-guide/)， Abra没有为几项最大的资产保管，但DCR并不是其中的一员，因此被保管。

警告: Decred Journal的作者不了解上述任何服务的可信赖性。在将您的个人信息或资产信任给任何实体之前，请先进行自己的研究。

## 外联活动

11月在世界各地的许多知名活动中均以Decred为特色。去年的许多相同团队成员今年又回到了葡萄牙里斯本的Web Summit，Decred是今年[唯一](https://twitter.com/NoahPierau/status/1192045467435188224) 拥有大量活动的加密货币项目。@ moo31337在名为“您可以信任您的银行吗？”的面板上代表加密货币行业，可以在[这里](https://vimeo.com/375884648)查看。@Dominic [代表](https://twitter.com/wanbihou/status/1193218449721311233) Decred参加了11月8日在中国嘉兴举行的2019年世界区块链大会上。

@Dustorf在#writers会议室中共享了所有新的decred.org子页面的草稿，在社区输入之后，所有内容都已提交给EETER，以进行最终组装，测试和发布。

Decred Assembly在v1.5 RC1上通过@davecgh进行了[Decred深度](https://www.youtube.com/watch?v=gGQuY0kOt7g)，在Decred in Depth中以PRICE的[@liz_bagot on PR](https://soundcloud.com/decredindepth/ep-11-liz-bagot-pr-marketing)和在[Africa and Governance](https://soundcloud.com/decredindepth/ep-12-akin-sawyerr-dcr-africa-governance)上的@akinsawyerr为特色。

Ditto11月的成就包括9种媒体报道：

- An op-ed for @jy-p in [Cointelegraph](https://cointelegraph.com/news/secrets-they-missed-at-devcon-what-its-really-like-in-a-working-dao) titled "Secrets They Missed at DevCon: What It's Really Like in a Working DAO".
- [A podcast](https://podcasts.apple.com/us/podcast/base-layer-episode-086-jake-yocom-piatt-decred/id1445373535?i=1000457565007) with @jy-p on the Base Layer Podcast with David Nage.
- [An article](https://www.forbes.com/sites/cbovaird/2019/11/11/who-will-win-the-race-for-digital-currency-supremacy/) in Forbes featuring @jy-p's commentary on the race between governments, corporations, and decentralized cryptocurrencies to remake the financial system.
- Coordinated [an interview](https://podcasts.apple.com/us/podcast/market-disruptors/id1463411709) for @jy-p on the Market Disruptors podcast.
- [Two feature articles](https://cryptotradernews.com/technology/our-data-privacy-is-under-attack-decred-is-fighting-back/) on Decred's privacy in a new crypto outlet called Crypto Trader News.
- [An interview](https://www.youtube.com/watch?v=4r6z9JZxRRI) between @akinsawyerr and the Nakamoto News Network at the World Crypto Conference in Las Vegas.
- [An interview](https://messari.io/podcast/developer-funding-governance-and-the-evolution-of-decred-with-jake-yocom-piat) with @jy-p on Messari's Unqualified Opinions podcast about developer funding, governance, and Decred.
- [A TV appearance](https://blocktv.com/watch/2019-10-30/5db9ab4487a7e-resolving-corporate-governance-in-cryptocurrency) on BlockTV about resolving corporate governance in cryptocurrency.

其它:

- @liz\_bagot appeared on the Decred in Depth [podcast](https://podcasts.apple.com/us/podcast/liz-bagot-pr-marketing/id1466716734?i=1000455667566) to talk about Ditto's work with Decred.
- Supported Decred's media presence at Web Summit. Secured an interview with BBC, and facilitated meetings with CoinDesk and Cointelegraph. We also created a briefing book of top-tier journalists for the Decred team to speak with and helped @moo31337 prep for his panel discussion in order to maximize their impact at the event.
- Supported @akinsawyerr's presence at the World Crypto Conference in Las Vegas by setting up on-the-ground interviews with media outlets including Legacy Research, Nakamoto News Network, Crypto TV News, and others.
- Secured several podcasts and online interviews for various community members.
- Identified and shared opportunities for the community to engage with Crypto Twitter and educate outsiders about Decred.
- Worked closely to support the Decred developer community's achievements over the last year.

@bee wrote an overview of [marketing strategies](https://xaur.github.io/writings/posts/20191127-marketing-strategies.html) to explore. Some of the key topics are to improve reporting, use word "money", promote the actual use of DCR for tipping, donations and funding projects, pitch DCR to highly aligned communities and individuals as a way to transfer value, and boost social media presence. ([Reddit](https://www.reddit.com/r/decred/comments/e2lhwd/marketing_strategies/))

## 活动

参加:

- Nov 4-7 - [Web Summit](https://websummit.com/) - Lisbon, Portugal. Decred team ran a [stand](https://twitter.com/marco_peereboom/status/1191651269640888320) for 2 days. Very [few](https://twitter.com/NoahPierau/status/1192045467435188224) blockchain projects have secured speaking slots, likely due to the bear market. @moo31337 [talked](https://twitter.com/decredproject/status/1192469998175948801) on the stage with representatives of the finance industry on the topic "Can you really trust your bank?". (photos: [1](https://twitter.com/JamieHoldstock/status/1191760511878279168), [2](https://twitter.com/NoahPierau/status/1192056049764904960), [3](https://twitter.com/kakalordao/status/1192131145141555201), [4](https://twitter.com/marco_peereboom/status/1192990143822454784))
- Nov 6 - [Decred Meetup](https://twitter.com/amxromero/status/1192241858816217089) - Medellín, Colombia. @elian and @victorarubin talked to around 40 people of age 20-50 who asked amazing questions about Politeia, Decred's plans for Latam, PoS attack vectors and smart contracts. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191106-decred-meetup-medellin-colombia.md))
- Nov 7 - [Journey 4.0](https://twitter.com/legal_medellin/status/1189918302061187073) - Medellín, Colombia. @elian was invited by Legal Hackers Medellín to talk about the challenges of blockchain technology for international law at EAFIT University, the biggest business administration university in Colombia. The students got interested by the concept of DAO that exists everywhere and nowhere and doesn't quite fit into traditional legal frameworks. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191107-journey-4-medellin-colombia.md))
- Nov 8 - [World Blockchain Conference](https://www.8btc.com/wbc-2019/) - Jiaxing, China. @Dominic has represented Decred and talked about DAO and privacy features. There have been reports of him being turned into a [cyborg](https://twitter.com/wanbihou/status/1192484367626424321) at the party preceding the event. Community members in the region are advised to follow standard protocols and take necessary precautions. Video footage of robotic [dance](https://twitter.com/wanbihou/status/1193154668601327617) has leaked and sparked [#DecredDanceChallenge](https://twitter.com/hashtag/DecredDanceChallenge). (photos: [1](https://twitter.com/wanbihou/status/1192806081568722944), [2](https://twitter.com/wanbihou/status/1193218449721311233))
- Nov 15 - [Open Banking, Fintech and Blockchain Summit](https://twitter.com/Decred_ES/status/1195025379255144448) in Mexico City, Mexico. @elian was invited to talk about digital identities. During the panel he gave a brief intro to Decred and the importance of security and privacy of personal data, and noted the challenging tradeoff between convenience ("forgot your password?" button) and control provided by self-sovereign identities. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191115-open-banking-summit-mexico-city-mexico.md))
- Nov 15-16 - [CriptoBlock](https://criptoblock.com.br/) - São Paulo, Brazil. @Rhama and @girino gave talks about Decred. Although the organizers worked hard, only around 250 people attended out of 1,000-1,200 expected, reflecting today's market. Decred was a bronze sponsor.
- Nov 21 - [Africa Blockchain Summit](https://www.africablockchainsummit.com/agenda.html) - Rabat, Morocco. @arij took the opportunity to discover the point of view of centralized organizations and to represent Decred to a wide variety of people from different backgrounds. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191121-africa-blockchain-summit-rabat-morocco.md))
- Nov 21 - [Africa Fintech Summit](https://africafintechsummit.com/addis/) - Addis Ababa, Ethiopia. @akinsawyerr spoke on a blockchain panel and made a few valuable connections. A week later he [talked](https://www.youtube.com/watch?v=WOqCjQELpao) about Decred and the trip at @VOANews. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191121-africa-fintech-summit-addis-ababa-ethiopia.md))
- Nov 21 - [Blockchain Conference](https://www.eventbrite.com.ar/e/conferencia-blockchain-tickets-81397410847) - Veracruz, Mexico. The event took place in the largest technology university in the city. @francov\_ and @luisantoniocrag introduced blockchains, Bitcoin and Decred to students and challenged fiat beliefs of a few teachers. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191121-blockchain-and-decred-veracruz-mexico.md))
- Nov 30 - [Decred Meetup](https://twitter.com/RodgersJabz/status/1194309441774063617) - Kampala, Uganda. @jabz's team introduced the audience of 53 to Decred and its features and gave a practical session showing how to use the wallet. ([report](https://github.com/decredcommunity/events/blob/master/reports/20191130-decred-meetup-kampala-uganda.md)).

即将到来:

- Dec 12-13 - Labitconf - Montevideo, Uruguay. Decred team members will be present at the biggest cryptocurrency and blockchain conference in Latin America.
- Jan 7 - [Digital Money Forum](https://thedigitalmoneyforum.com/) - Las Vegas, USA. The event is part of CES 2020. @akinsawyerr will talk on a [session](https://thedigitalmoneyforum.com/Sessions/the-problem-with-old-money-a-great-debate/) about future economy.
- Jan 29-31 - [Crypto 101 Online Summit](https://www.crypto2020summit.com/) - the web. @lukebp will give an overview of Decred's plans for 2020.
- Apr 13-17 - Blockchain Land at Talent Land - Guadalajara, Mexico. Decred will be sponsor of Talent Land and be present with a booth at Blockchain Land.
- May, date TBA - [BitConf](https://www.bitconf.com.br/portal/) - São Paulo, Brazil. The event was moved to May 2020.
- 5-year anniversary event for the Bitcoin Vietnam community. Details TBD.

Full report for October's Decred meetup in Bogota, Colombia, has been [added](https://github.com/decredcommunity/events/blob/master/reports/20191029-decred-meetup-bogota-colombia.md) to the [events repo](https://github.com/decredcommunity/events). There are 37 reports in total. Thanks to everyone for submitting!

## 媒体

Selected articles:

- LN & Multi-Owner Tickets by @matheusd ([blog.decred.org](https://blog.decred.org/2019/11/11/LN-Multi-Owner-Tickets/))
- Introducing 'Peer Production on the Crypto Commons' by @richardred ([blockcommons.red](https://blockcommons.org/post/crypto-commons/))
- Who Will Win the Race for Digital Currency Supremacy? by Charles Bovaird ([forbes](https://www.forbes.com/sites/cbovaird/2019/11/11/who-will-win-the-race-for-digital-currency-supremacy/), [tweet](https://twitter.com/ForbesCrypto/status/1193953360422080512)) - features @jy-p quotes
- Decred's Name Sucks and I'm Glad! by @Dustorf ([medium](https://medium.com/@dlefebvr/decreds-name-sucks-and-i-m-glad-853af487034e))
- What is Decred (DCR)? Why was this cryptocurrency created? by @Haon ([medium](https://medium.com/@NoahPierau/what-is-decred-dcr-why-was-this-cryptocurrency-created-4e5cae085bc7)) - a Frequently Asked Questions
- Secrets They Missed at DevCon: What It's Really Like in a Working DAO by @jy-p ([cointelegraph.com](https://cointelegraph.com/news/secrets-they-missed-at-devcon-what-its-really-like-in-a-working-dao))
- Decred: An Economic Breakthrough by @ammarooni ([medium](https://medium.com/@Ammarooni/decred-an-economic-breakthrough-4d2e3ea27338))
- Our Data Privacy is Under Attack: Decred is Fighting Back by Matthew Harris ([cryptotradernews.com](https://cryptotradernews.com/technology/our-data-privacy-is-under-attack-decred-is-fighting-back/))
- CTN Exclusive: Inside Decred With Co-Founder Jake Yocom-Piatt by Matthew Harris ([cryptotradernews.com](https://cryptotradernews.com/cryptocurrency/ctn-exclusive-inside-decred-with-co-founder-jake-yocom-piat/))
- Decred, Hyper-secure, Unforgeably Scarce by @Checkmate ([medium](https://medium.com/@_Checkmatey_/decred-hypersecure-unforgeably-scarce-e076b91a2be))
- BlackBearXVII's Decred X series continued with:
  - Decred X / Part VI - Triune of Trust ([medium](https://medium.com/@imagnusholdings/decred-x-part-vi-triune-of-trust-3fa7ad1476a5))
  - Decred X / Part VII - Field Manual A ([medium](https://medium.com/@imagnusholdings/decred-x-part-vii-field-manual-a-68306f23d2ca))
  - Decred X / Part VIII - Silver Linings Field Manual B ([medium](https://medium.com/@imagnusholdings/decred-x-part-viii-silver-linings-field-manual-b-d38cb0e6e17c))
  - Decred X / Part IX - Sub Economics ([medium](https://medium.com/@imagnusholdings/decred-x-part-ix-sub-economics-e3b0a5e948e1))

翻译:

- Decred Journal November 2019 was translated to Arabic (@arij), Chinese (@Dominic), Polish (@kozel) and Spanish (@francov\_ and @luisantoniocrag). Thank you for keeping the world updated!

视频:

- Building a Store-of-Value with Decred's Jake Yocom-Piatt on Messari's Unqualified Opinions ([player.fm](https://player.fm/series/messaris-unqualified-opinions/building-a-store-of-value-with-decreds-jake-yocom-piatt), [apple](https://podcasts.apple.com/us/podcast/building-a-store-of-value-with-decreds-jake-yocom-piatt/id1455666979?i=1000457903445)) - live stream viewers ([youtube](https://www.youtube.com/watch?v=LMJp8rKLkkM)) were treated to an angelic performance by @jy-p, answering interesting questions about Decred's history and approach.
- Decred Assembly Deep Dive with @davecgh ([youtube](https://www.youtube.com/watch?v=gGQuY0kOt7g)) - in depth discussion of consensus rules and v1.5.0 RC1.
- Digit-All episode about Decred with @akinsawyerr ([youtube](https://www.youtube.com/watch?v=4r6z9JZxRRI))
- Decred Review: Why DCR Deserves Attention! by Coin Bureau ([youtube](https://www.youtube.com/watch?v=elfBK5QBVmo))
- Why Decred is Overdue for a Coinbase Listing by @Exitus ([youtube](https://www.youtube.com/watch?v=Og3kGX_fYho), discussed on [reddit](https://www.reddit.com/r/decred/comments/dyl6vr/why_decred_is_overdue_for_a_coinbase_listing/))
- Can You Really Trust Your Bank? ([vimeo](https://vimeo.com/375884648)) - @moo31337 features in a panel at Web Summit. @Exitus made a couple of hilarious meme cuts ([first](https://www.youtube.com/watch?v=0Bq48X3cO_s), [second](https://twitter.com/coveryfire7777/status/1199866746192171010))

音频:

- Base Layer Episode 086 - Jake Yocom Piatt (Decred) ([podbean](https://www.podbean.com/media/share/pb-9ah38-c88678), [spotify](https://open.spotify.com/episode/4vMtWg6lejqR9pfKkmsgXc))
- Market Disruptors: Developing Privacy on the Blockchain with Jake Yocom-Piatt ([anchor.fm](https://anchor.fm/markmoss/episodes/Developing-Privacy-On-The-Blockchain-With-Jake-Yocom-e934qv), [stitcher](https://www.stitcher.com/podcast/anchor-podcasts/market-disruptors/e/65439848))
- Decred in Depth Ep. 12 - @akinsawyerr talks about opaque governance in [#cryptocurrency](https://twitter.com/hashtag/cryptocurrency) as a barrier to new entrants, Decred making the rules clear, and the opportunities offered by frictionless trust-minimized global payments in Africa. ([libsyn](https://decredindepth.libsyn.com/akin-sawyerr-dcr-africa-governance), [soundcloud](https://soundcloud.com/decredindepth/ep-12-akin-sawyerr-dcr-africa-governance))
- Decred in Depth Ep. 13 - @richardred talks about contributing to Decred, researching blockchain governance, writing [cryptocommons.cc](https://cryptocommons.cc), and choosing to remain pseudonymous. ([libsyn](https://decredindepth.libsyn.com/richard-red-dcr-research-politeia-mm-proposal), [soundcloud](https://soundcloud.com/decredindepth/ep-13-richard-red-dcr-research-politeia-mm-proposal))

LunarCRUSH shared several [charts](https://twitter.com/LunarCRUSH/status/1191017614971027458) that combine basic market data like price and volume with sentiment analysis of Decred on social media.

## Community Discussions

Selected Reddit posts:

- nnnko56's [reply](https://www.reddit.com/r/decred/comments/e2yiou/what_happens_when_we_reach_max_supply/) to the question: "What happens when we reach max supply?"
- [Decentralized Credits](https://www.reddit.com/r/decred/comments/dqocpf/decentralized_credits/), and [Tacotime Trilogy](https://www.reddit.com/r/decred/comments/dznwsr/tacotime_trilogy/), paintings by @AGNFAB1 on [Twitter](https://twitter.com/AGNFAB1/status/1197455821380243457).
- The 2 posts with the greatest number of comments also have the lowest scores (0), one [asking](https://www.reddit.com/r/decred/comments/dyvrht/so_what_makes_decred_a_better_cryptocurrency_than/) what makes Decred a better cryptocurrency than Nano, one [suggesting](https://www.reddit.com/r/decred/comments/e3vs1o/wouldnt_1_dcr_1_vote_be_fairer/) 1 DCR 1 vote would be better.

Selected Twitter highlights:

- @DCRtheSOV's intro to DCR [tweet](https://twitter.com/DCRtheSOV/status/1191215059680149505) thread
- @DCRtheSOV's monthly [recap](https://twitter.com/DCRtheSOV/status/1194480106892185601) of October progress.
- @karamble's Decred Dashboard for Raspberry Pi [tweet](https://twitter.com/karamblez/status/1197676296240861186) was well received.
- @dcrstakey is [back](https://twitter.com/dcrstakey/status/1193758944587657216).
- The #DecredDanceChallenge was [initiated](https://twitter.com/wanbihou/status/1193154668601327617) in China by the robotic dance moves of someone wearing the famous space cowboy jacket. Highlights include: [@Dustorf/Stakey](https://twitter.com/lefebvre_dustin/status/1195107934839230465), [@karamble](https://twitter.com/karamblez/status/1194664973030641664), [@Camilolwi](https://twitter.com/Camilolwi/status/1194358146027814912), [@JeonHaWoo2](https://twitter.com/JeonHaWoo2/status/1194389449062469634), [@treyditto](https://twitter.com/treyditto/status/1194351696522158080), [@liz_bagot](https://twitter.com/liz_bagot/status/1194393447035224065), [@elian](https://twitter.com/elianhuesca/status/1196526382970540032), [@Francov99_](https://twitter.com/Francov99_/status/1194410868001382401), [@s_ben](https://twitter.com/zen_bacon/status/1194756298987855872), [@luisantoniocrag](https://twitter.com/luisantoniocrag/status/1194438312678887425) and [@degeri](https://twitter.com/degeri_crypto/status/1194522586417225728).
- DCRComic's Bring Your Talent, Enjoy the DAO [tweet](https://twitter.com/DCRComic/status/1199325669055979520).
- @jholdstock [meets](https://twitter.com/JamieHoldstock/status/1192146283835854849) Portuguese Prime Minister.
- @Checkmate [thread](https://twitter.com/_Checkmatey_/status/1197225489959718913) on Decred security.
- @permabullnino [tweets](https://twitter.com/PermabullNino/status/1195356846778912769) about Decred competitive moats.
- @ammarooni [tweets](https://twitter.com/Ammarooni/status/1199804834133762054) to go with the economic breakthrough piece.
- Jesse Walden [tweet](https://twitter.com/jessewldn/status/1194632275389898753) about the Politeia one year report.
- @lukebp [tweets](https://twitter.com/lukebp_/status/1199134933773500416) about what it's like to develop for Decred, started a #cryptodevs hashtag with a number of other people adding their perspectives on what it's like working for Decred.

> - Work with a world class team
> - Build cutting edge, open source technology
> - Work from anywhere
> - Async communication (no meetings!)
> - Set your own schedule (part-time or full-time)

## Markets

In November DCR was trading between USD 15.68-24.73 / BTC 0.0020-0.0029. The average daily rate was $19.97.

## Relevant External

Coinbase published a [post](https://blog.coinbase.com/how-coinbase-views-proof-of-work-security-f4ba1a139da0) about PoW security, outlining its position that it is advantageous for security that the coin be mined by hardware for which this is the dominant use (i.e. ASICs), and that manufacturing and ownership diversity is well served by ASIC-friendly algorithms.

The CEO of MicroBT (maker of Whatsminer D1, one of the current top Decred miners) was [arrested](https://insidebitcoins.com/news/chinese-police-conduct-snap-raid-of-microbt-premises-arrests-ceo/242367) in Shenzhen, China, in relation to a mining patent infringement.

A bug in Zcash implementation [leaked metadata](https://duke.leto.net/2019/10/01/zcash-metadata-leakage-cve-2019-16930.html) and allowed an attacker to link IP addresses to Zcash shielded addresses (_missed in Oct_). From the developer who discovered it: "All people who use zaddrs and who have shared zaddrs with 3rd parties. (...) Consider your IP address and geo-location information associated with it as tied to your zaddr". The bug was copied from Bitcoin Core codebase and introduced in Zcash in 2016. The leak was fixed in v2.0.7-3, although the [security announcement](https://z.cash/support/security/announcements/security-announcement-2019-09-24/) just recommended to upgrade immediately without any details. A number of projects inheriting Zcash code are affected as well. This shows that privacy tech is very delicate and requires simplicity, robust programming approach and extremely thorough review and testing.

The Zcash Foundation and ECC reached [agreement](https://www.zfnd.org/blog/zcash-trademark-resolution/) on how to handle the Zcash trademark. This has been transferred to the Foundation, with an agreement where it shares bilateral power to enforce the mark with ECC. This CoinDesk [article](https://www.coindesk.com/zcash-trademark-talks-were-about-more-than-a-logo) explains how the dispute was about more than a logo, and the power of the trademark holder to effectively decide which chain is Zcash.

Decred adds another dimension whereby the legitimacy of the chain is established by voters, and minority forks are heavily disincentivized with significant challenges to overcome. Even if someone attempts to steal the Decred "trademark", there should not be confusion about what the original chain is because voters are signing each block. Also, Decred has a very clear answer to "who exactly is hiring the dev org? what is the 'community'?" - the stakeholders.

Resolution of the ZEC trademark issue allowed [polling](https://www.zfnd.org/blog/community-sentiment-collection-poll/) for NU4 to proceed, where the Zcash ecosystem/community can signal support for 13 options to fund development. The ECC and Zcash Foundation will consider the results from 3 [or 4](https://twitter.com/zooko/status/1200917828011876352) different polling methods when deciding what plan to adopt.

Aragon [completed](https://blog.aragon.org/final-results-from-aragon-network-vote-4/) its 4th AGP voting round, 15 proposals were voted on and ANT participation was around 3-18%. Among the approved proposals was [AGP-103](https://github.com/aragon/AGPs/blob/master/AGPs/AGP-103.md), introducing a maximum network budget of 5% Treasury value or 250,000 DAI (whichever is greater) per quarterly voting cycle. The largest proposal to be approved (with 9% turnout, 91% approval) is [AGP-106](https://github.com/aragon/AGPs/raw/1bee7c003d2e0dbfdc8cfe698198adeaf2cf0c7b/AGPs/AGP-106.md) to develop and launch Aragon Chain, at a cost of $500,000. The aim is to create a new layer 1 protocol and offer it as an alternative to the Ethereum-based Aragon network. Among the reasons cited were increasing costs of keeping up with changes to the Ethereum network's changes. [AGP-112](https://github.com/aragon/AGPs/raw/1bee7c003d2e0dbfdc8cfe698198adeaf2cf0c7b/AGPs/AGP-112.md), which also passed, issued a proclamation that Aragon is opposed to ProgPoW on Ethereum, or any other non-emergency change to the mining algorithm before Ethereum 2.0. The highest turnout proposal was [AGP-81](https://github.com/aragon/AGPs/raw/1bee7c003d2e0dbfdc8cfe698198adeaf2cf0c7b/AGPs/AGP-81.md), with 17% of ANT turning out to vote "no" on a collaboration with Kleros on the court system.

Aragon Court [launched](https://blog.aragon.org/aragon-court-is-live-on-mainnet/) on mainnet, it is a system for adjudicating "subjective disputes that cannot be resolved by smart contracts". ANT holders can stake their tokens for ANJ tokens, which can then be staked to participate in adjudication of cases brought before the court. Decisions are made through a Schelling game where those who guess the majority decision are rewarded and those who guess wrong have their stake slashed. Registration to become ANJ jurors is set to begin in Jan 2020.

Dragonfly Research published an [article](https://medium.com/dragonfly-research/breaking-mimblewimble-privacy-model-84bcd67bfe52) about "breaking Mimblewimble's privacy model" by monitoring the network in real time. @jy-p had identified this issue as part of his review of privacy solutions, and subsequently discussed it on the base layer [podcast](https://acrabaselayer.podbean.com/e/base-layer-episode-086-jake-yocom-piatt-decred/). A Grin developer [replied](https://medium.com/grin-mimblewimble/factual-inaccuracies-of-breaking-mimblewimbles-privacy-model-8063371839b9) to the article, stating that it has sensationalized a known limitation and does not constitute an attack.

An "Unknown Fund" was [announced](https://www.unknown.fund/press-release), pledging to invest and donate $75 million in Bitcoin for the startups which directly or indirectly support the idea of anonymity. "Preference will be given to the following niches: protection of personal data, tools for anonymity, cryptocurrency and blockchain". The fund is quite opaque, only saying that "Applications are closed for the Unknown Fund. Evaluation will take a few months". People are starting to [ask](https://twitter.com/hasufl/status/1202927790082932736) if it may have been a hoax.

The Stellar Development Foundation (SDF) [announced](https://www.stellar.org/blog/sdfs-next-steps/) that it had [burned](https://www.theblockcrypto.com/linked/45793/the-stellar-foundation-has-burned-over-50-of-the-total-xlm-token-supply-canceling-airdrop-programs) 55 billion XLM, worth over $4.4 billion (notionally), and representing more than 50% of the entirely pre-mined XLM supply. The stated reasons were a belief that the foundation could achieve its aims with less funding, and that the large scale airdrop campaigns were proving ineffective.

The EOS blockchain [entered](https://cointelegraph.com/news/eos-blockchain-congested-eidos-airdrop-95-of-transfers) "congestion mode" due to a surge in transactions related to an airdrop program (EIDOS), which at one stage accounted for 95% of all EOS transactions. One effect is that users who have less staked EOS are unable to make transactions until demand for the airdrop subsides or its CPU lease expires in 30 days. Another effect was a surge of 100,000% in the cost of CPU time on the network.

Block.One [announced](https://cointelegraph.com/news/eos-creator-blockone-to-vote-for-block-producers-with-95-of-coins) that it is going to begin voting for block producers with the 9.5% of EOS it controls - classifying itself as a "Small, but significant EOS token holder". Block.One did not announce how they will be voting.

EOS New York [tweeted](https://twitter.com/eosnewyork/status/1199813240307568641) to uncover the fact that 6 of the registered EOS BPs appear to be operated by the same entity. Although the BPs in question are [not in the top 21 active BPs](https://twitter.com/BlockCommons/status/1200133433009287168), they were receiving rewards regularly as standby BPs.

The Donuts-on-Ethereum experiment of /r/EthTrader is [transitioning](https://www.reddit.com/r/ethtrader/comments/dwiu4f/donutsonethereum_registration_is_open/) on chain to an Aragon DAO. Subreddit members had 2 weeks to register to claim their donuts, starting from Nov 15. As noted in previous issues, the /r/EthTrader community has already fragmented over the way the decentralization of donuts is being handled.

Justin Sun of Tron [revealed](https://www.coindesk.com/despite-denials-tron-founder-confirms-investment-in-poloniex-crypto-exchange) that he is part of an investor group that bought the Poloniex exchange. Mid-November Poloniex listed TRX and started a "deposit competition" with TRX and later [TRC20-USDT](https://support.poloniex.circle.com/hc/en-us/articles/360035962012-Poloniex-x-TRC20-USDT-Rush-Campaign-Information). Later in the month it was [announced](https://www.theblockcrypto.com/post/48603/poloniex-acquires-tron-based-dex-to-offer-decentralized-trading) that Poloniex had acquired a TRON-based DEX TRXMarket and rebranded to Poloni DEX to offer decentralized trading. A few days later the Poloniex Twitter account [tweeted](https://beincrypto.com/poloniex-caught-telling-followers-to-buy-tron-in-deleted-tweet/) "Let's buy #TRON", but this tweet was deleted shortly afterwards.

BitMEX unfortunately [leaked](https://www.coindesk.com/bitmex-exchange-exposes-user-base-in-email-mishap) their email database by sending an email to everyone using cc instead of bcc. Oops. This leads to targeting of users, revealing one aspect of their identity to parties with mal-intent.

Korean [OKEx](https://cointelegraph.com/news/cryptocurrency-exchange-okex-delists-xmr-dash-zec-zen-sbtc) and [Upbit](https://cointelegraph.com/news/upbit-exchange-delists-privacy-coins-due-to-money-laundering-concerns) announced delisting of privacy coins such as Monero, Zcash, Dash and others, although delisting of DASH and ZEC was halted for a [review](https://www.coindesk.com/okex-korea-reviewing-decision-to-delist-privacy-coins-zcash-and-dash) on OKEx. (_missed in Sep and Oct_)

Bittrex has [adopted](https://www.coindesk.com/bittrex-chainalysis-kyt) Chainalysis [Know Your Transaction](https://blog.chainalysis.com/reports/real-time-alerts-press-release) software that monitors 15 cryptoassets for suspicious activity in real-time. (_missed in Sep_)

CoinDesk was observed with pages not displaying unless javascript and certain browser features were enabled, as evidenced by the [lack of snapshots](https://archive.today/https://www.coindesk.com/*) in Oct and Nov. The reasons to disable javascript are: greatly improved security (not executing tons of random code), privacy (multiple fingerprinting vectors stop working) and performance (pages load extremely fast). Some websites are adopting javascript-only client-side rendering, which has an unfortunate side effect of preventing web archives from taking snapshots (and making sites less accountable). Other crypto sites that are doing this are [Brave New Coin](https://bravenewcoin.com/) and [The Block](https://www.theblockcrypto.com/).

U.S. Fed [announced](https://www.newyorkfed.org/markets/opolicy/operating_policy_191114) that they will expand their market interventions by offering 42-day "repos" (loans of sorts), in addition to 1-day and 14-day repos that started in September and "purchases" of Treasury bills that started in October. If you ever wonder who is getting these loans, you will have to wait [two years](http://gata.org/node/19583) for disclosure.

U.S. companies are [stacking up cash](https://www.axios.com/businesses-spending-indicators-recession-533481fc-dba7-4b5c-add4-c11628c335bc.html) to prepare for an economic downturn. A notable quote from the Axios story: "Data from the Investment Company Institute shows that even though the stock market has risen by nearly 25% this year, investors have been net sellers of stocks, pulling $100 billion out of equity funds". A Zero Hedge [article](https://www.zerohedge.com/markets/conundrum-2019-equity-outflows-are-biggest-ever-yet-stocks-are-all-time-highs-what-happens) shows a weird phenomenon of money flowing out of equities yet the prices setting new ATHs. How? Some factors making it possible are the companies themselves being the biggest buyers via stock buybacks, central banks creating money that flows into stocks, paired with a simultaneous decline of trading volume.

The "fun" part in these dynamics where investors are [moving to cash](https://www.bloomberg.com/news/articles/2019-11-12/world-s-rich-readying-for-major-stock-sell-off-ubs-wealth-says) is that while it saves their value from more risky assets and negative interest rates, it will still be diluted by creation of fiat money that is [almost impossible](https://www.home.saxo/en-hk/insights/content-hub/articles/2019/11/20/investing-themes-to-watch-over-the-next-decade) to stop now.

The Fed itself [admitted](https://realinvestmentadvice.com/powells-fantasy-the-economy-should-grow-faster-than-debt/) that U.S. national debt growing faster than the economy is "not sustainable", shortly after the debt [exceeded](https://cointelegraph.com/news/united-states-national-debt-hits-23-trillion-over-1m-per-bitcoin) $23 trillion.

Global debt is hitting all-time highs. The numbers vary by the source: $188 trillion and 230% of the world output figure comes from [IMF chief](https://www.ibtimes.com/global-debt-surges-record-high-188-tn-imf-chief-2861715), while $250 trillion and 320% of world output figure is from [Axios](https://www.axios.com/capital-markets-eye-world-soaring-debt-400f9f37-46b5-45ad-9487-c09ba8958c09.html), which cited the Institute of International Finance.

Certain physical security providers report an increased [demand](https://www.bloomberg.com/news/articles/2019-11-20/world-s-rich-are-rattled-and-looking-for-old-fashioned-security) for safe deposit boxes to store precious metals, cash and cryptocurrency. The motives cited are fears of a global recession, avoidance of negative interest rates and natural disasters.

Several U.S. organizations acted in concert to "deflate the bitcoin bubble of 2017" according to a CoinDesk [story](https://www.coindesk.com/trump-administration-popped-2017-bitcoin-bubble-ex-cftc-chair-says) _(missed in October)_. "One of the untold stories of the past few years is that the CFTC, the Treasury, the SEC and the \[National Economic Council\] director at the time, Gary Cohn, believed that the launch of bitcoin futures would have the impact of popping the bitcoin bubble. And it worked". While the move is presented as helping the market by "popping the bubble", giving traders the ability to "express a pessimistic view" even if they _don't own_ the asset, and preventing "believer's market", it somewhat reminds of the smart use of futures [in 1974](http://www.gata.org/node/17081) to increase volatility of gold and discourage people from holding it.

Czech Central Bank forbids the use of the word "coin" and is [prepared](https://www.bitcoininsider.org/article/77479/czech-central-bank-prepares-fine-calling-physical-bitcoins-coins) to fine a company that is calling physical coins containing Bitcoin paper wallets with 0.1 BTC "mince" ("coin" in Czech).

A law has been [passed](https://www.theblockcrypto.com/linked/48738/with-parliament-approval-german-banks-to-sell-and-custody-crypto-in-2020) by the German parliament which will allow banks to sell and custody cryptocurrencies from Jan 1 2020, subject to the required licenses.

During October [protests](https://twitter.com/dalalmawad/status/1186705664229466112) in Lebanon the banks were [closed](https://www.cnbc.com/2019/10/23/lebanon-protests-fears-of-a-cash-crisis-as-banks-remain-shut.html) for two weeks for safety reasons. Upon reopening on Nov 1, capital controls were [established](https://www.counterpunch.org/2019/11/07/how-unofficial-capital-controls-stopped-a-run-on-the-banks-in-lebanon/) limiting daily withdrawals and transfers abroad.

GitHub has [removed](https://techcrunch.com/2019/10/30/github-removes-tsunami-democratics-apk-after-a-takedown-order-from-spain/) the APK of an app for organizing protests in Catalonia, acting on a court takedown request sent by Spain's national police force.

The CEO of Mongolia-based IDAX exchange has [disappeared](https://idax.zendesk.com/hc/en-us/articles/360037327571-Urgent-announcement-about-current-situation-of-IDAX-Global) together with the keys for the exchange's cold storage. Five days prior to that the exchange announced withdrawal [problems](https://idax.zendesk.com/hc/en-us/articles/360036736211-Announcement-of-IDAX-withdrawal-channel-congestion) and that it will no longer serve users in [China](https://idax.zendesk.com/hc/en-us/articles/360036736691-IDAX-no-longer-provide-services-for-users-in-China). This is reminiscent of the case of Canadian QuadrigaCX whose keys also mysteriously disappeared along with the CEO. The takeaways here are: have several backup people with the keys if you run an important service, screen your exchanges and ideally, contribute to replacing custodial exchanges with [non-custodial](https://github.com/decred/dcrdex) ones.

A trojan-enabled version of Tor browser was [targeting](https://www.welivesecurity.com/2019/10/18/fleecing-onion-trojanized-tor-browser/) Bitcoin users, discovered by ESET. The trojan version was spreading from `tor-browser[.]org` and `torproect[.]org` domains.

The prominent getmonero.org site was [compromised](https://arstechnica.com/information-technology/2019/11/official-monero-website-is-hacked-to-deliver-currency-stealing-malware/) and wallet binaries were replaced with malicious code. The issue was identified by a user who checked the signature and found it didn't match, then promptly [fixed](https://web.getmonero.org/2019/11/19/warning-compromised-binaries.html) by the Monero team. At least one user reported losing funds.

A fake Zcash wallet was [distributed](https://twitter.com/mineZcash/status/1185908172105453568) through a github.su domain. (_missed in Oct_)

Another fake Decred wallet was noticed, reported and quickly removed by GitHub. The account named `decreds` and the way the fake [v1.5.0 release](https://archive.today/ivVRO) was published looked similar to previous "v1.5.0 Mandatory Update" by `DecredCoin` covered in [September](201909.md). It feels like hackers can't wait for v1.5 final release _(we too!)_. If you encounter anything like this on GitHub or elsewhere, please report it to the platform immediately and notify the community to minimize possible damage.

If you couldn't upload enough of your data to Google, it is [planning](https://www.cnbc.com/2019/11/13/google-reportedly-offering-checking-accounts-next-year.html) to enter the banking business and offer checking accounts next year. Project codename "Cache" is a bit ironic because in computing [caches](https://en.wikipedia.org/wiki/Cache_%28computing%29) are often wiped.

## About This Issue

This is issue 20 of Decred Journal. Index of all issues, mirrors and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, Ditto Team, Dustorf, elian, richardred, s\_ben
- reviews and feedback: akinsawyerr, chappjc, davecgh, kyle, lukebp, matheusd, Haon, emiliomann
- title image: saender

