# Decred Journal – August 2022

![](img/202208.1.github.png)

_Image: "Inspired" by @saender's new decred.org design._

Highlights of August:

- An overhaul of the decred.org website has been proposed, passed and deployed.
- Politeia v1.4.0 has been released, new features include a 5 minute window to edit one's comments.
- DCRDEX v0.5.2 is out and can be run already by impatient traders who don't want to wait for the Decrediton integration update which is in the works.
- v1.7.4 of core Decred software was released as source code only to fix a testnet which has been stalled by ASIC miners.

Contents:

- [Politeia v1.4.0 Released](#politeia-v140-released)
- [Development](#development)
- [People](#people)
- [Governance](#governance)
- [Network](#network)
- [Ecosystem](#ecosystem)
- [Outreach](#outreach)
- [Media](#media)
- [Discussions](#discussions)
- [Markets](#markets)
- [Relevant External](#relevant-external)


## Politeia v1.4.0 Released

New Politeia release is live after 8 months of development! Highlights include:

- Importing legacy proposals was the biggest chunk of work for this release. Now all proposals are available at [proposals.decred.org](https://proposals.decred.org/) and there is no separate archive website.
- Comments can be edited in the 5 minutes immediately after posting.
- Censorship reason and moderator is shown for censored proposals.
- Improved drafts UX.
- Initial work for the new architecture for building Politeia-like apps.

See full release notes in [politeia](https://github.com/decred/politeia/releases/tag/v1.4.0) and [politeiagui](https://github.com/decred/politeiagui/releases/tag/v1.4.0) repositories.


## Development

The work reported below has the "merged to master" status unless noted otherwise. It means that the work is completed, reviewed, and integrated into the source code that advanced users can [build and run](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c), but is not yet available in release binaries for regular users.


### dcrd

_[dcrd](https://github.com/decred/dcrd) is a full node implementation that powers Decred's peer-to-peer network around the world._

dcrd v1.7.4 was released to fix testnet mining algorithm as detailed below. It was a source code only release as it is primarily intended for developers.

Merged in `master` and backported to v1.7.4 release:

- Enforced [difficulty throttling](https://github.com/decred/dcrd/pull/2978) on testnet. Normally ASICs are not expected on testnet and blocks are mined with "slow" CPU mining, since it's not reasonable to require high-powered hardware to run testnet. There is no financial incentive either because testnet coins have no value and ASIC miners have a better choice to mine mainnet coins for profit. Despite that, an unusual hashrate of ~78 Th/s (equivalent of 2 Antminer DR5) joined Decred testnet and mined for ~5 hours, which ramped up the difficulty and effectively stalled the network. To limit the type of games that ASICs can play on testnet two new rules are introduced: a limit on maximum allowed difficulty and a limit on block production rate once maximum difficulty is reached. This should keep CPU mining feasible even in the presence of GPUs and ASICs. It should be noted that this solution is only suitable on a test network where no real monetary value is in play and thus the typical game theory mechanics do not apply.

- Optimized handling of blocks with too few ticket votes to also [copy the regular transactions](https://github.com/decred/dcrd/pull/2978/commits/659b7fed1f225861b8b689ead1a0466099992479) into an alternative block template in addition to the stake transactions. This makes template creation more robust in the case of duplicate spends and helps ensure that all transactions in an invalidated (under-voted) block are added to alternative block templates. Previously all transactions were copied too but only in the next block, so this change removes an unnecessary delay.

Merged in `master` towards v1.8:

- Made longer running `blockchain` tests [run in parallel](https://github.com/decred/dcrd/pull/2988) to reduce the overall testing time roughly in half.
- Removed all code related to [previous script snapshots](https://github.com/decred/dcrd/pull/2989) now that address index has been removed and there are no other indexers that require access to previous scripts.
- Maintenance and smaller fixes.


### dcrwallet

_[dcrwallet](https://github.com/decred/dcrwallet) is a wallet server used by command-line and graphical wallet apps._

Merged in `master` and backported to v1.7.4 source-only release:

- Implemented method for importing arbitrary [public keys](https://github.com/decred/dcrwallet/pull/2177) and their derived addresses. It is only supported for watching-only wallets.
- Added checkpoints to [hard-fork testnet3](https://github.com/decred/dcrwallet/pull/2178) to new rules implemented in dcrd. Checkpointing is used to push the wallet onto the intended unvoted chain due to it having significantly less total work than the chain being reorged.

Merged in `master`:

- Updated [difficulty checks](https://github.com/decred/dcrwallet/pull/2181) to the new throttling rules on testnet3.


### dcrctl

_[dcrctl](https://github.com/decred/dcrctl) is a command-line client for dcrd and dcrwallet._

- Updated to latest [Go modules](https://github.com/decred/dcrctl/pull/49) and [GitHub action](https://github.com/decred/dcrctl/pull/48) versions.


### Decrediton

_[Decrediton](https://github.com/decred/decrediton) is a full-featured desktop wallet app with integrated voting, StakeShuffle mixing, Lightning Network, DEX trading, and more. It runs with or without a full blockchain (SPV mode)._

- Added the ability to [refresh](https://github.com/decred/decrediton/pull/3785) the DEX window with F5 key.
- Treasury spending page now uses [testnet Pi keys](https://github.com/decred/decrediton/pull/3776) on testnet and has proper links to verify them in dcrd's source code.
- Corrected "Stakeshuffle++" to "StakeShuffle" in [Privacy tab](https://github.com/decred/decrediton/pull/3779).
- ~4 fixes and other internal updates.


### Politeia

_[Politeia](https://github.com/decred/politeia) is Decred's proposal system. It is used to request funding from the Decred treasury._

Backend:

- Optimized and improved validation in [`dbutil -migrate`](https://github.com/decred/politeia/pull/1667) command (used to migrate from one user database to another).
- Store [app version](https://github.com/decred/politeia/pull/1671) as a single string to simplify the release process.
- Various [updates](https://github.com/decred/politeia/pull/1672) for Go 1.19 (CI configuration, GitHub Actions, linter, and [code formatting](https://github.com/decred/politeia/pull/1673)).
- Delete [expired user sessions](https://github.com/decred/politeia/pull/1669) on startup. Tests for the session database have been [rewritten](https://github.com/decred/politeia/pull/1674) to fix numerous issues.
- Updated [`dbutil -dump`](https://github.com/decred/politeia/pull/1676) command to work with all of the user database implementations.
- Freeze [Trillian trees](https://github.com/decred/politeia/pull/1670) that correspond to Politeia records that no longer allow updates (such as Censored or Archived). Politeia's use of Trillian is quite different from its intended use case and it results in high CPU load. Freezing some trees should reduce it.

Current GUI:

- Keep [quorum label](https://github.com/decred/politeiagui/pull/2836) for Approved and Rejected proposals.
- Fixed common [invalid signature](https://github.com/decred/politeiagui/pull/2842) error for new keys that were used before getting registered on the server.
- Fixed 2 bugs with legacy [RFP proposals](https://github.com/decred/politeiagui/pull/2845) and ~6 bugs with legacy proposal [comments](https://github.com/decred/politeiagui/pull/2852).

GUI remake on the new [plugin architecture](https://github.com/decred/politeiagui/tree/master/plugins-structure#politeiagui---plugins-structure):

- Deduplicated common [Babel and Jest](https://github.com/decred/politeiagui/pull/2838) configuration.
- Added various information to the `pi` plugin: proposal status, vote duration, quorum, billing status changes, and error messages.
- Added [end-to-end tests](https://github.com/decred/politeiagui/pull/2803) based on Cypress.
- Implemented RFP [proposals and submissions](https://github.com/decred/politeiagui/pull/2848).
- Reuse [view breakpoints](https://github.com/decred/politeiagui/pull/2849) from pi-ui. Breakpoints control which layout is used to match the user's screen size.
- ~5 fixes
- Code refactoring and cleanup

pi-ui shared library:

- [Custom breakpoints](https://github.com/decred/pi-ui/pull/459) made reusable internally and by apps that consume `pi-ui`. Wired up [PostCSS](https://postcss.org/) for CSS processing.

![](../img/202208.2.github.png)

_Image: Updated RFP proposal view in Politeia._


### Lightning Network

_[dcrlnd](https://github.com/decred/dcrlnd) is Decred's Lightning Network node software. LN enables instant and low-cost transactions._

LN Daemon:

- Add `EnforcePing` [RPC call](https://github.com/decred/dcrlnd/pull/163). This allows callers to direct dcrlnd to ping the specified peer and wait for the response. If the response fails to be received, then the peer is disconnected.
- Added [stall detection and disconnection](https://github.com/decred/dcrlnd/pull/162) for peers. This is needed to handle situations where the computer running dcrlnd is suspended and then resumes after enough time has passed for the remote peer to have disconnected.
- Reduce [peer idle timeout](https://github.com/decred/dcrlnd/commit/02793bc8d7e2fb1b0775f24b87bad4c892e62ba9) to 1 minute and 30 seconds, down from 5 minutes. A 5 minute idle timeout is excessive and prevents correct early detection of stalled peers.

[Liquidity Provider Daemon](https://github.com/decred/dcrlnlpd):

- Configured [GitHub Actions](https://github.com/decred/dcrlnlpd/pull/5) for automated builds.
- Documented how the software [takes control](https://github.com/decred/dcrlnlpd/pull/4) of outbound channels.
- Added [TLS encryption](https://github.com/decred/dcrlnlpd/pull/6) support.


### DCRDEX

_[DCRDEX](https://github.com/decred/dcrdex) is a non-custodial, privacy-respecting exchange for trustless trading, powered by atomic swaps._

DCRDEX v0.5.2 has been released! Check the [v0.5.0 release](https://github.com/decred/dcrdex/releases/tag/v0.5.0) first for a long list of features, fixes and instructions to upgrade from v0.4. Starting with the [v0.5.2 release](https://github.com/decred/dcrdex/releases/tag/v0.5.2) DCRDEX now publishes its own binaries. As always, [verifying them](https://docs.decred.org/advanced/verifying-binaries) is strongly recommended.

Note that there has been no announcement yet because DCRDEX is coordinating with the other components (such as Decrediton).

August changes included in the v0.5 release:

- Moved [wiki contents](https://github.com/decred/dcrdex/pull/1714) to [docs/wiki](https://github.com/decred/dcrdex/tree/master/docs/wiki) in the main repo. Now all docs are in one place and can be updated and reviewed by more contributors via the pull request workflow.
- Rewritten much of [README](https://github.com/decred/dcrdex/pull/1747) for the v0.5 release.
- Updated to use the new [testnet3 rules](https://github.com/decred/dcrdex/pull/1773) and switched LTC block explorer from bitaps.com to sochain.com.
- Embeded site resources using [`go:embed`](https://github.com/decred/dcrdex/pull/1710).
- Updated [German](https://github.com/decred/dcrdex/pull/1815) translation.
- Code maintenance.

August fixes included in v0.5:

- Fixed several client wallet [hanging issues](https://github.com/decred/dcrdex/pull/1732).
- Fixed a [deadlock](https://github.com/decred/dcrdex/pull/1756) in BTC SPV wallet.
- Fixed [switching wallet type](https://github.com/decred/dcrdex/pull/1759) to SPV.
- Fixed several [deadlock and lock contention](https://github.com/decred/dcrdex/pull/1739) issues in the trade engine.
- Fixed having to [refresh Wallets page](https://github.com/decred/dcrdex/pull/1757) manually after creating a wallet.
- Fixed [match status](https://github.com/decred/dcrdex/pull/1772) display for revoked matches.
- ~10 other client fixes and ~2 backend/internal fixes.

User-facing changes towards the next v0.6 release:

- End user (trader) documentation [moved](https://github.com/decred/dcrdex/pull/1715) to [its own document](https://github.com/decred/dcrdex/blob/master/docs/wiki/Client-Installation-and-Configuration.md).
- Improved candlestick chart accuracy by using epoch's first and last [match price](https://github.com/decred/dcrdex/pull/1781) for candle's start and end rate.
- Restyled the [Wallets page](https://github.com/decred/dcrdex/pull/1700). The new style is responsive and adjusts to desktop, tablet and mobile screen sizes.
- Adjusted [order cancellation](https://github.com/decred/dcrdex/pull/1682) policy to penalize too fast cancellations. If the order sits for at least one full epoch it can still be cancelled for "free" (without hurting user's reputation score). This should improve trading experience [for humans](https://github.com/decred/dcrdex/pull/1682#issuecomment-1165059876).
- Implemented [live wallet reconfiguration](https://github.com/decred/dcrdex/pull/1786) for DCR and ETH. It allows to correctly track locked coins across changes to wallet configuration.

Backend and developer changes towards the next v0.6 release:

- Server installation guide [moved](https://github.com/decred/dcrdex/pull/1793) to [its own document](https://github.com/decred/dcrdex/blob/master/docs/wiki/Server-Installation.md).
- Updated [dependencies](https://github.com/decred/dcrdex/pull/1785) to latest btcsuite, go-ethereum, go-bip39 and minimum Go 1.18.
- Added a guide to get started with [writing fuzzing tests](https://github.com/decred/dcrdex/pull/1766).
- Automated [Markdown linting](https://github.com/decred/dcrdex/pull/1796) to ensure consistent formatting.
- Transaction wait time made [configurable](https://github.com/decred/dcrdex/pull/1789) by server operator. It is the maximum time server will search for client-reported transactions before erroring.
- Updated Node.js [dependencies](https://github.com/decred/dcrdex/pull/1792) for the v0.6 dev cycle.
- Translated page templates are now generated [at runtime](https://github.com/decred/dcrdex/pull/1826). It removes the need to re-generate them manually and simplifies updating translations or adding new languages.
- Support both released v1.7 and in-development v1.8 [versions of dcrd and dcrwallet](https://github.com/decred/dcrdex/pull/1822).
- Code maintenance.
- ~11 client fixes and ~2 backend/internal fixes.

Ethereum support:

- Enabled [token trading](https://github.com/decred/dcrdex/pull/1622) on the UI with new wallet creation flow for token wallets that includes a step to sync the parent chain (such as Ethereum).

![](../img/202208.3.github.png)

_Image: DCRDEX layout for tablet devices._


### GoDCR

_[GoDCR](https://github.com/planetdecred/godcr) is a lightweight desktop GUI wallet with integrated staking, privacy, Politeia voting, consensus voting, and more._

- Disabled Receive, Send and Mixer pages for [watch-only wallets](https://github.com/planetdecred/godcr/pull/1051).
- Updated [wallet Settings page](https://github.com/planetdecred/godcr/pull/1036) to v2 UI design.
- Updated [top-level Settings page](https://github.com/planetdecred/godcr/pull/1035) to v2 UI design.
- Implemented [layout for treasury spending](https://github.com/planetdecred/godcr/pull/975).
- Updated [color and icon](https://github.com/planetdecred/godcr/pull/1028) on the top bar.
- Fixed crash in [proposal details](https://github.com/planetdecred/godcr/pull/1045) when parsing a specific bit of Markdown.
- Fixed [app crash](https://github.com/planetdecred/godcr/pull/1048) after wallet restore is complete.
- Fixed top bar text color in [dark mode](https://github.com/planetdecred/godcr/pull/1049).

dcrlibwallet shared library:

- Added function to save [TSpend voting policy](https://github.com/planetdecred/dcrlibwallet/pull/253) locally and in VSPs managing the tickets.
- Updated [dcrwallet](https://github.com/planetdecred/dcrlibwallet/pull/263) dependency.
- Extracted Politeia into a [standalone package](https://github.com/planetdecred/dcrlibwallet/pull/262).
- Implemented API for fetching data from [external services](https://github.com/planetdecred/dcrlibwallet/pull/255) such as the dcrdata block explorer and exchanges.

![](../img/202208.4.github.png)

_Image: New Settings design in GoDCR._


### dcrdata

_[dcrdata](https://github.com/decred/dcrdata) is an explorer for Decred blockchain and off-chain data like Politeia proposals, markets, and more._

- Dependency and toolchain [updates](https://github.com/decred/dcrdata/pull/1931).
- Fixed treasury transaction [pagination](https://github.com/decred/dcrdata/pull/1929).
- Fixed [incorrect treasury](https://github.com/decred/dcrdata/pull/1930) balance on home page.
- ~3 smaller fixes.


### decred.org

_[dcrweb](https://github.com/decred/dcrweb) is the source code for the decred.org website._

[Decred.org](https://decred.org/) has been completely overhauled as approved by stakeholders in the [D.R.E.A.M. 2: Dream Harder](https://proposals.decred.org/record/5ef57f7) proposal. New messaging is "Decred - Money Evovled".

Summary of [site changes](https://github.com/decred/dcrweb/pull/1056):

- Complete overhaul of theme and style.
- Updated messaging using strong words and simple language.
- Support and Publications sections added to [Community page](https://decred.org/community/).
- Removed `/chat` subpage (it redirected to [chat.decred.org](https://chat.decred.org)).
- Removed `/brief`, `/sustainable`, `/adaptable`, `/security`, and `/history` subpages.
- Removed legacy stakepools from the [VSP list](https://decred.org/vsp/).

Technical details:

- Site is implemented as much as possible without JavaScript. JS is used for: top navigation bar on mobile, loading VSP table, OS-specific download links on the home page.
- Previous site was built on drag-and-drop editor Webflow. The Webflow CSS has been replaced with Bootstrap.
- All site CSS (including Bootstrap) is compiled from SCSS source.
- New site does not contain any videos or Lottie animations, so all CSS/JS for those has been removed.
- Data files (`apps.yml`, `current_release.yml` and `links.yml`) consolidated to remove duplcation. All wallet links and versions now reside in one file [`wallets.yml`](https://github.com/decred/dcrweb/blob/master/src/data/wallets/wallets.yml).
- SourceSansPro font replaced with a mixture of Poppins and Inter. SourceCodePro remains the monospace font.

Other site changes:

- Updated [Matrix support](https://github.com/decred/dcrweb/pull/1060) link. Now [decred.org/matrix-support](https://decred.org/matrix-support/) redirects to #support chat room in our self-hosted Element server.
- Removed 7 [defunct exchanges and wallets](https://github.com/decred/dcrweb/pull/1059). Updated links.

![](../img/202208.5.github.png)

_Image: New decred.org design._


### Other

- Updated to [Go 1.19](https://tip.golang.org/doc/go1.19) and dropped support for 1.17 in various repos.
- Android and iOS mobile wallets have been [removed](https://bounty.decred.org/2022/08/mobile-wallets-no-longer-in-scope/) from the Bug Bounty program's scope due to lack of supporting developers.


## People

Welcome to new first-time contributors with code merged to master:

- Abirdcfly ([dcrd](https://github.com/decred/dcrd/commits?author=Abirdcfly))
- herculesbrito ([Decrediton](https://github.com/decred/decrediton/commits?author=herculesbrito))
- norwnd ([dcrd](https://github.com/decred/dcrd/commits?author=norwnd))

Decred community members [João Paulo Sant'Anna](https://www.decredmagazine.com/introducing-decred-community-member-joao-paulo-santanna/) (curator of [@DecredBR](https://twitter.com/Decred_BR)) and [Philemon](https://www.decredmagazine.com/introducing-decred-developer-philemon/) (developer in DCRDEX, dcrdata, and other projects) were interviewed by @phoenixgreen on Decred Magazine.

Community stats as of Sep 1 (compared to Aug 1):

- [Twitter](https://twitter.com/decredproject) followers: 54,751 (+445)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 12,647 (+14)
- [Matrix](https://chat.decred.org/) #general users: 714 (+7)
- [Discord](https://discord.gg/GJ2GXfz) users: 1,796 (+31)
- [Telegram](https://t.me/Decred) users: 2,884 (+111)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,640 (+10), views: 214K (+2K)


## Governance

In August the new [treasury](https://dcrdata.decred.org/treasury) received 9,219 DCR worth $294K at August's average rate of $31.93. 3,788 DCR was spent to pay contractors, worth $121K at August's rate, or $91K at July's billing rate of $23.93.

The [treasury spend transaction](https://explorer.dcrdata.org/tx/c3f990e6c43babdfb782be90ca58ca6f6f8b6bcd3da96a622aba098d4e88c012) was mined on August 27, it had 23 outputs ranging from 0.7 DCR to 1,168 DCR. The transaction was approved with 6,795 Yes votes and 0 No votes.

As of Sep 3, combined balance of [legacy](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) and [new treasury](https://dcrdata.decred.org/treasury) is 810,984 DCR (24.3 million USD at $29.95).

One proposal was published and approved in August. [D.R.E.A.M. 2: Dream Harder](https://proposals.decred.org/record/5ef57f7) was submitted by @jy-p working with @jholdstock, @jz, and @saender to produce a revised decred.org prototype site along the lines of the [D.R.E.A.M. proposal](https://proposals.decred.org/record/b243fa7) which had the best voting response (48% approval) but did not pass for the decred.org [messaging RFP](https://proposals.decred.org/record/0917c1d) which was decided in September 2020. The present proposal to deploy the new design/messaging at a cost of $7,660 ($3K of which is reserved for translations) was approved with 97% Yes votes and 59% turnout.

See Politeia Digest [issue 53](https://blockcommons.red/politeia-digest/issue053/) for more detail on the month's proposal.


## Network

**Hashrate**: August's [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&zoom=l5vqeg6f-l7pjl52i&scale=linear&bin=block&axis=time) opened at ~44 Ph/s and closed ~70 Ph/s, bottoming at 38 Ph/s and peaking at 84 Ph/s throughout the month.

![](../img/202208.6.github.png)

_Image: Hashrate recovering from the lows._

Distribution of 75 Ph/s hashrate [reported](https://poolbay.io/crypto/54/decred) by the pools on Sep 1: Poolin 65%, F2Pool 26%, BTC.com 5.5%, AntPool 3.5%, CoinMine 0.6%.

Distribution of 1,000 blocks actually [mined](https://miningpoolstats.stream/decred) by Sep 1: Poolin 61%, BTC.com 5%, CoinMine 0.7%, unknown 33%.

![](../img/202208.7.github.png)

_Image: Pool hashrate distribution._

**Staking**: [Ticket price](https://dcrdata.decred.org/charts?chart=ticket-price&zoom=l5vqeg6f-l7pjl52i&axis=time&visibility=true-true&mode=stepped) varied between 220-239 DCR, with 30-day [average](https://dcrstats.com/) at 230.2 DCR (+3.4).

The [locked amount](https://dcrdata.decred.org/charts?chart=ticket-pool-value&zoom=l5vqeg6f-l7pjl52i&scale=linear&bin=block&axis=time) was 9.22-9.39 million DCR, meaning that 63.9-65.0% of the circulating supply [participated](https://dcrdata.decred.org/charts?chart=stake-participation&zoom=l5vqeg6f-l7pjl52i&scale=linear&bin=block&axis=time) in Proof of Stake. This is a new all-time high for stake participation and ticket pool value.

**VSP**: On Sep 1, ~7,050 (-120) live tickets were managed by [listed](https://decred.org/vsp/) vspd servers. Collectively the 18 VSPs managed 17.3% of the ticket pool (-0.1%).

![](../img/202208.8.github.png)

_Image: Distribution of tickets managed by VSPs._

**Nodes**: Node versions captured by [Decred Mapper](https://nodes.jholdstock.uk/user_agents) on Sep 1 (176 total, dcrd only): v1.7.1 - 31%, v1.7.2 - 29%, v1.7.4 - 18%, v1.7.0 - 8.5%, v1.8.0 dev builds - 3%, v1.7.0 dev builds - 1%, other - 10%.

![](../img/202208.9.github.png)

_Image: dcrd node version distribution._

The share of [mixed coins](https://dcrdata.decred.org/charts?chart=coin-supply&zoom=jz3q237o-la8vk000&scale=linear&bin=day&axis=time&visibility=true-true-true) varied between 60.8-60.9%. Daily [mixed amount](https://dcrdata.decred.org/charts?chart=privacy-participation&zoom=l5vqeg6f-l7pjl52i&bin=day&axis=time) varied between 233-546K DCR.

Decred's [Lightning Network](https://ln-map.jholdstock.uk/) has seen 42 nodes (-3), 68 channels (-10) with a total capacity of 35.4 DCR (-1.5), as of Sep 1.


## Ecosystem

VSP [synergy-crypto.net](https://vspd.synergy-crypto.net/) announced on its website that it is closing and is not accepting new tickets. Tickets with already paid fees will be voted as usual (180 tickets as of Sep 1).

ViaBTC [announced](https://support.viabtc.com/hc/en-us/articles/9197412971417-Announcement-on-Putting-Offline-DCR-Mining-Pool) on Aug 5 that they will shut down their DCR mining pool on Aug 10. Users were asked to withdraw or convert their DCR by Aug 17, and any DCR remaining by that deadline will be automatically converted to USDT.

A total of 7 defunct services have been [removed](https://github.com/decred/dcrweb/pull/1059) from decred.org [Exchanges page](https://decred.org/exchanges/) ([CoinSwitch](https://coinswitch.co/), [Sequoir](https://www.sequoir.com/) (ex Vertbase), [Evercoin](https://evercoin.com/home), [Bitcoin.com](https://exchange.bitcoin.com/)) and [Wallets page](https://decred.org/wallets/) ([Ownbit](https://ownbit.io/), [AnyBit](https://www.anybit.io/), [Atomic Wallet](https://atomicwallet.io/), [Evercoin](https://evercoin.com/)). As of Sep 12, 22 third-party exchanges and 6 third-party wallets remain listed.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

Join our [#ecosystem](https://chat.decred.org/#/room/#ecosystem:decred.org) chat to follow Decred ecosystem updates.


## Outreach

Monde PR's achievements:

- Pitched Decred to 2 PR opportunities.
- Responded to 3 requests for comments.

Secured the following news articles:

- An article in [Forbes Advisor](https://www.forbes.com/advisor/investing/cryptocurrency/what-are-meme-coins-are-they-worth-investing-in/) featuring commentary from @jz on the merit of meme coins. The piece was syndicated to 3 publications including [Nasdaq](https://www.nasdaq.com/articles/what-are-meme-coins-are-they-worth-investing-in).
- An article in [Cointelegraph](https://cointelegraph.com/news/bitcoin-lightning-network-vs-visa-and-mastercard-how-do-they-stack-up) featuring commentary from @jy-p on how Bitcoin's Lightning Network stacks up against Solana and Visa. The piece was syndicated to 30 publications including [Bitcoin Insider](https://www.bitcoininsider.org/article/181590/bitcoin-lightning-network-vs-visa-and-mastercard-how-do-they-stack) and [Crypto News Canada](https://cryptonewscanada.com/bitcoin-lightning-network-vs-visa-and-mastercard-how-do-they-stack-up/).
- The Cointelegraph piece also appeared in Portuguese on [Cointelegraph Brazil](https://cointelegraph.com.br/news/bitcoin-lightning-network-vs-visa-and-mastercard-how-do-they-stack-up).


## Media

Decred Magazine engagement stats for August:

- Total number of articles on DM: 305
- Newsletter subscribers: 55
- New posts and newsletters sent: 13
- Active social media campaigns: 5
- Social media posts: 75
- Post clicks: 224
- Likes: 412
- Re-tweets: 73
- Social media followers across all platforms and accounts: 927

Twitter users are more than welcome to support [@Decredmagazine](https://twitter.com/decredmagazine) with follows, likes and retweets to help spread the message.

**Selected articles:**

- [Introducing Decred community member João Paulo Sant'Anna](https://www.decredmagazine.com/introducing-decred-community-member-joao-paulo-santanna/) by @phoenixgreen
- [Introducing Decred developer Philemon](https://www.decredmagazine.com/introducing-decred-developer-philemon/) by @phoenixgreen
- [How Decred contributed to a more transparent election in Brazil](https://www.decredmagazine.com/how-decred-how-decred-contributed-to-a-more-transparent-election-in-brazil/) by @João
- [Peer-to-peer electronic corporation](https://www.decredmagazine.com/peer-to-peer-electronic-corporation/) by @Tivra
- [Inflection points](https://www.decredmagazine.com/inflection-points/) technical analysis by @Applesaucesome

**Videos:**

- [Decentralised treasury spending - Decred Fundamentals](https://www.youtube.com/watch?v=A0NR5ySIqoI) by @phoenixgreen
- [DCRDATA Decred's treasury - Decred Fundamentals](https://www.youtube.com/watch?v=lQebfO6qIoo) by @phoenixgreen
- [Why Decred will explode! $DCR crypto price prediction!](https://www.youtube.com/watch?v=0PerKqUmmfU) by Minted Max - better than a typical price talk video
- [Decred and the future of web3 - State of the Market with BlockchainBuck](https://www.youtube.com/watch?v=n3welZEDchU) by @phoenixgreen and @Exitus
- [Decred News Update - Development work surging across many repos - LN, DCRDEX, Politeia, DAO & more](https://www.youtube.com/watch?v=EPcUkmaaJlQ) by @Exitus

**Art and fun:**

- [New Website TikTok](https://twitter.com/exitusdcr/status/1565090356651237379) by @DCRDajana
- [Decred Heartbeat](https://www.decredmagazine.com/decred-heartbeat/) by @OfficialCryptos

**Translations:**

- Decred Journal April-July 2022 got a total of 6 new [translations](https://xaur.github.io/decred-news/). Thanks to @arij (Arabic), @Dominic (Chinese), and @kozel (Polish)!

**Non-English content:**

- [What is the Decred digital token project?](https://www.youtube.com/watch?v=B8Y3-z9Bs9A) by Be Coin (Arabic)
- [DCR DecreD Explose j'achete ou pas?](https://www.youtube.com/watch?v=6cWhwYQ9tbE) by Crypto for EveryOne (French, "Decred exploding, buy or not?")


## Discussions

Selected Reddit posts:

- [Can something like Tornado Cash ban happen to Decred?](https://www.reddit.com/r/decred/comments/x2c7u5/can_something_like_tornado_cash_ban_happen_to/)

Selected Twitter discussions:

- @elima\_iii has a draft of his research paper, which focuses on [Decred and the proposed Responsible Financial Innovation Act](https://twitter.com/elima_iii/status/1563655328209723404).
- @phoenixgreen has a [thread on his experiences using the DCRDEX](https://twitter.com/DecredSociety/status/1564625492795441153) to sell DCR for BTC using the platform's atomic-swap technology.


## Markets

In August DCR was trading between USD 25.60-70.40 / BTC 0.00114-0.00306. The average daily rate was $31.93.

Another [review](https://www.decredmagazine.com/inflection-points/) of crypto and stock markets by @Applesaucesome mentions unusual numbers in August's DCR pump:

![](../img/202208.10.github.png)

> The volume of that candle was massive. And I mean MASSIVE. Just on the DCR/USDT pairing there was nearly 2 million DCR traded back and forth. That's 14% of the entire supply. Note: This doesn't mean that much was bought or sold but the total combined amount bought + sold.

*The following quote is not financial advice:*

> In conclusion, the markets are likely going to pull back but if you're a bull then it could present one last solid buying opportunity. If you're a bear then this would be the time to sell more. Crypto still looks terrible right now but I'm not selling.

![](../img/202208.11.github.png)

_Image: DCRDEX monthly volume in USD._


## Relevant External

Tornado Cash, an Ethereum mixing service, was added to the OFAC sanctions list by the [US Treasury](https://home.treasury.gov/news/press-releases/jy0916), for its role in facilitating the laundering of proceeds of hacks by North Korea. The sanctions cover a set of Ethereum addresses associated with the mixer, and in the immediate aftermath of the sanctions being unveiled some trolls were [sending](https://www.coindesk.com/policy/2022/08/09/someone-is-trolling-celebs-by-sending-eth-from-tornado-cash/) small amounts of mixed ETH from Tornado to the wallets of celebrities to taint their funds. Circle quickly [blacklisted](https://twitter.com/bantg/status/1556712790894706688) $75K of USDC belonging to Tornado users. GitHub [removed](https://www.theregister.com/2022/08/10/github_tornado_cookies/) the repositories for Tornado Cash and also the accounts of at least 3 developers who worked on it.

Two days later a developer who worked on Tornado Cash, Alexey Pertsev, was [arrested](https://www.fiod.nl/arrest-of-suspected-developer-of-tornado-cash/) in Amsterdam by the Dutch Fiscal Information and Investigation Service, on suspicion of helping to facilitate money laundering. The Dutch authorities are holding Pertsev for 3 months until a trial can be arranged, but so far they have not been charged with a specific crime, and their wife has [denied links](https://www.coindesk.com/policy/2022/08/26/wife-of-pertsev-arrested-tornado-cash-developer-denies-russia-secret-service-links/) to Russian espionage.

A whole DeFi ecosystem on Solana (Saber protocol) was [revealed](https://www.coindesk.com/layer2/2022/08/04/master-of-anons-how-a-crypto-developer-faked-a-defi-ecosystem/) to be the work of two brothers, a lot of fake developer accounts, and some techniques for double or triple counting the assets locked into the protocol.

Maker DAO has been supporting the DAI stablecoin since launch in 2019 and its governance serves to determine how the MKR ecosystem develops. Most participants in Maker DAO governance seem to agree that it is not going well and needs to change, but there are disagreements about how it should change. In a recent [podcast debade](ttps://www.youtube.com/watch?v=UJ_kfHdCLUk) MKR founder Rune Christensen made a case that people working for the DAO were getting too comfortable and trying to expand the organisation in ways which suited themselves. Hasu (pseudonymous crypto researcher, MKR governance delegate) represented the side of DAO contributors who could see that MKR holders were being presented with sub-optimal proposal decisions which they were not always well suited to answer - but several proposals to create new core groups which would provide a certain kind of intelligence to the token holders were recently rejected. One [Twitter thread](https://twitter.com/g_dip/status/1564716178819653632) on the subject adds a 3rd faction, decentralization maximalists who want to see the smart contracts locked down or "ossified" so that they cannot be changed in response to changing regulation. Rune is however the main character whose return from semi-retirement heralded a change in direction away from what the DAO's contributors and in some cases VC backers were planning. Rune has provided an epic "End Game" plan but it is extremely long and complex, split into several long forum posts, so it's not clear how many people support that.

[Leaked videos](https://cryptoleaks.info/case-no-3) have been circulated of lawyer Kyle Roche bragging about their work with Ava Labs (of Avalanche network), which included tying other competing projects up with frivolous lawsuits. Ava labs have [denied](https://www.coindesk.com/business/2022/08/29/obvious-nonsense-prominent-blockchains-founder-dismisses-smear-campaign-allegation/) the sensational account of their arrangement with the firm which Crypto Leaks published, and Kyle Roche has [withdrawn](https://www.coindesk.com/business/2022/08/31/crypto-lawyer-kyle-roche-withdraws-from-tether-bitfinex-tron-and-bitmex-lawsuits-after-cryptoleaks-scandal/) from a number of the aforementioned class action lawsuits.

That's all for August. Share your updates for the next issue in our [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat room.


## About

This is issue 50 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from the source after a minimal sanity check. The authors of the Decred Journal cannot verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing, editing, publishing: bee, bochinchero, Exitus, jz, l1ndseymm, phoenixgreen, richardred
- reviews and feedback: davecgh
- funding: Decred stakeholders
