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

- [Cointelegraph](https://cointelegraph.com/news/secrets-they-missed-at-devcon-what-its-really-like-in-a-working-dao)中 @ jy-p的一篇文章，标题为“他们在DevCon上错过的秘密：在工作中的DAO中的真实情况”。
- 与David Nage在基础层播客上的@jy-p[播客](https://podcasts.apple.com/us/podcast/base-layer-episode-086-jake-yocom-piatt-decred/id1445373535?i=1000457565007)。
- 《福布斯》上的一篇[文章](https://www.forbes.com/sites/cbovaird/2019/11/11/who-will-win-the-race-for-digital-currency-supremacy/)，以@ jy-p的评论为特色，阐述了政府，企业与分散式加密货币之间的竞争，以重塑金融体系。
- 在Market Disruptors播客上协调@ jy-p 的[采访](https://cryptotradernews.com/technology/our-data-privacy-is-under-attack-decred-is-fighting-back/)。
- @akinsawyerr和拉斯维加斯世界密码会议上的Nakamoto新闻网络之间的[采访](https://www.youtube.com/watch?v=4r6z9JZxRRI)。
- 在Messari的有关开发者资金，治理和Decred的无条件意见播客中，对@ jy-p 的[采访](https://messari.io/podcast/developer-funding-governance-and-the-evolution-of-decred-with-jake-yocom-piat)。
- BlockTV上的[电视节目](https://blocktv.com/watch/2019-10-30/5db9ab4487a7e-resolving-corporate-governance-in-cryptocurrency)介绍了如何解决加密货币中的公司治理问题。
orporate governance in cryptocurrency.

其它:

- @liz_bagot出现在Decred in Depth 播客中，[谈论](https://podcasts.apple.com/us/podcast/liz-bagot-pr-marketing/id1466716734?i=1000455667566)Ditto与Decred的合作。
- 支持Decred在Web Summit上的媒体参与。获得了BBC的采访，并促进了与CoinDesk和Cointelegraph的会议。我们还为Decred团队制作了一本顶级新闻工作者的简报，以便与他交谈并帮助@ moo31337为他的小组讨论做准备，以最大程度地提高他们在活动中的影响力。
- 通过与Legacy Research，Nakamoto News Network，Crypto TV News等媒体进行现场采访，支持@akinsawyerr出席在拉斯维加斯举行的世界加密货币会议。
- 为各个社区成员获得了几个播客和在线采访。
- 为社区确定和共享机会，与Crypto Twitter互动并向外界宣传Decred。
- 紧密合作以支持Decred开发人员社区在过去一年中取得的成就。

@bee撰写了要探索的[营销策略概述](https://xaur.github.io/writings/posts/20191127-marketing-strategies.html)。一些关键主题是改善报告，使用“金钱”一词，促进DCR实际用于小费，捐赠和资助项目，将DCR推向高度团结的社区和个人，以作为转移价值的方式，并提高社交媒体的影响力。（Reddit）

## 活动

参加:

- 11月4日至7日- [Web Summit](https://websummit.com/) -葡萄牙里斯本。Decred团队获得了2天的[展位](https://twitter.com/marco_peereboom/status/1191651269640888320)。极少数区块链项目可能会由于熊市而获得发言权。@ moo31337 谈到在舞台上的话题金融业的代表“你真的相信你的银行？”。（照片：[1](https://twitter.com/JamieHoldstock/status/1191760511878279168), [2](https://twitter.com/NoahPierau/status/1192056049764904960), [3](https://twitter.com/kakalordao/status/1192131145141555201), [4](https://twitter.com/marco_peereboom/status/1192990143822454784)）
- 11月6日- [Decred Meetup](https://twitter.com/amxromero/status/1192241858816217089) -哥伦比亚麦德林。@elian和@victorarubin与大约40位20-50岁的人进行了交谈，他们询问了有关Politeia，Decred的Latam计划，PoS攻击媒介和智能合约的惊人问题。（[报告](https://github.com/decredcommunity/events/blob/master/reports/20191106-decred-meetup-medellin-colombia.md)）
- 11月7日- [Journey 4.0](https://twitter.com/legal_medellin/status/1189918302061187073)-哥伦比亚麦德林。@elian受法律黑客麦德林（Legal HackersMedellín）邀请，在哥伦比亚最大的工商管理大学EAFIT大学谈论区块链技术对国际法的挑战。学生对DAO的概念很感兴趣，因为DAO的概念无处不在，并且不太适合传统的法律框架。([报告](https://github.com/decredcommunity/events/blob/master/reports/20191107-journey-4-medellin-colombia.md))
- 11月8日- [World Blockchain Conference](https://www.8btc.com/wbc-2019/) -中国嘉兴。@Dominic代表Decred，并谈到了DAO和隐私功能。有报道说他在活动前的聚会上被变成了[机器人](https://twitter.com/wanbihou/status/1192484367626424321)。建议该地区的社区成员遵循标准协议并采取必要的预防措施。机器人[舞蹈](https://twitter.com/wanbihou/status/1193154668601327617)的录像带泄漏并引发了 [#DecredDanceChallenge](https://twitter.com/hashtag/DecredDanceChallenge)。（照片：[1](https://twitter.com/wanbihou/status/1192806081568722944), [2](https://twitter.com/wanbihou/status/1193218449721311233)）
- 11月15日- [Open Banking, Fintech and Blockchain Summit](https://twitter.com/Decred_ES/status/1195025379255144448) 。@elian被邀请谈论数字身份。在小组讨论中，他简要介绍了Decred以及个人数据的安全性和隐私性的重要性，并指出了便利性（“忘记密码？”按钮）和自我主权提供的控制权之间的挑战性折衷。（[报告](https://github.com/decredcommunity/events/blob/master/reports/20191115-open-banking-summit-mexico-city-mexico.md)）
- 11月15日至16日-[CriptoBlock](https://criptoblock.com.br/)-巴西圣保罗。@Rhama和@girino发表了关于Decred的演讲。尽管组织者努力工作，但在预期的1,000-1,200人中，只有大约250人参加，反映了当今的市场。Decred是铜牌赞助商。
- 11月21日- [Africa Blockchain Summit](https://www.africablockchainsummit.com/agenda.html) -摩洛哥拉巴特。@arij借此机会发现了集中组织的观点，并代表Decred代表了来自不同背景的各种各样的人。（[报告](https://github.com/decredcommunity/events/blob/master/reports/20191121-africa-blockchain-summit-rabat-morocco.md)）
- 11月21日- [Africa Fintech Summit](https://africafintechsummit.com/addis/) -埃塞俄比亚亚的斯亚贝巴。@akinsawyerr在区块链面板上发表了[讲话](https://www.youtube.com/watch?v=WOqCjQELpao)，并建立了一些宝贵的交流。一周后，他说话关于Decred和@VOANews的旅程。[报告](https://github.com/decredcommunity/events/blob/master/reports/20191121-africa-fintech-summit-addis-ababa-ethiopia.md)
- 11月21日- [Blockchain Conference](https://www.eventbrite.com.ar/e/conferencia-blockchain-tickets-81397410847) -墨西哥韦拉克鲁斯。该活动在城市最大的科技大学举行。@francov_和@luisantoniocrag向学生介绍了区块链，比特币和Decred，并挑战了一些老师的法定信念。（[报告](https://github.com/decredcommunity/events/blob/master/reports/20191121-blockchain-and-decred-veracruz-mexico.md)）
- 11月30日- [Decred Meetup](https://twitter.com/RodgersJabz/status/1194309441774063617) -乌干达坎帕拉。@jabz的团队向Decred的53位观众进行了介绍，并介绍了其功能，并举行了实际会议，展示了如何使用钱包。[报告](https://github.com/decredcommunity/events/blob/master/reports/20191130-decred-meetup-kampala-uganda.md)。

即将到来:

- 12月12日至13日-Labitconf-乌拉圭蒙得维的亚。Decred的团队成员将出席拉丁美洲最大的加密货币和区块链会议。
- 1月7日- [Digital Money Forum](https://thedigitalmoneyforum.com/) -美国拉斯维加斯。该活动是2020年CES的一部分。@ akinsawyerr将在有关未来经济的会议上发言。
- 1月29日至31日- 加密101在线峰会 -网络。@lukebp将概述Decred的2020年计划。
- 4月13日至17日-墨西哥瓜达拉哈拉Talent Land的区块链土地。Decred将成为Talent Land的赞助商，并在Blockchain Land的展位上出席。
- 越南比特币社区成立5周年纪念活动。详情待定。

## 媒体

精选文章：

- @matheusd的LN和多所有者选票 ([blog.decred.org](https://blog.decred.org/2019/11/11/LN-Multi-Owner-Tickets/))
- 由@richardred([blockcommons.red](https://blockcommons.org/post/crypto-commons/))介绍“加密货币共同体上的对等生产”
- 谁将赢得数字货币霸权竞赛？由Charles Bovaird（[forbes](https://www.forbes.com/sites/cbovaird/2019/11/11/who-will-win-the-race-for-digital-currency-supremacy/), [tweet](https://twitter.com/ForbesCrypto/status/1193953360422080512)）-功能@ jy-p引号
- Decred的名字很烂，但我喜欢！由@Dustorf([medium](https://medium.com/@dlefebvr/decreds-name-sucks-and-i-m-glad-853af487034e))
- 什么是Decred（DCR）？为什么创建这种加密货币？通过@Haon([medium](https://medium.com/@NoahPierau/what-is-decred-dcr-why-was-this-cryptocurrency-created-4e5cae085bc7))-常见问题解答
- 他们在DevCon上错过的秘密：@ jy-p([cointelegraph.com](https://cointelegraph.com/news/secrets-they-missed-at-devcon-what-its-really-like-in-a-working-dao))在工作中的DAO中的真实情况
- Decred: @ammarooni的经济突破([medium](https://medium.com/@Ammarooni/decred-an-economic-breakthrough-4d2e3ea27338))
- 我们的数据隐私受到攻击：Matthew Harris（Decred正在反击）([cryptotradernews.com](https://cryptotradernews.com/technology/our-data-privacy-is-under-attack-decred-is-fighting-back/))
- CTN独家新闻：Matthew Harris（共同创始人Jake Yocom-Piatt ）的内部观点([cryptotradernews.com](https://cryptotradernews.com/cryptocurrency/ctn-exclusive-inside-decred-with-co-founder-jake-yocom-piat/))
- Decred,高度安全的，不可伪造的SOV @Checkmate([medium](https://medium.com/@_Checkmatey_/decred-hypersecure-unforgeably-scarce-e076b91a2be))
- BlackBearXVII的Decred X系列继续进行：
  - Decred X / Part VI - Triune of Trust ([medium](https://medium.com/@imagnusholdings/decred-x-part-vi-triune-of-trust-3fa7ad1476a5))
  - Decred X / Part VII - Field Manual A ([medium](https://medium.com/@imagnusholdings/decred-x-part-vii-field-manual-a-68306f23d2ca))
  - Decred X / Part VIII - Silver Linings Field Manual B ([medium](https://medium.com/@imagnusholdings/decred-x-part-viii-silver-linings-field-manual-b-d38cb0e6e17c))
  - Decred X / Part IX - Sub Economics ([medium](https://medium.com/@imagnusholdings/decred-x-part-ix-sub-economics-e3b0a5e948e1))

翻译:

- Decred Journal 2019年11月被翻译成阿拉伯语（@arij），中文（@Dominic），波兰语（@kozel）和西班牙语（@francov_和@luisantoniocrag）。感谢您保持更新！

视频:

- 利用Decred的Jake Yocom-Piatt在Messari的无保留意见([player.fm](https://player.fm/series/messaris-unqualified-opinions/building-a-store-of-value-with-decreds-jake-yocom-piatt), [apple](https://podcasts.apple.com/us/podcast/building-a-store-of-value-with-decreds-jake-yocom-piatt/id1455666979?i=1000457903445))上建立价值存储-实时流观众([youtube](https://www.youtube.com/watch?v=LMJp8rKLkkM)) 被@ jy-p视为天使般的表演，回答有关Decred的历史和方法的有趣问题。
- Decred Assembly Deep Dive@davecgh([youtube](https://www.youtube.com/watch?v=gGQuY0kOt7g))-深入讨论共识规则和v1.5.0 RC1。
- Digit-有关@akinsawyerr的Decred的所有剧集([youtube](https://www.youtube.com/watch?v=4r6z9JZxRRI))
- Decred Review: 为什么DCR值得关注！([youtube](https://www.youtube.com/watch?v=elfBK5QBVmo))
- Coinbase列表为什么Decred过期了@Exitus([youtube](https://www.youtube.com/watch?v=Og3kGX_fYho), discussed on [reddit]
- 您真的可以信任您的银行吗？([vimeo](https://vimeo.com/375884648)) - @ moo31337功能在网络峰会的面板。@Exitus([1](https://www.youtube.com/watch?v=0Bq48X3cO_s), [2](https://twitter.com/coveryfire7777/status/1199866746192171010))

音频:

- Base Layer Episode 086 - Jake Yocom Piatt (Decred) ([podbean](https://www.podbean.com/media/share/pb-9ah38-c88678), [spotify](https://open.spotify.com/episode/4vMtWg6lejqR9pfKkmsgXc))
- 市场颠覆者：在区块链上发展隐私权 Jake Yocom-Piatt ([anchor.fm](https://anchor.fm/markmoss/episodes/Developing-Privacy-On-The-Blockchain-With-Jake-Yocom-e934qv), [stitcher](https://www.stitcher.com/podcast/anchor-podcasts/market-disruptors/e/65439848))
- Decred in Depth Ep. 12 - @akinsawyerr 谈论[#cryptocurrency](https://twitter.com/hashtag/cryptocurrency)中的不透明治理，这是新进入者的障碍，Decred阐明了规则，以及非洲无障碍信任最小化全球支付所提供的机会。([libsyn](https://decredindepth.libsyn.com/akin-sawyerr-dcr-africa-governance), [soundcloud](https://soundcloud.com/decredindepth/ep-12-akin-sawyerr-dcr-africa-governance))
- Decred in Depth Ep. 13 - @richardred 关于促进Decred，研究blockchain治理，写作会谈[cryptocommons.cc](https://cryptocommons.cc)，并选择保持匿名的。([libsyn](https://decredindepth.libsyn.com/richard-red-dcr-research-politeia-mm-proposal), [soundcloud](https://soundcloud.com/decredindepth/ep-13-richard-red-dcr-research-politeia-mm-proposal))

LunarCRUSH分享了几张[图表](https://twitter.com/LunarCRUSH/status/1191017614971027458)，这些图表将价格和数量等基本市场数据与社交媒体上Decred的市场情绪分析相结合。

## 社区讨论

选定的Reddit帖子：

- nnnko56 [回答](https://www.reddit.com/r/decred/comments/e2yiou/what_happens_when_we_reach_max_supply/) 问题：“当我们达到最大供应量时会发生什么？”
- [Decentralized Credits](https://www.reddit.com/r/decred/comments/dqocpf/decentralized_credits/), and [Tacotime Trilogy](https://www.reddit.com/r/decred/comments/dznwsr/tacotime_trilogy/), paintings by @AGNFAB1 on [Twitter](https://twitter.com/AGNFAB1/status/1197455821380243457).

Twitter精选内容：

- @DCRtheSOV's intro to DCR [tweet](https://twitter.com/DCRtheSOV/status/1191215059680149505) thread
- @DCRtheSOV's 的十月进度月度[回顾](https://twitter.com/DCRtheSOV/status/1194480106892185601)。
- @karamble的Raspberry Pi 的Decred[仪表板](https://twitter.com/karamblez/status/1197676296240861186)广受好评。
- @dcrstakey又[回来了](https://twitter.com/dcrstakey/status/1193758944587657216)。 
- #DecredDanceChallenge是在中国由穿着著名Decred太空夹克的人的机械舞动作发起的。亮点包括：[@Dustorf/Stakey](https://twitter.com/lefebvre_dustin/status/1195107934839230465), [@karamble](https://twitter.com/karamblez/status/1194664973030641664), [@Camilolwi](https://twitter.com/Camilolwi/status/1194358146027814912), [@JeonHaWoo2](https://twitter.com/JeonHaWoo2/status/1194389449062469634), [@treyditto](https://twitter.com/treyditto/status/1194351696522158080), [@liz_bagot](https://twitter.com/liz_bagot/status/1194393447035224065), [@elian](https://twitter.com/elianhuesca/status/1196526382970540032), [@Francov99_](https://twitter.com/Francov99_/status/1194410868001382401), [@s_ben](https://twitter.com/zen_bacon/status/1194756298987855872), [@luisantoniocrag](https://twitter.com/luisantoniocrag/status/1194438312678887425) 和 [@degeri](https://twitter.com/degeri_crypto/status/1194522586417225728).
- DCRComic发挥您的才能，享受DAO [tweet](https://twitter.com/DCRComic/status/1199325669055979520)。
- @jholdstock [会见](https://twitter.com/JamieHoldstock/status/1192146283835854849)葡萄牙总理。
- @Checkmate [推文](https://twitter.com/_Checkmatey_/status/1197225489959718913) 对Decred安全性的影响。
- @permabullnino 关于降低竞争护城河的[推文](https://twitter.com/PermabullNino/status/1195356846778912769) 。
- Jesse Walden [tweet](https://twitter.com/jessewldn/status/1194632275389898753) about the Politeia one year report.
- @lukebp [推文](https://twitter.com/lukebp_/status/1199134933773500416)介绍了为Decred开发的内容，并与许多其他人一起开始了#cryptodevs主题标签，添加了他们对为Decred工作的感觉的观点。

> - 与世界一流的团队合作
> - 建立最先进的开源技术
> - 随时随地工作
> - 异步通信（无会议！）
> - 设置自己的工作时间（兼职或全职）

## 市场表现

11月DCR交易价格在15.68-24.73美元/ BTC 0.0020-0.0029之间。每日平均价格为$ 19.97。

## 相关外部信息

Coinbase发表后有关战俘的安全性，概述了其立场，即有利的是，安全是硬币由硬件开采，也是它的主要用途（即ASIC），以及，制造业和所有权的多样性以及由ASIC友好型算法服务。

MicroBT的首席执行官（Whatsminer D1的制造商，Whatsminer D1是当前最大的Decred矿工之一）在中国深圳因采矿专利侵权被捕。

Zcash实现中的一个错误泄漏了元数据，并允许攻击者将IP地址链接到Zcash屏蔽的地址（十月份未提供）。来自发现它的开发人员：“所有使用zaddrs并与第三方共享zaddrs的人。（...）考虑与您的zaddr相关的与您相关的IP地址和地理位置信息”。该漏洞是从Bitcoin Core代码库复制的，并于2016年在Zcash中引入。此漏洞已在v2.0.7-3中修复，尽管该安全公告只是建议立即升级而无需任何细节。许多继承Zcash代码的项目也受到影响。这表明隐私技术非常微妙，需要简单，健壮的编程方法以及极其彻底的审查和测试。

Zcash基金会和ECC 就如何处理Zcash商标达成了协议。这已移交给基金会，并达成协议，由它与ECC共同拥有执行商标的双边权力。CoinDesk的这篇文章解释了争议不仅仅是徽标，还有商标持有人有效决定哪条链是Zcash的权力。

Decred增加了另一个维度，即选民确定了链条的合法性，而少数派则受到极大的激励，需要克服很多挑战。即使有人试图窃取Decred的“商标”，也不应对原始链是什么感到困惑，因为选民正在每个区块上签名。另外，Decred对“谁在招聘开发人员？到底是什么”社区有一个非常明确的答案。-利益相关者。

ZEC商标问题的解决使NU4的投票得以进行，Zcash生态系统/社区可以表示支持13种资助发展的方案。ECC和Zcash基金会在决定采用哪种计划时，将考虑3种或4种不同轮询方法的结果。

阿拉贡（Aragon）完成了第四轮AGP投票，投票了15份提案，而ANT的参与率约为3-18％。在批准的提案中，有AGP-103，该提案将每个季度投票周期的网络预算上限设为国债价值的5％或250,000 DAI（以较高者为准）。待批准的最大提案（投票率为9％，批准率为91％）是AGP-106，用于开发和启动Aragon Chain，费用为50万美元。目的是创建一个新的第1层协议，并将其作为基于以太坊的Aragon网络的替代方案。提到的原因之一是跟上以太坊网络变化的变化而增加的成本。AGP-112，也通过了，发布了一项声明，声明Aragon反对以太坊上的ProgPoW，或者以太坊2.0之前对挖掘算法进行的任何其他非紧急更改。投票率最高的提案是AGP-81，其中有17％的ANT对与Kleros在法院系统上的合作投反对票。

阿拉贡法院在主网上启动，它是一个用于裁定“无法通过智能合约解决的主观争议”的系统。ANT持有人可以将其令牌放到ANJ令牌上，然后再放到法庭上审理的案件中。通过Schelling游戏做出决定，那些猜出多数决定的人将得到奖励，而猜错了的人则被削减了赌注。成为ANJ陪审员的注册将于2020年1月开始。

Dragonfly Research发表了一篇有关通过实时监视网络来“破坏Mimblewimble的隐私模型” 的文章。@ jy-p已在审查隐私解决方案时发现了此问题，随后在基础层播客上对其进行了讨论。一位Grin开发人员回复了这篇文章，指出它引起了人们的注意，并且不构成攻击。

宣布了 “未知基金” ，承诺向直接或间接支持匿名概念的初创公司投资并向比特币捐赠7500万美元。“将优先考虑以下领域：个人数据保护，匿名工具，加密货币和区块链”。该基金非常不透明，只说“未知基金的申请截止。评估将需要几个月时间”。人们开始询问这是否可能是骗局。

恒星开发基金会（SDF）宣布已烧毁 550亿XLM，总价值超过44亿美元（名义上），占XLM总量的50％以上。陈述的理由是相信基金会可以用更少的资金实现其目标，并且大规模的空投活动被证明是无效的。

由于与空投程序（EIDOS）相关的交易激增，EOS区块链进入 “拥塞模式”，在某一阶段，该程序占所有EOS交易的95％。一个影响是，在空投需求减少或其CPU租约在30天到期之前，拥有较少EOS的用户无法进行交易。另一个影响是网络上的CPU时间成本激增了100,000％。

Block.One 宣布将开始以其所控制的9.5％的EOS开始对区块生产者进行投票-将自己归类为“小型但重要的EOS代币持有者”。Block.One尚未宣布他们将如何投票。

纽约EOS 发推文揭示了一个事实，即6个注册的EOS BP似乎由同一实体运营。尽管所讨论的BP 不在前21个活动BP中，但是它们经常作为备用BP获得奖励。

/ r / EthTrader的以太坊上的Donuts实验正在链上过渡到Aragon DAO。Subreddit成员从11月15日开始有2个星期的时间来申请其甜甜圈。正如先前的问题所述，/ r / EthTrader社区在处理甜甜圈分散化的方式上已经四分五裂。

特隆（Tron）的贾斯汀·孙（Justin Sun）透露，他是收购Poloniex交易所的一个投资者团体的成员。11月中旬，Poloniex在TRX上市，并与TRX和后来的TRC20-USDT进行了“存款竞争” 。本月晚些时候，宣布 Poloniex已收购了基于TRON的DEX TRXMarket，并更名为Poloni DEX，以提供去中心化交易。几天后的Poloniex Twitter帐户啾啾 “让我们买#TRON”，但这种鸣叫是不久之后删除。

不幸的是，BitMEX 通过使用cc而不是密件抄送给所有人发送电子邮件，泄漏了他们的电子邮件数据库。哎呀。这导致以用户为目标，向有恶意的当事方透露其身份的一方面。

韩国OKEx和Upbit宣布从Monero，Zcash，Dash等私密货币中除名，尽管DASH和ZEC的除名被暂停以等待OKEx 的审查。（9月和10月错过）

Bittrex已采用 Chainalysis 知道您的交易软件，该软件可实时监控15个加密资产的可疑活动。（9月错过）

除非启用了javascript和某些浏览器功能，否则观察到CoinDesk的页面不会显示，如10月和11月缺少快照所证明的。禁用javascript的原因是：大大提高了安全性（不执行大量随机代码），隐私（多个指纹向量停止工作）和性能（页面加载非常快）。一些网站正在采用纯JavaScript的客户端渲染，这带来了不幸的副作用，即阻止了Web存档获取快照（并降低了站点的责任感）。其他这样做的加密站点是Brave New Coin和The Block。

美联储宣布，除9月开始的1天和14天回购以及10月开始的“购买”国库券外，他们还将通过提供42天的“回购”（各种贷款）来扩展市场干预。 。如果您想知道谁获得了这些贷款，则必须等待两年才能披露。

美国公司正在积累现金以为经济下滑做好准备。Axios故事中的一个引人注目的引述是：“来自投资公司协会的数据显示，即使今年股市上涨了近25％，投资者还是股票的净卖家，从股票基金中撤出了1000亿美元”。零对冲文章显示了一种奇怪的现象，即资金从股票中流出，而价格却设定了新的ATH。怎么样？一些可能的因素使得公司本身通过股票回购成为最大的买家，中央银行创造了流入股票的资金，同时交易量同时下降。

在这些动态中，投资者转向现金的“乐趣”部分是，尽管它从更具风险的资产和负利率中节省了价值，但仍将被创造法定货币所稀释，这几乎是现在无法阻止的。

美联储本身承认，在债务超过 23万亿美元后不久，美国国债的增长速度就超过了经济增长的速度“是不可持续的” 。

全球债务创历史新高。这些数字因来源而异：188万亿美元和世界产出数字的230％来自IMF，而250万亿美元和世界产出数字的320％来自Axios，后者引用了国际金融学院的话。

某些物理安全提供商报告对用于存储贵金属，现金和加密货币的保险箱的需求增加。所提及的动机是担心全球经济衰退，避免负利率和自然灾害。

根据CoinDesk的故事 （10月缺失），几个美国组织共同行动以“缩小2017年的比特币泡沫” 。“过去几年的一个不为人知的故事是，CFTC，财政部，SEC和当时的[国家经济委员会]主任加里·科恩（Gary Cohn）相信，比特币期货的推出将对市场产生冲击。比特币泡沫。它奏效了。” 虽然此举被认为是通过“消除泡沫”来帮助市场，但使交易者即使不拥有资产也能“表达悲观的看法” ，并防止“信徒的市场”，

捷克中央银行禁止使用“硬币”一词，并准备罚款一家公司，该公司要求将包含带有0.1 BTC“切碎”的比特币纸钱包的实物硬币（捷克语中为“ coin”）。

德国议会通过了一项法律，该法律允许银行自2020年1月1日起根据要求的许可证出售和托管加密货币。

十月在黎巴嫩举行抗议活动时，出于安全原因，银行关闭了两个星期。在11月1日重新开放后，建立了资本管制措施，限制了每日提款和向国外转移的资金。

GitHub 删除了用于组织加泰罗尼亚抗议活动的应用程序的APK，该应用程序是根据西班牙国家警察部队发出的法院下架请求执行的。

总部位于蒙古的IDAX交易所的首席执行官与交易所冷库的钥匙一起消失了。在此之前的五天，交易所宣布退出问题，它将不再为中国用户提供服务。这让人想起加拿大QuadrigaCX案，该案的密钥也随着首席执行官一起神秘地消失了。这里的要点是：如果您运行一项重要的服务，请有几个备用人员带钥匙，对您的交易所进行筛选，并且在理想情况下，有助于用非托管交易所代替托管交易所。

ESET发现了一种启用了Trojan的木马版本的Tor浏览器，以比特币用户为目标。特洛伊木马版本从tor-browser[.]org和传播torproect[.]org。

著名的getmonero.org网站遭到破坏，钱包二进制文件已替换为恶意代码。用户检查了签名并发现签名不匹配，从而确定了该问题，然后由Monero团队迅速修复。至少一个用户报告资金损失。

假的Zcash钱包是通过github.su域分发的。（十月错过）

GitHub注意到了另一个虚假的Decred钱包，并迅速将其删除。该帐户的名称decreds以及虚假v1.5.0发行版的发布方式与9月DecredCoin涵盖的以前的“ v1.5.0强制更新”相似。感觉就像黑客迫不及待想要v1.5最终版本（我们也是！）。如果您在GitHub或其他地方遇到类似情况，请立即将其报告给平台，并通知社区以最大程度地减少可能的损害。

如果您无法将足够多的数据上传到Google，它计划在明年进入银行业务并提供支票帐户。项目代号“缓存”有点讽刺意味，因为在计算中经常会擦除缓存。

## 关于月报

这是Decred Journal的第20期。有关所有问题，镜像和翻译的索引，请参见 [此处](https://xaur.github.io/decred-news/)。

在经过最少的健全性检查之后，来自第三方的大多数信息都会直接从来源中继。Decred Journal的作者无权验证所有声明。请当心诈骗，并自行进行调查。

我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢(字母排列):

- 写作和编辑: bee, Ditto Team, Dustorf, elian, richardred, s\_ben
- 评论和反馈: akinsawyerr, chappjc, davecgh, kyle, lukebp, matheusd, Haon, emiliomann
- 标题图片: saender

## 中文社区

* [社区web](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [优酷频道](https://i.youku.com/decredproject)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)
