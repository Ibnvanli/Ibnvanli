# Ibnvanli

独立开发者，关注工具类软件与图形性能。

## 项目

### AchiPaint

轻量绘画工具，运行于 Chromium。

- **技术栈** — 原生 ES module + Canvas 2D，无框架、无构建步骤、运行时零依赖
- **笔刷引擎** — [hokusai](https://github.com/reearth/hokusai)（libmypaint 的 Rust 移植），编译为 WebAssembly
- **文件格式** — 自研 `.achi` 容器，magic + JSON 头 + 数据块 + CRC32，三层校验
- **状态** — `v0.1.0-alpha.1`，功能可用，稳定性仍在迭代
- **协议** — MIT

[仓库](https://github.com/Ibnvanli/achipaint) · [性能规划](https://github.com/Ibnvanli/achipaint/blob/main/PERFORMANCE.md)

## 设计原则

**轻核心，边缘插件。** 核心只保留画布、笔刷、图层、颜色四项，其余能力一律以插件形式接入。核心越小，越不容易在迭代中失控。

**性能是首要指标。** 功能可以慢慢补，但输入延迟一旦超过阈值，工具就失去意义。当前以「大笔刷笔画的输入到上屏耗时」作为第一验收项。

**买断制。** 不做订阅。

## 技术方向

渲染与合成基于 Chromium（Electron），而非 WebKit —— 渲染内核的可控性优先于平台原生性。

性能路线分为四个阶段：笔刷计算迁移至 Web Worker、合成迁移至 WebGL2、笔刷 LOD 与输入预测、大画布分块。目标与验收标准写在 [PERFORMANCE.md](https://github.com/Ibnvanli/achipaint/blob/main/PERFORMANCE.md) 中。

## 其他

本地语音合成（GPT-SoVITS）相关工具与实验。

## 联系

技术讨论与问题反馈请开 [Issue](https://github.com/Ibnvanli/achipaint/issues)。
