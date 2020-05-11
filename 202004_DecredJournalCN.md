# Decred月报 – 2020年4月

![abstract art](img/journal-202004-384.png)

_图片: Bridge Verticals by @saender_

四月重点:

- dcrd的优化仍在继续，dcr的速度越来越快，必须更新兼容标准以防被旧版本禁用。
- @moo31337发布了一项WIP PR，用于去中心化的开发基金支出工作。
- 非常欢迎新加入Decred GitHub的5位贡献者！
- Transak和Metal Pay进行集成DCR支付的最重要一个月。Steelbackup（金属DCR种子存储解决方案）还添加了新的预算选项。
- 线下聚会已经停止，与此同时线上聚会增长迅猛尤其是拉美地区!

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以构建和运行的源代码中，但对于普通用户来说，还不能在发布的二进制文件中使用。

[dcrd](https://github.com/decred/dcrd):

- 更多代码从Go的标准字段类型大移，显着提高了性能
- `schnorr` 软件包：安全性测试和性能方面的改进，添加Decred中使用的基于Schnorr的自定义签名方案的综合[描述](https://github.com/decred/dcrd/blob/master/dcrec/secp256k1/schnorr/README.md)文件

> Schnorr签名是一种数字签名方案，以其简单性，可靠的安全性和有效的短签名生成而闻名。与ECDSA签名相比，它具有许多优势，这使其成为Decred的理想选择，唯一的缺点是，在撰写本文时，它们还没有很好地标准化。

尽管共识支持Schnorr签名，但充分利用它们的好处所需的其余基础结构尚未补足，因此它们尚未得到广泛使用。当前的工作是要对此进行补救。

与v1.5.1相比，最新版本的ECDSA和Schnorr签名验证的速度提高了约[25%](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$15862341309060voZvJ:decred.org)。

在过去的几个月中，dcrd的许多优化导致产生了一些“[错误](https://twitter.com/degeri_crypto/status/1248522626210897921)”：旧节点现在认为新版本对太多数据的请求太快而做出[禁止](https://matrix.to/#/!HEeJkbPRpAqgAwhXWO:decred.org/$158650272611269MJQhM:decred.org)反应。必须调整“兼容率”参数以支持新版本的速度。

dcrd存储库不再配置为[btcd](https://github.com/btcsuite/btcd)的fork。添加了许多新功能，并对整体进行了改进，以使它们之间几乎没有共同的代码。同样，拥有叉子的主要原因之一是能够轻松拉入上游合并。即使这样，btcd中所做的大多数更改也不再适用于dcrd。“取消分叉”还消除了有关分叉计数的困惑，其中dcrd页面显示了btcd的所有分叉数（1,500+）。现在，它显示dcrd的235个fork和btcd的1,290个。最后，在这种情况下，按“新合并请求”将针对Decred的master分支上的所有更改针对上游btcd存储库打开PR。

`dcrctl`控制dcrd和dcrwallet 的命令行应用程序已从dcrd分离到其[自己的存储库](https://github.com/decred/dcrctl)中，以解决依赖性和维护[问题](https://github.com/decred/dcrd/issues/2133)。

正在开发中:

- 去中心化开发基金的[开发工作](https://github.com/decred/dcrd/pull/2170)，以使其更加透明并让更多的人参与讨论。这项工作基于[提案](https://proposals.decred.org/proposals/c96290a2478d0a1916284438ea2c59a1215fe768a87648d04d45f6b7ecb82c3f)，但是对规范进行了重大更改。

[dcrwallet](https://github.com/decred/dcrwallet):

- 引入新的[`addtransaction`](https://github.com/decred/dcrwallet/pull/1712)命令，对于即将到来的新VSP设计将特别有用
- bug修复和代码维护
- 出于与dcrd相同的原因，[btcwallet](https://github.com/btcsuite/btcwallet)不再是btcwallet的派生分支，截至撰写时已拥有137个自己的分支

正在开发中:

- [支持](https://github.com/decred/dcrwallet/pull/1714)与dcrd工作相对应的钱包的去中心化开发基金支出。

[Decrediton](https://github.com/decred/decrediton):

- 将[ProposalsList](https://github.com/decred/decrediton/pull/2448)迁移到[功能组件](https://github.com/decred/decrediton/pull/2449)（一个较新的方法在阵营[框架](https://programmingwithmosh.com/react/react-functional-components/)-它们更容易推理和检验）
- 放弃未被[开采或卡住](https://github.com/decred/decrediton/pull/2467)的交易
- [开始](https://github.com/decred/decrediton/pull/2457)对多个组件使用pi-ui库，使Decred的不同产品具有一致的外观
- [集成](https://github.com/decred/decrediton/pull/2452)[CSPP](https://github.com/decred/decrediton/issues/2455)

[Politeia](https://github.com/decred/politeia):

- [一种](https://github.com/decred/politeia/pull/1137)查询投票的新方法
- 将元数据从Politeia提案和CMS发票中[分离](https://github.com/decred/politeia/pull/1175)出来-这是消除以前使用提案标题的简单方法，并允许添加任意元数据，包括RFP提案所需的字段
- 允许无需[javascript](https://github.com/decred/politeiagui/pull/1833)即可查看Politeia
- 归一并添加了针对Paywall数据的[缓存](https://github.com/decred/politeiagui/pull/1844)
- [完成](https://github.com/decred/politeiagui/pull/1857)状态管理系统的[重构](https://github.com/decred/politeiagui/issues/1490)
- 大量的UI工作来支持[RFP提案](https://github.com/decred/politeiagui/pull/1820)
- CMS中的几个UI调整
- Politeia和CMS中的多个bug修复

[dcrstakepool](https://github.com/decred/dcrstakepool):

- 依赖项更新和bug修复

[dcrpool](https://github.com/decred/dcrpool):

- 添加了[缓存](https://github.com/decred/dcrpool/pull/180)，从而改善了数据流（集线器现在将新数据推送到缓存中，而不是对其进行GUI轮询）
- 在多个位置添加了分页功能-这可以完成设计师提供的[正确UI](https://github.com/decred/dcrpool/issues/146)上的工作
- 可配置[帐户](https://github.com/decred/dcrpool/pull/191)，用于从中支付奖励
- 添加了GUI以手动[请求付款](https://github.com/decred/dcrpool/pull/198)并清除所有余额（离开矿池时很有用）
- 增加测试范围

[dcrlnd](https://github.com/decred/dcrlnd): In progress:

- 为远程钱包启用和测试[SPV模式](https://github.com/decred/dcrlnd/pull/95)（有关更多背景信息，请参见[3月月报](202003.md#development)）
- 在v0.9.0-beta和0.10.0-beta之间[移植](https://github.com/decred/dcrlnd/pull/99)上游lnd更改-包括139个上游PR（加上一些非PR提交）。

[dcrdex](https://github.com/decred/dcrdex):

- 添加[通知系统](https://github.com/decred/dcrdex/pull/244)以在浏览器GUI中启用实时更新
- 添加用于管理命令的[Web服务器](https://github.com/decred/dcrdex/pull/221)
- 添加签名密钥[加密](https://github.com/decred/dcrdex/pull/259)
- 无[管理](https://github.com/decred/dcrdex/pull/268)状态设置
- 完成[市场页面](https://github.com/decred/dcrdex/pull/278)
- [安全输入](https://github.com/decred/dcrdex/pull/246)敏感的命令行参数
- bug修复，代码重构，日志记录和测试改进

[dcrandroid](https://github.com/decred/dcrandroid):

- 重新设计的[登录](https://github.com/decred/dcrandroid/pull/451)页面
- 通过在DCR和“发送”页面上的法定命令之间点击来[切换](https://github.com/decred/dcrandroid/pull/461)
- 添加了[法语](https://github.com/decred/dcrandroid/pull/423)翻译
- 其他UX调整和bug修复

[dcrios](https://github.com/raedahgroup/dcrios):

- 支持使用Touch ID或Face ID的[生物特征识别启动](https://github.com/raedahgroup/dcrios/pull/613)启动身份验证
- 重新设计[登录页](https://github.com/raedahgroup/dcrios/pull/615)并将其与钱包设置[合并](https://github.com/raedahgroup/dcrios/pull/628)
- 新的“[统计信息](https://github.com/raedahgroup/dcrios/pull/627)”页面可以实现[实时更新](https://github.com/raedahgroup/dcrios/pull/666)
- 新区块[提醒](https://github.com/raedahgroup/dcrios/pull/667)
- UX调整和bug修复

[dcrdata](https://github.com/decred/dcrdata):

- 混合硬币图表的[优化](https://github.com/decred/dcrdata/pull/1690)和[数据库重构](https://github.com/decred/dcrdata/pull/1720)
- 用于查询[地址](https://github.com/decred/dcrdata/pull/1714)的新API
- 用于流通硬币[供应](https://github.com/decred/dcrdata/pull/1697)的新的简单API
- bug修复

@mm以英语和[葡萄牙语](https://stakey.club/pt/articles/)发布了有关如何查询[dcrdata](https://stakey.club/en/querying-dcrdata/)以及如何运行[自己的区块浏览器](https://stakey.club/en/dcrdata-running-your-own-block-explorer/)实例的详细指南。

[tinydecred](https://github.com/decred/tinydecred):

- 连接到dcrd所需的设置](https://github.com/decred/tinydecred/pull/156)
- 添加了对[GCS过滤器](https://github.com/decred/tinydecred/pull/149)的基本支持
- 进一步提高测试覆盖率的一个无情的测试套件
- 所有测试已迁移到[pytest](https://github.com/decred/tinydecred/pull/161)
- 使用[Cython](https://github.com/decred/tinydecred/pull/160)增强了加密基元的性能，将测试执行时间从21秒减少到4秒（快速测试可实现富有成效的开发，并带来生活乐趣）

[docs](https://github.com/decred/dcrdocs):

- [添加](https://github.com/decred/dcrdocs/pull/1087)了一个[页面](https://docs.decred.org/advanced/mnemonic-seed/)，记录了Decred和BIP-0039种子之间的区别

[decred.org](https://github.com/decred/dcrweb):

- [nojs模式](https://github.com/decred/dcrweb/pull/875)改进
- 交易所页面更新

其他：

- 用于[构建](https://github.com/decred/release)复制可执行文件的工具已移至`decred` GitHub下
- @Checkmate发布了用于实现其指标的[研究](https://github.com/checkmatey/checkonchain/blob/master/research_articles/checkonchain_charts/checkonchain_charts.md)
- GitHub已为所有人[免费提供](https://help.github.com/en/github/getting-started-with-github/faq-about-changes-to-githubs-plans)了所有核心功能，其中包括针对无限用户的私有存储库

4月的开发活动统计：分布在16个存储库中的313个活动PR，247个核心提交，添加3.9万行和删除2.3万行。每个存储库的贡献来自2-7个开发人员。

## 人员

欢迎新的首次贡献者，他的代码已合并到主代码库中： @jdambron ([dcrandroid](https://github.com/decred/dcrandroid/commits?author=jdambron)), @matthawkins90 ([dcrd](https://github.com/decred/dcrd/commits?author=matthawkins90)), @leRequinNoir ([dcrdata](https://github.com/decred/dcrdata/commits?author=leRequinNoir)), @kevinstl ([dcrdex](https://github.com/decred/dcrdex/commits?author=kevinstl)) 和 @chillviben ([dcrios](https://github.com/raedahgroup/dcrios/issues?q=is%3Aissue+author%3Achillviben)).

截至5月1日的社区统计数据：

- Twitter 粉丝: 40,570 (-124)
- Reddit 订阅:  9,761 (+1)
- Matrix 用户: 624 (+23)
- Discord 用户:  1,184 (+24)
- Telegram 用户: 2,557 (-50)
- YouTube 订阅: 3,990 (+10)
- Facebook 粉丝: 3,618 (+12), 喜欢: 3,280 (+7)
- LinkedIn 粉丝: 774 (+30)
- GitHub dcrd 星星:539 (+3), 分叉: 235 (-1,272) - 过去的fork计数包括所有btcd fork，这具有误导性，现在已删除了与btcd的fork关系，该数字现在是dcrd自己的fork

## 治理

3月份，社区开发基金获得了13,250 DCR，并花费了17,228 DCR。以3月份的每日 DCR/USD 汇率 $12.34计算，这是收到的$164K和花费的$213K。以2月份的每日平均价格$13.40计算，该月完成工作的美元费用为$231K。截至4月3日，库存余额为636,000 DCR（917万美元，折合14.42美元）。

四月份提交了两个新提案，[一个](https://proposals.decred.org/proposals/bce7bf3cd1f74d571d23ac8a330ddf29a14a547ed0cc9c995f1a97dce733d1e1)提案广告牌营销活动被拒绝，批准率为17％（参投票为31％），[另一个](https://proposals.decred.org/proposals/83b59ef5ab40193a86073abbd93cea13ed6d071eecc78918ab5cf98cba7c7a67)针对内容营销活动的CryptoNoticias提案也被拒绝，批准率为31％，参投票为30％。

3月发起，本月投票的两项提案也被拒绝。[DCR Comic 2](https://proposals.decred.org/proposals/2f08f8518bc7672069a10ac6461fd9ab341d4a9e4c343fd4a7ec426250f3896f)获得了49.4％的投票支持（19％的参投），而[Decred Daily](https://proposals.decred.org/proposals/7d42c6f4bf3059b64789185af615c1df97cb61a379425933be5ff01d074ed4d5)提案获得了17％的参投率的44％的支持。两者均未达到20％的法定人数。

有关这些提案的更多详细信息，请参见《Politeia Digest》[第30期](https://blockcommons.red/politeia-digest/issue030/)。

## 网络

全网算力:[4月份的算力](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=k8f3rvwm-k9oqhibz&scale=linear&bin=block&axis=time)以〜302 Ph/s 的速度开始，以〜360 Ph/s的速度结束，最低为240 Ph/s，并在整个月达到峰值470 Ph/s。截至5月1日的池哈希率分布：UUPool 46％，Poolin 22％，lab.antpool.com 17％，F2Pool 2％，Luxor 2％，BTC.com 1.6％，BeePool 0.12％，CoinMine 0.05％，Suprnova 0.02％和其他〜9％。池分配数是近似值，无法准确确定。

Staking: [30天的平均票价](https://dcrstats.com/)为137.8 DCR（-4.1）。该[价格](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=k8f3rvwm-k9oqhibz&bin=window&axis=time&visibility=true-false&mode=stepped) 131.7-142.8 DCR之间变化。[锁定金额](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=k8f3rvwm-k9oqhibz&scale=linear&bin=block&axis=time)为562-571万DCR，相当于参与 PoS 的[可用供应量](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=k8f3rvwm-k9oqhibz&scale=linear&bin=block&axis=time)的49.2-50.3％。

节点: 整个[四月](https://charts.dcr.farm/d/000000014/nodes?orgId=1&from=1585699200000&to=1588291200000)，每个dcr.farm平均有131个公共监听节点，总共206个节点。4月的平均版本分布：44％dcrd v1.5.1、16％dcrd v1.5、6％dcrd v1.6开发人员版本，5％dcrd v1.5开发人员和RC版本，4％dcrd v1.4、9％dcrwallet v1.5.1、2.4％dcrwallet v1.4、1.4％dcrwallet v1.5。

来自@Checkmate的更新：

- [Our Network](https://ournetwork.substack.com/p/our-network-issue-15)新闻稿([tweet](https://twitter.com/_Checkmatey_/status/1247649984473894912))的Decred部分。基于@Checkmate的库存到流量模型，PoW矿工收入和 @permabullnino的票务数据研究的多个指标表明该网络被低估了。
- 相对于网络评估，[NVT和RVT](https://twitter.com/_Checkmatey_/status/1252754120345182210)指标而言，链上交易量很大。
- 由于增加了隐私使用量，因此增加了[交易量](https://twitter.com/_Checkmatey_/status/1255084712386654209)。

## 整合

[dcr.blue](https://dcr.blue/) VSP announced that it will shut down in a message sent to all users with verified email on Apr 20. It was [removed](https://github.com/decred/dcrwebapi/pull/97) from the [listing](https://www.decred.org/vsp/) and Decrediton but will stay online for the rest of 2020. Since the maximum lifetime of a ticket is roughly 4.7 months, this gives users around 3 months to stop buying tickets assigned to DCR.Blue. Users are advised to backup their redeem scripts if they haven't already (a copy is available in the VSP account) and start buying tickets to a different VSP. Please avoid joining too large VSPs to maintain a healthy distribution and better security for the network. This is the first VSP to attempt a "graceful shutdown" rather than just disappearing without notice as some other VSPs have done in the past.

[decred.raqamiya.net](https://decred.raqamiya.net/) VSP that was [delisted](https://github.com/decred/dcrwebapi/pull/95) in March is now again operational and was [added back](https://github.com/decred/dcrwebapi/pull/96) to the listing. As of writing, it holds about 330 live tickets (0.8%), has 4 servers, and features a custom UI.

Metal Pay [added](https://twitter.com/metalpaysme/status/1249745420206686208) [support](https://blog.metalpay.com/metal-pay-welcomes-decred/) for DCR on their marketplace. It provides another fiat onramp and works in most US states. They followed the announcement with [tweets](https://twitter.com/metalpaysme/status/1250424090172612615) about Decred.

[Transak](https://global.transak.com/) [announced](https://twitter.com/transak_finance/status/1256654711412776961) that trading DCR against EUR, GBP and INR is [available](https://global.transak.com/?defaultCryptoCurrency=DCR) on their fiat < > crypto payment gateway. USD pairs are coming soon.

An instant exchange [SwapSpace](https://swapspace.co/) [added](https://twitter.com/SwapSpaceCo/status/1250078395884539906) support for Decred.

[Steelbackup](https://steelbackup.com/), a physical seed backup solution added a [light version](https://twitter.com/steelbackup/status/1248058631523905538) of the product. Currently, there are two types of steel plates: [laser engraved](https://steelbackup.com/product/decred-laser-engraved/) and [laser marked](https://steelbackup.com/product/decred-laser-marked/). The engraved one is the most robust solution as steel is removed which makes the marking grid as permanent as the steel. The laser marked product is marked with a molybdenum disulfide solution which makes it resistant to scratches, acids, and high temperatures (up to 340 degrees C). The products are designed to be simple with no moving parts, users just need a center punch (found at a local hardware store) to indent their seed. Tamper evident bags are included. SteelBackup was launched in Feb 2020 by @zubair and ships worldwide.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

Decred's YouTube [channel](https://www.youtube.com/decredchannel) grew by 4 new videos, while Decred in Depth and Rough Consensus podcasts released 3 episodes in total (see [Media](#media) below).

Decred Brazil [channel](https://www.youtube.com/channel/UC73wa2ddXuPWsmenVfeFTYg) keeps actively generating content. Decred Semanal ("Decred Weekly") published 5 new episodes in April which received ~150 views on average, up from ~50 views in previous months (likely a result of [improved](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$158896614628001AwmOM:decred.org) distribution tactics). The series is also available in podcast format on all major platforms like [Apple](https://podcasts.apple.com/podcast/decred-brasil/id1451017413) (59 episodes total), Google, Spotify, [SoundCloud](https://soundcloud.com/decredbrasil) and others.

On Medium, [Decred Drive](https://twitter.com/decreddrive) keeps delivering nice weekly updates, [Decred Spanish](https://medium.com/decred-es) is adding new articles and translations, and [Phoenix Green](https://medium.com/@kencameron77) has emerged with writings about his crypto/Decred journey.

@jy-p commented on fiat credit issuance and remote work in a project survey by [8btc.com](https://news.8btc.com/8btc-interview-cryptos-and-coronavirus-what-we-learned-from-foreign-communities). 8btc is the oldest Bitcoin forum in China.

Monde PR's achievements for April:

- created and pitched a story idea targeted at investing, VC and tech publications
- created and pitched a story idea targeted at crypto and fintech publications
- created and pitched a story idea targeted at personal finance publications
- submitted comments from Decred spokespeople to 8 news stories
- secured a media interview with a mainstream newswire and 3 email Q&As with mainstream and crypto publications

News coverage secured by Monde PR:

- a thought leadership piece in [ValueWalk](https://www.valuewalk.com/2020/04/open-source-response-covid-19/) by @richardred
- an article in [Cointelegraph](https://cointelegraph.com/news/harsh-stablecoin-recommendations-from-g-20-are-a-step-in-the-right-direction-but-regulators-need-more-education) featuring commentary by @jy-p on the future of stablecoins, syndicated to [Investing.com](https://www.investing.com/news/cryptocurrency-news/g20s-harsh-stance-on-stablecoin-is-a-step-forward-but-regulators-have-more-to-learn-2144200) and [Bitcoin News Network](https://www.btcnn.com/harsh-stablecoin-recommendations-from-g-20-are-a-step-in-the-right-direction-but-regulators-need-more-education/)

## Events

Attended:

- Apr 4 - [Paxful Conversations](https://twitter.com/paxful_LATAM/status/1245066931155148800) - Internet. @elian was invited by Paxful LATAM to talk about how to spot scams and what to look at when researching cryptocurrency fundamentals. It was not a direct Decred talk but it was mentioned as an example of good practices within the industry. The webinar was "powered by Decred" and was viewed by ~70 people.
- Apr 9 - Hablemos Decred 03 - Internet. @pablito and @elian explained the PoS system. There were only 3 new viewers this time, although some lessons were learned about promoting the event and picking the optimal time. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200409-hablemosdecred-03-internet.md))
- Apr 16 - [Jalisco Talend Land @ Home](https://www.talent-land.tv/) - Internet. Decred team presented a panel titled "The future of money and remote work" to explore the intersection of money, technology, and remote working through the lens and experience of 4 Decred contractors in LATAM. They shared their experience working from Argentina, Colombia, and Mexico, and covered the challenges and opportunities of working for Decred remotely. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200416-talent-land-at-home-internet.md))
- Apr 16 - Hablemos de Criptomonedas - Internet. The webinar was co-hosted with Ibero University through its innovation hub IDIT. @adcade and @elian talked about cryptocurrency and blockchain to an audience of 22 (out of 34 registrations), mostly students. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200416-hablemos-de-criptomonedas-internet.md))
- Apr 23 - Hablemos Decred 04 - Internet. @pablito and @elian focused on exchanges and the DEX that Decred is building. Attendance was up to 15 this time, and the LATAM team is continuing to explore the best ways to host such events. ([report](https://github.com/decredcommunity/events/blob/master/reports/20200423-hablemosdecred-04-internet.md))
- Apr 30 - [Decred Virtual Meetup](https://www.meetup.com/Decred-Australia/events/270252645/) - Internet. @Checkmate presented his BTC and DCR on-chain analytics. The recording was uploaded to [YouTube](https://www.youtube.com/watch?v=H_COE9A-t3I).

Upcoming:

- May 12 - [Decred Foundations at Consensus Distributed](https://next.brella.io/events/consensusdistributed/schedule/118434) (requires signup at brella.io to view and "attend") - Internet. Consensus Distributed is the remote replacement for the annual Consensus conference, and Decred is one of the projects which was invited to contribute an hour of content, broken into 3 segments. In Construct, @richardred checks in with contributors to some important Decred subprojects to find out what they're about and what the latest is. Featuring @lukebp on Politeia, @matheusd on dcrlnd, @chappjc, and @buck54321 on dcrdex, dcrdata and TinyDecred. The second segment is Trade Secrets, where @Checkmate will be giving a quick intro to his top 5 Decred on-chain metrics. To finish, @jy-p will present a review of the year's progress across all of the major aspects of the project in ChangeLog, followed by a 10 minute live Q&A with Lucas Nuzzi. Video will be available on the Coindesk website afterwards, and an extended version of Trade Secrets will be uploaded to Youtube.
- May 14 - [Virtual meetup with BlockchainEx](https://twitter.com/Decred_ES/status/1258905004510973953) - Internet. Decred will participate in the panel "What is decentralized governance and DAOs?" co-hosted by @adcade and @caibarrad from Decred, Nadia Alvarez from MakerDAO, Gustavo Segovia from Colony and Jhonny Gomez from BlockchainEx. This panel will be live-streamed to the blockchain community in Colombia.
- May 14 - [Decred meetup with BlockConf](https://twitter.com/Decred_ES/status/1258165218204618759) - Internet. This will be a virtual meetup to showcase the platform and a fireside chat before the main conference. The team will give a brief on Decred's fundamentals and new developments in the pipeline.
- May 25 - [BlockConf](https://blockconf.digital/) - Internet. Decred is a [bronze sponsor](https://twitter.com/BlockconfD/status/1251194332079697922). Decred LATAM team will run a virtual booth for Decred to answer questions from the attendees. If anyone wants to help with keeping the booth active in several time zones during the 48-hour event, please contact @elian.

![Jalisco Talent Land @ Home shot](img/latam-stakeys-360.jpg)

_Image: No shortage of Stakey in LATAM_

## Media

Selected articles:

- Decred on-chain: Strongest hand market cap + ratio by @PermabullNino ([medium](https://medium.com/@permabullnino/decred-on-chain-strongest-hand-market-cap-ratio-146d6854e1d6))
- Decred market maker monitoring - Phase 1 wrap-up by @richardred ([blockcommons.red](https://blockcommons.red/publication/mm-phase1-wrapup/))
- Our Network issue #15 - featuring Decred updates from @Checkmate ([substack.com](https://ournetwork.substack.com/p/our-network-issue-15))
- Decred governance proposal: Protecting the Treasury by Phoenix Green ([medium](https://medium.com/phoenix-green/decred-governance-proposal-protecting-the-treasury-2bcab84800ad))
- Finance 2.0 by Phoenix Green ([medium](https://medium.com/@kencameron77/finance-2-0-5dea40e4b60e))
- The open-sourced mindset for finance by Phoenix Green ([medium](https://medium.com/@kencameron77/open-sourced-finance-7ce8a3fdb648)) - calls to think collectively and find common grounds, and lists tools to build a community
- 3 things everyone should know about cryptocurrencies by Phoenix Green ([medium](https://medium.com/@kencameron77/3-things-everyone-should-know-about-cryptocurrencies-e38c3db4127b))
- The Bitcoin time machine by Phoenix Green ([medium](https://medium.com/@kencameron77/the-bitcoin-time-machine-29f228656cd3)) - compared Bitcoin with Decred
- What if Bitcoin had a Treasury? by Ryan Watkins ([messari.io](https://messari.io/article/what-if-bitcoin-had-a-treasury), paywalled)
- Project Rundown interview with Decred by The Capital (former Altcoin Magazine, [medium](https://medium.com/the-capital/project-rundown-interview-with-decred-on-the-capital-8b647919a339))
- Let's talk about Decred and remote work by @adcade (in Spanish, [medium](https://medium.com/decred-es/hablemos-decred-sobre-el-proyecto-y-sobre-el-trabajo-remoto-e5a2510364ae))
- Article on the 4th Decred virtual meetup about CEXes and DEXes (in Spanish, [es.cointelegraph.com](https://es.cointelegraph.com/news/decred-organizes-virtual-meeting-on-decentralized-exchanges-for-the-spanish-speaking-community))

Translations:

- Secrets they missed at DevCon: What it's really like in a working DAO - [in Portuguese](https://stakey.club/translated/working-dao/) by @mm.
- Decred Journal March 2020 was translated to Arabic (@arij), Chinese (@Dominic), Polish (@kozel), and Spanish (@francov\_). @kozel is back in the game with 4 translated issues since December. Shortened Spanish versions are available on [Medium](https://medium.com/decred-es/revista-2020/home). Thank you all for building awareness of the project!

Videos:

- DCR 101 - Working for the Decred DAO by @Exitus ([youtube](https://www.youtube.com/watch?Ud4LVhFwL9g))
- Decred bi-weekly news update - April 18th, 2020 by @Exitus ([youtube](https://www.youtube.com/watch?v=3TLeEO8Mz1k))
- Decred Australia virtual meetup - BTC & DCR on-chain analytics event with @Checkmate ([youtube](https://www.youtube.com/watch?v=H_COE9A-t3I))
- Psychic Andre has good feelings about things going up, the video is mostly about the Federal Reserve but on the subject of Decred Andre says "they're fine" ([youtube](https://www.youtube.com/watch?v=ddjelXN5KZs))
- The Federal Reserve in its own words. Protect your wealth, buy Decentralized Credits ([twitter](https://twitter.com/coveryfire7777/status/1246169256020107266))
- DCR 101 - How to stake Decred by @Exitus ([youtube](https://www.youtube.com/watch?v=m5lcm6yttEk))
- Decred price analysis - 17th April 2020 by Brave New Coin ([youtube](https://www.youtube.com/watch?v=Q33i6xK_SPg))

Audio:

- Rough Consensus Ep. 4 - Gold, Bitcoin, and Decred. @mr.black, @Checkmate, and @PermabullNino discuss the state of macro and crypto markets in the context of collapsing economies and unlimited QE. The conversation considers the nature of sound money and how gold, Bitcoin, and Decred represent different areas of the sound money spectrum. ([libsyn](https://roughconsensus.libsyn.com/rough-consensus-4-gold-bitcoin-and-decred))
- Decred in Depth - Round Up 2 with @mr.black, @Checkmate and @PermabullNino. ([libsyn](https://decredindepth.libsyn.com/dcr-round-up-2-with-checkmate-permabull-nio), [youtube](https://www.youtube.com/watch?v=eb_GFdOkjwA), [soundcloud](https://soundcloud.com/decredindepth/dcr-round-up-2-with-checkmate))
- Decred in Depth (has given up on numbering) - Chris Burniske of Placeholder VC talks about recent developments, why Decred HAS (Hypersecure Adaptable Sustainable) it, opportunities for dcrdex, and Politeia to expand the Decred ecosystem, and much more! ([libsyn](https://decredindepth.libsyn.com/chris-burniske-institutional-investment-dcr-as-a-sov-current-events-dcr-custody-solutions), [youtube](https://www.youtube.com/watch?v=Q4wbt0JLA5k), [soundcloud](https://soundcloud.com/decredindepth/chris-burniske-crypto-in-the))

## Community Discussions

Selected Reddit posts:

- The Decred Journal's own Reddit [post](https://www.reddit.com/r/decred/comments/fy493y/decred_journal_march_2020/) was the most discussed one on the subreddit this month with 42 comments!
- The discussion of @bee's idea to add [vote reason](https://github.com/decredcommunity/issues/issues/118) information to Politeia votes [concluded](https://www.reddit.com/r/decred/comments/g2ozqc/reason_bits_for_politeia_no_votes_feature_idea/) that implementing it properly requires a privacy solution like a blind voting scheme.
- Phase 1 market making report [discussion](https://www.reddit.com/r/decred/comments/g5he83/decred_market_maker_monitoring_phase_1_wrapup/) speculated about the rate of adoption.
- [Perspectives](https://www.reddit.com/r/decred/comments/g66onn/perspectives/) thread collected 33 comments of which many are long read quality thinking.
- [Decred: Do Different](https://www.reddit.com/r/decred/comments/g66msa/decred_challenge_do_different/) mini-game.
- The [post](https://www.reddit.com/r/decred/comments/fyi49j/checkmate_on_twitter_cost_to_launch_a_1hr_double/) discussing @Checkmate's methodology of comparing the attack cost of Decred and other chains.

Selected Twitter discussions:

- @Checkmate [tweeted](https://twitter.com/_Checkmatey_/status/1248498765113126912) about the cost to double spend attack DCR being 54x higher than BTC, stimulating much discussion.
- @Checkmate [announced](https://twitter.com/_Checkmatey_/status/1253116008639811585) the launch of a new project, with a team of contributors working on a new Decred on-chain metrics site.
- Messari [musing](https://twitter.com/MessariCrypto/status/1255579343973232640) on what if Bitcoin had Decred's treasury, and [graphing](https://twitter.com/MessariCrypto/status/1255579345319596033) out how much that would have been worth if Bitcoin had spent ~23% of its monthly treasury income and saved the rest.
- @moo31337 [tweeted](https://twitter.com/marco_peereboom/status/1251174260925779977) about a WIP PR for work on the decentralized treasury spending proposal, but more than half of the comments were really concerned about his next cooking adventure.

![pork](img/marco-cooking.jpg "pork")

## Markets

In April DCR was trading between USD 11.08-15.01 / BTC 0.00151-0.00179. The average daily rate was $12.34.

@richardred wrote a [report](https://blockcommons.red/publication/mm-phase1-wrapup/) about the performance of the market makers during the term of their first [proposal](https://proposals.decred.org/proposals/2eb7ddb29f151691ba14ac8c54d53f6692c1f5e8fe06244edf7d3c33fb440bd9).

## Relevant External

[Another](https://www.coindesk.com/dforce-hacker-returns-almost-all-of-stolen-25m-in-crypto) DeFi attack occurred, although this time dForce got most of its lost $25 million back from the attacker and users are being reimbursed.

On the more obscure stablecoin network [PegNet](https://www.coindesk.com/miners-trick-stablecoin-protocol-pegnet-turning-11-into-almost-7m-hoard), rogue miners turned a $11 pJYP balance into a 6.7 million pUSD balance by manipulating price oracles with a form of 51% attack. The attackers were unable to liquidate more than a small proportion of the pUSD, and have subsequently reached out to say they were just trying to pen test the network, and have burned the magically created pUSD.

People are [wondering](https://twitter.com/econoar/status/1254063336779444226) why ProgPoW is back on the Ethereum Core devs agenda, and whether the inability to shake it off means there is something [rotten](https://twitter.com/hasufl/status/1254065039105024001) in Ethereum's governance.

The US Government's $349 billion loan program for small businesses has so far generated $10 billion in [fees](https://www.npr.org/2020/04/22/840678984/small-business-rescue-earned-banks-10-billion-in-fees) for banks, 1-5% for each loan processed, despite the very low risk the loans posed to the banks, considering that they were effectively just passing them on to the Small Business Administration which guaranteed all the loans. ([plaintext version](https://www.npr.org/2020/04/22/840678984/small-business-rescue-earned-banks-10-billion-in-fees))

Maker Foundation is subject to a [lawsuit](https://www.coindesk.com/makerdao-users-sue-stablecoin-issuer-following-black-thursday-losses) from investors who lost money in Black Thursday.

There have been a whole [barrage](https://www.theblockcrypto.com/post/60930/top-crypto-exchanges-token-issuers-named-in-friday-barrage-of-u-s-class-action-lawsuits) of class-action lawsuits filed against crypto exchanges and token issuers.

USDT balance held on exchanges has reached a new ATH of [$1.8 billion](https://twitter.com/glassnodealerts/status/1253343292403724294) on Apr 23, according to glassnode alerts.

YouTube have updated their policies to disallow anything about COVID-19 that goes against "authoritative sources" like the World Health Organization's guidelines, as disclosed in an [interview](https://reclaimthenet.org/youtube-ceo-coronavirus-right-information-misinformation/) with YouTube's CEO. While YouTube censoring videos on certain topics is not new, having these decisions be determined fluidly with reference to what "authoritative sources" are saying, and deliberately channelling traffic to those sources, is new.

In an update to the story about the sale of .org domain to a private equity firm, ICANN has [voted](https://twitter.com/EFF/status/1256053946289774594) to reject the sale, effectively blocking it.

## About This Issue

This is issue 25 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback) and [contributions](https://github.com/xaur/decred-news/blob/docs/contributing.md) are always welcome.

Credits (alphabetical order):

- writing and editing: bee, degeri, elian, Exitus, l1ndseymm, pablito, richardred, s\_ben, zubair
- reviews and feedback: chappjc, davecgh, emiliomann, jholdstock, jrick, lukebp
- title image: saender

