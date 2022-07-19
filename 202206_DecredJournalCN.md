# Decred月报 – 2022 年 5 月

Highlights for June:

- The Ethereum smart contract used in DCRDEX passed its first audit with great results.
- Politeia was busy with 3 proposals approved, 1 rejected and 3 new proposals submitted.
- First treasury spend transaction approved under the corrected spend policy (DCP-7).
- DCR listed on 2 exchanges, Guardarian and BitPanda.

Contents:

- [Development](#development)
- [People](#people)
- [Governance](#governance)
- [Network](#network)
- [Ecosystem](#ecosystem)
- [Outreach](#outreach)
- [Events](#events)
- [Media](#media)
- [Discussions](#discussions)
- [Markets](#markets)
- [Relevant External](#relevant-external)


## Development

The work reported below has the "merged to master" status unless noted otherwise. It means that the work is completed, reviewed, and integrated into the source code that advanced users can [build and run](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c), but is not yet available in release binaries for regular users.


### dcrd

_[dcrd](https://github.com/decred/dcrd) is a full node implementation that powers Decred's peer-to-peer network around the world._

- [Optimized](https://github.com/decred/dcrd/pull/2957) cumulative work calculation using the new zero-allocation [256-bit integers](https://github.com/decred/dcrd/pull/2787) package. The result is ~100 MiB less heap usage on average, and ~5% faster initial blockchain sync time.
- Support [clean shutdown](https://github.com/decred/dcrd/pull/2958) on more Unix variants and on Windows (triggered by events like user logging off, closing terminal window, or system shutdown).
- [Inverted order](https://github.com/decred/dcrd/pull/2956) in which transactions are added to the mempool during a reorg to correct the calculation of transaction chain statistics under special circumstances. This change helps ensure miners maximize fees for large transaction chains across reorgs. There have been no problems with the old code so far because blocks aren't full and reorgs are rare.
- [Removed](https://github.com/decred/dcrd/pull/2961) the spend journal pruning code that became unneeded with the removal of the address index.
- Explicitly [reject](https://github.com/decred/dcrd/pull/2963) standalone `treasurybase` transactions. As of the activation of [DCP-6](https://github.com/decred/dcps/blob/master/dcp-0006/dcp-0006.mediawiki) every block is required to have a `treasurybase` transaction that pays the required subsidy to the Treasury. "Standalone" are unconfirmed transactions that are not part of a block. `treasurybases` do not make sense as standalone transactions because they are only valid when part of the block generation process. They have already been rejected implicitly and this change only makes it more explicit as a form of defensive coding in case future changes violate those implicit assumptions.
- [Removed](https://github.com/decred/dcrd/pull/2964) the policy that allowed low-fee/free transactions to get relayed and mined. It served its purpose in the past at the cost of some downsides. Now it is unneeded and users can bump the priority of "stuck" transactions using additional transactions (aka Child Pays For Parent - CPFP). Related `--norelaypriority` and `--limitfreerelay` CLI flags were deprecated.
- ~5 smaller improvement PRs.


### dcrwallet

_[dcrwallet](https://github.com/decred/dcrwallet) is a wallet server used by command-line and graphical wallet apps._

- [Do not require](https://github.com/decred/dcrwallet/pull/2168) deprecated V1 compact filters support when querying HTTPS seeder for nodes.


### Decrediton

_[Decrediton](https://github.com/decred/decrediton) is a full-featured desktop wallet app with integrated voting, StakeShuffle mixing, Lightning Network, DEX trading, and more. It runs with or without a full blockchain (SPV mode)._

- Added revoked [ticket hash](https://github.com/decred/decrediton/pull/3770) to the Revocation transaction page.
- Fixed a possible [never-ending loading button](https://github.com/decred/decrediton/pull/3769) on the Treasury Spending tab.
- Fixed [scrolling not working](https://github.com/decred/decrediton/pull/3771) when UI animations were disabled.
- Extended automated tests to verify the recent fixes.


### Politeia

_[Politeia](https://github.com/decred/politeia) is Decred's proposal system. It is used to request funding from the Decred treasury._

Backend:

- Updated and improved [signal-handling logic](https://github.com/decred/politeia/pull/1644) in politeiavoter by supporting SIGTERM. On Windows, this will shutdown politeiavoter cleanly if the user logs off or if the system is shutting down.
- Improved [identity logging](https://github.com/decred/politeia/pull/1647) in the dbutil tool.
- Improved [error handling](https://github.com/decred/politeia/pull/1650) in the MySQL key-value store implementation.
- ~2 smaller improvement PRs.

GUI:

- Support [dropdown header](https://github.com/decred/pi-ui/pull/455) customization.
- Fixed the submission of [empty comments](https://github.com/decred/politeiagui/pull/2783).
- Smaller optimizations and improvements.

GUI migration to the new [plugin architecture](https://github.com/decred/politeiagui/tree/master/plugins-structure#politeiagui---plugins-structure):

- Implemented [generic listeners](https://github.com/decred/politeiagui/pull/2769) that can subscribe and react to actions and state changes in any plugins.
- [Visual enhancements](https://github.com/decred/politeiagui/pull/2780) for proposals: handle censored/abandoned proposals, handle empty lists, make logo clickable.
- Implemented [New Proposal](https://github.com/decred/politeiagui/pull/2751) page.
- Implemented [default behavior](https://github.com/decred/politeiagui/pull/2775) for plugins to improve experience for developers of new plugins and Politeia-like apps.
- Implemented showing of [proposal attachments](https://github.com/decred/politeiagui/pull/2792).
- Improved UX and handing of [proposal version diffing](https://github.com/decred/politeiagui/pull/2789).
- Fixed navigating to [external links](https://github.com/decred/politeiagui/pull/2793).
- Fixed a link to [Comments](https://github.com/decred/politeiagui/pull/2802) on proposals list.
- Fixed GUI theme [not saving](https://github.com/decred/politeiagui/pull/2801) on page refresh.


### vspd

_[vspd](https://github.com/decred/vspd) is server software for running a Voting Service Provider. A VSP votes on behalf of its users 24/7 and cannot steal funds._

- More refactoring to [remove global vars](https://github.com/decred/vspd/issues/339) to make the code more reusable.


### Lightning Network

_[dcrlnd](https://github.com/decred/dcrlnd) is Decred's Lightning Network node software. LN enables instant and low-cost transactions._

- Added a new [Initial Chain Sync](https://github.com/decred/dcrlnd/pull/158) RPC service that allows to track the progress of the initial chain sync process and is useful for clients that connect to a dcrlnd instance that is still in the early startup stage to provide better feedback to the user.
- Fixed the [expected location](https://github.com/decred/dcrlnd/pull/159) of the `peers.json` file when running an embedded dcrwallet install in SPV mode.
- 4 commits with smaller improvements.


### DCRDEX

_[DCRDEX](https://github.com/decred/dcrdex) is a non-custodial, privacy-respecting exchange for trustless trading, powered by atomic swaps._

User-facing changes:

- Added support for [mixed DCR](https://github.com/decred/dcrdex/pull/1498) accounts.
- Made cancel button [change to spinner](https://github.com/decred/dcrdex/pull/1640) and report any errors in the form.
- Fixed [order age display](https://github.com/decred/dcrdex/pull/1667) when server system clock is behind client's.
- Allow users to switch between [different host names](https://github.com/decred/dcrdex/pull/1605) of the same DEX server.
- Added a [Send action](https://github.com/decred/dcrdex/pull/1611) that doesn't subtract the fee from the amount, unlike the Withdraw action.
- Added SPV support for [native (built-in) DCR wallets](https://github.com/decred/dcrdex/pull/1633).
- [Added support](https://github.com/decred/dcrdex/pull/1659) for [Descriptor Wallets](https://outputdescriptors.org/) which became default in [Bitcoin Core v23](https://bitcoincore.org/en/releases/23.0/).

Asset support progress:

- Added [results](https://twitter.com/blockchainbuck/status/1532546291783319552) of the first ETH [smart contract audit](https://github.com/decred/dcrdex/pull/1643) performed by InterFi Network (mirrored in [their repo](https://github.com/interfinetwork/smart-contract-audits/blob/audit-updates/DecredDEX_AuditReport_InterFi.pdf)). The audit concluded that Solidity code has "low risk severity" and "Decred DEX's centralization risk correlated to the active owner is NULL".
- Updated to latest [Solidity compiler](https://github.com/decred/dcrdex/pull/1679).
- Added support for [Zcash](https://github.com/decred/dcrdex/pull/1570) (decoding blocks and transactions, signing inputs, tests).
- Upgraded to [Litecoin v0.21.2](https://github.com/decred/dcrdex/pull/1536). Custom decoding of block and transaction data was added to support Litecoin's new [Extension Blocks](https://github.com/litecoin-project/lips/blob/master/lip-0002.mediawiki) and the [MimbleWimble sidechain](https://github.com/litecoin-project/lips/blob/master/lip-0003.mediawiki).
- [Generalized](https://github.com/decred/dcrdex/pull/1656) load testing to support all markets.

Internal, developer, and other changes:

- Fixed [funds unlocking](https://github.com/decred/dcrdex/pull/1642) math for smaller lot sizes.
- Redesigned [connection management](https://github.com/decred/dcrdex/pull/1474) to be more robust and have a nicer API.
- Print better [version and compatibility](https://github.com/decred/dcrdex/pull/1645) info in dexcctl output.
- Added utility for running different combinations of client [harness tests](https://github.com/decred/dcrdex/pull/1632) on simnet.
- Added [metering](https://github.com/decred/dcrdex/pull/1629) where processing of new blocks will not be triggered more frequently than every 10 seconds. e.g. in Ethereum occasionally several blocks are generated in a single second.
- Reduced [lock contention](https://github.com/decred/dcrdex/pull/1563) and fixed a memory leak in swap code.
- ~7 smaller fixes and improvements.
- ~9 bug fixes.


### GoDCR

_[GoDCR](https://github.com/planetdecred/godcr) is a lightweight desktop GUI wallet with integrated staking, privacy, Politeia voting, consensus voting, and more._

Feature development:

- Allow to restore wallets from a [hex private key](https://github.com/planetdecred/godcr/pull/950). It also shows the private key hex code on the wallet backup page.
- When Privacy has been turned on, the auto ticket buyer will only allow to [select a mixed account](https://github.com/planetdecred/godcr/pull/958) to fund ticket purchases. It also resets the config saved earlier to prevent accidental use of unmixed funds.
- Added fee asset selector to the [DEX registration](https://github.com/planetdecred/godcr/pull/900) flow.

Optimization for mobile devices:

- ~11 fixes and changes to enhance usability for [mobile device layouts](https://github.com/planetdecred/godcr/pull/963).
- ~11 more [layout fixes](https://github.com/planetdecred/godcr/pull/971) for mobile screens.

UI design updates:

- Started update to the ['V2' design](https://github.com/planetdecred/godcr/pull/969). This adds the main app navigation and implements a wallet selection page.
- Updated wallet [onboarding views](https://github.com/planetdecred/godcr/pull/996) to support multiple assets. When fully implemented, users could choose to create a Decred or Bitcoin wallet, and this will complement the DEX trading integration.
- New V2 [layout](https://github.com/planetdecred/godcr/pull/1002) and styling for the More tab.
- Updated the [Security Tools](https://github.com/planetdecred/godcr/pull/998) page to V2 design.

Internal changes:

- New string variables have been [localized](https://github.com/planetdecred/godcr/pull/906) to facilitate translations to other languages.
- Bumped the [gioui version](https://github.com/planetdecred/godcr/pull/964).
- Refactored page and modal [navigation](https://github.com/planetdecred/godcr/pull/972) to remove duplication and separate concerns.
- Added [unit tests](https://github.com/planetdecred/godcr/pull/980) for the `app` package. Added running tests to GitHub workflow.

Bug fixes:

- Fixed being [unable to access](https://github.com/planetdecred/godcr/pull/970) watch-only wallet settings menu.
- Fixed a [crash](https://github.com/planetdecred/godcr/pull/954) when deleting a watch-only wallet.
- Fixed a [crash](https://github.com/planetdecred/godcr/pull/979) when opening the Governance page.
- Fixed unintended [command prompt](https://github.com/planetdecred/godcr/pull/973) window appearing on Windows.
- Fixed buttons [not working](https://github.com/planetdecred/godcr/pull/1000) on the Governance tab. Fixed app crash due to division by zero.
- Fixed [key event handling](https://github.com/planetdecred/godcr/pull/974) for the updated gioui package.

![](../img/202206.2.github.png)

_Image: Improved mobile layout in GoDCR._


### dcrdata

_[dcrdata](https://github.com/decred/dcrdata) is an explorer for Decred blockchain and off-chain data like Politeia proposals, markets, and more._

- Use [Clipboard API](https://github.com/decred/dcrdata/pull/1917) on the UI.
- Removed experimental [CockroachDB](https://github.com/decred/dcrdata/pull/1902) support.
- Fixed incorrect [vote status](https://github.com/decred/dcrdata/pull/1919) display.
- Started the dev cycle for the [dcrdata app v6.2](https://github.com/decred/dcrdata/pull/1922) which will target Decred/dcrd v1.8. Bumped `dcrdata` module to v8 and made first breaking changes and refactoring.


### TinyDecred

_[TinyDecred](https://github.com/decred/tinydecred) is a Python toolkit for integrating Decred. It includes an experimental light GUI wallet based on PyQt5._

@buck54321 has shared an [update](https://matrix.to/#/!pzavcGbNMqkWfglXQD:decred.org/$ci88l_0Qa7W_uNgz12KXXs5fV49FmFjmuANJMAWevcg) on the second version of TinyDecred he's been working since early 2021:

- There are working Bitcoin and Decred SPV wallets that can be imported and used in Python (or any other language with a C [FFI](https://en.wikipedia.org/wiki/Foreign_function_interface)).
- A large portion of TinyWallet 2 is written in Go, combining the dcrwallet, btcwallet, and dcrlnd stuff behind a single C-shared interface.
- Since a bunch of wallet code moved to Go, using dcrwallet directly, it is now possible (with some minor modifications to dcrlnd) to use TinyWallet 2 on Lightning.
- TinyWallet 2 is designed to be available through any platform that supports web apps. This includes all major desktop and mobile platforms and browser extensions.
- To demonstrate the tech, TinyWallet has prototyped in-wallet private chat via Lightning, and a website that your wallet can interact with to guide the user into opening a Lightning channel and even finding others to add to their address book.
- TinyWallet 2 will have a DEX integration to trade DCR/BTC directly in the wallet.

A lot of this is still work-in-progress but is quite exciting already. Read the [full post](https://matrix.to/#/!pzavcGbNMqkWfglXQD:decred.org/$ci88l_0Qa7W_uNgz12KXXs5fV49FmFjmuANJMAWevcg) in Matrix and join the [#tinydecred](https://matrix.to/#/#tinydecred:decred.org/) chat to follow the development.


### Documentation

_[dcrdocs](https://github.com/decred/dcrdocs) is the source code for Decred [user documentation](https://docs.decred.org/)._

- Added [1.7 consensus votes](https://github.com/decred/dcrdocs/pull/1197) to Consensus Vote Archive. Also added versions and release dates of Decred software that implemented those consensus changes.
- Updates for the [DCP-10](https://github.com/decred/dcps/blob/master/dcp-0010/dcp-0010.mediawiki): [New numbers and graphs](https://github.com/decred/dcrdocs/pull/1198) for the [Issuance page](https://docs.decred.org/advanced/issuance/), updated [block reward values](https://github.com/decred/dcrdocs/pull/1202) on the docs home page.
- Fixes for [dark mode only](https://github.com/decred/dcrdocs/pull/1199) images.
- Issuance page graphs [changed to SVG](https://github.com/decred/dcrdocs/pull/1200) since they scale better and are easier to modify if needed in the future.
- Updated [CoinShuffle++ server name](https://github.com/decred/dcrdocs/pull/1204) to [mix.decred.org](https://mix.decred.org/). Note that it also uses a new certificate.

![](../img/202206.3.github.png)

_Image: Updated DCR issuance projection._


### decred.org

_[dcrweb](https://github.com/decred/dcrweb) is the source code for the decred.org website._

- Added [disclaimer to Exchanges page](https://github.com/decred/dcrweb/pull/1043) letting users know that only DCRDEX is self-custodial and will not request additional information.
- Removed [Contributors page](https://github.com/decred/dcrweb/pull/1047) after multiple discussions reaching the general consensus that it had reflected reality poorly.
- [Updated](https://github.com/decred/dcrweb/pull/1048) Hugo, nginx, and Lottie webplayer.
- Removed the outdated [1.6 Release page](https://github.com/decred/dcrweb/pull/1049).
- [Added](https://github.com/decred/dcrweb/pull/1044) GoDCR to the [Wallets page](https://decred.org/wallets/).


### Other

- @degeri posted his [last update](https://github.com/decred/dcrbounty/pull/88) for the Bug Bounty program. One vulnerability report has been disclosed - Android and iOS wallets were lacking screenshot protections and this has been fixed. Congrats to @trapp3rhat for joining the Hall of Fame!


## People

Community stats as of Jul 1 (compared to Jun 1):

- [Twitter](https://twitter.com/decredproject) followers: 54,380 (-94)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 12,636 (+5)
- [Matrix](https://chat.decred.org/) #general users: 689 (+12)
- [Discord](https://discord.gg/GJ2GXfz) users: 2,326 (+21)
- [Telegram](https://t.me/Decred) users: 2,810 (-48)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,630 (+0), views: 210K (+1K)


## Governance

In June the new [treasury](https://dcrdata.decred.org/treasury) received 9,134 DCR worth $256K at June's average rate of $28.06. 2,426 DCR was spent to pay contractors, worth $68K at June's rate, or $100K at May's billing rate of $41.46.

With the activation of DCP-0007 it was once again possible to pay contractors from the new treasury using the proper stakeholder-approved method. This [transaction](https://explorer.dcrdata.org/tx/18cede674d4d47919e7fcdb48fef0f56162a1a2f9536d5f08ac70e093a14e4f5) hit the required voting threshold (with 4,822 Yes votes and 0 No votes) on June 27th, meaning the vote ended in 10 days versus the full possible 12 days due to being guaranteed to pass regardless of the remaining votes, and so the turnout among the ~14,400 tickets that had a chance to vote was ~33% (above the quorum of 20%). There were 23 outputs, suggesting roughly this number of contractors/intermediaries were paid in the month, amounts ranging from 2.87 DCR to 767 DCR. Check the [May 2021 issue](202105.md#new-treasury-activated) for a recap on how the new treasury works.

As of July 3, combined balance of [legacy](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) and [new treasury](https://dcrdata.decred.org/treasury) is 799,639 DCR (17.9 million USD at $22.39).

Three new proposals were submitted in June:

- The [Decred Brazil proposal](https://proposals.decred.org/record/7f1d013) requests a budget of $22,000 for social media content production and events in Brazil, it is being led by @victorguedes.

- The [GoDCR proposal](https://proposals.decred.org/record/0ef42e5) requests $250,000, edited down from $300,000 initially, to continue development of GoDCR for one year. GoDCR was funded [initially](https://proposals-archive.decred.org/proposals/e5c8051) by the treasury but a second [request](https://proposals.decred.org/record/f7d9fc8) for $200,000 funding was rejected in Oct 2021 by stakeholders with 49% Yes votes and 73% turnout.

- [Decred Magazine](https://proposals.decred.org/record/3bb2c7e) has requested $34,000 for a year of content production and aggregation on the new website [DecredMagazine.com](https://www.decredmagazine.com/), led by @phoenixgreen.

Voting was held for four proposals, three of which were approved and one failed to reach the quorum requirement:

- The [proposal](https://proposals.decred.org/record/4fdef29) to fund Decred Journal and Politeia Digest was approved with 99% Yes votes and turnout of 56%.

- The [proposal](https://proposals.decred.org/record/7057e0b) to fund Decred content and asset translations was approved with 99% Yes votes and turnout of 56%.

- The [proposal](https://proposals.decred.org/record/da2f32d) to fund continuation of the Bug Bounty program was approved with 99% Yes votes and turnout of 56%.

- The [proposal](https://proposals.decred.org/record/6bdffcb) to fund university events in Uganda was rejected with 47% Yes votes and turnout of 6%.

See [May issue](202205.md#governance) for a recap on voted proposals and Politeia Digest [issue 52](https://blockcommons.red/politeia-digest/issue052/) for more details on June's proposals.


## Network

**Hashrate**: June's [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&zoom=l3n3qjwe-l5batou0&bin=block&axis=time&visibility=true-false) opened at ~117 Ph/s and closed ~85 Ph/s, bottoming at 68 Ph/s and peaking at 132 Ph/s throughout the month.

![](../img/202206.4.github.png)

_Image: Hashrate has somewhat stabilized around 100 Ph/s._

Distribution of hashrate [reported](https://miningpoolstats.stream/decred) by the pools on Jul 1: Poolin 51%, ViaBTC 20%, F2Pool, 17%, AntPool 7%, BTC.com 4%, LuxorTech 1.2%, CoinMine 0.5%.

Distribution of 1,000 blocks actually [mined](https://miningpoolstats.stream/decred) by Jul 1: Poolin 50%, ViaBTC 20%, BTC.com 5%, LuxorTech 1.3%, CoinMine 0.3%, unknown 24.1%.

**Staking**: [Ticket price](https://dcrdata.decred.org/charts?chart=ticket-price&zoom=l3n3qjwe-l5batou0&axis=time&visibility=true-true&mode=stepped) varied between 216-235 DCR, with 30-day [average](https://dcrstats.com/) at 223.7 DCR (+0.1).

The [locked amount](https://dcrdata.decred.org/charts?chart=ticket-pool-value&zoom=l3n3qjwe-l5batou0&scale=linear&bin=block&axis=time) was 8.97-9.17 million DCR, meaning that 62.9-**64.2%** of the circulating supply [participated](https://dcrdata.decred.org/charts?chart=stake-participation&zoom=l3n3qjwe-l5batou0&scale=linear&bin=block&axis=time) in Proof of Stake.

![](../img/202206.5.github.png)

_Image: Staking participation crawling up._

**VSP**: On Jul 1, ~7,150 (+250) live tickets were managed by [listed](https://decred.org/vsp/) vspd servers. Collectively the 16 VSPs managed 17.3% of the ticket pool (+0.5%).

Top 3 gainers are stakey.com (+408, +19%), ultravsp.uk (+295, +101%), and stakeminer.com (+127, +23%).

**Nodes**: Throughout June there were around 180 reachable nodes according to [PD Analytics](https://analytics.planetdecred.org/nodes).

Node versions captured by [Decred Mapper](https://nodes.jholdstock.uk/user_agents) on Jul 1 (118 total, dcrd only): v1.7.1 - 41%, v1.7.2 - 26%, v1.7.0 - 12%, v1.7.0 dev builds - 8%, v1.8.0 dev builds - 3.4%, v1.6 series - 6.8%, v1.5 series - 0.9%, v1.4 series - 2.5%.

The share of [mixed coins](https://dcrdata.decred.org/charts?chart=coin-supply&zoom=jz3q237o-la8vk000&scale=linear&bin=day&axis=time&visibility=true-true-true) varied between 59.8-**60.2%**. Daily [mixed amount](https://dcrdata.decred.org/charts?chart=privacy-participation&zoom=l3n3qjwe-l5batou0&bin=day&axis=time) varied between 160-455K DCR.

Decred's [Lightning Network](https://ln-map.jholdstock.uk/) has seen 44 nodes (-1), 72 channels (-6) with a total capacity of 36.7 DCR (-4.8), as of Jul 1 (compared to Jun 1).


## Ecosystem

[Guardarian](https://guardarian.com/) has [announced](https://www.reddit.com/r/decred/comments/v7mske/more_ways_to_buy_decred/) that buying and selling DCR for fiat is possible on their platform. Supported fiat currencies are EUR, USD, and GBP, and they can be sent over payment processors like MasterCard, Visa, SWIFT, SEPA, and Faster Payments. Fiat payouts go directly to the user's bank account, while purchased coins go directly to the user's wallet. There is a minimum amount to buy (EUR 30) and the service fee (EUR 2.49) is added to exchanges. Guardarian is licensed in Estonia.

[Bitpanda](https://www.bitpanda.com/en) announced that [DCR is listed](https://twitter.com/bitpanda/status/1537047267647037442) on their exchange and acknowledged its open governance and sustainable funding. Bitpanda is [headquartered](https://en.wikipedia.org/wiki/Bitpanda) in Vienna, Austria.

BisonPool [revealed](https://twitter.com/BisonPool/status/1540362478588203011) that it will be a custodial staking service allowing users to stake with less than a full ticket (recently around 220 DCR). The reveal came after [teasing](https://twitter.com/BisonPool/status/1537812247283744769) on Twitter demonstrating a ticket purchased from 3 parts around 80 DCR each. The announcement received [some criticism](https://matrix.to/#/!ggjLwhBHTjsMROezFf:decred.org/$Ixlkkg5b0Pf7p6WMsz8X7etigqAg9p6XSCkp8EyN-9c) in the Matrix #media room for the service's custodial nature. BisonPool came to [respond](https://matrix.to/#/!ggjLwhBHTjsMROezFf:decred.org/$Pn_E4JWbdTKheQ8NfwKFDm5auZLIhPSUv2ruCmFs-cs) and explain their vision and strategy.

[JobsOnBlocks](https://jobsonblocks.com) is a new job board for offering/requesting jobs to get paid in crypto. Site beta was [launched in June](https://twitter.com/Toussaint_dev/status/1537512603345293312) and as of writing it supports 5 coins and has 3 jobs posted. The founder has dropped the announcement in our #trading chat, saying that DCR is supported since launch:

> you can post a job and choose dcr as a payment coin, added it just for the bison crew 😉 \[[@Toussaint](https://matrix.to/#/!lDZCzVQjFoJsXMPkvr:decred.org/$uxS2SUWZRUVbKH9DMiok_uuiomuZmq82q7bI61wDuW0)\]

@jz [posted a script](https://twitter.com/jz_bz/status/1535350896091189249) for spinning up a Decred full node on popular systemd-based Linux distros with a simple `curl -L node.dcr.pw | bash` command. It is a good practice to not blindly run code from the Internet and read it before executing (the script is just 40 lines).

VSP users may find these two tables useful for deciding which provider to use: one summarizing how legacy VSPs [have been shutdown](https://github.com/decred/vspd/issues/231#issuecomment-774877129), and another showing how the VSP operators [have been upgrading](https://github.com/decred/vspd/issues/231#issuecomment-1046703692) their servers (sooner is better).

Luxor's Decred mining pool shutdown was [rumored on Reddit](https://www.reddit.com/r/decred/comments/v6d0lw/luxor_shutdown_their_dcr_mining_pool/) after one user received an email asking to withdraw all funds by Jun 10. Screenshot of the email had a notable factual error "DCR is going to PoS". While Decred has [reduced](https://github.com/decred/dcps/blob/master/dcp-0010/dcp-0010.mediawiki) PoW miners' block reward share from 60% to 10%, there is no intent or even a discussion to switch to pure PoS. As of Jul 9, there has been no official commentary from [@LuxorTechTeam](https://twitter.com/LuxorTechTeam) and their API still report the hashrate of 1.5 Ph/s (1.5% of network's total 95 Ph/s) and 107 miners.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

Join our [#ecosystem](https://chat.decred.org/#/room/#ecosystem:decred.org) chat to follow Decred ecosystem updates.


## Outreach

Monde PR's achievements:

- Pitched Decred to 5 PR opportunities.
- Responded to 1 request for commentary.
- Secured 1 media interview.

Secured the following news articles:

- A video interview with [Invezz](https://invezz.com/news/2022/06/01/co-founder-jake-yocom-piatt-discusses-alternate-stores-of-value-to-bitcoin/) and @jy-p talking about Decred's governance model, the hybrid PoW/PoS model, project treasury, privacy, future outlook and how we compare to Bitcoin.
- Invezz posted the story in 10 other languages including [Dutch](https://invezz.com/nl/nieuws/2022/06/01/mede-oprichter-jake-yocom-piatt-bespreekt-alternatief-oppotmidd-voor-bitcoin/) and [Swedish](https://invezz.com/sv/nyheter/2022/06/01/medgrundaren-jake-yocom-piatt-diskuterar-alternativa-vardebutiker-till-bitcoin/).
- The story was also syndicated to three publications including [Bitcoin Insider](https://www.bitcoininsider.org/article/168719/co-founder-jake-yocom-piatt-discusses-alternate-stores-value-bitcoin) and [Crypto News BTC](https://cryptonewsbtc.org/2022/06/01/co-founder-jake-yocom-piatt-discusses-alternate-stores-of-value-to-bitcoin/).
- @jy-p appeared on the [CoinJournal podcast](https://coinjournal.net/news/interview-with-decred-project-lead-jake-yocom-piatt/) talking about a range of topics including sovereign money, true decentralization, DEXs and privacy.
- CoinJournal posted the interview on its [Norway](https://coinjournal.net/no/nyheter/intervju-med-decred-prosjektleder-jake-yocom-piatt/) and [Finland](https://coinjournal.net/fi/uutiset/haastattelussa-decred-projektin-johtaja-jake-yocom-piatt/) sites.
- The interview was also syndicated to [Bitcoin Insider](https://www.bitcoininsider.org/article/172467/interview-decred-project-lead-jake-yocom-piatt).


## Events

**Attended:**

- @arij [signed a partnership](https://decredcommunity.github.io/events/index/20220601.1) with Moroccan JCI, which is the first branch of the global [Junior Chamber International](https://en.wikipedia.org/wiki/Junior_Chamber_International) NGO in Africa and the Arab world. The partnership includes providing training to members of this organization and other companies, concerning blockchain and Decred tech.

**Upcoming:**

- On October 6-7 Decred will be participating in [Crypto Forum](https://twitter.com/Decred_BR/status/1540102065128603649) in Sao Paulo, Brazil.


## Media

[Decred Magazine](https://www.decredmagazine.com/) has grown by 12 posts in June and continues serving as a mirror for [Decred Journal](https://www.decredmagazine.com/tag/decred-journal/) and [Politeia Digest](https://www.decredmagazine.com/tag/politeia-digest/) with nice features like lightweight pages and working well without JavaScript. @phoenixgreen made 3 videos about Decred Magazine:

- [Decred Magazine overview](https://www.youtube.com/watch?v=OQ9adrXDJNo)
- [Becoming a contributor](https://www.youtube.com/watch?v=g2BE1GoNE98)
- [Privacy, translations and backups](https://www.youtube.com/watch?v=RJy8Ky7Ovhc)

Authors wanted! Contact @phoenixgreen in Matrix [#writers](https://chat.decred.org/#/room/#writers:decred.org) chat or [@DecredSociety](https://twitter.com/DecredSociety) on Twitter.

**Videos:**

- [Decred interview: Co-founder Jake Yocom-Piatt discusses alternate stores-of-value to Bitcoin](https://www.youtube.com/watch?v=_QsWw4EDPyg) by Dan Ashmore for Invezz
- [Changing the rules - Decred and the State of the Market with Dave Collins - Lead Developer](https://www.youtube.com/watch?v=9rzyYxS3T74) by @Exitus and @phoenixgreen
- [DCRDATA growth and adoption charts](https://www.youtube.com/watch?v=KXfqaYyCUmE) by @phoenixgreen - also as a [blog post](https://www.decredmagazine.com/dcrdata-growth-and-adoption-charts/)
- [GoDCR: A new lightweight SPV wallet for Decred - Quick Overview](https://www.youtube.com/watch?v=IDilYl3GhKw) by @Exitus
- [DCRDATA - Comparing on-chain data](https://www.youtube.com/watch?v=BDKgjgHN83A) by @phoenixgreen - also as a [blog post](https://www.decredmagazine.com/dcrdata-comparing-on-chain-data/)
- [Interview w/ Jake Yocom-Piatt: Sovereignty, privacy, Decred so far](https://www.youtube.com/watch?v=EAiIAbKQAjI) with Joe K.B. and Dan Ashmore for CoinJournal - also [on Spotify](https://open.spotify.com/episode/7fB2BUmg8zFoIt1F7wZU4l)

**Art and fun:**

- u/ersfbddfgwe created a [music track](https://soundcloud.com/openbeats/ob1) as part of the Open Beats idea, which has a goal to provide community-made music that can be freely used for any Decred-related content

**Translations:**

- Decred Journal April 2022 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij) and Chinese (@Dominic). The May 2022 issue was also translated to Chinese (@Dominic). Thank you all!


## Discussions

Selected Reddit posts:

- [Should we re-brand Decred DEX?](https://www.reddit.com/r/decred/comments/v3gxa8/should_we_rebrand_decred_dex/) by @buck54321. @bee has collected the 12 name ideas posted so far [in one table](https://gist.github.com/xaur/5527e5ed280a448e56a62751ab636f14). "[QuackDEX](https://www.reddit.com/r/decred/comments/v3gxa8/should_we_rebrand_decred_dex/ib4o30g/)" has a chance.
- The Weekly Contributions initiative had its [Week 1](https://www.reddit.com/r/decred/comments/v5ipch/weekly_contributions_week_1/), [Week 2](https://www.reddit.com/r/decred/comments/vav9h6/weekly_contributions_week_2/) and [Week 3](https://www.reddit.com/r/decred/comments/vg6rpn/weekly_contributions_week_3/) with a few old-timers trying to bootstrap it with their submissions. Anything from running a full node to making a cool tweet thread or a meme counts, so don't hesitate to participate!

Selected Twitter discussions:

- @jy-p commented on central banks painting themselves into a corner with FRS having to choose between [allowing inflation or causing a recession](https://twitter.com/behindtext/status/1537151269357375490), which presents a huge [opportunity for crypto](https://twitter.com/behindtext/status/1537587436905439232), although it's not expected to be a smooth ride.
- Vitalik Buterin [stealth-pushed](https://twitter.com/VitalikButerin/status/1540233065368354817) "the 2013-15 era designs where you have interwoven PoW and PoS blocks" in response to Dan Robinson's poll on changing Bitcoin, but refrained from mentioning [any specific project](https://cointelegraph.com/news/decred-an-innovative-cryptocurrency-or-a-well-arranged-scam) implementing those designs, hopefully to build up anticipation and discussion among the audience.


## Markets

In June DCR was trading between USD 20.00-41.19 / BTC 0.00102-0.00141. The average daily rate was $28.06.

@Applesaucesome posted two biweekly [market](https://www.decredmagazine.com/bear-market-blues/) [overviews](https://www.decredmagazine.com/bottom-calling/) with charts and commentary on crypto and the broader market.

> If we turn on both indicators we can find that there is strong confluence between the two. If you pair the 2-year MA Multiplier's buy zones along with price action within the bottom most Mayer Multiple band you'll find that you could've just stocked up hard in those areas and then waited out the bear market. Will this be the same? Only time will tell. Also, don't be irresponsible with your money.

![](../img/202206.6.github.png)

_Image: Combined 2Y MA Multiplier and Mayer Multiplier may signal buy zones. Or not. Trade wisely._

![](../img/202206.7.github.png)

_Image: DCRDEX monthly traded volume in DCR._


## Relevant External

The crypto markets saw a significant decline in June, and although this paralleled non-crypto market sell-offs more broadly the crypto space saw its own particular issues around the insolvency of centralized entities and fears of contagious bad debt which could wipe out influential players in the crypto markets. One of the major threads to this unwinding concerned Three Arrows Capital (3AC), a hedge fund which was heavily exposed to the collapse of LUNA and then began [struggling](https://www.wsj.com/articles/battered-crypto-hedge-fund-three-arrows-capital-considers-asset-sales-bailout-11655469932) to meet margin calls as the prices for crypto assets tanked - partially instigated by the selling of Terra Foundation's BTC reserve to try and support the collapsing price of TerraUSD. The opacity of dealings between these centralized entities was highlighted by the behavior of 3AC's founders, formerly very active social media users who reportedly ghosted everyone their fund owed money to for an extended period. Over the course of June it has been slowly [revealed](https://www.coindesk.com/business/2022/06/29/genesis-faces-hundreds-of-millions-in-losses-as-3ac-exposure-swamps-crypto-lenders-sources/) that many large industry players had placed money with 3AC (which in turn placed significant sums in Anchor protocol for 20% yield on TerraUSD) and now won't expect to see much of this back. It is striking that such significant events for the crypto markets were mostly known about for some time through the on-chain investigations of interested parties sharing their findings on Twitter - and that the on-chain entities these parties were transacting with held up relatively well through market turbulence, behaving as expected and forecast by observers.

On-chain investigations have also revealed things that market participants would have rather kept confidential, like the price at which their leveraged positions would be liquidated. It was seemingly forced selling of assets to meet margin calls on DeFi platforms which alerted the observers to 3AC's issues. For the Solana chain lending service Solend, one particular whale's liquidation price and the scale of their position (>95% of the pool's deposits) was concerning enough that a vote was held to [determine](https://www.coindesk.com/tech/2022/06/19/solana-defi-platform-votes-to-control-whale-account-in-bid-to-avoid-liquidation-chaos/) whether Solend Labs should be granted "emergency powers" to take control over this whale's funds and liquidate their position OTC in a way which would not cause chaos for Solend users generally.

Some DAO on DAO [conflict](https://www.coindesk.com/business/2022/06/14/gaming-dao-merit-circle-ygg-terminate-relationship/) occurred in the "play to earn" space, with Merit Circle previously voting to "refund" the investment of Yield Guild Games (YGG) in their tokens - at a price much lower than the current market price. This raised many questions about whether a DAO's members could unilaterally vote to change the terms of a deal the DAO had entered into - complicated significantly by the [confidentiality](https://twitter.com/Crypt0_lawyer/status/1536826577945862144) of the contract between the firms/DAOs. It seems that some members of the "DAOs" have hashed out a [deal](https://www.coindesk.com/business/2022/06/14/gaming-dao-merit-circle-ygg-terminate-relationship/) to bring this to a conclusion without a potentially complex and expensive legal intervention.

For some months now [concern](https://www.coindesk.com/layer2/2022/04/20/is-ethereum-staking-pool-lidos-growth-an-omen-of-centralization/) has been growing in the Ethereum community about the level of ETH 2.0 staking which Lido Finance is responsible for (30% in April) - and the level of control over this mechanism which holders of the LDO token can exercise. In June a new [governance](https://research.lido.fi/t/ldo-steth-dual-governance/2382) proposal was introduced for LDO which would give stETH holders veto powers over some aspects of decision-making about the protocol.

To use Lido one deposits ETH and receives stETH, which will be redeemable for ETH on the new chain some months after "the merge" occurs - so the staked ETH is illiquid, but one can sell the stETH. Loss of parity between ETH and stETH was a particular stressor for [Celsius](https://decrypt.co/102812/celsius-liquidity-crunch-lido-staked-ethereum-steth), which was reliant on parity between ETH/stETH for its products to work as intended. Celsius was one of the firms that has been implicated in the contagious bad debt situation, owing significant sums to depositors and [freezing withdrawals](https://www.cnbc.com/2022/06/20/celsius-asks-users-for-more-time-to-fix-issues-after-withdrawal-freeze.html) due to inability to meet demand.

The European Union has moved closer to [finalizing](https://www.coindesk.com/policy/2022/06/29/eu-finalizes-crypto-money-laundering-rules/) its regulatory treatment of many aspects of crypto transactions. Many aspects of the regulation have been known for some time, but last minute negotiation was needed to determine thresholds for when a transfer between a CASP's (Crypto Asset Service Providers) wallet and an "unhosted" wallet would need to verify the recipient's identity. For transfers between CASPs they must verify each others' control of addresses. When a customer requests withdrawal to an unhosted address they must state the identity, and when it is to their own wallet they must verify control of the address when the value of the transfer exceeds 1,000 Euros. Peer to peer transactions have no reporting requirements. Long [established](https://twitter.com/paddi_hansen/status/1540640287923380225) aspects of the regulation will see significant barriers to the issuance of stablecoins, including "algorithmic" stablecoins.

The founder of Maker DAO (MKR), Rune, [returned](https://thedefiant.io/makerdao-radical-makeover-plan/) to the governance forum this month, bringing with him some radical plans to shake up Maker's governance in the form of an "[Endgame Plan](https://thedefiant.io/makerdao-radical-makeover-plan/)". Rune had been absent from the scene since the Foundation was dissolved, and he has returned just as the people who were filling the voids he left in Maker's governance in various ways were bringing their own proposals for how things should work to the Maker stakeholders. Three proposals which had been under discussion for some time met resistance in their formal votes as participation rates for MKR voting [set a new all time high](https://thedefiant.io/makerdao-governance-proposals/), with a maximum of 33% voting in the LOVE-001 proposal - a proposal which would have introduced an "oversight Core Unit", and was defeated with 60% No votes. The three big proposals to change how Maker DAO functions were all defeated, with significant late stage [redelegation](https://dirtroads.substack.com/p/-42-valkyrie-makerdao-and-our-side) of votes and the reappearance of another co-founder who had fallen out with the project long ago but retained a large voting stake and came back to vote No on everything, dropping an [expletive-filled tirade](https://forum.makerdao.com/t/a-few-thoughts-before-i-finish-voting/16078) against the community's decision to turn off the buy-back and burn mechanism.

That's all for June. Share your updates for the next issue in our [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat room.


## About

This is issue 48 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from the source after a minimal sanity check. The authors of the Decred Journal cannot verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing and editing: bee, bochinchero, Exitus, l1ndseymm, richardred
- reviews and feedback: davecgh, buck54321
- funding: Decred stakeholders
