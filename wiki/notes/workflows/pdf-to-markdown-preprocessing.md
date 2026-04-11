---
title: PDF to Markdown Preprocessing
updated: 2026-04-09
status: active
---

# Summary

这个工作区已经建立了一条稳定的 PDF 预处理流程：先用本地 `marker` 工具把 PDF 转成 Markdown，再把生成结果作为原始资料放入 `raw/sources/`，之后再按 `AGENTS.md` ingest 到 `wiki/`。

## Workflow

1. 把 PDF 放进 `raw/inbox/`
2. 运行 `scripts/pdf-to-md raw/inbox/<file>.pdf`
3. 查看 `raw/sources/<file>/` 下生成的 Markdown、元数据和提取图片
4. 再把该 Markdown 作为新资料 ingest 到 `wiki/`

## Current Setup

- 转换工具仓库位于 `marker/`
- 隔离环境位于 `marker/.venv/`
- 统一入口命令是 `scripts/pdf-to-md`
- 默认输入目录是 `raw/inbox/`
- 默认输出目录是 `raw/sources/`

## Operational Notes

- 第一次运行 `marker` 时会下载并缓存模型，因此会明显更慢。
- 模型缓存完成后，后续 PDF 转换会快很多。
- 输出通常包括：
  - `<name>.md`
  - `<name>_meta.json`
  - 从 PDF 中提取的图片文件
- 该流程不改写原始 PDF，只是新增 Markdown 产物。

## Verified Example

- 输入文件：`raw/inbox/1511.06391v4.pdf`
- 输出目录：`raw/sources/1511.06391v4/`
- 已验证生成：
  - `raw/sources/1511.06391v4/1511.06391v4.md`
  - `raw/sources/1511.06391v4/1511.06391v4_meta.json`

## Links

- [[order-matters-sequence-to-sequence-for-sets]] / [../../sources/order-matters-sequence-to-sequence-for-sets.md](../../sources/order-matters-sequence-to-sequence-for-sets.md)
- [[the-annotated-transformer]] / [../../sources/the-annotated-transformer.md](../../sources/the-annotated-transformer.md)
