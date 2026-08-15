---
name: research-note
description: >
  生成中文深度研究笔记、LaTeX/PDF、StudyHub 论文卡片和研究日志。适用于论文精读、
  多篇论文综合、专题笔记、暑研阅读、研究问题沉淀。默认面向 Codex + Windows +
  Obsidian StudyHub 工作流；长论文不能压缩成短摘要，必须产出教学型、可复用的深度笔记。
---

# Research Note — Codex/Windows + StudyHub 深度研究笔记

## 0. Core Goal

输出不是论文摘要，而是**可复用的研究材料**：

1. 中文深度 LaTeX/PDF 研究笔记。
2. StudyHub Markdown 论文卡片与研究状态更新。
3. 对用户当前研究主线的具体连接和后续问题清单。

默认风格参考深度专题笔记：先补基础概念，再进入方法、理论、实验、对比、批判和研究启发。长论文或多论文任务不得压缩到 5-6 页，除非用户明确要求 brief。

## 1. Trigger And Mode

- `Day N`: 按学习计划生成当天研究日志。
- `专题 <主题>`: 从基础到前沿的专题型笔记。
- `papers <pdf...>` 或用户给出论文 PDF: 多篇论文精读/综合。
- 用户提到 Obsidian、StudyHub、研究主线、暑研、与我研究的关联时：必须使用 StudyHub 记忆层。

如果用户没有指定模式：

- 单篇论文: 默认 `专题/论文精读`。
- 多篇相关论文: 默认 `多论文综合专题`。
- 论文总页数 > 40 或任一论文 > 20 页: 默认 `深度模式`。

## 2. Mandatory StudyHub Memory Layer

先解析 `STUDYHUB_ROOT`，不要假设所有用户使用同一个绝对路径。按以下优先级：

1. 用户在当前请求中明确提供的 vault 路径。
2. skill 根目录旁的可选 `local-config.yaml` 中的 `studyhub_root`。
3. 环境变量 `STUDYHUB_ROOT`。
4. 仍无法解析时，先向用户询问 vault 路径，再进行任何 StudyHub 写入。

`local-config.yaml` 是仅限本机的配置，不得提交到公共仓库。格式参考 `local-config.example.yaml`。

涉及用户研究方向、暑研、paper reading、“与我的研究关联”、后续计划时，先读：

1. `{STUDYHUB_ROOT}\Home\Codex Runtime Memory.md`
2. `{STUDYHUB_ROOT}\Research\Sustech research\Sustech research.md`
3. 若存在，再读：
   - `{STUDYHUB_ROOT}\Research\Sustech research\Current Research State.md`
   - `{STUDYHUB_ROOT}\Research\Sustech research\Paper Reading Index.md`
   - `{STUDYHUB_ROOT}\Research\Sustech research\Research Questions.md`
   - `{STUDYHUB_ROOT}\Research\Sustech research\Open Problems.md`
   - `{STUDYHUB_ROOT}\Research\Bandits\Bandits.md`

不要把“与我的研究的关联”写成泛泛而谈。必须连接用户当前主线：

- statistics / bandits / offline evaluation
- LLM exploration-exploitation
- in-context RL
- LLM agents as decision-making systems
- SUSTech summer research with Prof. Fang Kong

## 3. Output Contract

每次深度研究任务默认输出：

1. `deep_research_note.tex`
2. `deep_research_note.pdf`
3. `references.bib`
4. StudyHub paper card(s), Markdown:
   - `{STUDYHUB_ROOT}\Research\Sustech research\Paper Notes\<short-title>.md`
5. StudyHub updates where relevant:
   - `Paper Reading Index.md`
   - `Research Questions.md`
   - `Open Problems.md`
   - `Weekly Research Log.md`

如果时间或环境不允许全部完成，优先级为：

PDF note > references.bib > paper cards > index/log updates.

### 3.1 Workspace Layout Contract

当用户给出项目目录或工作目录时，必须保持根目录干净。

项目根目录只允许出现：

1. 用户明确提供的原始源文件，例如论文 PDF。
2. 一个最终成品文件夹，例如 `final_deliverables`。
3. 一个中间文件夹，例如 `intermediate_files`。

项目根目录禁止出现：

- 抽取出的 `.txt` 文本。
- 仅用于参考的样例 PDF 副本。
- 页面渲染 PNG。
- LaTeX 源码、`.aux`、`.bbl`、`.bcf`、`.log`、`.out`、`.toc`、`.run.xml`。
- BibTeX 文件。
- 临时脚本。
- 旧版本输出文件夹。

所有非最终 research-note 产物必须进入中间文件夹，例如：

```text
intermediate_files/
  sources_text/
  reference_samples/
  research_note/
  render_checks/
```

最终成品文件夹只放用户会直接打开或提交的文件。若与 slide skill 同时使用，两个 skill 必须共用同一个中间文件夹和同一个最终成品文件夹。

## 4. Depth Requirements

### Brief Mode

仅在用户明确要求“简短/brief/快速总结”时使用。

- 3-6 页 PDF。
- 适合快速扫读。

### Standard Mode

- 单篇短论文或普通阅读: 8-12 页 PDF。
- 至少覆盖 problem, method, theory/algorithm, experiments, critique, research connection.

### Deep Mode

触发条件：任一论文 > 20 页，或多篇论文总页数 > 40，或用户要做 presentation / 暑研材料。

- 目标 12-25 页 PDF。
- 多篇论文时，每篇论文至少 4-6 页实质内容。
- 必须逐节覆盖：
  1. 背景与前置概念
  2. 论文问题设定
  3. 方法机制
  4. 关键公式/算法/理论
  5. 实验设计与结果
  6. 与相关方法对比
  7. 批判性分析
  8. 与用户研究主线的连接
  9. 可执行后续问题

禁止把 40+ 页材料压缩成只含摘要、优缺点和几条启发的短文。

## 5. Recommended Structure

### Single-Paper Deep Topic

```latex
\part{I} 基础概念
1. 问题背景
2. 关键前置知识

\part{II} 方法详解
3. 核心设计
4. 算法/模型/训练目标
5. 部署或推断流程

\part{III} 理论与实验
6. 理论结果或机制解释
7. 实验设置
8. 关键结果与现象

\part{IV} 深入理解与对比
9. 与相关方法对比
10. 失败模式与边界条件

\part{V} 批判性分析与研究展望
11. 批判性评价
12. 与我的研究的关联
13. 后续问题与计划
14. 自检清单
\printbibliography
```

### Multi-Paper Synthesis

```latex
\part{I} 背景与统一问题
\part{II} Paper A 精读
\part{III} Paper B 精读
\part{IV} 横向综合：共同问题、关键差异、互补关系
\part{V} 对用户研究主线的启发
\part{VI} 批判性分析、后续实验、开放问题
\printbibliography
```

## 6. Content Rules

- 全部中文撰写，术语可保留英文括注。
- 数学公式必须用 LaTeX。
- 每个新概念配一个直觉解释，优先使用 `intuitionbox`。
- 关键公式需要说明每个符号的含义。
- 关键理论不要只抄 theorem，要解释假设、结论、直觉和局限。
- 实验部分必须写清：数据/环境、baseline、metric、主要发现、作者想证明什么。
- 跨方法对比必须用 `comparebox` + `booktabs` 表格。
- 批判性分析必须四段式：
  - 优势
  - 局限
  - 未解决问题
  - 研究机会
- 与我研究的关联必须给出具体可执行连接，不写空泛“有启发”。

## 7. StudyHub Markdown Rules

StudyHub 笔记使用 Obsidian-renderable Markdown。

- inline math: `$...$`
- display math: `$$...$$`
- 不使用 `\(...\)` 或 `\[...\]`。

Paper card 模板：

```markdown
---
type: paper-note
status: read
topic: <topic>
created: <date>
source: <pdf/arxiv>
---

# <Paper Title>

## One-Sentence Contribution

## Problem Setting

## Method

## Theory / Algorithm

## Experiments

## Limitations

## Connection to My SUSTech Line

## Possible Research Questions

## Terms To Remember
```

## 8. Windows/Codex Compilation Protocol

Use `xelatex` and `biber`. For Chinese filenames, avoid biber encoding problems by compiling with an ASCII job name:

```powershell
xelatex -jobname=deep_note -interaction=nonstopmode "<中文文件名>.tex"
biber deep_note
xelatex -jobname=deep_note -interaction=nonstopmode "<中文文件名>.tex"
xelatex -jobname=deep_note -interaction=nonstopmode "<中文文件名>.tex"
```

After compilation:

1. Run `pdfinfo` and confirm page count.
2. Render first 3 pages and last page with `pdftoppm`.
3. Check logs for:
   - undefined citations
   - empty bibliography
   - fatal errors
   - severe overfull boxes

Warnings about minor `fancyhdr` headheight or small underfull boxes are acceptable if the PDF renders cleanly.

### Known Windows/LaTeX pitfalls

- Avoid math, commas, square brackets, or unmatched punctuation inside optional `tcolorbox` titles such as `\begin{comparebox}[...]`. Titles like `[$(k,v)$ 设计轴]` can be parsed as pgfkeys options and break compilation. Use plain titles such as `[k-v 设计轴]`.
- Compile Chinese `.tex` files with an ASCII `-jobname`; otherwise `biber` may look for mojibake `.bcf` filenames.
- If Poppler prints a non-fatal warning such as `Syntax Error: Weird page contents` but renders PNG pages successfully, treat it as a warning and inspect the images.
- Tables with long English identifiers (`ScienceWorld`, `REINFORCE+LoRA`, `Neural-LinLogUCB`) often cause underfull boxes. Prefer `tabularx`, shorter labels, or split into multiple tables.
- Do not deliver if the log contains `! LaTeX Error`, `! Package ... Error`, `undefined references`, or `Empty bibliography` after the final run.

## 9. Box Usage

Use these tcolorbox environments when available in the template:

| Box | Purpose |
|---|---|
| `keybox` | 核心公式/论文主张 |
| `intuitionbox` | 新概念直觉 |
| `derivbox` | 推导过程 |
| `comparebox` | 方法对比表 |
| `flowbox` | 流程图/研究路线 |
| `warnbox` | 局限、陷阱、假设 |
| `critiquebox` | 批判性分析 |
| `notebox` | 补充说明 |

## 10. Final Response

报告：

- PDF 路径与页数。
- `.tex` 与 `references.bib` 路径。
- StudyHub 更新了哪些文件。
- 编译/渲染验证结果。
- 如果因环境限制跳过了某项，明确说明。
