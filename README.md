# Ibnvanli

在做一件有点不讨巧的事：**把绘画工具的性能抢回来**。

## AchiPaint

> 轻核心 · 边缘插件 —— 一个性能优先的轻量绘画工具

一个跑在 Chromium 里的绘画软件。纯原生 ES module + Canvas 2D，没有框架，没有构建步骤。

笔刷不自己写，直接接 [hokusai](https://github.com/reearth/hokusai)（libmypaint 的 Rust 移植）编译成的 WASM，
所以压感、倾斜、速率响应都是 libmypaint 原本的数学。

**现在状态**：`v0.1.0-alpha.1`，能用，但别拿它干正事。缺的东西不少，随机崩也时有发生。

→ [github.com/Ibnvanli/achipaint](https://github.com/Ibnvanli/achipaint)

### 为什么做这个

主流绘画软件都在往订阅制走，而且一个比一个重。
Krita 免费但卡，Clip Studio 好用但订阅，Procreate 便宜但锁在 iPad 上。

想要的是一个：**买断、轻、快、跨平台**的东西。

### 技术判断

- **押 Chromium，不押 WebKit** —— 内核攥在自己手里比什么都强，Apple 砍项目的历史太多
- **性能是唯一的护城河** —— 功能上追 Krita 要几年，性能上超过它只要几个版本
- **不做订阅** —— 目标用户就是讨厌订阅的人和嫌 Krita 太卡的人

[性能规划](https://github.com/Ibnvanli/achipaint/blob/main/PERFORMANCE.md) 里写了完整路线：
把笔刷计算挪进 Web Worker、合成换 WebGL、笔刷 LOD，
目标是 300px 笔刷单笔从 92ms 压到 16ms 以内。

## 最近在弄

- AchiPaint 的 alpha 迭代
- 本地 TTS（GPT-SoVITS）做配音

## 找我可以聊

性能优化、Web 图形、绘画工具的产品判断。开 issue 就行。
