# 引用规范

## 行内简写（正文中使用）
紧跟公式或结论，方括号格式：
- `[HNN, Thm.5]` — 论文简称 + 定理/引理编号
- `[ILNN, §3.2, Eq.7]` — 论文简称 + 章节 + 公式编号
- `[ECCV Tutorial, Part 2, 32:15]` — 教程名 + 部分 + 时间戳
- `[WWW Tutorial, Slide 14]` — 教程名 + 幻灯片编号

## 正式 BibTeX 引用
首次提及论文全名时用 `\textcite{key}`（"Ganea et al. (2018)"），后续用 `\cite{key}`。
文末统一 `\printbibliography`。

## .bib 条目命名
格式：`{第一作者姓氏小写}{年份}{关键词}`
- `ganea2018hnn` — Ganea et al., HNN
- `chen2024ilnn` — ILNN 论文
- `eccv2022tutorial` — ECCV 教程

## 来源类型
| 类型 | BibTeX entry type | 必填字段 |
|------|-------------------|----------|
| 会议论文 | `@inproceedings` | author, title, booktitle, year |
| 期刊论文 | `@article` | author, title, journal, year, volume |
| 预印本 | `@misc` | author, title, year, eprint (arXiv ID), archiveprefix |
| 教程/视频 | `@misc` | author, title, year, howpublished (URL), note |
