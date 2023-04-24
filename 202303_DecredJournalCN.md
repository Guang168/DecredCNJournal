# Decred 月报 – 2023 年 3 月

![](img/202303.1.768.png)

_图片: @Exitus_

三月亮点：

- 提出并批准了一项提案，将区块补贴从 10/80 PoW/PoS 更改为 1/89，并更改算法用以排除现有ASIC。

- Bison Relay v0.1.5 已发布，v0.1.6 RC1 也已发布。

- DCRDEX 0.6 正在进行 Beta 测试，发布候选版本。

- Decred月报 是本月批准的四项提案之一，其它三项是针对 DCRDEX 开发的特定方面。

内容：

- [更改 PoW 算法并减少 PoW 奖励的提案](#proposal-to-change-pow-algorithm-and-reduce-pow-rewards)
- [Bison Relay v0.1.6 候选发布版](#bison-relay-v016-release-candidate)
- [开发进展总结](#development)
- [人员](#people)
- [治理](#governance)
- [网络](#network)
- [生态系统](#ecosystem)
- [外展](#outreach)
- [活动](#events)
- [媒体](#media)
- [市场](#markets)
- [相关外部信息](#relevant-external)


## 更改 PoW 算法并减少 PoW 奖励的提案

Decred 的共识和经济学正在发生重大变化。新提案将进一步将奖励的工作量证明份额从 10% 减少到 1%，将权益证明奖励从 80% 增加到 89%，并将挖矿算法从 BLAKE-256 更改为 BLAKE3。这将从网络中删除所有当前正在挖掘的 ASIC 硬件，目的是修复 DCR 的价格发现。在撰写本文时，该提案已获得批准。下一步将是在代码中实施新的共识规则，发布新版本的核心软件，让网络安装它并让利益相关者投票激活新规则。所有这一切应该需要几个月的时间，并且在 Decred 的[官方渠道](https://decred.org/community/)上会有更多关于每个阶段的交流。


## Bison Relay v0.1.6 候选发布版

三月份发布了两个版本，重点是改善群聊体验。

v0.1.5 版本亮点：

- 新的付款统计页面
- 存款地址二维码
- 改进错误信息
- 修复群聊成员列表不同步的问题
- 固定群聊消息排序
- 其他错误修复和用户界面调整

v0.1.6 Release Candidate 1 的亮点：

- 支持多个管理员的新版群聊
- 新消息的侧边栏通知
- 捆绑在邀请文件中的自动群聊邀请
- 突出显示带有用户昵称的消息
- 更明显的新帖子按钮
- 所有帖子评论都指向原始帖子，对中继副本的评论被禁用
- GUI 和 CLI 应用程序中的许多错误修复和 UI 改进

在 [GitHub](https://github.com/companyzero/bisonrelay/releases) 上获取最新版本的二进制文件（截至在 bisonrelay.org 上编写 [下载页面](https://bisonrelay.org/download/) 仍然 显示 v0.1.4)。 欢迎在 [GitHub 问题跟踪器](https://github.com/companyzero/bisonrelay/issues) 和 [#br 聊天](https://chat.decred.org/#/room/#br:decred.org）在 Matrix 或 Bison Relay 本身上。


## 开发进展总结

除非另有说明，否则下面报告的工作为“合并至核心存储库”状态。这意味着该工作已完成、审查并集成到高级用户可以[构建和运行](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c)的源代码中，但普通用户尚不可用。


### dcrd

_[dcrd](https://github.com/decred/dcrd) 是一个完整的节点实现，为 Decred 在全球的点对点网络提供支持。_

从 [上个月](202302.md#dcrd) 开始继续强化共识更改投票代码：

- 增强了部署参数的启动[验证](https://github.com/decred/dcrd/pull/3068)，以确保它们满足计票逻辑所依赖的假设。 例如，它检查每张选票是否恰好有一张弃权票和一张否决票，没有重复的投票选择，以及选择是否以位正确编码。 这允许优化和简化与计票相关的代码。
- 添加验证以确保共识更改投票参数 [不要使用特殊位](https://github.com/decred/dcrd/pull/3073) 保留用于批准或不批准前一个块。
- 添加验证以确保同一投票批次中不同投票使用的位 [不重叠](https://github.com/decred/dcrd/pull/3077)。
- 添加了使用 [空 ID](https://github.com/decred/dcrd/pull/3079) 拒绝投票选择的验证。 ID 是总结投票选择含义的短字符串，它们通常是“是”、“否”或“弃权”。
- 重新编写代码确定共识 [投票阶段和计票](https://github.com/decred/dcrd/pull/3069) 逻辑以优化它并使其更容易推理。
- 更改了获胜共识投票选择的内部表示，以提高可读性并防止 [滥用](https://github.com/decred/dcrd/pull/3080) 此代码。
- 重新编写了 [共识投票处理](https://github.com/decred/dcrd/pull/3075) 代码的测试，使它们更易于理解，测试更多的边缘案例，并 [更可靠](https://github.com/decred/dcrd/pull/3076)。
- 请注意，上述更改不会以任何方式破坏版本之间的共识，它们添加了更多检查，如果 dcrd 检测到共识代码所做的任何假设被违反，则允许它提前失败。

其他变化：

- 如果被查询的对等节点断开连接，则重新请求块和交易[更快](https://github.com/decred/dcrd/pull/3067)。 不再等待此数据稍后再次公布，而是立即从已知拥有该数据的对等方请求该数据。
- 修复了其他同行的[已知库存](https://github.com/decred/dcrd/pull/3074) 的缓存。 这是一个非常小的错误，可能会导致比绝对必要的流量略高的流量。
- 重构和 [构建配置](https://github.com/decred/dcrd/pull/3081) 更新。


### dcrwallet

_[dcrwallet](https://github.com/decred/dcrwallet) 是命令行和图形界面钱包应用程序使用的钱包服务器。_

- 删除了使用带余额的自动购票时不必要的[余额计算](https://github.com/decred/dcrwallet/pull/2203)以保持未设置或为零。 在较繁忙的钱包上，这会显着提高性能。
- 迁移到 [vspd](https://github.com/decred/vspd) 存储库提供的 [VSP 客户端](https://github.com/decred/dcrwallet/pull/2213)。 它主要是从 dcrwallet 借来的相同代码，但是将 VSP 代码合并到一个地方允许删除可能不同步的重复，例如错误代码、数据结构等。
- 修复了 SPV 模式下的 [数据竞争](https://github.com/decred/dcrwallet/pull/2210)。
- 修复了由于票价变化而取消购票请求时可能[丢失相关交易](https://github.com/decred/dcrwallet/pull/2212)的问题。


### Decrediton

_[Decrediton](https://github.com/decred/decrediton) 是一款功能齐全的桌面钱包应用程序，集成了投票、StakeShuffle 混币、闪电网络、DEX 交易等功能。 它在有或没有完整的区块链（SPV 模式）的情况下运行。_

进行中：

- Decrediton [Ledger 集成](https://github.com/JoeGruffins/ledger-decred-poc) 工作已由@JoeGruff 启动，并带有初始[概念证明](https://github.com/JoeGruffins/ledger-decred-poc) 和后续 [提案](https://proposals.decred.org/record/609db9e) 以使其做好生产准备。 目前用户需要使用 Ledger Live 软件从他们的 Ledger 设备发送/接收 DCR，但历史上存在太多[技术问题](https://matrix.to/#/!MYLcxlwzxwViTaFPGo:decred.org/$fxDMmKpCE-Edb1fRQyhyy_Rjlx2HuKNGtpwSmC76nIA?via=decred.org&via=matrix.org&via=planetdecred.org) 使用该软件。 在 Decrediton 中直接拥有 Ledger 支持将给 DCR 持有者一个更好的选择。

其它:

- 使用 Decrediton + Trezor 质押 DCR 再次被[阻止](https://github.com/decred/decrediton/issues/2681#issuecomment-1366432017) 固件所需的更改。 修复已于 12 月[提交](https://github.com/trezor/trezor-firmware/pull/2703) 到 Trezor 固件存储库，但尚未审查或合并。


### vspd

_[vspd](https://github.com/decred/vspd) is server software used by Voting Service Providers. A VSP votes on behalf of its users 24/7 and cannot steal funds._

Changes to make vspd code easier to consume by other software (such as dcrwallet):

- Removed ability to [override server signature validation](https://github.com/decred/vspd/pull/372) with a custom function. This feature was added to facilitate testing but turned out to be unnecessary and make the VSP client library harder to consume.
- Removed the need to [convert errors](https://github.com/decred/vspd/pull/374) in the calling code. This was required to bump the major version of the module to v2.

Other changes:

- Added [rate limiting](https://github.com/decred/vspd/pull/373) of admin login requests (max 3 attempts per second) and a sample Nginx config to support it.
- Added new [development tool](https://github.com/decred/vspd/pull/366) for testing various steps of the VSP protocol: create VSP fee transaction, send it to the VSP, query ticket status, and change ticket's vote choices. VSP operators can use this tool to verify that their VSP works correctly.
- Increased test coverage.


### dcrpool

_[dcrpool](https://github.com/decred/dcrpool) is server software for running a mining pool._

- Updated to [Go 1.18](https://github.com/decred/dcrpool/pull/338).


### Lightning Network

_[dcrlnd](https://github.com/decred/dcrlnd) is Decred's Lightning Network node software. LN enables instant and low-cost transactions._

- Upgraded to build and test against [Go 1.20](https://github.com/decred/dcrlnd/pull/176).
- Updated [dependencies](https://github.com/decred/dcrlnd/pull/177).

[LN Liquidity Provider](https://github.com/decred/dcrlnlpd) (LP):

- Added client-side [sanity checks](https://github.com/decred/dcrlnlpd/pull/9) to fail earlier when it is not possible to get an inbound channel from the LP. The client will use server's policy to determine if the server can create a channel of the desired size, and if the client will be able to pay for it. This makes it possible to avoid fetching an invoice that will not be paid.
- Capacity to [configure](https://github.com/decred/dcrlnlpd/pull/9) LP server's invoice expiration policy. Invoices are generated by the server to collect fees for opening LN channels to clients. Server operator can now configure how long invoices are valid for, and how long clients must wait before requesting a new invoice.
- Updated [dependencies](https://github.com/decred/dcrlnlpd/pull/10).

LN Liquidity Provider is software that takes control of a normal LN node and adds one useful feature to it: client software can ask the LP to open a channel back to the client. This gives the client additional inbound capacity and allows them to receive more funds over the Lightning Network. In return the LP operator collects a small fee for the service.

Bison Relay is a major user of Decred's Lightning Network and benefits from improvements in both the base LN software and the Liquidity Provider.


### cspp

_[cspp](https://github.com/decred/cspp) is a server for coordinating coin mixes using the CoinShuffle++ protocol. It is non-custodial, i.e. never holds any funds. CSPP is part of StakeShuffle, Decreds privacy system._

- Updated [Go dependencies](https://github.com/decred/cspp/pull/89).


### DCRDEX

_[DCRDEX](https://github.com/decred/dcrdex) is a non-custodial, privacy-respecting exchange for trustless trading, powered by atomic swaps._

Internal pre-release testing of the big v0.6 release has started with one beta and two release candidates [tagged](https://github.com/decred/dcrdex/tags) in March. All changes reported below will be included in the v0.6 release.

Client changes:

- Removed [default Bitcoin node](https://github.com/decred/dcrdex/pull/2193) for getting compact block filters in SPV mode. It was added when there were few public Bitcoin full nodes supporting [BIP-157](https://bitcoin.stackexchange.com/questions/86231/whats-the-distinction-between-bip-157-and-bip-158-are-they-supported-by-bitcoi/86232#86232). Now there are plenty and removing the default one may improve connectivity because it is often overloaded.
- Improved error message when database [failed to initialize](https://github.com/decred/dcrdex/pull/2205), most commonly when attempting to start a second instance of dexc.

Client fixes:

- Fixed empty [gaps between candles](https://github.com/decred/dcrdex/pull/2195) on the price chart.
- Fixed inconsistent decimal [precision](https://github.com/decred/dcrdex/pull/2208) on different UI elements.
- Fixed [price](https://github.com/decred/dcrdex/pull/2214) not being updated in some places.
- Fixed reorg indication for [DCR](https://github.com/decred/dcrdex/pull/2219) and [BTC](https://github.com/decred/dcrdex/pull/2225) in SPV mode to match dcrd and dcrwallet. Specifically, blocks that are not on the main chain ("orphaned" blocks) will be reported as having "-1" confirmations.
- Fixed [wallet birthday](https://github.com/decred/dcrdex/pull/2236) showing UTC date instead of system's local date.
- Fixed ~5 other UI bugs and ~1 concurrency bugs.

Ethereum, client:

- Improved handling of poor connections to RPC providers while the DEX client is [shutting down](https://github.com/decred/dcrdex/pull/2191).
- Added [Ethereum wallet guide](https://github.com/decred/dcrdex/pull/2233) wiki page.
- Added a 20% buffer to the [fee estimates](https://github.com/decred/dcrdex/pull/2234) ensure sending ETH will succeed even if network's base fee jumps right before sending.
- Updated to [Geth v1.11](https://github.com/decred/dcrdex/pull/2238). This is required for the Shanghai network upgrade scheduled on April 12, 2023.
- Fixed token's [parent asset balance](https://github.com/decred/dcrdex/pull/2201) not being updated when cancelling an order involving that token.
- Fixed [unconfirmed transactions](https://github.com/decred/dcrdex/pull/2211) not being reflected in the available balance.
- Fixed error messages.

Ethereum, server:

- Allow server operators to rank RPC provider endpoints by [priority](https://github.com/decred/dcrdex/pull/2199) in the config file. The healthy connection with the highest priority will always be attempted first.

Fidelity bonds:

- [UI updates](https://github.com/decred/dcrdex/pull/2200) to replace registration fees with bonds, including integration of bonds into account import and export flows. Different cases are considered when restoring from same or new app seed, and when using existing or creating new DEX account.
- Implemented bonds funding [with BTC](https://github.com/decred/dcrdex/pull/2196) in both the client and the server. It will be possible to switch bonds to use a different asset, e.g. from DCR to BTC.

Other changes:

- Added more strict server-side [checks](https://github.com/decred/dcrdex/pull/2248) for addresses used in swaps.
- Updated [LTC dependencies](https://github.com/decred/dcrdex/pull/2268) to pull in a [critical fix](https://github.com/ltcsuite/ltcd/pull/25) for handling large transactions.
- Improvements in test infrastructure, build scripts, dependency updates.

Client changes on `master` towards the next release (likely v0.6.1):

- Notify the user about [unstable connection](https://github.com/decred/dcrdex/pull/2028).
- Fixed error when [failing to subscribe](https://github.com/decred/dcrdex/pull/2252) to new header notifications from Ethereum RPC provider.

Other stuff:

- DCRDEX was [rejected](https://github.com/getumbrel/umbrel-apps/pull/430#issuecomment-1452436145) in the official Umbrel App Store because "for crypto-related apps, we're exclusively accepting apps that solely focus on bitcoin". Two weeks later they [tweeted](https://twitter.com/umbrel/status/1636068336101621760) that censoring developers is anti-free market, which surprised some community members in context of the rejection. DCRDEX can still be installed via Umbrel by adding DEX'es own [Community App Store](https://github.com/decred/umbrel-app-store). The difference is it requires more manual steps and exposes DCRDEX to fewer users compared to the central official Umbrel App Store.
- First mainnet swaps with DigiByte (DGB) have been [spotted](https://twitter.com/DigiByteCoin/status/1640820963532214273) on Twitter.

![](../img/202303.2.930.png)

_Image: UI updates in DCRDEX to replace registration fees with time-locked bonds. UI design is a work in progress. DCR amounts shown are not real._


### dcrdata

_[dcrdata](https://github.com/decred/dcrdata) is an explorer for Decred blockchain and off-chain data like Politeia proposals, markets, and more._

- Added an [allowed hosts](https://github.com/decred/dcrdata/pull/1958) middleware to ensure that any `Host` value set in the request header is on a whitelist of hosts. This prevents invalid or unexpected `Host` values even if dcrdata is deployed without Nginx, which normally takes care of it.
- Updated Decred and third party [Node.js modules](https://github.com/decred/dcrdata/pull/1952) and Go [dependencies](https://github.com/decred/dcrdata/pull/1959) to their latest versions, and moved builds to Go 1.19 and 1.20.


### Documentation

_[dcrdocs](https://github.com/decred/dcrdocs) is the source code for Decred [user documentation](https://docs.decred.org/)._

- Added [syntax highlighting](https://github.com/decred/dcrdocs/pull/1219) to fix issues with hard to read code syntax, particularly in dark mode.
- Updated [PoS reward](https://github.com/decred/dcrdocs/pull/1220) numbers (30% to 80%) in the proof-of-stake [Overview page](https://docs.decred.org/proof-of-stake/overview/).
- Added a [glossary entry](https://github.com/decred/dcrdocs/pull/1217) for "Redeem Script".
- Updated [VSP staking information](https://github.com/decred/dcrdocs/pull/1217) on multiple pages. This includes removing most references to Redeem Scripts, removing "legacy" staking instructions, and simplifying the remaining staking instructions.
- Consolidated the [pros and cons](https://github.com/decred/dcrdocs/pull/1217) of using VSP and solo staking.
- Added a [note](https://github.com/decred/dcrdocs/pull/1217) to the Redeem Script page indicating they are no longer relevant.
- The [Buying Tickets With dcrwallet](https://github.com/decred/dcrdocs/pull/1217) page has been optimized. It now clearly separates Purchasing and Voting tickets in two steps and removes any references to the outdated dcrstakepool system.
- Optimized [Docker build](https://github.com/decred/dcrdocs/pull/1222): switched to much smaller image based on Alpine Linux, fixed MIME type for RSS feeds, and updated scripts to fail on error.


### Dev Docs

_[dcrdevdocs](https://github.com/decred/dcrdevdocs) is the source code for Decred [developer documentation](https://devdocs.decred.org/)._

- Upgraded to [MkDocs Material 9](https://github.com/decred/dcrdevdocs/pull/108) with improved search. Also upgraded to Python 3.11, Nginx 1.22, and optimized the Docker build.


### decred.org

_[dcrweb](https://github.com/decred/dcrweb) is the source code for the [decred.org](https://decred.org/) website._

Changes to the [News page](https://github.com/decred/dcrweb/pull/1106):

- A more readable news outlet name is now displayed instead of website's domain name.
- Outlet and author are no longer displayed for software releases.


### Bison Relay

_[Bison Relay](https://github.com/companyzero/bisonrelay) is a new social media platform with strong protections against censorship, surveillance, and advertising, powered by Decred Lightning Network._

End user binaries have been released for Bison Relay v0.1.5 with all changes and fixes we reported in the [February issue](202302.md#bison-relay). Just one week later v0.1.6 Release Candidate 1 became available for download. Below are all changes in v0.1.6 RC1 and v0.1.6 final. The latter added very minor fixes and no binaries have been made for it.

Common changes in GUI and CLI apps in v0.1.6:

- Implemented [new version of group chats](https://github.com/companyzero/bisonrelay/pull/155) that introduces support for multiple admins. Admins can invite or remove members, and assign or revoke admin privileges. The permission to kill the group chat is still only possible by the special Owner role. Existing group chats will have an option to upgrade to new version.
- Improved error handling and logging of [failed payments](https://github.com/companyzero/bisonrelay/pull/156) (such as tipping).
- Improved help text for [adding LN receive capacity](https://github.com/companyzero/bisonrelay/pull/166).
- Disallow comments on [relayed posts](https://github.com/companyzero/bisonrelay/pull/162). Commenting on posts will require a key exchange with the original author. Also, once the original post is received from the author, all relayed copies will be removed in favor of the original.
- Fixed bug preventing to accept [multiple group chat invites](https://github.com/companyzero/bisonrelay/pull/154) at the same time.
- Dependency updates and internal refactoring.

GUI app changes in v0.1.6:

- Added sidebar notification icon for [new chat messages](https://github.com/companyzero/bisonrelay/pull/157).
- Show [unread count](https://github.com/companyzero/bisonrelay/pull/157) as "1k+" when it is over 1,000.
- Avoid redundant [last read indicator](https://github.com/companyzero/bisonrelay/pull/157) when there are no previous messages in the chat.
- Added a prominent [New Post](https://github.com/companyzero/bisonrelay/pull/159) button that is easy to access from different views.
- Added [highlighting of messages](https://github.com/companyzero/bisonrelay/pull/164) that include user's nick.
- Added [seed verification step](https://github.com/companyzero/bisonrelay/pull/174) where user is required to answer questions about their seed.
- Added [About page](https://github.com/companyzero/bisonrelay/pull/175) with app version and copyright info.
- Fixed segfault error [on close](https://github.com/companyzero/bisonrelay/pull/157).
- Fixed errors when [leaving or killing](https://github.com/companyzero/bisonrelay/pull/170) group chats.
- Smaller UI tweaks and fixes.

CLI app changes in v0.1.6:

- Added [autocompletion](https://github.com/companyzero/bisonrelay/pull/163) of user names and group chat names to various commands.
- Added [Alt+V](https://github.com/companyzero/bisonrelay/pull/153) as a Paste hotkey.
- Added a command to decode and inspect [LN invoices](https://github.com/companyzero/bisonrelay/pull/166), improved logging of LN events (such as channel opened or closed).
- Display invite to group chat in a [private chat](https://github.com/companyzero/bisonrelay/pull/169) with the inviting user.
- Added an option to include a [group chat invite](https://github.com/companyzero/bisonrelay/pull/178) in an invite file. Invite recipient will be invited to group chat automatically after completing the initial key exchange with invite author.
- Fixed [wrapping](https://github.com/companyzero/bisonrelay/pull/153) of multi-line text.

`clientrpc` [automation API](https://github.com/companyzero/bisonrelay/tree/master/clientrpc) changes in v0.1.6:

- Improved [cancellation and shutdown](https://github.com/companyzero/bisonrelay/issues/158) handling of the read loop.
- Added methods for [managing group chats](https://github.com/companyzero/bisonrelay/pull/161) and [sending files](https://github.com/companyzero/bisonrelay/pull/179).
- Fixed [reading](https://github.com/companyzero/bisonrelay/pull/161) from the message replay log file.

Other stuff and what to expect:

- Image attachments are now delivered between Bison Relay and Matrix in both directions.
- Prepaid invites have been [announced](https://twitter.com/behindtext/status/1641080004778897408), they will help to onboard new users without requiring them to obtain DCR externally and fund their Bison Relay wallet.
- Next important [milestone](https://matrix.to/#/!aNnAOHkWUdNcEXRGjJ:decred.org/$oCz1kQZLJ_wc4Wwjq6z8x8numCsuZWyy7IyPWw3vDIA?via=decred.org&via=matrix.org&via=planetdecred.org) is prepaid group chat invites, which combine prepaid invites and bundled group chat invites.
- The tech behind Bison Relay GUI (Flutter) provides infrastructure to build mobile apps from the same codebase. Effort is still required to adjust the UI/UX to fit the mobile platform and fix the edge cases specific to mobile, but it's much easier compared to building mobile apps from scratch in native Android and iOS stacks.
- In the medium term developers plan to add pages and storefronts which will take quite some work to implement.


### Other

- Decred Bug Bounty [website](https://bounty.decred.org/): added [email templates](https://github.com/decred/dcrbounty/pull/95), optimized [Docker builds](https://github.com/decred/dcrbounty/pull/96), and [added](https://github.com/decred/dcrbounty/pull/94) Tanvir0x1 to Hall of Fame.
- Multiple websites updated to use latest Hugo site generator.


## People

Community stats as of Apr 3 (compared to Mar 1):

- [Twitter](https://twitter.com/decredproject) followers: 53,189 (+125)
- [Reddit](https://www.reddit.com/r/decred/) subscribers: 12,678 (+18)
- [Matrix](https://chat.decred.org/) #general users: 761 (+11)
- [Discord](https://discord.gg/GJ2GXfz) users: 1,556 (-1), verified to post: 923 (-9)
- [Telegram](https://t.me/Decred) users: 2,619 (-137)
- [YouTube](https://www.youtube.com/decredchannel) subscribers: 4,630 (+0), views: 226.5K (+1.9K)


## Governance

In March the new [treasury](https://dcrdata.decred.org/treasury) received 8,388 DCR worth $174K at March's average rate of $20.69. 4,271 DCR was spent to pay contractors, worth $88K at March's rate.

A [treasury spend tx](https://explorer.dcrdata.org/tx/57c226c50632baf64aa3bb366e11c586c38689248a067b4642173a6a96fd47d0) was mined on March 13, it had 27 outputs making payments to contractors, ranging from 2.7 DCR to 1,264 DCR. At January's billing rate of $22.05 the TSpend is equivalent to $94K.

As of Apr 13, combined balance of [legacy](https://dcrdata.decred.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx) and [new treasury](https://dcrdata.decred.org/treasury) is 852,332 DCR (17.8 million USD at $20.90).

There were 7 proposals submitted in March:

- The Decred Journal and Politeia Digest [proposal](https://proposals.decred.org/record/9e68dca) requested a budget of $40,000 and was approved with 86% Yes votes and turnout of 46%.

- There were 3 proposals from the Decred DEX team which were all approved. The main [proposal](https://proposals.decred.org/record/ca6b749) for client development asked for a budget of $182,000 and was approved with 94% Yes votes and 49% turnout. A [proposal](https://proposals.decred.org/record/ae7c4fe) to fund work on packaging the DEX software as a desktop app was funded with a budget of $29,000, 91% approval from 43% turnout. A [proposal](https://proposals.decred.org/record/8b1ceda) to fund development of a market maker and arbitrage bot was funded with a budget of $73,000, gaining 89% approval from the 42% of tickets that voted.

- A [proposal](https://proposals.decred.org/record/ff64137) from Cointelegraph for $50,000 worth of content was rejected with 41% Yes votes from turnout of 51%.

- A [proposal](https://proposals.decred.org/record/a8501bc) from @jy-p to change the PoW/PoS subsidy split to 1/89 and also change the PoW algorithm to BLAKE3, removing ASIC hardware designed to mine DCR from the network.

- A [proposal](https://proposals.decred.org/record/609db9e) from @joegruff to develop Decrediton support for Ledger hardware at a cost of $20,500.

See Politeia Digest [issue 57](https://blockcommons.red/politeia-digest/issue057/) and [issue 58](https://blockcommons.red/politeia-digest/issue058/) for more details on the month's proposals.

Politeia Digest is available on: [Block Commons](https://blockcommons.red/politeia-digest/), [Decred Magazine](https://www.decredmagazine.com/tag/politeia-digest/), [Medium](https://medium.com/politeia-digest), and [GitHub](https://github.com/RichardRed0x/politeia-digest).


## Network

**Hashrate**: March's [hashrate](https://dcrdata.decred.org/charts?chart=hashrate&scale=linear&bin=day&axis=time) opened at ~71 Ph/s and closed ~73 Ph/s, bottoming at 64 Ph/s and peaking at 83 Ph/s throughout the month.

![](../img/202303.3.720.png)

_Image: Decred hashrate._

Distribution of 74 Ph/s hashrate [reported](https://miningpoolstats.stream/decred) by the pools on Apr 1: Poolin 54%, F2Pool 35%, AntPool 11%, CoinMine 0.2%.

Distribution of 1,000 blocks actually [mined](https://miningpoolstats.stream/decred) by Apr 3: Poolin 44%, F2Pool 43%, AntPool 9%, BTC.com 3%.

![](../img/202303.4.720.png)

_Image: Historical pool hashrate distribution._

**Staking**: [Ticket price](https://dcrdata.decred.org/charts?chart=ticket-price&axis=time&visibility=true-true&mode=stepped) varied between 223-254 DCR.

![](../img/202303.5.720.png)

_Image: Ticket price has stabilized._

The [locked amount](https://dcrdata.decred.org/charts?chart=ticket-pool-value&scale=linear&bin=day&axis=time) was 9.64-9.83 million DCR, meaning that 64.0-65.2% of the circulating supply [participated](https://dcrdata.decred.org/charts?chart=stake-participation&scale=linear&bin=day&axis=time) in Proof of Stake.

![](../img/202303.6.720.png)

_Image: DCR locked in tickets keeps crawling up._

**VSP**: The [16 listed VSPs](https://decred.org/vsp/) collectively managed ~7,200 (-210) live tickets, which was 17.6% of the ticket pool (-0.8%) as of Apr 1.

Biggest gainers in March were ubiqsmart.com (280 tickets or +155%) and dcrhive.com (+225 tickets or +25%).

![](../img/202303.7.720.png)

_Image: Distribution of tickets managed by VSPs._

**Nodes**: [Decred Mapper](https://nodes.jholdstock.uk/user_agents) observed between 162 and 176 dcrd nodes throughout the month. Versions of 166 nodes seen on Apr 1: v1.7.5 - 36%, v1.7.1 - 21%, v1.8.0 dev builds - 13%, v1.7.2 - 13%, v1.7.0 - 8%, v1.7.4 - 4%, other - 7%.

![](../img/202303.8.720.png)

_Image: Historical dcrd version distribution, data from nodes.jholdstock.uk. Data until Jan 2023 was incomplete._

The share of [mixed coins](https://dcrdata.decred.org/charts?chart=coin-supply&zoom=jz3q237o-la8vk000&scale=linear&bin=day&axis=time&visibility=true-true-true) varied between 60.5-61.1%. Daily [mixed volume](https://dcrdata.decred.org/charts?chart=privacy-participation&bin=day&axis=time) varied between 317-495K DCR.

![](../img/202303.9.720.png)

_Image: Mixed supply has recovered from a brief drop._

Decred's [Lightning Network](https://ln-map.jholdstock.uk/) explorer has seen 175 nodes (+17), 354 channels (+49) with a total capacity of 129 DCR (+14), as of Apr 3. These stats vary depending on the LN node. For example, @karamble's node reported 175 nodes (+0), 376 channels (-9) and 135 DCR (-33) capacity on same day Apr 3.


## Ecosystem

[Metal Pay](https://metalpay.com/) has disabled DCR trading according to a [user report](https://matrix.to/#/!teQafvHMYpIbqLIieU:decred.org/$JvKPmPcgLw-bUW-7Tn2QFlqmRFtLQN0pPC-4Qq5u0yY?via=decred.org&via=matrix.org&via=t2bot.io). This is confirmed by their support site which no longer shows DCR in the list of [assets available for trading](https://help.metalpay.com/hc/en-us/articles/4409447985303-What-Cryptocurrencies-are-Available-for-Trading-on-Metal-Pay-). Assets supporting [deposits and withdrawals](https://help.metalpay.com/hc/en-us/articles/4409465061911-Which-Cryptocurrencies-Support-Deposit-and-Withdrawal-on-Metal-Pay-) do not include DCR either, and apparently never did. Other coins delisted in the same batch with DCR include BNB, BUSD, DGB, PAX and TUSD. In the bigger picture, Metal Pay [delisted](https://www.reddit.com/r/CryptoCurrency/comments/zlmxj3/delisting_notice_for_select_tokens_on_metal_pay/) 13 assets in December including XMR, ZEC, DASH and BSV. Since [November 2022](https://web.archive.org/web/20221207223930/https://help.metalpay.com/hc/en-us/articles/4409447985303-What-Cryptocurrencies-are-Available-for-Trading-on-Metal-Pay-) the list of tradeable assets reduced from 63 to just 15. Metal Pay first listed DCR in [April 2020](https://twitter.com/metalpaysme/status/1249745420206686208).

Bittrex's [Instant Buy](https://global.bittrex.com/instant) feature did not work for DCR due to low liquidity, according to a [user report](https://matrix.to/#/!teQafvHMYpIbqLIieU:decred.org/$GWyVIBD5k_vDEUPxJK3QTOFqdAot8he-q4RNcxLsmqo?via=decred.org&via=matrix.org&via=t2bot.io). This did not affect limit orders on the full trading interface.

[Ledger](https://www.ledger.com/) representative came to Decred's Matrix chat room to share a [status update](https://matrix.to/#/!teQafvHMYpIbqLIieU:decred.org/$kwC-IMBBr92cstg707O_SlLBJEtCiOt_RmVTtE6S0dI?via=decred.org&via=matrix.org&via=t2bot.io). The summary is: Decred support in Ledger Live is broken for some users, it is taking a long time to fix, and Ledger would love to redirect affected users to third party services compatible with their devices in the situation where an integration is broken on Ledger's side. Therefore Ledger will benefit from the upcoming [direct integration](https://proposals.decred.org/record/609db9e) in Decrediton.

Binance [announced](https://www.reddit.com/r/decred/comments/123tn1i/binance_close_isolated_margin_for_decred_and_some/) the delisting of DCR/BTC and DCR/USDT pairs from Isolated Margin. For context, NEBL and XVG were also part of this delisting batch. Regular (Spot) DCR trading is NOT affected by this. At the same time, personal quota in the Simple Earn product has [increased](https://matrix.to/#/!aNnAOHkWUdNcEXRGjJ:decred.org/$Iv4uASbdiLZIMZWbVVYFqY-motmynF19DH5MYvSRgNo?via=decred.org&via=matrix.org&via=planetdecred.org) from 300 to 10,000 DCR per person. As of Mar 27, Simple Earn showed 1.67% APR while staking DCR directly yields about 7%/year.

Bittrex made a big announcement about [shutting down U.S. operations](https://twitter.com/BittrexExchange/status/1641879884682387457) due to regulatory and economic challenges. Per their [timeline](https://bittrex.zendesk.com/hc/en-us/articles/10080271948701), fiat withdrawals must conclude by Apr 24 and crypto withdrawals by Apr 29 (sooner is better). Bittrex Global is not (directly) affected and will continue operations for non-U.S. customers. The move came after Bittrex was [fined](https://www.reuters.com/business/finance/crypto-exchange-bittrex-fined-53-mln-by-us-treasury-dept-2022-10-11/) in December for $29 million for violating sanctions and AML regulations. Despite closing U.S. operations Bittrex may be hit by another [lawsuit](https://reason.com/2023/04/19/sec-sues-crypto-exchange-bittrex-shortly-after-it-announces-its-leaving-u-s-markets/) from the SEC for operating an unregistered securities exchange.

Join our [#ecosystem](https://chat.decred.org/#/room/#ecosystem:decred.org) chat to follow Decred ecosystem updates.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.


## Outreach

Monde PR's achievements:

- Pitched 2 commentary opportunities
- Pitched 8 media opportunities

Secured the following media placements:

- An article in [Cointelegraph](https://cointelegraph.com/news/trezor-crypto-wallet-s-move-into-the-semiconductor-business-isn-t-for-everyone) featuring commentary from @jz on Trezor crypto wallet's move into the semiconductor business. The article was syndicated to 14 publications including [Ethereum Today](https://www.ethereum.today/trezor-crypto-wallets-move-into-the-semiconductor-business-isnt-for-everyone/) and [Bitcoin Insider](https://www.bitcoininsider.org/article/207994/trezor-crypto-wallets-move-semiconductor-business-isnt-everyone).
- An article in [CoinDesk](https://www.coindesk.com/markets/2023/03/16/crypto-observers-believe-us-banking-crisis-could-strengthen-crypto-ecosystem-in-the-long-term/) featuring commentary from @jz on the long term effects of the U.S. banking crisis on crypto. The article was syndicated to 3 publications including [Yahoo! Finance](https://finance.yahoo.com/news/crypto-observers-believe-u-banking-113017805.html) and [Markets Insider](https://markets.businessinsider.com/news/currencies/crypto-observers-believe-us-banking-crisis-could-strengthen-crypto-ecosystem-in-the-long-term-1032172484).


## Events

**Attended:**

- @arij gave a [presentation](https://decredcommunity.github.io/events/index/20230304.1) at Technopark Casablanca on the theme "Blockchain and Entrepreneurship". It started with an intro to blockchain tech use cases and history, followed by a demo of Decrediton and Politeia. The attendees were of different backgrounds including finance, energy and IT sectors. The majority came in response to a LinkedIn announcement.
- [Second event](https://decredcommunity.github.io/events/index/20230311.1) by the Decred Arabia team was co-organized by the sports association of Aïn Chock and the District Council of Aïn Chock Casablanca. @khalidesi presented an introduction to blockchains on day 1 and application of blockchains and the Decred example on day 2. The theme was to demonstrate how the blockchain can improve the way businesses operate and promote greater economic and social inclusion.

**Upcoming**:

- @elian will present the latest updates from Decred in [Monerotopia](https://monerotopia.com/) in Mexico City on May 5, 6, and 7. Decred will have a small booth.


## Media

**Selected articles:**

- [Decred vs DigiByte: Speed race!](https://www.decredmagazine.com/decred-vs-digibyte/) by @Joao
- [Why is Decred not EVM compatible?](https://www.decredmagazine.com/why-is-decred-not-evm-compatible/) by @BlockchainJew

Decred Magazine engagement stats for March:

- Total number of articles on DM: 427
- Newsletter subscribers: 93
- New DM posts and newsletters sent: 18
- Active social media campaigns: 35
- Completed social media campaigns: 35
- Social media posts: 127
- Likes: 709
- Re-tweets: 181
- Social media followers across all Twitter and Facebook platforms and accounts (including [@DecredSociety](https://twitter.com/DecredSociety)): 1,290

**Videos:**

- [Accounts in Decrediton - Money Evolved](https://www.decredmagazine.com/accounts-in-decrediton/) by @phoenixgreen
- [Timestamply - redesign for timestamping digital existence](https://www.decredmagazine.com/timestamply-redesign-for-timestamping-digital-existence/) by @phoenixgreen - also as a [text post](https://www.decredmagazine.com/timestamply-redesign-for-timestamping-digital-existence/) and as a [Spotify podcast](https://podcasters.spotify.com/decred-magazine/episodes/Timestamply---Redesign-for-timestamping-digital-existence-e204bff)
- [DCRDEX 0.6 is coming - multi-chain wallets, market maker bots, DigiByte support & more](https://www.decredmagazine.com/dcrdex-0-6-is-coming/) by @phoenixgreen - also as a text post and as a [podcast](https://podcasters.spotify.com/pod/show/decred-magazine/episodes/DCRDEX-0-6-is-coming-e210q07)
- [Timestamply tutorial demonstration - Decred time stamping](https://www.youtube.com/watch?v=Vw1J5nleUK8) by @phoenixgreen - also as a [text post](https://www.decredmagazine.com/timestamply-tutorial/)

Livestream:

- [State of the Market - Content and development proposals for Decred feat. Cointelegraph](https://www.decredmagazine.com/state-of-the-market-content-and-development-proposals/) by @phoenixgreen and @Exitus joined by Matthew and Yana - also as a [podcast](https://podcasters.spotify.com/pod/show/decred-magazine/episodes/State-of-the-market---Content-and-Development-Proposals-e209gfm)

**Audio:**

- [Living on Crypto - Rediscovering the original purpose of crypto as cash](https://twitter.com/i/spaces/1djGXlALNNdGZ) - @Tivra talks to [@TheDesertLynx](https://twitter.com/TheDesertLynx) who has been living on crypto since 2016. "If you're tired of trad banking and wanna break free, this is for you". Mirrored on [Spotify](https://podcasters.spotify.com/decred-magazine/episodes/Living-on-Crypto--Rediscovering-the-Original-Purpose-of-Crypto-as-Cash-e205aup).

**Art and fun:**

- [Bison Relay rewards](https://twitter.com/karamblez/status/1631583670732480514) animation by @karamble
- [Do you even timestamp your existence?](https://twitter.com/karamblez/status/1632551305469128704) animation by @karamble
- [Decred DEX - There's a better way](https://www.youtube.com/shorts/CpwiihYotbI) by @buck54321
- [The future will not be centralised](https://www.decredmagazine.com/the-future-will-not-be-centralised/) by @OfficialCryptos
- [Decred Pepe crushing miners](https://twitter.com/karamblez/status/1640492718211182592) by @karamble
- [What the heck did you just say about Decred?](https://www.youtube.com/watch?v=WRL-ISUme0I) by Laboratory for Memetic Experimentation
- [TikTok on Cointelegraph proposal](https://twitter.com/exitusdcr/status/1641796401725337602) by @DajanaDcr and @Exitus

**Translations:**

- Decred Journal January-February got a total of 3 new [translations](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic) and Polish (@kozel). Thank you friends!

**Discussions:**

- Effects of the current banking crisis on the [crypto markets](https://twitter.com/BisonDigest/status/1636523254050324481) and related issues. Follow [@BisonDigest](https://twitter.com/BisonDigest) for best convos spotted on Bison Relay, or better, [join Bison Relay](https://bisonrelay.org/) to not miss any.
- [Survey of good marketing ideas](https://twitter.com/exitusdcr/status/1639809057870721024)

**Other:**

- @decredmagazine made 3 new [TikTok videos](https://www.tiktok.com/@decredmagazine)


## Markets

In March DCR was trading between USDT 17.53-25.90 and BTC 0.00068-0.00102. The average daily rate was $20.69.

![](../img/202303.10.920.png)

_Image: Applesaucesome is bullish. Follow on [Twitter](https://twitter.com/applesaucesome1) for more._

![](../img/202303.11.720.png)

_Image: DCRDEX monthly volume in USD._


## Relevant External

Three US banks [failed in March](https://www.decredmagazine.com/is-this-the-start-of-a-new-banking-crisis/), the largest of them being [Silicon Valley Bank](https://www.nytimes.com/2023/03/10/business/silicon-valley-bank-stock.html) (SVB), which was the [second largest](https://www.decredmagazine.com/is-this-the-start-of-a-new-banking-crisis/) US bank failure of all time. One of the ripple effects was a temporary [de-pegging](https://www.coindesk.com/markets/2023/03/11/usdc-stablecoin-depegs-from-1-circle-says-operations-are-normal/) of the USDC stablecoin as news emerged that ~10% of the funds backing USDC were stuck with SVB when the FDIC stepped in to take over before Circle's withdrawal was processed.

The operators of the Tether stablecoin allegedly used falsified documents and shell companies to get bank accounts, in an [article](https://www.wsj.com/articles/crypto-companies-behind-tether-used-falsified-documents-and-shell-companies-to-get-bank-accounts-f798b0a5) by the Wall Street Journal (non-paywalled [link](https://archive.is/50s0q)). WSJ reviewed a cache of emails from Tether staff which indicated a long-running effort to retain banking access by engaging in various schemes, including having someone in China making fake invoices and contracts to disguise deposits and withdrawals - a policy which was ultimately stopped when owner Stephen Moore wrote he "... would not want to argue any of the above in a potential fraud/money laundering case".

Nic Carter has documented [evidence](https://www.piratewires.com/p/2023-banking-crisis) for what he terms Operation Choke Point 2.0, a deliberate effort to restrict banking access to crypto firms by discouraging banks from dealing with them using various means.

Binance has been [charged](https://decrypt.co/124800/binance-cftc-lawsuit-crypto) by the CFTC in a wide ranging complaint which covers a number of offences, including weak KYC/AML that allowed US customers to trade derivatives and securities which they were not registered to offer, allowed money laundering to occur, and traded against their own customers. The 74 page [complaint](https://www.docdroid.net/60YAbCz/cftc-binance-pdf) includes quotes from messages sent between internal staff, including such gems as "I HAZ NO CONFIDENCE IN OUR GEOFENCING", from the money laundering reporting officer. The complaint also mentions Bitcoin and Ethereum as commodities, in service to defining Binance's activities as subject to CFTC's jurisdiction. CZ [reacted](https://twitter.com/cz_binance/status/1640372505046052866) with "4" [meaning](https://twitter.com/cz_binance/status/1610018096122851328) "Ignore FUD", and later with a longer [response](https://www.binance.com/en/blog/from-cz/czs-response-to-the-cftc-complaint-2408916493005890282) which recaps how much Binance has [invested](https://decrypt.co/124683/binance-cftc-lawsuit-response) in compliance and cooperation with regulators. Some analysts are [pessimistic](https://twitter.com/adamscochran/status/1640378686397448192) about Binance's chances against CFTC.

Coinbase has been [threatened](https://reason.com/2023/03/23/sec-to-coinbase-nice-crypto-exchange-you-got-there-itd-be-a-shame-if-something-happened-to-it/) by the SEC of a possible legal action for violations of the federal securities laws. Coinbase representative went public about company's frustration about SEC's unclear selection of cryptoassets considered to be securities, and cited SEC's denial to tell which specific assets traded on Coinbase platforms are securities.

Justin Sun and his companies Tron Foundation, BitTorrent Foundation and Rainberry have been [sued](https://www.sec.gov/news/press-release/2023-59) by the SEC for violations including sale of unregistered securities (TRX and BTT) and manipulating the secondary market for TRX through extensive wash trading. A number of celebrities who were engaged to promote Sun's projects have also been sued in the same motion for promoting TRX/BTT without disclosing the arrangement, they include Lindsey Lohan, Jake Paul, Soulja Boy, and Lil Yachty. The period for which Sun is accused of wash trading covers April 2018 to February 2019, during which time Sun allegedly provided between 4.5 million and 7.4 million TRX and instructed staff to wash trade it using two of his accounts.

Do Kwon, of Terra/Luna infamy, was [arrested](https://www.coindesk.com/business/2023/03/23/do-kwon-arrested-in-montenegro-interior-minister/) in Montenegro for using forged documents. Both the US and South Korea have [announced](https://www.coindesk.com/consensus-magazine/2023/03/29/the-questions-that-linger-after-do-kwons-arrest/) their wish to extradite and prosecute him.

The second Retroactive Public Goods Funding (RetroPGF) initiative by Optimism was [completed](https://optimism.mirror.xyz/Upn_LtV2-3SviXgX_PE_LyA7YI00jQyoM1yf55ltvvI) in March, with 10 million OP being distributed to 195 different projects and people that had contributed something to the Optimism or Ethereum ecosystem. The funds were distributed to recipients in three different sections, Infrastructure (received 37%), Tooling & Utilities (32%) and Education (31%). To decide how the OP would be distributed, a panel of 90 community members was [formed](https://community.optimism.io/docs/governance/retropgf-2/#voting-badge-distribution) by selecting community members using a variety of different means. Each "badgeholder" ranked the nominated projects and funds were dispersed according to a weighted average of their votes.

Arbitrum, an Ethereum Layer 2, conducted its long-anticipated airdrop, and there has been controversy about how well anticipated the conditions were by airdrop hunters. [Analysis](https://mirror.xyz/x-explore.eth/AFroG11e24I6S1oDvTitNdQSDh8lN5bz9VZAink8lZ4) of the airdrop indicated that, despite rules to avoid giving airdrops to Sybil users, as much as 48% of the airdropped tokens went to an address that was strongly associated with at least one other address which also received the airdrop - with 22% going to advanced Sybil users who had thousands of associated addresses receiving the airdrop.

Once the tokens were airdropped their holders (those who didn't dump immediately) became Arbitrum's governance decision-makers. In the first proposal (AIP-1) they would decide on whether to allocate 750 million ARB (worth $1 billion) tokens to the Arbitrum Foundation, and it turned [messy](https://www.coindesk.com/business/2023/04/01/arbitrums-first-governance-proposal-turns-messy-with-1b-arb-tokens-at-stake/). Community members objected to the Foundation having discretion to spend some of these funds without on-chain community approval, and when it was clear that the proposal was in difficulty the Foundation published a [blog post](https://forum.arbitrum.foundation/t/clarity-around-the-ratification-of-aip-1/12864) explaining that the vote was to ratify something that was already happening, the Foundation already had the funds and had in fact started spending them. This appears to have been a miscommunication about the nature of the vote, but following the controversy which erupted the Foundation has taken steps to reassure the community that the remaining 700 million ARB will not be touched until a proposal has been approved by the community.

This month's record breaking DeFi hack is a good news story, because it's the largest ever [recovery](https://twitter.com/eulerfinance/status/1643345907344379904) of funds, by the Euler Labs team. The Euler Finance protocol was [exploited](https://cointelegraph.com/news/euler-labs-hacker-returns-all-of-the-recoverable-funds-timeline) by a flash loan attack on March 13, the attacker was able to obtain $197 million, and causing the value locked in Euler contracts to drop as low as $10 million. Euler Labs tried to negotiate the return of 90% of the funds with the hacker and when the negotiations broke down put out a $1 million bounty for information about the attacker. Although a deal could not be reached the attacker began to sporadically return the funds, until eventually on April 4 Euler Labs announced that all the "recoverable funds" had been returned and the bounty was cancelled.

LinksDAO is seemingly on course to [achieve](https://twitter.com/LinksDAO/status/1636433901232222208) its main objective and buy a Links Golf Club, specifically Spey Bay on the Moray Coast of Scotland. The Club was listed for $905,000 and LinksDAO's representatives were the top bidders, with the sale to be confirmed and the final sale price as yet unknown. LinksDAO is still [reported](https://www.golfdigest.com/story/links-golf-club-buys-spey-bay-golf-links) to be on the lookout for US golf properties, as presumably not many of its 5,400 global members have easy access to the Moray Coast to play a round.

The "Skull of Satoshi", an art installation commissioned by Greenpeace as part of a campaign to highlight the impact of PoW mining, has been [adopted](https://decrypt.co/124622/skull-satoshi-artist-says-was-wrong-bitcoin-mining) by the Bitcoin community as its own. The artist has come to the realization that it is not a black and white issue, as they thought it was when they began creating the piece.

Ron DeSantis, Governor of Florida, has [proposed](https://www.coindesk.com/policy/2023/03/20/florida-governor-ron-desantis-proposes-law-to-ban-cbdcs/) legislation to ban the acceptance of Central Bank Digital Currency (CBDC) in the state. [Doubts](https://www.coindesk.com/consensus-magazine/2023/03/22/cbdc-desantis-ban-digitaldollar/) have been raised whether the legislation is workable, it is likely that a Federal push for a CBDC could overturn pre-existing state law.

Dubai has published new laws in February that ban issuance and use of [anonymity-enhancing cryptocurrencies](https://www.coindesk.com/policy/2023/02/08/dubai-prohibits-privacy-coins-under-new-crypto-rules/) like Monero.

Two UK banks have [restricted](https://www.bloomberg.com/news/articles/2023-03-02/uk-banks-ramp-up-crypto-restrictions-with-new-retail-limits) retail customers' access to crypto. Nationwide introduced a daily limit of £5,000 on debit-card purchases, while disallowing to use credit cards to buy crypto. HSBC has also blocked crypto purchases with its credit cards.

Nigeria has been pushing its CBDC, when [incentives](https://www.coindesk.com/consensus-magazine/2023/03/06/nigerians-rejection-of-their-cbdc-is-a-cautionary-tale-for-other-countries/) like discounts on taxi fares didn't work to increase adoption they restricted access to cash to force the issue, but people are protesting about the lack of cash and still adoption of the CBDC is at less than 0.5% of the population.

That's all for March. Share your updates for the next issue in our [#journal](https://chat.decred.org/#/room/#journal:decred.org) chat room.


## About

This is issue 57 of Decred Journal. Index of all issues, mirrors, and translations is available [here](https://xaur.github.io/decred-news/).

Most information from third parties is relayed directly from the source after a minimal sanity check. The authors of the Decred Journal cannot verify all claims. Please beware of scams and do your own research.

Credits (alphabetical order):

- writing, editing, publishing: bee, bochinchero, Exitus, jz, karamble, l1ndseymm, phoenixgreen, richardred
- reviews and feedback: davecgh
- title image: Exitus
- funding: Decred stakeholders
