# Decred月报 – 2021年2月

![abstract art](img/202103.1.github.png)

_图片：@saender_

三月份的亮点：

- 启用去中心化国库的共识投票已获得批准，预计会于5月7日左右启动，届时版本低于v1.6的软件节点将被分叉。
- v1.6.2已于4月初发布，它修复了混币和VSP购票的许多问题，并改善了SPV节点的稳定性以及其它改进。
- Politeia更加灵活和可扩展的存储后端开发已经进行了一年多，现在终于完成了！
- Decred社区已经为项目选择了一种灵性动物，雄伟的野牛！

内容：

- [硬分叉来了](#fork-is-coming)
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

## 硬分叉来了

启用去中心化国库的共识投票已获得[批准](https://explorer.dcrdata.org/agenda/treasury)，新共识将在5月7日左右激活。低于v1.6的节点将停止同步，因此请升级以保留在网络上。您可以在[此处](https://voting.decred.org/)跟踪剩余的日期。

最新版本v1.6.2修复了一些与VSP购票和混币有关的错误，并改进了SPV的操作。请在[此处](https://github.com/decred/decred-binaries/releases/tag/v1.6.2)查看完整的发行说明和下载，并且不要忘记在安装前对其进行[验证](https://docs.decred.org/advanced/verifying-binaries/)。

## 开发进展总结

除非另有说明，否则此处报告的工作仅限为“合并到主核心存储库”状态。这意味着这项工作已经完成、审查并集成到高级用户可以[构建和运行](https://medium.com/@artikozel/the-decred-node-back-to-the-source-part-one-27d4576e7e1c)的源代码中，但对于普通用户来说，还不能使用。

<a id="dcrd" />

**[dcrd](https://github.com/decred/dcrd)**

合并在master和v1.6.2版本中：

- 仅将[快速](https://github.com/decred/dcrd/pull/2606)阻止公告发送给完整的对等节点，而不发送给无法正确处理它们的轻量级客户端。这样可以提高SPV连接的稳定性，因此，SPV钱包应该需要更少的重新扫描。

本月的主要新增功能是用于处理[标准地址](https://github.com/decred/dcrd/pull/2610)的新软件包，该软件包比其替换的代码更易于遵循和使用。它也更通用，允许将来添加新的地址类型。如果您想知道“脚本”和“地址”之间是如何关联的，或者“标准”与“共识”之间有何不同，请查看包装中崭新的[自述文件](https://github.com/decred/dcrd/tree/master/txscript/stdaddr)或遵循示例和全面的测试以全面了解其工作原理。感谢所有评论者并欢迎新来者-拥有一双崭新的眼睛总是好事！

新的地址软件包以及其他与地址相关的合并更改都是为未来的共识投票奠定一些基础和基础设施的一部分。

其它合并工作：

- 不在日志中记录[时间戳](https://github.com/decred/dcrd/pull/2608的选项
- more accurate detection of [own IP](https://github.com/decred/dcrd/pull/2571) address to fix some UPnP configurations
- increased test coverage for `rpcserver` and the new UTXO cache

<a id="dcrwallet" />

**[dcrwallet](https://github.com/decred/dcrwallet)**

合并在master和v1.6.2版本中：

- 防止向混合服务器收取[低费用](https://github.com/decred/dcrwallet/pull/2011)，这些费用现已被拒绝
- 固定的[UTXO处理](https://github.com/decred/dcrwallet/pull/2013)，以避免余额足以购买一张选票时出现“余额不足”错误
- 如果在dcrwallet设置中配置了VSP，则使用命令更新vspd票证的投票选择`setvotechoices`
- 新的`accountunlocked` [命令](https://github.com/decred/dcrwallet/pull/2020)报告帐户加密和锁定状态（对于DCRDEX是必需的，但通常也很有用）
- config标志以禁用[日志记录](https://github.com/decred/dcrwallet/pull/2014)到文件

<a id="decrediton" />

**[Decrediton](https://github.com/decred/decrediton)**

修补程序版本v1.6.2已修复了多个错误，并更新了Decred- patched [trezor-connect](https://github.com/decred/decrediton/pull/3340)库。

合并在master中：

- 使用pi-ui库中的新[滑块](https://github.com/decred/decrediton/pull/3046)组件
- 重组[余额](https://github.com/decred/decrediton/pull/3319)概览
- 列出UTXO视图转换为[模态](https://github.com/decred/decrediton/pull/3323)
- 改进了与[Trezor](https://github.com/decred/decrediton/pull/2956)相关的模态的布局
- 项目已更新为最新的[Electron 12](https://github.com/decred/decrediton/pull/3318) 和 [Webpack 5](https://github.com/decred/decrediton/pull/3322)
- 大约25个拉取请求结束了为期1年的探索，将代码库迁移到具有功能组件，挂钩和[CSS模块](https://github.com/decred/decrediton/issues/2439)的现代React编程风格
- 增加的UI测试覆盖率
- 约11个bug修复

对来自5个贡献者的总共53个PR进行了[合并](https://github.com/decred/decrediton/pulls?q=is%3Apr+merged%3A2021-03-01..2021-03-31+sort%3Aupdated-asc)，更改了504个文件，添加了14.5K，并删除了1.47K行代码。没有太多用户可见的更改，这些大量的内容基本上意味着要进行大量的“幕后”基础架构升级，从而使将来的开发变得更加容易。

正在进行中：[DCRDEX](https://github.com/decred/decrediton/pull/3356)集成和设计更新。

<a id="politeia" />

**[Politeia](https://github.com/decred/politeia)**

经过近一年的开发，向更可扩展和[灵活](https://twitter.com/lukebp_/status/1376238020563767303)的存储后端的史诗迁移已[合并](https://github.com/decred/politeia/pull/1180)。总体而言，它为我们带来了以下优势：

- 可扩展性-不再受限于单个实例的文件系统
- 时间戳和数据是分开的，从而可以真正审查（和删除）数据，而无需权衡取舍。请注意，检查只会删除数据，而不会删除证明服务器已看到数据的记录，即“审计线索”是不可变的。
- 能够检索任何数据的带密码时间戳证明，例如单个注释。在Git后端没有简单的方法可以做到这一点。
- 一种适当的插件体系结构，在该体系结构中，插件可以通过附加功能（如评论或票证投票）来扩展带有时间戳的通用“记录”。无需编写代码即可在配置文件中打开和关闭插件。
- 简化的 `politeiad` API
- `politeiawww` 重写API使其具有通用性且与应用程序无关，而插件可处理专用路由
- 检查[请求](https://github.com/decred/politeia/pull/1180)以获取更多详细信息

从统计数据可以看出，[后端](https://github.com/decred/politeia/pull/1180)和[前端](https://github.com/decred/politeiagui/pull/2306)的更改重写了大部分Politeia代码库：添加了51K行，删除了42K行，并且更改了474个文件。

对于开发人员，[v0.2.0](https://github.com/decred/politeia/releases/tag/v0.2.0)标签标记了支持politeiad Git后端，politeiad v1 API以及大多数politeiawww `www/v1` 和 `www/v2`API的最后一次提交。

欢迎每个人都通过[test-proposals2.decred.org](https://test-proposals2.decred.org/)加入新版本的测试小组。

其它变化：

- politeiavoter命令行工具的点滴模式是真正[随机](https://github.com/decred/politeia/pull/1368)的，而不是使用随机的时段

> 短期内，我们将专注于功能开发，这些功能在这些体系结构升级期间处于倒退状态。诸如来自作者的提案更新，为在Politeia上运行的社区启动Reddit之类的论坛，添加非正式的利益相关方民意测验等。
> 
> 从长远来看，我们的想法是使Politeia成为可配置的，带有时间戳的数据存储，可以作为各种用例的基础。 ([@lukebp](https://twitter.com/lukebp_/status/1376259489704337408))

<a id="dcrpool" />

**[dcrpool](https://github.com/decred/dcrpool)**

候选发布版2对于即将到来的V1.2.0是[测试](https://twitter.com/dnldd/status/1376476239062564868)版本。有关错误修复，改进和一些重大更改的完整列表，请参见[发行说明](https://github.com/decred/dcrpool/releases/tag/v1.2.0-rc2)。

合并在master中：

- 固定保存[存档](https://github.com/decred/dcrpool/pull/309)付款
- 在不可用的单独池中禁用帐户[查找UI](https://github.com/decred/dcrpool/pull/310)
- `--homedir` config标志已重命名为`--appdata`与其它软件一致

<a id="dcrlnd" />

**[dcrlnd](https://github.com/decred/dcrlnd)**

@matheusd发现了一个有趣的hack，该hack可以在几乎不为HTLC构建的现有LN代码更改的情况下实现PTLC。

PTLC（点时间锁定合约）是闪电网络中令人振奋的发展，因为它有潜力解决当前使用的HTLC（哈希时间锁定合同）的[局限性](https://suredbits.com/payment-points-monotone-access-structures/)，并有可能使新的用例成为可能。

实际上，启用PTLC的黑客对于@matheusd是如此简单，以至于他还能够使用它编写一个有趣的结构，称为多救赎者交易树（MRTTREE），并在其上建立一个离线LN捐赠/付款原型。该系统由修补的[dcrlnd](https://github.com/decred/dcrlnd/compare/v0.3.1...matheusd:ptlc-poc)，用于协调MRTTREE的PoC[服务器](https://github.com/matheusd/mrttree)和修补的[Decrediton](https://github.com/matheusd/decrediton/commits/mrttree_poc)组成。在发送给lightning-dev邮件列表的[email](https://lists.linuxfoundation.org/pipermail/lightning-dev/2021-March/002983.html)和演示[视频](https://www.youtube.com/watch?v=m1sQGHUKU7I)中对数学进行了解释（离线LN付款演示在[15分钟](https://www.youtube.com/watch?v=m1sQGHUKU7I&t=915s)左右开始）。

该hack行为是实验性的，需要进行认真的密码研究以确保其安全性。尽管如此，这项工作在以LN驱动的[多所有者选票](https://blog.decred.org/2019/11/11/LN-Multi-Owner-Tickets/)（选票拆分的一种更好形式）以及MRTTREE支持的其他用例（例如链下捐赠和众筹）的背景下还是很有趣的。与原始[blog](https://blog.decred.org/2019/11/11/LN-Multi-Owner-Tickets/)文章中提到的基于HTLC的MRTTREE构造不同，基于PTLC的构造不需要新的操作码：现有的Schnorr checkig操作码（或最终添加的任何新操作）足以启用它。

您可以在最近的Decred Depth中@matheusd从[28](https://www.youtube.com/watch?v=O6oIrRsZnMQ&t=27m54s)分钟开始了解有关Decred的LN的更多信息。

<a id="cspp" />

**[cspp](https://github.com/decred/cspp)**

- 最小[对等](https://github.com/decred/cspp/pull/64)体数量可配置为希望增加其数量以提供更高质量混合的服务器
- 支持[LOGFLAGS](https://github.com/decred/cspp/pull/66)以便更灵活地记录日志

<a id="dcrdex" />

**[DCRDEX](https://github.com/decred/dcrdex)**

- 重置和更改[密码](https://github.com/decred/dcrdex/pull/978)的功能
- [禁用](https://github.com/decred/dcrdex/pull/985)帐户的功能
- 允许对您的订单表进行[排序](https://github.com/decred/dcrdex/pull/955)
- 指示[断开](https://github.com/decred/dcrdex/pull/989)状态
- 支持针对DCR钱包的基于帐户的[加密](https://github.com/decred/dcrdex/pull/1023)和锁定（Decrediton将使用它仅锁定交易帐户，而不锁定其他帐户）
- 允许多个经过身份验证的[会话](https://github.com/decred/dcrdex/pull/1012)（同时登录不同的浏览器）
- 将最新[费率估算](https://github.com/decred/dcrdex/pull/1000)发送给客户以支持SPV客户，改进订单估算并加强安全性
- 发送原始[交易](https://github.com/decred/dcrdex/pull/804)数据以容纳没有mempool且一直处于黑暗状态的SPV客户端，直到挖掘出合同的tx为止（这也使该过程更加强大，可防止tx在网络上的不良传播）
- 以太坊simnet[工具](https://github.com/decred/dcrdex/pull/956)在开发过程中进行测试
- [Bitcoin Cash](https://github.com/decred/dcrdex/pull/944)支持的基础
- 添加了数据库[版本控制](https://github.com/decred/dcrdex/pull/959)并生成了历史交易数据（交易量，最高和最低等）
- 更新为使用[Webpack 5](https://github.com/decred/dcrdex/pull/990)和其他较新的模块
- [dex.decred.org](https://dex.decred.org/) 更新了很酷的新视觉效果@ 30000fps

[合并](https://github.com/decred/dcrdex/pulls?q=is%3Apr+merged%3A2021-03-01..2021-03-31+sort%3Aupdated-asc)了来自6个贡献者的25个PR ，增加了22K，删除了9000行代码。

正在进行中：以太坊支持，新的[注册](https://github.com/decred/dcrdex/pull/1017)协议（更强大+支持任意资产的费用支付），演示[Electron](https://github.com/decred/dcrdex/pull/999)集成以及多项其它改进。

以太坊专家对所使用的[交换合约](https://github.com/decred/dcrdex/issues/1001)的反馈表示赞赏。

请参阅[v0.2](https://github.com/decred/dcrdex/milestone/6)和[v0.3](https://github.com/decred/dcrdex/milestone/12)里程碑以跟踪下一版本的进度。

<a id="dcrios" />

**[dcrios](https://github.com/planetdecred/dcrios)**

进行中：

- 显示Politeia [提案](https://github.com/planetdecred/dcrios/pull/715)
- [混币](https://github.com/planetdecred/dcrios/pull/727)实施
- 将dcrlibwallet更新为最新的Decred模块并修复同步问题

<a id="godcr" />

**[godcr](https://github.com/planetdecred/godcr)**

- 新的用户[发送](https://github.com/planetdecred/godcr/pull/320)页面
- 更新了[概述](https://github.com/planetdecred/godcr/pull/338)和[帐户](https://github.com/planetdecred/godcr/pull/348)页面的用户界面
- 添加了[关于](https://github.com/planetdecred/godcr/pull/352)页面
- 向帐户[详细信息](https://github.com/planetdecred/godcr/pull/337)页面添加了抵押和其他信息
- 调整了文字[输入](https://github.com/planetdecred/godcr/pull/341)
- 带有日志的[调试](https://github.com/planetdecred/godcr/pull/346)页面
- 输入密码后，在应用启动时开始[同步](https://github.com/planetdecred/godcr/pull/343)
- 同步还原的钱包时请求[密码](https://github.com/planetdecred/godcr/pull/324)，以允许生成地址
- 代码清理和bug修复

正在进行中：“ Politeia[提案](https://github.com/planetdecred/godcr/pull/331)”页面和进一步的UI工作。

<a id="dcrdata" />

**[dcrdata](https://github.com/decred/dcrdata)**

- [限制](https://github.com/decred/dcrdata/pull/1808)POST请求中允许的地址数量

<a id="dcrdevdocs" />

**[dcrdevdocs](https://github.com/decred/dcrdevdocs)**

- [扩展脚本](https://devdocs.decred.org/developer-guides/script-extensions/) 页面已从dcrdocs中移出

<a id="dcrweb" />

**[decred.org](https://github.com/decred/dcrweb)**

- 在VSP页面上列出[vspd](https://github.com/decred/dcrweb/pull/965)
- 更新 [交易所](https://decred.org/exchanges/)页面

<a id="dcraddrscanner" />

**[Decred Address Scanner](https://github.com/decred/dcraddrscanner)**

- 代码存储库移至[decred](https://github.com/decred/dcraddrscanner)组织
- 许可证已更改为ISC以符合F-Droid要求

除了[Google Play](https://play.google.com/store/apps/details?id=com.joegruff.decredaddressscanner)和直接[APK](https://github.com/decred/dcraddrscanner/releases/tag/v1.08)下载外，该应用程序现在还可以在[F-Droid](https://f-droid.org/en/packages/com.decred.decredaddressscanner/)上使用！

<a id="dcrmapper" />

**[Decred Mapper](https://github.com/jholdstock/dcrmapper)**

@jholdstock发布了一个网站，其中包含节点和每个[用户代理](https://nodes.jholdstock.uk/user_agents)的数量的[世界地图](https://nodes.jholdstock.uk/)。源代码可在此处获得。该站点的Testnet版本在[此处](https://testnet-nodes.jholdstock.uk/)。Unix灰胡子将享受386[386主题](https://nodes.jholdstock.uk/?theme=386)。

<a id="ticketsplitting" />

**[Ticket Splitting](https://docs.decred.org/proof-of-stake/ticket-splitting/)**

@bee已编译了一份全面的[文档](https://github.com/decredcommunity/wiki/blob/master/wiki/ticket-splitting-v1.6.md)，其中包含有关选票拆分和v1.6软件的所有最新知识。关键要点：

- 现有的选票拆分解决方案将与v1.5.2软件一起使用，直到2021年5月7日左右停止同步
- 每个人都同意可以进行选票拆分，但是由于需求低（目前每月有81张票证大约占所有票证的0.2％），目前没有多余的资源可用于分配票务
- 最低的收获是修补客户端以支持dcrwallet v1.6中的新身份验证
- 这是新开发人员熟悉Decred的好机会，同时参与Decred的选票更便宜

其它：

- [decredpower.com](https://decredpower.com/)收到了大量的新链接和设计调整
- Bug Bounty报告说，它已经处理了157个提交项目，其中15个有资格获得付款。恭喜[@proabiral](https://twitter.com/proabiral)登上名人堂！

![386](img/202103.2.github.png)

_图片：Decred Mapper的未来派设计_

## 人员

欢迎来到新的第一次贡献者，他们的代码已合并到主存储库中：@tuhalang ([godcr](https://github.com/planetdecred/godcr/commits?author=tuhalang))!

截至4月2日的社区统计数据：

项目|数量|变化
:--|---:|---:
[Twitter](https://twitter.com/decredproject) 粉丝|43,628|+706
[Reddit](https://www.reddit.com/r/decred/) 订阅s|10,797|+238
[Matrix](https://chat.decred.org/) #general 用户|407|+25
[Discord](https://discord.gg/GJ2GXfz) 用户|1,409|-35
[Telegram](https://t.me/Decred) 用户|2,594|+76
[YouTube](https://www.youtube.com/decredchannel) 订阅 / 观看|4,460 / 179K|+40 / +4K
GitHub [dcrd](https://github.com/decred/dcrd) 星 / 叉|589 / 255| +5 / +3

在约90个跟踪的帐户中[检测到](https://github.com/decredcommunity/social-media-stats)显着的活动：

- 主要的Twitter，Reddit和Telegram又有一个月的良好增长
- 自3月中旬开始追踪[CoinGecko](https://www.coingecko.com/en/coins/decred)以来，它获得了+409个赞（至9,516个）
- [@Checkmate](https://twitter.com/_Checkmatey_) aka“ The Machine”获得+1,816位关注者（+ 35％，至7,042位），每天以〜34条推文发布另外1K条推文
- [@PermabullNino](https://twitter.com/PermabullNino) 增加了398位关注者（+ 13％，达到3,391）
- [@ConsensusRough](https://twitter.com/ConsensusRough) 的关注者人数达到惊人的+ 34％（达到580）
- [@decredbr](https://t.me/decredbr) TG获得了6％的用户（至384）
- [@Decred_ES](https://twitter.com/Decred_ES) TW拥有+ 5％的关注者（至1,365）
- [DECRED BRasil](https://www.facebook.com/groups/decredbrasil/) FB在30天的帖子中从50下降到19明显下降

上面是最值得注意的亮点，但是您可以在新的专用位置查看3月和2月的完整报告（最终可以容纳我所有的数字-@bee）。

感谢Decred在所有平台上的大使提高了对该项目的认识！

## 治理

在3月份，[国库](https://explorer.dcrdata.org/address/Dcur2mcGjmENx4DhNqDctW5wJCVyT3Qeqkx)收到了11,531 DCR，支出了4,196 DCR-但是其中3,010被延迟支付了1月份的发票，因此，支付给2月份的发票的金额仅为1,184 DCR。使用3月份的每日DCR / USD平均汇率$ 161.01，得出的总收入为186万美元，支出为67.6万美元。2月为过去工作支付的美元数据是2月的13.5万美元（113.76美元）和1月的16.3万美元延迟付款（54.25美元）。截至4月4日，国库余额为663,658 DCR（1.24亿美元，折合187.04美元）。

三月份发表了三份提案。

- The Moderation 2021 [提案](https://proposals.decred.org/proposals/e1cda44) 估算了该年度的预算为8,800美元（最高为16,500美元），并获得了93.4％的支持和36％的投票率。
- The Design [提案](https://proposals.decred.org/proposals/76eba5a) 涵盖2021年余下时间的设计提案最多需要58,850美元，并且报告说，先前提案的支出不足，因此仅使用了其预算的60％。大部分的支出不足都与身份和视觉传达子域相关。先前提案的工作日志报告已发布在[此处](https://github.com/decred/dcrdesign/issues/252)。 
- 视频内容[提案](https://proposals.decred.org/proposals/95a1409)（第3阶段）即将续订，另外6个月的最高预算为$ 18,800，并增加了2个新的贡献者（@karamble和@DecredSociety）。在上一个阶段中，仅使用了预算的41％。

@bee发布了所有[有效批准](https://decredcommunity.github.io/proposals/approved)提案的列表，以跟踪即将过期的提案。

《Politeia Digest》第[41](https://blockcommons.red/politeia-digest/issue041/)期提供了有关本月提案的更多详细信息。

## 网络

**Hashrate**: March's [hashrate](https://explorer.dcrdata.org/charts?chart=hashrate&zoom=kln9bt1o-kn255ihw&scale=linear&bin=block&axis=time) opened at ~410 Ph/s and closed ~496 Ph/s, bottoming at 228 Ph/s and peaking at 620 Ph/s throughout the month.

Distribution of hashrate [reported](https://miningpoolstats.stream/decred) by the pools on Apr 1: Antpool 37%, Poolin 29%, F2Pool 10%, Easy2Mine 8%, Luxor 1.3%, BTC.com 1.3%, Coinmine 0.04%, UUPool 0.04%, unknown 13%.

Distribution of 1,000 blocks actually [mined](https://miningpoolstats.stream/decred) before Apr 1: Poolin 30%, Antpool 27%, F2Pool 8%, Easy2Mine 4%, Luxor 2%, BTC.com 1.6%, Coinmine 0.1%, unknown 27%.

Hashrate of the previously top UUPool appears to have migrated to Antpool and F2Pool.

**Staking**: [Ticket price](https://explorer.dcrdata.org/charts?chart=ticket-price&zoom=kln9bt1o-kn255ihw&axis=time&visibility=true-true&mode=stepped) varied between 154.3-221.5 DCR, with 30-day [average](https://dcrstats.com/) at 178.0 DCR (-3.7). In the first 3 months of 2021 the ticket price had the highest oscillation since the price algorithm change in 2017, swinging between ~150 and ~220.

The [locked amount](https://explorer.dcrdata.org/charts?chart=ticket-pool-value&zoom=kln9bt1o-kn255ihw&scale=linear&bin=block&axis=time) was 7.10-7.46 million DCR, meaning that 56.0-58.7% of the circulating supply [participated](https://explorer.dcrdata.org/charts?chart=stake-participation&zoom=kln9bt1o-kn255ihw&scale=linear&bin=block&axis=time) in proof-of-stake - again new all-time highs.

**VSP**: On Apr 1, 6.6K live tickets were held by vspd servers and 4.0K by the legacy dcrstakepool servers. Compared to Mar 1, more than 2.2K tickets have migrated to the new vspd system. Legacy VSPs have reported 11K active and 22K total users. All VSPs together (17 old, 11 new) held 26% of the ticket pool.

**Nodes**: Throughout March there were around 215 reachable nodes according to [dcrextdata](https://dcrextdata.planetdecred.org/nodes).

Node versions as of Apr 1 [snapshot](https://nodes.jholdstock.uk/user_agents) (247 total, dcrd only): v1.6.1 - 32%, v1.6.0 - 32%, v1.5.1 - 10%, v1.5.2 - 8%, v1.7 dev builds - 8%, v1.6 dev builds - 6%, v1.5.0 - 2.4%, v1.6.2 - 1.2%.

The share of [mixed coins](https://explorer.dcrdata.org/charts?chart=coin-supply&zoom=kln9bt1o-kn255ihw&bin=day&axis=time&visibility=true-true-true) has gradually increased from 39% to 44%. Daily [mixed amount](https://explorer.dcrdata.org/charts?chart=privacy-participation&zoom=jzk95g03-kncehhc0&bin=day&axis=time) varied between 200-350K DCR.

Decred's [Lightning Network](https://ln-map.jholdstock.uk/) has seen 34 nodes (+4), 60 channels (+4) with a total capacity of 20 DCR (+3.2), as of Apr 1.

@Checkmate shared charts showing increased [transaction](https://twitter.com/_Checkmatey_/status/1372684156908437508) volumes (2021 volume looks even more dramatic when [adjusted](https://twitter.com/_Checkmatey_/status/1369787880776691712) for circulating supply) and how the share of [fees](https://twitter.com/_Checkmatey_/status/1375608621417996288) in the total block reward went from 0.01% to 0.12% since October 2020.

@matheusd [shared](https://www.reddit.com/r/decred/comments/m547to/not_focusing_on_split_tickets_will_affect_us/gr0in3e/) charts of split ticket purchases [by month](https://github.com/decredcommunity/wiki/blob/files/files/20210315.1.png) (80 on average, topped at 127 on March 2020) and by the number of [participants](https://github.com/decredcommunity/wiki/blob/files/files/20210315.2.png) (4 is most common).

## Integrations

[decred.raqamiya.net](https://decred.raqamiya.net/) VSP announced that it will be shutting down. As of Apr 5 it [had](https://decred.raqamiya.net/stats) 128 active users and 284 total users, 52 live tickets, and over 20K tickets voted since 2017. The VSP featured a custom UI, email notifications on voted tickets, and 4 voting servers in 3 continents. The [home page](https://decred.raqamiya.net/) asks to not buy any new tickets, but live tickets will be supported until all of them are called. Thank you for your service!

[CexZ](https://www.cexz.ca/) exchange [announced](https://twitter.com/_cexz_/status/1366501324536299523) the listing of a DCR/BTC pair and came to [visit](https://www.reddit.com/r/decred/comments/lvl8i0/decred_dcr_added_to_the_btc_market/) r/decred.

Warning: the authors of the Decred Journal have no idea about the trustworthiness of any of the services above. Please do your own research before trusting your personal information or assets to any entity.

## Outreach

A new bison [theme](https://twitter.com/BisonContent/status/1370827335973416960) has exploded in March, culminating in DCR Bison species getting its own Twitter account specializing in [@BisonContent](https://twitter.com/BisonContent). Most bison research took place in [#trading](https://chat.decred.org/#/room/#trading:decred.org) (almost 400 mentions). First [mentions](https://matrix.to/#/!hxDOGQVaUlvoqMMcOB:decred.org/$CWpMA7avAE_gWjVVwGglZPIAxxEO-QJ1WwqfT4JfIrw) date back to 2019 chats about Bison Trails, a New York City blockchain infrastructure company (that happens to offer [Decred services](https://bisontrails.co/decred/) now!). But the hype really took off when a stronger link with Decred was found by @Void and @karamble in a 2015 [paper](https://www.researchgate.net/publication/281933407_Collective_decision_making_during_group_movements_in_European_bison_Bison_bonasus) titled "Collective decision making during group movements in European bison, Bison bonasus".

> Group coordination and the synchronization of activities are essential to maintain group cohesion during collective movements. Collective decisions arising from this synchronization are influenced by both ecological and sociodemographic factors. (...) The initiator was more likely to be followed if it went in the direction indicated by the majority of individuals, suggesting a _voting process_.

[@DCRann](https://t.me/DCRann) Telegram channel was created to mirror important announcements and reduce dependency on Twitter.

@pavel has shared more [insights](https://github.com/decredcommunity/proposals/blob/master/proposals/2bf72e/updates/20210313.md) from running the [withDecred.org](https://proposals.decred.org/proposals/2bf72e6) proposal. In total 11.6 DCR was distributed in 5 rounds. People were quite engaged on Twitter even without being rewarded. Getting people to visit the [website](https://withdecred.org/) was a challenge though, even with sponsored tweets. It is most common for Twitter users to quickly consume and like/retweet if they like the content. With that in mind, site content was boiled down to a giant [tweet-storm](https://twitter.com/withdecred/status/1325147231935098880) pinned on the Twitter profile.

Reports from outreach experiments like the one above are appreciated as they help the community to learn what works and what doesn't, and get better at spreading our message.

Monde PR's achievements for March:

- created & pitched 2 stories to finance and crypto publications
- responded to 1 request for comment
- secured 1 media interview

News coverage secured by Monde PR:

- @jy-p appeared on the [Finance Magnates](https://www.financemagnates.com/cryptocurrency/interview/decreds-jake-yocom-piatt-on-bitcoin-blockchain-governance-dcr-more/) podcast talking about Bitcoin, blockchain governance, and DCR, syndicated to 4 news outlets including [Tech Centry](https://techfans.co.uk/decreds-jake-yocom-piatt-on-bitcoin-blockchain-governance-dcr-more/)

A reminder for everyone, if you have an awesome tweet or content to share, don't hesitate to drop it in the [#media](https://chat.decred.org/#/room/#media:decred.org) chat and ask for a retweet via @decredproject.

![bison](../img/202103.3.github.jpg)

_Image: Bison PoWer_

## Events

Attended:

- Mar 12-14 - [Hackathon Nayarit 2021](https://decredcommunity.github.io/events/index/20210312.1) - Internet. Decred in Spanish sponsored the hackathon organized by the Ministry of Education of Nayarit. To prepare participants, the Spanish team hosted Blockchain Education training week, consisting of 5 webinars. Hackathon prize pool of $1,000 was divided as follows: $500 for first place, $300 second place and $200 divided among the rest of the 20 participants that presented final projects. After the hackathon a learning session was made for the winners to learn how to use Decrediton, mobile wallets and a general info on how to store and use crypto. It lasted for 3 hours and winners had a chance to ask questions while receiving their prizes. More details [here](https://decredcommunity.github.io/events/index/20210312.1).
- Mar 15 - [State of crypto adoption in Morocco](https://decredcommunity.github.io/events/index/20210315.1) - Internet. @arij was invited to an interview with Tony Obiajuru from on \#InsideBlockchain at CryptoTvplus where she told about the state of crypto adoption in Morocco, and about Decred and her work with the project.

## Media

Selected articles:

- @arij of "cryptocurrency firm Decred" gave commentary to [CoinDesk](https://www.coindesk.com/crypto-is-banned-in-morocco-but-bitcoin-purchases-are-soaring) on the state of crypto adoption in Morocco. The article was translated to 4+ languages and went a bit viral in Moroccan electronic news. Governor of the central bank of Morocco [commented](https://www.youtube.com/watch?v=yWLNOlKbhtc) on the article, saying that they've put together a committee for studying crypto and central bank digital currencies to keep up with the innovation, that Bitcoin is not money because it's speculative and unregulated, but in the end people cannot be stopped from using it. As a follow-up the bank has launched a [video](https://www.youtube.com/watch?v=38N24GrUTxY) discouraging from using Bitcoin because it's too risky.
- Decred's v1.6.1 release and "User Activated Hard Fork" to decentralize the treasury have been mentioned in f2pool's bi-weekly PoW Round-Up [Mar-09](https://f2pool.io/mining/pow-round-up/20210309-pow-round-up/) and [Mar-23](https://f2pool.io/mining/pow-round-up/20210323-pow-round-up/) issues
- What is Decred? by Samuel Sherwood ([exodus.com](https://www.exodus.com/blog/what-is-decred/))

Videos:

- Matheus Degiovani interview Decred in Depth (live) by @elima\_iii ([youtube](https://www.youtube.com/watch?v=O6oIrRsZnMQ)) - new treasury, opcodes, LN and more
- Decred staking tutorial - \[2021 updated\] by @Exitus ([youtube](https://www.youtube.com/watch?v=olWfTqw16OQ))
- Exploring Decred and on-chain analysis by Real Vision ([realvision.com](https://www.realvision.com/shows/the-interview-crypto/videos/exploring-decred-and-on-chain-analysis/)) - an interview with @Checkmate, you can see a free sample on [YouTube](https://www.youtube.com/watch?v=SLr-XTqPL4s) (mentions the unprecedented reduction of liquid BTC) or the full episode by signing up on the site
- PTLCs, MRTREEs and offline LN payments by @matheusd ([youtube](https://www.youtube.com/watch?v=m1sQGHUKU7I))
- Decred News Update - $110M treasury decentralization, on-chain governance voting, network ATH & more by @Exitus ([youtube](https://www.youtube.com/watch?v=yX9zfO_2KTo))
- Decred Price Analysis - 24th March 2021 by Josh Olszewicz of Brave New Coin ([youtube](https://www.youtube.com/watch?v=5UyRni0rjHc)) - _Decred slices and dices!_

Audio:

- Decred's Jake Yocom-Piatt on Bitcoin, blockchain governance, DCR, & more by Rachel McIntosh ([youtube](https://www.youtube.com/watch?v=SOoCbr51sus), edited text version at [financemagnates.com](https://www.financemagnates.com/cryptocurrency/interview/decreds-jake-yocom-piatt-on-bitcoin-blockchain-governance-dcr-more/))

Translations:

- Spanish subtitles added to some of the top viewed [channel](https://www.youtube.com/decredchannel)'s videos: [How to Stake](https://www.youtube.com/watch?v=m5lcm6yttEk) tutorial, [Full Node & Tor](https://www.youtube.com/watch?v=B-5O_GBcbV0) on Raspberry Pi, [Governance Walkthrough](https://www.youtube.com/watch?v=1QiC0btcf7E) with @Checkmate, Decred Assembly 15 on [Decred and ASICs](https://www.youtube.com/watch?v=7K2sDhyjQys), Feb 14 [News Update](https://www.youtube.com/watch?v=cZx4azGOvqQ), and the recent [Decred in Depth](https://www.youtube.com/watch?v=O6oIrRsZnMQ) with @matheusd
- Decred Journal February 2021 was [translated](https://xaur.github.io/decred-news/) to Arabic (@arij, @abdulrahman4), Chinese (@Dominic), and Spanish (@francov\_). Thank you all for spreading Decred news!

## Community Discussions

Selected Reddit posts:

- odd [patterns](https://www.reddit.com/r/decred/comments/lzr2w8/decredbitcoin_chart/) on the price chart
- a compilation of [rough edges](https://www.reddit.com/r/decred/comments/m3k31o/161_things_ive_learned/) in mixed staking with Decrediton v1.6.1 and how to workaround them
- invitation to Twitter poll [tournament](https://www.reddit.com/r/decred/comments/m618sa/decred_is_in_the_2021_ultimate_crypto_tournament/) (and the irony of pitching it to a community obsessed with solid voting tech)
- notes on [quantum](https://www.reddit.com/r/decred/comments/m6w2ue/q_re_quantum_resistance/) resistance
- [generating](https://www.reddit.com/r/decred/comments/marjaa/generating_media_for_upcoming_consensus_vote/) media for the latest consensus vote (and challenges of getting the word out)
- March's last [price talk](https://www.reddit.com/r/decred/comments/mg5hhj/has_anybody_noticed_that_decred_has_finally/) again got pretty intelligent and compared Decred to Python

Selected Twitter discussions:

- @jy-p on going in the [opposite](https://twitter.com/behindtext/status/1368655110449094657) direction by creating a fairer opt-in financial system
- @ammarooni [suggests](https://twitter.com/Ammarooni/status/1367655623698096128) to talk more about the USD value locked in tickets because it going above 1 billion is quite an achievement
- @bochinchero has [linked](https://twitter.com/TheBochinchero/status/1375072938106445824) the price rally with rising stake participation, voter turnout and mixing activity, and noted that fungibility is strong when massive:

> Over 43% of the available $DCR supply is now mixed and unspent. Some argue that opt-in privacy or a transparent ledger can never be truly fungible... I honestly can't think of a rational actor that would willingly accept a currency, but reject half of the circulating coins. ([@TheBochinchero](https://twitter.com/TheBochinchero/status/1375072954493636608))

## Markets

In March DCR was trading between USD 140.16-180.60 / BTC 0.00275-0.00310. The average daily rate was $161.01.

@PermabullNino [posted](https://twitter.com/PermabullNino/status/1366915444355964932) that Decred's on-chain data is in beast mode, having settled 4x more native units than Bitcoin in February.

@Checkmate has updated his [comparison](https://twitter.com/_Checkmatey_/status/1369769392884436992) chart of "Lindy Coins" vs Bitcoin as it has rallied from $10K to $58K. DCR continues to stand out.

## 相关外部信息

3月的大型DeFi Dumpster Fire是PAID，遭受了无限造币攻击，攻击者向自己发行了1.8亿美元的PAID，但他们显然只能通过将其转换为其他货币（而不是迅速贬值）来获取300万美元的价值（下降了85％）的付费代币。在验尸中，解释了攻击者获得了原始合同部署者对私钥的访问权，并使用它来“升级”合同，以便他们可以铸造新令牌。快照将用于“重置” PAID令牌，以清除攻击者被发现之前无法出售的令牌。

SushiSwap一直在解决一个重大难题关于如何分配从2020年10月起欠流动性提供商的代币，代币有6个月的“归属期”，而如何分配代币的问题在2021年1月提出。SUSHI持有人已经投票反对直接空投代币并选择了一种索赔机制，该机制将收取索赔人的费用，但随后发现，智能合约的代码已经过编辑，因此通过第三方智能合约（例如Harvest.finance）与之交互的用户无法再对其进行索取。 ，其用户将被欠这些令牌的5-6％）。部署此更新的开发人员给出的原因与“寄生场”将转储其令牌分配有关。最新的是，这些农场可以提交有关如何分配其分配的提案，

Cosmos选民之间已批准了Cosmos“区块链内部通信（IBC）”协议，该协议以1.12亿至75的绝大多数获得批准，它有望实现满足特定条件的区块链之间的安全通信。由于Cosmos是唯一支持该IBC标准的区块链，因此目前还不是很有用，但是其他基于Tendermint的区块链也可能很快也会增加支持。

根据3月5日核心开发者会议的决定，以太坊的EIP 1559已包含在即将到来的伦敦硬分叉中。EIP1559将从根本上改变交易费用的计算和支付方式，并承诺会大幅改善，从而赢得大多数用户和开发者的支持。用户体验。但是，矿工已经表示 反对这一变化，超过60％的人反对这一变化，因为它将干扰他们的一种收入来源。Hasu的分析表明，矿工无论如何都会坚持下去，因为他们仍然可以从区块奖励和矿工可提取价值（MEV）中获得丰厚的利润，而替代方案可以解释为对网络的攻击，并且很可能会破坏ETH。价格（因此是矿工的底线）。

英国税务局已经更新了其处理加密资产的指南，首次涵盖了抵押-这将以与目前处理采矿收入相同的方式进行处理，但可能会为将来的差异化处理敞开大门。

隐私权倡导者@ 6102bitcoin收到一份报告，Bitstamp Europe要求用户在提款后不久向其用户说明使用Wasabi钱包进行的CoinJoin交易，该请求是在活动开始数月后提出的。一份答复指出，实施这些规则的政府对运营商施加了压力，例如法国DASP授权要求以两种方式（入站和出站）检查链上啤酒花。此前Bitstamp所做的消息询问基于荷兰客户共享的个人信息不寻常的数量，包括净资产和年收入，居住证明，以及菲亚特和加密资金的来源。

在显然是错误地删除了他们的频道之后，CoinDesk的YouTube帐户被暂停了大约1天。

兑现加密货币的新方法显然已在俄罗斯普及，“埋藏的宝藏”或将空投的现金滴落到特定坐标上。

## 关于月报

这是Decred Journal的第36期。有关所有问题，镜像和翻译的索引，请参见[这里](https://xaur.github.io/decred-news/)。

在经过最少的健全性检查之后，来自第三方的大多数信息都会直接从来源中继。Decred Journal的作者无权验证所有声明。请当心诈骗，并自行进行调查。

您可以在[此处](https://github.com/xaur/decred-news/labels/next%20release)提交内容，以供撰写下一期月报内容。我们随时欢迎您的[反馈](https://github.com/xaur/decred-news/blob/docs/contributing.md#feedback)和[贡献](https://github.com/xaur/decred-news/blob/docs/contributing.md)。

感谢 (字母排列):

- 写作和编辑: bee, degeri, l1ndseymm, richardred
- 评论和反馈: arij, davecgh, dnldd, jholdstock, JoeGruff, lukebp, matheusd
- 封面图片: saender
- 资助: Decred stakeholders

## 中文社区

* [社区网址](https://blog.dcrclub.org/)
* [微博](https://www.weibo.com/DecredProject)
* [微信公众号](https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzg2NTExNzc3MA==&scene=124#wechat_redirect)
* [中文电报群](https://t.me/decred_cn)
* [bilibili频道](https://space.bilibili.com/425519478)
* QQ群号-258412796

