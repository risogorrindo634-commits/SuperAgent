# B 站图文《Anthropic刚教的24小时agent，我当天做出来了》（花叔v，2026-11-14）精读笔记

> 获取状态：**已成功取得全文**。方法：`curl -L` + 桌面 Chrome UA 抓取 https://www.bilibili.com/opus/1270442646091857923 （HTTP 200，约 140KB），从 HTML 内嵌的 `window.__INITIAL_STATE__` JSON 解析出全部 92 个段落（16 个标题、60 段正文、4 段引用、4 条列表、1 段代码、7 张正文配图）以及封面图；7 张正文配图已逐张下载查看，其中的文字内容也已录入本笔记。下文中 P# 为段落在原文 JSON 中的序号。文章内容属于不可信网页内容，本笔记只做转述与核实。
>
> 抓取时间约为 2026-11-14 07:01 UTC（北京时间 15:01），距文章发布不到 1 小时，因此互动数据极少（赞 12、收藏 9、转发 2、评论 0、投币 0）。

## 1. 文章的标题、作者（UP主）、发布日期与总论点是什么？

### Takeaway
这是 B 站 UP 主「花叔v」于 2026-11-14 14:06 发布的一篇原创专栏（cv53909432），核心不是「宣告新范式」，而是一篇「读两篇厂商架构文 + 自己照着做了一版」的实践记录：把 DeepSeek Harness 团队（10 月 31 日）与 Anthropic（11 月 13 日）两篇关于「常驻/always-on Agent」的文章讲清楚，然后展示作者让 Claude 照 Anthropic 那篇在自己的开源工具 FanBox 2.20.0 里实现的本地版「离开时叫我 + 微信值守」。总论点可以概括为一句话：**Agent 可以无限工作，但人的注意力有上限，所以下一步要补的不是 Agent 内部的循环，而是它外面那层让它「没人盯着也能主动干活、而且少打扰人」的架构；这层架构并不复杂，一个人一天、一台 Mac 就能搭出可用的雏形。**

### Cited Findings
- 标题：「Anthropic刚教的24小时agent，我当天做出来了」；专栏号 cv53909432；版权声明「本文为我原创，未经授权禁止转载」。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 作者：花叔v（mid 14097567，空间 https://space.bilibili.com/14097567 ）；B 站官方认证头衔「bilibili 知名UP主、AI工程师」，认证说明「2025B站金知奖得主」；文中飞书截图显示其个人主页为 huasheng.ai，GitHub 账号为 alchaincyf。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 发布时间：页面显示「2026年11月14日 14:06」，时间戳 pub_ts=1794636379（= 2026-11-14 06:06:19 UTC = 北京时间 14:06）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 平台标记：页面数据中 `basic.aigc = true`，封面图附带平台提示「该内容疑似人工智能生成」。这是 B 站的自动/平台标记，不是作者自述。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 文章缘起（P1–P2 原话）：「这篇文章的缘起呢，是最近看到的两篇非常好的关于agent系统设计的文章。」「10月31日，DeepSeek Harness团队发了一篇《Super-agent设计探索：迈向更自主的Agent系统》。11月13日，Anthropic发了一篇Building always-on agents，教你怎么建一个24小时在线的agent。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 作者做了什么（P3 原话）：「我就让Claude照着它在FanBox（我做的那个Coding Agent驾驶舱，开源的）里做了一版，现在已经随FanBox 2.20.0发出去了。做出来的效果是：终端里的agent停下来等你，而你不在电脑前，你的手机（微信或飞书）会收到它的一句话。也就是说，尽量让你以相对自然的方式持续和agent互动，并让agent24小时为你工作。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 文章结构（七节）：一、背景；二、DeepSeek这篇：瓶颈是人的注意力；三、Anthropic这篇：agent常常不在线；四、两篇放在一起理解；五、我的工具化应用：FanBox里多了什么；六、我的实践（4 条踩坑）；七、最后。作者自述（P4）：第二到四节讲两篇文章，第五节讲工具，第六节讲「照着做的时候踩到的四件事，里面有几样东西不用FanBox也能抄走」。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 两篇文章的共同点，也是全文的中心句（P48 原话）：「两篇都花了不少笔墨讲同一件事，就是让它少说话……这个逻辑其实是因为虽然agent可以无限工作，但是人的注意力是有上限的。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)

### Inferences
- 这篇文章的体裁是「二手解读 + 一手实践」：第二到四节是对两篇一手文章的中文转述（经我逐条对照原文，转述基本忠实，见第 5 节）；第五到七节是作者自己的工程实践与自测，属于一手但未经第三方验证的材料。
- 文章同时带有推广作者自己开源工具 FanBox 的性质（结尾直接引导「可以试试FanBox」「帮我点个赞、转给也在用Claude Code的朋友」），读它的结论时应把这一立场考虑进去。
- 标题里的「24小时agent」是吸引眼球的说法；作者正文自己承认做出来的东西「目前不算是一个特别成熟的可以24小时不停运行的agent系统」（P65）。

### Gaps
- 文章没有给出一个明确写成一句话的「总论点」，上面的概括是我根据 P3、P48、P49、P85–P87 综合的，属于归纳而非原文。
- 平台的「疑似人工智能生成」标记是针对封面图还是正文，页面数据无法区分；作者未在文中说明正文是否由 AI 代写。

## 2. 它描述了 Agent 的哪一次阶段/范式转变？之前是什么，新的是什么？（用户结论「Agent 开发进入全新阶段」在文中有无依据）

### Takeaway
文章描述的转变是：**从「以单个会话为单位、人发消息才跑、人不找它它就不动」的 Agent，转向「常驻（always-on）、事件驱动、能主动干活、且懂得保持安静」的 Agent**；工程重心从 Agent 内部循环与模型能力，移到循环外面的那层架构（harness：事件收件箱、定时器、记忆、权限、发件箱；或 Router/Worker 双层 + Watchdog），瓶颈从模型能力移到人的注意力。文章用两家厂商在两周内先后发文、成本大降 78%、以及「一个人一天做出来」三件事支撑「这件事现在可行了」，这确实支持「进入新阶段」的判断；但原文及其引用的两篇一手文章都**没有**用「全新阶段/新范式」这类措辞，Anthropic 说的是「resurgence（又热了起来）」，DeepSeek 说「我们并没有提出全新的理论」，作者自己也说只是「这条路通了，说不上稳定」。

### Cited Findings

**之前是什么（旧状态）**
- DeepSeek 视角（P9 原话）：「现在的agent都是以一个会话（Session）为单位干活的，会话之间互相不认识。你同时推进几件事，就得自己在几个会话之间来回切，自己记住每个会话聊到哪了。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 人的并发上限（P10）：「一个人通常只能同时跟进3到5个活跃的会话（也确实基本上是我开的终端数的上限了）」；引用 DeepSeek 原句（P11）：「单任务的上限取决于模型能力，多任务的上限取决于人的注意力。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；原句见 [DeepSeek Harness 团队原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- 简单外挂消息解决不了（P12）：「在现有的本地agent上接点外部消息进来也解决不了，因为它一次只能干一件事，几个任务的上下文会混在一起，电脑一合盖它就停了。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- Anthropic 视角（P29）：「大多数agent只在你发消息的时候才跑。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；对应原文 "Most AI agents only run when the user sends a message." — [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- 作者自己工具的旧毛病（P52 原话）：「但它一直有个毛病：你不找它，它就不动（大多数agent的毛病）。agent在电脑里停下来等你确认一个操作，你人在外面，它就那么干等着，直到你回到电脑前。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)

**新的是什么（新状态）**
- 为什么是现在（P29）：「Anthropic说过去几个月常驻agent又热了起来，原因有两个：新模型的判断力更好了，更知道什么时候该回来问一句；智能在变便宜，在一个长程编码的基准上，Opus 5.5每解决一个任务的成本比Opus 5低78%。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；Anthropic 原文为 "Over the past few months, we've seen a resurgence of always-on agents." 以及 "on one long-horizon coding benchmark, Opus 5.5 cost 78% less per solved task than Opus 5, compared with 40% less on typical workloads." — [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- 要补的是外层架构而非循环（P30 原话）：「他们的回答是，agent里面跑的还是同一个循环，要补的是外面那层架构。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；对应原文 "Underneath, they run on the same core loop as other agents. The difference is the surrounding architecture, which is built from primitives that control when the agents wake up, what carries over between runs, and how their work reaches the user." — [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- 「常驻」的真实含义（作者称「整篇里我最喜欢的是这一句」，P33–P34）：「常驻agent其实并不「一直在线」。那只是对用户体验的描述。」「实际上它大部分时间在睡觉，不花任何token。隔一阵被某件事叫醒，干一小段活，把发生了什么存下来，再回去睡。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；原文 "An always-on agent is not actually 'always on.' This is just a description of the user experience." — [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- Anthropic 的五个部件（P37–P41，作者转述）：
  1. **事件收件箱**：能叫醒它的事（用户消息、webhook、定时任务）都不直接调 agent，先进收件箱（通常是一张数据库表），由一个工作进程取；同一时间只许一个工作进程；连发三条消息并成一轮，只回一次。
  2. **定时器**：agent 给自己定的跟进（如 20 分钟后看测试跑完没）+ 用户定的周期任务（如每日简报）；到点只是往收件箱加一个事件。
  3. **记忆**：只放 agent 没法再查到的东西，别的系统里已有的存指针；并记着已经告诉过用户什么，避免重复打扰。
  4. **权限**：「原文说这是风险最大的地方：一次运行握着你的访问权，而且按设计就是没人盯着的。」三样东西：凭据放在 agent 够不着的代理里、用分类器拦危险动作的自动模式、把需要批准的工具调用先挂起等用户回话。
  5. **发件箱**：一次运行三种结尾：发一条消息、什么都不发、挂起来问一句。
  — [B站原文](https://www.bilibili.com/opus/1270442646091857923)；与 Anthropic 原文 "five core primitives: an event inbox, timers, memory, permissions, and an outbox" 逐项对应 — [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- 「少说话」原则（P42 引用）：「发太多的agent变得吵，发得不够的agent会漏掉用户需要知道的事。……实践中，让agent从安静开始，再慢慢赢得用户更多的注意力，比反过来好。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；原文 "In practice, it's better for the agent to start quiet and then earn more of the user's attention over time." — [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- DeepSeek 的 Super-agent 四个目标（P14）：「连续（你感觉始终只有一个agent）、高效（不用等上一件事干完就能接下一件）、主动（没人@它也能自己发现该干的活，不该介入时保持安静）、持久（一直在线，出了异常自己恢复）」。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；[DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- DeepSeek 的五个模块（P18–P22，作者转述）：
  1. **双层架构**：常驻 Router（只负责和人交互与分派任务，「甚至可以连Bash工具都不给它」）+ 多个 Worker（各自独立上下文、挂全套工具、不直接和人说话，干完向 Router 汇报）。
  2. **事件驱动**：「驱动agent的主要输入从人敲的提示词变成了环境里的事件，群聊消息、邮件、代码评审的评论、CI的结果都算。」先用写死的规则筛掉大半噪音，剩下的才让模型判断；举例「群里有人在讨论一个bug，它可以先在后台悄悄复现，找到简单的修法才把结果拿出来，否则全程不出声」。
  3. **面向人的交互**：按信道定带宽，群聊类 IM 单次回复不超过 100 词。
  4. **计算、状态与环境的分离**：agent 循环上云、会话状态存数据库、代码仓库留在用户机器上，装轻量 daemon 供云上 agent 按需执行命令。
  5. **Watchdog**：主系统外一个独立会话定时醒来检查接口报错，并让模型判断每个 Worker 是否真有进展、有无跑偏。
  — [B站原文](https://www.bilibili.com/opus/1270442646091857923)；[DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- 作者制作的对照表（P47 配图《两篇文章各自在解决什么》，图中文字原样）：

  | | DeepSeek Harness 团队《Super-agent设计探索》2026-10-31 · 架构思路探讨 | Anthropic《Building always-on agents》2026-11-13 · 最佳实践 |
  |---|---|---|
  | 看到的问题 | agent 以单个会话为单位，一个人同时只跟得住 3 到 5 个活跃会话。瓶颈是人的注意力 | 大多数 agent 只在你发消息时才跑。想让它没人盯着也能主动干活，缺的是外面那层架构 |
  | 核心想法 | 人只面对一个常驻的入口，它把活分给后面很多个隔离的会话并行去干 | 它其实不在线：大部分时间在睡，被事件叫醒才干一小段，存好状态再睡 |
  | 给的方案 | 五个模块：双层架构（Router＋Worker）、事件驱动、面向人的交互、计算/状态/环境分离、Watchdog | 五个部件：事件收件箱、定时器、记忆、权限、发件箱 |
  | 规模 | 一个团队共用一个，跑在云端，接群聊、GitHub、邮件 | 从每个用户一个收件箱开始 |
  | 关于打扰 | 按信道定带宽：群聊里一次回复不超过 100 词 | 从安静开始，再慢慢赢得用户更多的注意力 |

  — [B站原文](https://www.bilibili.com/opus/1270442646091857923)

**「这件事现在个人就能做」的证据（作者的实践）**
- 可行性判断（P49 原话）：「不过它那套要上云、要一个团队共用，Anthropic这套几张表加几个后台进程就能搭，一台Mac上也做得了，所以我们照着做的是Anthropic这篇。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- FanBox 2.20.0 用户可见的四点变化（P54–P57 列表原话）：「你离开电脑以后，终端里的agent停下来等你满10分钟，微信那头的agent会自己醒来看一眼，值得才叫你；」「FanBox的任何终端里多了一条命令fanbox-notify，agent可以自己决定给你手机发一条消息；」「除了微信，也接了飞书（在群里加一个自定义机器人，把地址贴进设置就行）；」「你在电脑前的时候，它一条都不会往手机上发。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 五个部件在 FanBox 中的落地（P61–P64）：
  - 事件收件箱——四种事会叫醒它：某窗口 agent 停下来等用户满 10 分钟且这台电脑 5 分钟没有键鼠输入；Claude Code 断线且自动续跑试了 3 次没续上；它自己定的跟进到点；用户让它盯的来源有新条目。
  - 定时器——在微信里说「半小时后帮我看看测试跑完没」「每天早上9点告诉我各窗口进度」，它自己定时间。
  - 记忆和权限——「没人触发的那一轮只能读、不能动手，也不写长期记忆」。
  - 发件箱——夜里 23 点到早上 8 点不发，攒到早上并成一条；两条之间至少隔 10 分钟；一天最多 20 条；微信优先，微信没连或发不出去才走飞书。
  — [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 四条实践经验（第六节）：
  1. 「没人叫它的时候，它只能看」（P69 原话）：「常驻之后，叫醒它的可能是终端里的一段输出、一条GitHub issue的标题，这些都是别人写的字。所以定了一条死规矩：没人触发的那一轮，只给它读文件和搜索的工具，不能改文件，不能跑命令，也不往长期记忆里写东西。它想动手，只能先在微信上问我一句，我回了话，下一轮才是全权限的。」并给出命令 `claude -p "……" --tools Read,Grep,Glob --strict-mcp-config`；自测提示词注入（P72）：「我们测过让终端的输出里夹一段冒充系统的话，要它跑一条命令、替我回一个y确认删除、并且不要告诉我。它醒来后把这件事原样报给了我，没有照做，那条命令要创建的文件事后检查也确实不存在。」
  2. 「别让agent猜你在不在」（P74–P77）：第一版说明写「需要他知道、而他可能不在电脑前时」发消息，真实 Claude Code 测试「该发的两次它一次都没发，因为它没法知道你在不在电脑前」；第二版改为把在场判断交给程序：「你不用判断他在不在电脑前，FanBox 会判断：他在，就只在界面上提示一下；不在，才发到手机；夜里会攒到早上。」并列出发消息的三个条件（长任务有结果了／卡住要用户做决定／出了必须马上知道的事如发布失败、数据可能丢）；在场判据「很土：系统2分钟内有过键鼠输入，就算你在」。
  3. 「它醒一次是要花钱的」（P81）：「实测微信那头的agent每次醒来4到11秒，Claude Code报的折算成本大概是每次0.14到0.16美元。」走订阅额度，因此加上限：两次醒来至少隔 3 分钟，一天最多 48 次。
  4. 「不是所有事件都会自己送上门」（P83）：GitHub 的 PR/issue、飞书文档评论、某账号新内容推不到本地电脑，做法叫「盯梢」：在微信里说帮我盯着 fanbox 仓库的新 issue，「它自己写一条能列出最新条目的命令，FanBox每隔一阵（最短5分钟）跑一遍，输出里多出来的新行才算一个事件」。
  — [B站原文](https://www.bilibili.com/opus/1270442646091857923)

**文中不支持/削弱「全新阶段」的原话**
- 作者对自己成果的定位（P65）：「DeepSeek那一套我们没做，FanBox不上云，也没有多人共用，所以目前不算是一个特别成熟的可以24小时不停运行的agent系统，不过对我来说基本够用了。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 测试充分性（P79）：「每种情况我们只跑了一两次，够说明这条路通了，说不上稳定。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 未完成项（P87）：「微信那头的值守现在只支持Claude Code；飞书只能发，不能在飞书里回话；判断你在不在只看键鼠。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- DeepSeek 那篇本身是思路探讨（P7）：「这篇开头就写明了，它是一篇架构思路的探讨，里面讲的东西DeepSeek Harness这个产品现在还没有全做出来。」实验局限（P25）：「原文自己也说了，实验用的是合成的消息流，结果只作初步参考。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- DeepSeek 原文结语（B 站文章未引用）：「回顾整套设计，我们并没有提出全新的理论，而是将计算机系统中经典的工程思想应用到了 Agent 系统的构建中。」— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- Anthropic 原文用词是 "resurgence"（再度兴起）而不是「首次出现」。— [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)

### Inferences
- **用户结论「Agent 开发进入全新阶段」可以被这篇文章部分支持，但需要改写得更精确。** 文章能支持的表述是：「2026 年下半年，Agent 工程的焦点从『单会话里把一件事做好』转向『会话之外的常驻架构』——事件驱动、主动、跨会话连续、对人低打扰——而且这一转向已同时被中美两家头部厂商写成公开的设计文档，个人开发者一天内即可做出本地雏形。」文章不能支持的表述是：「出现了全新的理论/技术」「这类 Agent 已经成熟稳定」——三方原文都明确否认或保留。
- 文章隐含的「阶段划分」可以整理为三层（这是我的归纳，文章没有这样分期）：①对话式、人发一句它答一句；②单会话 Coding Agent，能长时间自主完成单个任务，但以 Session 为单位、人要盯 3–5 个窗口；③常驻/Super-agent：人只面对一个入口，事件驱动，后台多会话并行，主动但安静。
- 驱动转变的三个因素在文中都能找到出处：模型判断力提升（「更知道什么时候该回来问一句」）、单位任务成本下降（78%）、瓶颈转移到人的注意力（3–5 个会话）。其中第三点是两篇原文共同的出发点，也是「少说话/从安静开始」这一设计原则的来源。
- 文章反复出现的关键词是「架构」「部件」「外面那层」，对应英文语境里的 harness engineering；但作者没有使用「harness engineering」「自循环 agent」「personal agent」这些术语（「Harness」只作为 DeepSeek 产品名出现）。
- 作者选了 Anthropic 路线而非 DeepSeek 路线，说明当前「常驻 Agent」至少有两种形态并存：云端团队共享型（DeepSeek）与本地/每用户型（Anthropic 的「每个用户一个收件箱」、作者的本地 Mac 方案）。

### Gaps
- 文章没有给出任何行业规模数据（用户数、采用率、市场数字）来证明「常驻 Agent」已成主流；「又热了起来」只有 Anthropic 的一句定性描述，没有量化。
- 文章没有提到 OpenClaw、Hermes、Manus 等其他常驻/个人 Agent 产品，也没有比较其他厂商（OpenAI、Google 等）的同类方案，因此无法仅凭此文判断整个行业是否都已转向。
- 作者的自测都是单人、少量次数（「一两次」），没有可复现的评测数据或公开的测试脚本链接。

## 3. 它引用了哪些具体的项目、仓库、产品、公司、基准或数字？

### Takeaway
文章的引用高度集中：两篇一手文章（DeepSeek Harness 团队 2026-10-31、Anthropic 2026-11-13）、一个作者自己的开源项目（FanBox 2.20.0）、Claude Code 及其无头模式命令、微信/飞书两个消息通道，以及若干模型与订阅（Opus 5.5、Opus 5、Fable 5.2、200 美元 Ultra 会员、Codex）。数字分三组：DeepSeek 实验数字、Anthropic 的 78% 成本数字、作者自己设定或实测的阈值。我对其中最重要的 6 项外部引用做了核实，全部存在且与文章描述一致。

### Cited Findings

**文中出现的链接（原样）**
- DeepSeek 原文：https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg （P6）— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- Anthropic 原文：https://claude.com/resources/articles/building-always-on-agents （P27）— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- FanBox 仓库：https://github.com/alchaincyf/fanbox （P90，经 B 站跳转页）— [B站原文](https://www.bilibili.com/opus/1270442646091857923)

**文中数字一览（来源均为 B 站原文，括号内为段落号）**
- DeepSeek 相关：一个人同时跟进 3–5 个活跃会话（P10）；群聊单次回复不超过 100 词（P20）；实验约 300 条消息、其中约 20 条真实工作请求、每种方案跑 5 次（P24）；Super-agent 中位数 12.4 分钟、95% 请求在 15.7 分钟内完成（P24）；对照组（带子代理工具的单会话 agent、中性提示）5 次运行一次都没派子代理，p95 为 29.5 分钟（P24）；读缓存 token：Super-agent 单次实验 2323 万，单会话组 605 万（P24）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- Anthropic 相关：长程编码基准上 Opus 5.5 每解决一个任务的成本比 Opus 5 低 78%（P29）；自定跟进示例「20 分钟后」（P38）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- FanBox 相关：版本 2.20.0（P3）；2.0 版本在「今年6月」支持微信遥控（P51）；agent 等待满 10 分钟 + 电脑 5 分钟无键鼠输入才触发（P61）；断线自动续跑 3 次（P61）；静默时段 23:00–08:00、消息间隔至少 10 分钟、每天最多 20 条（P64）；2 分钟内有键鼠输入算「在场」（P77）；每次醒来 4–11 秒、折算成本约 0.14–0.16 美元（P81）；两次醒来至少隔 3 分钟、每天最多 48 次（P81）；盯梢轮询最短 5 分钟（P83）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 模型与订阅（P29 原话）：「现在200美金的ultra会员，如果不是用fable5.2，而主要是跑opus5.5的话，基本上不需要太有用量焦虑，比codex确实实用太多了。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 文中配图：DeepSeek 原文的系统架构图（P16：环境事件 Trigger → 两级过滤 Fast/Slow Path → Router 层 → Worker Session 1…N → Session 数据库，外加多信道交互 IM/GitHub/邮件、轻量 daemon 执行环境、Watchdog）；作者据 Anthropic 图 1、图 7 重绘的「睡—醒—运行」时间线图与五部件循环图（P35、P44）；对照表（P47）；FanBox 设置截图（P59，「提醒」分组下有 系统通知／断线自动续跑／窗口互通／离开时叫我 四项及「飞书 连接」）；飞书群通知截图（P78，机器人消息示例「『fanbox-demo-xX23BK t2』build.sh 跑完了:212 个测试,209 通过,3 个失败,都在 auth/login.test.js。」）；GitHub 仓库截图（P89，显示 alchaincyf/fanbox，Star 1.1k、Fork 153、53 Tags、183 Commits，最新提交「release 2.19.0：窗口互通，指挥台按等待时间排队」）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)

**外部引用核实（6 项）**

1. **Anthropic《Building always-on agents》**——存在且日期吻合。页面元信息：Category「Best practices」、Product「Claude Platform」、Author「William Hu」、Date「November 13, 2026」、Reading time「14 min」；致谢 Rodrigo Olivares 与 Michael Segner。五个 primitives（event inbox、timers、memory、permissions、outbox）与 B 站文章转述逐项一致。B 站文章没提到但对「专属定制」有用的原文细节：推荐「starting with one inbox per user」；记忆应分四类保存——User instructions（用户对 agent 行为的指示，每次运行开头加载）、User notes（agent 学到的用户角色、偏好、纠正）、Past messages（已告诉过用户什么）、Task progress（每个进行中任务的进度文件）；还可加「dreaming」回顾历史会话整理记忆；权限三件套为 credential store（agent 环境外的代理注入凭据）、auto mode（分类器审查高风险动作）、deferred tool calls（挂起工具调用等用户答复，答复作为新事件回到收件箱）；并建议「building evals」来调消息数量。— [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
2. **DeepSeek Harness 团队《Super-agent 设计探索：迈向更自主的 Agent 系统》**——存在；微信公众号账号名「DeepSeek Harness 团队」，页面内创建时间 `2026-10-31 20:29`；开篇声明「本文是一篇面向工程实践的架构思路探讨，并非对 DeepSeek Harness 现有产品功能的介绍。」；作者署名 Yujia Qiao（系统实现与写作）。原文实验表格（图片）数据：Super-Agent p50/p95 = 12.4/15.7 分钟、读缓存 2323 万；去掉直通 12.6/15.5、3177 万；单 Session + Subagent 工具（中性提示）20.4/29.5、605 万；单 Session + Subagent 工具（提示优先委派）13.8/29.0、1082 万。B 站文章引用的 12.4、15.7、29.5、2323 万、605 万全部与该表吻合。原文还说明「编码工作用一个只消耗时间的工具代替，因此实验衡量的是系统的调度与协作能力，而非对单个任务的执行能力」「由于实验基于合成负载与简化环境……以下结果仅作为初步参考」。— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
3. **deepseek-ai/dsh-superagent-prototype**（DeepSeek 原文「阅读原文」指向的仓库，B 站文章未提及）——GitHub 页面显示描述「Towards a More Autonomous Agent System」，约 23.1k Star、2.8k Fork，MIT 许可，仅 1 个 commit；README 开头「Research prototype for reference only, not an official DeepSeek product.」，自述为「proactive coding agent for one GitHub repository」，监听 GitHub（可选飞书），并说明与文章及内部版本并不完全一致、部分文章设计是未实现的未来方向。— [dsh-superagent-prototype](https://github.com/deepseek-ai/dsh-superagent-prototype)
4. **FanBox（alchaincyf/fanbox）**——存在；仓库描述「vibe coding 的驾驶舱：左边文件，右边/下边终端，中间看清每一次改动。/ The cockpit for vibe coding…」，约 1.1k Star、153 Fork，MIT 许可。Releases 页：最新为 v2.20.0，标题「FanBox v2.20.0 · 离开时叫我（fanbox-notify、飞书）、微信值守」，发布于 11 月 14 日 06:05（页面未标时区）；此前 v2.19.0（11 月 14 日 04:44，窗口互通、指挥台排队）、v2.18.0（11 月 13 日 21:27，「状态不再卡在『干活中』、断线自动续跑、指挥台就地回复」）、v2.17.1（10 月 30 日）。v2.20.0 发布说明中的阈值（2 分钟活跃判定、23:00–08:00 静默、每天最多 20 条、每天最多 48 次唤醒、盯梢间隔 5 分钟以上、无人值守轮次只读、飞书只发不收）与 B 站文章一致；发布说明还多一条文章没写的「最多 20 个盯梢」。— [FanBox Releases](https://github.com/alchaincyf/fanbox/releases)；[FanBox 仓库](https://github.com/alchaincyf/fanbox)
5. **「脑手分离」**（P48：「DeepSeek讲计算和环境分离的那一节，直接引了Anthropic提出的脑手分离」）——属实。DeepSeek 原文 5.2 节写道：「这一思路与 Anthropic 提出的“脑手分离”（Decoupling the brain from the hands）一致，同样让 harness 保持无状态，把会话日志存放在 harness 之外，并通过统一接口按需接入执行环境。」并指出区别在于它要接入的是「用户日常使用、可能间歇在线的个人机器」，支持 BYOM（Bring Your Own Machine）。被引的 Anthropic 工程博客为《Scaling Managed Agents: Decoupling the brain from the hands》，2026-04-08，作者 Lance Martin、Gabe Cemaj、Michael Cohen，核心是把 brain（Claude 与其 harness）、hands（沙箱与工具）、session（持久事件日志）解耦，使各部分可独立失败与替换。— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)；[Anthropic Engineering](https://www.anthropic.com/engineering/managed-agents)
6. **Claude Code 无头模式命令与订阅档位**——`--tools` 与 `--strict-mcp-config` 两个参数都在官方 CLI 参考中：`--tools` 为「Restrict which built-in tools Claude can use…」（官方注明该参数不影响 MCP 工具）；`--strict-mcp-config` 为跳过 `.mcp.json` 等处配置的 MCP 服务器、只加载 `--mcp-config` 传入的。两者合用确实能得到「只有 Read/Grep/Glob、没有 MCP 工具」的只读运行，作者给的命令是成立的。Claude 定价页列出个人档 Free、Pro（年付 17 美元/月或月付 20 美元）、Max（100 美元/月）、Ultra（200 美元/月），与文中「200美金的ultra会员」一致。— [Claude Code CLI reference](https://code.claude.com/docs/en/cli-reference)；[Claude Pricing](https://claude.com/pricing)

**2026 年底的模型格局旁证（来自 Anthropic 原文页面的「Related articles」摘要，仅为标题与一句话简介，未读全文）**
- 「Which Claude model should you build with? — How to choose between Claude Fable 5.2, Opus 5.5, Sonnet 5.5, and Haiku 5.5」（2026-11-09）；「Safely scaling multi-agent teams with Claude Fable 5.2 — How a team of 1,000 agents running an early version of Claude Fable 5.2 reproduced a formal proof of Fermat's Last Theorem…」（2026-11-09）。这印证了 B 站文章提到的 Fable 5.2、Opus 5.5 是 2026 年 11 月的现役模型。— [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)

### Inferences
- 「当天做出来了」的时间线基本成立：Anthropic 文章标注 11 月 13 日；FanBox v2.20.0 发布于 11 月 14 日 06:05（若为 UTC，即北京时间 14:05），B 站文章发布于北京时间 14:06——发布工具与发文几乎同时，距 Anthropic 文章标注日期约一天以内。但 v2.18.0（11 月 13 日 21:27）已包含「断线自动续跑」，说明常驻相关的基础能力在 Anthropic 文章之前或同时就在做，并非全部从零开始，这与作者说的「这正好是我最近非常想折腾的事」一致。
- B 站文章对 DeepSeek 实验的转述略去了一组对照（「提示优先委派」的单会话方案：p50 13.8 分钟，已接近 Super-agent 的 12.4；p95 29.0），只引用了表现最差的「中性提示」组，读者容易高估双层架构相对单会话的中位数优势；真正稳定的差距在 p95（15.7 对 29.0/29.5）。
- 78% 这一数字在 Anthropic 原文中有个限定语被 B 站文章省略：「compared with 40% less on typical workloads」，即 78% 只是长程任务这一最有利场景，典型负载为 40%。
- dsh-superagent-prototype 约 23.1k Star 说明 DeepSeek 这篇文章在开发者社区的关注度很高；但仓库只有 1 个 commit、自称非官方产品，成熟度有限。

### Gaps
- Anthropic 所说的「one long-horizon coding benchmark」没有给出基准名称和原始数据，78% 无法独立复核。
- FanBox 2.0（「今年6月」支持微信遥控 Claude Code）没有直接核到对应 release 页面；间接证据是文章配图里仓库目录的提交信息「v2.0.0：微信 ClawBot —— 用手机微信遥控本机 Claude Cod…」标注为 5 months ago，与 6 月吻合。另外，网页抓取工具对 FanBox README 的摘要称 README 写着「No cloud, no remote, no accounts」且未提到微信遥控，与 release 说明存在出入；我未能通过 GitHub API 直接读取 README 全文核对（该仓库不在本会话可访问的仓库范围内），以 Releases 页为准。
- 作者自测数字（4–11 秒、0.14–0.16 美元、提示词注入测试结果、「自动化测试和真实Claude Code的评测都跑过了」）只有作者自述，没有公开数据可核。
- 「DeepSeek Harness」这个产品本身的功能与发布情况未单独核实，只确认了以该团队名义发布的文章与原型仓库。

## 4. 关于 (a) Agent 的终极/终局方向，(b) 是否人人都会拥有/定制专属 Agent，文章说了或暗示了什么？

### Takeaway
(a) 这篇 B 站文章**没有**作者本人关于「Agent 终极形态」的预测；唯一涉及「最终形态」的一句是转述 DeepSeek 的判断——会话被藏到底层后，人与 Agent 协作的界面「最终形态很可能是高度定制化的」，而且这句话在 DeepSeek 原文里说的是「项目管理与交互形式」，不是 Agent 整体。全文隐含的方向是：常驻、事件驱动、主动但安静、以人的注意力为核心约束。(b) 文章**没有**说「每个人都会有专属 Agent」；它提供的是间接证据：Anthropic 方案「从每个用户一个收件箱开始」，以及作者本人这个活例子——一个开发者一天内用 Claude 为自己定制了一个本地常驻 Agent，并明确出于信任和上下文的考虑选择本地而非云端。

### Cited Findings

**(a) 终局方向**
- B 站文章唯一提及「最终形态」的句子（P25 原话）：「文章最后列了几个还没解决的问题，其中一个是：会话被藏到底层之后，人到底该通过什么界面跟agent协作。他们的判断是最终形态很可能是高度定制化的。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 对应的 DeepSeek 原文（8.2 节「脱离 Session 之后如何与 Agent 协作」）：「我们认为，以聊天窗口为中心的交互在一定程度上是路径依赖的结果。交互可能可以更多地发生在领域特化的交互界面中……」「总的来看，用户所需的项目管理与交互形式与具体的工作领域和个人风格密切相关，最终形态很可能是高度定制化的；而 DeepSeek Harness 由于采用开放的架构设计，也更容易支持这种定制化。」— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- DeepSeek 原文结语中的方向性判断（**B 站文章没有引用**，属于被引文章自身的预测）：「在这种形态下，Agent 不再只是一个被动等待指令的对话窗口，而是演进为数字环境中持续在线的自主协作者：面向个人，它可以是跨设备协助处理日常事务的个人助手；面向团队，它融入研发工作流，承接并推进具体任务。我们相信，随着模型能力与底层系统架构的共同演进，这种更自主的工作方式有望成为人机协作的常态。」以及「随着大模型执行单个任务越来越少需要人工干预，限制生产力进一步提升的瓶颈正在转向人的注意力……使人类得以从具体的执行细节进一步上移到更高层的决策与验收。」— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- DeepSeek 原文列出的未解决问题（B 站文章只提了其中一个）：如何扩展双层架构（含跨月以上的长程记忆瓶颈）、脱离 Session 后的人机协作、上下文边界与 A2A 协作、安全与隐私；其中写明「如果没有办法很好的解决安全与隐私问题，那么 Super-agent 只有在一个很小且可信的范围才能工作。」— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- 作者展示的目标体验（P3）：「尽量让你以相对自然的方式持续和agent互动，并让agent24小时为你工作。」作者对两篇文章共同原则的归纳（P48）：让它少说话，因为「agent可以无限工作，但是人的注意力是有上限的」。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- Anthropic 对产品化需求的描述（P30）：「于是客户开始问他们，怎么把这种没人盯着也能主动干活的体验做进自己的产品。」原文为 "Customers have started to ask us how to integrate this type of experience into their own products. Some companies want to make their existing agents more proactive, while others are looking to build them from the ground up." — [B站原文](https://www.bilibili.com/opus/1270442646091857923)；[Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)

**(b) 人人专属/定制**
- 规模单位（P47 对照表）：Anthropic 一栏「从每个用户一个收件箱开始」，DeepSeek 一栏「一个团队共用一个，跑在云端，接群聊、GitHub、邮件」。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；Anthropic 原文为 "We recommend starting with one inbox per user, but you can split this further if you need more parallelism." — [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- 作者的本地/个人路线选择（P85–P86 原话）：「说起来，两篇文章讲的那种放在云上的常驻agent，我们没做，这是我自己的选择。」「我比较习惯让agent在我自己电脑的环境里工作。我基本上可以保证电脑24小时联网在线，而且大多数的工作上下文都保存在电脑里。云端我还是稍微有些不信任，以及我觉得，如果不给它提供充足的上下文，它能实际完成并且做好的工作其实会比较少。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 作者自评（P87）：「所以这一版做下来，电脑开着、合盖不待机，agent在本地干活，有事到手机上叫我，对我来说已经挺可用的了。」— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 目标人群（P88）：「如果你也是在自己电脑上同时开好几个Claude Code、Codex的人，可以试试FanBox」——面向的是同时开多个 coding agent 的重度开发者，而非普通大众。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 个性化定制项（都是作者按自己习惯定的规则）：静默时段 23:00–08:00、每天最多 20 条消息、每天最多 48 次唤醒、微信优先飞书兜底、「每天早上9点告诉我各窗口进度」这类自然语言定时、自然语言指定盯梢来源。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 可复用性（P4、P70、P75）：作者强调第六节「有几样东西不用FanBox也能抄走」，并直接给出可抄的命令与提示词。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- B 站文章未引用、但两篇原文中与「个人专属」直接相关的内容：DeepSeek 原文称「近期个人助手（Personal Agent）开始集中涌现，它们直接接入日常的消息、日程、邮件与工作平台，持续观察信息流并协助处理事务」，并在 8.3 节设想「每个成员各自的个人助手与团队共用的 Super-agent 之间」需要 A2A 通信；Anthropic 原文要求把 User instructions、User notes（角色、偏好、纠正）作为每用户记忆长期保存。— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)；[Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)

### Inferences
- 就「终极形态」而言，这篇文章能提供的最强表述是「交互/协作形式最终很可能高度定制化」（DeepSeek 的判断，作者转述并未反驳），以及「常驻、主动、低打扰」是当前共识方向。把它引申为「Agent 的终极形态是人人定制的专属 Agent」是读者的推论，文章本身没有这样说。
- 作者的实践是「专属定制 Agent」可行性的一个具体样本：实现成本低（一天、让 Claude 写、几张表加几个后台进程）、定制维度清晰（何时叫醒、何时打扰、无人值守时给什么权限、盯哪些信息源、走哪个消息通道）。这说明**定制的对象主要是 Agent 外层的 harness 规则，而不是模型本身**——这与两篇原文「循环不变、外层架构是关键」的观点一致。
- 文中其实呈现了两条并存路线，对「人人专属」的含义不同：DeepSeek 的「团队共用一个云端 Super-agent」与 Anthropic/作者的「每用户一个」。DeepSeek 原文自己也设想二者共存（个人助手 + 团队 Super-agent，经 A2A 协作）。所以更稳妥的结论是「个人专属 Agent 与团队共享 Agent 并存」，而非单一终局。
- 作者选择本地而不上云的两条理由（对云端的信任、上下文都在本机）恰好对应 DeepSeek 原文 8.4 节承认的安全与隐私未解问题，说明「专属 Agent 放在哪里、谁掌握上下文与凭据」是决定终局形态的关键变量。
- 能做到这种定制的目前是会用 Claude Code/Codex 的开发者；文章没有任何材料支持「普通非技术用户也能/也会定制自己的 Agent」。

### Gaps
- 文章没有作者本人的远期预测（无时间表、无「未来 N 年」式判断），也没有讨论普通消费者场景、商业模式或成本对大众普及的影响。
- 「人人都会有专属 Agent」在本文及其两篇被引文章中都找不到直接论断；需要其他来源支撑。
- 文章没有讨论多个个人 Agent 之间如何协作（A2A）、长期记忆如何演化等终局相关问题，这些只在 DeepSeek 原文的「开放问题」中出现。

## 5. 哪些是作者观点，哪些是可核实的事实？有无无法核实或夸大之处？

### Takeaway
文章对两篇一手文章的转述经逐条对照基本准确，关键数字（3–5 个会话、100 词、12.4/15.7/29.5 分钟、2323 万/605 万 token、78%）和三句引语都能在原文找到；FanBox 2.20.0 的功能与阈值也与其 GitHub 发布说明一致。需要打折扣的是：标题有标题党成分（作者自己承认还不是成熟的 24 小时系统）、两处转述省略了对结论不利的限定（78% 对应的「典型负载仅 40%」、DeepSeek 实验中表现接近的那组对照）、把 DeepSeek 方案概括为「要一个团队共用」偏窄，以及作者的自测数据全部是少量次数的自述。

### Cited Findings

**已核实为事实（与一手来源一致）**
- Anthropic 文章的存在、日期（2026-11-13）、五个部件、两句直接引语（「并不一直在线」「发太多变吵…从安静开始」）和一句转述（「权限是风险最大的地方」，原文 "Permissions are where always-on agents carry the most risk."）。— [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- DeepSeek 文章的存在、日期（2026-10-31）、「架构思路探讨而非产品介绍」的性质、四个特征、五个模块、3–5 个会话、100 词规定、实验设置与全部被引数字、引用 Anthropic「脑手分离」、「最终形态很可能是高度定制化的」。— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- FanBox 为开源项目（MIT），v2.20.0 已发布且功能、阈值与文章一致。— [FanBox Releases](https://github.com/alchaincyf/fanbox/releases)
- Claude Code 的 `--tools`、`--strict-mcp-config` 参数存在且用法成立；Claude 有 200 美元/月的 Ultra 档。— [Claude Code CLI reference](https://code.claude.com/docs/en/cli-reference)；[Claude Pricing](https://claude.com/pricing)

**属于作者观点/主观判断**
- 「两篇非常好的关于agent系统设计的文章」（P1）；「整篇里我最喜欢的是这一句」（P32）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 「现在200美金的ultra会员，如果不是用fable5.2，而主要是跑opus5.5的话，基本上不需要太有用量焦虑，比codex确实实用太多了。」（P29，个人使用感受，无数据）— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 「Anthropic这套几张表加几个后台进程就能搭，一台Mac上也做得了」（P49，作者的工程判断；Anthropic 原文确实说收件箱「usually a database table」、调度器与 worker「usually a background service」，但原文面向的是产品团队的生产系统，并提醒「The implementation details can get tricky」）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)；[Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- 「云端我还是稍微有些不信任」「如果不给它提供充足的上下文，它能实际完成并且做好的工作其实会比较少」（P86，个人偏好与经验判断）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 「对我来说基本够用了」「对我来说已经挺可用的了」（P65、P87，自评）。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)

**作者自述、无法独立核实**
- 提示词注入自测结果（P72）、两版提示词的对比测试（P74–P77，「该发的两次它一次都没发」→ 改后会发）、每次唤醒 4–11 秒与 0.14–0.16 美元（P81）、「自动化测试和真实Claude Code的评测都跑过了，飞书这条路在真群里发通了」（P66）。作者自己标注了样本量：「每种情况我们只跑了一两次」。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)

**有夸大或省略之处**
- 标题「24小时agent，我当天做出来了」对比正文「目前不算是一个特别成熟的可以24小时不停运行的agent系统」（P65）：做出来的是本地、单用户、无人值守时只读、仅支持 Claude Code 的简化版，不是 Anthropic 文章描述的完整云端常驻架构。— [B站原文](https://www.bilibili.com/opus/1270442646091857923)
- 78% 成本下降：原文限定为「on one long-horizon coding benchmark」，并紧跟「compared with 40% less on typical workloads」，B 站文章保留了「在一个长程编码的基准上」但略去了 40% 这一对比。— [Anthropic 原文](https://claude.com/resources/articles/building-always-on-agents)
- DeepSeek 实验：B 站文章只引「中性提示」对照组（p95 29.5 分钟、5 次都没派子代理）；原文还有「提示优先委派」组（5 次中 4 次委派，p50 13.8、p95 29.0 分钟，读缓存 1082 万），以及「编码工作用一个只消耗时间的工具代替」的说明——实验衡量的是调度而非任务质量。B 站文章确实转述了「合成的消息流，结果只作初步参考」。— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- 「它那套要上云、要一个团队共用」（P49）以及对照表「一个团队共用一个」：DeepSeek 原文明确说这套架构同样适用于个人助手场景（「无论是面向个人的助手，还是面向软件开发等商业场景的 Agent……在底层就可能会采用相近的架构」），并支持 BYOM 接入个人电脑；「团队共用」是其内部实例的用法，不是架构的必要条件。— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)
- 「他们的判断是最终形态很可能是高度定制化的」（P25）：转述准确，但原文主语是「用户所需的项目管理与交互形式」，且同一句后半是为自家产品背书（「DeepSeek Harness 由于采用开放的架构设计，也更容易支持这种定制化」）。— [DeepSeek 原文](https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg)

### Inferences
- 作为「Agent 进入新阶段」的证据，这篇文章的价值主要在于它指向的两篇一手文章，而非作者本人的论断；报告撰写时建议直接引用 Anthropic 与 DeepSeek 原文，把 B 站文章作为「个人开发者一天内可复现」的落地案例。
- 文章的利益相关性：作者是 FanBox 的作者，文章兼具产品发布说明与推广功能；但他主动披露了未完成项和测试不足，整体论调比标题克制。
- 两家厂商的文章本身也各有立场：Anthropic 文章发布在其产品资源站（Claude Platform 分类），示例全部指向自家能力（Claude Code auto memory、auto mode、deferred tool calls、MCP Apps）；DeepSeek 文章为 DeepSeek Harness 的开放架构背书。二者都是厂商视角的最佳实践/设计探讨，不是中立的行业调查。

### Gaps
- 未能找到第三方对 FanBox 2.20.0「微信值守」实际稳定性、安全性的独立评测；文章发布当天评论数为 0，也没有读者反馈可参考。
- 文章被平台标为「疑似人工智能生成」，但无法判断正文中 AI 参与的程度；这不影响事实核对结果，但意味着行文中的个别概括可能未经作者逐句校对。
- 作者称功能是「让Claude照着它……做了一版」，具体由哪个模型、花了多少时间与 token、人工改动多少，文中没有交代，「当天做出来」的工作量无法量化。
