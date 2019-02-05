# Decred月报 - 12月 

## 开发进展总结
{per-project summary, drop items without updates}

[dcrd](https://github.com/decred/dcrd):

An issue was discovered during the testing of RC1: the change to reverse UTXO set semantics accidently corrected wrong behavior in consensus rules. Old incorrect behavior was [preserved](https://github.com/decred/dcrd/pull/1570) until a consensus vote can take place to fix it. {comment on impact} The code for the consensus vote is [completed](https://github.com/decred/dcrd/pull/1579) and will be included in the final v1.4 release. The fix and vote was prioritized because it is necessary for Lightning Network.

[dcrwallet](https://github.com/decred/dcrwallet): {}

[Decrediton](https://github.com/decred/decrediton):

* Work ongoing to allow user to specify config options as command line arguments https://github.com/decred/decrediton/pull/1975

[Politeia](https://github.com/decred/politeia):

* cache layer entered review https://github.com/decred/politeia/pull/660
* thanks to lemonkabir for discovering a couple of [security](https://github.com/decred/politeia/issues/647) [issues](https://github.com/decred/politeia/issues/650)
* onboarding modal was replaced with relevant links to dcrdocs https://github.com/decred/politeiagui/pull/986

* missing feature to allow admin to censor public proposal was identified and discussed, there must be a way to remove a public proposal that was edited to include content that wouldn't pass initial moderation https://github.com/decred/politeia/issues/662 {Dev or Gov?}, implementation started https://github.com/decred/politeiagui/issues/991
* multiple choice voting discussion https://github.com/decred/politeia/issues/664 {Dev or Gov?}
* Developers are discussing [automated e2e testing](https://github.com/decred/politeiagui/issues/976) and [QA checklist](https://github.com/decred/politeiagui/issues/977) for major changes.
* Large code refactoring discussion [started](https://github.com/decred/politeiagui/issues/990) to address complexity, performance and dev productivity issues. First proposed [solution](https://github.com/decred/politeiagui/issues/990#issuecomment-454535696) is to use GraphQL.

[dcrandroid](https://github.com/decred/dcrandroid): 3rd release candidate was published on Google Play Store for [mainnet](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.mainnet) and [testnet](https://play.google.com/store/apps/details?id=com.decred.dcrandroid.testnet). Test coins can be requested in the [faucet](http://faucet.decred.org/). Bug reports are welcome [on GitHub](http://github.com/decred/dcrandroid/issues).

https://www.reddit.com/r/decred/comments/am7j40/decred_wallet_for_android_v10_released/

[dcrios](https://github.com/raedahgroup/dcrios): {}

Trezor: {}

[dcrdata](https://github.com/decred/dcrdata):

* @buck54321 is exterminating imperative jQuery code https://github.com/decred/dcrdata/pull/915
* HTTPS is now [enforced](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$154818146313660CWvZy:decred.org) on explorer.dcrdata.org and mainnet.dcrdata.org
* Team is preparing for stress testing of Insight API _(they call it torture testing, ouch)_.

WIP:

* Exchange rate monitoring to enable features that depend on it: https://github.com/decred/dcrdata/pull/951

Ticket splitting:

* You can monitor active sessions on this page https://mainnet-split-tickets.matheusd.com/

[docs](https://github.com/decred/dcrdocs):

* Guide for [Operating a VSP](https://docs.decred.org/advanced/operating-a-vsp/)
* [Solo PoS Voting](https://docs.decred.org/advanced/solo-proof-of-stake-voting/) guide by @jz was polished and added to the docs.
* new [Address Details](https://docs.decred.org/advanced/address-details/) page explains address format an lists all possible kinds of addresses
* deep dive security discussion in #documentation, it will be beneficial to the whole space to assemble thorough OPSEC guidelines https://github.com/xaur/decred-issues/issues/101

[decred.org](https://github.com/decred/dcrweb):

* huge effort is [ongoing](https://github.com/decred/dcrweb/pull/491) by @peter\_zen to migrate the site to Hugo (static site generator written in Go) is complete. This makes updating site content much easier. {comment from @peter\_zen or other devs why it's cool} {is it deployed at decred.org?}
* speed optimizations {right?} https://github.com/decred/dcrweb/pull/513
* {comment on SRI: what is it, what was before, what is now, why it's cool}

Other:

* Google BigQuery dataset submitted by u/cmorq https://www.reddit.com/r/decred/comments/agpkjv/sql_interface_to_live_onchain_decred_data/
* More terminology changes in dcrwallet, dcrdocs and dcrweb
* {comment on contractor-mgmt sndurkin? is it worth mentioning it yet?}
* projects are gradually switching to a faster golangci-lint linter
* github now allows private repos on free accounts https://github.blog/2019-01-07-new-year-new-github/


1月开发活动数据: 分布于{}个存储库（repositories) 有 {} 有效PRs, {} 主要提交, {} 行添加 及 {} 行删除。每个存储库中有来自{}个开发者的贡献。

## 人员

{welcome contributors whose work was merged to master branches for the first time}

{welcome new individual and company contractors listed on decred.org, updates from existing}

congrats! https://github.com/decred/dcrweb/pull/486

4 inactive developers [removed](https://github.com/decred/dcrweb/issues/528) from decred.org

{interviews about people}

Independent Decred contractors [published](https://medium.com/decred/decred-independent-contractor-roadmap-884faba3db39) their plans for 2019 which faced mixed feedback [in #marketing](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15476119656176jVTYW:decred.org).

## 治理

{high level recap of decision-making activity, most important events, defer to Politeia Digest for the rest}

Decred Bug Bounty program [launched](https://twitter.com/decredproject/status/1087486930093264897), congrats @degeri! Check the rules and guidelines on the new website [bounty.decred.org](https://bounty.decred.org/). Website is built with Hugo and the code is [on GitHub](https://github.com/decred/dcrbounty) so feel free to contribute. {anyone else to credit?}

Intro blog post https://medium.com/decred/decred-launches-debug-decred-bug-bounty-program-7e4d2af27ec9

@oregonisaac {@isaac?} is [looking](https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15474111512672Whvns:decred.org) for Java developers to evaluate requirements for ATM integration. Draft of the RPF document was posted and discussed here https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$154828004015153jWdiD:decred.org , there is some concensus to use 2-phase voting: first vote to see if stakeholders want ATMs at all, and second to chose a specific implementation. Another good point discussed was whether to wait for mobile apps releases before proceeding with the ATMs.

@Dustorf is drafting proposals for [marketing budget]( https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154897255124536mFHoo:decred.org) and [events budget](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154896889724431Mxlvj:decred.org) to improve transparency and engage stakeholders.

Discussions:

* attack vector: offer to airdrop some token to stakeholders in return for funding a proposal https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15468733339790vCEoH:decred.org
* reflecting on engagement in Politeia https://matrix.to/#/!MIGqWXfLFBwhipPKYL:decred.org/$15481365491827928DiBLm:matrix.org
* governance UX to pre-emptively address bad proposals https://github.com/decred/politeia/issues/678

## 网络

算力: 1月算力以{}Ph/s开始，以{}Ph/s结束，本月中最高{}Ph/s及最低{}Ph/s，而大部分时间平均于{}Ph/s左右。在{}根据[dcrstats.com](https://dcrstats.com/pow)数据显示，矿池算力分布为：{}矿池分布数据为大约值无法精确计算。 

投票: 按dcrstats.com（数据显示）, 30日 平均票价为 {} DCR。价格在{} DCR 至 {} DCR之间浮动。锁仓数额为{} 百万 DCR, 大约为总流通量的 {}%。

节点: 截止于{}月{}日，[dcred.eu](https://dcred.eu/nodeStats)显示 共有 {} public listening Node 及 {} Normal Node。版本分布: {}

## 挖矿

https://www.reddit.com/r/decred/comments/ae8hy8/class_action_lawsuit_officially_filed_against/

## 整合

{new items of infrastructure or updates from existing}

New VSP: [dcr.grassfed.network](https://dcr.grassfed.network) [added](https://github.com/decred/dcrwebapi/pull/53).

Exchange integrations:

* https://twitter.com/bitturkcom/status/1082201314912862209
  * wait until this is resolved
* Brazilian exchange BitJa [announced](https://twitter.com/bitjabr/status/1090066185302036480) DCR/BRL fiat pair.

{OTC desks}

{payment processors}

{wallets}

Ellipal wallet [announced](https://twitter.com/ellipalwallet/status/1089850526202613760) Decred support in latest firmware release. {keep? anybody used it?}

Exodus wallet [integrated](https://twitter.com/exodus_io/status/1090263399122923520) USDC, a USD-pegged token by Circle.

## Adoption

New merchants:

* {}

{applications of Decred blockchain and related projects: Politeia, atomicswap}

{investment adoption}

BlueYard (one of Decred investors) [announced](https://medium.com/@BlueYard/blueyard-2-3d0bbaf1f1b6) they have raised their second fund and explained what "contrarian" projects they invest in.
 
## 外联活动

{overview of outreach/communications/marketing activity for past month and any short-term plans}

Ditto's Bi-Weekly Update https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154688457110052CiWYd:decred.org , one thing they learned that week was:

> The community welcomes and encourages questions, even if the person asking fears that their questions are "stupid." We've observed a spirit of collaboration and willingness to help that we haven't seen in other communities. It's refreshing!

Ditto has set up a system to catch every piece of media written about Decred and to address inaccuracies in real time. As a test case for that workflow one horrible article was scrutinized by the community and Ditto collected the feedback for that and future cases. Another issue discussed was integrating Ditto's workflow with voluntary submissions from the community. https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15468814029997AWtQJ:decred.org

Ditto shared a second version of the Foundational Messaging document https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154706728112462ubmNo:decred.org
https://docs.google.com/document/d/19r9SjOWin4Fb9E2_90S7mdsG0BNxRBSYzsJjSYK2Jjw/edit

[Final version](https://pastebin.com/E5L6u2RV) of the document was [shared](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154880432321730DYSYl:decred.org) at the end of Jan.

Tagline for Decred was extensively discussed [in #marketing](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154711632712869dqRko:decred.org) and [on Reddit](https://www.reddit.com/r/decred/comments/afctai/tagline_to_capture_the_decred_project/).

On Jan 11 Ditto [reported](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$1547232200845NiZnO:decred.org) about the Forbes article and advised individuals to share it because amplification is just as important as the media placement itself.

Example of "thought leadership" placement can be seen the [comment here](https://cryptobriefing.com/scaling-delay-ethereum-constantinople/) by @richardred. {keep? reword?} In the following [discussion](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15476630757260cGbJc:decred.org) of it an issue was raised that Decred and Ethereum have very different backgrounds and this must be taken into account.

Ditto's Bi-Weekly Update https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15478384869864RTCsv:decred.org

Custom Decred merch on the Decredible shop https://www.reddit.com/r/decred/comments/ae07as/custom_decred_merch_with_19_discount_in_the/

Important notice: new batch of Stakey plushies is available! https://www.reddit.com/r/decred/comments/ahalex/new_batch_of_stakey_plushies_available/

@Matt D started [Decred Aggregator](https://t.me/DecredAgg) in Telegram that aims to collect news, press, videos, podcasts, Decred announcements, trending tweets and Reddit posts, as well as market stats. Introduction and motivation was shared in [this chat]( https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154825336714293nfWdU:decred.org).

## 社区活动

Attended:

* {}

Upcoming:

* {}

{announcements from events people}

Open source and hacker oriented events like DEFCON, CCC and FOSDEM were discussed https://github.com/xaur/decred-issues/issues/83

@Matt D [suggested](https://matrix.to/#/!aNPTuiryMFmdMQWUzb:decred.org/$154914199426705SWAOr:decred.org) event calendar workflow using Trello.

## 媒体链接

[blog.dcrclub.org](https://blog.dcrclub.org/) is a new website in Chinese that collects various articles and translations in one place. The source hosted [on GitHub](https://github.com/0x5826/blog.dcrclub.org) makes it easy to contribute or mirror the website on other domain for more resiliency. Credits to @TogT4V (Telegram) for starting the site.

@butterfly published some articles about Decred in [Arabic blog](https://decred-arabia.blogspot.com/2019/01/blog-post.html).

@michae2xl [started](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$1548814257223928fVjiP:matrix.org) Portuguese podcasts that are available on [Soundcloud](https://soundcloud.com/user-770106247/), Spotify, Apple Podcasts and Google Podcasts - search "Decred Brasil".

[Decred page](https://en.wikipedia.org/wiki/Decred) on Wikipedia is under attack again. On Jan 8 user R2d232h2 [removed](https://en.wikipedia.org/w/index.php?title=Decred&diff=prev&oldid=877407037) a bunch of "bad sources". On Jan 10 the same user [vandalized](https://en.wikipedia.org/w/index.php?title=Decred&diff=next&oldid=877407037) the page by removing a large and important part of content. Just 4 hours later another user nominated Decred page for deletion - the [3rd attempt](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%283rd_nomination%29) to take it down. On Jan 11 the second purge was reverted and R2d232h2 was banned as sockpuppet, but next day the removal was applied again. As it stands after the cutting, the page is very small and has all [votes](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%283rd_nomination%29) to delete it. All suggested recent articles in major crypto media are [not good enough](https://en.wikipedia.org/wiki/Talk:Decred#Request_edit_on_12_January_2019) references. For background, the author of [2nd nomination](https://en.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Decred_%282nd_nomination%29) for deletion had interesting [views](https://archive.today/QAlRp) on notability of articles and was [banned](https://en.wikipedia.org/wiki/User:Prince_of_Thieves) as a sockpuppet. Extensively discussed [in #marketing](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$1547202592212vKSyw:decred.org) ([continued](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15472392171087ucpIb:decred.org)), including possilble solutions. On Jan 18 the page was deleted and removed from List of cryptocurrencies that contains more notable entries. More details are captured in [this issue](https://github.com/xaur/decred-issues/issues/79).

The good news, is it [can mean](https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$15474897963391hhDDU:decred.org) Decred is moving in the right direction.

{community efforts: Decred Assembly, websites, etc}

{ratings news}

Articles:

* Understanding Decred Governance ([in Chinese](https://mp.weixin.qq.com/s/z3hzILiPBsLJR72Q2tP7TQ) at qq.com, [Google translation](https://translate.google.com/translate?sl=auto&tl=en&hl=en&u=https%3A%2F%2Fmp.weixin.qq.com%2Fs%2Fz3hzILiPBsLJR72Q2tP7TQ), _missed in Dec issue_) by "Dr Bitcoin"
* https://www.coindesk.com/how-to-last-the-crypto-winter-seek-simplicity-manage-complexity (notably, the tagline was collectively brainstormed in #marketing)
* https://bithub.pl/wywiady/decred-wywiad-z-community-managerem/ {en title please}
* https://cryptoinsider.com/decred-dcr-prioritizes-blockchain-based-governance-and-decentralized-decision-making/ {worthy?}
* https://www.linkedin.com/pulse/funadamental-analysis-decred-dcr-piotr-arendarski-ph-d {worthy?}
* https://www.coinbureau.com/analysis/best-decred-wallets/
* https://www.forbes.com/sites/leslieankney/2019/01/11/who-should-hold-power-decred-governance-and-what-it-means-for-investors/
* https://medium.com/decred/decred-independent-contractor-roadmap-884faba3db39
* https://mp.weixin.qq.com/s/_-lY0rtWSPiyLPZeTRR7gg (Chinese, {good?} by yinguochao})
* Blockchain Project Review: Decred:8.4 Autonomous Digital Currency by Evaluape ([medium](https://medium.com/@EVALUAPE1/blockchain-project-review-decred-8-4-autonomous-digital-currency-323771d65529)) - Decred rated 8.4
* Decred coin review: Replacing BTC? (Dutch, [bitcoinsaltcoins.nl](https://www.bitcoinsaltcoins.nl/decred-coin-review-vervanger-van-btc/)) - Decred scored 8.8.
* https://bitsonline.com/consensus-mechanism-of-decred-decentralization/
* 3 Cryptocurrencies to HODL During This Crypto Winter (Opinion) by Daniel Frumkin ([investinblockchain.com](https://www.investinblockchain.com/cryptocurrencies-hodl-during-crypto-winter/))
* https://seekingalpha.com/article/4235521-fundamental-value-crypto-bitcoin-decred-store-value-investments
* Binance info listed a new rating report([EN](https://info.binance.com/en/rate/detail/2506),[CN](https://info.binance.com/cn/rate/detail/2493)) of Decred by [Evaluape](https://www.evaluape.io/project/browse/54155/report)
* The role of Decred voters in defending against majority attacks by @richardred ([medium](https://medium.com/@richardred/the-role-of-decred-voters-in-defending-against-majority-attacks-ec658af0a8fd))
* https://blog.goodaudience.com/decentralized-off-chain-governance-in-the-context-of-digital-currencies-ef6db7d97412
* https://medium.com/@artikozel/decred-infrastructure-interviews-stephen-founder-of-crypto-only-luxury-goods-marketplace-68d3214a4fd7
* https://weeklyglobalresearch.wordpress.com/2019/01/31/decred-dcr-review/

Above are most interesting articles, but more were published on the web. The [decred-media-tracker](https://github.com/RichardRed0x/decred-media-tracker) project is intended to track all articles.

Translations:

* [Detailed analysis of Decred fork resistance](https://medium.com/decred/detailed-analysis-of-decred-fork-resistance-93022e0bcde7) by @Haon - [in Russian](https://medium.com/decred-russia/%D0%B4%D0%B5%D1%82%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7-%D1%83%D1%81%D1%82%D0%BE%D0%B9%D1%87%D0%B8%D0%B2%D0%BE%D1%81%D1%82%D0%B8-decred-%D0%BA-%D1%84%D0%BE%D1%80%D0%BA%D1%83-b30c78f764ea) by @DZ

Videos:

* Why 2019 will be the biggest year for Decred by Hack Crypto - interview with @joshuam from TNABC https://www.youtube.com/watch?v=Kyihc6Uh4XA
* Decred Realized Disputes in Blockchain Projects Were Inevitable: Joshua Buirski by Bitsonline from TNABC ([youtube](https://www.youtube.com/watch?v=CUxDxJ4YAUA), [bitsonline.com](https://bitsonline.com/decred-disputes-inevitable-buirski/))
* Governance: Blockchain's Most Overlooked Pillar talk by @oregonisaac from Token Forum 2 conference ([tfblock.io](https://www.tfblock.io/post/governance-blockchain-s-most-overlooked-pillar))

Audio:

* https://badcryptopodcast.com/2019/01/08/autonomous-crypto-decred/
* 51percent Crypto Research podcast: Noah Pierau and Tom Shaughnessy talk about blockchain governance in Decred, Bitcoin, Dash and Ethereum ([itunes](https://itunes.apple.com/us/podcast/noah-pierau-on-blockchain-governance-decred-bitcoin/id1438148082?i=1000428113722&mt=2))
* How Decred Revolutionizes Funding in Crypto with Marco Peereboom ([evolvement.io](https://evolvement.io/how-decred-revolutionizes-funding-in-crypto-with-marco-peereboom/), with mirrors on soundcloud, youtube and more) - Michael Nye and Marco discuss current state of crypto, how Decred began, PoW vs PoS, Decred's funding model and more.



## 社区讨论

Community stats:

* Twitter followers: {} (+{})
* Reddit subscribers: {} (+{})
* Matrix users: {} (+{})
* Slack users: {} (+{})
* Telegram users: {} (+{})
* YouTube subscribers: {} (+{})
* Facebook followers: {} (+{}), likes: {} (+{})
* LinkedIn followers: Decred page {} (+{}), Politeia page {} (+{})
* GitHub dcrd stars: {} (+{}), forks: {} (+{})

Comm systems news:

* @sambiohazard wrote an excellent plan to address Discord spam, implemented it, reported on first few weeks. With this in place we can finally appreciate Discord as an opportunity to onboard more people. Thank you!
* https://github.com/xaur/decred-issues/issues/16
* landing page for new matrix users https://github.com/decred/dcrweb/pull/462

More [criticism](https://twitter.com/tonevays/status/1086702239853379584) from Bitcoin maximalists triggered a [discussion](https://www.reddit.com/r/decred/comments/ahuawl/decred_launch_security_laws/) on how Decred looks in context of securities laws. One vector critics use is that Decred's premine and airdrop was not fair and "hand selected". This is a misrepresentation of the (huge) manual effort to filter out airdrop cheaters, per [this discussion]( https://matrix.to/#/!OfChXgczrIlpEZSFAv:decred.org/$154810656412322VrQLg:decred.org) that also has many useful links describing Decred's launch. One interesting insight shared there is that ~300k (35%) airdropped coins never moved. Another related [chat](https://matrix.to/#/!kdpEDksmOMNrlMqffD:decred.org/$15467943549316LjeYZ:decred.org) was about Twitter attacks claiming how Decred's initial distribution was not transparent or fair, while avoiding inconvenient facts about Bitcoin's early mining. Finally, this [history lesson](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$15467944729319gvTvt:decred.org) explained early days of staking and made a point that original devs had no unilateral control of consensus rules from day 1.

* {other convos}

{selected discussed topics, as bullet list or one paragraph per topic}

Reddit: {interesting threads}

Twitter: {interesting threads}

{link to chat index}

## 市场

{markets overview: USD and BTC prices, highs and lows, interesting events, interesting analysis}

ICO projects withdrew ~441k ETH from treasuries, which can impact the whole market https://www.circle.com/en/research/recap-dec28-jan3



## 相关外部信息


{PoW, ASIC resistance, tech}

Ethereum Classic (ETC) was subject to a 51% attack, with the alert being raised by [CoinNess](https://www.coinness.com/news/198264) on Jan 7.  Coinbase then [announced](https://blog.coinbase.com/ethereum-classic-etc-is-currently-being-51-attacked-33be13ce32de) that it had detected a deep reorganization of the ETC chain and had halted ETC transactions. The article lists a number of reorgs that involved double spends, putting the total amount involved at $1.1 million, across 15 distinct reorg events. Coinbase was not itself a target for these attacks. The Gate.io exchange subsequently [announced](https://www.gate.io/article/16735) that it had been targeted and had lost around $200k, and that it would absorb the loss. Gate.io also significantly increased the number of confirmations required for ETC deposits. In an unusual development, the attacker then [returned](https://www.gate.io/article/16740) $100k of the ETC to gate.io, they have tried but failed to make contact with the attacker and do not know the reason for the return of funds. Other victims of the ETC double spends have not come forward. 

Ethereum's developers [decided](https://www.coindesk.com/ethereum-developers-give-tentative-greenlight-to-asic-blocking-code) (tentatively)  on Jan 4 to go ahead with a change of mining algorithm from Ethash to ProgPoW. This move is intended to stop ASICs from mining Ethereum.

Ethereum developers also [delayed](https://breakermag.com/what-we-know-about-the-vulnerability-behind-ethereums-rollback-of-constantinople/) the Constantinople hard fork on Jan 15 after a security vulnerability which would have enabled a "reentrancy attack" was [detected](https://medium.com/chainsecurity/constantinople-enables-new-reentrancy-attack-ace4088297d9). 

Fundamentals of Proof of Work [article](https://blog.sia.tech/fundamentals-of-proof-of-work-beaa68093d2b) by David Vorick makes the case for exclusive hardware cryptocurrencies and contrasts them with shared hardware cryptocurrencies that suffer from multiple issues, especially ASIC-resistant ones. One of the issues with non specialized hardware is hashrate marketplaces. They allow hardware owners to better profit from their hardware by not caring about which coin they mine, even if the hashrate is rented to attackers. Decred benefits from specialized hardware but is not "exclusive" to it, other coins exist or may appear in future that use the same mining algorithm. What protects Decred is the (current) hashrate dominance for its algorithm and the ability to strip mining rewards from the blocks.

The first round of Aragon proposal voting [concluded](https://blog.aragon.org/final-results-from-aragon-network-vote-1/) on Jan 26. Of the 12 submitted proposals, 3 were excluded from the vote by the Aragon Foundation (1 because of lack of full time leadership and engineering talent, 2 were excluded to reduce cognitive load on voters). 8 of the 9 proposals voted on were [approved](https://mainnet.aragon.org/#/governance.aragonproject.eth/0x277bfcf7c2e162cb1ac3e9ae228a3132a75f83d4) by ANT holders, with one proposal (to change the voting period duration from 48 hours to 1 week) rejected. ANT participation rates [ranged](https://mainnet.aragon.org/#/governance.aragonproject.eth/0x277bfcf7c2e162cb1ac3e9ae228a3132a75f83d4) from 2.3 to 7.8%. The most expensive [proposal](https://github.com/aragon/flock/blob/master/teams/Aragon%20One/2019.md) to be approved will pay Aragon One $4 million for 2019 operating costs plus an incentive package consisting of 1.675 million ANT on a 5 year vesting schedule. An incentive in ANT with a vesting schedule was included as part of most proposals, in addition to the main cost to be paid in DAI. In total this round of approved proposals will cost around $5.94 million + 2.52 million ANT (~$880k).

The EOS referendum system for constitutional amendments went [live](https://medium.com/@eosnationbp/the-fate-of-eos-is-in-the-hands-of-token-holders-3d345147ef6) on Jan 11. So far 77 proposals have been [submitted](https://bloks.io/vote/referendums). The voting period for these proposals is flexible and specified by the submitter, some last as long as four months. The proposals with the most votes (as of Jan 31) have votes from around 2% of circulating EOS, but most proposals have very low participation (only 10 have greater than 0.5% participation). So far the most popular proposals are to [change](https://bloks.io/vote/referendums/rex4all) where the fees for short names and RAM purchases go, [delete](https://bloks.io/vote/referendums/decaf) the EOS Core Arbitration Forum, and [burn](https://bloks.io/vote/referendums/burnsaving) the inflation funds in eosio.saving (to be used for funding the worker proposal system).

The NEM Foundation [announced](https://forum.nem.io/t/nem-foundation-message-to-the-community/21753) that it is in financial difficulty and needs to downsize its workforce. A new council took over the foundation on January 1 and when they opened the books they saw a problem. The previous council had a burn rate of 9 million XEM per month ($360k now, considerably more at the time) which was spent by independent regional entities on promotional activities with little accountability. This was deemed not sustainable, and the new council has restructured the foundation and is presently seeking additional funds.

{governance, forks, chain splits, controversy}

Updated version of the "forkonomy" research by Wassim Alsindi (@parallelind) was [published](https://hackernoon.com/towards-an-analytical-discipline-of-forkonomy-summer-2018-e6da993ee3f9) along with an up-to-date [follow-up](https://medium.com/@parallelind/forkonomy-revisited-where-are-they-now-73fbfbec6b4d).

Hcash forked a few [more](https://archive.today/rEhWX) Decred projects: [Autonomy](https://archive.today/KTCdX) (Politeia), [hcexplorer](https://archive.today/2KTtW) and [hctime](https://archive.today/K151A). In Politeia, they accidently [removed](https://archive.today/ECplt) copyright of Decred developers and forgot to rename the project. After being notified they quickly reacted by removing multiple repositories from TKFORKED account,  [reinstating](https://github.com/TKFORKED/autonomy/commit/4b05c2c31829df64be69e546d939a563247e1927) the license and [renaming](https://github.com/TKFORKED/autonomy/commit/98d5f63f676e45e6a91eba99da3db985effdb1f2) the Politeia fork to Autonomy. A few [missed](https://twitter.com/michae2xl/status/1084270468234915840) subtle Decred icons were fixed. Some [projects](https://archive.today/https://github.com/HcashOrg/hc*) were forked with their commit history erased and without marking them as forks on GitHub. Complaints on their subreddit were silently censored without reply ([1](https://www.reddit.com/r/hcash/comments/adwmx2/hcash_being_shady_again/), [2](https://www.reddit.com/r/hcash/comments/afepsc/hcash_cant_be_bothered_to_change_the_decred_logo/). Discussed [here](https://matrix.to/#/!MgQoetFiyjrHAywokv:decred.org/$154696507010921TRgid:decred.org).

Grin [struggles](https://www.grin-forum.org/t/solved-early-disappointments/3682) to get funding.

Another [sad example](https://twitter.com/BrianDColwell/status/1090286752831434752) of what can happen when the team runs out of money.

{DEX}

{related exchanges and websites}

[Staked](https://staked.us/about/), a startup that provides staking services for institutional investors, raised $4.5M from Pantera, Coinbase, DCG and others. Covered by [CoinDesk](https://www.coindesk.com/pantera-coinbase-join-4-5-million-round-in-staking-as-a-service-startup), [The Block](https://www.theblockcrypto.com/2019/01/31/winklevoss-twins-pantera-get-behind-a-new-business-thats-capitalizing-on-a-new-trend-sweeping-crypto-hedge-funds/) and [Bloomberg](https://www.bloomberg.com/news/articles/2019-02-01/some-crypto-investors-are-playing-it-safe-after-volatile-run). Staked operates a [VSP](https://decred.staked.us/) that launched in Nov 2018.

Coinbase [banned](https://cryptocoinspy.com/coinbase-bans-gab-again/). Good reminder of the old but still very relevant mantra: "not your keys not your coins". This is [not the first](https://www.cnbc.com/2018/04/23/coinbase-suspends-wikileaks-bitcoin-account.html) big case of account suspension.

Medium censored an article 'How to use Bitcoin anonymously' https://bitcoinist.com/how-to-use-bitcoin-anonymously-ban-medium/

{other: regulations, security, fun}

Hacked addresses. {impact?}

* https://eprint.iacr.org/2019/023
* https://cryptoslate.com/researchers-discover-vulnerability-bitcoin-ethereum-ripple-digital-signatures/
* {ask devs to comment, e.g. how bad can it be if user has a poor source of random on his device}
* some speculate Copay is involved https://www.reddit.com/r/Bitcoin/comments/aectx5/nadiaheninger_and_joachim_breitner_discoverer/edpedar/

Largest data breach in history contains a collection of thousands of hacked databases https://www.troyhunt.com/the-773-million-record-collection-1-data-reach/ . Choose wisely who you share data with.

Bank for International Settlements released a very optimistic [study](https://www.bis.org/publ/work765.htm) of cryptocurrencies.

Cryptopia was [hacked](https://www.investinblockchain.com/cryptopia-hack-estimated-16-million-lost/) with loss estimates varying between $3-16 million. Binance [froze](https://www.investinblockchain.com/binance-freezes-funds-cryptopia-hack/) some funds coming from the hack.

https://www.zdnet.com/article/new-ransomware-strain-is-locking-up-bitcoin-mining-rigs-in-china/

Resource exhaustion vulnerability was [discovered](https://medium.com/@dsl_uiuc/fake-stake-attacks-on-chain-based-proof-of-stake-cryptocurrencies-b8b05723f806) 26+ currencies based on PoSv3, majority of them deployed mitigations. Part of the root cause is that in many such systems the Proof of Stake layer was "grafted in" Bitcoin Core codebase insecurely. Decred is [not affected](https://twitter.com/Sanket1729/status/1087829688347701254).

## 关于月报
1月为英文第10期[GitHub](https://xaur.github.io/decred-news/journal/201901)月报。 点击[这里](https://xaur.github.io/decred-news/)浏览往期月报。

大部分来自第三方的信息在基本检查无误后转发。Decred Journal 及月报作者无法验证所有信息。请注意骗局并进行自己的研究。

欢迎在 Reddit, [GitHub](https://github.com/xaur/decred-news/issues)和[Matrix](https://matrix.to/#/!lbzTjhzNbIaDbuAxkS:decred.org) 上评论，反馈及贡献。

感谢 (按字母排序): 

## 中文社区 

* [微博](https://www.weibo.com/DecredProject)
* 微信群
* [中文电报群](https://t.me/decred_cn)
* QQ群号-258412796

欢迎同时关注[英文月报](https://github.com/xaur/decred-news)了解更多最新消息

中文月报相关意见欢迎提交到[Github](https://github.com/Guang168/DecredCNJournal/issues)

感谢 (按字母排序): 