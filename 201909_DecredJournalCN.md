# Decred月报 - 2019年9月

![abstract art](img/journal-201909-384.jpg)

_图片: On-Chain Seasonality by @saender_

* Decred项目家族新添加了PoW矿池软件dcrpool。高质量的开源矿池软件很少，并且对此类软件的需求成为新矿池的障碍。dcrpool填补了这一空白，现在任何人都可以启动自己的私人或公共矿池，这将有利于PoW挖矿的去中心化。
* dcrstakepool v1.2.0已发布。此版本始于2017年9月的开发工作，带来了许多增强功能，包括管理员可以使用不同的界面来处理不足费用购买的选票，全面改进的前端设计，增加安全性，更新的术语，减少了对第三方，以及各种错误修复。
* 9月是整合添加的重要月份，DCR支持已添加到Trust Wallet，Exodus移动钱包，添加使用LN进行付款的Joule Chrome扩展以及其它服务。

## 开发进展总结

[dcrd](https://github.com/decred/dcrd): 已[实现](https://github.com/decred/dcrd/pull/1856)第2版紧凑型过滤器。与v1滤镜相比，它们占用的空间更少，这对于轻节点客户端（SPV）而言将是一个改进。同样，v2过滤器将用于[区块头](https://proposals.decred.org/proposals/0a1ff846ec271184ea4e3a921a3ccd8d478f69948b984445ee1852f272d54c58)中。

`内存池`模块接收到的一部分错误代码。在相关的代码中被删除，包括[删除](https://github.com/decred/dcrd/pull/1736)支持`getwork`的`getblocktemplate` 。

进行了多个小范围调整，以进行重构，改进测试覆盖的范围和文档以及错误修复。

[dcrwallet](https://github.com/decred/dcrwallet): dcrwallet的Go代码现在其模块名称使用`decred.org`而不是`github.com`。[这里](https://github.com/decred/dcrd/issues/1264)讨论了更广泛地采用这种方法以减少对GitHub的依赖的看法。

为Go 1.13添加了构建支持，以及为1.11提供了构建支持。

集成[CoinShuffle++](https://github.com/decred/dcrwallet/pull/1541)的工作仍在继续。

[Decrediton](https://github.com/decred/decrediton): “帐户”界面进行了改善，而“安全”界面则显示了钱包的地址[派生](https://github.com/decred/decrediton/pull/2184)信息（可用于调试）。

闪电网络的集成工作[即将完成](https://github.com/decred/decrediton/pull/2107)。工作继续将 [启动重构](https://github.com/decred/decrediton/pull/2182)为有限状态机，使其更加安全可靠。

[Politeia](https://github.com/decred/politeia): 新的Politeia设计在[测试网](https://test-proposals.decred.org/)上进行，欢迎进行测试/反馈。

CMS系统取得了重大进展，DCC系统的基础和与承包商交互的[功能](https://github.com/decred/politeia/pull/981)已[合并](https://github.com/decred/politeia/pull/980)，同时为CMS和DCC提供了一系列较小的改进和错误修复。提案网站上即将出现的优先事项是[RFP提案](https://github.com/decred/politeia/issues/966)和[Trillian](https://github.com/google/trillian)集成，这将为单个内容加盖时间戳。

[dcrstakepool](https://github.com/decred/dcrstakepool): v1.2版本已发布在主网上。

前端增加了一个新的仅用于管理低价票的管理员页面。此页面将列出所有已购买且费用不足的选票，并允许管理员手动将这些选票添加到符合条件的选票中。以前，必须通过直接操作数据库来手动执行此操作。

新的前端设计使dcrstakepool达到了其他Decred软件（例如Decrediton）中看到的专业标准。

根据VSP运营商的要求，已经实现了对加密SMTP连接的支持，包括对自签名证书的支持。这使VSP可以保护通过SMTPS传输的注册和帐户找回电子邮件。

与dcrwallet的所有通信现在都必须通过StakePoold进行。这种架构改变降低了RPC调用在网络上的数量，降低了代码复杂度，并且允许关闭DCRelpSpCon和DCRWalk之间的端口。

自定义MySQL数据存储已取代了用于存储会话cookie的基于文件的存储解决方案。这解决了与会话数据有关的几个已知的安全问题。

Google的reCAPTCHA已被[Go](https://github.com/dchest/captcha)中实现的自托管解决方案取代。现在，所需的所有资源都由VSP托管，而不是由第三方托管。此版本中包含的前端完全不执行任何外部JavaScript，从而大大提高了用户的安全性和隐私性。

进行了一些安全性改进，为了防止跨站点请求伪造（CSRF）攻击，将私人数据泄露给第三方，恶意链接以及浏览器缓存敏感信息。

此次发布是自2017年9月以来20位贡献者发出的160个合并的成果。有关正式版的完整详细信息，请参见[版本说明](https://github.com/decred/dcrstakepool/releases/tag/v1.2.0)。

[dcrpool](https://github.com/decred/dcrpool): 经过一年多的酝酿之后，Decred的开源矿池程序终于 [发布](https://twitter.com/decredproject/status/1176914732399439873)了([博客](https://blog.decred.org/2019/09/25/Introducing-Dcrpool/))。dcrpool功能：

* 可以作为私人矿池或公共矿池使用
* 支持所有相关的矿机
* PPS和PPLNS支付方式
* 具有网络统计信息和帐户数据的用户界面
* 所有矿机的连接详细信息
* 帐户工作量和支付分析

该软件由@dnldd使用Go开发，是让Decred的PoW挖矿去中心化的重要一步。恭喜发布！

[dcrlnd](https://github.com/decred/dcrlnd): 最终合并了来自上游lnd的端口[合并](https://github.com/decred/dcrlnd/pull/36)请求的大量工作。

启用[远程钱包](https://github.com/decred/dcrlnd/pull/40)功能的工作已经开始。这将使用户可以使用现有的钱包，而不必为dcrlnd管理具有单独种子的额外钱包。它还允许用户直接在Decrediton中运行的钱包启动LN钱包，从而简化了UX。

[cspp](https://github.com/decred/cspp)（CoinShuffle ++）: 添加了重新连接[支持](https://github.com/decred/cspp/pull/18)，更新了安装说明，添加了Go 1.13版本，错误修复。（CoinShuffle ++）

[dcrdex](https://github.com/decred/dcrdex): [基础布局](https://github.com/decred/dcrdex/issues/8)已经完成，其中数千行代码合并在主库中。已添加[DCR](https://github.com/decred/dcrdex/pull/17)和[BTC](https://github.com/decred/dcrdex/pull/26)的初始后端。规范进行了几处小的[更改](https://github.com/decred/dcrdex/pulls?q=is%3Apr+is%3Aclosed+label%3Aspec+merged%3A2019-09-01..2019-09-30)。

与使用ISC许可证的其他软件不同，dcrdex选择了BlueOak。在这次聊天中[讨论](https://matrix.to/#/!EzTSRQITaqHuFBDFhM:decred.org/$RaxvOZy5x4cby5rwhph7gUED6LR0yQkKIihst4C5Og4)了原因。

[dcrandroid](https://github.com/decred/dcrandroid): 新版UI的工作正在全面开展，对[主页](https://github.com/decred/dcrandroid/pull/401)进行了改进，以使该应用程序与Android的标准应用程序设计建议保持一致。[多钱包](https://github.com/raedahgroup/dcrlibwallet/pull/57)支持工作已经开始。这将允许用户从Decrediton导入其公钥，以便他们可以从手机监控选票的状态。

[dcrios](https://github.com/raedahgroup/dcrios):正在进行重构以利用dcrlibwallet中的[新tx过滤器](https://github.com/raedahgroup/dcrlibwallet/pull/48)方法。这包括对[历史页面](https://github.com/raedahgroup/dcrios/pull/515)的全面检查，用于[存储事务](https://github.com/raedahgroup/dcrios/pull/520)的新数据结构以及对[发送页面](https://github.com/raedahgroup/dcrios/pull/521)的全面检查，以使用户能够将DCR同时发送到多个目标。

简化了[后台同步](https://github.com/raedahgroup/dcrios/pull/518)并使其更加安全可靠。这解决了一些用户由于手机进入睡眠状态而停止同步区块链时遇到的问题。

UI优化随着 [主页](https://github.com/raedahgroup/dcrios/pull/512)更新正在继续。

[docs](https://github.com/decred/dcrdocs):[dcrtime](https://docs.decred.org/advanced/dcrtime/)的页面已[添加](https://github.com/decred/dcrdocs/pull/960)。

开发人员文档的工作仍在继续，预计将很快从私人存储库移植到Decred GitHub组织中，以提高可视性。

[decred.org](https://github.com/decred/dcrweb): 更新了[蓝图](https://decred.org/roadmap/)，[钱包下载](https://decred.org/wallets/)和[交易所](https://decred.org/exchanges/)页面。

多个项目已将其持续集成（CI）系统从Travis CI切换到GitHub Actions。动作速度更快，集成度更高，开源且可共享，并且在允许范围内总体上更加灵活。

9月的开发活动统计：分布在15个存储库中的248个活动PR，201个提交，添加2.8万行和删除1.7万行。每个存储库贡献者为2-8个开发人员。

## 人员

欢迎新的首次贡献者到来： imestin ([dcrdocs](https://github.com/decred/dcrdocs/commits?author=imestin)), Muharem Hrnjadovic ([politeia](https://github.com/decred/politeia/commits?author=al-maisan)), Amir Massarwa ([politeiagui](https://github.com/decred/politeiagui/commits?author=amassarwi)).

@s_ben写了一篇很棒的中等篇幅文章，介绍了他在Decred DAO工作的经历，并对流动性，波动性和他的未来计划进行了描述。

截至10月2日的社区统计数据：

* Politeia 用户: 181 (+7)
* Twitter 粉丝: 40,578 (-19)
* Reddit 订阅: 9,631 (+37)
* Matrix 用户: 436 (+24)
* Slack 用户: 6,851 (+17)
* Discord 用户: 2,487 (+45), verified to post: 325 (+15)
* Telegram 用户: 3,048 (-100)
* YouTube 粉丝: 3,830 (+11)
* Facebook 粉丝: 3,278 (+7), likes: 3,003 (+4)
* LinkedIn 粉丝: 622 (+19)
* GitHub dcrd库星星: 517 (+1), 分叉: 1,394 (+11)

## 治理

九月份，[社区基金](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了14,510 DCR，支出了7,810 DCR（注意：支出发生在10月初）。使用9月份的每日DCR / USD平均价格$ 22.02，得出的总收入为$ 320K，支出为$ 172K。由于这些付款是针对8月份完成的工作，因此在8月份的每日平均费率$ 26.23的情况下考虑这些费用也很有帮助-在这种情况下，美元支出的金额为$ 205K。截至10月2日，社区基金余额为641,802 DCR（1,100万美元，折合17.12美元）。

i2 Trading赢得了成为Decred指定做市商的竞争，获得了68％的批准，而Tantra Labs和Grapefruit Trading的批准率分别为49％和47％。i2还吸引了41％的较高选票率参与，相比之下，Tantra Labs(41%)比Grapefruit Trading(33％)的票务参与度更高（现在在[dcrdata alpha](https://alpha.dcrdata.org/proposals)上可见投票率）

Tantra Labs祝贺I2，发表后他们就Politeia的经验，并表示，他们打算继续他们的[计划](https://medium.com/@TantraLabs/proof-of-politeia-ac87f52243f4)。

@ permabullnino的[提案](https://proposals.decred.org/proposals/f0d1bd7447182328b44c691de88cb660b63df17f1f3a94990af19acea57c09bb)为“关于DCRUSD＆DCRBTC指标的研究和出版”用83％的赞成票和27％的选票参与率获得批准。Permabull将在大约3个月的时间内提供4-6篇有关“ Hyperactive HODLer的价格（HHP）”的文章。Permabull已出版的作品将收取3500美元的费用，而新作品将收取13,000美元的费用。

否决了“在2019-2020年在CIS中举行大型活动和聚会” 的[提案](https://proposals.decred.org/proposals/fdd68c87961549750adf29e178128210cb310294080211cf6a35792aa1bb7f63)，赞成率为4％，选票参与率为25％。

Politeia Digest 第[22期](https://medium.com/politeia-digest/issue-22-september-1-12-2019-d82f5f617c92)提供了有关这些建议的更多信息。9月下半月的Politeia是安静的，当有新提案时，将出版新一期的《Politeia Digest》。

## 网络

全网算力: 9月份的哈希率以〜619 Ph/s开启，以〜472 Ph/s结束，最低为404 Ph/s，并在整个月达到峰值679 Ph/s。截至10月2日的池哈希率分布：UUPool 21％，Poolin 19％，F2Pool 19％，lab.antpool.com 5.8％，BTC.com 2.9％，Luxor 2.12％，Coinmine 0.10％，BeePool 0.10％，suprnova 0.03％和其他每个[dcrstats.com](https://dcrstats.com/pow)为 30％。池分配数是近似值，无法准确确定。

Staking: 30天平均选票价格为128.70 DCR（-1.35）。价格在121.92-134.4 DCR之间变化。锁定金额为522-533万DCR，相当于可用供应量的49.87-51.15％。

Nodes: 整个9月，大约有182个监听节点，总共406个节点。截至10月4日，运行dcrd v1.4.0的大约81％，运行dcrwallet v1.4.0的6.5％，运行v1.5.0（pre）的6％。

平均来看，9月的DCR测试网闪电网络[显示](https://charts.dcr.farm/d/DHPdAO4Wz/lightning-network?orgId=1&from=1567296000000&to=1569888000000)了17个节点，35个通道和227个DCR的总容量。

## 整合

Binance 的[官方](https://www.binance.com/en/blog/295063453682311168/Trust-Wallet-20-One-App-for-All-Your-Crypto)钱包[Trust Wallet](https://trustwallet.com/)宣布[增加](https://twitter.com/TrustWalletApp/status/1175864708961845253)Decred。

Exodus 将 Decred [添加](https://twitter.com/exodus_io/status/1168886493617840131)到了其手机钱包中。为了回应Twitter上的一个问题，Exodus表示了他们在开源上的[立场](https://support.exodus.io/article/89-is-exodus-open-source)。

decred支持已[添加](https://github.com/joule-labs/joule-extension/pull/230)到[Joule](https://lightningjoule.com/)（流行的Chrome扩展）中，该扩展允许用户通过闪电网络进行付款。

[Uphold](https://uphold.com/)增加了对Decred的支持。

[StealthEX](https://stealthex.io/)已添加 DCR。该服务提供匿名和无帐户即时加密交换。

[InstaEx](https://instaex.io/)交换添加了 DCR交易，并提交了合并请求以在decred.org上添加。在与竞争对手的简短对比中，该服务声称无需KYC或电子邮件。
[Tokenview](https://tokenview.com/en)已将Decred区块数据[添加](https://twitter.com/tokenview2018/status/1176394157327147008)到其多资产[区块浏览器](https://dcr.tokenview.com/en)中。

警告：Decred Journal的作者不了解上述任何服务的可信赖性。在将您的个人信息或资产信任给任何实体之前，请先自行研究。

## 外联活动

Decred outreach in September focused on education and awareness regarding the recent privacy implementation. Presentations were created for [Surveying the Privacy Landscape](https://www.notion.so/Transaction-Privacy-75c4bd707c194de18ff5d943f8909e26) and [Decred Privacy](https://www.notion.so/Privacy-Keynote-4902c63379894765a545351f8fcc7d7f), and Decred community organizers across the world have presented Privacy at various meetups. @jy-p travelled to San Francisco and Los Angeles, presenting Privacy at Decred meetups in both cities, and presenting the privacy landscape to the San Francisco Bitcoin Meetup. @Dustorf published a blog, [Decred Privacy, Taking the Long Road](https://medium.com/decred/decred-privacy-taking-the-long-road-62d218223db6), contextualizing privacy from a values and development perspective.

Decred in Depth released an [episode](https://soundcloud.com/decredindepth/dcr-checkmate) featuring @Checkmate, where he delved into his research on Decred. Decred Assembly will shortly release a Deep Dive episode fetauring Decred developer @jrick, where he discussed many of the nuances of Decred's path to privacy, the implementation, and next steps.

Decred and Exodus hosted a [giveaway](https://twitter.com/decredproject/status/1171900177365569536) of Trezor Model Ts to 3 best tweets explaining why the author loves Decred. Congrats to the winners [@encldi](https://twitter.com/decredproject/status/1172577786227281920), [@OfficialCryptos](https://twitter.com/decredproject/status/1172578137948983297) and [@dcrstack](https://twitter.com/decredproject/status/1172578432343040000)!

Ditto's September achievements:

* Secured media coverage: feature on Decred's treasury in [Crypto Briefing](https://cryptobriefing.com/decred-venture-capital-centralizing/) based on interview with @richardred; interview with @jy-p on POV Crypto Podcast, the episode aptly titled "[In Search of Sovereignty](https://povcryptopod.libsyn.com/77-discovering-decred-w-jake-y-p)"; an [interview](https://open.spotify.com/show/4y3hF660v5FNPpRlg9muCC) with @lukebp in The Daily Chain podcast; Decred profile in [Blockchain Tech News](https://www.blockchaintechnews.com/articles/company-profile-decred-aims-to-deliver-decentralized-future/).
* Secured a keynote speaking slot for @jy-p at the SF Bitcoin Meetup, where he gave a presentation on the privacy landscape. There were 50+ attendees from a variety of projects. Overall a big win to have Decred speak at a Bitcoin Meetup! Jake's speech was [livestreamed](https://www.youtube.com/watch?v=LgLfMLFfOHQ?t=191). Ditto also spent quality time with @anshaw and @jy-p during their visit to San Francisco.
* Coordinated with journalists and other crypto enthusiasts in LA and SF to drive attendees to the meetups in the last week of September.
* Coordinated with the organizers of Voice of Blockchain in Chicago, where @jy-p will give not 1 but 2 presentations: one on The Decentralized Grant and Funding Process (as part of a panel with The Block), and one on Why Direct Sovereignty & Multi-Stakeholder Inclusive Governance Will Last.
* Secured two interviews with @jy-p.
* @liz\_bagot was recorded on the Decred in Depth podcast with @anshaw - episode coming soon.
* Moved the educational resources repository closer to completion.
* Coordinated with the community to continue pushing Decred's privacy narrative across Twitter.
* New Ditto team member Anastasia has joined Margaret Mei, Leslie Ankeny, and Liz Bagot on all our various Decred projects. Welcome!

## 社区活动

出席:

* Aug 25 - Poolin China Mining Tour - Shanghai, China. @Dominic was invited to participate in a panel discussion on PoW and delivered a keynote speech on Decred. Trivia - Poolin recently became [2nd largest](https://twitter.com/officialpoolin/status/1171451086999191557) mining pool for Bitcoin, and is contributing around [90 Ph/s](https://twitter.com/NoahPierau/status/1171527633391079424) to Decred network. ([event stats](https://twitter.com/officialpoolin/status/1166702227727310848), [photos](https://twitter.com/wanbihou/status/1166028812305321985), _missed in Aug issue_)
* Sep 4 - [Campus Party](https://brasil.campus-party.org/campus-party-goias/) - Goiânia, Brazil. Decred team members delivered a total of 5 talks about blockchain, consensus, Decred and Lightning Network. (photos: [1](https://twitter.com/Decred_BR/status/1171402110031847424), [2](https://twitter.com/Decred_BR/status/1170136831272325121), [3](https://twitter.com/Decred_BR/status/1169812440051109888))
* Sep 5 - [Blockchain Summit](https://blockchainsummit.uy/) - Montevideo, Uruguay. @camilolwi and @pablito presented an overview of Decred called "Governing Together" and talked to devs and journalists after the event. Full report with all media links was [published](https://github.com/decredcommunity/events/blob/master/reports/20190905-blockchainsummituy-montevideo-uruguay.md) in the events repository.
* Sep 5 - [Digital Economy](https://twitter.com/Decred_ES/status/1169677346506297344) - La Paz, Bolivia. @elian's team presented the project to the local community of entrepreneurs and enthusiasts Bolivian Mind Blockchain. ([report](https://twitter.com/elianhuesca/status/1170055934284111872) with photos)
* Sep 7 - Tech4Amazonia - La Paz, Bolivia. The event was collecting donations to fight the wildfires on the Bolivian side of the Amazon River. @elian presented the project to engineering students of El Alto Public University. ([photos](https://twitter.com/elianhuesca/status/1171034359027195904))
* Sep 10 - [Decred Privacy](https://www.meetup.com/Permissionless-Society/events/dnkzvqyzmbnb/) - Amsterdam, Netherlands. @Haon gave an overview of existing privacy projects and introduced Decred's approach. Full report with media links is [here](https://github.com/decredcommunity/events/blob/master/reports/20190910-decred-privacy-amsterdam-netherlands.md).
* Sep 12 - [Decred Meetup](https://twitter.com/Decred_ES/status/1171471998989389824) - Morelia, Mexico. @francov\_ and @luisantoniocrag hosted the first meetup in Morelia and among other things, answered questions from a little kid who seemed to understand Decred. ([photos](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$1568342471606746ojsnf:matrix.org))
* Sep 18 - [Bitcoin and Blockchains Workshop](https://www.facebook.com/events/959839374354073/) - Oaxaca, Mexico.
* Sep 18 - [The Great Bitcoin vs Blockchain Debate](https://www.meetup.com/BlockchainMelbourne/events/264425160/) - Melbourne, Australia. @eSizeDave participated in the debate around the topic "Does blockchain have a viable use case outside of sound money?" as a member of Bitcoin Team, against the Blockchain Team that represented the "blockchain-for-everything" mindset. The setup of the event was not in favor of the Bitcoin team and it lost in the final voting. However, @eSizeDave managed to put Decred and governance in the spotlight quite a few times, including a fabulous Decred T-shirt "coming out". Read his full story, along with some wisdom about attending events efficiently, in [this report](https://github.com/decredcommunity/events/blob/master/reports/20190918-the-great-bitcoin-vs-blockchain-debate-melbourne-australia.md).
* Sep 20 - [A Framework for Blockchain Governance](https://www.eventbrite.com/e/a-framework-for-blockchain-governance-tickets-70134180221) - Washington DC, USA. @akinsawyerr participated in a governance presentation with Thomas Cox of [StrongBlock](https://strongblock.io/) at [Blockshop](https://www.blockshopdc.com/). Engaged in a Q&A session on Blockchain Governance and perspectives on Decred's governance process.
* Sep 21 - [French Vibes Connection](https://twitter.com/Decred_ES/status/1160669435989856256) - Mexico City, Mexico. This was a promo experiment where the Decred logo was blended with visual effects while electronic bands played their tracks to a crowd. @francov\_ notes: "It was extraordinary, Decred's designs were incredible and, together with the music, an environment was created where Decred stood out a lot, there were interested people who asked who we are.". (videos: [1](https://twitter.com/elianhuesca/status/1175609208705863681), [2](https://twitter.com/elianhuesca/status/1175610899006197761); [instagram](https://www.instagram.com/p/B268Uougtbo/))
* Sep 21 - [Decred Meetup](https://twitter.com/DecredArabia/status/1171117988461854721) - Casablanca, Morocco. @arij (@butterfly) talked about her experience as Decred contributor, Decred's governance, privacy and her future plans. People were quite interested and eager to learn, to the point where they stayed an hour after the event was supposed to end, and requested more meetups and even courses in universities and associations. ([report](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156914094936513JoWdj:decred.org), [photos](https://twitter.com/in_insaf/status/1175692906826481664))
* Sep 23 - [SF Bitcoin Meetup](https://www.meetup.com/San-Francisco-Bitcoin-Social/events/dhdhsqyzmbgc/) - San Francisco, USA. @liz\_bagot noted: "@jy-p gave a solid overview of the privacy coins and got a lot of questions at the end. About 50 people showed up from a variety of projects and backgrounds. A big success for Decred - nobody from Decred has ever spoken at a Bitcoin meetup before!" _(to be fair, @camilolwi and @pablito bravely [risked](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$156529022111295SCOiX:decred.org) their lives one month [earlier](201908.md#events) at Espacio Bitcoin)_. The event was hosted by [Starfish](https://twitter.com/starfishsf) and the talk was [livestreamed](https://www.youtube.com/watch?v=LgLfMLFfOHQ?t=191) on YouTube.
* Sep 24 - [Decred Privacy](https://twitter.com/decredproject/status/1174374566359183360) - San Francisco, USA. @jy-p gave an overview of the privacy landscape and a deep dive on Decred's implementation. Sponsored and hosted by Coinbase Custody. ([photos](https://twitter.com/HaileyLennonBTC/status/1176697168196849664))
* Sep 25 - [La Conexión](https://twitter.com/Conexion_Events/status/1165075848782852101) - Buenos Aires, Argentina. @elian presented a high level overview of Decred and its history, ran a small booth and talked to the attendees. The day before the event, @elian and @victorarubin had a lunch with several local crypto personalities. Argentinians are very advanced and are looking into alternatives to their currency that may hit 50% inflation this year: "From cap drivers to shop vendors they all know about bitcoin and other cryptocurrencies.". ([report](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15704543735491DFGIA:decred.org), photos: [1](https://twitter.com/victorarubin/status/1176926844916043782), [2](https://twitter.com/victorarubin/status/1176933542762287104)).
* Sep 26 - [Inaugural Decred Meetup](https://twitter.com/MattDavidKaye/status/1164974520081342464) - Los Angeles, USA. @jy-p talked about fundamentals, tech, governance and future of Decred. Hosted by Blockhead Capital. (photos: [1](https://twitter.com/Tantra_Labs/status/1177412535059808256), [2](https://twitter.com/degeri_crypto/status/1177412554101932032))
* Sep 27 - [Crypto Fest](https://argentinacryptofest.com/) - Córdoba, Argentina. @elian and @victorarubin delivered another high level overview of Decred and took the opportunity to connect with members of the local Bitcoin and blockchain community. Notably, the event was endorsed by the local government. Read @elian's full report and impressions about Argentina [here](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$15704543735491DFGIA:decred.org) (or wait for GitHub version). (photos: [1](https://twitter.com/victorarubin/status/1177976167145586693), [2](https://twitter.com/victorarubin/status/1178038340505030658))
* Sep 27 - [Blockchain for Business and Government](https://www.eventbrite.com/e/blockchain-para-empresas-y-gobierno-tickets-72417321157) - Monterrey, Mexico. Alteumx (an exchange in Mexico) invited @luisantoniocrag to be present at this event where he had the opportunity to talk about Decred to the public (businessmen and politicians). ([photos](https://twitter.com/Decred_ES/status/1178690139008229376))
* Sep 28 - [Bali Block Confex](https://bali.blockconfex.com/) - Legian, Indonesia. Duyen Em talked to people at the event about Decred, handed out postcards and made some connections. Most people hear about Decred for the first time, and many get interested pretty quickly. Full report is [here](https://github.com/decredcommunity/events/blob/master/reports/20190928-bali-block-confex-legian-indonesia.md).
* Sep 30 - [Voice of Blockchain](https://twitter.com/BlockchainVoice/status/1154772731575099392) - Chicago, USA. @jy-p talked about decentralizing the allocation of capital and why direct sovereignty will last into the future. (photos: [1](https://twitter.com/BlockchainVoice/status/1179100328102203392), [2](https://twitter.com/BlockchainVoice/status/1179088345638621185))

即将到来的:

* Oct 17 - Blockchain and Decred - Morelia, Mexico. @luisantoniocrag and @francov\_ will talk about blockchain and Decred in a university at Morelia city.
* Oct 29-31 - [World Crypto Conference](https://worldcryptocon.com/) - Las Vegas, USA. @akinsawyerr will be speaking on a panel on "Governance Practices" and will also give a presentation titled: "Governing the Crypto Commons". The presentation will highlight Decred's governance process in contrast with other efforts across the public blockchain space.
* Oct 31 - Blockchain APAC - To be confirmed and announced.
* Nov 4-7 - [Web Summit](https://websummit.com/) - Lisbon, Portugal. Decred will have a booth.
* Nov 16 - [BitConf](https://www.bitconf.com.br/portal/) - São Paulo, Brazil. This is one of the biggest crypto events in Latin America. Decred team will present around 3 lectures.

A total of 4 new reports were added to the [events repo](https://github.com/decredcommunity/events), and 1 more is coming. As a reminder, the events repo serves to collect experiences from worldwide events in one place and gives you an accessible report link to disseminate. The repo can be easily replicated to protect the data, and you can even submit a report without leaving your terminal.

Thanks to everybody for writing and submitting reports to grow our knowledge base!

## 媒体

Selected articles:

* Decred: An Investment Thesis by Wally Hansen ([medium](https://medium.com/coinmonks/decred-an-investment-thesis-bf9ba3cd1042)) - This comprehensive summary of Decred and assessment of opportunities and risks arrived out of the blue, pieced together from public sources by an enthusiastic stakeholder.
* Introducing Dcrpool by @dnldd ([blog.decred.org](https://blog.decred.org/2019/09/25/Introducing-Dcrpool/)) - A blog post introducing and describing the rationale for building an open source stratum mining pool for Decred.
* I Dump Coins on You by @s\_ben ([medium](https://medium.com/@seth.benton/i-dump-coins-on-you-ee6db4331e18))
* Decred Privacy: Taking the Long Road by @Dustorf ([medium](https://medium.com/decred/decred-privacy-taking-the-long-road-62d218223db6))
* Writing Proposals on Politeia (Pi) by Decred Dragon ([medium](https://medium.com/@decreddragon/writing-proposals-on-politeia-pi-e345621652a2))
* How Decred Aims to Build a Decrentralized Governance Model by @evok3d ([bitsonline](https://bitsonline.com/decred-decentralized-governance/))
* The Decred Experiment: Can Decentralization Help Mexico? by @evok3d ([medium](https://medium.com/@evok3d/the-decred-experiment-can-decentralization-help-mexico-1e0e8156430c))
* Proof of Politeia by Tantra Labs ([medium](https://medium.com/@TantraLabs/proof-of-politeia-ac87f52243f4))
* DAOs and the Missing Link: Reputation Protocols by @s\_ben ([medium](https://medium.com/sourcecred/the-dao-missing-link-reputation-protocols-8e141355cef2))
* Decred Lead: Venture Capital Is a "Very Centralizing" Force by Paddy Baker ([cryptobriefing.com](https://cryptobriefing.com/decred-venture-capital-centralizing/))

Translations:

* Iterating Privacy [in Arabic](https://github.com/Insaf01/decred-arabic/blob/master/articles/iterating-privacy.md) by @arij, [in Russian](https://medium.com/decred-russia/iterating-privacy-6d242f78a648) by @DZ and [in Portuguese](https://stakey.club/translated/iterating-privacy/) by @mm
* Turns out a lot of earlier articles were translated to Portuguese as well at [stakey.club](https://stakey.club/pt/translated/)
* More translations of Decred Journal to Arabic (@arij), Chinese (@Dominic and co), Polish (@kozel), Russian (@DZ), Spanish (@francov\_ and @luisantoniocrag) and Vietnamese (@duyenemdo). Thank you for spreading the word!

Videos:

* Decred Assembly Deep Dive: Decentralizing the Treasury with Marco Peereboom ([youtube](https://www.youtube.com/watch?v=4N8Fq1tU3XM))
* @jy-p talks privacy at the San Francisco Bitcoin Meetup ([youtube](https://www.youtube.com/watch?v=LgLfMLFfOHQ?t=191))
* @akinsawyerr talks about Blockchain and Decentralized Finance's Impact on Emerging and Frontier Markets on the Global Startup Movement ([youtube](https://www.youtube.com/watch?v=OIO1q1UO4qM))

Audio:

* Decred in Depth Ep. 8 with @Checkmate - Checkmate talks about the DCR value stack and stock to flow ratio, Bitcoin and Decred on-chain metrics, monetary premiums, sustainable funding to attract committed contributors, and his own research plans. ([youtube](https://www.youtube.com/watch?v=2JbMWgJUoSQ), [soundcloud](https://soundcloud.com/decredindepth/dcr-checkmate))
* POV Crypto Podcast Ep. 76 - @jy-p joins the POV Crypto crew for an episode titled "In Search of Sovereignty" which considers Bitcoin and Decred fundamentals, sovereignty, backwards compatibility and privacy. ([youtube](https://www.youtube.com/watch?v=WnY3c-F5caw), [libsyn](https://povcryptopod.libsyn.com/77-discovering-decred-w-jake-y-p))

## 社区讨论

Comm systems news:

* Chris Burniske's Telegram account was [compromised](https://twitter.com/cburniske/status/1177747319426621440) and was asking people to send him crypto. Make sure to [set your password](https://twitter.com/cburniske/status/1180527281350955008) in Telegram. This is also a good reminder to check your defenses against SIM swapping attacks.
* Impersonation on Discord via Discord Nitro is becoming more common. Nitro allows to change your name _and_ the ID code.
* Decred [airdrop](https://archive.today/GXimX) where you get free ETH is obviously not your friend.
* In general, pay attention and report any suspicious accounts and groups on all platforms.

Selected Reddit posts:

This section tends to feature Reddit threads that had a significant number of comments, many of these posts have low scores and therefore low visibility on Reddit.

* Abstract terminology about [levels of privacy](https://www.reddit.com/r/decred/comments/d0jg3l/abstract_terminology_about_levels_of_privacy/) - discussion of the privacy overview blog post.
* Random Decred Reddit community [question](https://www.reddit.com/r/decred/comments/d6kt1v/random_decred_reddit_community_question/) - about why the number of online members on /r/decred is consistently high relative to total subscribers.
* What Decred [feature or tool](https://www.reddit.com/r/decred/comments/dappgf/what_decred_feature_or_tool_would_you_want_more/) would you want more community members to use?
* Ticket splitting [guide available?](https://www.reddit.com/r/decred/comments/d50wkw/ticket_splitting_guide_available/)
* [Analysis](https://www.reddit.com/r/decred/comments/d1c69a/analysis_of_ticket_voting_so_far_on_the_market/) of ticket voting so far on the market maker proposals.

Selected Twitter discussions:

* @Dustorf's Decred thesis in 2 minutes ([9 tweets](https://twitter.com/lefebvre_dustin/status/1174789127105105928)), based on Wally Hansen's thesis.
* @karamblez [video](https://twitter.com/karamblez/status/1178346009178644481) visualizing activity of btcsuite and Decred repositories since 2013.
* @Checkmate on Decred [hashrate](https://twitter.com/_Checkmatey_/status/1177650799050133504) growth as compared to other assets.
* @Checkmate on Decred and Bitcoin [Stock to Flow](https://twitter.com/_Checkmatey_/status/1173672584933777408).
* dcrpool announcement and summary [tweet](https://twitter.com/decredproject/status/1176914732399439873).
* @jholdstock's pull request to Joule was [merged](https://twitter.com/JamieHoldstock/status/1171347711536357378).
* @matheusd [tweets](https://twitter.com/matheusd_tech/status/1168897318432706561) about bringing 400+ pull requests from upstream Lightning Network's repository to dcrlnd.
* @fernandoabolafio [invites](https://twitter.com/oxfernando/status/1174268398458609664) people to check out the Politeia redesign.
* @moo31337 [suggests](https://twitter.com/marco_peereboom/status/1176856040991801345) that when the markets are down, it's a good opportunity to join a project like Decred and get paid.
* @lukebp's [prediction](https://twitter.com/lukebp_/status/1175441776041058304) about smart contract platforms vs permissionless money and society transformation.
* [Summary](https://twitter.com/jcliff42/status/1170039176277835776) of Decred privacy tech from Jordan Clifford of Scalar Capital.

## 市场表现

In September DCR was trading between USD 16.49-25.20 / BTC 0.0020-0.0024. The average daily rate was $22.02.

DCR/USD lost more than 20% together with BTC/USD around Sep 24. Among possible causes discussed in the media are: [sharp drop](https://www.ccn.com/bitcoin-hashrate-flashcrash-price-slump/) of Bitcoin's hashrate, [disappointing launch](https://cryptobriefing.com/bakkt-crypto-launch/) of Bakkt that didn't bring the anticipated institutional bull run, and [liquidations](https://bitcoinist.com/yes-bitmex-liquidations-caused-bitcoin-price-to-crash-heres-how/) on derivatives trading platforms.

## 相关外部信息

The [Crypto Rating Council](https://www.cryptoratingcouncil.com/) was [announced](https://blog.coinbase.com/introducing-the-crypto-rating-council-d6ee33a8f34d), this is a group of cryptocurrency businesses producing ratings of whether cryptoassets are likely to be considered as securities by the SEC. An initial set of 20 [ratings](https://www.cryptoratingcouncil.com/asset-ratings) which position assets on a scale between 1 (not a security) to 5 (very likely a security) were released. Bitcoin, Litecoin, Monero and DAI received the best score (1). Assets like EOS, Tezos, Stellar and Hedera Hashgraph all received a 3.75 score, XRP got 4 and Polymath 4.5. The CRC will not publish the names of projects that received a rating of 5. More ratings will be published in the future. While the methodology is not published, it can be inferred from the bullet-point summaries of ratings that emphasis is placed on whether there was a token sale, whether that occurred before the system had utility, whether there was investment-like language in promotional materials for a token sale, and whether there is decentralized development and usage of the system.

More than 640 crypto projects did not publish any new code in 2019, according to a [study](https://blog.coincodecap.com/analyzing-cryptocurrencies-github-activity/) by CoinCodeCap. The combined cap of these currencies is around $415 million, with the highest individual cap of $85 million. The exchange and market cap data for these tokens is incomplete, but in what is available, YoBit leads the exchanges listing such tokens by having 62 of them.

A settlement between the SEC and EOS was [announced](https://www.sec.gov/news/press-release/2019-202) in which Block.One must pay $24 million in penalties for conducting an unregistered securities sale. This relates to the sale of ERC-20 EOS tokens in a year-long ICO that raised $4.1 billion, the fine amounting to 0.6% of the raised amount. According to Block.One's [press release](https://block.one/news/block-one-announces-settlement-with-us-securities-and-exchange-commission/) the settlement only applies to the ERC-20 tokens, which have since been swapped for EOS mainnet tokens, considered to be in the clear and not require SEC registration for trading.

The Bisq network [announced](https://bisq.network/blog/bisq-dao-first-four-cycles/) that four monthly cycles of its funding DAO have been completed. The Bisq DAO can mint BSQ colored coins to fund development work, and these are burned when used to pay trading fees. Proposals include compensation requests, bonded roles which receive ongoing compensation, parameter changes (trading fees were increased) and signalling approval for other development decisions. In each cycle the number of proposals was around 20 and the number of votes 200-300. The first and second cycles were highly inflationary, with much more BSQ minted than burned, but the 3rd cycle had similar levels of burning and minting and in the 4th cycle more BSQ was burned than minted. _(missed in Aug issue)_

The OKCoin exchange [launched](https://twitter.com/OKCoin/status/1168917669493579776) an [initiative](https://www.okcoin.com/1000btc) on Sep 3 to donate up to 1,000 BTC to the developers of BTC, BCH and BSV software. Verified OKCoin users can vote for the project they prefer and that project's developers will receive 0.02 BTC per vote. This initiative was much discussed on Twitter, with some Bitcoiners promoting it to support the developers while others adopted a more disdainful attitude citing issues with the inclusion of BCH and BSV and the historical timeline presented. As of Oct 2 voting has closed and there are only 47 votes in total (equating to 0.94 BTC) but OKCoin have bumped the total amount donated up to 20 BTC.

CasperLabs, a startup led by Vlad Zamfir, has [received](https://www.theblockcrypto.com/post/39087/vlad-zamfir-led-blockchain-project-casperlabs-bags-14-5m-series-a-to-improve-ethereum-2-0-scalability) $14.5M in Series A funding to work on Ethereum 2.0 Scalability.

Ethereum miners [voted](https://decrypt.co/9573/ethereum-expands-blockchain-capacity-by-25-percent) to increase the gas limit for blocks (and therefore block size) by 25%, in response to rising transaction fees. Miners control the Ethereum gas limit directly and can each edge the limit up or down slightly, so it took some time for the 25% increase to be settled on.

Ethereum also saw the deployment of the Istanbul hard fork on the Ropsten testnet this month, which [happened](https://www.coindesk.com/ethereums-istanbul-upgrade-arrives-early-causes-testnet-split) earlier than expected and caused a chain split. This hard fork is expected to break a number of smart contracts in use on Ethereum mainnet, [including](https://www.coindesk.com/ethereums-istanbul-upgrade-will-break-680-smart-contracts-on-aragon) around 680 of Aragon's smart contracts.

Stellar [launched](https://www.coindesk.com/stellar-to-airdrop-2-billion-xlm-into-keybase-wallets) an airdrop campaign giving users of Keybase free XLM, over the next 20 months Keybase users will receive monthly airdrops of 100 million XLM. Over the course of the 20 months this method of distribution will increase the circulating supply of XLM by 10%. Current circulation is 20 billion XLM out of 105 billion and Stellar Development Foundation controls the distribution.

Stellar Development Foundation also [announced](https://medium.com/stellar-development-foundation/our-proposal-to-disable-inflation-8c9f8b80387) a plan to disable inflation of XLM as part of the version 12 upgrade. Stellar validators will vote to accept or reject this change. XLM inflation was intended as a way for holders to fund projects by setting an address to which their inflationary rewards would accrue. In practice, XLM holders have tended to nominate addresses they control or to join pools so that they can receive the inflation for their XLM holdings themselves. The inflation mechanism is not serving its intended purpose and therefore SDF wishes to disband it.

Dash launched the [Dash Investment Foundation](https://www.dashinvests.org), an entity which will apply for Dash Treasury funds and then invest these in projects which aim to enhance the Dash ecosystem. The DIF is a legal entity which can make loans or investments in exchange for equity in the endeavours it funds. Decisions about what to invest in will be made by a board of elected supervisors.

Tezos Foundation [announced](https://tezos.foundation/news/announcing-second-cohort-of-tezos-ecosystem-grants) funding for a second cohort of 14 Tezos Ecosystem Grants, again with no details of how much was awarded or under what terms. In an FAQ the Foundation explained that they do not disclose details of grants as it would harm their negotiating position. The Tezos Foundation Biannual [update](https://tezos.foundation/news/tezos-foundation-releases-first-biannual-report) (released and missed in Aug issue) does have some information about how the Foundation is spending its resources. In the previous year $14.8M was spent on Research, Education & Core Development, $14.1M was spent on Community grants, and $8.5M was spent on Ecosystem Tools and Applications Grants. On Jul 31 2019 the Foundation held assets valued at $652M, 61% as BTC, 15% as XTZ, 15% in a "stability fund" (diversified portfolio of Bonds, ETFs, Commodities), and 6% as USD fiat.

[Miniscript](http://bitcoin.sipa.be/miniscript/) was [announced](https://twitter.com/pwuille/status/1163592166062473217) by Pieter Wuille, it is a way to write some Bitcoin scripts in a structured way which allows static analysis, generic signing and compilation of policies. It is effectively a set of tools which make it easier to write Bitcoin scripts and be sure of how they will behave. _(missed in Aug issue)_

A large Bitcoin transaction of $1 billion caused [speculation](https://cointelegraph.com/news/someone-just-moved-1b-in-bitcoin-for-700-fee-overpaying-20-times) about who was behind it and what the purpose of the transaction was.

France has [decided](https://cointelegraph.com/news/france-wont-tax-crypto-only-trades-will-tax-crypto-to-fiat-sales) to not tax crypto-to-crypto trades. Only sells of crypto for fiat will be taxed.

European Central Bank (ECB) [started](https://www.bloomberg.com/news/articles/2019-09-12/ecb-cuts-rates-restarts-qe-to-fight-slowdown-as-draghi-era-ends) another round of quantitative easing (QE). It will "purchase" bonds (pumping the price) at a rate of 20 billion EUR per month for "as long as necessary" to hit its euro devaluation goal. This is to "stimluate" the economic growth. Or, as Murad [puts it](https://www.youtube.com/watch?v=XkvcdjSH0c0&t=9m21s), to "electrocute" people. Another good [quote](https://www.youtube.com/watch?v=XkvcdjSH0c0&t=6m21s) comes to mind: "people in cryptocurrencies believe that no living human being should have the power to create wealth from thin air". If you hold EUR or were looking to purchase bonds on a fair market, a good question to ask ECB is where the money comes from and if they worked as hard as you to earn it. Also notice how the language is carefully chosen to not call it what it is, and how hard it is to find a news piece that would explicitly mention the source of money for these "purchases".

GitHub user "DecredCoin" registered on Oct 1 2019 released ["v1.5.0 Mandatory Update"](https://archive.today/Huxft) for Decred. This is obviously a scam, as confirmed by the [virus scan](https://www.virustotal.com/gui/file/ffac37aab22c85952ba022079205700864514f44ea39cdf2bb01504ce2bb9d56/detection). Please report such things as soon as you see them.

For people who like to follow the Bitcoin discussion on Twitter, be careful what you say, as it seems the threshold for being [blocked](https://twitter.com/NickSzabo4/status/1169992390339227648) is getting lower and the overton window of acceptable discussion points or opinions is shrinking.

## 关于月报

这是Decred月报的第18. [这里](https://xaur.github.io/decred-news/)提供所有问题，镜像和翻译的索引。

来自第三方的大多数信息在经过小范围的检查后直接转发。Decred月报的作者无法验证所有声明。请注意诈骗并做自己的研究。

我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢(字母排列):

* 编写和编辑: akinsawyerr, anastasia, bee, degeri, Dustorf, richardred, s\_ben
* 评论和反馈: davecgh, emiliomann, isuldor, jholdstock, lukebp, matheusd, raedah
* 封面图片: saender

## 中文社区

* [社区web](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [优酷频道](https://i.youku.com/decredproject)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)
