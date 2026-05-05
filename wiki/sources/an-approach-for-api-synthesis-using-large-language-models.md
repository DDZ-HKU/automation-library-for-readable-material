---
title: An Approach for API Synthesis Using Large Language Models
source_path: raw/sources/2502.15246v1/2502.15246v1.md
source_type: paper
author: Hua Zhong; Shan Jiang; Sarfraz Khurshid
published: 2025
processed: 2026-04-11
topics:
  - api-synthesis
  - program-synthesis
  - llm-agents
  - software-engineering
entities:
  - Hua Zhong
  - Shan Jiang
  - Sarfraz Khurshid
  - FrAngel
status: active
---

# Summary

这篇论文研究的是 API synthesis。它的核心问题不是让 LLM 使用已有工具，也不是自动生成工具库，而是让 LLM 基于输入输出示例和 API 签名，直接综合出可执行的 API 实现，并与传统 component-based API synthesis 方法比较。

## Core Claims

- 传统 component-based API synthesis 依赖巨大的搜索空间、正式规格或特定搜索策略，成本很高。
- LLM 可以作为一种新的 synthesis engine，利用训练语料中的程序知识和 prompt engineering 来减少显式搜索负担。
- 对复杂 API synthesis，LLM 不必显式枚举全部组件空间，也能基于少量输入输出示例生成正确实现。
- follow-up prompts 对修正编译或测试失败的实现有明显帮助。
- LLM 不仅能合成正确 API，还往往能给出更可读的变量名和注释。

## Key Facts

- 论文比较对象包括 FrAngel 等 component-based API synthesis 工具。
- 作者在 135 个真实任务上评估该方法，并报告 133 个任务成功。
- 该方法主要依赖：
  - assistant creation
  - chain of thought
  - few-shot learning
  - follow-up prompts
- 任务覆盖不同复杂度的 Java API synthesis 场景。
- 评价维度不仅包含正确率，还包含 compilability、test pass 和 code readability。

## Tensions / Contradictions

- 这篇工作虽然和 tool generation 有交叉，但它更偏 program synthesis / code generation，而不是 agent-style tool governance。
- 它的核心不是“让 LLM 管理一组工具”，而是“让 LLM 直接综合新的 API 实现”。
- 因此它更像 tool line 的旁支：与 tool making 有关，但问题重心更接近 synthesis methodology。

## Links Into Wiki

- [[tool-use-in-llms]] / [../concepts/tool-use-in-llms.md](../concepts/tool-use-in-llms.md)
- [[how-to-use-llm-capabilities-for-agents-and-harness-engineering]] / [../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md](../notes/frameworks/how-to-use-llm-capabilities-for-agents-and-harness-engineering.md)
