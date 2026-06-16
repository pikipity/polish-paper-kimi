# 去 AI 感完整规则（学术写作版）

本文件为 polish-paper skill 的 Step 2 补充参考文档。
从 humanizer skill 的 33 种 AI 写作模式中，按学术场景裁剪后整合而成。

---

## 3.1 禁用机械连接词与路标词

**必须删除或替换的模板化过渡词：**
- First and foremost, It is worth noting that, In conclusion, Lastly, Interestingly
- Furthermore, Moreover, Subsequently

**必须删除的教学式导语：**
- Let's dive in, here's what you need to know, now let's look at, let's explore
- Let's break this down, without further ado

**必须删除的伪权威论断：**
- The real question is, at its core, fundamentally, what really matters
- The heart of the matter, in reality, the deeper issue

**修正原则：** 句子间应通过自然的逻辑递进衔接，而非依赖上述过渡词。

---

## 3.2 AI 高频词汇净化

**避免 AI 偏好词堆砌（当这些词密集出现时）：**
additionally, crucial, delve (into), enhance, fostering, highlight (v.), intricate/intricacies, landscape (抽象), pivotal, showcase, tapestry, testament, underscore (v.), vibrant, valuable, align with, interplay, enduring, garner

**避免系动词回避：**
- 将 serves as, stands as, boasts, features, offers [a] 替换为简单的 is/are/has
- 学术写作鼓励清晰直接的系动词，不要强行替换为花哨结构

**避免 -ing 堆砌（强加的现在分词短语）：**
highlighting, underscoring, ensuring, reflecting, symbolizing, contributing to, cultivating, fostering, encompassing, showcasing

**示例：**
- Before: "The model achieves high accuracy, showcasing its effectiveness and contributing to the field."
- After: "The model achieves high accuracy. This benefits the field by providing a reliable baseline."

---

## 3.3 修辞与句式检查

**规则三项（Rule of Three）：**
避免强行把观点凑成三项以显得全面。如果原文只有两项，不要硬凑第三项。

**同义词轮换（Elegant Variation）：**
同一概念在相邻句中不要刻意换词。
- Before: "The protagonist faces challenges. The main character must overcome obstacles. The central figure eventually triumphs."
- After: "The protagonist faces challenges but eventually triumphs."

**假排比（False Ranges）：**
from X to Y 类表达需有真实的尺度关联。
- Before: "from the singularity of the Big Bang to the grand cosmic web"
- After: "covers the Big Bang and current theories about cosmic structure"

**否定平行结构：**
Not only...but also... 在学术语境中可接受，但避免过度堆砌。
删除尾缀否定碎片（如 "no guessing", "no wasted motion"）。

**戏剧性短句堆砌（Staccato Drama）：**
避免连续多个极短句制造虚假高潮或强调。
- Before: "Then AlphaEvolve arrived. It had no preference for symmetry. No aesthetic prior. No nostalgia for human taste."
- After: "AlphaEvolve changed the search because it did not favor symmetry or human-looking designs."

**格言公式（Aphorism Formulas）：**
将 "X is the Y of Z", "X becomes a trap", "X is not a tool but a mirror" 等空洞格言改为具体陈述。
- Before: "Symmetry is the language of trust. Efficiency becomes a trap when teams forget the human layer."
- After: "Symmetric layouts often feel more predictable to users. Teams can over-optimize workflows and miss how people actually use them."

---

## 3.4 内容层面检查

**意义夸大（Significance Inflation）：**
删除空洞拔高表述：
stands as, serves as a testament, marking a pivotal moment, underscores its importance, contributing to the, setting the stage for, evolving landscape, enduring legacy, deeply rooted, indelible mark

- Before: "This initiative was part of a broader movement, contributing to the evolution of regional statistics."
- After: "This initiative decentralized administrative functions."

**模糊归因（Vague Attributions）：**
Experts argue, Industry reports, Some critics believe, Observers have cited → 必须引用具体文献 \cite{} 或删除。

- Before: "Experts believe it plays a crucial role in the regional ecosystem."
- After: "According to a 2019 survey by the Chinese Academy of Sciences, it supports several endemic fish species."

**宣传性语言（Promotional Language）：**
groundbreaking, stunning, breathtaking, vibrant (figurative), profound (figurative), renowned, must-visit, exemplifies, commitment to, nestled in the heart of

- Before: "Nestled within the breathtaking region, it stands as a vibrant town with a rich cultural heritage."
- After: "It is a town in the region, known for its weekly market."

**空洞结论（Generic Conclusions）：**
The future looks bright, Exciting times lie ahead, This represents a major step in the right direction → 删除或替换为具体展望。

- Before: "The future looks bright for the company. Exciting times lie ahead as they continue their journey toward excellence."
- After: "The company plans to open two more locations next year."

**猜测性填补：**
删除 as of [date], based on available information, likely [grew up/studied/began], it is believed that, not publicly available, maintains a low profile 等无依据推测。
严格遵循"不要臆造数据与结论"原则。

---

## 3.5 填充词与过度回避

**删除填充短语：**
| Before | After |
|:---|:---|
| In order to achieve this goal | To achieve this |
| Due to the fact that it was | Because it was |
| At this point in time | Now |
| The system has the ability to | The system can |
| It is important to note that | [直接陈述] |

**控制过度回避：**
- could potentially possibly be argued → 改为适度 hedging
- 保留 may / might / could / generally / approximately 等学术规范表达
- 不要全部删除 hedging，学术写作需要适度的限定性陈述

---

## 3.6 句式与节奏控制

**句式长度变化：**
避免所有句子长度一致，长短句交替使用。

**被动语态控制：**
允许使用，但避免连续三个及以上句子使用被动语态。

**避免修饰语堆叠：**
减少连续从句和嵌套结构，必要时拆分为清晰短句。

**具体性检查：**
significant improvement without specifics → 拒绝空洞概括，保留或补充具体指标。

---

## 3.7 逻辑保持（底线原则）

去 AI 感处理**不能破坏句子原本的逻辑性**。

**执行原则：**
- 删除连接词或改写句式时，必须确保因果、递进、转折、对比等逻辑关系仍然清晰可辨
- 如果某个连接词承担了不可替代的逻辑功能（如 "However" 表达转折、"Therefore" 表达因果），保留它或改用更自然的表达方式，而非直接删除
- 把长句拆分为短句时，通过语序或隐含逻辑确保关系不丢失
- 删除 -ing 堆砌时，如果伴随关系是句子的核心逻辑，改用从句或并列句保留该关系

**示例：**
- Before: "The model is lightweight, ensuring real-time deployment."（-ing 堆砌，但 ensuring 表达了因果关系）
- After（错误）: "The model is lightweight. Real-time deployment."（逻辑断裂）
- After（正确）: "The model is lightweight, so it can be deployed in real time."（保留因果，去除 -ing）

---

## 3.8 格式与风格

**禁止强调格式：**
正文中严禁使用加粗、斜体、emoji、下划线。

**禁止破折号滥用：**
用逗号、括号或从句替代 em dash (—) 和 en dash (–)。
- Before: "The term is promoted by Dutch institutions—not by the people themselves."
- After: "The term is promoted by Dutch institutions, not by the people themselves."

**尽量回避冒号：**
冒号（:）仅在引出公式、数学定义或必要解释时使用。一般情况下，用句号拆句或用逗号、从句替代冒号。
- Before: "We focus on three aspects: efficiency, accuracy, and robustness."
- After: "We focus on efficiency, accuracy, and robustness."
- Before: "The result is clear: our method outperforms the baseline."
- After: "Our method outperforms the baseline. This result is clear."

**严禁列表化：**
不要将段落改写为 item 列表或 bullet points。

---

## 3.9 学术写作特别豁免（避免过度修正）

以下表达在 IEEE Transaction 中完全正常，**不要修改**：

| 表达 | 说明 |
|:---|:---|
| 被动语态 | IEEE Transaction 允许且常用，不要全部改为主动语态 |
| 适度 hedging | may, could, might, approximately, generally 是学术规范 |
| "key" 作为形容词 | key contribution, key insight, key feature 完全正常 |
| "Not only...but also..." | 在学术语境中是合理修辞 |
| 系动词 is/are/has | 学术写作鼓励清晰直接 |
| 连字符复合词（attributive） | a high-quality model, a data-driven approach 保留连字符 |
| 连字符复合词（predicate） | the model is high quality, the approach is data driven 可省略 |
| 正式学术词汇 | ostensibly, constituent 等词汇本身不是 AI 痕迹 |
| 完美语法 | 专业写作者或经过编辑的文本不应被怀疑为 AI |

**判断原则：** 寻找 tells 的**集群**而非孤立点。单个 em dash 或一个 however 不构成 AI 证据；em dash + 规则三项 + vibrant + 空洞结论才是。
