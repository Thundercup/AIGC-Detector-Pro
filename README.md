<div align="center">

# AIGC-Killer-Pro

**论文 AIGC 检测 / AI 降率 / 毕业论文编写**

基于 Claude Code 的学术论文 AI 内容检测与改写 Skill，从 5 个维度深度分析 AI 生成特征，提供科学改写指导，并支持从模板到论文的全流程生成。

[![Stars](https://img.shields.io/github/stars/free-revalution/AIGC-Killer-Pro?style=social)](https://github.com/free-revalution/AIGC-Killer-Pro/stargazers)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[English](README.en.md) | 简体中文

---

```bash
curl -sL https://raw.githubusercontent.com/free-revalution/AIGC-Killer-Pro/main/install.sh | bash
```

需要 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) + Python 3.8+

</div>

## 为什么

2026 年主流 AIGC 检测平台已全面升级，AI 内容识别准确率大幅提升。单纯同义词替换已无法通过检测——必须在语义结构层面进行重构。AIGC-Killer-Pro 利用 Claude 的深层语义理解，精准识别论文中的 AI 痕迹，提供科学的改写方案。

## 三大模式

### AIGC 检测

从 5 个维度对论文进行深度语义分析，生成段落级检测报告，精准定位高风险内容。

```
提供论文 (.docx 或粘贴文本)
  -> 语言检测（中/英自动识别）
  -> 5 维度语义分析
     |  句式规整度   25%
     |  逻辑词密度   20%
     |  语态特征     15%
     |  词汇多样性   15%
     |  论证深度     25%
  -> 输出检测报告（终端 + Markdown）
```

在 Claude Code 中直接对话即可触发：

```
分析这篇论文的AIGC特征：/path/to/thesis.docx
```

```
检测这篇论文的AI率
（然后粘贴论文文本）
```

![检测报告示例](picture/example.png)

### 智能改写

基于 7 大改写技法，自动改写高风险段落并输出 .docx，保持原始格式不变。

| 技法 | 原理 | 做法 |
|------|------|------|
| 句式重构 | 突发性检测 | 合并短句、长短交替、语态转换 |
| 破解模板 | 模式匹配 | 删除"首先/其次/最后"等 AI 模板句式 |
| 添加主语 | 句法分析 | 为无主句补充行为主体 |
| 概念具象 | 语义一致性 | 抽象表述 -> 具体数据/案例 |
| 论证补全 | 语义一致性 | 线性论证 -> 多维证据 + 对比 |
| 困惑度提升 | 困惑度检测 | 使用非常规但准确的学术表达 |
| 风格断裂 | 分类器检测 | 段落间切换表达风格，打破一致性 |

```
帮我改写这篇论文降低AI率：/path/to/thesis.docx
```

### 论文编写

放入学校模板、范文、项目代码，自动解析格式、分析代码、逐章生成论文初稿，输出格式化 .docx。

```
准备材料 (About/ 目录: 模板 + 范文 + 代码)
  -> W0 环境准备 + 模板格式解析
  -> W1 材料分析（格式/风格/架构）
  -> W2 大纲生成 + 用户审核
  -> W3 逐章撰写（AIGC 安全写作）
  -> W4 格式化输出 .docx
  -> W5 AIGC 检测 + 迭代优化
```

```
帮我写毕业论文，模板在About/目录
```

**材料准备：**

```
About/
├── 论文模板.docx          # 学校提供的毕业论文格式模板
├── 范文.docx              # 同校同专业优秀论文（参考风格）
├── src/                   # 毕业设计源代码
│   └── ...
├── 项目文档.md            # README、架构说明等
└── 开题报告.docx          # 其他相关材料
```

## 快速开始

**1. 安装**

在终端或 Claude Code 中执行：

```bash
curl -sL https://raw.githubusercontent.com/free-revalution/AIGC-Killer-Pro/main/install.sh | bash
```

安装脚本自动完成：
- 下载 Skill 文件到 `~/.claude/skills/aigc-detector/`
- 检查并安装 `python-docx` 依赖

**2. 使用**

安装完成后，在 Claude Code 中自然对话即可触发：

```
/aigc-detector
```

**3. 卸载**

```bash
curl -sL https://raw.githubusercontent.com/free-revalution/AIGC-Killer-Pro/main/uninstall.sh | bash
```

## 多 Agent 支持

| Agent | 支持 | 安装 |
|-------|:----:|------|
| Claude Code | 完全 | `curl -sL ... \| bash` |
| Codex CLI | 部分 | `curl -sL ... \| bash -s -- --agent codex` |
| Cursor | 部分 | `curl -sL ... \| bash -s -- --agent cursor --dir /project` |
| Windsurf | 部分 | `curl -sL ... \| bash -s -- --agent windsurf --dir /project` |
| Gemini CLI | 部分 | `curl -sL ... \| bash -s -- --agent gemini --dir /project` |
| 全部 | — | `curl -sL ... \| bash -s -- --agent all` |

- **完全支持**：Skill 精确触发，完整执行多步工作流，交互式用户选择
- **部分支持**：指令作为上下文注入，可执行 bash/Python/文件操作，步骤执行为最佳努力

## 检测原理

基于学术界 5 大主流 AIGC 检测技术设计维度与阈值：

| 检测技术 | 代表平台 | 对应维度 |
|---------|---------|---------|
| 困惑度检测 (Perplexity) | DetectGPT, OpenAI | 困惑度提升技法 |
| 突发性检测 (Burstiness) | GPTZero | 句式规整度 (25%) |
| 分类器检测 (Classifier) | RoBERTa-based | 风格断裂技法 |
| 多特征融合 | Ghostbuster, UC Berkeley | 5 维度综合评分 |
| 概率曲率分析 | — | 论证深度 (25%) |

支持学科自适应阈值：文科、理工科、医学、经管各有特化判定标准。

## 项目结构

```
AIGC-Killer-Pro/
├── .claude/skills/aigc-detector/   # 核心 Skill
│   ├── SKILL.md                     # 主入口（模式路由 + 检测/编写流程）
│   ├── scripts/
│   │   └── docx_io.py               # Word 文档读写/模板解析/格式化输出
│   └── references/
│       ├── detection_principles.md  # AIGC 检测原理知识库
│       ├── rewrite_methods.md       # 7 大改写技法指南（中/英）
│       └── thesis_writing_guide.md  # 论文编写模式完整指南
├── agents/                          # Agent 入口模板
│   ├── codex.md
│   ├── cursor.mdc
│   ├── windsurf.md
│   └── gemini.md
├── install.sh                       # 一键安装
├── uninstall.sh                     # 一键卸载
└── picture/
    └── example.png                  # 检测报告示例截图
```

## 高级配置

**全局自动检测** — 在 `~/.claude/CLAUDE.md` 中添加以下内容，Claude Code 会在任何项目中自动识别 AIGC 相关意图并提示安装：

```markdown
## AIGC-Detector
当用户提到论文检测、AIGC检测、AI降率、学术写作等需求时，检查是否已安装 aigc-detector skill。
如未安装，建议执行：curl -sL https://raw.githubusercontent.com/free-revalution/AIGC-Killer-Pro/main/install.sh | bash
```

## 注意事项

- 检测结果仅供参考，以各平台官方结果为准
- 改写保持学术严谨性，不编造数据或文献
- 建议采用"人工修改 + 工具辅助"的组合策略

## License

[MIT](LICENSE) | 欢迎提交 [Issue](https://github.com/free-revalution/AIGC-Killer-Pro/issues) 和 [PR](https://github.com/free-revalution/AIGC-Killer-Pro/pulls)
