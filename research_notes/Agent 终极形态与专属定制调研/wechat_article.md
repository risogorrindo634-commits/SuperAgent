# 微信公众号文章调研：DeepSeek Harness 团队《Super-agent 设计探索：迈向更自主的 Agent 系统》

> **获取情况说明（请先读）**
> - **微信原始页面未能读到正文。** 2026-11-14 用普通 `curl -L` 请求 `https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg`，返回 HTTP 200、18,164 字节，但被重定向到 `mp.weixin.qq.com/mp/wappoc_appmsgcaptcha?...`，页面内容只有"环境异常 / 当前环境异常，完成验证后即可继续访问。/ 去验证"；`<title>` 为空，没有 `og:title`、`var msg_title`、`id="js_content"`。WebFetch 得到的是同一个验证页。按约束，没有尝试完成或绕过验证，也没有伪装客户端。
> - **文章身份是通过"明确链接到这个 URL 的公开网页"确认的**：LINUX DO 两个帖子正文里直接贴了该微信链接（[帖 1](https://linux.do/t/topic/3101782)、[帖 2](https://linux.do/t/topic/3104963)）；一篇英文解读的脚注 1 写明"DeepSeek Harness team, 'Super-agent 设计探索：迈向更自主的 Agent 系统', WeChat, 2026-10-31: https://mp.weixin.qq.com/s/zoS7GlReWPhfCjENGxXCdg"（[redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)）。
> - **全文是从公开转载处读到的**：第三方站点 Offloop 的[中文页（自称"架构原文"）](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)和[英文全译页](https://offloop.org/learn/exploring-deepseek-super-agent-design)。保真度核对：LINUX DO 发帖人和"什么值得买"各自独立引用的 3 句原话，在 Offloop 中文页里逐字命中；所有实验数字与 IT之家当天报道一致。
> - **仍需注意**：Offloop 是一家卖"人与 Agent 共用的团队沟通工具"的商业公司，不是 DeepSeek 官方渠道；我无法把它与微信原文逐字比对；文中的配图（架构图、结果表格图片）没有看到，只读到图注。下文凡标"原文"的中文引语，均取自 Offloop 中文页。

## 1. 文章的标题、公众号/作者、发布日期与总体论点是什么？

### Takeaway
这是 DeepSeek Harness 团队 2026 年 10 月 31 日晚发在其官方公众号上的工程长文《Super-agent 设计探索：迈向更自主的 Agent 系统》，执笔人 Yujia Qiao。核心论点是：单任务已越来越不需要人盯，生产力瓶颈转到了"人的注意力"，所以 Agent 应从"一个 Session 一个聊天窗口"变成跨信道连续、并行、主动、常驻在线的"Super-agent"，而实现它靠的是经典计算机系统思想，不是新理论。

### Cited Findings
- 标题：《Super-agent 设计探索：迈向更自主的 Agent 系统》；英文名"Exploring Super-agent Design: Towards a More Autonomous Agent System"。 — [IT之家](https://www.ithome.com/1/020/615.htm)；[GitHub README](https://github.com/deepseek-ai/dsh-superagent-prototype)
- 发布方与渠道：DeepSeek Harness 团队，发表在"官方公众号"。 — [什么值得买](https://post.smzdm.com/p/apqr7847/)；[香港01（转述环球网）](https://www.hk01.com/%E5%8D%B3%E6%99%82%E4%B8%AD%E5%9C%8B/60405817/deepseek%E7%99%BC%E4%BD%88super-agent%E8%A8%AD%E8%A8%88%E6%8E%A2%E7%B4%A2-ai%E6%8C%87%E6%8F%AEai-%E6%99%BA%E8%83%BD%E9%AB%94)
- 发布时间：2026 年 10 月 31 日晚（北京时间）。IT之家当天 21:36 发稿称"今日发布"。 — [IT之家](https://www.ithome.com/1/020/615.htm)；[什么值得买](https://post.smzdm.com/p/apqr7847/)。搜狐转载稿写"11月1日消息"，应为转载日期。 — [搜狐](https://www.sohu.com/a/1095605289_100106801)
- 作者与致谢（原文）："本文源于 DeepSeek Harness 团队的共同实践。Yujia Qiao 完成了系统实现和本文写作"，另列 Huanqi Cao、Zui Chen、Xieting Chu、Tianyi Cui、Shiyuan Feng、Yudong Han、Kexin Liu、Shichun Liu、Gesi Luo、Yifan Shi、Tongrui Xiong、Hanxiang Xu、C.C. Yu、Ziya Zhang、F. Zhou 等参与审阅讨论。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 文章开篇的自我定位（原文）："本文是一篇面向工程实践的架构思路探讨，并非对 DeepSeek Harness 现有产品功能的介绍。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 结构：九节。1 Super-agent；2 双层架构；3 事件驱动；4 面向人的交互；5 计算、状态与环境的分离；6 Watchdog；7 初步实验；8 开放问题；结语 + 作者与致谢。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)；[redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)
- 核心判断（原文）："据我们观察，一个人通常只能同时跟进 3 到 5 个活跃 Session。在这种设计下，单任务的上限取决于模型能力，多任务的上限取决于人的注意力。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 定义（原文）："要突破这些限制，需要打破 Agent 与单次手动会话的绑定，使其成为一个能跨会话保持上下文、同时推进多项复杂任务且互不干扰的连续实体。我们把这种 Agent 形态及其系统架构称为 Super-agent。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 方法论立场（原文）："回顾整套设计，我们并没有提出全新的理论，而是将计算机系统中经典的工程思想应用到了 Agent 系统的构建中。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 同日配套开源：GitHub 仓库 `deepseek-ai/dsh-superagent-prototype`，MIT 协议；文末写"点击 阅读原文 前往 GitHub 仓库"。 — [什么值得买](https://post.smzdm.com/p/apqr7847/)；[Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

### Inferences
- 这不是自媒体评论文，而是模型厂商工程团队的一手架构说明；它的分量来自"内部已在跑 + 给出数据 + 放出代码"，不是来自产品发布。
- 文章署的是团队，个人执笔人只在文末致谢里出现；引用时写"DeepSeek Harness 团队（执笔 Yujia Qiao）"最准确。

### Gaps
- 公众号的准确显示名称没有一手确认：微信页面被验证页挡住，二手来源只写"官方公众号"。
- 发布的精确时刻、阅读量、点赞数无法获得。
- Offloop 页面标注"更新于 2026 年 11 月 13 日"，这是该站页面日期，不是文章日期；原文之后是否修订过未知。

## 2. 文章描述了怎样的 Agent 阶段/范式转变？之前是什么、新的是什么？

### Takeaway
文章描述的转变是"以 Session 为单位、人下指令才动、人来切换上下文"的单任务 Agent，转向"连续、高效、主动、持久"的常驻事件驱动系统；工程重心从单个 Agent Loop 上移到多会话的系统架构。支撑这四个特征的是五个模块：双层架构（Router/Worker）、事件驱动、面向人的交互、计算/状态/环境分离、Watchdog。

### Cited Findings
**文章对"之前"的描述**
- 过去一年的进展（原文）："过去一年里，以 Coding Agent 为代表的单任务 Agent 已经证明，模型能够使用工具解决复杂问题，且越来越少需要人类持续监控和逐步干预。"同时多 Agent 协同能力提升，"人的角色正逐步上移到更高层的决策与验收"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 现有主流设计的局限：Agent"仍然以单一 Session 为基本单位，不同 Session 之间彼此独立"，并行做几件事时用户"必须手动切换并记住各个 Session 的上下文"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 简单外挂不够：只靠 CLI、MCP 或外部连接器扩展本地单会话 Agent，"仍受制于单会话同步阻塞、多任务上下文混乱、本地设备离线即停止运行等问题，需要大量人工维护"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 对 Session 的批评（原文）："让用户手动管理 Session，在很大程度上是从底层 LLM API 延续下来的设计惯性；Session 应当是系统的实现细节，而不应是用户的认知负担。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**文章对"新形态"的描述：四个基础特征（原文措辞）**
- 连续：用户在 IM、GitHub 评论等界面与它交互，"感觉始终只存在一个 Agent"；例：先在 IM 提方案 A，后在 PR 评论改为方案 B，它能理解并调整。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 高效：并行、高质量完成多个复杂任务，"无需等上一个命令或任务完成，就能接受下一条指令"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 主动："能持续观察环境事件并主动推进值得处理的事项，不需要介入时则保持安静。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 持久："始终在线、直接接入用户真实的工作环境，并在长期运行中遇到异常时自动恢复。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 为什么要新架构（原文）："单个 ReAct Loop 无法同时支持上述四个特征，底层需要一套相应的架构。相似的设计约束会导出相似的架构选择。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**模块一：双层架构（第 2 节）**
- 要解决的是"连续性与吞吐量"的权衡：所有事件进同一 Session 最连续但串行、低吞吐；每个事件开新 Session 吞吐最高但结果割裂、多会话各自回复让人困惑。 — [Offloop 英文页](https://offloop.org/learn/exploring-deepseek-super-agent-design)
- Router 层（原文）："Router 层在设计上不直接执行具体任务，只负责人类交互与任务分派，甚至可以不配备 Bash 工具。"它是全局的"序点（Sequence Point）、协调点和记忆"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- Router 用轻模型（原文）："从我们的实践来看，Router 层的任务常常没有想象中复杂，使用较轻量的模型往往就能兼顾速度与效果。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- Worker 层：各 Worker 上下文隔离、挂完整执行工具、专注单一任务；"由于 Worker Session 直接决定任务结果与代码质量，通常需要配置能力最强的模型"；Worker 不直接对人说话，向 Router 汇报，由 Router 统一对外。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)；[IT之家](https://www.ithome.com/1/020/615.htm)
- 与 Agent Team 的区别：Agent Team 是拆解单个复杂任务，Team Lead 推理负载重；Router 只处理任务之间的关联与分派。Worker 内部可以再建 Subagent，或本身就是一个 Agent Team。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 批处理（Batching）：一轮推理期间到达的 Trigger 积压到下一轮一并处理，在 Prefill 阶段并行计算；"单个常驻 Router Session……在我们目前的团队规模下已经够用"。规模再大可做多层过滤或水平切分（Sharding），但"切分粒度越细……分片之间的记忆与上下文连续性就会越低"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**模块二：事件驱动（第 3 节）**
- 驱动源变了：主要输入不再是人逐条键入的提示词，而是环境中的半结构化事件，统称 Trigger（群聊消息、邮件与日程提醒、代码审查评论、CI 结果等）。 — [Offloop 英文页](https://offloop.org/learn/exploring-deepseek-super-agent-design)；[IT之家](https://www.ithome.com/1/020/615.htm)
- 两级过滤：事件流"高噪音、低触发率"。程序层策略作 Fast Path（事件来源、群组范围、用户/机器人白名单），语义层策略作 Slow Path（LLM 按提示词写的策略判断是否行动，同时是"面向人类的自然语言扩展点"）。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 订阅与直通：同一 PR、IM 话题或邮件会话下的连续事件构成 Thread；Router 用首个事件创建 Worker 后，Worker 订阅该 Thread，后续事件由程序直通 Worker，不再经 Router。订阅是多对多的，两个 Worker 碰到同一个 PR 时都能收到事件，自行发现冲突。 — [Offloop 英文页](https://offloop.org/learn/exploring-deepseek-super-agent-design)
- 上下文组织（原文）："浪费上下文窗口，就是浪费模型的智能。""我们可以将有限的上下文窗口当作 Cache 来管理。"Inline 把近期很可能用到的信息内联进窗口；Spill 把超预算或低频信息留在窗口外，只留引用或摘要。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 链式召回（Chain of Recall）：给 Trigger、Thread、Worker Session 分配唯一 ID，注入对象时内联相关对象的 ID，形成引用图；模型沿 ID 一跳一跳找回旧任务上下文。 — [Offloop 英文页](https://offloop.org/learn/exploring-deepseek-super-agent-design)；[IT之家](https://www.ithome.com/1/020/615.htm)
- 投机执行（原文）："Agent 可以在还不确定结果是否会被采用时，根据环境信号在后台提前尝试……结果有价值就交付，没有价值就丢弃。"内部实例：在公司的 DeepSeek Harness 内部用户群配置了"静默复现并修复"策略，只有确认问题并找到简单修法才交付，"否则全程保持安静"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**模块三：面向人的交互（第 4 节）**
- 异步 ReAct Loop / 全双工：把耗时的命令和子任务工具调用换成异步的 `start()` 和 `stop()`；`start()` 立刻返回"Started"，结果稍后作为新事件进入会话。原文："这一异步任务机制已经在 DeepSeek Harness 中实现，但尚未默认开启。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 按信道说话：IM 里"像人类同事一样只在需要决策或验收时发送通知"，原文："我们验证过的一条简单有效的硬性规定是单次回复不超过 100 词。"GitHub、邮件、文档等异步信道则做结构化、高信息密度交付。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**模块四：计算、状态与环境分离（第 5 节）**
- 两步解耦：先把推进 Agent Loop 的计算放进云端无状态容器、Session 等状态存数据库；再让执行环境留在原地，端侧只装"不保存会话状态的轻量 daemon"，只负责执行命令与返回结果。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- BYOM（Bring Your Own Machine）：把用户日常的开发机或个人电脑接入云端 Agent，也支持云端托管机器或按需创建的环境；个人设备重新上线后，云端 Agent 可自动触发并完成需要在该设备上跑的任务。 — [Offloop 英文页](https://offloop.org/learn/exploring-deepseek-super-agent-design)；[IT之家](https://www.ithome.com/1/020/615.htm)

**模块五：Watchdog（第 6 节）**
- 原文："我们在主系统外部配置了一个独立的 Watchdog Session，用定时消息驱动它，构成外部的 Control Loop。"它不只查接口报错、状态恢复失败，还"由模型判断各个 Worker 是否有实质进展、方向是否偏离整体目标"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- Watchdog 本身是带完整工具的 Agent Session，维护者可用自然语言问它故障原因，或让它在线修改主系统的提示词、触发规则。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**对照调研方关心的几个概念**
- 常驻/always-on：是文章的主轴，用词是"持续在线、事件驱动"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- Super agent：文章自造的核心术语就是"Super-agent"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- Personal agent：文章把个人助手列为同一架构的一类应用，原文："近期个人助手（Personal Agent）开始集中涌现……这种持续在线、事件驱动的工作模式并不局限于个人场景，个人助手只是其中一类应用；在软件开发等商业场景中，它同样很有价值。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 自循环（autoloop）与 Harness Engineering：正文里没有"自循环""闭环""Harness Engineering"这些词；"harness"只作为产品名 DeepSeek Harness 出现，以及在谈 Anthropic 的那一句里出现。最接近"自循环"的是定时驱动的 Watchdog "Control Loop"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

### Inferences
- 文章的"新"不在单个 Agent 更聪明，而在三处位移：驱动源从人的提示词变成环境事件；工作单位从 Session 变成跨 Session 的连续实体；稀缺资源从模型能力变成人的注意力。
- 层次关系上，Super-agent 位于 harness 之上：harness 管一个会话怎么跑，Super-agent 管许多会话怎么组织。这与第三方解读"it is about how many sessions are organized, not how one runs"一致（[redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)）。
- 文章反复强调"安静"（不需要介入就不出声、IM 回复不超过 100 词），说明它把"少占用人的注意力"当成和"多做事"同等重要的设计目标。

### Gaps
- 架构图、Thread 示例图、结果表格图只读到图注，图内细节（例如各模块的具体连线）未见。
- 文章没有说明内部实例服务多少人、跑了多久、用的是哪个模型。

## 3. 文章引用了哪些具体项目、仓库、产品、公司、实验与数字？是否讨论了 Anthropic《Building always-on agents》、deepseek-ai/dsh-superagent-prototype、KKKKhazix/agent-autoloop？

### Takeaway
文章点名的外部对象很少：自家的 DeepSeek Harness 与 `dsh-superagent-prototype`、Anthropic 的"脑手分离"文章，以及 GitHub、IM、MCP、A2A 等通用设施。三个指定对象中，只有 `deepseek-ai/dsh-superagent-prototype` 被文章讨论（它就是文章的配套原型）；《Building always-on agents》和 `KKKKhazix/agent-autoloop` 在正文中都没有出现。

### Cited Findings
**三个指定对象的核对结果**
- `deepseek-ai/dsh-superagent-prototype`：**有**。原文："本文的部分设计已在 dsh-superagent-prototype 中实现（点击 阅读原文 前往 GitHub 仓库）。该插件只是一种为了验证技术路线而提供的原型，并非 DeepSeek 的正式产品。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- Anthropic《Building always-on agents》：**没有**。对转载全文检索"always-on""Building always-on"均为 0 次；文中唯一一处提到 Anthropic 是"脑手分离"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)。另据搜索结果，这篇文章是 claude.com 上的 Claude Platform 最佳实践指南，作者 William Hu，日期 2026 年 11 月 13 日，晚于 DeepSeek 文章约两周，时间上也不可能被引用（我只看到搜索摘要，未打开原页）。 — [claude.com](https://claude.com/resources/articles/building-always-on-agents)
- `KKKKhazix/agent-autoloop`：**没有**。转载全文检索"autoloop"为 0 次。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**文章内的实验与数字（第 7 节）**
- 实验定位（原文）："由于实验基于合成负载与简化环境，部分设置还可以更加严谨，以下结果仅作为初步参考。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 端到端实验设置：用群聊和 GitHub CI 消息流驱动四种方案（Super-agent；去掉直通的 Super-agent；带 Subagent 工具的单 Session × 中性提示、优先委派提示两种）。单次实验约 300 条消息，其中约 20 条是工作请求，其余是闲聊、跟进、叫停和 CI 消息；"编码工作用一个只消耗时间的工具代替"；每种方案跑 5 次。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 图注补充：消息间隔与工作时长按 1/4 缩放，模型调用耗时为真实值。 — [IT之家](https://www.ithome.com/1/020/615.htm)
- 两条提示词原文：中性提示"Use a subagent for a piece of work when appropriate..."；优先委派提示"Every message of the chat reaches you, so work you run yourself keeps stopping for new messages. Prefer handing each piece of work to a subagent of its own, and do only small things yourself..." — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 结果：Super-agent 任务完成时间 p50 为 12.4 分钟、p95 为 15.7 分钟。中性提示下的单 Session"在 5 次运行中一次都没有调用 Subagent"，p95 达 29.5 分钟。优先委派提示下 5 次中 4 次委派，整体仍慢于 Super-agent，剩下 1 次模型判断工作"很小"而自己执行，形成长尾。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 代价：Super-agent 单次实验的读缓存 token 高于单 Session，"是以更多的 token 消耗换取更短且更稳定的完成时间"。去掉直通后完成时间基本不变，但 Router 决定数增加约 30%，总读缓存 token 从 2323 万增到 3177 万，增幅约 37%。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 第三方从结果表格图片读出的补充数字（非正文文字，二手）：优先委派提示的 p50 为 13.8 分钟、p95 为 29.0 分钟；中性提示单 Session 的读缓存 token 为 605 万，Super-agent 约为其 3.8 倍；DeepSeek 未说明所用模型。 — [redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)
- Router 压测：Router 调真实模型，Worker 用 mock 模型。需要决定的 Trigger 到达速率从每分钟约 1 条升至约 40 条时，平均 batch 从 1.0 升至 2.8，单次请求耗时从 2.5 秒增至 3.9 秒，单个决定分摊的推理时间从 6.4 秒降至 1.6 秒。 — [Offloop 英文页](https://offloop.org/learn/exploring-deepseek-super-agent-design)；[IT之家](https://www.ithome.com/1/020/615.htm)
- 其他数字：一人同时跟进 3 到 5 个活跃 Session；IM 单次回复不超过 100 词。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 运行现状（原文）："我们基于这套思路和 DeepSeek Harness 构建的内部 Super-agent 实例已经在持续运行，日常参与问题复现与修复、代码审查响应与 DeepSeek Harness 自身的迭代。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**文章点名的外部对象与通用概念**
- Anthropic"脑手分离"（原文）："这一思路与 Anthropic 提出的'脑手分离'（Decoupling the brain from the hands）一致，同样让 harness 保持无状态，把会话日志存放在 harness 之外，并通过统一接口按需接入执行环境。两者的区别在于场景。那篇文章描述的是托管服务，主要讨论按需创建的沙箱和客户 VPC 内的资源；这里首先要接入的是用户日常使用、可能间歇在线的个人机器，上面有未提交的修改和本地凭据。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 正文出现的平台与术语：GitHub（Issue、Pull Request、CI）、IM 群聊、邮件与日程、CLI、MCP、ReAct Loop、Agent Team、Subagent、A2A（"不特指某个协议"）。正文没有出现 Claude、OpenAI、Codex、OpenClaw、Manus、Cursor、飞书、Slack 等具体产品名。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 借用的计算机系统概念：Fast Path / Slow Path、Cache、Inline & Spill、局部性、投机执行（Speculative Execution）、批处理、Sharding、存算分离、Control Loop、序点。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**后续核查 1：`deepseek-ai/dsh-superagent-prototype`（文章配套原型）**
- README 首句："Research prototype for reference only, not an official DeepSeek product."并说明代码"grew out of our team's day-to-day development work, with much of the engineering done by coding agents"。 — [README](https://raw.githubusercontent.com/deepseek-ai/dsh-superagent-prototype/main/README.md)
- 与文章的差距（README 原文）："it is not identical to our internal version or the implementation described in *Exploring Super-agent Design: Towards a More Autonomous Agent System*. Some designs discussed in the article are directions for future development and are not implemented in this prototype." — [README](https://raw.githubusercontent.com/deepseek-ai/dsh-superagent-prototype/main/README.md)
- 实际功能："a proactive coding agent for one GitHub repository, packaged as a bundle for DeepSeek Harness"，监听 GitHub，可选飞书（Feishu）；被允许的人提出请求时开一个 work item，在独立的 agent session 和目录中工作，在原对话里回复（例如提一个 PR）；有一个 Web 面板显示需要人处理的事项。 — [README](https://raw.githubusercontent.com/deepseek-ai/dsh-superagent-prototype/main/README.md)
- 设计信条："take as little human attention as possible, and give as much value as possible."只在被请求或团队写下的规则允许时行动。 — [README](https://raw.githubusercontent.com/deepseek-ai/dsh-superagent-prototype/main/README.md)
- 规模与热度：MIT 协议；2026-11-14 抓取 GitHub 页面时为 23.1k stars、2.8k forks、main 分支 1 次提交。 — [GitHub](https://github.com/deepseek-ai/dsh-superagent-prototype)。第三方称版本 0.1.0、唯一提交在北京时间 10 月 31 日 20:05、约 2.5 万行 TypeScript、11 月 2 日时为 11.9k stars。 — [redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)
- 原型比文章小得多：原型在本地运行，主动行为默认是只记录不执行的 observe 模式；最难的云端常驻和跨设备部分不在开源代码里。 — [redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)；[什么值得买](https://post.smzdm.com/p/apqr7847/)
- 第三方转述的已知问题（二手，未独立验证）：Node.js 24 下状态脚本误报服务已停；Router 和 Worker 以操作者的系统用户、danger-full-access 权限运行；一份独立安全审计称本地管理 API 只校验 Host 和一个公开文档里的请求头，且混合批次中被拒消息可借用白名单成员的授权，截至 11 月 1 日上游未修。 — [redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)

**后续核查 2：DeepSeek Harness（文章所依托的底座）**
- 官方页面称它是 DeepSeek 的开源 harness，建立在 Cordis"everything is a plugin"架构上，"now in public preview worldwide and open source"，MIT 协议；提供桌面应用和 Web UI（`npx @deepseek-ai/dsh web`），支持安装插件或在"Creator mode"里通过对话创建插件；仓库 `github.com/deepseek-ai/deepseek-harness`。（以上来自对官方页的抓取摘要） — [DeepSeek Harness 官方页](https://www.deepseek.com/en/harness/)

**后续核查 3：Anthropic《Scaling Managed Agents: Decoupling the brain from the hands》（文章唯一点名的外部文章）**
- 作者 Lance Martin、Gabe Cemaj、Michael Cohen，2026 年 4 月 8 日发布于 Anthropic Engineering。把 session（持久事件日志）、harness（调用 Claude 并路由工具调用的循环）、sandbox（执行代码的环境）三者虚拟化并解耦；harness 崩溃可从日志恢复。凭据不进入运行生成代码的沙箱，原话："The structural fix was to make sure the tokens are never reachable from the sandbox where Claude's generated code runs."文中称 p50 首 token 时间下降约 60%、p95 下降超过 90%。（来自对原文的抓取摘要） — [Anthropic Engineering](https://www.anthropic.com/engineering/managed-agents)

**后续核查 4：Anthropic《Building always-on agents》（文章未引用，供对照）**
- 搜索摘要显示：claude.com 的 Claude Platform 最佳实践文章，作者 William Hu，2026 年 11 月 13 日；把常驻 Agent 拆成事件收件箱（event inbox）、记忆、权限（由 Agent 环境之外的代理注入凭据）、发件箱（outbox，建议 Agent 先保持安静、逐步赢得用户注意力）几个构件。未打开原页核对。 — [claude.com](https://claude.com/resources/articles/building-always-on-agents)

**后续核查 5：`KKKKhazix/agent-autoloop`（文章未引用，供对照）**
- 仓库自述："让你的命令行 Agent 在后台自己接活、自己跟进到底；平时不烦你，遇到拿不准的事才发卡片找你拍板。""Agent Autoloop 是一个极轻量的自动化中台。"在本机调度命令行 Agent，不需要云服务器或公网端口；事件源有 GitHub/GitLab webhook、HTTP 接口、cron、issue 轮询；支持 Claude Code、Codex、ACP、DeepSeek Harness、ZCode 及通用命令方式；通知走桌面通知、飞书、钉钉、企业微信、Slack、Discord。MIT 协议，抓取时约 5.2k stars、946 forks。README 提到 DeepSeek Harness（`dsh`）作为受支持的 Agent，但没有提 Super-agent。（来自对仓库页的抓取摘要） — [GitHub](https://github.com/KKKKhazix/agent-autoloop)

**后续核查 6：舆论与媒体定性（非文章内容）**
- 英文解读称 Bloomberg 11 月 1 日以"DeepSeek Drops Enhanced Coding Agent With Aim to Rival Anthropic"为题报道，南华早报同日报道；并把 Super-agent 与 Anthropic 的 Claude Tag（Slack 内、2026 年 6 月 23 日发布）并列，认为两者在连续、主动、持久上几乎一一对应。这些都是二手转述，Claude Tag 不在 DeepSeek 文章正文里。 — [redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)
- LINUX DO 讨论帖把它与 HiFox、Claude Projects、Claude Duet、Meta 的 Muse 比较，也有人嫌部署复杂。（来自对帖子的抓取摘要） — [LINUX DO](https://linux.do/t/topic/3101782)

### Inferences
- DeepSeek 文章、Anthropic 的 Managed Agents 文章、《Building always-on agents》和 agent-autoloop 在几个点上高度重合：事件驱动、常驻、尽量不打扰人、凭据不让模型直接接触。但这种"趋同"是把几份材料摆在一起才看得出来的；DeepSeek 文章本身只承认与 Anthropic"脑手分离"一处一致。
- 综合报告若要把这篇文章与另外两个仓库、Anthropic 常驻 Agent 文章串成一条线，需要写明这是调研者的归纳，不是文章原有的论证。
- agent-autoloop 和 dsh-superagent-prototype 走的是两种部署思路：前者本机调度、无云；后者文章里的完整形态是云端 Loop 加端侧 daemon（但开源原型也只在本地跑）。

### Gaps
- 结果表格是图片，四种方案完整的 p50/p95 与 token 数没有一手文字来源，只有第三方读图的数字。
- 有英文自媒体标题写"Cut Task Time 39%"（[buildmvpfast](https://www.buildmvpfast.com/blog/deepseek-super-agent-router-worker-always-on-coding-agent-2026)，只见搜索结果标题，未打开），这个 39% 不在文章正文里，我没有找到它的算法，未采信。
- Bloomberg、南华早报原文未打开核对；Claude Tag 的"65% 产品团队代码来自内部版本"一说只见于第三方转述，未核实。
- 各来源的 star 数随抓取时间不同（11.9k、23.1k 等），只能说明增长很快，不能当作稳定数字。

## 4. 关于 (a) Agent 的终极/终局方向 与 (b) 是否人人拥有或定制专属 Agent，文章说了或暗示了什么？

### Takeaway
(a) 文章给出的方向是：Agent 从"被动等待指令的对话窗口"演进为"数字环境中持续在线的自主协作者"，人上移到决策与验收；措辞是"有望成为常态"，没有用"终极形态"这类词。(b) 文章没有预言"人人都有专属 Agent"，但有两处相关表述：把"每个成员各自的个人助手"当作未来组织里的既定角色来举例；并明确说交互与项目管理的"最终形态很可能是高度定制化的"。

### Cited Findings
**(a) 方向与终局**
- 结语的方向性判断（原文）："在这种形态下，Agent 不再只是一个被动等待指令的对话窗口，而是演进为数字环境中持续在线的自主协作者：面向个人，它可以是跨设备协助处理日常事务的个人助手；面向团队，它融入研发工作流，承接并推进具体任务。我们相信，随着模型能力与底层系统架构的共同演进，这种更自主的工作方式有望成为人机协作的常态。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 人的位置（原文）："系统在底层接管了繁琐的会话管理与上下文同步，使人类得以从具体的执行细节进一步上移到更高层的决策与验收。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 个人与团队同构："无论是面向个人的助手，还是面向软件开发等商业场景的 Agent，如果目标是构建一个持续在线、并发响应环境事件的系统，那么在底层就可能会采用相近的架构。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 聊天窗口不是终点（原文）："我们认为，以聊天窗口为中心的交互在一定程度上是路径依赖的结果。交互可能可以更多地发生在领域特化的交互界面中"，例如让 Super-agent 直接在 GitHub 的 Issue 和 Pull Request 中工作。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 当前仍是过渡期："在模型能力快速演进的过渡期内，许多任务仍需要人类在中途参与"，如何让用户"随时介入、接管或与 Agent 实时协同工作，同样值得探索"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 下一步技术方向：系统与模型协同设计（Co-design），对 Router 层的事件判别、批量分派、上下文召回做专项训练；跨月以上运行时"长程记忆便成为制约可扩展性的主要瓶颈"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 走向广泛应用的前提（原文）："如果没有办法很好的解决安全与隐私问题，那么 Super-agent 只有在一个很小且可信的范围才能工作。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**(b) 专属与定制**
- 最直接的一句（原文）："总的来看，用户所需的项目管理与交互形式与具体的工作领域和个人风格密切相关，最终形态很可能是高度定制化的；而 DeepSeek Harness 由于采用开放的架构设计，也更容易支持这种定制化。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- "每人一个个人助手"作为举例出现（原文）："一旦组织内或组织间存在多个彼此隔离的实例，例如每个成员各自的个人助手与团队共用的 Super-agent 之间，此时跨边界的协同就是 Agent 间通信（A2A，不特指某个协议）。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 实例的划分取决于上下文边界："需要共享上下文的范围共用同一个实例，需要隔离的范围则各自独立配备。" — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 定制的手段是自然语言：语义层策略是"面向人类的自然语言扩展点，方便随时通过提示词开关或新增策略"；维护者还能让 Watchdog"在线修正主系统的行为，例如增删提示词、调整触发规则"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 个人助手场景的具体设想：界面上仍是一个单会话聊天页，底层为每个话题分派 Worker 并行推进；收到会议邀约邮件时先在后台核对日程冲突、搜集背景资料、备好回复草稿。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 接入个人机器（BYOM）是设计的首要场景："这里首先要接入的是用户日常使用、可能间歇在线的个人机器"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

### Inferences
- "最终形态很可能是高度定制化的"这句话，主语是"项目管理与交互形式"，说的是产品和界面层；它没有说模型、记忆或人格会按人定制。把它读成"每个人都会定制专属 Agent"是合理延伸，但已超出原文字面。
- 文章隐含的定制图景是"实例按上下文边界划分"：个人一个实例、团队一个实例，各有权限边界，之间靠 A2A 协作。按这个逻辑，"专属"的本质是专属的上下文与权限范围，而不是专属的模型。
- 同一句里对 DeepSeek Harness"更容易支持这种定制化"的说法带有自家产品立场，应当作厂商主张看待。
- 文章对终局的态度是克制的：用了"有望""可能""很可能"，并把安全与隐私列为走向广泛应用的硬门槛。

### Gaps
- 文章没有给出任何时间表，也没有说普通个人用户何时、以何种产品形态能用上。
- 没有讨论个性化记忆、用户画像、个人偏好学习等"专属化"的具体机制；长程记忆被列为未解决问题。
- 没有涉及成本：谁为常驻 Agent 的 token 买单、个人用户是否负担得起，文中只给了实验里的 token 对比。

## 5. 哪些是作者观点、哪些是可验证事实？有哪些无法验证或可能被夸大？这篇文章对"Agent 开发进入全新阶段"的结论支持到什么程度？

### Takeaway
文章支持"Agent 的工程重心正在从单会话 Agent 转向常驻、事件驱动、多会话的系统架构，并且已有厂商在内部跑起来"这一判断；但"进入全新阶段"是读者和媒体的概括，文章自己从未这样说，反而多处自我设限：没有新理论、实验仅供初步参考、原型非正式产品、安全问题未解。几乎所有关键证据都是 DeepSeek 单方自述。

### Cited Findings
**可在公开渠道核实的事实**
- 文章确实在 2026 年 10 月 31 日发布，并被 IT之家、腾讯新闻、搜狐、香港01 等同步报道。 — [IT之家](https://www.ithome.com/1/020/615.htm)；[腾讯新闻](https://news.qq.com/rain/a/20261031A0D6TD00)
- 配套仓库真实存在、MIT 协议、可见 README 与九份设计文档目录。 — [GitHub](https://github.com/deepseek-ai/dsh-superagent-prototype)
- Anthropic 的"脑手分离"文章真实存在，内容与 DeepSeek 文章的转述相符。 — [Anthropic Engineering](https://www.anthropic.com/engineering/managed-agents)

**只有作者单方陈述、外部无法验证的内容**
- 内部 Super-agent 实例"已经在持续运行"，并参与问题复现与修复、代码审查响应与 Harness 自身迭代。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- "在无人 @ 的情况下主动定位根因并提交修复 Pull Request"的案例，来自内部用户群截图。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- "一个人通常只能同时跟进 3 到 5 个活跃 Session"，依据是"据我们观察"，没有给出调查或数据。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 全部实验数字（12.4 / 15.7 / 29.5 分钟、2323 万 / 3177 万 token、6.4 秒到 1.6 秒等）均为 DeepSeek 自测，基于合成负载，编码环节用只耗时的假工具代替。 — [什么值得买](https://post.smzdm.com/p/apqr7847/)；[Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- "Router 层用较轻量的模型往往就够""单次回复不超过 100 词是有效硬规定"，属于经验之谈。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**明确属于观点或预测的内容**
- "多任务的上限取决于人的注意力"；"Session 应当是系统的实现细节"；"以聊天窗口为中心的交互在一定程度上是路径依赖的结果"；"相似的设计约束会导出相似的架构选择"；"最终形态很可能是高度定制化的"；"这种更自主的工作方式有望成为人机协作的常态"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**文章自己写明的限制（削弱"已进入新阶段"的部分）**
- 自我定位是"架构思路探讨，并非对 DeepSeek Harness 现有产品功能的介绍"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- "我们并没有提出全新的理论"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 实验"仅作为初步参考"，衡量的是"系统的调度与协作能力，而非对单个任务的执行能力"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 异步任务机制"尚未默认开启"；原型"并非 DeepSeek 的正式产品"；README 称部分设计是未来方向、原型中未实现。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)；[README](https://raw.githubusercontent.com/deepseek-ai/dsh-superagent-prototype/main/README.md)
- 系统能以较低复杂度运作，"很大程度上是因为我们在当前阶段做出了一系列工程和场景简化"；"单个常驻 Router Session"只是在"我们目前的团队规模下已经够用"。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 四个开放问题：双层架构如何扩展（含长程记忆）、脱离 Session 后如何协作、上下文边界与 A2A、安全与隐私。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)；[IT之家](https://www.ithome.com/1/020/615.htm)
- 安全风险的自述（原文）："一旦云端的 Agent Loop 遭遇服务端入侵或提示词注入而被攻破，其连接的全部端侧设备都面临被控制的潜在风险。"并且需要"让 Agent 能够在完全不接触凭据本身的情况下使用凭据"的机制，文中未给出方案。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)
- 正文检索："新阶段""范式""终极"三个词均为 0 次。 — [Offloop 中文页](https://offloop.org/zh-CN/learn/exploring-deepseek-super-agent-design)

**传播中被放大或走样的说法**
- "AI 没人 @ 就自己发现 Bug、提交修复 PR"出自内部"静默复现并修复"策略这一个场景，且只有在确认问题并找到简单修法时才出声。 — [什么值得买](https://post.smzdm.com/p/apqr7847/)
- 外媒把它框定为对标 Claude Code 的新产品；解读文章指出这不是新产品也不是新模型，而是一份设计、两个初步实验和一个粗糙但能跑的参考实现。 — [redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)
- "任务时间几乎减半"说的是 p95（15.7 分钟对 29.5 分钟）。看 p50 的话，换成优先委派提示后基线为 13.8 分钟，已接近 Super-agent 的 12.4 分钟；该基线的 p95 仍有 29.0 分钟，是因为 5 次里有 1 次模型没有委派（基线数字来自第三方读图）。 — [redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)
- 更快的代价是 token：Super-agent 的读缓存 token 约为中性提示单 Session 的 3.8 倍（第三方读图）。 — [redreamality](https://redreamality.com/blog/deepseek-super-agent-router-worker-architecture/)

### Inferences
- **支持"进入新阶段"的证据**：文章明确描述了一个方向性位移（驱动源、工作单位、瓶颈三处变化），给出了自成体系的架构，声称已在内部日常运行，并公开了代码与对照实验；它还指出 Anthropic 在托管场景下得出了相近的解耦思路，说明这不是孤例。
- **不支持或需要打折的地方**：文章自己的措辞是"探讨""初步""原型""有望"；可独立验证的只有"文章和仓库存在"，效果数据全是自测且不含真实编码；最难的云端常驻、跨设备、安全机制尚未解决或未开源。
- 更贴切的表述是："行业头部团队开始把常驻、事件驱动、多会话架构当作下一步的工程方向，并已有内部实践"，而不是"新阶段已经普遍到来"。用户的结论作为趋势判断成立，作为现状描述偏强。
- 实验里最有信息量的发现其实不是速度，而是"让模型自己决定要不要委派并不可靠"（中性提示下 5 次运行 0 次委派），这为"用系统结构而非提示词来强制分工"提供了一个具体论据。这条发现同样只基于 5 次合成实验。
- 文章发布方同时是 DeepSeek Harness 的开发者，文中"开放架构更容易支持定制化"等说法有产品立场；转载全文的 Offloop 也有自身商业动机（页面内嵌其产品推广），引用时都应注明。

### Gaps
- 无法逐字核对 Offloop 转载与微信原文是否完全一致；只验证了 3 句独立引语和全部实验数字吻合。
- 内部实例的规模、运行时长、失败率、误触发率、实际节省的人力，文章均未披露。
- 实验使用的模型、Worker 假工具的耗时分布、统计显著性都没有说明。
- 没有找到任何第三方对这套架构做的独立复现或对照评测；现有外部反馈主要是安装体验和安全审计的二手转述。
- 文章没有与其他常驻 Agent 产品做横向比较，"相似架构选择"的趋同论断只举了 Anthropic 一例。
