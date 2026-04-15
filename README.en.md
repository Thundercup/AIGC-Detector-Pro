<div align="center">

# AIGC-Killer-Pro

**AIGC Detection / AI Rate Reduction / Thesis Writing**

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) Skill for academic paper AI content detection, rewriting, and thesis generation. Analyzes papers across 5 dimensions, provides targeted rewrite guidance, and supports end-to-end thesis writing from templates.

[![Stars](https://img.shields.io/github/stars/free-revalution/AIGC-Killer-Pro?style=social)](https://github.com/free-revalution/AIGC-Killer-Pro/stargazers)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
English | [简体中文](README.md)

---

```bash
curl -sL https://raw.githubusercontent.com/free-revalution/AIGC-Killer-Pro/main/install.sh | bash
```

Requires [Claude Code](https://docs.anthropic.com/en/docs/claude-code) + Python 3.8+

</div>

## Why

By 2026, mainstream AIGC detection platforms have comprehensively upgraded their AI content identification. Simple synonym replacement no longer works — semantic restructuring is required. AIGC-Killer-Pro leverages Claude's deep semantic understanding to precisely identify AI-generated patterns and provide scientifically-grounded rewriting guidance.

## Three Modes

### AIGC Detection

Deep semantic analysis across 5 dimensions with paragraph-level reports pinpointing high-risk content.

```
Provide paper (.docx or paste text)
  -> Language detection (Chinese / English auto)
  -> 5-dimension semantic analysis
     |  Sentence Regularity   25%
     |  Connector Density     20%
     |  Voice Characteristics 15%
     |  Vocabulary Diversity  15%
     |  Argumentation Depth   25%
  -> Detection report (terminal + Markdown)
```

```
Analyze this paper for AI content: /path/to/thesis.docx
```

```
Detect the AI rate of this paper
(paste paper text)
```

### Smart Rewriting

7 proven rewrite techniques targeting mainstream detection methods. Automatically rewrites high-risk paragraphs and outputs formatted .docx.

| Technique | Target Detection | Strategy |
|-----------|-----------------|----------|
| Sentence Variation | Burstiness (GPTZero) | Merge short sentences, vary length, switch voice |
| Replace Template Transitions | Pattern Matching | Remove "Firstly/Secondly/Finally" AI patterns |
| Active Voice Priority | Syntactic Analysis | Add explicit agents to agentless sentences |
| Concrete Language | Semantic Coherence | Abstract claims -> specific data/cases |
| Counterargument Addition | Semantic Coherence | Linear argument -> multi-dimensional evidence |
| Controlled Informality | Perplexity (DetectGPT) | Unconventional but accurate expressions |
| Register Variation | Classifier (RoBERTa) | Vary formality across paragraphs |

```
Help me rewrite this paper to reduce AI rate: /path/to/thesis.docx
```

### Thesis Writing

Provide your school template, sample papers, and project code. The Skill auto-parses formatting, analyzes code architecture, generates chapters with AIGC-safe writing, and outputs a formatted .docx.

```
Prepare materials (About/ dir: template + sample + code)
  -> W0 Environment setup + template parsing
  -> W1 Material analysis (format / style / architecture)
  -> W2 Outline generation + user review
  -> W3 Chapter-by-chapter writing (AIGC-safe)
  -> W4 Formatted .docx output
  -> W5 AIGC detection + iterative optimization
```

```
Help me write my graduation thesis, template is in About/
```

## Quick Start

**1. Install**

```bash
curl -sL https://raw.githubusercontent.com/free-revalution/AIGC-Killer-Pro/main/install.sh | bash
```

The installer automatically:
- Downloads Skill files to `~/.claude/skills/aigc-detector/`
- Checks and installs `python-docx` dependency

**2. Use**

Trigger through natural conversation in Claude Code:

```
/aigc-detector
```

**3. Uninstall**

```bash
curl -sL https://raw.githubusercontent.com/free-revalution/AIGC-Killer-Pro/main/uninstall.sh | bash
```

## Multi-Agent Support

| Agent | Support | Install |
|-------|:-------:|---------|
| Claude Code | Full | `curl -sL ... \| bash` |
| Codex CLI | Partial | `curl -sL ... \| bash -s -- --agent codex` |
| Cursor | Partial | `curl -sL ... \| bash -s -- --agent cursor --dir /project` |
| Windsurf | Partial | `curl -sL ... \| bash -s -- --agent windsurf --dir /project` |
| Gemini CLI | Partial | `curl -sL ... \| bash -s -- --agent gemini --dir /project` |
| All | — | `curl -sL ... \| bash -s -- --agent all` |

- **Full**: Intent-based triggering, complete multi-step workflow, interactive choices
- **Partial**: Instructions injected as context; bash/Python/file operations work, step execution is best-effort

## Detection Principles

Built on 5 mainstream academic AIGC detection technologies:

| Technology | Platform | Skill Dimension |
|-----------|----------|----------------|
| Perplexity Detection | DetectGPT, OpenAI | Controlled Informality technique |
| Burstiness Detection | GPTZero | Sentence Regularity (25%) |
| Classifier Detection | RoBERTa-based | Register Variation technique |
| Multi-feature Fusion | Ghostbuster, UC Berkeley | 5-dimension composite score |
| Probability Curvature | — | Argumentation Depth (25%) |

Discipline-adaptive thresholds for humanities, STEM, medical, and business/economics.

## Project Structure

```
AIGC-Killer-Pro/
├── .claude/skills/aigc-detector/   # Core Skill
│   ├── SKILL.md                     # Entry point (mode routing + workflows)
│   ├── scripts/
│   │   └── docx_io.py               # Word I/O, template parsing, formatted output
│   └── references/
│       ├── detection_principles.md  # AIGC detection knowledge base
│       ├── rewrite_methods.md       # 7 rewrite techniques (CN/EN)
│       └── thesis_writing_guide.md  # Thesis writing guide
├── agents/                          # Agent entry templates
│   ├── codex.md
│   ├── cursor.mdc
│   ├── windsurf.md
│   └── gemini.md
├── install.sh                       # One-line installer
└── uninstall.sh                     # Uninstaller
```

## Advanced

**Global auto-detection** — Add the following to `~/.claude/CLAUDE.md` so Claude Code automatically detects AIGC-related intent in any project:

```markdown
## AIGC-Detector
When the user mentions paper detection, AIGC detection, AI rate reduction, or academic writing, check if the aigc-detector skill is installed.
If not, suggest: curl -sL https://raw.githubusercontent.com/free-revalution/AIGC-Killer-Pro/main/install.sh | bash
```

## Notes

- Detection results are for reference only; defer to official platform results
- Rewriting maintains academic rigor — no fabricated data or citations
- Recommended: "Human revision + tool assistance" combined strategy

## License

[MIT](LICENSE) | [Issues](https://github.com/free-revalution/AIGC-Killer-Pro/issues) and [PRs](https://github.com/free-revalution/AIGC-Killer-Pro/pulls) welcome
