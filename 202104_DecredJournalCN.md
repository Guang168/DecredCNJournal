# Decred月报 – 2021年4月

![abstract art by @saender](img/202104.1.github.png)

_图片:@saender_

四月亮点：

- Decred的第六次共识投票已获得一致通过并获得了很高的参投率。
- Politeia v1.0现在更具可扩展性并且是面向未来的基础架构。
- 正在对Politeia的第一个开发提案进行投票，以正式确定发展路线和预算。
- DCRDEX正朝着v0.2更新的方向发展，它对后端和UX进行了一些改进，并为将来令人兴奋的功能奠定了基础。
- 初始版DCRDEX集成已合并到Decrediton中。

内容：

- [开发进展总结](#development)
- [人员](#people)
- [治理](#governance)
- [网络](#network)
- [整合](#integrations)
- [外展](#outreach)
- [活动](#events)
- [媒体](#media)
- [社区讨论](#community-discussions)
- [市场](#markets)
- [相关外部信息](#relevant-external)

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以[构建和运行](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c)的源代码中，但对于普通用户来说，还不能使用。

<a id="dcrd" />

**[dcrd](https://github.com/decred/dcrd)**

- 代码库已[转换](https://github.com/decred/dcrd/pull/2625)为使用新`stdaddr`程序包。现在，处理地址的代码支持不同的脚本版本，并且距离能够干净地引入新的脚本语言版本仅一步之遥。与大的更改一样，为了使审核更容易，此操作被分成一系列单独的提交，以便每一个步骤的每一步都建立并通过所有测试。
- 引入[UTXO](https://github.com/decred/dcrd/pull/2632)数据库。它为专门的UTXO数据库实现铺平了道路，可以在处理时间和内存使用方面提高效率。
- 在最后11个区块中增加了[中位时间](https://github.com/decred/dcrd/pull/2638)来表示详细信息`getblock` 和 `getblockheader`结果（由DCRDEX使用）
- 允许指定网络接口以使用其[名称](https://github.com/decred/dcrd/pull/2623)以及确切的IP地址进行侦听

dcrd v1.4.0与最新版本之间的初始链同步[比较](https://www.reddit.com/r/decred/comments/mi4ezt/initial_chain_sync_comparison_between_dcrd_v140/)显示了所有改进如何累积到性能上的巨大差异。尽管现在的块增加了约70％，但最新版本几乎需要花费相同的时间来同步，同时分配的内存更少。

<a id="dcrwallet" />

**[dcrwallet](https://github.com/decred/dcrwallet)**

- 一种返回钱包[同步状态](https://github.com/decred/dcrwallet/pull/1991)的新方法
- 当VSP[收到](https://github.com/decred/dcrwallet/pull/1965)费用tx但尚未广播时，处理选票状态
- 修复了由DCRDEX使用时发现的bug

<a id="decrediton" />

**[Decrediton](https://github.com/decred/decrediton)**

- 初始[DEX集成](https://github.com/decred/decrediton/pull/3356)
- 允许使用现有的电子钱包帐户[代替](https://github.com/decred/decrediton/pull/3438)DEX
- 添加了[QR码](https://github.com/decred/decrediton/pull/3112)生成功能以导出活动选票（用于使用Decred Address Scanner应用程序进行跟踪）
- 选票自动购买设置[记忆](https://github.com/decred/decrediton/pull/3441)
- 添加了一个迁移，以使用钱包密码来初始化[帐户](https://github.com/decred/decrediton/pull/2664)密码。此外，某些操作（发送，购买票证，混合，吊销）切换为仅解锁单个帐户，而不是解锁整个钱包。
- 创建后锁定[新帐户](https://github.com/decred/decrediton/pull/3424)
- 允许恢复最多128个字符的十六进制种子（包括BIP0039种子）
- 更新了[交易](https://github.com/decred/decrediton/pull/3326), [提案](https://github.com/decred/decrediton/pull/3345)和[购票](https://github.com/decred/decrediton/pull/3349)视图的设计
- 许多较小的设计调整
- 切换到严格的Protobuf生成，而没有eval()并且仅限于https使用CSP标头通过生产版本访问外部服务器
- 状态管理重构，关注点分离，依赖关系升级
- 增加测试范围
- 修复约为24个bug

正在准备v1.6.3版，其中包括许多上述更改。

<a id="politeia" />

**[Politeia](https://github.com/decred/politeia)**

Politeia v1.0.0已发布，具有新的存储后端，简化的API，新的插件体系结构和5个插件。阅读[发行说明](https://github.com/decred/politeia/releases/tag/v1.0.0)以获取有关每个功能的完整详细信息。新版本已部署在[proposals.decred.org](https://proposals.decred.org/)上。

2FA双重验证已支持。用户可以在帐户设置中进行设置。不要忘记备份密钥。

四月份合并：

- 为了方便起见，在proposal.decred.org上列出了[proposals-archive.decred.org](https://proposals-archive.decred.org/)中的提案
- 使用新`politeiaverify`工具[验证](https://github.com/decred/politeia/pull/1377)评论和投票
- 在购买[历史](https://github.com/decred/politeiagui/pull/2322)中列出注册费
- 修复了新版本中发现的约24个bug

一个显着的变化是添加了[时间戳](https://github.com/decred/politeia/pull/1395)以进行投票。在Git后端，没有存储准确的时间戳以改善选民的隐私，因此，只能确定是否在约60分钟内进行了投票。在tstore中，Trillian已经记录了后端时间戳，除非编写自定义Trillian实现，否则无法更改此时间戳。由于表决时间戳现在无论如何都是公共数据，因此将其直接添加到表决结构中可使dcrdata更加轻松地获取它（例如，构建其表决图）。但这也意味着对于一次投票的人们来说，隐私权会有所降低。谁想要保护自己的隐私的人，强烈建议使用politeiavoter的功能。

@lukebp讨论了Politeia的发展，最新版本以及Decred in Depth[播客](https://www.youtube.com/watch?v=J6IAjmwkki0)的未来方向（从12分钟开始）。

Politeia自己的第一个[提案](https://proposals.decred.org/record/91cfcc8)现已上线（并投票），正式制定了其发展路线图和预算，直至2021年底。

<a id="dcrpool" />

**[dcrpool](https://github.com/decred/dcrpool)**

- 改善连接性
- 更有效的 矿工 处理

<a id="dcrlnd" />

**[dcrlnd](https://github.com/decred/dcrlnd)**

- 支持[解锁](https://github.com/decred/dcrlnd/pull/136)特定帐户（对于Decrediton）

<a id="dcrdex" />

**[DCRDEX](https://github.com/decred/dcrdex)**

- 在用户支付注册费之前显示重要的[服务器信息](https://github.com/decred/dcrdex/pull/1042)（例如最小可交易量）
- 更好地处理[无效](https://github.com/decred/dcrdex/pull/1030)订单
- 使用[中位数时间](https://github.com/decred/dcrdex/pull/1058)完成交易
- 确保所有[费用费率](https://github.com/decred/dcrdex/pull/1060)均受配置限制
- 减少数据库升级期间的[内存](https://github.com/decred/dcrdex/pull/1070)使用量
- [响应式](https://github.com/decred/dcrdex/pull/1016)GUI
- 支持CPU和HTTP[分析](https://github.com/decred/dcrdex/pull/1035)
- 改进了[couch](https://github.com/decred/dcrdex/pull/1038)测试体验
- 为[服务器API](https://github.com/decred/dcrdex/pull/1047)和[资产后端](https://github.com/decred/dcrdex/pull/1054)添加了版本控制
- 修复了一些同步问题

An [update](https://www.reddit.com/r/decred/comments/n9i8z2/dcrdex_updates_v02_release_decrediton_integration/) on Phase 2 development was posted in May with the following key points:

- v0.2 release has finished beta testing, expect binaries and server update soon
- v0.2 brings many improvements, including support for the upcoming Decrediton integration
- SPV wallet support for both Decred and Bitcoin are planned in next releases this year
- ETH development is in progress and is expected to release toward the end of Phase 2
- for more exciting features read the [update](https://www.reddit.com/r/decred/comments/n9i8z2/dcrdex_updates_v02_release_decrediton_integration/) and the linked release notes

<a id="dcrandroid" />

**[dcrandroid](https://github.com/planetdecred/dcrandroid)**

- show [USD equivalent](https://github.com/planetdecred/dcrandroid/pull/539) balance on Overview page
- dcrlibwallet [updated](https://github.com/planetdecred/dcrlibwallet/pull/183) to new dcrwallet module

<a id="dcrios" />

**[dcrios](https://github.com/planetdecred/dcrios)**

- show Politeia [proposals](https://github.com/planetdecred/dcrios/pull/715) and notify on certain events (new proposal, vote started, vote ended)
- database [upgraded](https://github.com/planetdecred/dcrios/pull/742) to BadgerDB

<a id="godcr" />

**[godcr](https://github.com/planetdecred/godcr)**

- show Politeia [proposals](https://github.com/planetdecred/godcr/pull/331)
- polished UI on [Transactions](https://github.com/planetdecred/godcr/pull/356), [Wallet](https://github.com/planetdecred/godcr/pull/355), and [Receive](https://github.com/planetdecred/godcr/pull/354) pages
- show USD equivalent on the [nav bar](https://github.com/planetdecred/godcr/pull/380) and on the [Send](https://github.com/planetdecred/godcr/pull/371) confirmation popup
- added sending to own [account](https://github.com/planetdecred/godcr/pull/353)
- numerous smaller UX tweaks

<a id="dcrdata" />

**[dcrdata](https://github.com/decred/dcrdata)**

- improved [Attack cost](https://github.com/decred/dcrdata/pull/1777) page layout
- improved display of [Treasury](https://github.com/decred/dcrdata/pull/1817)-related tx
- updated to [Webpack 5](https://github.com/decred/dcrdata/pull/1809) and other dependencies

<a id="dcrdocs" />

**[docs](https://github.com/decred/dcrdocs)**

- [dark mode](https://github.com/decred/dcrdocs/pull/1161)!
- [Migrations](https://github.com/decred/dcrdocs/pull/1163) page for the upcoming Decrediton v1.6.3

## People

Get to know Decred contributors in the new interviews with [@lukebp](https://www.youtube.com/watch?v=J6IAjmwkki0) and [@phoenixgreen](https://www.youtube.com/watch?v=WOVUvzsp3Eo).

Community stats as of May 1:

- [Twitter](https://twitter.com/decredproject) followers: 44,391 (+763)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 10,987 (+190)
- [Matrix](https://chat.decred.org/) #general users: 434 (+27)
- [Discord](https://discord.gg/GJ2GXfz) users: 1,566 (+157)
- [Telegram](https://t.me/Decred) users: 2,645 (+51)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,500 (+40), views: 182K (+3K)
- GitHub [dcrd](https://github.com/decred/dcrd) stars: 591 (+2), forks: 254 (-1)

See the [April report](https://decredcommunity.github.io/social-media-stats/posts/20210506.1) for notable social media stats updates.

## Governance

In April the [Treasury](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) received 10,949 DCR and spent 984 DCR. Using April's average DCR rate of $198.60, this is $2.17M received and $195K spent. At March's average rate of $161.01, the USD billed for past work is $158K. As of May 2, the Treasury balance is 672,768 DCR (140 million USD at $208.13).

The consensus vote to enable the new treasury has [passed](https://explorer.dcrdata.org/agenda/treasury) with 99.9% approval and 83% voter participation. This is the second highest voter turnout in Decred's history after the [stake difficulty](https://dcrdata.decred.org/agenda/sdiffalgorithm) vote in 2017 (88%).

Proposal news:

- A new [proposal](https://proposals.decred.org/record/91cfcc8) for funding Politeia development accompanied the deployment of v1.0.0. This proposal requests a maximum budget of $118K to cover a range of new features, expected to be delivered over a six month period. The features on this roadmap include another upgrade to the plugin architecture, user API overhaul, email-free accounts, extra metadata for proposals, proposal life cycles, and proposal author updates. The vote started on May 11.
- The video production phase 3 [proposal](https://proposals-archive.decred.org/proposals/95a1409) was approved with 98% approval and voter participation of 40%.
- The Design domain [proposal](https://proposals-archive.decred.org/proposals/76eba5a) for the remainder of 2021 was approved with 97% approval and voter participation of 28%.

See Politeia Digest [issue 42](https://blockcommons.red/politeia-digest/issue042/) for more details on the month's proposals.

## Network

**Hashrate**: April's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kmvlwq6x-ko7rp8zy&scale=linear&bin=block&axis=time) opened at ~464 Ph/s and closed ~429 Ph/s, bottoming at 219 Ph/s and peaking at 587 Ph/s throughout the month.

Distribution of hashrate [reported](https://miningpoolstats.stream/decred) by the pools on May 1: Poolin 35%, Antpool 28%, F2Pool 18%, Easy2Mine 4%, BTC.com 1.8%, Luxor 1.3%, UUPool 0.09%, Coinmine 0.06%, Huobipool 0.02%, others 12%. This time the reported hashrate closely matched the distribution of 1,000 actually [mined blocks](https://miningpoolstats.stream/decred).

A sharp hashrate drop around Apr 15-20 has been attributed to a major [power outage](https://www.reddit.com/r/decred/comments/mvk976/network_hashrate_plummeting/) in China.

**Staking**: [Ticket price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kmvlwq6x-ko7rp8zy&axis=time&visibility=true-false&mode=stepped) varied between 163.5-204.1 DCR, with 30-day [average](https://dcrstats.com/) at 185.8 DCR (+7.8).

The [locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kmvlwq6x-ko7rp8zy&scale=linear&bin=block&axis=time) was 7.11-7.51 million DCR, meaning that 55.4-58.5% of the circulating supply [participated](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kmvlwq6x-ko7rp8zy&scale=linear&bin=block&axis=time) in proof-of-stake.

**VSP**: On May 1, 7.1K (+0.5K) live tickets were managed by vspd servers and 2.2K (-1.8K) by the [listed](https://decred.org/vsp/) legacy dcrstakepool servers. Collectively the 15 legacy and 13 new VSPs managed 23% of the ticket pool. The 2 recently delisted legacy VSPs still had 105 live tickets.

**Nodes**: Throughout April there were around ~210 reachable nodes according to [dcrextdata](https://dcrextdata.planetdecred.org/nodes).

Node versions as of May 1 [snapshot](https://nodes.jholdstock.uk/user_agents) (257 total, dcrd only): v1.6.0 - 26%, v1.6.2 - 24%, v1.6.1 - 22%, v1.5.2 - 7%, v1.5.1 - 7%, v1.7 dev builds - 7%, v1.6 dev builds - 4%, v1.5.0 - 2%.

The share of [mixed coins](https://explorer.dcrdata.org/charts?chart=coin-supply&zoom=kmvlwq6x-ko7rp8zy&bin=day&axis=time&visibility=true-true-true) has slightly declined from 44% to 42%. Daily [mixed amount](https://explorer.dcrdata.org/charts?chart=privacy-participation&zoom=kguk0rxu-koc4hs00&bin=day&axis=time) varied between 150-300K DCR.

Bison's presence has been spotted on [LN](https://ln-map.jholdstock.uk/) as a node called "El Gran Bisonte ⚡🐂⚡".

## Ecosystem

Welcome the new [vspd](https://github.com/decred/vspd) server from [stakey.com](https://vspd.stakey.com/) with 0.3% fee - lowest on the market as of writing. Its legacy VSP server has been removed from the [listing](https://decred.org/vsp/) but is still operational with 80 [live tickets](https://stakey.com/stats) as of May 7.

dcr.farm's [legacy VSP](https://dcr.farm/stats) was observed with a 30% fee, possibly to discourage new registrations. Pay attention to the fees to not buy a high-fee ticket by accident. dcr.farm's [vspd server](https://vsp.dcr.farm/) has a normal 0.95% fee.

[Baap ATM](https://baap.app/) [tweeted](https://twitter.com/baapapp/status/1376975012830326786) that their ATMs and agents will help to [buy DCR](https://baap.app/buy-decred-coin/) for CAD in some locations in Canada.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to anyone.

Join our [#services](https://chat.decred.org/#/room/#services:decred.org) chat to follow Decred ecosystem updates.

## Outreach

A new process has been set up to broadcast important project announcements on multiple platforms. The "ANNs" are issued only for important updates and have much lower traffic compared to Decred's [Twitter](https://twitter.com/decredproject). Matrix room [#dcr](https://chat.decred.org/#/room/#dcr:decred.org) is the newest addition, the other destinations being: [Twitter](https://twitter.com/decredproject), [Telegram](https://t.me/DCRann), Discord, [Reddit](https://www.reddit.com/r/decred/), [CoinGecko](https://www.coingecko.com/en/coins/decred), [Blockfolio](https://blockfolio.com/coin/DCR), and [Gab](https://gab.com/decredproject).

Supporters on Reddit have made the case for Decred in multiple relevant conversations on r/CryptoCurrency ([one](https://www.reddit.com/r/CryptoCurrency/comments/m03ay0/what_are_your_favorite_top_100_coins_to_stake_and/), [two](https://www.reddit.com/r/CryptoCurrency/comments/m2cza0/lets_talk_about_dexs_and_do_we_really_need_so_many/), [three](https://www.reddit.com/r/CryptoCurrency/comments/m895oa/which_is_your_favorite_dao/), [four](https://www.reddit.com/r/CryptoCurrency/comments/madahw/you_can_buy_5_coins_now_anf_only_access_them/), [five](https://www.reddit.com/r/CryptoCurrency/comments/mcqzk7/too_many_post_your_undervalued_coins_posts_here/), [six](https://www.reddit.com/r/CryptoCurrency/comments/msifo2/one_crypto_for_the_rest_of_your_life/)). Thank you all for spreading awareness.

Monde PR's achievements for April:

- created/pitched 2 stories to finance and crypto publications
- secured 2 media interviews
- responded to 1 request for comment

News coverage secured by Monde PR:

- the Decred treasury announcement was covered by [Bankless Times](https://www.banklesstimes.com/2021/04/12/decred-makes-consensus-change-to-further-decentralize-128m-treasury/)
- an interview with @lukebp on the [Keyword: Crypto podcast](https://www.keywordcrypto.com/luke-p-from-decred/)

## Events

Attended:

- Apr 21 - [Blockchain Land](https://blockchainland.talent-republic.tv/) - Internet. @adcade talked about "[Opinions](https://blockchainland.talent-republic.tv/on-demand/que-opinar-sobre-las-criptomonedas/) on cryptocurrencies" and the [future](https://blockchainland.talent-republic.tv/on-demand/blockchains-futuro-escalabilidad-u-oportunismo/) of crypto as part of Decred participation in Blockchain Land by Talent Land. The panels were streamed in [virtual worlds](https://es.cointelegraph.com/news/first-massive-spanish-speaking-blockchain-event-created-by-decentraland-and-cryptovoxels) Decentraland and Cryptovoxels.

## Media

Selected articles:

- Decred makes consensus change to further decentralize $128M treasury ([banklesstimes.com](https://www.banklesstimes.com/2021/04/12/decred-makes-consensus-change-to-further-decentralize-128m-treasury/))
- What is Decred and DCR? by Ivan on Tech ([ivanontech.com](https://academy.ivanontech.com/blog/what-is-decred-and-dcr))
- Q1'21 currency sector review by Mira Christanto ([messari.io](https://messari.io/article/q1-21-currency-sector-review)) - Messari [tweeted](https://twitter.com/MessariCrypto/status/1381654632515174402) that DCR is second biggest mover after DOGE in Q1 2021

Videos:

- Luke Powell interview Decred in Depth (live) by @elima\_iii ([youtube](https://www.youtube.com/watch?v=J6IAjmwkki0))
- Decred Society interview Decred in Depth (live) @elima\_iii ([youtube](https://www.youtube.com/watch?v=WOVUvzsp3Eo))
- Decred's proposal platform Politeia: The decision-making force behind the ~$125M Decred DAO by @Exitus ([youtube](https://www.youtube.com/watch?v=dfpUgwXBUmM))
- The evolution of money - Decred fundamentals by @phoenixgreen ([youtube](https://www.youtube.com/watch?v=1qadfuFuqzs))
- Interoperability for digital cash by @phoenixgreen ([youtube](https://www.youtube.com/watch?v=iBN0ZzlEKMA))
- Decred Price Analysis - 27th April 2021 by Josh Olszewicz of Brave New Coin ([youtube](https://www.youtube.com/watch?v=NfSp5IjPtAI))

@karamble has mirrored all Decred YouTube [channel](https://www.youtube.com/decredchannel) videos at [tube.decredcommunity.org](https://tube.decredcommunity.org/). It is powered by [PeerTube](https://joinpeertube.org/) - an open-source, self-hosted, lightweight alternative to YouTube that can connect to the [Fediverse](https://en.wikipedia.org/wiki/Fediverse). [Here](https://docs.joinpeertube.org/use-third-party-application) is a list of tools for regular users. Admins running PeerTube instances can help to make the content even more resilient by setting up [following and redundancy](https://docs.joinpeertube.org/admin-following-instances).

Audio:

- Rough Consensus 18: Bull market blues - Checkmate, Permabull Nino & Mister Black ([libsyn](https://roughconsensus.libsyn.com/episode-18-bull-market-blues), [spotify](https://open.spotify.com/episode/0E7k86gme05YINpdBlVPqy))
- Keyword: Crypto Podcast - Luke P. from Decred ([youtube](https://www.youtube.com/watch?v=pRJ1zJFVoFo), [keywordcrypto.com](https://www.keywordcrypto.com/luke-p-from-decred/))

Translations:

- Decred Blockchain Analysis - Part 2 PoW wow - [in Spanish](https://medium.com/decred-es/an%C3%A1lisis-de-la-blockchain-de-decred-pt-2-pow-wow-376aab0be23c) by @francov\_
- Decred Journal March 2021 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), and Spanish (@francov\_). Thank you all!

Other non-English content:

- @Dominic talked to Mable Jiang on 51% Podcast episode 20 titled "On Decred's Hybrid Consensus and Collective Wisdom", hosted by Multicoin Capital ([apple](https://podcasts.apple.com/cn/podcast/51-with-mable-jiang-presented-by-multicoin-capital/id1540917284?l=en&i=1000515571194), [simplecast.com](https://51-with-mable-jiang-presented-by-multicoin-capital.simplecast.com/episodes/ep20-cn-dt-decred))

## Community Discussions

Comm systems news:

- a new flavor of scammers are DMing people as they join #support. Please be warned, no admins or devs will ever DM you, or ask you for money!

Selected Reddit posts:

- [r/decred](https://www.reddit.com/r/decred/new/) now has weekly Trader Talk Thursdays and Many Musings Mondays to host content that would otherwise be removed as duplicate price talks or off-topic
- a marketing idea to run Decred-funded [mail service](https://www.reddit.com/r/decred/comments/n11zwu/decredmail_a_marketing_idea/)

Selected Twitter discussions:

- @lukebp clears up what a [DAO](https://twitter.com/lukebp_/status/1378381506947784706) is
- @overthrowy shared his Decred [investment deck](https://twitter.com/overthrowy/status/1381097293122740225)

> For people who believe that "the market" makes the best decisions, Bitcoin may be the right choice. During any contentious change, the network may split into two or more forks that will compete (fight) for the financial and social support of PoW miners, developers, investors, and exchanges.
> 
> For people who believe in collaboration, who aspire to pursue the common good, and who are willing to align themselves behind the general will of the decentralized voter collective, Decred may be the right choice.
> 
> Bitcoin and Decred are different social contracts. _They can coexist._ ([@overthrowy](https://twitter.com/overthrowy/status/1381104927108296707))

## Markets

In April DCR was trading between USD 169.50-243.70 / BTC 0.0031-0.0040. The average daily rate was $198.60.

## Relevant External

The Fei "stablecoin" was [launched](https://www.coindesk.com/1b-fei-stablecoins-rocky-start-is-a-wake-up-call-for-defi-investors) in early April but defied expectations by trading at significantly lower than the target of $1. This left many investors in a position where they were unable to exit their FEI position without taking heavy losses, due to the complex and unpredictable behavior of the novel incentive and burn mechanisms. FEI did eventually [attain](https://www.coindesk.com/1b-stablecoin-fei-hits-price-target-for-first-time-a-month-after-launch) its $1 target after about 1 month after launch.

The Yearn Finance community have been discussing [YIP-61](https://gov.yearn.finance/t/yip-61-governance-2-0/10460/25) "Governance 2.0", which extends the multisig arrangement put in place temporarily by YIP-41, and [approving](https://snapshot.org/#/ybaby.eth/proposal/QmSMyYeKrRpnA7Xn56o2NtbCUzxmhzCupL7LxMA1reXxq4) it with 99.97% yes votes. This proposal also delegates certain powers to a set of Yearn contributor teams ("yTeams"), and "clarifies" the role of YFI holders as being primarily about delegating powers to these teams and approving YIPs.

The NFT sub-community is crowdfunding its own new media platform ([NFTs WTF](https://nfts.wtf)), via the mechanism of selling 100 NFTs that confer voting rights in a DAO that will support the platform. It is interesting to note that the [post](https://nfts.wtf/crowdfunding-the-worlds-first-d-zine/) announcing the first phase of the crowdsale, in which 51 of the 100 controlling tokens were sold, only 3 were sold to Venture Capitalists, and only as individuals and not representatives of their organizations.

Coinbase started [selling](https://uk.finance.yahoo.com/news/coinbase-direct-listing-stock-cryptocurrency-bitcoin-172655492.html) shares on the Nasdaq, unlike an IPO this did not involve creating new shares but instead the existing shareholders bringing some of theirs to market.

That's all for April. Submit your stories [here](https://github.com/xaur/decred-news/labels/next%20release) or simply share your [feedback](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback). We're always looking for [contributors](https://github.com/xaur/decred-news/blob/docs/contributing.md) to improve DJ!

## About

This is issue 37 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from source after a minimal sanity check. The authors of the Decred Journal have no ability to verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing and editing: bee, degeri, l1ndseymm, richardred
- reviews and feedback: chappjc, davecgh, jholdstock, lukebp
- title image: saender
- funding: Decred stakeholders
