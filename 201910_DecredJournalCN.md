# Decred月报 - 2019年10月

![abstract art](img/journal-201910-384.png)

_图片: Source Relay by @saender_

十月重点:

- 核心软件v1.5的RC1版本已准备好进行测试。主要更改包括：增加共识规则更改投票模块，以增加区块头承诺；挖矿基础设施（dcrd），隐私保护（dcrwallet），闪电网络集成和UI调整（Decrediton）以及移植大量的上游更新（dcrlnd）。
- i2 Trading在提案通过之后，已开始在3个交易所（4个交易对）上提供流动性。
- 重新设计的Politeia前端已上线。它具有与其他Decred软件相同风格的新外观，并优化提升了性能。
- 10月是Decred参加活动的忙碌月份，世界各地的社区成员都代表Decred组织或参加各种活动。
- 10月，三个活跃的研究计划也发表了，第四个已在11月初获得批准。关于Politeia第一年（周年纪念日为10月16日），也发布了许多文章在其他媒体。

## 新的链上共识投票要来了!

核新软件v1.5即将进行更改共识规则的投票。候选二进制文件现在已 [可使用](https://github.com/decred/decred-binaries/releases/tag/v1.5.0-rc1)，最终正式版将随之发布。

请通过升级软件为您的solo选票或VSP选票设置准备投票。

您可以访问追踪在dcrdata的[议程](https://explorer.dcrdata.org/agendas)页面，或在[voting.decred.org](https://voting.decred.org/)查看详情。

让我们为Decred的未来选择方向吧！

## v1.5 RC1版本

dcrd、dcrwallet、Decrediton和dcrlnd的候选版本已可用于测试。以下是其发布说明中的重点内容。

**dcrd v1.5**

区块头承诺已实现，等待成功的链上投票准备激活。升级到v1.5后，利益相关者可以通过其钱包或投票服务提供商（VSP）网站设置投票偏好。此更改的主要目标是提高轻节点客户端（SPV）的安全性和效率，例如SPV模式下的Decrediton和dcrandroid / dcrios移动钱包。它还将添加基础设施，为将来的一些可伸缩性增强铺平道路。可以从资助该工作的[Politeia提案](https://proposals.decred.org/proposals/0a1ff846ec271184ea4e3a921a3ccd8d478f69948b984445ee1852f272d54c58)中找到有关变更的高级概述。

新的区块过滤器已实现。为这些轻节点客户端（例如SPV钱包）提高效率，人体工程学以及包含其它信息，例如完整的选票承诺脚本。新的区块过滤器为版本2。较旧的版本1过滤器现已弃用，并计划在下一个版本中删除，因此，用户应尽快更新到新的过滤器。请注意，有一个一次性的数据库更新来为所有现有的历史区块构建和存储新的过滤器，这可能需要一段时间才能完成（通常在HDD上大约8到10分钟，在SSD上大约4到5分钟）。

用于构建模块模板并将工作交付给矿工的挖矿基础设施已得到全面修改。改进包括通过智能投票传播处理支持异步后台模板生成，当当前提示无法获得足够的投票时改进对链重组的处理，更好的当前状态同步，在接收到新的区块和投票和订阅时几乎消除了过时的模板用于流模板更新。PoW矿工当前用于执行挖掘过程的标准[getwork RPC](https://github.com/decred/dcrd/blob/master/docs/json_rpc_api.mediawiki#getwork)已进行了更新，以利用此新基础架构，因此现有的PoW矿工将无需任何更新即可无缝地获得绝大多数收益。此外，新的[notifywork RPC](https://github.com/decred/dcrd/blob/master/docs/json_rpc_api.mediawiki#notifywork)现在可用，允许矿工注册通过WebSockets [工作通知](https://github.com/decred/dcrd/blob/master/docs/json_rpc_api.mediawiki#work)可用时异步交付的工作。这些通知包括getwork提供的相同信息以及其它参数。此参数使矿工可以更好地决定何时应该指示算力立即丢弃当前模板，或者何时应该允许算力完成当前任务，然后才提供新模板。

鼓励矿工更新其软件以使用新的异步通知基础结构，因为它比手动确定上述条件的轮询工作更高效且迅速。**注意:** 不会在挖掘时滚动时间戳字段的矿工应确保每次将其分发给矿工时都将其软件升级为将时间戳滚动到最新的时间戳。这有助于确保块时间戳尽可能准确。[dcrpool](https://github.com/decred/dcrpool)中已实现了使用通知和滚动时间戳的功能。

事务脚本验证几乎已完全重写，以显着提高其速度并减少内存分配的数量。这带来了显着的好处，包括更快的初始同步处理20-25％，更快的投票投放（这有助于减少miss的投票）以及更快的区块传播。

现在，自动外部IP地址发现使全节点可以更轻松地以分散方式发现网络上的其他节点。这将使以前的手动配置步骤自动化，例如在CLI上设置外部IP地址，为入站连接配置防火墙和/或路由器，以及将端口转发到运行dcrd的内部IP地址。

添加了Tor IPv6支持。除了现有的IPv4支持之外，现在还可以通过Tor解析并连接到IPv6用户。

**dcrwallet v1.5**

此版本的主要功能是初步的[CoinShuffle++](https://github.com/decred/dcrwallet/pull/1541)实现，该实现允许从集体混合的CoinJoin交易中购买选票。保护利益相关者的隐私至关重要，因为它还可以提高网络的安全性。初始版本有很多限制，最明显的是缺少对VSP票池的支持，没有图形用户界面以及对中央服务器的依赖。这些将在以后的版本中解决。值得注意的是，与较早的CoinJoin设计相反，服务器无法知道哪些输出属于哪个用户。

其他功能包括：针对区块头承诺达成共识性变更的投票议程，能够[导入](https://github.com/decred/dcrwallet/pull/1471) 任意扩展的公开密钥（消除地址重用的重要步骤），多种有用的RPC方法，提升性能和多个错误修复。

**Decrediton v1.5**

该版本的主要功能包括初始版本的闪电网络模块集成，大多数页面的响应，添加的夜晚模式，大量的UI调整，[大量数据下载修复](https://github.com/decred/decrediton/issues/2166)以及其他错误修复。

**dcrlnd v0.2**

上游更改已[移植](https://github.com/decred/dcrlnd/pull/42)到lnd [v0.8.0-beta](https://github.com/lightningnetwork/lnd/releases/tag/v0.8.0-beta)。共计379次提交和90个PR被合并。这带来了Safu Commitments, Watchtowers 和 Hodl invoices等功能。完成大量工作，以使dcrlnd与Decrediton更加无缝地集成。

用于计算支付哈希的哈希算法已从最初的BLAKE-256 [切换回](https://github.com/decred/dcrlnd/pull/46)了原始的SHA-256。这允许BTC / DCR / LTC 的闪电网络进行跨链支付。这是一个**重大变化**。在运行v0.1和v0.2的节点之间进行的跨渠道付款将不起作用，并且会导致自动强制关闭渠道。由于节点数量仍然很少，因此预计不会造成严重的干扰。

远程钱包现在可用 ; 这允许用户通过将dcrlnd连接到现有的远程dcrwallet来运行dcrlnd，而不是运行嵌入式dcrlnd。

有关所有4个项目的详细信息和下载，请参见[v1.5 RC1发布页面](https://github.com/decred/decred-binaries/releases/tag/v1.5.0-rc1)。与往常一样，验证二进制文件。虽然这很麻烦，但这是确保文件没有被更改的最佳方法。

非常欢迎您在正式版发布之前测试并提交您在测试版中发现的任何问题。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): RIPEMD-160哈希算法实现已[导入](https://github.com/decred/dcrd/pull/1907)dcrd存储库中，这是由于它在`x/crypto`中弃用和繁琐的依赖项管理所致。 尽管不建议在新的应用程序中使用它，但dcrd必须_永远_支持成熟的ripemd160才能验证历史事务并支持依赖它的p2sh脚本。 通常，内部化dcrd依赖的所有加密是一个好主意，因为共识应用程序的要求比其依赖项严格得多，正如比特币中的OpenSSL[问题](https://bitcoin.org/en/alert/2014-04-11-heartbleed)所证明的那样。

在v1.5发布之后，v1.6的改进已经开始。通过利用导出日志，实现了更快的[索引查找](https://github.com/decred/dcrd/pull/1969)。在v1.5版本开始之前无法完成的代码清理。工作继续将RPC服务器分割成自己的包，作为分离组件的更大开发活动的一部分。值得注意的是，一些更改正移植到上游btcd存储库。

[dcrwallet](https://github.com/decred/dcrwallet): 代码已更新为来自dcrwallet的新模块和来自dcrd的最新模块，添加了追踪代码以收集性能指标。

[Politeia](https://github.com/decred/politeia): 重新设计的Politeia前端于10月29日上线，外观与其它Decred的软件风格相匹配，移动端的体验也得到显著改善。同时还优化了性能。已经有好几个月了，恭喜Politeia开发团队！

`politeia选民`对[错误投票](https://github.com/decred/politeia/pull/1022)的抵抗能力更强。

[dcrstakepool](https://github.com/decred/dcrstakepool): UI调整，错误修复，直到v1.2发行为止。所有内联javascript已被[删除](https://github.com/decred/dcrstakepool/pull/560)。许多模块已更新为最新版本。

继续开展工作以实现[无帐户](https://github.com/decred/dcrstakepool/pull/515)购票，这将使电子邮件成为可选邮件，改善UX，并为消除投票地址重复使用铺平道路。

[dcrpool](https://github.com/decred/dcrpool):难度计算的[精度](https://github.com/decred/dcrpool/pull/135)已经提高。该池子已从轮询工作切换为通过dcrd使用新的参数获取工作通知。时间戳字符的滚动已添加。

[cspp](https://github.com/decred/cspp): 增加了保存已完成混币的JSON和CSV报告以及错误修复的功能。

[dcrdex](https://github.com/decred/dcrdex): 规范已进行了几处[更改](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2019-10-01..2019-10-31+label%3Aspec)，包括将原子交换合同转换为P2SH，并用自定义消息协议替换了JSON-RPC。构建了新的基本组件：[通信枢纽](https://github.com/decred/dcrdex/pull/33), [撮合服务器](https://github.com/decred/dcrdex/pull/39), [持久性订单存储](https://github.com/decred/dcrdex/pull/47), [交易列表订阅路由器](https://github.com/decred/dcrdex/pull/62), [交易列表路由器](https://github.com/decred/dcrdex/pull/65)。Simnet[测试工具](https://github.com/decred/dcrdex/pull/34)已添加。

[dcrandroid](https://github.com/decred/dcrandroid): 新的[用户界面](https://github.com/decred/dcrandroid/pull/401) 上的工作继续。 [跨平台钱包支持](https://github.com/raedahgroup/dcrlibwallet/pull/57)的工作仍在继续。这将允许用户从Decrediton导入他们的公钥，以便他们可以从手机上监视他们的选票的状态。

[dcrios](https://github.com/raedahgroup/dcrios): 正在对[种子还原钱包](https://github.com/raedahgroup/dcrios/pull/527)和[概述页面](https://github.com/raedahgroup/dcrios/pull/526)以及[导航菜单](https://github.com/raedahgroup/dcrios/pull/524)进行UI改进。

[dcrdata](https://github.com/decred/dcrdata): 重新设计[区块数据列表](https://github.com/decred/dcrdata/pull/1577)，性能改进，错误修复。

[docs](https://github.com/decred/dcrdocs): 添加了新页面，该页面解释了[区块生产时间](https://github.com/decred/dcrdocs/pull/995)，[词汇表术语](https://github.com/decred/dcrdocs/pull/1003)，部分更新和清理。

[devdocs](https://github.com/decred/dcrdevdocs): 开发人员文档已移至Decred GitHub组织。该站点尚未正式启动，但可以在[devdocs.decred.org](https://devdocs.decred.org/)上进行预览。如果您想添加任何内容，请在issues中提出或通过[#documentation](https://matrix.to/#/!tfqymymiNgzSUJTHqS:decred.org) 频道告知我们！

[decred.org](https://github.com/decred/dcrweb): [交易所](https://decred.org/exchanges/)页面已更新（[Easyrabbit](https://github.com/decred/dcrweb/pull/741)和[Cobo保管钱包](https://github.com/decred/dcrweb/pull/745)已删除，[Koi](https://github.com/decred/dcrweb/pull/731)场外交易补充）。Keybase已[添加](https://github.com/decred/dcrweb/pull/729)到[社区](https://decred.org/community/)页面。添加了一条Dev控制台消息来招募web黑客。Piwik analytics已被[删除](https://github.com/decred/dcrweb/pull/738)（在此之前，它是自托管的）。

10月份的开发活动统计：243个活动PRs、317个主提交、67K行添加和16K行删除，分布在12个存储库中。贡献来自每个存储库1-8个开发人员。

## 人员

欢迎新的首次贡献者到来，他们的代码已合并到主库中：Enrico Bonetti Vieno([dcrweb](https://github.com/decred/dcrweb/commits?author=ebonetti))。

因为我们的首次贡献者检测器仅扫描[提交](https://github.com/degeri/decred_contributor_track)，所以我们错过了两位新设计师：

- 自5月以来，Vlad Kharlantsev（来自Block 42的设计师）一直致力于[dcrtimegui](https://github.com/decred/dcrtimegui/issues?q=author%3Aharlovski)和[dcrdata](https://github.com/decred/dcrdata/issues?q=author%3Aharlovski)。
- 自9月底以来，Hannes Dvorjanski（EETER的设计师）一直为[Decrediton](https://github.com/decred/decrediton/issues?q=author%3Ahqnnes) 做贡献。

有点晚了，但是仍然热情的欢迎你们！

社区统计数据:

- Politeia 用户: 190 (+9)
- Twitter 粉丝: 40,632 (+54)
- Reddit 订阅: 9,656 (+25)
- Matrix 用户: 456 (+20)
- Slack 用户: 6,858 (+7)
- Discord 用户: 2,542 (+55), verified to post: 358 (+33)
- Telegram 用户: 2,967 (-81)
- YouTube 订阅: 3,860 (+30)
- Facebook 粉丝: 3,296 (+18), likes: 3,019 (+16)
- LinkedIn 粉丝: 638 (+16)
- GitHub dcrd 星星: 517 (+0), 叉子: 1,400 (+6)

## 治理

8月向承包商支付的款项已于10月2日支付，并在上一期《月报》中进行了[说明](201909.md)，未包含在以下数字中。

十月份，[社区基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)获得了14,970 DCR，并支出了12,539 DCR。使用10月份的每日DCR / USD平均价格$ 15.59，得出的收入为$233K，支出为$195K。以9月的每日平均汇率$ 22.02计算，该月完成工作的美元费用为$276K。截至11月5日，库存余额为643,041 DCR（1,280万美元，20.00美元）。

10月发布了5项新提案（截至11月8日的状态）：:

- DCR Comic [提议](https://proposals.decred.org/proposals/2ef74fa5f0b558442cb85b1235c8c551a51ff5d8b8de44dead48b8b59c8fc1de)以10,800美元的价格再生产6部漫画，获得了65％的批准，投票率为28％。
- 要求283,000美元开设咖啡店并建立Decred奖励积分系统的Coffee Points [提案](https://proposals.decred.org/proposals/1b4b72fa08792b6500ef770546c24ee751c2b0fee2975db769722524a2754829)遭到3％的批准和25％的参与而被拒绝。
- @ammarooni提出经济现象研究和教育[提案](https://proposals.decred.org/proposals/65bde4146b845e7e839d6916d4d8f642bc39c250df5379c2f1e26c4ab778ec1a)，要求已完成的工作$ 2,000，再工作3个月则要求$ 6,000。该计划获得了80％的支持和29％的投票率。
- [提议](https://proposals.decred.org/proposals/5a1bd4116565d107c1672799ed16cae9e92ec633c6e39d9b463b8218e66ff759)为DotA 2在线游戏的奖金提供资金，要求获得450美元的奖金和管理费用。它以3％的赞成票和28％的参与票被拒绝。
- 关于部分资助@ evok3d参加黑客大会并获得$ 2,050的提议已被放弃。其编辑了该[提议](https://proposals.decred.org/proposals/42b16d2741d58903963d8535e04017bbc3a8193391a83b305f44c082b62e3aa8)，提供了演讲和报告的链接，并表示他不打算进一步推行该提案，而是添加了捐款地址。

Politeia于10月16日为止上线了一年，并发布了许多文章：

- 来自[@Dustorf](https://twitter.com/lefebvre_dustin/status/1184511963965079552)和[@BlockCommons](https://twitter.com/BlockCommons/status/1184581107578298369)的统计信息的推文
- @richardred [记录](https://blockcommons.red/publication/politeia-at-1/) Politeia第一年的数据
- 加密简报文章中所写的@ jy-p [访谈](https://cryptobriefing.com/decred-politeia-decentralized-governance/)谈
- 来自@Exitus的[视频](https://www.youtube.com/watch?v=58gTCW7DTMg)评论
- [回顾](https://blockcommons.red/post/year-of-politeia/) @richardred

Politeia的重新设计于10月29日开始生效，使其设计风格与Decred的其他项目保持一致，并对性能进行了提升以及许多其他改进。@lukebp在[推特](https://twitter.com/lukebp_/status/1189219953855082497)上发布了相关信息，其中说到Politeia可能需要另一位有才华的前端开发人员。

@degeri提供了赏金计划的[更新](https://bounty.decred.org/2019/10/status-update/)。自7月以来，已处理了16份新报告，其中1份有资格获得付款-dcrdata中的安全性 [问题](https://github.com/decred/dcrdata/pull/1563)（现已修复）。

[提案](https://github.com/decredcommunity/proposals)存储库于8月启动，最初是一个高层次的想法，使利益相关者可以快速找到有关提案的所有重要信息。收集了[DEX](https://github.com/decredcommunity/proposals/tree/master/dex)和[做市商](https://github.com/decredcommunity/proposals/tree/master/market-makers)建议的初始数据，其中包括重要文件和讨论的索引以及对这些建议的分析。在10月，存储库的范围扩大到了索引可交付成果并托管已批准提案的进度更新。为[开源研究](https://github.com/decredcommunity/proposals/tree/master/research-richardred), [Ditto PR](https://github.com/decredcommunity/proposals/tree/master/pr-ditto)和[Bug 赏金计划](https://github.com/decredcommunity/proposals/tree/master/bug-bounty-program)添加了第一批索引和更新，还有更多后续更新。最大的目标是改善报告和监督。

[准则](https://github.com/decredcommunity/guidelines)存储库已启动，以从多个Decred贡献者那里收集指导文档。现在，它已移交给decredcommunity组织，以托管新的社区组织者行动手册。

有关治理的更深入报道，请参阅《Politeia摘要》第[23](https://www.blockcommons.red/politeia-digest/issue023/)期和第 [24](https://www.blockcommons.red/politeia-digest/issue024/)期。

## 网络

全网算力：10月份的全网算力以约446 Ph/s的速度开启，以约452 Ph/s的速度结束，在整个月均达到339 Ph/s的谷底。截至11月2日的池算力分布：UUPool 19％，Poolin 15％，F2Pool 5.6％，lab.antpool.com 5％，BTC.com 2.4％，Luxor 1.95％，Coinmine 0.10％，BeePool 0.10％，suprnova 0.01％和其他每个[dcrstats.com](https://dcrstats.com/pow)为 50％。池分配数是近似值，无法准确确定。

值得注意的是，在11月2日的快照中，“其他”（未知）来源的算力百分比达到了50％，而10月2日为30％。

截至11月8日，过去30天中的全网算力变化是每dcrdata -24％。在10月9日至25日之间，平均算力从〜500 Ph/s降至〜400 Ph/s，难度从〜38B降至〜29B。这种下降与DCR / USD价格跌破16.5美元跌至13美元相关。

Staking: 每dcrstats.com的30天平均票价为132.3 DCR（+3.6）。价格在120.8-142.3 DCR之间变化。锁定金额为522.38百万DCR，相当于可用供应量的49.59-50.97％。

节点: 整个[十月](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1569888000000&to=1572566400000)，每个dcr.farm大约有146个监听节点，总共402个节点。根据月平均节点数，大约有76％的运行dcrd v1.4.0，7.5％是v1.5.0，0.7％是v1.6.0（pre）开发版本。在SPV模式下，有9.4％的节点是dcrwallet v1.4。

截至11月8日，根据[dcrdata](https://explorer.dcrdata.org/agendas)显示，大约有17％的PoS选民表示他们已经升级并准备投票赞成共识规则更改。

根据10月14日发布的[推文](https://twitter.com/decredproject/status/1183770504580206593)，约有15％的选票是使用隐私交易，这使得匿名交易占流通中所有DCR的7.5％。

## 外联活动

宣传活动继续针对隐私发布进行，其中包括以@jrick 为特色的Decred Assembly[插曲](https://www.youtube.com/watch?v=iWdA1C-SHSk)，但重点已转移例如治理，DAO和正在开发的项目。 [社区组织者行动手册](https://github.com/decredcommunity/guidelines/blob/master/community-organizer-playbook.md)与社区成员的最佳实践和包括活动指南，这是由@eSizeDave发起并@zohand来自澳大利亚。这些工具旨在帮助社区成员在全球范围内构建由用户，开发人员，合作伙伴和媒体组成的Decred生态系统。如果您看到改进的方法，请在[此处](https://github.com/decredcommunity/guidelines/pull/5)评论。

Decred in Depth在十月份发布了两集：[DCR Security](https://www.youtube.com/watch?v=FX2ZncHIAd4)上的@zubair和[OKCoin](https://www.youtube.com/watch?v=UBRjkjbmYDc)观点上的 Alex Feinberg 。生态系统中的社区成员为宣传和教育工作做出了巨大贡献，其中最著名的是 [@BlackBearXVII](https://medium.com/@imagnusholdings)，他将在Decred上发布一个由十部分组成的Medium系列。@permabullnino，他发表了[Decred On-Chain: A Look at Block Subsidies](https://medium.com/@permabullnino/decred-on-chain-a-look-at-block-subsidies-6f5180932c9b)；@Checkmate，他发布了各种各样的研究和推文主题；@Exitus，他录制了有关Politeia第一年的[视频](https://twitter.com/coveryfire7777/status/1186075335076528130) ；和@richardred发布的[推文](https://twitter.com/BlockCommons/status/1184581107578298369)Politeia的第一年，以及对 [加密共享对等生产](https://twitter.com/RichardRed0x/status/1190315513043472385)，这是他自2019年初以来一直在研究的免费书籍。

随着即将改版的网站的推出，Decred社交媒体活动的增加以及不断涌现的研究和出版材料，Decred很好地弥补了信息不对称方面的空白。

Ditto十月成就:

- 13家媒体报道，包括

  - 在CryptoWendyO的[YouTube](https://www.youtube.com/watch?v=dF7hkxzggvk)频道上接受Jake的采访，谈论DAO和Decred。
  - [Crypto Slate](https://cryptoslate.com/data-shows-autonomous-coin-decred-has-a-power-law-relationship-with-bitcoin/)上的专题文章“数据显示自主硬币Decred与比特币有幂律关系”。
  - [Crypto Briefing](https://cryptobriefing.com/decred-politeia-decentralized-governance/)中有关Politeia上线一周年的专题文章。
  - @jz对比特币在[CCN](https://www.ccn.com/bitcoin-best-store-of-value-over-last-decade/)中的价值存储的评论。
  - 在[Bloxlive](https://bloxlive.tv/video/MTc0Mg==/zubair-zia-explains-the-decred-digital-currency-and-its-origins)上采访Zubair 。
  - 在 Brave New Coin的 [The Crypto Conversation Podcast](https://bravenewcoin.com/insights/podcasts/decreds-privacy-flow-building-a-better-bitcoin-and-the-legend-of-satoshi)中接受Jake的采访-这是Jake迄今为止最好的表演之一。
  - 在[The Daily Chain podcast](https://anchor.fm/thedailychain/episodes/Decred---a-Bitcoin-Hedge-e5rhmt)上接受卢克的采访，他雄辩地解释了比特币的硬分叉问题。
  - 在[Crypto Briefing](https://cryptobriefing.com/eos-governance-ico-settlement/) 中的一篇文章中，Jake讨论了EOS治理和Decred的选民投票率。

- 为Decred出席Web Summit提供媒体关系支持：创建了顶级媒体简报，确定了要见面的记者等。

- 在世界加密货币会议上安排了对Akin的四次媒体采访，包括Anthony“ Pomp” Pompliano，用于加密电视新闻节目的Nicole Grinstead，用于Digit-All网络节目的Jimmy Peralta以及来自Legacy Research的Greg Wilson。

- 与主流记者就DAO的概念和（匿名）工作场所的未来展开对话。

## 社区活动

参加:

- 9月18日-  [Bitcoin & Blockchains Common Meetup](https://www.facebook.com/events/959839374354073/) -墨西哥瓦哈卡。这是由@ evok3d组织的实践研讨会，有10人参加。主题包括安全性，治理，提案系统和区块链应用程序。（[photos](https://twitter.com/Decred_ES/status/1174803011610259456)，9月遗漏）
- 10月4日至5日- [Blockchain & Digital Assets Conference](https://www.eventbrite.com/e/abuja-blockchain-digital-assets-conference-2019-tickets-67571336687) -尼日利亚阿布贾。Raedah Group的团队经营了Decred展位并回答了问题。([报告](https://github.com/decredcommunity/events/blob/master/reports/20191004-blockchain-digital-asset-conference-abuja-nigeria.md), photos: [1](https://twitter.com/beansgum/status/1180117854240288768), [2](https://twitter.com/raedahgroup/status/1180930491244937216))
- 10月4日至6日- [Hackers Congress](https://opt-out.hcpp.cz/) -捷克共和国布拉格。@ evok3d在演讲中（[23:53](https://www.youtube.com/watch?v=fmgNbLGCO5U&t=23m53s)）介绍了Decred的治理，融资模式和隐私，并在接受 World Crypto Network 采访时[22:37](https://www.youtube.com/watch?v=dq2SGpI5-Gw&t=22m37s)[讨论](https://www.youtube.com/watch?v=fmgNbLGCO5U)了Decred 。完整的报告发布在Medium上，并反映在事件中。另请参阅相关的Politeia[提案](https://proposals.decred.org/proposals/42b16d2741d58903963d8535e04017bbc3a8193391a83b305f44c082b62e3aa8)。
- 10月8日- [Tech Tuesday](https://www.meetup.com/PermanentBeta/events/qtcrhryznblb/) -荷兰乌得勒支。这是大型聚会的一部分，该聚会主要关注一般技术（智慧城市，IoT，生物黑客等）。@ evok3d知道组织者，因此他在聚会期间促进了区块链跟踪。出现了4名感兴趣的人（一名学生，研讨会之后给她留下了深刻的印象）。@Haon演示了Decred的钱包的简短演示。
- 10月10日-[Devcon 5](https://devcon.org/)-日本大阪。@joshuam谈论了Decred的治理。([照片](https://twitter.com/kate_sills/status/1182474689995653120))
- 10月13日-[O-link by Odaily](http://odaily001.huodongxing.com/event/2511153700300)-西安。@Dominic参加了一个小组讨论了Decred的隐私。([照片](https://twitter.com/wanbihou/status/1184183795940880384))
- 10月16日- [DAOfest Meetup](https://thenextweb.com/hardfork-summit/events/daofest-amsterdam-meetup) -荷兰阿姆斯特丹。@ evok3d [讨论](https://www.youtube.com/watch?v=Jt_2vk-hf4o&t=19m38s)了Decred的治理模型，并与@Haon一起参加了有关DAO的小组讨论。主要活动之后进行了网络会议。([报告](https://github.com/decredcommunity/events/blob/master/reports/20191016-daofest-amsterdam-netherlands.md))
- 10月17日-科技大学-墨西哥莫雷利亚。@luisantoniocrag和@francov_向区块链技术，加密货币和Decred引入了100多人（主要是学生和一些教师）。人们第一次听说它，对此感到非常好奇。引起他们注意的事情之一是“大学学位，年龄，国籍或其他任何能够工作和做伟大的事情都没有关系”。他们还要求举办后续研讨会。会谈结束后，团队被邀请参加“人才之夜”，这对企业家来说是一项重要活动。([报告](https://github.com/decredcommunity/events/blob/master/reports/20191017-decred-meetup-morelia-mexico.md), [照片](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$1571354151416323TNRDg:matrix.org))
- 10月18日-  [Crypto Friday](https://www.meetup.com/Crypto010-Rotterdam-Virtual-Currency-Blockchain-Meetup/events/264476624/)，荷兰鹿特丹。@ evok3d大约有20-30人参加了会议，谈到了DAO和Politeia。音频将很快上传。([照片](https://mega.nz/#!R2pgAKSB!bHjwi3t3N687xNpec4YDTnl0pBhJcMJ1HFtdDk0ou28))
- 10月20日- Wafaa Association -摩洛哥卡萨布兰卡。在9月在卡萨布兰卡举行的Decred [聚会](https://github.com/decredcommunity/events/blob/master/reports/20190921-decred-meetup-casablanca-morocco.md上，@ arij被要求在Wafaa协会介绍区块链技术。大约有20人参加，其中大多数是学生。@arij讨论了整整2个小时的区块链基础知识和共识系统。人们是该技术的新手，并要求再次发表演讲以了解更多信息。([报告](https://github.com/decredcommunity/events/blob/master/reports/20191020-wafaa-casablanca-morocco.md))
- 10月23日- World Bank Innovation Lab -美国华盛顿特区。@akinsawyerr在Decred上向世界银行创新实验室的工作人员进行了概述介绍。对话还探讨了世界银行10月24日- [Bullish Night](https://www.eventbrite.com/e/bullish-night-at-bull-and-bear-academy-tickets-77415737555) -墨西哥墨西哥城。@elian与墨西哥和拉塔姆的商人社区进行了交谈，并简要介绍了Decred的含义。Decred是赞助商。([照片](https://twitter.com/Decred_ES/status/1187534463569289216))
- 10月24日- [Cryptocurrency Workshop](https://twitter.com/Decred_ES/status/1187206051000655872) -墨西哥莫雷利亚。@francov_和@luisantoniocrag在莫雷利亚技术大学举办了一个为时4小时的研讨会，向他们展示了如何使用Decred钱包。与10月17日的演讲不同，研讨会的内容更为详尽，尽管只有15名学生，但他们所有人都完全了解了区块链和Decred的操作。不仅在技术方面，而且在财务方面。([照片](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$157202936428052qbfho:matrix.org))
- 10月29日- [Decred Governance Workshop](https://www.meetup.com/Blockchain-innovation-Singapore/events/265738541/) -新加坡。@joshuam和@zohand在新加坡首次向WeWork的亲密人群介绍了Decred。这是对区块链治理和稳健资金，Decred的治理模型和总体设计的深入研究。人群精通加密技术，他们发现内容非常有用，并将问答环节变成了一个小时的深入讨论。要求进行一次后续会议。([报告](https://github.com/decredcommunity/events/blob/master/reports/20191029-decred-governance-workshop-singapore.md), [照片](https://twitter.com/GuangGuang168/status/1189381286458089473))
- 10月29日- [Decred Meetup](https://www.eventbrite.com/e/que-hace-a-decred-una-criptomoneda-diferente-primer-meetup-oficial-tickets-78464211569) -哥伦比亚波哥大。@elian和@victorarubin对该项目进行了高级别的概述，从其赛博朋克的起源到其混合共识，Politeia，隐私，全球团队和未来。大约60位年龄在20至50岁之间的人参加了该活动，主要是加密爱好者。其中约有10个曾经使用GPU来挖掘DCR。在问答环节中，该团队收到了有关Decred的集中管理，ASIC的角色，Latam中的采用计划以及何时可以使用DCR来购买啤酒的一些很好的问题。该活动由哥伦比亚Blockchain Academy，Panda Exchange，[Cointelegraph en Español](https://es.cointelegraph.com/news/decred-starts-series-of-meetings-in-colombia)和[Diario Bitcoin](https://www.diariobitcoin.com/index.php/2019/10/28/colombia-blockchain-academy-realizara-primer-meetup-sobre-decred-en-bogota/)共同主办。后两者在其网站上报道了该事件。（照片：[1](https://twitter.com/Decred_ES/status/1188496680133500934), [2](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$157244810128246sZnzI:decred.org)）
- 10月29日- [World Crypto Conference](https://worldcryptocon.com/) -美国拉斯维加斯。@akinsawyerr代表Decred在“实践中的治理”面板上进行了演讲，并作了名为“治理加密货币共同体”的演讲，概述了Decred的治理过程并分享了从一年的Politeia数据中得出的见解。Akin还进行了Ditto安排的几次采访和会议。

即将到来的:

- 11月15日至16日- [CriptoBlock](https://criptoblock.com.br/) -巴西圣保罗。前两个版本很小，Decred没有参加，但是这次组织者希望有大约1000名与会者。Decred将成为青铜赞助商，@ Rhama和@girino将介绍有关Decred的基本话题。
- 11月16日- [BitConf](https://www.bitconf.com.br/portal/) -巴西圣保罗。拉丁美洲最大的加密货币活动之一。计划举办约3场Decred讲座。
- 11月21日- [Africa Fintech Summit](https://africafintechsummit.com/addis/) -埃塞俄比亚亚的斯亚贝巴。@akinsawyerr将在区块链面板上发言。
- 11月21日- Decred Meetup -德国柏林。讨论Decred的隐私保护并与其他解决方案进行比较。

## Media

This month saw the release of two new websites which have been produced as part of the [Decred Open Source Research](https://proposals.decred.org/proposals/67de0e901143400ae2f247391c4d5028719ffea8308fbc5854745ad859fb993f) program.

[Peer Production on the Crypto Commons](https://www.cryptocommons.cc/) is a free book authored by @richardred. It considers how a number of different constituencies (miners, developers, merchants, users) work together to produce a blockchain and give it value. It also considers blockchains as a type of common pool resource built with open source software, and what the broader implications of this are.

[BlockCommons.red](https://www.blockcommons.red/) is a site which hosts research and educational content about "the crypto commons", including the [Pi Research](https://www.blockcommons.red/#reports) and [Crypto Governance Research](https://www.blockcommons.red/crypto-governance-research/overviews/) write-ups. [Politeia Digest](https://www.blockcommons.red/politeia-digest/) has also moved there (although it will continue to be published on Medium and GitHub also).

[textassets](https://github.com/decredcommunity/textassets) repository was created to collect text pieces from various websites and social media platforms. Having all texts in one place allows to quickly find outdated texts using a simple text search. It also allows the use of GitHub features to discuss and collaborate on future changes before implementing them (a recent example is the [update](https://github.com/decredcommunity/textassets/pull/1) of Reddit sidebar).

Selected articles:

- Delphi Digital has [released](https://twitter.com/Delphi_Digital/status/1181228136274518016) a deep dive on Decred for their institutional subscribers (not publicly available).
- Decred - An Alternative Contender by @ammarooni ([medium](https://medium.com/@Ammarooni/decred-an-alternative-contender-a3547a014745))
- Decred, Following in Bitcoin's Footsteps by @Checkmate ([medium](https://medium.com/@_Checkmatey_/decred-following-in-bitcoins-footsteps-f8d0e0bbaff5)) - part of his [proposal](https://proposals.decred.org/proposals/78b50f218106f5de40f9bd7f604b048da168f2afbec32c8662722b70d62e4d36).
- Data Shows Autonomous Coin Decred Has a Power Law Relationship with Bitcoin ([cryptoslate](https://cryptoslate.com/data-shows-autonomous-coin-decred-has-a-power-law-relationship-with-bitcoin/))
- @BlackBearXVII has been [releasing](https://twitter.com/BarnardTheBear/status/1185200240770670596) a 10-part series on Medium (Decred X), one installment every 3 days. October's pieces:
  - [Part I - Narrative](https://medium.com/@imagnusholdings/decred-x-part-i-narrative-41f3e08599be)
  - [Part II - Deck of Cards](https://medium.com/@imagnusholdings/decred-x-part-ii-deck-of-cards-33d488751f16)
  - [Part III - Tech](https://medium.com/@imagnusholdings/decred-x-part-iii-tech-6f1ca4546108)
  - [Part IV - Code](https://medium.com/@imagnusholdings/decred-x-part-iv-code-c04e71c29ca4)
  - [Part V - Property](https://medium.com/@imagnusholdings/decred-x-part-v-property-8b1a5570b924)
- Decred On-Chain: A Look at Block Subsidies by @permabullnino ([medium](https://medium.com/@permabullnino/decred-on-chain-a-look-at-block-subsidies-6f5180932c9b)) - part of his [proposal](https://proposals.decred.org/proposals/f0d1bd7447182328b44c691de88cb660b63df17f1f3a94990af19acea57c09bb).
- Decred: A Sound Store of Value by @Haon ([medium](https://medium.com/coinmonks/decred-4cb7eb66db14)) - also circulated to Coinmonks subscribers and on [Twitter](https://twitter.com/coinmonks/status/1186294858903736323).
- One Year of Decred's Politeia in Numbers and Graphs by @richardred ([blockcommons.red](https://www.blockcommons.red/publication/politeia-at-1/))
- Decred's Politeia: Lessons Learned From a Year of Decentralized Governance by Darren Kleine ([cryptobriefing](https://cryptobriefing.com/decred-politeia-decentralized-governance/)) - worth checking out for the image alone!
- The First Year of Decred's Politeia by @richardred ([blockcommons.red](https://www.blockcommons.red/post/year-of-politeia/))

Translations:

- Decred Journal September 2019 was translated to Arabic (@arij), Chinese (@Dominic and co), Polish (@kozel) and Spanish (@francov\_ and @luisantoniocrag). Thank you so much!

Videos:

- Year 1 Review of Politeia by @Exitus ([youtube](https://www.youtube.com/watch?v=58gTCW7DTMg))
- @jy-p giving a presentation about Decred and Privacy at an LA meetup hosted by Blockhead Capital ([youtube](https://www.youtube.com/watch?v=JNPPMwr9TU8))
- @jy-p interview on BlockTV about Libra and the very different approach that Decred takes to governance. ([BlockTV](https://blocktv.com/watch/2019-10-30/5db9ab4487a7e-resolving-corporate-governance-in-cryptocurrency))
- Unfortunately titled but highly informative 10-minute video about Decred from Ready Set Crypto ([youtube](https://www.youtube.com/watch?v=DtzDBnenYYY))
- What is a DAO? Interview with @jy-p on the CryptoWendyO show ([youtube](https://www.youtube.com/watch?v=dF7hkxzggvk))
- @zubair introduced Decred and its origins to the bloxlive audience ([bloxlive.tv](https://bloxlive.tv/video/MTc0Mg==/zubair-zia-explains-the-decred-digital-currency-and-its-origins))
- Decred Assembly - Deep Dive - Privacy with @jrick ([youtube](https://www.youtube.com/watch?v=iWdA1C-SHSk))
- @pablito's take on generating music from Decred blockchain ([youtube](https://www.youtube.com/watch?v=BzTCwsmnPJ8))

Audio:

- Decred in Depth Ep. 9 with @zubair - Zubair talks about blockchain security, how PoW works, majority attacks, PoS issues, and how Decred leverages the strengths of PoW and PoS to enhance security. ([youtube](https://www.youtube.com/watch?v=FX2ZncHIAd4), [soundcloud](https://soundcloud.com/decredindepth/ep-9-zubair-zia-security-dcr-spend))
- Decred in Depth Ep. 10 with Alex Feinberg of OKCoin - Alex talks about his background and interest in blockchain, weaknesses of fiat currency, the "Let's Build Bitcoin Together" program, DEXes, and how OKCoin sees its role in the space. ([youtube](https://www.youtube.com/watch?v=UBRjkjbmYDc), [soundcloud](https://soundcloud.com/decredindepth/ep-10-alex-feinberg-blockchain-exchange-process))
- Decred in Depth Ep. 11 with [@liz_bagot](https://twitter.com/liz_bagot/status/1190279034132815872) of Ditto talking about crypto PR, Ditto's work on Decred, why Bitcoin doesn't need PR but other projects do, and why shills are bad for long-term sustainability. ([soundcloud](https://soundcloud.com/decredindepth/ep-11-liz-bagot-pr-marketing))
- Crypto Conversation Ep. 11 - @jy-p talks about Decred privacy and the project's origin story, interactions with the pseudonymous @tacotime and @\_ingsoc and speculation about their intentions. ([bravenewcoin.com](https://bravenewcoin.com/insights/podcasts/decreds-privacy-flow-building-a-better-bitcoin-and-the-legend-of-satoshi))
- The Daily Chain podcast - Decred - a Bitcoin Hedge - @lukebp talks about Decred as augmenting Bitcoin with governance and coordination, and the strong development team and open source culture that enticed him to start working on the project. ([anchor.fm](https://anchor.fm/thedailychain/episodes/Decred---a-Bitcoin-Hedge-e5rhmt))

## Community Discussions

Comm systems news:

- New Reddit style is [injecting](https://archive.today/3HoCx) "promoted" posts that were never submitted to our subreddit straight into our post listing, stealing about 2.5x vertical space occupied by a normal post.
- The Reddit sidebar was updated via the new [textassets](https://github.com/decredcommunity/textassets/pull/1) repository and using latest [messaging](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md). You might need to use [old.reddit.com](https://old.reddit.com/r/decred/) to see it.
- New chat room aliases have been added to have less typing and better reflect the content: #events (was #event\_planning), #media (was #social\_media) and #writers (was #writers\_room).

Selected Reddit posts:

- A thoughtful [discussion](https://www.reddit.com/r/decred/comments/dku88o/what_does_decreds_governance_model_incentivize/) between @bee and @oiezz about the incentives associated with Decred's governance.
- A [post](https://reddit.com/r/decred/comments/dgycc3/long_term_decred_believer_and_investor_any/) about a large price drop attracted 40 comments.
- A [post](https://old.reddit.com/r/decred/comments/doinau/concerning_zksnarks/) discussing the possibility of zk-SNARKS for Decred.
- A [post](https://reddit.com/r/decred/comments/dmaza0/does_decred_have_bounties_for_github_issues/) asking whether Decred has bounties for GitHub issues attracted 35 comments and prompted an in-depth discussion of Decred's open source approach and the need for committed contributors with skin in the game when it comes to core development. For some reason this post only has a score of 6.
- A [post](https://reddit.com/r/decred/comments/dhrq4i/why_tickets_be_so_expensive/) asking why tickets are so expensive had 22 comments.

Selected Twitter discussions:

- Privacy usage [update](https://twitter.com/decredproject/status/1183770504580206593), ~15% of ticket purchases are using the new privacy feature.
- @DCRComic has been tweeting comics about [making proposals](https://twitter.com/DCRComic/status/1181647636492963844) and [mining](https://twitter.com/DCRComic/status/1184471574784741376).
- @DCRtheSOV monthly [update](https://twitter.com/DCRtheSOV/status/1188943254223372289) on Politeia
- @lukebp [tweets](https://twitter.com/lukebp_/status/1189219953855082497) about the deployment of Politeia redesign
- @akinsawyerr [tweets](https://twitter.com/AkinSawyerr/status/1186718327219130368) about the reduction in transaction costs as the story of human progress.

## Markets

In October DCR was trading between USD 12.91-17.59 / BTC 0.0015-0.0021. The average daily rate was $15.59.

Since the beginning of the month the price was declining from $17.5 all the way down below $13. This reversed around Oct 25 and by the end of the month it recovered back to $17.

i2 Trading reported in the [#proposals](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$157176144520723FSmYA:decred.org) channel that their market making activities officially launched on Oct 22 on all exchanges except OKCoin, where there is a holdup. i2 will start billing from Oct 22, and previous testing will not be charged for.

## Relevant External

Iterative Capital [introduced](https://iterative.capital/introducing-escher-hub-making-every-foss-wallet-a-cheap-and-fast-way-to-transact-bitcoin/) Escher, a Lightning-enabled BTC-USD on and off-ramp that can connect Bitcoin wallets and Lightning channels to users' bank accounts. Developers of FOSS cryptocurrency wallets can integrate with Escher Hub, which will allow users to manage the wallets and channels they control and move funds between BTC and USD easily. Chris Dannen [stated](https://twitter.com/chrisdannen/status/1187387952386707457) on Twitter that DCR is the only other cryptocurrency that support is planned for.

A [review](https://blog.coincodecap.com/dead-coins-on-crypto-exchanges/) of 3,162 projects by CoinCodeCap found that 1,240 of these had no code commits in the previous 90 days and by this criterion were considered dead. The report also considers centralized and decentralized exchanges in terms of how many dead projects they list.

A [proposal](https://ethereumclassic.org/blog/2019-10-06-pow-mining-explicit-social-contract/) has been made within the Ethereum Classic community for an explicit social contract in favor of PoW mining. There was apparently strong social consensus at the recent ETC conference in Vancouver and an ECIP is being prepared for consideration. ECIP editors will decide whether the proposal is approved, the intention of approving it would be to signal to PoW miners that the community intends to support them for the long run.

A Bitcoin Mining Parliament has been [proposed](https://coinspice.io/news/radical-proposal-bitcoin-mining-parliament-drama-ending-governance-or-more-alienating-devs/) by Javier Gonzalez as a way for miners to coordinate by voting with their hashpower on proposals about the consensus rules.

The 3rd round of Gitcoin quadratic funding was completed, and Vitalik Buterin wrote a [post](https://vitalik.ca/general/2019/10/24/gitcoin.html) about it. In total $163K was donated to 80 projects by 477 contributors, augmented by a matching pool of $100K. Buterin compared Gitcoin's funding with that of the Ethereum Foundation and found that it was more inclined to fund projects that were valued by the community. The version of quadratic funding was changed from previous rounds to make it less susceptible to the kind of manipulation that had occurred.

StakerDAO, a DAO for investing in PoS blockchains, [launched](https://www.coindesk.com/theres-now-a-dao-for-deciding-which-blockchains-to-stake-on). StakerDAO is created by the Tezos Capital CEO and the main investor is Polychain Capital. At launch they published a number of research reports, including [one](https://medium.com/stakerdao/decred-research-833585a988d5) for Decred.

Coinbase Custody now [supports](https://blog.coinbase.com/coinbase-custody-now-supports-maker-governance-ced7aabfa054) Maker governance, allowing people who hold their MKR with Coinbase Custody to participate in voting without withdrawing their tokens.

The CEO of the Maker Foundation [announced](https://blog.makerdao.com/breaking-launch-date-of-multi-collateral-dai-announced-at-devcon-5/) that Multi-Collateral Dai will launch on Nov 18, and [announced](https://blog.makerdao.com/say-goodbye-to-cdps-and-hello-to-maker-vaults/) a re-naming of several key components on Oct 31.

Chinese President Xi Jinping made a positive [statement](https://www.coindesk.com/president-xi-says-china-should-seize-opportunity-to-adopt-blockchain) about blockchain technology and said that China should seize the opportunity to adopt blockchain technology.

CryptoBridge, a "_Gateway_ to the BitShares _decentralized_ trading platform", is [requiring](https://twitter.com/CryptoBridge/status/1178913681117196293) users to verify their identities in response to EU's 5th Anti-Money Laundering Directive (AMLD5). The linked [blog post](https://crypto-bridge.org/2019/10/01/introducing-user-verification/) assures that this is great for users.

A BTC flash crash [occurred](https://www.coindesk.com/bitcoin-prices-slides-2-after-deribit-coinbase-flash-crash) on Deribit and Coinbase Pro, with the price dipping from $9,150 to $7,720 on Deribit for a few minutes before rebounding. Deribit [stated](https://twitter.com/DeribitExchange/status/1190047067365953536) that they will reimburse $1.3 million in losses for the people who were negatively affected.

Tired of missing out on the global crypto market, Poloniex is [leaving](https://blog.circle.com/2019/10/18/poloniex-to-spin-out-of-circle/) U.S. jurisdiction to focus on an international cryptocurrency exchange backed by an Asian investment group. U.S. customers will be unable to create new accounts. Existing accounts will have to finish trading by Nov 1 and withdraw by Dec 15. To celebrate the move, Poloniex has set 0% trading fees till the end of 2019. As usual with acquisitions, customer data will change hands once again. Let's see if customers will be asked their consent before their data is handed to new people.

Huobi will [freeze](https://huobiglobal.zendesk.com/hc/en-us/articles/360000659122-Arrangement-to-freeze-US-user-accounts-on-13-November-2019-GMT-8-) all U.S. accounts on Nov 13 as part of enforcement of their user agreement that prohibits U.S. users from trading.

United Nations International Children's Emergency Fund (UNICEF) has [announced](https://www.unicef.org/press-releases/unicef-launches-cryptocurrency-fund) that it is now able to receive, hold and disburse donations of BTC and ETH. The fund will not sell the cryptocurrency for fiat but instead hold and disburse it. The first donations are from the Ethereum Foundation.

In the United States, the IRS has updated the main form used by individual taxpayers to add a question about whether the person had interacted with cryptocurrencies during the year. According to this [tweet](https://twitter.com/allyversprille/status/1184827340737654785), IRS Chief Counsel Michael Desmond thinks there are around 12 million taxpayers that should be reporting cryptocurrency assets.

The IRS has also ["clarified"](https://www.journalofaccountancy.com/news/2019/oct/irs-income-cryptocurrency-hard-forks-airdrops-201922209.html) its position on the receipt of forked coins and airdrops. The position has been widely criticized, as it would mean that every time a ledger is forked all of the holders must report the coins they received on the new chain.

In Hong Kong, people withdrew so much cash from ATMs that they ran out of supply. Localbitcoins volume [surged](https://blockonomi.com/hong-kong-bank-run-bitcoin/) temporarily, then fell back to its normal range.

U.S. Federal Reserve will buy about [$60B of Treasury bills](https://www.ft.com/content/baa7e796-ec38-11e9-85f4-d00e5018f061) per month for at least 6 months. They call it "_organic growth_ of the central bank's balance sheet" and try very hard to not call it _QE4_, which appears to be finally gaining a negative connotation after multiple rounds of money creation that did not solve the problem. Market interventions by the Fed [started](https://www.newyorkfed.org/markets/opolicy/operating_policy_190917) on Sep 17 when for some reasons there was not enough liquidity in the "repo market". Some observations: 1) Fed has not had to do this since the financial crisis of 2008; 2) Fed and ECB began their interventions around the same time; 3) just like with ECB, it is very hard to understand how it works exactly. Similar to the [previous](201909.md#relevant-external) question to the ECB, it is unknown how hard the Fed worked to earn the money. Feel free to bring some clarity in Reddit comments.

Austrian central bank Governor thinks that ECB's QE is [counterproductive](https://www.bloomberg.com/news/articles/2019-10-13/ecb-s-holzmann-says-draghi-s-qe-policy-is-counterproductive).

A flaw was [identified](https://www.engadget.com/2019/10/14/linux-unix-sudo-command-security-flaw/?guccounter=1) in the ubiquitous sudo command of Linux. It would allow anyone with sudo access on the machine to gain full root privileges if exploited. Make sure to update your systems.

The Internet has celebrated 50 years. On Oct 29, 1969, the first data was sent between two computers - a crazy idea back then. The first message to transmit was "login" but the receiving computer crashed after getting 'o'. "So, the first message was 'Lo' as in 'Lo and behold'. We couldn't have a better, more succinct first message" [noted](https://usa.inquirer.net/44807/ucla-anniversary-kleinrocks-technology-lab) Leonard Kleinrock, who led the experiment. When speaking about the "dark side" of the Internet he remained optimistic: "I still feel that the benefits are far more significant; I wouldn't turn off the internet if I could" and expressed interest in blockchain tech.

## About This Issue

This is issue 19 of Decred Journal. Index of all issues, mirrors and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: akinsawyerr, bee, degeri, Haon, kozel, richardred, s\_ben
- reviews and feedback: davecgh, Dominic, jholdstock, emiliomann, evok3d, jz, linnutee, lukebp, raedah, zohand
- title image: saender

