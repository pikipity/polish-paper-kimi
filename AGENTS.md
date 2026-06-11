# Agent 开发指南 — Polish Paper

## 项目概述

本项目是一个 Kimi CLI Skill，用于交互式润色 IEEE Transaction 级别的英文学术论文。核心特点是**多段逻辑整理 + 逐段交互确认 + 润色后去除 AI 感**。

## 目录结构

```
polish-paper-kimi/
├── README.md                          # 面向人类用户的说明
├── AGENTS.md                          # 本文件
└── polish-paper/
    └── SKILL.md                       # Skill 主定义文件
```

## Skill 文件规范

### 位置

Skill 文件目前位于 `polish-paper/SKILL.md`。Kimi CLI 通过此路径加载 skill 定义。

### 文件格式

SKILL.md 采用标准 Kimi CLI Skill 格式：

```markdown
---
name: polish-paper
description: |
  多行描述...
---

# 标题

## 触发条件
...

## 工作流程
...

## Prompt 模板
...
```

### 修改原则

1. **Prompt 是核心**：SKILL.md 中的「润色 Prompt 模板」直接决定润色质量，修改需谨慎
2. **约束优先于自由**：所有 Constraints 以「严禁」「必须」开头，减少模型自由发挥空间
3. **两步流程固定**：Step 1（学术润色）→ Step 2（去 AI 感），顺序不可颠倒
4. **交互指令稳定**：用户依赖 `"逻辑OK"`、`"满意"` 等指令推进流程，变更需考虑兼容性

## 工作流程详解

### 步骤 1：输入类型判断

- **多自然段**（空行分隔的 ≥2 段）→ 进入 Phase 1
- **单自然段** → 跳过 Phase 1，直接进入 Phase 2

### Phase 1: 段落间逻辑整理

输出结构固定为：
1. 段落结构总览（每段的核心作用）
2. 逻辑连接评价（顺序、过渡、断层）
3. 改进建议（如无不输出）

**必须等待用户确认**后才可以进入 Phase 2。

### Phase 2: 逐段润色 + 去 AI 感

每段执行两步：

1. **Step 2a — 学术润色**
   - 修正语法、优化句式、提升学术严谨性
   - 注重句间逻辑和段间逻辑
   - IEEE Transaction 语体规范

2. **Step 2b — 去 AI 感处理**
   - 禁用机械连接词（First and foremost, It is worth noting that, Lastly 等）
   - 长短句交替
   - 控制被动语态密度
   - 拒绝空洞概括
   - 严禁加粗/斜体/emoji

**每段输出必须包含**：
- 最终文本（两步后的结果）
- Modification Log 表格（五列：序号、修改位置、修改后、修改类型、修改原因）

**必须等待用户确认**后才可以进入下一段。

## 关键设计决策

### 为什么去掉 Role？

原 Prompt 以「资深学术编辑」角色开头，容易让模型过度发挥、按自己的审美大幅改写。去掉 Role、直接以 Task 驱动，可以减少不必要的"编辑存在感"，让模型更克制。

### 为什么分两步（润色 → 去 AI 感）？

学术润色需要正式、严谨、规范；去 AI 感需要自然、变化、有节奏。两者目标有张力：
- 如果合并为一步，模型容易为了"自然"而牺牲"严谨"
- 分开执行，先确保学术质量达标，再在此基础上做自然化处理，更容易平衡

### 为什么交互式？

论文润色是高度主观的工作。作者对"保留原风格""不要改这句"有具体偏好。交互式流程让作者每一步都能干预，避免一次性输出大量修改后作者无法接受。

### 为什么 Modification Log 用表格？

透明化改动，让作者快速判断：
- 哪些改动是必要修正（语法错误）
- 哪些改动是风格调整（可能需要作者判断接受与否）
- 哪些是去 AI 感处理

## 扩展建议

如需扩展本 Skill，可考虑以下方向：

1. **增加其他期刊支持**：在 Task 中增加期刊选择变量（IEEE Transaction / ACL / CVPR 等），不同期刊的语体要求不同
2. **支持中英混合输入**：当前仅支持英文论文片段，可考虑增加中文草稿的中转英支持
3. **段落类型自动识别**：自动判断段落是 Introduction / Method / Experiment / Conclusion，应用不同的润色侧重
4. **批量模式**：增加非交互模式（`--batch`），适合对已有成熟草稿进行快速统一润色

## 触发边界与冲突规避

### 与 humanizer skill 的边界

用户本地同时安装了 `humanizer`（通用文本去 AI 感）和 `polish-paper`（学术论文润色）。两者的触发条件如果重叠，会导致 Kimi CLI 同时激活两个 skill，产生指令冲突。

**冲突根因**：
- `humanizer` 的 description 包含 `polishing` 关键词
- 如果 `polish-paper` 的 description 中出现 "humanizer" 或过于泛化的 "去 AI 感"，会被 AI 判定为与 humanizer 同场景

**规避策略**：
1. `polish-paper` 的 description **严禁出现 "humanizer" 一词**，改用"去除 AI 写作痕迹"
2. `polish-paper` 的 description **必须限定 "英文学术论文"**，与 humanizer 的通用场景形成区隔
3. `polish-paper` 内部 Prompt 中的去 AI 感规则**独立内聚**，不依赖外部 humanizer skill

**触发边界对照**：

| 用户输入 | 预期触发 | 原因 |
|:---|:---|:---|
| "humanize this blog post" | 只触发 **humanizer** | polish-paper 限定"学术论文" |
| "remove AI patterns from this email" | 只触发 **humanizer** | polish-paper 限定"学术论文" |
| "润色这段论文" | 只触发 **polish-paper** | 匹配"学术论文润色" |
| "polish this IEEE paper" | 只触发 **polish-paper** | 明确匹配 |
| "去一下 AI 感，这是论文草稿" | 两者都可能 | 灰色地带，AI 根据上下文自行判断；用户可用 `/skill:polish-paper` 明确指定 |

### description 演进记录

| 版本 | description 内容 | 问题 |
|:---|:---|:---|
| v1 | "支持多段逻辑整理 + 逐段润色 + 自动 humanizer 去 AI 感" | 包含 "humanizer" 关键词，与 humanizer skill 触发冲突 |
| v2（当前） | "IEEE Transaction 英文学术论文交互式润色 Skill。支持多段逻辑整理、逐段润色、去除 AI 写作痕迹。仅用于英文学术论文..." | 明确限定场景，规避冲突 |

## 注意事项

- 修改 SKILL.md 后，建议用实际论文片段测试，验证交互流程是否正常推进
- 不要过度扩展 Prompt 的 Constraints，约束越多模型越容易"失忆"，保持核心约束在 5-7 条内
- 去 AI 感规则已内聚在 polish-paper 内部，不依赖外部 humanizer skill；但 humanizer skill 本身更新时，可考虑同步检查 polish-paper 内的规则是否需要对齐
