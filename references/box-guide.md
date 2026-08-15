# Box 使用指南（8 种）

## keybox (红) — 核心概念
论文核心主张、关键公式（加 `\boxed{}`）、重要定义的高亮版。
每节最多 1-2 个，避免滥用。标题示例：`[HNN 的核心思想 --- "三步走" 范式]`

## derivbox (蓝) — 推导过程
完整公式推导链。内用 `align` 环境，关键步骤用 `\underbrace`/`\overbrace` 标注。
每步标注来源：`% 由 [HNN, Lemma 6] 得`

## comparebox (紫) — 跨方法对比
内嵌 `booktabs` 表格做 A vs B 对比。列标题为方法名，行为比较维度。
标题示例：`[HNN vs ILNN --- FC 层对比]`

## flowbox (青) — 流程图 + 研究路线
TikZ 流程图展示计算管道或论文发展谱系。
也用于展示与 Klein 模型研究目标的联系。

## intuitionbox (黄) — 几何/物理直觉
每个新概念必配。可含 TikZ 几何图示。
标题示例：`[为什么弯曲空间距离包含 sinh⁻¹？]`

## notebox (绿) — 补充说明
参数归属、性质列表、实现细节、辅助信息。

## warnbox (橙) — 警告与局限
数值不稳定性、常见错误、方法的技术局限。
标题示例：`[Poincaré 球的数值陷阱]`

## critiquebox (深红左竖线) — 批判性分析  ← 核心特色
每篇主要论文/方法必配一个。固定四段结构：
```latex
\begin{critiquebox}[论文 X 的批判性评价]
\textbf{✓ 优势}：...

\textbf{✗ 局限}：...

\textbf{? 未解决问题}：...

\textbf{→ Klein 模型研究机会}：...
\end{critiquebox}
```
