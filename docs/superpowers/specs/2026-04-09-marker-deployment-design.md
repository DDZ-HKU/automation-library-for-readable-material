# Marker Deployment Design

摘要：本设计定义一个最小可用的本地 PDF 转 Markdown 预处理流程，在知识库主工作流之外部署 `marker`，把 `raw/inbox/` 中的 PDF 转成 `raw/sources/` 中的 Markdown，供后续 ingest 到 `wiki/`。

## Goal

建立一个稳定、低摩擦的本地转换流程：

- 原始 PDF 保留在 `raw/inbox/`
- 通过本地 `marker` CLI 转换为 Markdown
- 转换结果写入 `raw/sources/`
- 后续知识整理仍按现有 `AGENTS.md` 规则执行

本阶段只做部署与可用性打通，不改造 `wiki/` ingest 流程。

## Scope

### In Scope

- 在 `marker/` 下配置独立 Python 运行环境
- 安装并验证 `marker` CLI 可用
- 在主仓库中提供一个统一入口触发单文件 PDF 转 Markdown
- 固定输入输出目录约定
- 以一个真实 PDF 完成端到端验证

### Out of Scope

- 自动目录监听
- 后台常驻进程
- `--use_llm` 增强模式
- 多文档批处理编排
- 对 `wiki/` ingest 逻辑做自动联动

## Constraints

- 不改写已有 `raw/` 原始资料
- PDF 原件必须保留
- Markdown 作为新增原始资料写入 `raw/`
- 尽量不把 `marker` 的依赖污染到知识库主环境
- 主目录 `/Users/ddz/Documents/exp` 当前不是 git 仓库，因此设计文档只能写入文件系统，不能在该目录提交 commit

## Current Context

- 知识库目录已存在 `raw/inbox/` 与 `raw/sources/`
- PDF 转换项目位于 `marker/`
- `marker` 是独立 Python 项目，提供 `marker_single` 与 `marker` CLI
- 用户目标是先完成部署，再把 PDF 预处理纳入日常使用流程

## Recommended Approach

采用“独立部署 + 轻量包装入口”的方案。

### Why This Approach

- 比直接手敲 `marker_single` 更稳定，减少记忆成本
- 比自动监听目录简单，故障面小
- 与现有知识库结构兼容，不引入额外基础设施
- 后续如需扩展为批处理或自动化，可在同一路径上增量演进

## Architecture

系统分为两层：

1. `marker/` 工具层
   - 负责 Python 环境、依赖与实际 PDF 转换
   - 独立于知识库主目录运行

2. 主仓库包装层
   - 提供统一命令入口
   - 负责输入文件校验、输出路径规范化、调用 `marker_single`

## Data Flow

1. 用户把 PDF 放入 `raw/inbox/`
2. 用户运行统一转换命令，传入该 PDF 路径
3. 包装入口调用 `marker` CLI
4. 生成的 Markdown 输出到 `raw/sources/`
5. 原 PDF 保持不变
6. 后续由知识库 ingest 流程读取 `raw/` 中的新 Markdown 并更新 `wiki/`

## Command Design

统一入口应满足以下行为：

- 接收单个 PDF 文件路径
- 默认输出到 `raw/sources/`
- 在运行前检查 `marker` 虚拟环境与 CLI 可用性
- 对失败给出明确报错
- 成功后打印输出文件路径，方便后续 ingest

第一阶段不追求高度抽象，优先做一个简单、透明、可调试的本地命令。

## Error Handling

需要明确处理以下失败场景：

- 输入路径不存在
- 输入文件不是 PDF
- `marker` 环境尚未安装
- 首次运行需要下载模型或依赖失败
- 转换过程异常退出但未产生输出文件

处理原则：

- 直接失败
- 报错信息尽量指向下一步操作
- 不自动清理用户原始 PDF

## Verification Plan

完成实施后至少验证以下两项：

1. 工具验证
   - `marker_single --help` 能运行

2. 端到端验证
   - 选择一个真实 PDF
   - 成功生成 Markdown
   - 输出文件位于 `raw/sources/`
   - 结果可供后续知识库 ingest 使用

## Future Extensions

后续可以在本设计基础上增量加入：

- 目录批处理
- 自动监听 `raw/inbox/`
- OCR 或 `--use_llm` 高质量模式
- 产物命名与元数据规范
- 转换后自动触发知识库 ingest

## Acceptance Criteria

- `marker` 在本机可运行
- 有一个固定、可复用的 PDF 转 Markdown 命令入口
- 至少一个真实 PDF 转换成功
- 生成 Markdown 进入 `raw/` 而非 `wiki/`
- 不改动已有原始资料内容
