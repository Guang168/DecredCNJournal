# Decred月报 - 2019年8月

![abstract art](img/journal-201908-384.png)

_图片: 对称 by @saender. 当信息对称时，就会发生大事._

八月重点:

* Company 0 秘密开发的的隐私功能披露，初步隐私保护功能已经发布，首次混币在主网上被观察到，请参阅下面的隐私部分。
* 在由@chappjc和@buck54321领导的提案中，90％的选民批准了高达230,000美元的资金后，Decred去中心化交易工具的开发工作已经开始。
* 锁定在PoS选票中的流通DCR百分比在8月15日首次突破50％以上。随着选票价格的上涨，表明Decred持有者的信心随着时间的推移而增加，因为更多持有者选择锁定他们的DCR参与治理。
* Decred利益相关者表示他们希望为做市商提供资金以解决流动性问题（87％的批准）。来自i2 Trading，Grapefruit Trading和Tantra Labs的提案的投票于9月4日开始，他们都非常具有竞争力，因为这3个提案在发布时都有50-62％的支持。有关详细信息，请参阅治理部分。

## 隐私保护

@ jy-p [分析](https://blog.decred.org/2019/08/21/Surveying-the-Privacy-Landscape/)隐私保护领域的博客文章于8月21日发布。本文考虑了与加密货币隐私保护的不同方案相关的权衡，并回顾了Monero，Zcash，Grin，Beam，Dash，Bitcoin的Wasabi钱包所采用的方案的优缺点。

由Company 0秘密开发的隐私功能的首个细节由@jz 于8月27日在一集 Laura Shin的[Unchained Podcast](https://unchainedpodcast.com/after-years-of-secret-work-decred-adds-a-new-feature-privacy/)上公开发布。

8月28日，@ jy-p[发布](https://blog.decred.org/2019/08/28/Iterating-Privacy/)了一篇博客文章，全面介绍了Company 0对隐私保护的态度，并解释了选择这种方案的原因。仅考虑了允许修剪已用完交易的方法，优先选择不复杂的解决方案，以保持DCR底层供应的可审计性。这篇[推文](https://twitter.com/decredproject/status/1166746979160023046)提供了更简洁的介绍，@ Dustorf还撰写了一篇[文章](https://medium.com/@dlefebvr/decred-privacy-taking-the-long-road-62d218223db6)，该文章考虑了隐私的重要性，并提供了关于新方案如何运作的技术复杂性较低的观点。@ jy-p也录制了一个小时的[视频](https://twitter.com/decredproject/status/1168558002867191808)与@anshawblack关注隐私的深度讨论，他讨论了从逃避监视资本主义及怎样的隐私保护方案适合Decred的主题。@anshawblack和GhostWridah还合作了1分钟关于Decred和隐私的[rap](https://soundcloud.com/decredindepth/privacy-flow/s-5ifuN)。

该方法基于CoinShuffle++协议，集成到购买选票流程中，以便利益相关者可以选择在购买选票时混合他们的DCR。较小的面额也可用于常规混合（非POS）交易。该协议解决了底层可追溯性（匿名保护发送者和接收者）但不隐藏金额。该解决方案依赖于集中式服务器来协调混合 - 有关输入地址和更改地址的信息输入到到服务器，并且输出地址是完全匿名的。由于混合发生在链下，因此不需要改变共识规则。所有的开发都是由Company 0资助的，因此也不需要Politeia为此开发提供资金。

初始版本仅适用于命令行界面CLI dcrwallet的用户。将混合集成到decrediton还需要一段时间，并且为了向VSP用户提供混合，需要对dcrstakepool进行重大改进。从长远来看，将考虑保密交易。这些可以用来隐藏金额，这将提高隐私，避免交易中出现大量混合变量的需要。这种方式需要改变共识规则，未来或将通过链上治理途径。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 新命名的模块blockchain/standalone[发布](https://github.com/decred/dcrd/pull/1808)，其目的是提供几个目前可用的独立功能 区块链 模块。通过单独的模块提供这些功能的主要目的是减少客户端代码的依赖性。对于需要确保基本安全属性保持并计算适当的选票的轻量级客户端等应用程序也是有益的。我们有机会编写更强大，更高效的函数，这些函数将取代 区块链 下一个主要版本中模块中的函数。新模块将附带全面的测试，完整的文档和基本用法示例。

新的主要版本[`blockchain`](https://github.com/decred/dcrd/pull/1823), [`mining`](https://github.com/decred/dcrd/pull/1831), [`connmgr`](https://github.com/decred/dcrd/pull/1833), [`peer`](https://github.com/decred/dcrd/pull/1834) 和 [`mempool`](https://github.com/decred/dcrd/pull/1835)模块已被引入到使用其它新的主要模块的版本。主要模块也进行了[更新](https://github.com/decred/dcrd/pull/1837)，以便全面使用它们。总体好处是它更新dcrd以利用所有最新的代码更新，并在需要API更改构成主要语义版本控制中断时，显着减少某些模块中所需的未来流失量。

`gcs`模块得到了多项 [改进](https://github.com/decred/dcrd/pulls?q=is%3Apr+is%3Aclosed+merged%3A2019-08-01..2019-08-31+gcs)，使其达到共识代码所要求的质量水平，详细细节在[header commitments](https://proposals.decred.org/proposals/0a1ff846ec271184ea4e3a921a3ccd8d478f69948b984445ee1852f272d54c58)中。[添加](https://github.com/decred/dcrd/pull/1854)了独立的误报率和Golomb译码窗口尺寸。除此之外，这允许更优化的参数以最小化要指定的滤波器尺寸。此功能将用于即将发布的版本2过滤器中，最终将包含在标头承诺中。模块的v2开发周期的开始也标志着在发布周期之间处理模块版本控制的[新方法](https://github.com/decred/dcrd/pull/1843)的开始，以减少维护负担。

Blake256实现已被[复制到](https://github.com/decred/dcrd/pull/1811)dcrd存储库中，因此dcrd不再具有外部依赖性。虽然dcrd所需的优化是在上游[接受](https://github.com/dchest/blake256/pull/3)的，但仍然需要在dcrd维护者的严格控制下使用共识关键代码以避免[此处](https://github.com/decred/dcrd/issues/1810)提到的情况。

自动地址发现已[合并](https://github.com/decred/dcrd/pull/1522)。它允许NAT后面的用户运行可公开发现的完整节点而无需指定`--externalip`。

测试覆盖率在代码库的多个区域中得到增强。

工作[开始](https://github.com/decred/dcrd/pull/1829)根据mempool中的事务链最大化块模板费用。

[dcrwallet](https://github.com/decred/dcrwallet): 添加了一个新的[RPC](https://github.com/decred/dcrwallet/pull/1522)，允许用户从钱包中放弃（或删除）未经证实的事务，以及依赖于其输出的任何其他事务。另一个新的RPC允许在解锁钱包后导出帐户的[扩展私钥](https://github.com/decred/dcrwallet/pull/1533)。

代码维护：更新dcrd中的新模块并[删除](https://github.com/decred/dcrwallet/pull/1531)旧模块的使用，[改进](https://github.com/decred/dcrwallet/pull/1539)了与Go 1.13错误的兼容性。

工作已经开始增加对购买“拆分”交易的门票交易的CoinJoin交易的[支持](https://github.com/decred/dcrwallet/pull/1541)，以及将各个组合变更输出混合成较小的标准数额。

[Decrediton](https://github.com/decred/decrediton): UI调整，BUG修复，代码清理。

初始[夜间模式](https://github.com/decred/decrediton/issues/2089)已完成。继续使用UI[响应](https://github.com/decred/decrediton/pull/2163)，[添加](https://github.com/decred/decrediton/pull/2174)了四个新的响应视图。

[Politeia](https://github.com/decred/politeia): 在Politeia重新设计工作正在进行，在步伐，以[数量](https://github.com/decred/politeiagui/pull/1356) [的](https://github.com/decred/politeiagui/pull/1338) [PRs](https://github.com/decred/politeiagui/pull/1360)合并是增加现有功能的重新设计的界面。在后端，为[DCC流程](https://proposals.decred.org/proposals/fa38a3593d9a3f6cb2478a24c25114f5097c572f6dadf24c78bb521ed10992a4)奠定基础的重要工作已[合并](https://github.com/decred/politeia/pull/980)到CMS中。

关于如何支持关于Politeia的RFP类型提案的[问题](https://github.com/decred/politeia/issues/966)一直是本期和#politeia 讨论的主题（更多细节见治)。

用户名登录后切换回电子邮件以防止有[针对性地锁定](https://github.com/decred/politeia/issues/860#issuecomment-520871500)帐户。[2FA](https://github.com/decred/politeia/issues/544)将解决此问题并无需电子邮件登录。

[dcrdex](https://github.com/decred/dcrdex): dcrdex存储库于7月宣布[收纳](https://twitter.com/decredproject/status/1156652694502817793)DEX[规范](https://github.com/decred/dcrdex/tree/master/spec)，第一批实质性PR已经[开放](https://github.com/decred/dcrdex/pull/17)。还为Matrix上的DEX开发聊天创建了一个新的[#dexdev](https://riot.im/app/#/room/!EzTSRQITaqHuFBDFhM:decred.org)聊天室。

[cspp](https://github.com/decred/cspp): 这个新的存储库提供客户端和服务器实现来执行[CoinShuffle++](https://crypsys.mmci.uni-saarland.de/projects/FastDC/paper.pdf)混合协议。虽然旨在用于创建Decred CoinJoin事务，但客户端和服务器包的通用性足以匿名混合和连接任何其它的元素。

在CoinShuffle ++之前，Company 0开发了TumbleBit协议的Go语言实现。尽管没有将它集成到Decred中，但代码是在[tumblebit](https://github.com/decred/tumblebit)存储库中为公共利益发布的。

[dcrstakepool](https://github.com/decred/dcrstakepool): 从4月份开始的将dcrstakepool与dcrwallet分离的大量[工作](https://github.com/decred/dcrstakepool/issues/227)终于[完成](https://github.com/decred/dcrstakepool/pull/470)了。此次更新降低了代码复杂性并减少了通过网络rpc调用的数量，从而提高了性能和安全性。

VSP运营商获得了对SMTPS的支持，通过加密连接（包括自[自签名证书](https://github.com/decred/dcrstakepool/pull/486)），改进的[状态页面](https://github.com/decred/dcrstakepool/pull/484)和更好的错误报告来发送注册和帐户恢复电子邮件。

添加了tmux[测试工具](https://github.com/decred/dcrstakepool/pull/476)以提高测试效率。

共有[30个PR](https://github.com/decred/dcrstakepool/pulls?q=is%3Apr+is%3Aclosed+merged%3A2019-08-01..2019-08-31)合并。

[dcrlnd](https://github.com/decred/dcrlnd):8月合并的工作涉及改进测试的稳定性和支持使用现有钱包的初始工作（目前仅支持嵌入dcrlnd的钱包）。

在dcrlnd合并之前，更多的上游工作被[移植](https://github.com/decred/dcrlnd/pull/36#issuecomment-526721084)并正在测试。共调整了400多个PR和1700多行代码。

> 为了保持同步，我们需要在1月10日合并点之后调整几乎所有的提交([@matheusd](https://twitter.com/matheusd_tech/status/1169194706636615680))

lightning-faucet获得了[支付发票](https://github.com/decred/lightning-faucet/pull/8)和新配置参数的 [表格](https://github.com/decred/lightning-faucet/pull/14)。

[dcrandroid](https://github.com/decred/dcrandroid): 正在努力实现[新的用户界面](https://github.com/decred/dcrandroid/pull/400)，这将使应用程序与Android的标准应用程序设计建议保持一致。后端的工作也在进行[多钱包](https://github.com/decred/dcrandroid/issues/188)支持，这将使[仅限观察](https://github.com/decred/dcrandroid/issues/393)的钱包用于选票监控。

[dcrios](https://github.com/raedahgroup/dcrios):改进的用户界面和仅限观察的钱包支持工作正在进行，类似于Android应用程序。

[dcrdata](https://github.com/decred/dcrdata):整合了来自dcrd的升级，UI调整，优化和BUG修复。

长期以来，todo列表中的一个重大变化是[删除 SQLite](https://github.com/decred/dcrdata/pull/1480)。这使得数据库体系结构更加简单，只需要postgresql，并构建cgo-free（纯go，没有c）。

重新设计正在加速，但后端开发主要处于维护模式，因为主要贡献者将重点转向dcrdex。dcrdata的改进和扩展仍有很大空间，特别是对于混合交易。

[docs](https://github.com/decred/dcrdocs): [添加](https://github.com/decred/dcrdocs/pull/968)了一个新的页面，详细说明了[原子交换](https://docs.decred.org/advanced/atomic-swap/)，更新了[硬件钱包](https://docs.decred.org/wallets/hardware-wallets/)的支持信息，并清理了部分内容。

工作已经开始在一个长期要求的单独的开发人员文档站点上。最初的工作是在个人存储库中进行，当该网站启动时，该存储库将在主要的Decred GitHub组织下活动。

[decred.org](https://github.com/decred/dcrweb): 路线图已经[更新](https://github.com/decred/dcrweb/pull/695)，[新闻报道页面](https://github.com/decred/dcrweb/pull/706)更新了最近的报道，并在主页和路线图中[添加](https://github.com/decred/dcrweb/pull/712)了隐私。

8月的开发活动统计数据：244个活动PR，274个主要提交，46K添加和24K删除的行分布在15个存储库中。贡献来自每个存储库2-9个开发人员。

## 人员

欢迎来到Decred的首次贡献者：aarcamp([dcrd](https://github.com/decred/dcrd/commits?author=aarcamp))，skipcheru([dcrandroid](https://github.com/decred/dcrandroid/commits?author=skipcheru))，RyanBRiley([politeia](https://github.com/decred/politeia/commits?author=RyanBRiley))，UferePease([dcrstakepool](https://github.com/decred/dcrstakepool/commits?author=UferePease))，fguisso([lightning-faucet](https://github.com/decred/lightning-faucet/commits?author=fguisso))。

社区数据统计:

* Politeia 用户: 174 (+20)
* Twitter 粉丝: 40,597 (+25)
* Reddit 订阅: 9,594 (+38)
* Matrix 用户: 412 (+28)
* Slack 用户: 6,834 (+25)
* Discord 用户: 2,442 (+65), verified to post: 310 (+29)
* Telegram 用户: 3,148 (-142)
* YouTube 订阅: 3,819 (+19)
* Facebook 粉丝: 3,271 (+18), likes: 2,999 (+16)
* LinkedIn 粉丝: 603 (+12)
* GitHub dcrd 星星: 516 (+18), 分叉: 1,383 (+18)

在胡志明市举办的[活动](https://github.com/decredcommunity/events/blob/master/reports/20190725-cointime-summit-ho-chi-minh-city-vietnam.md) 之后，已经创建了越南[Telegram](https://t.me/decredvietnam), [Twitter](https://twitter.com/DecredVietnam) and [Facebook](https://www.facebook.com/Decred-DCR-Vietnam-108991833777572/)帐户。所有Decred社交媒体组的列表都在[这里](https://github.com/decredcommunity/wiki/blob/master/wiki/social-media.md)。

## 治理

8月，[社区开发基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了15,278个DCR，并花费了8,223个DCR。使用8月份的每日平均DCR / USD为26.23美元，约收到的401,000美元。由于这些付款用于7月完成的工作，因此在7月平均每日费率28.97美元的情况下考虑它们也是有用的 - 在这种情况下，美元花费是238,000美元。截至8月9日，财政部余额为638,000 DCR（1580万美元，汇率24.80美元）。

来自@chappjc和@ buck54321（在dcrdata上工作）的DEX开发[提案](https://proposals.decred.org/proposals/417607aaedff2942ff3701cdb4eff76637eca4ed7f7ba816e5c0bd2e971602e1)在Company 0的支持下提交 - 并获得90％赞成票批准。该提议的成本估计为230,000美元，用于提供命令行界面应用程序，可以通过未来的提议进行扩展，以使用Electron框架提供用户界面。

decred社区提案[库](https://github.com/decredcommunity/proposals)具有DEX相关材料的 [索引](https://github.com/decredcommunity/proposals/blob/master/dex/index.md)。

3个做市商的提案于8月7日发布，来自[Altonomy](https://proposals.decred.org/proposals/772d083fef79fa2e443d8424b353deadc3af69c8d8764e473cb200f98f356c60), [i2 Trading](https://proposals.decred.org/proposals/2eb7ddb29f151691ba14ac8c54d53f6692c1f5e8fe06244edf7d3c33fb440bd9) 和 [Grapefruit Trading](https://proposals.decred.org/proposals/4becbe00bd5ae93312426a8cf5eeef78050f5b8b8430b45f3ea54ca89213f82b)。经过几天的讨论，主要议题是社区开发基金是否应该习惯于雇佣做市商。@jz提交了一份[RFP 提案](https://proposals.decred.org/proposals/30822c16533890abc6e243eb6d12264b207c3923c14af42cd9b883e71c7003cd)，以确定利益相关者原则上是否希望雇用指定的做市商。该提案解释了@jz，@ maxbronstein和Chris Burniske在提交提案之前已经采取的流程 - 并提出了批准其中一项提案的案例。RFP提案还澄清了投票条款（最多可以批准1个做市商提案，并且必须符合通常的标准）。

Altonomy提交了一项建议，即10个交易对供5万美元，他们积极参与Politeia并提供许多问题的答案，但在8月16日他们撤回了他们的建议，编辑它说“对不起，由于我们的技术能力，我们决定撤回这个提议。

i2 Trading提交了一项建议，即对6个交易对提供5万美元，他们积极参与Politeia和#proposals聊天室，回答大多数问题。为了回应对透明度的担忧，i2允许在一段有限的时间内允许Decred代表以只读方式访问其交易账户。i2对他们的提案进行了一些编辑，添加了关于提供API访问的说明，澄清借款需求和条款，然后修改他们的提议以放宽差价，将最高交易费用报销减少到10K /月，并且下降提供服务的费用从每月4万美元到每月35,000美元。

Grapefruit在他们的提案中开始提供2个优惠（两个价格均为3对3万美元），其中一个价格较低，每月费用为4万美元，另一个价格较宽松，每月费用为28,000美元。@grapefruittrading于8月8日和20日回答了关于Politeia的问题，在向其他人提供[实质性](https://proposals.decred.org/proposals/4becbe00bd5ae93312426a8cf5eeef78050f5b8b8430b45f3ea54ca89213f82b/comments/6) [回复](https://proposals.decred.org/proposals/4becbe00bd5ae93312426a8cf5eeef78050f5b8b8430b45f3ea54ca89213f82b/comments/5)时忽略了一些问题。在授权投票开始之前，@ grapefruittrading编辑了他们的建议删除了更昂贵的报价，选择运行较便宜的报价，因为他们认为来自利益相关者的需求，无论如何这是他们的首选。

i2 和 Grapefruit 授权8月27日开启提案投票。

Tantra Labs于8月28日提交了一份[提案](https://proposals.decred.org/proposals/82ce113827140caaaf8b5779ab30402d3ed39f1911fdd2e8fa64cf0dc9e09ecb)，提出了一个非常不同的提议，每个交易对3万美元，6个交易对([或 7](https://proposals.decred.org/proposals/82ce113827140caaaf8b5779ab30402d3ed39f1911fdd2e8fa64cf0dc9e09ecb/comments/8))对最高3％的差价，并且向提供给社区开发基金的服务不收取任何费用。相反，社区开发基金只收取借入库存的成本和交易费10,000美元/月的费用。Tantra Labs只允许他们的交换账户访问“当选”的Decred代表，以便可以验证所承诺的流动性可用性。Tantra还为一组开源订单簿透明工具提供了一个Web界面。

关于Tantra的提案的大部分讨论都关注它是否太好而不是真实的，有许多人表达了他们对Tantra可以兑现他们的建议的疑虑，并想知道低成本是否伴随着隐藏的缺点。Tantra一直活跃在#proposals，并回答了有关Politeia的一些问题。社区的一些成员越来越不耐烦等待Tantra授权开始投票，这表明RFP提案被迟交的提议放慢了问题，并强调了明确的时间表的价值。

由@betterfuture提交的关于做市商的第四个[提案](https://proposals.decred.org/proposals/c9604f7879e4b2cd4f2582d238a7ccea210005c63481bec1ddae44ff93e1340f)于8月31日发布。这提出了一个激励做市商在没有坚定承诺的情况下为特定货币对提供流动性的计划。该提案描述了使参与者保持一致的规则和处罚，并且需要代表Decred项目的可信中介来审核做市商的活动。@jz在提案中被提名担任此角色，但他[表示](https://proposals.decred.org/proposals/c9604f7879e4b2cd4f2582d238a7ccea210005c63481bec1ddae44ff93e1340f/comments/5)他不希望接受。对该提案的审议和改进被其支持者视为长期努力，并且不会与其他提案竞争。

9月4日，3个做市商提案开始投票。

有关做市商提案和其他Politeia活动的更详细考虑，请查看Politeia Digest 第[20](https://github.com/RichardRed0x/politeia-digest/blob/master/issue-020.md)期（8月1日至12日）和第 [21](https://github.com/RichardRed0x/politeia-digest/blob/master/issue-021.md)期（8月13 日至31 日）。还有一些社区生产的资源，旨在帮助那些不熟悉市场营销理念的人理解它，并在不同的提案之间进行比较：

* [这里](https://github.com/decredcommunity/proposals/blob/master/market-makers/index.md)保留了所有着名文件的索引以及与做市商相关的讨论。
* [comparison table](https://github.com/decredcommunity/proposals/blob/master/market-makers/comparison.md) 旨在比较其提议和成本方面的建议 - 本表中估计的最高月费为Tantra为17,000美元，i2为$ 53K，Grapefruit为$ 31K（对于Tantra和i2最高交易费为$ 10,000 /假设是月份。
* @bee撰写了关于具体问题和论点的讨论的[全面概述](https://github.com/decredcommunity/proposals/blob/master/market-makers/arguments.md)，并详细解释了该[主题](https://github.com/xaur/writings/blob/master/20190822-dissection-market-makers-for-decred.md)，介绍了相关术语并概述了关键考虑因素。
* @exitus制作了一个相关的[Politeia视频概述](https://www.youtube.com/watch?v=BKSMA-eanoY)。

在#research频道中进行讨论之后，@ richardred开始收集该[存储库](https://github.com/RichardRed0x/exchange-data)中选择的交易对和交换的订单簿数据。目标是更好地了解目前DCR和其他选定加密模块的订单如何看，并在做市商提案投票之前准备了初步报告。如果雇佣了这些数据，这些数据也可用于跟踪订单簿，以观察做市商的影响。订单簿数据可能会在某个阶段添加到dcrdata的外部数据产品中，但这些数据的性质是只能实时记录。历史订单簿数据的唯一来源是专有且[昂贵](https://www.kaiko.com/products/binance-10-order-books)的。

值得一提的是Decred社区提案 [存储库](https://github.com/decredcommunity/proposals)，其中可以找到许多上述资源。创建此存储库是为了收集讨论和分析提案时产生的信息。

处理做市商提案和RFP流程已经产生了很多讨论和见解，并且正在准备Politeia的RFP功能的初始集成。将有一个新的RFP类型提案，候选提案可以链接，投票和确定选项/结果将通过这些RFP提案进行控制。在开启RFP提案之前，将提交并批准一份普通提案，询问“我们是否应该提供此RFP” - 迄今为止Politeia所见的2个“RFP提案”属于此类提案。

关于新的RFP提案类型的讨论主要是围绕这些是否应该作为多项选择提案（选民可以投票选出1-N选项和获得最多选票的选项）或者作为票数可以平行提案对每个提案投赞成票/否，并且获胜者是具有最高投票权的投票总得分（因为MM RFP正在进行）。竞争提案的平行投票似乎是优先考虑的事项，多选投票可能会在以后出现，并用于不同的目的（更像是民意调查）。

提交了一份Reddit [讨论](https://www.reddit.com/r/decred/comments/cutc16/decred_events_meetups_in_the_cis_in_20192020/)以供反馈，该提议旨在作为独立国家联合体（CIS） - 特别是俄罗斯，乌克兰和格鲁吉亚的Decred活动和聚会的筹资预案。


## 网络

全网算力：八月份的哈希值约为563 Ph/s起步，收于约567 P/s，最低时达到374 Ph/s，最高达到671 Ph/s。截至9月5日的池哈希值分布：F2Pool 23％，UUPool 16％，Poolin 16％，lab.antpool.com 4.1％，BTC.com 2.3％，Luxor 1.8％，BeePool 0.10％，Coinmine 0.10％，suprnova 0.01％和其他36％每个[dcrstats.com](https://dcrstats.com/pow)。池分布数是近似值，无法准确确定。

Staking: 每个dcrstats.com的30天平均票价为130.05 DCR（+4.25）。价格在119.9-134.5 DCR之间变化。锁定金额为5.03-5.25百万DCR，相当于现有供应量的49.40-50.93％。

节点: 整个[8月份](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1564617600000&to=1567296000000)，每个dcr.farm大约有167个监听节点和445-530个总节点。大约78％运行dcrd v1.4.0,5.7％运行dcrwallet v1.4.0,6.2％运行v1.5.0（预）dev版本。

截至9月5日，DCR[闪电网络测试网](https://charts.dcr.farm/d/DHPdAO4Wz/lightning-network?orgId=1)显示拥有19个节点，32个通道，总容量为253 DCR。

已经检测到使用新隐私协议的第一笔[交易](https://twitter.com/decredproject/status/1167269901293297664)。

## 整合

Exodus [增加了](https://twitter.com/exodus_io/status/1168886493617840131)向他们的移动钱包发送，接收和交换DCR的能力。

Ellipal冷钱包宣布他们即将[推出](https://twitter.com/ellipalwallet/status/1163771448042803201)的硬件钱包Titan将支持Decred。

注意：Decred Journal的作者不知道上述任何服务的可信度。在将您的个人信息或资产信任托管给任何第三方实体之前，请先自行研究。

## 外联活动

由于我们专注于Decred隐私的发布，因此大部分正在进行的Outreach工作被推到一边。8月21日开始努力，@ jy-p发布了“[Surveying the Privacy Landscape](https://blog.decred.org/2019/08/21/Surveying-the-Privacy-Landscape/)”。这项工作得到了一个[tweetstorm](https://twitter.com/decredproject/status/1164245224274767873)的支持，这个[tweet话题](https://twitter.com/decredproject/status/1164245224274767873)吸引了fluffypony（门罗首席开发者），Zooko（Zcash创始人)，MimbleWimble协议开发人员（Girn，Beam）等参与。当@jz继续使用Laura Shin的[Unchained Podcast](https://unchainedpodcast.com/after-years-of-secret-work-decred-adds-a-new-feature-privacy/)谈论Decred及其新功能时，隐私的第一个细节就披露了。

二十四小时后，Decred隐私的第一份书面消息释放，在@ JY-P的文章，出版了迭代隐私，其中深入探讨动机，操作细节，限制和Decred的下一步[隐私](https://blog.decred.org/2019/08/28/Iterating-Privacy/)。这得到了大量[支持](https://twitter.com/decredproject/status/1166746979160023046)，并引起了很多关注和参与。除了CoinDesk之外，Decred的隐私实施已经获得了大量报道，在Media中有详细介绍。

为了继续支持隐私保护功能的发布，@ anshawblack在GhostWridah上发布了[Privacy Flow](https://twitter.com/decredproject/status/1169011789255925762)，并在发布后的几天内发布了一个非常特别的Decred in Depth [音频](https://twitter.com/decredproject/status/1168558002867191808) @ jy-p。在这个音频中，@ jy-p深入研究了监管经济，为什么要保护隐私，以及当前和未来的Decred隐私状态。

在发布时，Ditto团队继续致力于将Decred隐私放在首位。此外，@ Dustorf发布了针对非技术相关人群的[博客概述](https://medium.com/@dlefebvr/decred-privacy-taking-the-long-road-62d218223db6)。

Outreach通过关于Decred的高质量内容和教育，共同努力提高Twitter的参与度。从7月到超过560万，项目印象数增加了一倍以上。获得最多吸引力的消息之一是关于DEX规范公告的4部分[tweet风暴话题](https://twitter.com/decredproject/status/1156652694502817793)。

Decred已于11月4日至7日在葡萄牙里斯本的[网络峰会](https://websummit.com/)上确认其展位，如果您有兴趣帮助我们，请在Matrix的#event_planning会议室与我们联系。我们还计划在亚洲举办路演，但在发布时没有任何细节可供分享。

[基础消息](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md)已更新为v2。[更改](https://github.com/decredcommunity/pr/commit/fc407b8f037a222db22a4507e4a5ade5b746f4dd)包括使用Decred原则和常见问题解答扩展的Pitch，Tagline和Vision。Tagline稍作调整，以“可持续”取代“自筹资金”。

Ditto八月的成就:

* 到目前为止，在隐私发布方面获得了8项成就 - 这包含在所有顶级加密媒体中：Unchained Podcast，[The Block](https://www.theblockcrypto.com/tiny/crypto-project-decred-adds-privacy-features-to-its-coin/)（也在其时事通讯中提到），[Crypto 简报](https://cryptobriefing.com/decred-struts-privacy-credentials-with-surprisingly-awesome-rap-snippet/)时事通讯专题和关于Privacy Rap的文章（对@anshawblack的赞誉）），[Cointelegraph](https://cointelegraph.com/news/crypto-project-decred-adds-privacy-features-to-its-coin), [Decrypt Media](https://decrypt.co/8796/decred-aims-to-be-a-more-effective-privacy-coin-than-monero-or-zcash), [Modern Consensus](https://modernconsensus.com/cryptocurrencies/alt-coins/decred-cryptocurrency-launches-launches-privacy-mixing-feature/)，俄语新闻网站[Forklog](https://forklog.com/menshe-koda-menshe-vzloma-razrabotchiki-kriptovalyuty-decred-dobavili-optsiyu-privatnosti-tranzaktsij/)，西班牙语新闻网站[Criptonoticias](https://www.criptonoticias.com/redes-protocolos/decred-anade-privacidad-criptomoneda-dcr/)。
* 今年的成就：对Laura Shin's Unchained的独家突破性报道（对于@jz的不可思议的交付感到荣幸） - 我们已经努力确保6个月以上，并且它终于发生了！
* 与感兴趣的社区成员协调，为Decred的教育资源库聚合互联网上的最佳资源。如果你有宝藏，请分享隐藏的宝藏。
* 继续与各社区成员合作，在Twitter上采用富有成效/教育的方式。这包括与7名社区成员通话，讨论社交媒体手册策略，反馈和提问。
* 围绕Decred隐私创造了热门话题，24小时内发布了大约85条推文，上周发布了近400条，包括来自Chris Burniske，Justin Yashoufar（Blockhead Capital），Blockfolio，Max Bronstein（DharmaHQ）和Weiss Reports的对话和推文。
* 围绕隐私新闻进行协调的推特和社区外展活动。
* 预计将在未来几周内再发布另外2个播客采访。
* 获得Decrypt Media项目负责人@ jy-p的深入剖析。
* 发布@ akinsawyerr对[Base Layer Podcast](https://acrabaselayer.podbean.com/e/base-layer-episode-059-akin-sawyerr-decred/)的采访。
* 关于做市商提案的安全加密简报[文章](https://cryptobriefing.com/decentralized-governance-in-action-decred-debates-market-liquidity/)。
* 刷新[消息](https://github.com/decredcommunity/pr/blob/release/foundational-messaging.md)传递。
* 为@matheusd撰写并提交了一份提案，在柏林闪电会议上发言。
* 在多伦多未来主义者大会上获得了@zubair的电视采访。

## 社区活动

出席：

* 7月2 - 3日 - 2019年亚洲区块链峰会 - 台湾台北。穿着Decred Jacket的@morphymore在那里出席，并向那些想要了解该项目的人介绍Decred。
* 月8日 - [Blockchain Bajio](https://www.eventbrite.com/e/blockchain-bajio-2do-meetup-tickets-66510186759) - 墨西哥莱昂。@elian，@ francov_，@victorarubin和@luisantoniocrag 向约60位与会者展示了Decred 的高级[概述](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156537300012257UWNLZ:decred.org)。（照片：[1](https://twitter.com/Decred_ES/status/1159621068027551744) [2](https://twitter.com/victorarubin/status/1159898002858893313)）
* 8月12日 - [Crypto Mondays](https://www.meetup.com/Bitcoin-Argentina/events/263594472) - 阿根廷布宜诺斯艾利斯。第一次在Espacio比特币，@ pablito和@camilolwi有15分钟的时间向当地比特币社区和其他项目的成员解释 Decred最相关的方面。([照片](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156570965016592IkfFu:decred.org))
* 8月13日 - 未来主义者会议 - 加拿大多伦多。@ michae2xl，@ zubair和@ammarooni在展位上进行了一些采访，并在“Blockchain Social Impact＆Governance for Good”小组讨论。Decred是一名银牌赞助商。（照片：[1](https://twitter.com/Decred_CA/status/1161466609267105792) [2](https://twitter.com/Ammarooni/status/1161707860822302722) [3](https://twitter.com/Decred_CA/status/1161982417781047297) [4](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156581155118027SCAXO:decred.org)）
* 8月16日 -  [Campus Party](https://brasil.campus-party.org/campus-party-natal/) - 巴西纳塔尔。@guisso和@claranobre代表Decred。（[照片](https://twitter.com/Decred_BR/status/1163473134676258816)）
* 8月20日 - Bitcoin Embassy - 墨西哥墨西哥城。@elian被邀请到比特币大使馆接受El Financiero（Bloomberg在墨西哥的分支机构）的[采访](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15664995075484PTrhJ:decred.org)，谈论墨西哥的加密货币。（照片：[1](https://twitter.com/LOR_ena_OR/status/1164205626723098630) [2](https://twitter.com/bitcoinemb/status/1164269677381652480)）
* 8月21日 - [Decred Meetup](https://www.meetup.com/Chicago-Decred-Meetup/events/263814807/) - 美国芝加哥。
* 8月22日 - [Binance Meetup](https://www.facebook.com/events/406522099975717/) - 墨西哥蒙特雷。@elian和@francov_代表Decred。（照片：[1](https://twitter.com/binance/status/1166526786525487105) [2](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15665195371107618foQnv:matrix.org) [3](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15666946921832943HyclD:matrix.org)）
* 8月24日 - [Decred Live AMA](https://twitter.com/coin98_net/status/1164845587910414337) - 互联网。@Haon和ViệtAnhĐàm在他们的Facebook页面上回答了Coin98组织的越南社区提出的问题。总共有309条评论（包括答案），对于最佳问题，DCR的奖励为50美元。（[获奖名单](https://github.com/noahpierau/articles/blob/master/Decred-Vietnam-AMA.md)）
* 8月25日 - [币印中国行](https://twitter.com/wanbihou/status/1166028812305321985) - 中国上海。@dominic受邀出席主题演讲和圆桌讨论。
* 8月28日 - [Blockchain Bootcamp](https://www.meetup.com/blockchaincentre/events/263601014/) - 澳大利亚Docklands。安永会计师事务所[邀请](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156739040517633gdQNG:decred.org) @zohand和@eSizeDave为来自学术界，商界，法律界和政府部门的代表举办关于区块链治理的Decred特定演讲。演示文稿和Decred都很受欢迎，导致了许多后续活动。（[照片](https://twitter.com/DecredAustralia/status/1166592295296208896)）
* 8月29日 - [Binance Meetup](https://twitter.com/Decred_ES/status/1166132690342567938) - 墨西哥城，墨西哥。@elian [指出](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156713369714381PAoax:decred.org)：“我们有大约60名与会者，主要是爱好者和企业家，对Decred的隐私实施和治理即服务的想法很感兴趣。非常感谢@francov_ @luantantoniocrag和@victorarubin的帮助去”。（照片：[1](https://twitter.com/TRADcoinMX/status/1168541349395738624) [2](https://twitter.com/interprocsys/status/1167243076726861824) [3](https://twitter.com/victorarubin/status/1167495971539836928)）

即将到来的:

* 9月10日 - [BlockDAM Co-working Tuesdays](https://twitter.com/NoahPierau/status/1170198038301855745) - 荷兰阿姆斯特丹。@Haon将发表关于加密货币隐私技术和Decred的新隐私功能的演讲。
* 9月16日 - [Decred Special Interest Group](https://www.meetup.com/Philadelphia-Technology-for-Blockchain-and-Cryptocurrency/events/hmqlhryzmbvb/) - 美国费城。由[@mikeghen](https://twitter.com/mikeghen)组织。
* 9月20日 - [A Framework for Blockchain Governance](https://www.eventbrite.com/e/a-framework-for-blockchain-governance-tickets-70134180221) - 美国华盛顿特区。与[StrongBlock](https://strongblock.io/)的首席治理官Thomas Cox 一起，@akinsawyerr正在就区块链治理框架发表演讲并提出问题，开发了他所属的Wharton Crypto Governance圆桌会议组。
* 9月21日 - [French Vibes Connection](https://twitter.com/Decred_ES/status/1160669435989856256) - 墨西哥城，墨西哥。Decred将与Telepopmusik，Cherokee和Else共同举办音乐会。@elian的品牌意识实验。
* 9月21日 - [Decred Meetup](https://twitter.com/DecredArabia/status/1171117988461854721) - 摩洛哥卡萨布兰卡。@arij将谈论她作为Decred承包商，Decred的治理和隐私以及未来计划的经验。
* 9月25日 - [La Conexion Conference](https://la-conexion.com/home/) - 阿根廷布宜诺斯艾利斯。该项目将在主要阶段提出。
* 9月26日 - [Inaugural Decred Meetup](https://twitter.com/MattDavidKaye/status/1164974520081342464) - 洛杉矶，美国。Blockhead Capital和@ jy-p将讨论Decred背后的基本面。
* 9月27日 - [Crypto Fest](https://argentinacryptofest.com/)。该项目将在主要阶段提出。
* 9月30日 - 10月1日 - [Voice of Blockchain](https://twitter.com/BlockchainVoice/status/1154772731575099392) - 美国芝加哥。@ jy-p将发表主题演讲“为什么直接主权和多利益相关方包容性治理将持续”。
* 10月29日至31日 - [World Crypto Conference](https://worldcryptocon.com/) - 美国拉斯维加斯。@akinsawyerr将在“治理实践”小组发言，并将有机会突出Decred治理模型和流程。
* 11月4日至7日 - [Web Summit](https://websummit.com/) - 葡萄牙里斯本。Decred将有一个展位。

Alex Von Schulze正在[寻找](https://twitter.com/avonschulze/status/1166026265805172737 )人们在美国堪萨斯城组织首次Decred [meetup](https://www.meetup.com/Decred-KC/)。


## 媒体

精选文章：

* Decred | 自我思考的力量 @BlackBearXVII ([medium](https://medium.com/@imagnusholdings/decred-the-power-to-think-for-oneself-46b9aab9ff0e))
* Decred Q&A with @elian for Crypto Hispano ([steemit](https://steemit.com/btc/@cryptohispano01/decred-q-and-a))
* Decred去中心化交易所雄心勃勃的愿景 by Nate Urbas ([cryptolinks.com](https://cryptolinks.com/news/decreds-ambitious-vision-for-a-truly-decentralized-exchange))
* 实现去中心化治理: Decred 争论市场流通性 by Darren Kleine ([cryptobriefing.com](https://cryptobriefing.com/decentralized-governance-in-action-decred-debates-market-liquidity/))
* 探索隐私币生态 by @jy-p ([blog.decred.org](https://blog.decred.org/2019/08/21/Surveying-the-Privacy-Landscape/))
* 迭代隐私 by @jy-p ([blog.decred.org](https://blog.decred.org/2019/08/28/Iterating-Privacy/))
* Decred 项目领导人 Jake Yocom-Piatt: 行动要和思想一致 by Matt Hussey ([decrypt.co](https://decrypt.co/8801/decred-project-lead-jake-yocom-piatt-interview-profile))

翻译:

* 探索隐私币生态 - [葡萄牙语](https://stakey.club/translated/privacy-landscape/) by @mm.
* Decred的7月月报被翻译成阿拉伯语（@arij），中文（@Dominic），4-7月月报被翻译成西班牙语（@francov\_ 和 @luisantoniocrag），波兰语（@kozel）和越南语（Duyen Em）。所有翻译的索引在[这里](https://xaur.github.io/decred-news/)。

视频：

* Decred的做市商提案 - 实现区块链治理! by @Exitus ([youtube](https://www.youtube.com/watch?v=BKSMA-eanoY))
* 无费用的Decred DEX被批准了! by @Exitus ([youtube](https://www.youtube.com/watch?v=An5YCY_q894))
* Futurist 19 访问 @ammarooni ([youtube](https://www.youtube.com/watch?v=YmQce50dfGY))

音频：

* Decred in Depth Ep. 6 with @jholdstock - Jamie谈到了他的Decred之旅，从空投接收者到兼职文档贡献者，最近过渡到全职开发人员，以及为什么这是一个有吸引力的选择。([youtube](https://www.youtube.com/watch?v=A-zcLGSYxbA))
* Decred in Depth Ep. 7 with @jy-p - Jake谈到隐私和资本主义的监控以及如何避免泄漏隐私，为什么Company 0觉得CoinShuffle++是最适合Decred的隐私技术，以及隐私对项目的重要性。([player.fm](https://player.fm/series/decred-in-depth/jake-yocom-piatt-dcr-privacy))
* Decred in Depth 音频已复制到[SoundCloud](https://soundcloud.com/decredindepth)和[Libsyn](https://decredindepth.libsyn.com/).
* Unchained Podcast Ep. 134 with Laura Shin - @jz全面介绍了Decred及他在项目里的角色，然后发布Decred新隐私功能的初始信息。([unchainedpodcast.com](https://unchainedpodcast.com/after-years-of-secret-work-decred-adds-a-new-feature-privacy/))
* Inclusionism: Akin Sawyerr评论什么是金钱 ([jamesfeltonkeith.com](https://www.jamesfeltonkeith.com/radioshow/episode/c3b1bb50/inclusionism-guest-akin-sawyerr-on-what-money-is), [soundcloud](https://soundcloud.com/inclusionism/inclusionism-guest-akin-sawyerr-on-what-money-is))
* Base Layer Ep. 59 - Akin Sawyerr (Decred) ([podbean.com](https://acrabaselayer.podbean.com/e/base-layer-episode-059-akin-sawyerr-decred/), [spotify](https://open.spotify.com/episode/6tT4PTA572I1PAbHsZEX6N))
* Decred使用令人惊讶的Rap片段推广隐私功能([cryptobriefing.com](https://cryptobriefing.com/decred-struts-privacy-credentials-with-surprisingly-awesome-rap-snippet/))

自4月份以来，Decred 月报一直在变得更去中心化。 这包括写下月报组成部分的描述以及制作它们的原因。 这个想法是，通过形式化各方面，月报变得不那么依赖于个别贡献者和他们的知识。以下文件可供希望成为月报贡献者参考，值得一看：

* 新月报的[范例文件](https://github.com/xaur/decred-news/blob/docs/journal-template.md)
* 全新的[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)页面
* [内容安排](https://github.com/xaur/decred-news/blob/docs/content.md)
* 详细的[指引](https://github.com/xaur/decred-news/blob/docs/guidelines.md) ，包括月报的理念和翻译的提示

## 社区讨论

通讯系统新闻：

* Reddit [讨论](https://www.reddit.com/r/decred/comments/coppup/i_did_a_review_of_the_powpos_mechanism_used_in/) 被管理者移除，因为作者在没有足够理据的情况下表示Decred的混合PoW+PoS系统并不可行。我们的管理是[透明的](https://snew.notabug.io/r/decred)，感谢[publicmodlogs](https://www.reddit.com/user/publicmodlogs)。
* Reddit [讨论](https://www.reddit.com/r/decred/comments/csc0ne/what_is_c0s_role_going_forward_with_the_dcr/) Company 0的未来角色，并收到了许多建设性回复，但在作者的Reddit帐户被删除后（巧合，同一天）消失了。 要通过重新提交链接，在r/decred 恢复[讨论](https://www.reddit.com/r/decred/comments/csq58r/what_is_c0s_role_going_forward_with_the_dcr/)。
* Telegram中检测到更多诈骗者，承诺帮助您解决技术问题，并支付0.05 BTC，小心诈骗者。

@Haon和ViệtAnhĐàm在Facebook上进行了与越南社区的AMA。 共有309条评论（包括答案），完整文档在[这里](https://github.com/noahpierau/articles/blob/master/Decred-Vietnam-AMA.md)。

选定的Reddit帖子：

* 对EXMO的问题没有[答案](https://www.reddit.com/r/decred/comments/cr8u4w/post_politeia_approval_fiat_pairs_integration_on/)。
* [为什么我会被](https://www.reddit.com/r/decred/comments/crci7p/why_im_into_the_decred_project/)Somebody__Online 邀请加入Decred项目
* [MimbleWimble技术的合作努力？](https://www.reddit.com/r/decred/comments/ct7aw9/collaborative_effort_for_mw_tech/)
* @matheusd解决对承包商倾销DCR和促进采用LN关注长期的[答复](https://www.reddit.com/r/decred/comments/ctp1zf/bitcoin_lighting_network/)。
* 隐私保护：该功能已[实施](https://www.reddit.com/r/decred/comments/cw1wd8/privacy_feature_revealed/)，隐私已经在主网上[使用](https://www.reddit.com/r/decred/comments/cxrb42/decred_privacy_was_announced_and_its_already_in/)，与比特币的CoinJoin和Decred的隐私理念背景不同，对12倍交易存储增加的[评论](https://www.reddit.com/r/decred/comments/cxdxso/what_does_it_mean_by_12x_increase_of_onchain/)。

选定的Twitter讨论：

* [引用](https://twitter.com/Ammarooni/status/1161707860822302722)从[@zubair](https://twitter.com/generalsaccount)的谈话- ‘我们现在需要解决的blockchain治理的透明度，使我们有一个机制，从现在作决定的二十年。
* Decred隐私 [tweet风暴话题](https://twitter.com/decredproject/status/1166746979160023046).
* @Checkmate 关于[隐私](https://twitter.com/_Checkmatey_/status/1167502975276933121).
* @richardred对Decred的[开源状态](https://twitter.com/RichardRed0x/status/1160972879133073409) “挖掘并找到有用的东西”。 
* @DCRtheSoV关于[Politeia的成长](https://twitter.com/DCRtheSOV/status/1165708600410402816)及其在项目中扮演的角色。
* @DCRtheSoV关于[如何POS](https://twitter.com/DCRtheSOV/status/1163514060542894080)DCR。
* @Checkmate 关于 [社区开发基金](https://twitter.com/_Checkmatey_/status/1157342578787913733).

新的Twitter帐户[@DCRtheSOV](https://twitter.com/DCRtheSOV)旨在成为一个有信誉的新闻和分析来源，涵盖Decred，并正在寻求反馈。


## 市场表现

8月份DCR的交易价格为22.63-32.17美元/BTC 0.00227-0.00275。每日平均价格为26.23美元。

从bw.com [观察](https://www.reddit.com/r/decred/comments/ctm0rq/whats_with_the_new_trade_volume/)到不切实际的数量激增。

比特币在8月份的大部分时间里再次突破10,000美元大关，短暂触及12,200美元。许多人猜测即将推出[Bakkt](https://cointelegraph.com/news/bitcoin-price-will-bakkts-launch-this-month-take-btc-to-new-highs)将使比特币突破这一周期。

在讨论做市商提案的背景下，[CoinMarketBook](https://coinmarketbook.cc/)认为：“市值是谎言。买入支撑说明真实的故事”。截至8月19日，DCR在该评级中排名第95，只有26万美元的购买支持，距离最高出价10％。具体情况：BTC有3.6亿美元，ETH有5500万美元，LTC 2300万美元，XMR 950万美元，DASH 570万美元，DOGE 460万美元。

## 相关外部信息

Blockstream 宣布了他们的比特币采矿业务（始于2017年），其中魁北克（加拿大）和佐治亚州（美国）的网站拥有自己的机器以及客户的机器。Blockstream还宣布了一个新的采矿池，第一个使用BetterHash协议的生产采矿池。BetterHash允许单个矿工选择要包含在他们找到的块中的事务，这将使采矿池操作员更难以恶意地使用其池的哈希值。

Braiins 宣布开源Stratum挖掘协议V2将包含受BetterHash启发的类似功能，允许配置池，以便矿工可以直接为其提案选择交易和版本位。

在创始人的奖励停止向ECC，Zcash基金会和其他受益人提供20％的块奖励之后，Zcash社区继续争取如何为发展提供资金的决定。下面是对看似相关的帖子的一些简短描述 - 遵循这个过程非常费力，因此有可能错过了重要的项目。

Zcash基金会（ZF）已经公布，以使自己的立场明确，他们的首选是通过大宗奖励发展资金的强制性，并规定，所有接受这些资金的实体必须是不以营利为目的。ECC目前是一家营利性公司，其信托义务是关注股东的利益，股东的利益可能与网络的健康发生冲突。这是大多数讨论的共同主题，人们并不热衷于向营利性公司提供大量奖励，并可能丰富创始人/投资者。

ZF不太喜欢的选择是矿工的选择性资金（他们会选择是否要烧钱或捐赠，以及捐赠给谁）以及没有开发资金。Zcash基金会的预计燃烧率为370万美元/年（工资为200万美元），并且可以在2023年之前运行，此后它将需要替代资金。

Zcash基金会正在组织一个社区治理小组，个人可以在Twitter上注册。专家组的成果没有约束力。

ECC发布了透明度报告，该报告在2019年第一季度分解了ECC的收入和支出.ECC的有效燃烧率在第一季度为63.5万美元/月，公司持有价值640万美元的美元和ZEC。该公司第一季度的收入为449,000美元。

其他建议包括来自Zcash基金会的Josh Cincinnati的一项重大妥协，其将激发EFF和ZF共享的另外4年20％的奖励，释放8％（ECC为4％，ZF为4％）更多地采用屏蔽交易。

战略委员会提案，将持续20％的块奖励和5人的董事会决定如何花费。这来自avichal，一个连续的企业家和Electric Capital的创始人，该公司投资了许多第1层协议（但不是Zcash）。

詹姆斯·普雷斯特威奇（James Prestwich）提出了一项建议（在Google Doc中）批评ECC的管理，并使用其资金对ECC进行例外处理，以开展旨在为其持续资金提供支持的营销活动。本文件还强调了Zcash商标所有权为ECC提供的权力，并认为在该问题得到解决之前不应进行任何决策过程。

Zooko已发布以解决有关如何管理Zcash商标的不同意见。该商标是ECC的唯一财产，但长期以来一直同意与Zcash基金会达成一项新的法律协议来控制它，该协议将提供双重否决。ECC已经考虑过在2-of-2 multisig类型的安排中共享控制，因为这很容易出现死锁和无所作为。最后，该帖认为ECC应该等到有关资金的决定，以决定如何分散商标的控制权。这并没有得到许多社区成员的欢迎。

Icon宣布了一篇论文关于他们的贡献提案系统如何运作。提案将在链上提交（最低保证金约为100美元），多数投票（“ICON主义者”，ICX人员）将确定该提案是否被批准接受资金。批准的提案可以接受授权，实际上该提案将获得一部分可用资金，这些资金由ICX授予它的比例决定。这与大多数项目处理资金决策的方式不同，收件人通常会定义和请求自己的预算。每30天所有已批准的提案都需要提交进度报告，ICX利益相关方将阅读这些提案，并可以多数票通过撤销提案的批准。目前尚不清楚该系统的目标日期是完成和生产的。

Maker 部署了一个新的治理投票门户。用户体验已得到改进，使投票更容易，并允许MKR持有人在对治理民意调查投票的同时投票决定具有约束力的行政决策（关于稳定费） - 这在以前是不可能的。与治理民意调查相关的所有内容都存储在“任何可公开访问的来源”的链外。轮询的哈希被提交给区块链，参与者可以通过检查该哈希来检查公共源中的内容是否已被编辑。

制造商对选民进行了调查，以确定将风险团队预先批准的7种不同资产整合为多抵押DAI的优先级。GNT（17％批准，1.2％参与），ZRX（76％批准，2.3％参与），OMG（38％批准，1.2％参与），REP（92％批准，3.6％参与），BAT（99.8％批准，参与率为2.3％），ETH（100％批准，4.3％参与），DGD（42％批准，1.3％参与）。每个提案的唯一投票钱包的最大数量为50（对于ETH投票）。这些投票是向开发商发出的信号，表明选民希望首先添加哪些资产。

Tezos 推出了Agora治理跟踪器，它提供了有关协议修订周期当前状态的实时信息，以及有关过去周期的历史信息。直接在Agora网站上进行讨论，而不是每个提案都链接到Discourse论坛帖子。Agora提供的功能与voting.decred.org页面相同，因为它提供了有关共识规则更改投票的信息。Agora在这方面还有更多工作要做，因为Tezos投票过程比Decred更复杂，部署新共识规则的过程有更多阶段。

巴比伦2.0提案目前正处于测试阶段，在第一轮击败巴比伦1.0（前一版本）（78％至22％，选民投票率为49％）并在第二轮获得了几乎一致的支持（选民投票率为82） ％，虽然只有463名面包师中的179人投票。此协议更改进行了一些改进，调整动态仲裁规则以限制它，并从通货膨胀中减去500 XTZ，以便开发人员可以购买一些饮料。

该Tezos基金会作出了补助金，以CamlCase开发一个分散的交换协议，由Uniswap启发，在Tezos blockchain。公告中没有关于赠款金额的详细信息，这是Tezos Foundation报告的标准。

Steemit 在8月27日宣布了一项硬分叉，以使工人提案系统或DAO能够从块奖励中管理资金 - 旨在加快和分散开发。Steem用户进行股权加权投票，优先考虑资金申请，最高投标收到资金，直到可用预算用完为止。

出售DAO是为了证明MolochDAO（或Moloch克隆）的成员可以出售他们的权利，通过智能代理合同提交提案，允许最高出价者提交提案。这个初始版本似乎仅用于演示目的，但版本2显然已经到来。

/ r / ethtrader主持人团队和社区似乎已经经历了一次硬分叉，因为6位主持人辞职开始/ r / ethfinance，因为主持人已经做出单方面决定并剥离了不同意他的mod的主持人身份。部分分歧是关于甜甜圈的实验，主持人比其他任何人都有更多的甜甜圈，并且没有更新其他主持人与Reddit管理员的进展。

PIVX正处理一个问题，其中一些小赌注者获得了比他们应有的更多的奖励，在一篇关于它的长篇文章中，PIVX大使证明情况并不像另一篇文章所暗示的那样严重，并认为困难的位置PIVX开发人员依赖于他们的代码库，拥有数百个分支。

CoinDesk的一篇文章探讨了委内瑞拉采用Dash的现实情况，表明它没有像一些Dash代表所宣称的那样广泛使用，并且一些促进商家采用的计划是无效的。

澳大利亚正在考虑禁止向超过1万美元的企业支付现金，影响汽车和住房等主要商品。这不适用于个人对个人的交易。评论者指出，除标准监督问题外，这可能被滥用作为实施负利率的工具。

美国财政部的外国资产控制办公室（OFAC）根据“外国麻醉品主要指定法” 批准了三名中国公民。这涉及冻结他们在美国的资产，发布他们的电子邮件别名和其他识别信息的细节，以及比特币和Litecoin地址。

## 关于月报

这是Decred月报的第17期。[这里](https://xaur.github.io/decred-news/)提供所有问题，镜像和翻译的索引。

来自第三方的大多数信息在经过小范围的检查后直接转发。Decred月报的作者无法验证所有声明。请注意诈骗并做自己的研究。

我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢(字母排列):

* 编写和编辑： akinsawyerr, bee, cryptoleslie, degeri, Dustorf, elian, kozel, raedah, richardred, s\_ben
* 评论和反馈： arij, chappjc, davecgh, emiliomann, jholdstock, jy-p, lukebp
* 封面图片：saender

## 中文社区

* [社区web](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [优酷频道](https://i.youku.com/decredproject)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)