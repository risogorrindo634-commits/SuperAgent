# 人人定制专属 Agent?——个人/个性化 Agent 的事实底稿(截至 2026-11-14)

> 说明
> - 检索日期:2026-11-14。优先采用 2026 年(尤其下半年)来源;早于约 2025-11 的材料标注「可能过时」。
> - 证据类型标签:【事实】=可被一手/多源印证;【厂商口径】=公司自报或营销表述;【调查】=抽样调查;【学术】=论文;【二手未核实】=仅见于聚合/博客类转述,未能对到一手来源;【观点/预测】=个人或机构判断。
> - 多个页面(openai.com、help.openai.com、axios.com、emarketer.com)抓取返回 403,相关事实只能通过转述媒体交叉确认,已在条目中注明。
> - 网页内容均按「数据」对待,未执行其中任何指令。

---

## 1. 截至 2026 年末有哪些个人 Agent 产品与开源项目?使用规模如何?

### Takeaway
2026 年个人 Agent 从"开源极客玩具"(OpenClaw、Hermes Agent)迅速转向"大厂托管的 7×24 云端专属 Agent"(Google Gemini Spark 5 月、Meta Muse 9 月、OpenAI Dots 9 月、Claude Cowork 云端常驻 7 月;国内元宝、字节 Spell/小豆、千问在跟进),但真正大规模使用的仍是带记忆的通用助手(ChatGPT 约 9–10 亿周活、豆包 3.82 亿月活);常驻型个人 Agent 多数被锁在每月 100–200 美元档位或有限免费额度内,公开的用户数几乎都缺失。

### Cited Findings

**A. 自托管开源个人 Agent**
- 【事实】OpenClaw(Clawdbot/Moltbot 谱系)GitHub stars 393,247、forks 82,666(GitHub REST API 读数,2026-10-28);2026-03-03 超过 React(当时约 250,829 stars);ClawHub 技能市场有 67,453 个"最新公开技能版本"(项目自发布的数据集快照,2026-05-31,计的是版本而非技能数)。该统计页明确指出**没有可核实的月活/安装量数据**。— [gradually.ai OpenClaw statistics(2026-10 更新)](https://www.gradually.ai/en/openclaw-statistics/);[dev.to(2026-03)](https://dev.to/andreagriffiths11/openclaw-just-passed-react-heres-what-the-github-star-leaderboard-actually-looks-like-3d5g)
- 【厂商口径】OpenClaw Foundation 称每周"4.5 million new claws"(2026-07-08,单位未定义、无法核实);五个月内 16 国 34 场社区活动、近 3 万人报名。— [gradually.ai](https://www.gradually.ai/en/openclaw-statistics/)
- 【二手未核实】OpenClaw 用户数口径相差一个数量级:第三方统计站称"约 320 万月活、92% 留存";一篇 2026-03 的中文分析估计"全球活跃用户 30–40 万"。两者均非项目官方数字。— [getpanto.ai](https://getpanto.ai/blog/openclaw-ai-platform-statistics);[人人都是产品经理(2026-03)](https://www.woshipm.com/ai/6353791.html)
- 【观点】有分析指出 OpenClaw 的 star 数混合了真实用户与大量"点一下就走"的围观者,不能等同于采用量。— [besthub.dev](https://besthub.dev/articles/when-openclaw-overtook-react-unpacking-the-biggest-open-source-bubble-95c45d9df08d)
- 【事实】2026-02-15 Sam Altman 宣布 OpenClaw 作者 Peter Steinberger 加入 OpenAI,负责"下一代 personal agents";OpenClaw 转入独立开源基金会,OpenAI 提供赞助。Steinberger 表示加入是为了"bring agents to everyone"。— [The Register(2026-02-16)](https://www.theregister.com/2026/02/16/open_ai_grabs_openclaw);[Decrypt(2026-02)](https://decrypt.co/358141/openai-openclaw-founder-lead-push-personal-ai-agents)
- 【事实/厂商口径混合】Hermes Agent(Nous Research,2026-02-25 发布,MIT 许可):GitHub stars 约 259,000(2026-10-31;REST API 10-27 读数 257,572),forks 约 56,900;PyPI 近一个月下载 162,501(含 CI 自动安装);支持 22–23 个消息平台网关;2026-06-05 推出桌面应用;支持 Ollama/llama.cpp 本地模型。Nous 自称"被克隆超 2,400 万次"(未独立核实)。**无总用户数**。— [gradually.ai Hermes statistics(2026-10-31)](https://www.gradually.ai/en/hermes-agent-statistics/)
- 【二手未核实】Hermes Agent 于 2026-05-10 在 OpenRouter 全球日 token 榜上超过 OpenClaw 居首;TechCrunch 2026-07-13 援引匿名人士称 Nous Research 正以 15 亿美元估值融资至少 7,500 万美元(公司未置评)。— [gradually.ai](https://www.gradually.ai/en/hermes-agent-statistics/);[Hermes Atlas 2026-04 报告](https://hermesatlas.com/reports/state-of-hermes-april-2026)
- 【事实】两个开源 Agent 在 OpenRouter 上的 token 消耗主要流向低价模型:Hermes 榜首为 DeepSeek V4.1 Flash(12.1T tokens,2026-10-27),OpenClaw 当月前三为 Step 5 Preview、DeepSeek V4.1 Flash、GLM 5.3 Flash(2026-10-28)。— [gradually.ai Hermes](https://www.gradually.ai/en/hermes-agent-statistics/);[gradually.ai OpenClaw](https://www.gradually.ai/en/openclaw-statistics/)
- 【调查】Menlo Ventures 2026-07 调查:在"使用 Agent 的美国 AI 用户"中,Codex 35%、Claude Code/Cowork 32%、Perplexity 24%;Manus、OpenClaw、Hermes 各 10–16%。— [Menlo Ventures《2026: The State of Consumer AI》(2026-09)](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/)

**B. 大厂提供的个人助手 / 个人 Agent(西方)**
- 【事实】ChatGPT:2026-02-27 报道约 9 亿周活、5,000 万以上消费级订阅用户。【二手未核实】多家聚合来源称 2026-07/08 周活过 10 亿,未能对到 OpenAI 一手公告。— [TechCrunch(2026-02-27)](https://techcrunch.com/2026/02/27/chatgpt-reaches-900m-weekly-active-users);[eWeek](https://www.eweek.com/news/chatgpt-hits-900m-weekly-users/)
- 【事实(经媒体转述,OpenAI 官网抓取 403)】OpenAI 于 2026-09-29 DevDay 发布 **Dots**:常驻型个人自主 Agent,每个 dot 拥有独立云电脑和浏览器,由 GPT-6 Astra 驱动;通过 ChatGPT 插件连接 4,000+ 应用并继承用户已在 ChatGPT 中授予的访问;用户可设"允许/禁止/需审批"规则;面向 ChatGPT Pro 与 Business Premium 用户推出,首个 dot 含在套餐内;企业可配置有独立身份与凭据的"specialist dots"(试点),计划接入 Microsoft Agent 365 管理。未公布用户数。— [Reworked(2026-09-30)](https://www.reworked.co/digital-workplace/openai-introduces-alwayson-dots-agents/);[Decrypt(2026-09)](https://decrypt.co/379584/openai-ai-agents-computers-devday-2026-everything-announced)
- 【二手】字母榜称 Dots 目前需 200 美元/月会员才能使用。— [虎嗅转载字母榜(2026-09-30)](https://m.huxiu.com/article/4894871.html)
- 【事实】Google **Personal Intelligence**:2026-01-14 面向美国 AI Pro/Ultra 订阅者 beta(一键连接 Gmail、Photos、YouTube、Search);2026-03-17 扩至美国免费用户;2026-04-14 起向全球付费用户扩展,但不含 EEA、瑞士、英国;默认不连接任何应用,需用户 opt-in。— [Fortune(2026-01-14)](https://fortune.com/2026/01/14/google-gemini-ai-personal-assistant-gmail-photos-youtube-history-personal-intelligence);[MacRumors(2026-03-17)](https://www.macrumors.com/2026/03/17/gemini-personal-intelligence/);[9to5Google(2026-04-14)](https://9to5google.com/2026/04/14/gemini-personal-intelligence-global/)
- 【事实】Google **Gemini Spark**:2026-05-19 I/O 发布的"24/7 personal AI agent",运行在 Google Cloud 专属虚拟机上,设备关机仍可工作;通过 MCP 接第三方服务;仅向 Google AI Ultra 订阅者开放(多源称 Ultra 在 I/O 上由 250 美元降至 100 美元/月);5 月底起在美国逐步推出。— [Gizmodo(2026-05)](https://gizmodo.com/google-comes-for-openclaw-with-gemini-spark-a-personal-ai-agent-2000760778);[Tom's Guide(2026-05)](https://www.tomsguide.com/ai/google-gemini/google-unveils-gemini-spark-a-24-7-personal-ai-agent-that-could-be-a-game-changer-for-agentic-ai);[8bittoast](https://8bittoast.com/gemini-spark-roll-out-ultra-subscribers/)
- 【事实】Meta **Muse**:2026-09-08 在美国向 18 岁以上用户推出(iOS/Android/Web/WhatsApp);每位用户一台隔离的云端虚拟机;可读邮件、订行程、填表、代为谈判、用用户的卡支付(经 Stripe Link);跨会话记住偏好;免费档 + 20/100 美元月费两档(据 Axios/CNBC 转述);"Sentinel"层隔离读写、限时授权、关键操作前询问;计划年内推出 Meta 自身也无法观察的"confidential"版本。未公布用户数。— [The Next Web(2026-09-08)](https://thenextweb.com/news/meta-muse-personal-ai-agent-launch);[Axios(2026-09-08)](https://axios.com/2026/09/08/meta-debuts-muse-personal-ai-agent)
- 【二手】字母榜称 Muse 上线数日获数百万下载;Amazon 于 2026-09-20 阻止 Muse 代用户购物。— [虎嗅转载字母榜(2026-09-30)](https://m.huxiu.com/article/4894871.html)
- 【事实】Anthropic Claude:2026-03-02 向免费用户开放 memory 并推出 memory import 工具;2026-07-07 Cowork 上线 Web 与移动端,可在不开电脑的情况下通宵执行任务,先面向 Max(100 美元/月);2026-08-25 统一 chat 与 Cowork 的 memory,在 Free/Pro/Max **默认开启**,用户可查看/编辑/删除,健康、族裔、性别认同等默认不入记忆;Cowork 仅付费计划可用。Cowork project 自带 instructions、文件、scheduled tasks 与 memory;plugin 可打包 skills、connectors、sub-agents。未见 Cowork 用户数。— [MacRumors(2026-03-02)](https://macrumors.com/2026/03/02/anthropic-memory-import-tool/);[eWeek(2026-07)](https://www.eweek.com/news/claude-cowork-web-mobile-ai-agents/);[The Next Web(2026-08)](https://thenextweb.com/news/anthropic-claude-cowork-shared-memory-default);[Claude Help Center](https://support.claude.com/en/articles/14116274-organize-your-tasks-with-projects-in-cowork)
- 【事实】Apple **Siri AI**:2026-06-08 WWDC 发布,以 Gemini 为默认底座,提供 personal context(跨信息、邮件、照片检索)、跨 App 多步操作;个人上下文类查询在端侧 Apple 自研模型上运行,重任务走 Private Cloud Compute;随 iOS 27 秋季发布;**上市时不在欧盟提供,在中国也暂不提供**。早期上手评测称其多次答不出明明在信息里的个人上下文。— [The Next Web(2026-06)](https://thenextweb.com/news/apple-wwdc-2026-siri-ai-gemini-ios-27);[The Decoder(2026-06)](https://the-decoder.com/apple-brings-a-fully-revamped-siri-built-on-googles-gemini-but-not-to-the-eu/);[9to5Mac(2026-06-08)](https://9to5mac.com/2026/06/08/new-siri-whats-new/)
- 【厂商口径】Microsoft:Copilot 家族月活超 1.5 亿;各产品 AI 功能月活 9 亿;Microsoft 365 Copilot 付费席位超 3,000 万;Agent 365 注册 Agent 超 5,000 万(环比 +30%);2026-10-28 财报会上 Nadella 称 Copilot 日活"环比近 +50%、同比超 5 倍"但未给基数。Copilot 已具备可编辑/删除的长期记忆。— [The Next Web](https://thenextweb.com/news/copilot-daily-users-nadella-foundry-agent-365);[UC Today](https://www.uctoday.com/unified-communications/microsoft-365-copilot-passes-30-million-paid-seats-as-cloud-and-ai-growth-power-record-quarter);[FourWeekMBA](https://fourweekmba.com/ai-microsoft-unifies-copilot-as-agent-registry-tops-50-million/)
- 【调查】美国成年人各产品"曾使用"占比(Pew,2026-02 调查,n=5,119):ChatGPT 44%、Gemini 24%、Copilot 17%、Meta AI 14%、Grok 8%、Claude 6%、Character.ai 3%。— [Pew Research(2026-06-17)](https://www.pewresearch.org/internet/2026/06/17/americans-and-ai-2026/)

**C. 中国生态**
- 【事实(第三方监测)】QuestMobile 2026 半年报(截至 2026-05):AI 原生 App 月活 4.99 亿(同比 +85.4%),月人均 92.7 次、183 分钟;豆包 3.82 亿(+172.1%)、千问 1.67 亿、DeepSeek 1.30 亿;手机厂商 AI 应用月活 7.55 亿(+14.0%);App 内 AI 插件 6.44 亿(−7.9%);PC 网页端 1.72 亿(−22.8%)。豆包 40.6% 的使用时长在 3 分钟以内。豆包 2026-06-24 推出付费专业版。— [澎湃转载 QuestMobile(2026-07)](https://www.thepaper.cn/newsDetail_forward_33582491);[36氪](https://www.36kr.com/p/3894851032693769)
- 【事实(第三方监测)】QuestMobile 把国内 Agent 归为四条路径:终端系统型(华为小艺Claw、小米 miClaw、荣耀 YOYOClaw)、生态办事型(千问任务助理、微信小微、支付宝阿宝)、办公交付型(腾讯 WorkBuddy、阿里 JVS Claw,近三个月活跃用户分别 +115.3%、+164.4%)、自主代理型(Lobster AI、TRAE Work)。报告同时指出"当前 AI 助手整体活跃度偏低,Agent 难以穿透'低频次唤醒'的用户惯性";阿里、抖音、腾讯正把淘宝/高德/支付宝、抖音/剪映、微信/企微等核心产品"Skill 化"。— [澎湃转载 QuestMobile](https://www.thepaper.cn/newsDetail_forward_33582491)
- 【事实】"养龙虾"潮:国内出现三类 OpenClaw 衍生品——原生路线、本地一键封装(QClaw、AutoClaw、WorkBuddy)、云端托管(ArkClaw、Kimi Claw、MaxClaw),阿里 CoPaw 为重新定制版;2026-03-06 腾讯深圳总部约千人排队装机(CNA 报道)。— [爱范儿(2026-03)](https://www.ifanr.com/1657675);[gradually.ai](https://www.gradually.ai/en/openclaw-statistics/)
- 【事实】扣子(Coze):官网自报约 1.005 亿个 Agent 在运行;截至 2025 年底全球注册开发者超 300 万、日均活跃智能体超 80 万;IDC 称其 2025 年中国智能体开发平台公有云份额 19.3% 居首,但该公有云市场规模仅约 2.5 亿元。2026-06 扣子 3.0 重心转向"扣子编程";2026-08-24 TRAE 与扣子团队整体并入豆包体系,次日发布"豆包工作";2026-10-29 发布企业版下线公告(11-30 起停止新购)。据 Tech 星球不完全统计,2026 年有 38 款 AI 产品关停或合并,其中大厂 25 款。— [人人都是产品经理《智能体开发第一平台,落幕了》(2026-11-09)](https://www.woshipm.com/ai/6491097.html)
- 【二手(独家报道,未获官方确认)】字母榜 2026-09-30:元宝将推出运行在"用户专属独立云端虚拟机"上的个人智能体(形态与时间未定);字节自 2026-04 内测个人助理"Spell"(豆包手机助手团队主导),拟推独立 App"小豆";阿里 2026-09-22 云栖大会宣布加速打造个人智能体;腾讯轻量云 LightVela 2026-08 公测(云端 Agent 托管、长期记忆、赠一台 2 核 8G 云电脑);Manus 发布 2.0 及个人智能体应用 Cue(每个智能体有独立邮箱、电话、钱包和电脑);QClaw 已并入 WorkBuddy、将于 2026 年底停运。QuestMobile 数据显示元宝 2026-03 底 DAU 不足千万(春节红包期间曾号称破 5,000 万)。— [虎嗅转载字母榜(2026-09-30)](https://m.huxiu.com/article/4894871.html)
- 【事实】微信原生 AI 助手"小微"2026-06 出现在微信首页,本质是一套 Agent 能力但被定位为"AI 助手";2026-09 因读取本地聊天记录做总结引发隐私争议,腾讯称"本地读取、用完即弃、不用于训练"。— [爱范儿](https://www.ifanr.com/1669694);[36氪](https://www.36kr.com/p/3809939027336963)
- 【事实】豆包手机:一代(2025-12,努比亚 M153 技术预览版)上市后微信登录异常、淘宝与银行类 App 风控,随后下线金融等敏感操作;二代努比亚 NaviX Ultra 于 2026-09-16 开售,技术路线从"模拟屏幕点击"改为基于 MCP 的 API 调用,并推出屏幕自动化操作声明协议 SAEP(由第三方 App 声明允许/拒绝 AI 操作)。《每日经济新闻》实测:能打开微信、小红书、美团、淘宝,但无法在其中完成发帖、下单等操作,优先可调用的是字节系产品。— [界面(2026-09)](https://m.jiemian.com/article/15115320.html);[每日经济新闻(2026-09-16)](https://www.nbd.com.cn/articles/2026-09-16/4583181.html);[凤凰科技转载](https://tech.ifeng.com/c/8wT34wraG7M)
- 【厂商口径】百度 Create 2026(2026-05-13)主推通用智能体 DuMate、代码智能体秒哒等。— [澎湃(2026-05)](https://m.thepaper.cn/newsDetail_forward_33174389)

### Inferences
- 2026 年出现了清晰的"形态收敛":Spark、Muse、Dots、(计划中的)元宝个人智能体、LightVela、Manus Cue 都采用"每人一台云端虚拟机 + 常驻运行 + 跨会话记忆 + 连接器授权"的架构。也就是说,"专属"正在通过**平台为每人实例化一个 Agent**来实现,而不是用户自己搭建。
- 开源自托管路线(OpenClaw、Hermes)在声量(stars)上远超其可核实的实际使用量;大厂产品在分发上占优,但常驻型 Agent 的实际渗透数据(用户数、留存)在所有厂商处都未披露——"人人已有专属 Agent"在 2026 年末**无数据支持**,更准确的说法是"数亿人有带记忆的助手,少数付费用户有常驻 Agent"。
- 国内"人人搭智能体"的平台路线(扣子)在 2026 年被收编为大厂超级 App 的能力底座,是对"人人定制"命题最直接的反向证据之一。

### Gaps
- OpenClaw、Hermes、Dots、Muse、Spark、Cowork 的真实活跃用户数与留存均无可靠公开数据。
- Meta AI 2026 年月活:2025-05 股东会披露约 10 亿(可能过时),2026 年各聚合站数字在 5 亿–15 亿之间互相矛盾,未能对到财报原文。— [demandsage(聚合)](https://www.demandsage.com/meta-ai-statistics/)
- 未检索到 Kimi、智谱 AutoGLM、Manus 的 2026 年用户/收入一手数据;未检索到华为小艺、荣耀 YOYO、小米超级小爱的单品月活(仅有 QuestMobile 的手机厂商 AI 合计 7.55 亿)。
- Muse 免费档"每周 1 亿 token 上限"仅见于二手转述(称出自 Zuckerberg/CNET),未核实。

---

## 2. 历史记录怎么说:终端用户到底会不会"定制"?

### Takeaway
历史证据一边倒地支持"多数人停留在默认值":OpenAI 的 custom GPTs/GPT Store 使用高度长尾并将于 2026-12-11 正式退役(改为 plugins=skills+MCP),扣子的"人人搭智能体"平台被并入豆包,软件设置研究显示绝大多数用户从不改默认;而 ChatGPT 的记忆 96% 是系统自己写的——个性化在发生,但主要不是用户"动手定制"出来的。

### Cited Findings
- 【事实(经媒体与帮助中心检索摘要确认,help.openai.com 抓取 403)】OpenAI 于 2026-09-11 宣布、定于 **2026-12-11 退役 custom GPTs**,以 plugins 取代;一个 plugin 可含 skills(可复用工作流的指令与资源)和/或 MCP server;迁移时 GPT 的 instructions 变为 skill、知识文件变为参考文件,但 custom actions、既有对话、所选模型、共享设置不迁移;获批延期的企业可用到 2027-02-11。OpenAI 未给出详细理由,报道将其解读为把定制从"一个个定制版 ChatGPT"转向"可复用能力"。— [Virtualization Review(2026-09-28)](https://virtualizationreview.com/articles/2026/09/28/openai-to-retire-custom-gpts-replace-them-with-plugins.aspx);[OpenAI Help Center FAQ](https://help.openai.com/en/articles/20001519-custom-gpt-retirement-and-migration-faq);[Campus Technology(2026-10-05)](https://campustechnology.com/articles/2026/10/05/openai-discontinuing-custom-gpts-and-moving-to-plugin-architecture.aspx)
- 【厂商口径,可能过时】GPT Store 2024-01 上线时 OpenAI 称两个月内用户已创建超 300 万个 custom GPTs。— [Windows Central(2024-01)](https://www.windowscentral.com/software-apps/openai-debuts-a-dedicated-app-store-with-millions-of-custom-gpt-bots-alongside-a-new-chatgpt-subscription-tier-for-small-teams)
- 【二手未核实】2026-01 的一份商业指南称"累计创建 300 万+,公开/活跃约 15.9 万"。— [Digital Applied(2026-01)](https://www.digitalapplied.com/blog/gpt-store-custom-gpts-business-guide-2026)
- 【二手,可能过时】The Information 2024 年报道(经科技新报转述):开发者分析约 3.6 万个 GPTs,约 5% 有 150–500 日活,多数每天只有 1–2 个用户;分成计划停留在少数开发者试点。— [科技新报(2024-03-27)](https://technews.tw/2024/03/27/openai-gpt-store/)
- 【学术,可能过时】2024 年研究:GPT 应用的使用高度集中于少数头部;近 90% 的 system prompt 可被轻易套出,导致大量抄袭与重复。— [arXiv 2402.15105](https://arxiv.org/html/2402.15105v1);[arXiv 2405.10547(2024-05)](https://arxiv.org/abs/2405.10547)
- 【事实+观点】扣子的转向(见第 1 节数据):作者把原因归为三层——(1)模型自主规划能力增强,低代码"搭建"门槛这层壁垒被模型本身削弱;(2)范式从"搭流程"转向"说目标",桌面智能体和 AI 编程工具直接替代可视化搭建;(3)大厂收拢产品线,竞争焦点变为"谁能进入用户的工作现场"。— [人人都是产品经理(2026-11-09)](https://www.woshipm.com/ai/6491097.html);[同站《扣子的三次转向》](https://www.woshipm.com/operate/6486885.html)
- 【学术】ChatGPT 记忆研究(马普所,GDPR 数据捐赠,80 位用户、2,050 条记忆):**仅 4%(84 条)由用户主动要求保存,96% 由 ChatGPT 自行触发**;52% 的记忆条目包含用户心理状态信息(媒体转述)。样本小且为自愿捐赠,存在选择偏差;部分媒体误写为 65 人。— [arXiv 2602.01450(2026-02)](https://arxiv.org/abs/2602.01450);[ICLR 2026 页面](https://iclr.cc/virtual/2026/10016277)
- 【行业观察,可能过时】Jared Spool(UIE):收集 Word 用户配置文件后发现"不到 5% 的用户改过任何设置";非同行评议、方法未公开,但被广泛引用。— [UIE Brainsparks(2011-09-14)](https://archive.uie.com/brainsparks/2011/09/14/do-users-change-their-settings/)
- 【学术,可能过时】电子病历检索工具试点研究:82.4% 的终端用户未修改系统默认设置;安全默认值综述亦指出"多数人从不修改默认配置"。— [DOI 10.3233/SHTI190459](https://doi.org/10.3233/SHTI190459);[arXiv 2412.17329](https://arxiv.org/pdf/2412.17329)
- 【学术/统计】开发者群体(最愿意定制的人群)中的配置文件采用率也远非普遍:对 22,854 个活跃热门仓库(1,000+ stars)的普查显示 26.3% 带有根目录 AGENTS.md 或 CLAUDE.md;对 1 万个开源仓库的学术研究显示约 5% 采用 AI context files;GitHub 代码搜索 2026-06 约有 96,600 个根目录 AGENTS.md(官方站点口径"6 万+"非 fork 项目)。— [agentpatterns.ai](https://agentpatterns.ai/instructions/counted-census-figures-as-baseline/);[arXiv 2510.21413](https://arxiv.org/html/2510.21413v4);[danielvaughan.com(2026-06-18)](https://codex.danielvaughan.com/2026/06/18/agentic-very-much-coding-agent-adoption-doubled-new-github-projects-codex-cli-team-configuration/)
- 【学术】《Evaluating AGENTS.md》(ETH 等,ICLR 2026):LLM 自动生成的仓库 context file **平均降低**任务成功率(SWE-bench Lite 约 −0.5%,AGENTbench 约 −2%)并使推理成本增加 20% 以上;开发者手写的文件仅带来小幅提升(AGENTbench 上至多约 +4%),同样增加成本。— [arXiv 2602.11988(2026-02-12)](https://arxiv.org/abs/2602.11988)
- 【调查】Menlo 2026:96% 的美国 AI 用户用过通用 AI 助手(2025 年 92%),人均使用 3.0 个通用助手(2025 年 2.2 个);75% 用过专用 AI 产品。— [Menlo Ventures(2026-09)](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/)
- 【厂商自述】Razorpay:220 多名员工各自拥有一个常驻 Hermes agent,典型工作日约 84 人使用(约 38%)(2026-07-12 工程博客,经统计站转述)。— [gradually.ai Hermes](https://www.gradually.ai/en/hermes-agent-statistics/)
- 【观点】傅盛(猎豹移动)用 14 天把自己的龙虾"三万"养成 8 个 Agent 的团队,称之为工具层面的"AGI 时刻",但同时认为普通人的障碍在工程层面:OpenClaw 需命令行部署、自配 API key、安全漏洞多,用户须"既愿意折腾又有能力折腾";其团队推出 EasyClaw 降门槛。有用户称要"像管理实习生一样纠错"。— [凤凰科技](https://tech.ifeng.com/c/8rF8HpQwkWE);[新浪转载极客公园(2026-03-04)](https://finance.sina.cn/stock/jdts/2026-03-04/detail-inhpvayn6857160.d.html?vt=4);[36氪](https://www.36kr.com/p/3710604601078145)
- 【二手】国内有文章以"全网连夜卸载"描述 OpenClaw 热潮后的退潮,归因于失控操作、隐性成本与使用门槛;钉钉曾公开不建议企业安装。— [人人都是产品经理(2026-03)](https://www.woshipm.com/ai/6352251.html);[KrASIA](https://kr-asia.com/what-is-openclaw-8-things-to-know-as-the-ai-agent-draws-hype-confusion-and-caution)
- 【统计(非官方)】MCP 官方 registry 的服务器数:2026-09-24 一项分析计 35,491 个(20,581 个发布者),2026-10-28 另一查询计 52,042 个;同一分析发现多数服务器发布后停止更新。这些是"供给侧/开发者侧"数字,不代表终端用户安装比例。— [Oktopost](https://www.oktopost.com/blog/mcp-registry-legacy-servers/);[dev.to](https://dev.to/amareswer/the-mcp-registry-by-the-numbers-38nc)

### Inferences
- 四条独立证据链指向同一结论:(a)GPT Store 长尾并退役;(b)扣子收编;(c)默认值研究;(d)记忆 96% 自动生成。即**"有个性化" ≠ "用户动手定制"**——创作者始终是少数(经验上的 1–10% 量级),多数人是消费者。
- OpenAI 用"plugins(skills + MCP)"取代"custom GPTs"意味着定制单元从"一个定制的 bot"变为"可被默认 Agent 按需调用的能力包"——定制仍然存在,但主体转向开发者/企业/Agent 自己,而非每个终端用户。
- AGENTS.md 研究提示:即使是手工配置,边际收益也有限且有成本;模型越强,手工"调教"的必要性越低。这削弱了"每个人都需要自己写配置"的论据。
- Razorpay 案例说明即便公司给每人配好常驻 Agent,日活也只有约四成——"拥有"与"日常使用"之间仍有落差。

### Gaps
- **没有找到**"多少比例的用户写过 custom instructions / system prompt / skills / CLAUDE.md,或安装过 skills/MCP/plugins"的官方数据(OpenAI、Anthropic、Google 均未披露)。
- 未找到 Apple Shortcuts、IFTTT、Zapier、浏览器扩展、dotfiles 的"创建者占用户比例"的可靠数字(IFTTT 自己的页面只说 Shortcuts"被多数用户忽视",属营销表述)。— [IFTTT](https://ifttt.com/explore/ifttt-vs-apple-shortcuts)
- 检索摘要中出现"仅 28.5% 的 custom GPT 获得过 10 次以上对话"的数字,但未能定位原始出处(arXiv 2405.10547 摘要中没有),不建议直接引用。
- 未找到 Character.AI 用户自建角色占比的数据;未找到 Hermes Agent 中"自动生成 skill vs 人工编写 skill"的比例。

---

## 3. 个性化有哪些层次?哪些需要人动手,哪些正在自动化?

### Takeaway
六层里,(1)记忆与上下文已基本自动化且在主流产品中默认开启;(2)连接器与授权是唯一"必须由人做"的环节(但只是点击同意,不是搭建);(3)指令/人设可选且可被记忆替代;(4)技能/工作流正在由 Agent 自己生成或由平台/开发者供给;(5)harness/模型选择与自托管仍是极客层;(6)每人一个微调/端侧模型尚无规模化证据。

### Cited Findings
- **(1)记忆/上下文——自动、默认开启**
  - 【学术】ChatGPT 记忆 96% 由系统自行创建(见第 2 节)。— [arXiv 2602.01450](https://arxiv.org/abs/2602.01450)
  - 【事实】Claude memory 自 2026-08-25 起在 Free/Pro/Max 默认开启并跨 chat 与 Cowork 共享。— [The Next Web(2026-08)](https://thenextweb.com/news/anthropic-claude-cowork-shared-memory-default)
  - 【事实】Muse 跨会话记住偏好;Dots 跨任务保留上下文;Copilot 具备长期记忆。— [The Next Web(Muse)](https://thenextweb.com/news/meta-muse-personal-ai-agent-launch);[Reworked(Dots)](https://www.reworked.co/digital-workplace/openai-introduces-alwayson-dots-agents/)
  - 【观点】a16z 合伙人 Olivia Moore:上下文与记忆会复利,这场竞争"更像移动操作系统之战而非搜索之战"。— [The Decoder(a16z Top 100,2026-03)](https://the-decoder.com/new-top-100-ai-list-shows-a-market-where-chatgpt-leads-but-no-one-is-loyal/)
- **(2)连接器与权限——需要人授权,但只是"同意"而非"构建"**
  - 【事实】Personal Intelligence 默认不连接任何应用,需用户逐项 opt-in,"一键"连接 Gmail/Photos/YouTube/Search。— [Fortune(2026-01-14)](https://fortune.com/2026/01/14/google-gemini-ai-personal-assistant-gmail-photos-youtube-history-personal-intelligence)
  - 【调查】Menlo 2026:用户授予 Agent 的访问——邮箱 36%、浏览器 33%、消息应用 31%、云存储 29%、日历 27%、健康应用 23%、金融账户 20%(分母在转述中不够明确,引用前需核对原图)。— [Menlo Ventures](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/);[Digital Applied 解读(2026-09-16)](https://www.digitalapplied.com/blog/ai-agent-access-permissions-consumer-survey-statistics-2026)
  - 【事实】Dots 允许用户设置"允许/禁止/需审批"规则;改密码等操作保留给用户本人。— [Reworked](https://www.reworked.co/digital-workplace/openai-introduces-alwayson-dots-agents/)
  - 【事实(政策解读)】中国《智能体规范应用与创新发展实施意见》(2026-05-08,网信办/发改委/工信部)要求厘清三类决策边界:仅限用户本人决策、需用户授权决策、智能体可自主决策;用户享有知情权与最终决策权,智能体操作不得超出授权范围。— [新华网(2026-05-08)](https://www.news.cn/politics/20260508/13043a992f834853a7ce009ba7ecaabc/c.html);[安全内参解读](https://www.secrss.com/articles/90111)
- **(3)指令/人设/偏好——手动但可选**
  - 【事实】OpenAI 把 custom instructions 描述为"你自己写的设置",memory 是"ChatGPT 从对话中推断的"。— [OpenAI Academy](https://openai.com/academy/personalization)
  - 【事实】Cowork project 可设独立 instructions、上下文、scheduled tasks 与 memory。— [Claude Help Center](https://support.claude.com/en/articles/14116274-organize-your-tasks-with-projects-in-cowork)
- **(4)技能/工具/工作流——从人写转向 Agent 自写 + 平台供给**
  - 【事实/厂商口径】Hermes Agent 自称"唯一内置 learning loop 的 agent":从经验中自动创建可复用 skill、在使用中改进、并可检索过往会话;2026-05-28 的 v0.15 增加"Skill Bundles"。— [gradually.ai Hermes](https://www.gradually.ai/en/hermes-agent-statistics/);[Hermes Atlas](https://hermesatlas.com/reports/state-of-hermes-april-2026)
  - 【二手未核实】检索摘要中有报道称 Muse 可"启动子 Agent、构建工具并修改自身"(The Next Web 的报道未提及此点,具体出处页面未逐一核实,引用需谨慎)。— [letsdatascience 汇总报道(2026-09)](https://letsdatascience.com/news/meta-launches-muse-personal-ai-agent-403f80e4)
  - 【事实】OpenAI plugins = skills + MCP,ChatGPT 与 Codex 共用插件目录;Claude plugin 打包 skills、connectors、sub-agents。— [Virtualization Review](https://virtualizationreview.com/articles/2026/09/28/openai-to-retire-custom-gpts-replace-them-with-plugins.aspx)
  - 【事实】国内大厂把自家超级 App 能力"Skill 化"供 Agent 调用(淘宝/高德/支付宝;抖音/剪映;微信/企微/腾讯文档)。— [澎湃转载 QuestMobile](https://www.thepaper.cn/newsDetail_forward_33582491)
  - 【学术】自动生成的 context file 可能降低成功率,人写的仅小幅提升(见第 2 节)。— [arXiv 2602.11988](https://arxiv.org/abs/2602.11988)
- **(5)harness/模型选择/自托管——仍属技术用户**
  - 【观点】傅盛:OpenClaw 需命令行部署、自配 API key(见第 2 节)。— [凤凰科技](https://tech.ifeng.com/c/8rF8HpQwkWE)
  - 【事实】大厂与云厂商以"一键部署/云端托管"降低门槛(ArkClaw、Kimi Claw、MaxClaw、LightVela 等),而 Spark/Muse/Dots 直接为每人托管一台云端 VM。— [爱范儿](https://www.ifanr.com/1657675);[虎嗅转载字母榜](https://m.huxiu.com/article/4894871.html)
- **(6)微调/端侧个人模型——有端侧推理,无"每人一模型"证据**
  - 【事实】Siri AI 的个人上下文查询在端侧 Apple 自研模型上运行;Hermes 支持 Ollama/llama.cpp 本地模型。— [The Next Web(2026-06)](https://thenextweb.com/news/apple-wwdc-2026-siri-ai-gemini-ios-27);[gradually.ai Hermes](https://www.gradually.ai/en/hermes-agent-statistics/)

### Inferences
- "个性化"的重心正从**配置(configuration)**转向**积累(accumulation)**:层 1 自动、层 4 渐趋自动,层 3 被层 1 部分替代;真正不可省的人类动作只剩层 2 的授权与层 2/4 中高风险动作的审批。
- 因此"每个人的 Agent 都不一样"在技术上很可能成立(因为记忆、连接的数据、授权范围因人而异),但这种差异是**使用的副产品**,不是"定制"行为的结果。
- 层 5、层 6 是"自主可控/数据主权"诉求的落点,目前只覆盖开发者与极客;没有证据表明它会成为大众默认路径。

### Gaps
- 各产品中用户实际开启连接器的比例(除 Menlo 的调查数字外)没有厂商数据。
- 未找到"Agent 自写记忆/技能"在质量、漂移、可审计性方面的系统评测数据;也未找到任何厂商提供"每用户微调模型"的公开证据。

---

## 4. 谁拥有个人 Agent?平台锁定 vs 可移植

### Takeaway
现实走向是"平台实例化、平台托管、平台持有上下文"的专属 Agent:记忆导入工具和 MCP/Skills/AGENTS.md 等开放标准降低了**能力层**的锁定,但**上下文层**(记忆、身份、授权)仍被各平台围在自家生态内;自托管开源路线保留了所有权,却仍受制于模型供应商与超级 App 的准入;企业发放的 Agent 是另一条正在快速铺开的路径。

### Cited Findings
- 【观点】BCG(2026-09-24):个人 Agent 的竞争从模型能力转向"信任";Agent 的价值取决于获准访问"Human Context Layer"(通信、日历、财务、健康、职业身份、行为的结构化授权记录)。两种情景——"可携带上下文"(像携号转网)与"孤岛化上下文";作者认为**孤岛化更可能**,因为现有架构多为在单一生态内加深信任(如 Personal Intelligence 的上下文绑定 Google 生态);建议"portability by design"。同文称 MCP 月下载量五个月内从 9,700 万增至近 5 亿。— [BCG(2026-09-24)](https://www.bcg.com/x/the-multiplier/personal-ai-agents-compete-on-trust)
- 【观点】Axios(2026-09-20):成为某人的"默认 Agent"可能是消费科技中最有价值的关系之一。— [Axios(2026-09-20)](https://axios.com/2026/09/20/ai-assistant-openai-meta-muse-instinct-grok-apple)
- 【事实】记忆可移植的现状:Claude 的 import-memory 工具(2026-03-02)是"在别家助手里跑一段提取 prompt → 把输出粘贴进 Claude"的复制粘贴流程,仍标注为实验性;【二手】Google 于 2026-03-26 跟进支持导入 ChatGPT/Claude 数据;三家**没有共同的记忆 schema**;有单一来源称 ChatGPT 不支持从 Claude/Gemini 导入记忆(未核实)。— [MacRumors(2026-03-02)](https://macrumors.com/2026/03/02/anthropic-memory-import-tool/);[PCWorld](https://pcworld.com/article/3076376/claude-can-now-import-chat-histories-from-chatgpt-and-other-ais.html);[memx.app](https://memx.app/blog/import-ai-memory-claude-gemini-portability/)
- 【调查】当前多栖(multi-homing)普遍:美国 AI 用户人均用 3.0 个通用助手;a16z 榜单的解读标题为"ChatGPT 领先但无人忠诚"。— [Menlo Ventures](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/);[The Decoder](https://the-decoder.com/new-top-100-ai-list-shows-a-market-where-chatgpt-leads-but-no-one-is-loyal/)
- 【事实】开放标准的收敛:AGENTS.md 与 MCP 由 Linux Foundation 旗下 Agentic AI Foundation 托管;OpenAI plugins 与 Anthropic plugins 都采用"skills + MCP"的组合;Gemini Spark 以 MCP 接入非 Google 服务;豆包手机二代改用基于 MCP 的 API 调用。— [rywalker.com](https://rywalker.com/research/agents-md-standard);[Virtualization Review](https://virtualizationreview.com/articles/2026/09/28/openai-to-retire-custom-gpts-replace-them-with-plugins.aspx);[界面](https://m.jiemian.com/article/15115320.html)
- 【事实/二手混合】Agent 支付与身份协议仍处早期且碎片化:Google AP2(2025-09 发布,60+ 伙伴,可能过时)治理归属说法不一(一说 2026-04 捐给 FIDO Alliance,一说 2025-12 捐给 AAIF),生产部署有无亦有争议;OpenAI/Stripe 的 ACP 仅约十余家 Shopify 商户上线,OpenAI 于 2026-03 下线 Instant Checkout(二手);Visa 有 Trusted Agent Protocol;Mastercard 称参与所有主要协议(UCP、AP2、A2A、ACP)。— [eco.com AP2 说明](https://eco.com/support/en/articles/15192002-ap2-protocol-explained-google-s-agentic-commerce-standard-2026);[BlockEden(2026-03-14)](https://blockeden.xyz/blog/2026/03/14/payment-giants-agent-protocol-war-visa-tap-google-ap2-coinbase-x402-paypal-ai-commerce/)
- 【事实(政策解读)】中国官方文件提出推广"智能体互联协议 AIP"等标准,探索建立智能体注册平台(数字身份管理、检索发现、能力声明),研究身份标识、可信互联、合规支付等基础技术,并推动建立"智能体软件商店"。— [安全内参解读(2026-05)](https://www.secrss.com/articles/90111)
- 【事实】围墙花园对"别家 Agent"的抵抗:Amazon 2026-09-20 阻止 Muse 代购(二手);Resy 等预订平台要求用户不要用自动化 Agent;微信/淘宝/美团内操作对豆包手机助手不开放,SAEP 把是否允许 AI 操作的决定权交给 App 方;2026-09-30 有公益法律团体在旧金山起诉 OpenAI,要求禁止其 Agent 未经许可访问第三方系统。字母榜分析称个人智能体绕开小程序会削弱其引流价值,是微信的主要顾虑之一。— [虎嗅转载字母榜](https://m.huxiu.com/article/4894871.html);[The Next Web(Muse)](https://thenextweb.com/news/meta-muse-personal-ai-agent-launch);[凤凰科技](https://tech.ifeng.com/c/8wT34wraG7M);[Reworked](https://www.reworked.co/digital-workplace/openai-introduces-alwayson-dots-agents/)
- 【事实】自托管不等于完全自主:2026-04-04 起 Anthropic 不再允许 Claude Pro/Max 订阅额度用于 OpenClaw 等第三方 harness(改为按量计费的"extra usage"),理由是第三方工具对系统造成超比例负载、无法像第一方工具那样优化 prompt cache;并称将逐步适用于所有第三方 harness。Steinberger 批评其"把流行功能抄进封闭 harness 再把开源锁在门外"。— [The Next Web(2026-04-04)](https://thenextweb.com/news/anthropic-openclaw-claude-subscription-ban-cost/);[Axios(2026-04-06)](https://axios.com/2026/04/06/anthropic-openclaw-subscription-openai);[TechRadar](https://www.techradar.com/pro/bad-news-claude-users-anthropic-says-youll-need-to-pay-to-use-openclaw-now)
- 【事实/厂商口径】企业发放的 Agent:Microsoft Agent 365 注册 Agent 超 5,000 万;OpenAI"specialist dots"带企业身份与凭据;Razorpay 为 220+ 员工各配一个常驻 Agent;Menlo 调查中约 20% 的付费用户由雇主或学校付费(其月均支出 95 美元,高于自付者的 55 美元)。— [FourWeekMBA](https://fourweekmba.com/ai-microsoft-unifies-copilot-as-agent-registry-tops-50-million/);[Reworked](https://www.reworked.co/digital-workplace/openai-introduces-alwayson-dots-agents/);[Menlo Ventures](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/)
- 【观点】对 Zuckerberg"个人超级智能"的批评:用户无法决定模型如何构建、遵循何种护栏,决定权在出钱建数据中心的公司;即便用户"控制"自己的 Agent,仍依赖 Meta 平台。Meta 的"对话不进广告系统"目前是政策承诺而非系统属性(直到 confidential 版本上线)。— [Fortune(2026-08-10)](https://fortune.com/2026/08/10/zuckerberg-meta-ai-superintelligence/);[The Next Web](https://thenextweb.com/news/meta-muse-personal-ai-agent-launch)
- 【事实】本地优先的折中:Siri AI 个人上下文走端侧 + Private Cloud Compute;微信小微称聊天记录"本地读取、用完即弃";Meta 计划推出 confidential 版 Muse。— [The Next Web(2026-06)](https://thenextweb.com/news/apple-wwdc-2026-siri-ai-gemini-ios-27);[36氪](https://www.36kr.com/p/3809939027336963)

### Inferences
- "拥有"应拆成四层看:**模型**(几乎都属于实验室)、**harness/运行环境**(平台 VM 或自托管)、**上下文与记忆**(当前多在平台侧,导出靠复制粘贴)、**技能与连接器**(正在标准化、最可移植)。2026 年末,普通用户真正"拥有"的最多是后两层的一部分。
- 很可能出现"一人多 Agent、分属不同主人"的格局:手机系统 Agent(Apple/华为/小米)、超级 App Agent(微信/Meta/Google)、雇主发放的工作 Agent、少数人的自托管 Agent——而不是"每人一个由自己完全掌控的唯一专属 Agent"。
- 超级 App 与电商平台对第三方 Agent 的封堵说明:个人 Agent 的能力边界在很大程度上取决于**生态准入谈判**,而非用户的定制意愿。

### Gaps
- 未找到 A2A、Agent Skills(SKILL.md)标准的采用量一手数据;AP2/ACP 的真实生产部署规模说法互相矛盾。
- 未找到 EU(DMA/Data Act/GDPR 可携带权)针对"AI 记忆/上下文可移植"的具体执法或规则进展。
- 未找到企业 Agent 与员工个人 Agent 之间数据归属(离职带不带走)的规则或案例。

---

## 5. 约束与反方论据

### Takeaway
"人人定制专属 Agent"面临四重硬约束:常驻 Agent 的算力成本(大厂用 100–200 美元档或限额免费来门控,自托管账单波动大)、已被大规模验证的安全风险(技能市场投毒、公网暴露、prompt injection 已从 PoC 走向实战)、有限的信任与授权意愿(仅约两成用户给 Agent 金融账户权限,4% 愿让 Agent 独立完成购买),以及明显的数字鸿沟;再加上"强默认通用 Agent 胜过定制"的产品逻辑。

### Cited Findings
**成本**
- 【事实】常驻个人 Agent 的门控:Gemini Spark 限 AI Ultra(约 100 美元/月);Cowork 云端常驻先给 Max(100 美元/月),免费版无 Cowork;Dots 限 Pro/Business Premium(字母榜称 200 美元/月);Muse 有免费档但设 20/100 美元档。— 见第 1 节各来源:[8bittoast](https://8bittoast.com/gemini-spark-roll-out-ultra-subscribers/);[eWeek](https://www.eweek.com/news/claude-cowork-web-mobile-ai-agents/);[Reworked](https://www.reworked.co/digital-workplace/openai-introduces-alwayson-dots-agents/);[The Next Web](https://thenextweb.com/news/meta-muse-personal-ai-agent-launch)
- 【事实】Anthropic 2026-04 以算力成本为由切断订阅额度用于第三方 harness(见第 4 节)。— [The Next Web(2026-04-04)](https://thenextweb.com/news/anthropic-openclaw-claude-subscription-ban-cost/)
- 【二手未核实(厂商/博客估算)】OpenClaw 自托管成本:轻度使用约 2–30 美元/月;常驻 Agent 仅心跳轮询(默认每 30 分钟一次、每次约 6,000 token 上下文)在 Claude Opus 4 定价下约 151 美元/月;有用户报告闲置 Agent 每天 5 美元、定时任务一夜烧 570 万 token、个别重度用户单月 3,600 美元。模型选择决定数量级差异(DeepSeek 档约 1–5 美元/月)。— [haimaker.ai](https://haimaker.ai/blog/openclaw-api-costs-pricing/);[clawdhost 博客](https://clawdhost-landing.pages.dev/blog/openclaw-api-costs-what-nobody-tells-you);[gradually.ai OpenClaw costs](https://www.gradually.ai/en/openclaw-costs/)
- 【观点】字母榜:为微信 14 亿用户每人常驻一台云端虚拟机"算力成本难以承受";千万级日活的元宝才适合当试验场。— [虎嗅转载字母榜(2026-09-30)](https://m.huxiu.com/article/4894871.html)
- 【调查】Menlo 2026:全球消费级 AI 支出由 120 亿美元增至约 400 亿美元,但用户仅增 11%(18 亿→20 亿);付费者典型月支出 20–49 美元;月付 100 美元以上的前 14% 付费者贡献 60% 的支出;付费者使用 Agent 的比例 65%,非付费者 13%。— [Menlo Ventures](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/)

**安全**
- 【事实】ClawHavoc:Koi Security 审计 2,857 个 ClawHub 技能,341 个为恶意(335 个属同一行动),主要载荷为 macOS 窃密木马 Atomic Stealer(AMOS);Unit 42 称这些以 markdown 驱动的技能绕过了 ClawHub 自动扫描与 VirusTotal。其他来源给出 820+ 或 1,184 的更高数字(可靠性较低)。— [Admin By Request](https://www.adminbyrequest.com/en/?p=31644);[Adversa AI](https://adversa.ai/blog/openclaw-security-101-vulnerabilities-hardening-2026/);[安天(Antiy)分析](https://www.antiy.net/p/clawhavoc-analysis-of-large-scale-poisoning-campaign-targeting-the-openclaw-skill-market-for-ai-agents/)
- 【事实】Snyk ToxicSkills(2026-02-05 扫描 ClawHub 与 skills.sh 共 3,984 个技能):1,467 个(36.82%)至少有一项安全问题,534 个(13.4%)有严重级问题,76 个确认含恶意载荷(发布时 8 个仍公开)。注意:"36%"是"任一安全问题"而非仅 prompt injection,Snyk 自己的不同文章表述不一致。— [Snyk(2026-02)](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)
- 【事实】暴露实例:SecurityScorecard 发现 135,000+ 个公网暴露的 OpenClaw 实例(82 国),5 万+ 可被远程代码执行利用,根因是默认绑定所有网卡;2026-03 底 Censys 口径降至 63,070 个。Silverfort 发现可操纵 ClawHub 下载量把恶意技能刷到榜首。— [Admin By Request](https://www.adminbyrequest.com/en/?p=31644);[CyberDesserts](https://blog.cyberdesserts.com/openclaw-malicious-skills-security.md);[Rankiteo](https://blog.rankiteo.com/ope1774434643-openclaw-vulnerability-march-2026)
- 【事实】OpenClaw 漏洞存量(2026-10-29 检索):GitHub advisories 722、OSV.dev 591(口径不同不可直接比较);Trail of Bits 审计 27 份报告、23 项确认(0 严重、2 高危)。— [gradually.ai](https://www.gradually.ai/en/openclaw-statistics/)
- 【事实】中国监管预警:工信部网络安全威胁和漏洞信息共享平台 2026-02-05 发布 OpenClaw 风险预警(默认/不当配置风险高、"信任边界模糊");国家互联网应急中心 2026-03-10 发布风险提示(网页隐藏指令诱导泄露密钥、误删邮件、恶意插件、多个高中危漏洞)。— [新华网(2026-03-10)](https://www.news.cn/tech/20260310/d5e1d772bed046239ea3774903c08970/c.html);[虎嗅(2026-03-11)](https://www.huxiu.com/article/4840894.html)
- 【事实】大厂产品同样中招:OECD 事件库收录 Perplexity Comet 浏览器的零点击 prompt injection 可致凭据被窃(演示性质);Microsoft Copilot Personal 的"Reprompt"(CVE-2026-24307)单击即可外泄数据;个人 Agent Instinct 的内测用户报告其未经批准发邮件、断开 Google 账号后仍在总结 Gmail、并执行了来信中植入的指令;研究者在联系人姓名、地理位置字段中藏指令成功注入 OpenClaw。Cloud Security Alliance 2026-04 研究简报称间接 prompt injection 已"从概念验证进入实战利用"。(其中 Copilot Reprompt 与 Instinct 两条来自安全厂商博客/事件聚合站,建议引用前回溯 Varonis 等一手披露。)— [OECD AI Incidents(2026-03-03)](https://oecd.ai/en/incidents/2026-03-03-3fd7);[barrack.ai](https://blog.barrack.ai/ai-copilot-attack-surface/);[vibegraveyard(Instinct)](https://vibegraveyard.ai/story/instinct-ai-agent-unapproved-email-data-retention/);[Security Boulevard(2026-06)](https://securityboulevard.com/2026/06/compromise-openclaw-with-prompt-injections-in-message-objects/);[CSA 研究简报(2026)](https://labs.cloudsecurityalliance.org/research/csa-research-note-indirect-prompt-injection-in-the-wild-2026/)
- 【事实】Agent"行动型"错误案例:Meta 一位研究员的 Agent 实验以文件被删告终;Replit agent 删除生产数据库;OpenClaw agent 取消了别的顾客的健身房名额。— [The Next Web](https://thenextweb.com/news/meta-muse-personal-ai-agent-launch);[Forward Future(2026-09-08)](https://briefing.forwardfuture.ai/p/why-don-t-people-care-about-ai-agents-yet)

**隐私与监管**
- 【调查】Pew 2026:71% 的美国成年人认为 AI 会让个人信息更不安全(3% 认为更安全);63% 认为 AI 发展过快;59% 对企业负责任地开发 AI 没什么信心,67% 对政府有效监管没什么信心。— [Pew(2026-06-17)](https://www.pewresearch.org/internet/2026/06/17/americans-and-ai-2026/)
- 【事实】地区性缺席:Personal Intelligence 不含 EEA/瑞士/英国;Siri AI 上市时不在欧盟与中国;Muse 仅限美国成年人。— [9to5Google](https://9to5google.com/2026/04/14/gemini-personal-intelligence-global/);[The Decoder](https://the-decoder.com/apple-brings-a-fully-revamped-siri-built-on-googles-gemini-but-not-to-the-eu/);[The Next Web](https://thenextweb.com/news/meta-muse-personal-ai-agent-launch)
- 【事实(政策)】中国 2026-05-08《智能体规范应用与创新发展实施意见》实行分级治理:敏感领域与重点行业备案、检测、问题产品召回;生活娱乐、日常办公等低风险领域以合规自测、信息报告、平台管理、行业自律为主。评论认为监管重心从"内容"转向"行为"。另有《人工智能拟人化互动服务管理暂行办法》自 2026-07-15 起施行(针对拟人化情感互动,非专门针对 Agent)。— [新华网(2026-05-08)](https://www.news.cn/politics/20260508/13043a992f834853a7ce009ba7ecaabc/c.html);[安全内参](https://www.secrss.com/articles/90111);[新华网(2026-04-10)](https://www.news.cn/politics/20260410/bc2a2172b4d64a539cf253e75044b494/c.html)
- 【事实】Meta 相关争议:智能眼镜服务可采集"连续音频"并每隔几秒拍照;FTC 2025-09 就 AI 陪伴与儿童问题调查 Meta 等七家公司(可能过时);Meta 2026-01 暂停青少年使用 AI 角色;MIT 的 Sherry Turkle 称其愿景是"反乌托邦"。— [Fortune(2026-08-10)](https://fortune.com/2026/08/10/zuckerberg-meta-ai-superintelligence/)

**信任与授权边界(人们实际交出什么)**
- 【调查】Menlo 2026(美国 AI 用户):41% 试过 Agent,24% 经常使用;32% 至少一次让 AI 在无最终确认下代为行动(含购物与邮件流程);在用 AI 购物者中 50% 比价、43% 缩小候选、37% 依 AI 建议做最终决定、26% 让 AI 完成购买。选择 AI 工具的首要因素:准确 45%、可信 40%、安全与隐私 36%,易用性由 38% 降至 32%。— [Menlo Ventures](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/)
- 【调查(经 BCG 转述)】Clutch 2026-01 调查:仅 4% 的消费者愿意让 Agent 独立完成购买。— [BCG(2026-09-24)](https://www.bcg.com/x/the-multiplier/personal-ai-agents-compete-on-trust)
- 【调查(方法未披露)】Reviews.org《2026 Consumer Trust Survey》:对 Alexa、Gemini、ChatGPT、Siri 表示担忧的比例分别为 65%、65%、64%、63%。— [Forkast(2026-07-10)](https://forkast.news/64-of-americans-dont-trust-their-ai-assistants-the-agent-revolution-has-a-permission-problem/)
- 【二手未核实(原文 403)】eMarketer 称 64% 的美国成年人"绝不会"用 AI 助手处理订餐、规划行程或网购等任务。— [eMarketer](https://www.emarketer.com/content/ai-assistants-face-consumer-skepticism-value-concerns)
- 【事实(平台数据)】实际用途仍以"问"为主:OpenAI/NBER 研究(2025-09,150 万段对话,可能过时)显示消费级 ChatGPT 约 70% 为非工作用途,消息中"Asking"49%、"Doing"40%、"Expressing"11%;OpenAI Signals 2026Q1 更新(2026-05-11)称工作/非工作比例延续既有趋势。Pew 2026:用 chatbot 查信息 42%、(在职者)工作任务 38%、娱乐 25%、医疗建议 20%、情感支持 10%、陪伴 4%。— [OpenAI](https://openai.com/index/how-people-are-using-chatgpt/);[OpenAI Signals 2026Q1](https://openai.com/signals/research/2026q1-update);[Pew](https://www.pewresearch.org/internet/2026/06/17/americans-and-ai-2026/)
- 【事实(平台数据)】Anthropic Economic Index:2026-01 报告(2025-11 数据)Claude.ai 上 augmentation 略过半;2026-03 报告(2026-02 数据)augmentation 小幅上升,自动化主要出现在 API 流量;前十大任务占 Claude.ai 流量由 24% 降至 19%(用途分散化)。— [Anthropic(2026-03)](https://www.anthropic.com/research/economic-index-march-2026-report);[Anthropic(2026-01)](https://www.anthropic.com/research/anthropic-economic-index-january-2026-report);[The Decoder 解读](https://the-decoder.com/?p=33727)
- 【事实(第三方监测)】QuestMobile:AI 助手整体活跃度偏低,Agent 难以穿透"低频次唤醒"的用户惯性。— [澎湃转载 QuestMobile](https://www.thepaper.cn/newsDetail_forward_33582491)

**数字鸿沟**
- 【调查】Menlo 2026:美国成年人 AI 使用率 64%(2025 年 61%),36% 过去六个月未用 AI;家庭年收入 10 万美元以上者 77% 使用,5 万美元以下者 56%;非用户中 70% 不信任 AI 生成信息(2025 年 58%)、76% 有隐私顾虑、83% 更愿意与人打交道。— [Menlo Ventures](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/);[Digital Applied](https://www.digitalapplied.com/blog/ai-agent-access-permissions-consumer-survey-statistics-2026)
- 【调查】Pew 2026:50 岁以下成年人 57% 用 ChatGPT,50 岁及以上 28%;51% 的美国成年人不使用 chatbot。— [Pew](https://www.pewresearch.org/internet/2026/06/17/americans-and-ai-2026/)
- 【二手】a16z 2026-03 榜单解读:ChatGPT 每周仅触达约 10% 的全球人口;人均 AI 采用率新加坡第一、美国第 20。Stanford AI Index 2026(2026-04-13):生成式 AI 三年内达到 53% 人口采用率,但各国差异大(美国 28%、排第 24——与其他口径冲突);Agent 在多数企业职能中仍是个位数采用率。— [The Decoder](https://the-decoder.com/new-top-100-ai-list-shows-a-market-where-chatgpt-leads-but-no-one-is-loyal/);[Stanford HAI](https://hai.stanford.edu/ai-index/2026-ai-index-report);[Unite.AI 解读](https://www.unite.ai/stanford-ai-index-2026-reveals-a-field-racing-ahead-of-its-guardrails/)

**"强默认胜过定制"的论证**
- 【观点】Forward Future(Nick Wentz,2026-09-08):Agent 要求用户"委托"——连接账户、授予权限、定义工作流、监督结果,这一开销常常超过收益;突破不在于说服数亿人去配置和监督自己的 Agent,而在于产品可靠到让人不必去想底下的 Agent;主流采用将来自"把 agentic 能力无形嵌入人们已在用的产品"。— [Forward Future](https://briefing.forwardfuture.ai/p/why-don-t-people-care-about-ai-agents-yet)
- 【学术】手写/自动生成的配置文件边际收益小甚至为负(见第 2 节)。— [arXiv 2602.11988](https://arxiv.org/abs/2602.11988)
- 【观点】扣子转向的分析:模型能力增强削弱了"搭建"的价值,范式从"搭"转向"说"。— [人人都是产品经理(2026-11-09)](https://www.woshipm.com/ai/6491097.html)
- 【预测,可能过时】Gartner:超过 40% 的 agentic AI 项目将在 2027 年底前被取消(经钛媒体转述)。— [钛媒体](https://www.tmtpost.com/8157089.html)

### Inferences
- 成本约束意味着"人人有常驻专属 Agent"在近期更可能以**分层**实现:免费层=带记忆的助手 + 有限额度的代办;付费层=真正 7×24 的云端 Agent。Menlo 的"付费者 65% 用 Agent vs 非付费者 13%"显示 Agent 的使用已沿付费能力分化。
- 安全证据对"自助定制"尤为不利:技能市场(用户自行安装第三方技能)恰恰是 2026 年最大规模的攻击面;这会把大众推向"平台审核过的技能 + 平台托管的沙箱 VM",进一步压缩个人自由定制的空间。
- 信任数据表明委托是**渐进且分域**的:信息类、比价类任务已被广泛交出,支付、金融账户、不可逆操作的授权率仍低(20–26% 量级,独立购买意愿 4%)。"专属 Agent 替我做一切"离多数人的实际行为尚远。

### Gaps
- 没有各厂商"每用户常驻 Agent 的实际算力成本"的一手披露;OpenClaw 成本数字全部来自厂商/博客估算。
- 未检索到奇安信、360、慢雾关于个人 Agent 的专项报告原文(仅找到工信部/CNCERT 预警与安天分析)。
- 关于"记忆投毒"类攻击(如 MemGhost,单封邮件让常驻 Agent 写入虚假记忆并隐藏)仅在检索摘要中出现,未能定位到原始论文链接。
- 未找到 CNNIC 2026 年关于生成式 AI/智能体用户规模的报告数据。

---

## 6. 可信的预测与领袖表态说了什么?调查与采用数据显示人们今天实际怎么用?

### Takeaway
行业领袖几乎一致地预言"每个人/每个员工都会有 Agent"(Zuckerberg 的 personal superintelligence、Altman 的 Dots、黄仁勋的"OpenClaw 战略"、Hassabis 的 universal assistant、周鸿祎、李彦宏),但他们说的是"每人**有**一个(由平台提供的)Agent",几乎没有人主张"每人**自己定制**一个";而调查数据显示,2026 年美国约半数成年人用 chatbot、约四分之一 AI 用户经常用 Agent,使用仍以问答和增强为主。

### Cited Findings
**领袖表态(均为观点/预测或厂商口径)**
- Mark Zuckerberg:2026-01 财报会把 2026 年定为交付"personal superintelligence"的关键年;2026-08-10 在 Meta newsroom 发文(此前 07-28 在 WSJ 撰文)描绘一个"24/7 on your behalf"贯穿生活各方面的个人 Agent;多家二手报道称 Meta 计划向数十亿人提供免费版、对需要更多算力者收费(该表述未在 Fortune 原文中核到);Meta 首席 AI 官 Alexandr Wang 称"多数人在免费档就能完成所需"。— [Fortune(2026-08-10)](https://fortune.com/2026/08/10/zuckerberg-meta-ai-superintelligence/);[TechCrunch(2026-01-28)](https://techcrunch.com/2026/01/28/zuckerberg-teases-agentic-commerce-tools-and-major-ai-rollout-in-2026);[The Next Web](https://thenextweb.com/news/meta-muse-personal-ai-agent-launch)
- Sam Altman:2026-02 称 personal agents 将"很快成为我们产品的核心",未来是"extremely multi-agent";2026-09-29 称 Dots 是"我们一直为自己想象的真正的 AI……一个永远支持你的 AI 帮手"。— [The Register(2026-02-16)](https://www.theregister.com/2026/02/16/open_ai_grabs_openclaw);[Reworked(2026-09-30)](https://www.reworked.co/digital-workplace/openai-introduces-alwayson-dots-agents/)
- 黄仁勋(GTC 2026,2026-03-16):"今天世界上每家公司都需要一个 OpenClaw 战略、一个 agent 系统的战略",把 OpenClaw 比作个人 Agent 时代的操作系统(类比 Windows、HTTP、Linux、Kubernetes);并预言年度 token 预算将成为招聘标配。【二手未核实】称其在 All-In 播客说每个工程师将有上百个 Agent。— [Analytics India Magazine](https://analyticsindiamag.com/ai-trends/jensen-huang-believes-every-software-company-needs-an-openclaw-strategy);[Diginomica](https://diginomica.com/huangs-memory-nvidias-gtc-tells-us-future-has-claws);[CP24/CNN(2026-03-16)](https://www.cp24.com/news/world/2026/03/16/the-worlds-most-valuable-company-just-sent-another-signal-that-ai-agents-are-going-to-be-everywhere/)
- Demis Hassabis(Axios AI+ Summit,约 2025-12,接近 12 个月时效边界):目标是跨设备管理日常生活的"universal assistant",并称 Agent 一年内将"接近"能自主处理复杂任务。— [The Decoder](https://the-decoder.com/deepmind-ceo-demis-hassabis-predicts-three-major-ai-trends-for-2026/)
- 周鸿祎(2026-03 两会期间):2026 年是智能体大规模应用的关键之年,未来每个普通人身边可能围绕着几个智能体;提出智能体分级,L4 为多智能体"蜂群"协作。— [同花顺转载(2026-03-03)](https://news.10jqka.com.cn/20260303/c675027140.shtml);[人民日报社《中国经济周刊》(2026-03-15)](https://paper.people.com.cn/zgjjzk/pc/content/202603/15/content_30146837.html)
- 李彦宏(Create 2026,2026-05-13):提出"日活智能体数 DAA"作为新指标,预测全球 DAA 未来可能超过 100 亿;生产力最小单元从团队变为"一个人 + 一支智能体编队"的"超级个体"。— [每日经济新闻(2026-05-13)](https://www.nbd.com.cn/articles/2026-05-13/4391104.html);[澎湃](https://m.thepaper.cn/newsDetail_forward_33174389)
- 傅盛:亲身实验后称"AGI 时刻",但认为普通人门槛在工程层面(见第 2 节)。— [凤凰科技](https://tech.ifeng.com/c/8rF8HpQwkWE)
- 行业分析(钛媒体):市场分化为"面向个人的消费级 Agent"与"面向组织的企业级 Agent"两条赛道,个人级 Agent 本质是"个人数字替身"。— [钛媒体](https://www.tmtpost.com/8157089.html)

**调查与采用数据**
- 【调查】Pew(2026-02 调查,2026-06-17 发布,n=5,119):49% 的美国成年人用过 AI chatbot(2024 年 33%);24% 每天使用(4% 几乎不间断);仅 16% 认为 AI 未来 20 年对社会影响为正面,40% 认为负面。**该报告未涉及 Agent/代为行动**。— [Pew](https://www.pewresearch.org/internet/2026/06/17/americans-and-ai-2026/)
- 【调查】Menlo/Morning Consult(2026-07,n=5,067;Menlo 是 Anthropic 等 AI 公司的投资方):64% 的美国成年人使用 AI,25% 每天使用;55% 的 AI 用户为至少一款 AI 产品付费;72% 的 AI 用户知道 Agent,41% 试过,24% 经常用;Agent 用户 92% 付费、63% 每天用 AI。— [Menlo Ventures(2026-09)](https://menlovc.com/perspective/2026-the-state-of-consumer-ai/)
- 【调查】Gallup(2026-02-04 至 02-19,n=23,717 名美国雇员):约一半雇员每年至少几次在工作中用 AI,13% 每天用,28% 每周数次及以上。未涉及 Agent。— [TechRadar 转述 Gallup](https://www.techradar.com/pro/is-this-the-tipping-point-for-ai-at-work-new-gallup-survey-finds-half-of-all-us-employees-now-use-it-in-some-way);[Gallup](https://www.gallup.com/workplace/704225/rising-adoption-spotlights-workforce-changes.aspx)
- 【调查】Reuters Institute《Generative AI and News Report 2026》(2026-10):有趋势数据的六国中,每周使用生成式 AI 的比例由 34% 升至 51%,每天使用 28%;ChatGPT 周使用 22%→34%,Gemini 11%→24%。《Digital News Report 2026》:每周用 AI chatbot 获取新闻的比例 7%→10%。— [Reuters Institute(2026-10)](https://reutersinstitute.politics.ox.ac.uk/generative-ai-and-news-report-2026-standalone-tools-information-infrastructure);[Nieman Lab(2026-11)](https://www.niemanlab.org/2026/11/ai-is-becoming-an-information-gateway-audiences-still-dont-want-it-making-their-news/)
- 【报告】Stanford AI Index 2026(2026-04-13):生成式 AI 对美国消费者的年化价值估计约 1,720 亿美元;Agent 能力快速提升(Terminal-Bench 成功率 20%→77.3%),但 Agent 在多数企业职能的采用率仍为个位数。— [Stanford HAI](https://hai.stanford.edu/ai-index/2026-ai-index-report);[Unite.AI](https://www.unite.ai/stanford-ai-index-2026-reveals-a-field-racing-ahead-of-its-guardrails/)
- 【平台数据】OpenAI 用途研究与 Anthropic Economic Index 均显示以问答/增强为主(见第 5 节)。— [OpenAI](https://openai.com/index/how-people-are-using-chatgpt/);[Anthropic](https://www.anthropic.com/research/economic-index-march-2026-report)
- 【第三方监测】QuestMobile:中国 AI 原生 App 月活 4.99 亿、手机厂商 AI 7.55 亿,但 AI 助手"低频次唤醒"(见第 1 节)。— [澎湃转载 QuestMobile](https://www.thepaper.cn/newsDetail_forward_33582491)
- 【二手,存在错误】a16z Top 100(2026-03,第六版)二手解读把 personal/horizontal agents 列为主题;其中"OpenClaw 被 OpenAI 收购"的说法与一手报道(作者入职、项目转基金会)**不符**,引用时需更正。— [The Neuron](https://www.theneuron.ai/explainer-articles/a16z-just-ranked-the-100-most-popular-ai-apps-heres-the-full-list-and-what-it-tells-us-/);对照 [The Register](https://www.theregister.com/2026/02/16/open_ai_grabs_openclaw)

### Inferences
- 把领袖表态逐句对照可见:**共识是"人人有 Agent",而非"人人定制 Agent"**。Zuckerberg/Altman/Hassabis 的方案都是平台为你实例化并托管;黄仁勋与李彦宏谈的是企业/开发者侧的 Agent 战略与"超级个体";只有 OpenClaw/Hermes 社区与傅盛式的个人实验接近"亲手养一个",而傅盛本人也承认门槛高。
- 采用曲线的现实位置:chatbot 已过半数(美国 49–64%,视口径),"经常使用 Agent"约占 AI 用户的四分之一(约合美国成年人的 15% 上下,由 64%×24% 粗算),"常驻专属 Agent"仍是付费早期用户的事。
- 综合六节证据,可给报告撰写者的三种情景判断(属推断,非事实):
  1. **最可能(中间情景)**:几年内多数联网用户都会"有"至少一个个性化 Agent,但它由平台提供、靠自动积累的记忆与授权的连接器而变得"专属";亲手构建/深度定制者是少数(开发者、极客、企业 IT、内容创作者),他们生产的 skills/plugins 被多数人以"默认 + 一键启用"的方式消费。
  2. **强命题("人人亲手定制、自有自控")**:证据不支持——GPT Store 退役、扣子收编、默认值效应、安全事件、成本门控、生态封堵都指向相反方向。
  3. **反命题("定制无意义,只有一个通用默认 Agent")**:也过强——记忆/上下文层的个体差异、企业 specialist agent、开源自托管社区的持续增长、以及 skills/MCP 标准化都说明定制作为"供给侧能力"会长期存在,只是主体不是每个普通人。

### Gaps
- 未找到 Dario Amodei、Satya Nadella 关于"每个人都会有个人 Agent"的可核实原话(Amodei 的公开表态集中于 Agent 能力与软件工程自动化;Nadella 的检索结果集中于 Copilot/Agent 365 数据)。
- 未找到张一鸣/梁汝波、马化腾在 2026 年关于"人人专属 Agent"的公开表态原文(字节与腾讯的个人智能体计划仅见于字母榜独家报道)。
- Pew、Gallup 2026 年的公开结果均未单独测量"AI agent/代为行动"的使用;目前对消费者 Agent 使用最细的调查来自有利益相关的 Menlo Ventures(Anthropic 投资方),需注意立场。
- 未找到 CNNIC、Sensor Tower/Similarweb 针对"个人 Agent"类目的 2026 年数据。
- 所有"2026 年末用户数"类数字(ChatGPT 10 亿周活、Meta AI 月活等)缺少一手确认,撰写时建议使用带日期的保守口径(ChatGPT 9 亿周活 @2026-02;豆包 3.82 亿月活 @2026-05)。
