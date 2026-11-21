# Ibnvanli

在做 AchiPaint —— 一个轻核心 + 边缘插件架构的绘画工具。

## 项目

### AchiPaint

轻量绘画工具，运行于 Chromium。

- **技术栈** — 原生 ES module + Canvas 2D，无框架、无构建步骤、运行时无 `node_modules` 依赖
- **笔刷引擎** — [hokusai](https://github.com/reearth/hokusai)（libmypaint 的 Rust 移植），编译为 WebAssembly
- **文件格式** — 自研 `.achi` v2 容器：按 256×256 瓦片存储，只写有笔迹的块，含 CRC32 三层校验
- **测试** — 66 项，跑在真实 Chromium 里，断言合成层像素与 DOM 行为
- **状态** — `v0.1.0-alpha.1`，核心绘画能力已完整，稳定性仍在迭代
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

**[dsh-gsv-bridge](https://github.com/Ibnvanli/dsh-gsv-bridge)** — DeepSeek Harness 与本机 GPT-SoVITS 之间的桥接插件。
自动识别 `api.py` / `api_v2.py` 两套 API 方言，把合成结果落盘并接回界面朗读。MIT。

## 联系

技术讨论与问题反馈请开 [Issue](https://github.com/Ibnvanli/achipaint/issues)。
