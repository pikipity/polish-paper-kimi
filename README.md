# Polish Paper — IEEE Transaction 论文交互式润色

> 一个 Kimi CLI Skill，帮你把论文润色到能投 IEEE Transaction 的水准，同时去掉让人一眼看出是 AI 写的痕迹。

## 核心特性

- **多段逻辑先行**：给多个自然段时，先分析段落间逻辑结构，确认合理后再逐段润色
- **逐段交互确认**：每一段润色后都停下来等你确认，满意了才继续下一段
- **润色 + 去 AI 感两步走**：先学术润色，再自动 humanizer 去 AI 感
- **格式自适应**：给 LaTeX 就保留命令，给纯文本就保持原样
- **改动全透明**：每段输出 Modification Log 表格，改了哪里一目了然

## 安装

将本项目的 skill 注册到 Kimi CLI：

```bash
# 方式一：安装到用户 skill 目录
mkdir -p ~/.kimi/skills
cp -r polish-paper ~/.kimi/skills/

# 方式二：在 Kimi CLI 中通过 skill-installer 安装
# 待补充
```

## 使用方法

### 单自然段润色

直接粘贴一段英文论文文本，skill 会自动润色并输出结果：

```
请润色下面这段：

The proposed method achieves good results. It is worth noting that ...
```

### 多自然段润色

粘贴多段文本（用空行分隔），skill 会进入**交互式流程**：

1. **Phase 1 — 逻辑分析**：先输出段落结构总览和逻辑评价，等你确认
2. **Phase 2 — 逐段润色**：每段依次执行「学术润色 → 去 AI 感 → 输出结果」

交互指令：

| 阶段 | 你说 | Skill 做 |
|:---|:---|:---|
| 逻辑分析后 | `逻辑OK` / `继续` | 进入逐段润色 |
| 逻辑分析后 | `调整：xxx` | 重新分析 |
| 每段润色后 | `满意` / `next` | 进入下一段 |
| 每段润色后 | `修改：xxx` | 按建议修改当前段 |
| 每段润色后 | `重新润色` | 重做当前段 |
| 任意时候 | `全部完成` | 输出已确认段落的合并版本 |

## 工作流程

```
用户输入
    │
    ├─ 单自然段 ───────→ 直接润色 → 输出结果
    │
    └─ 多自然段 ───────→ Phase 1: 段落间逻辑分析
                                │
                                ▼
                        输出逻辑报告，等待用户确认
                                │
                                ▼
                        Phase 2: 逐段润色（每段）
                            │
                            ├─ Step 1: 学术润色
                            ├─ Step 2: Humanizer 去 AI 感
                            └─ 输出：最终文本 + Modification Log
                                │
                                ▼
                        等待用户确认，满意后进入下一段
```

## Modification Log 表格

每段润色后会输出如下格式的改动记录：

| 序号 | 修改位置（原文） | 修改后 | 修改类型 | 修改原因 |
|:---:|:---|:---|:---|:---|
| 1 | achieves good results | achieves competitive performance | 用词改进 | "good" 过于口语 |
| 2 | It is worth noting that | （删除） | 去AI感 | 删除机械连接词 |
| 3 | ... | ... | 语法修正 | 修正冠词错误 |

## 润色规范

本 Skill 针对 **IEEE Transaction** 的出版标准设计，核心约束包括：

- **零错误**：拼写、语法、标点、冠词零容忍
- **Simple & Clear**：拒绝生僻词和华丽辞藻
- **逻辑连贯**：注重句间、段间逻辑衔接
- **不臆造**：严禁添加原文不存在的数据或结论
- **保持风格**：尊重作者原有行文风格
- **去 AI 感**：禁用机械连接词，长短句交替，避免被动语态堆砌

## 项目结构

```
polish-paper-kimi/
├── README.md                          # 本文件
├── AGENTS.md                          # Agent 开发指南
└── polish-paper/
    └── SKILL.md                       # Skill 主文件
```

## License

MIT
