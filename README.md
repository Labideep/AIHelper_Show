<div align="center">

<img src="assets/hero.png" width="100%" alt="AIHelper — AOI vision workflow validation platform">

# AIHelper

### AOI 视觉流水线验证与调试工作台

从图源输入到检测、分类、方向校正、子结构分析与 OCR，  
用一条可追溯的流水线统一桌面调试、批量执行和基线验证。

<p>
  <img alt="Python" src="https://img.shields.io/badge/Python-3.11%20%7C%203.12-3776AB?logo=python&logoColor=white">
  <img alt="Computer Vision" src="https://img.shields.io/badge/Computer%20Vision-AOI-00A6A6">
  <img alt="Inference" src="https://img.shields.io/badge/Inference-ONNX%20%7C%20TensorRT-76B900">
  <img alt="Source" src="https://img.shields.io/badge/Source-Private-7C3AED">
</p>

[产品演示](#产品演示) · [系统设计](docs/architecture.md) · [工程实践](docs/engineering.md) · [English](README.en.md)

</div>

> [!IMPORTANT]
> 这是 AIHelper 的公开项目展示仓库。业务源码、模型权重、生产数据和内部配置均保留在私有仓库中；这里仅展示经过整理的产品能力、架构思路与工程实践。

## 项目概览

AIHelper 面向 PCB/AOI 视觉算法的开发与验证场景，将原本分散的图像输入、模型推理、结果回映射、人工复核和基线对比整理为一致的工程流程。它既能帮助算法工程师快速定位“差异从哪一阶段开始”，也能为批量回归提供稳定、可审计的执行入口。

| 维度 | 能力 |
| :--- | :--- |
| 核心流程 | Input → SMT → CLS → DIR → IC → OCR |
| 使用方式 | 桌面 GUI、批量任务、独立推理入口 |
| 结果追踪 | 阶段事件、结构化结果、可视化报告、运行身份 |
| 质量保障 | 基线只读、差异即失败、报告保留、输入与配置可追溯 |
| 工程重点 | 统一流水线、坐标一致性、线程安全、GPU 生命周期管理 |

## 产品演示

### 单程序完整推理

从程序图源进入多阶段推理，并在同一界面查看阶段状态、检测结果与耗时。

<div align="center">
  <img src="assets/smt-workflow.gif" width="92%" alt="AIHelper single-program workflow demo">
</div>

### 多程序批量验证

统一执行多程序任务，持续反馈进度，并保留每次运行的独立结果与差异报告。

<div align="center">
  <img src="assets/multi-program.gif" width="92%" alt="AIHelper multi-program batch demo">
</div>

## 核心能力

| 统一推理工作流 | 可解释的阶段结果 |
| :--- | :--- |
| GUI 与批处理共享同一套请求和执行契约，避免入口之间逐渐产生行为差异。 | 每个阶段保留输入来源、模型角色、坐标变换和结果关联，便于定位第一处差异。 |
| **可靠的基线验证** | **复杂图源与几何处理** |
| 标准答案保持只读；任何差异都会失败并生成报告，不用自动更新掩盖回归。 | 支持大图切块、DZI、旋转框、透视裁切、非等比缩放和板级坐标恢复。 |
| **桌面交互与后台任务解耦** | **面向生产的推理资源管理** |
| 后台任务只发布事件，界面更新回到主线程，降低卡顿和线程不安全风险。 | 对模型准备、会话池、并发和 GPU 重资源阶段建立明确生命周期。 |

## 系统架构

<div align="center">
  <img src="assets/architecture.svg" width="96%" alt="AIHelper public architecture overview">
</div>

系统以统一应用流水线连接多种入口，业务模块只关注阶段能力；图源、配置、状态与输出由基础设施层提供稳定边界。更多说明见[公开架构设计](docs/architecture.md)。

## 推理流水线

<div align="center">
  <img src="assets/pipeline.svg" width="100%" alt="AIHelper inference pipeline">
</div>

基线流程按照固定顺序执行。DIR 校正分类后的生产父框，随后 IC 与 OCR 复用经过确认的几何和父子关系；最终结果统一回到板级坐标空间。

## 工程亮点

- **单一执行契约**：不同入口构造相同类型的请求，由同一服务编排阶段顺序、事件和失败行为。
- **坐标与证据优先**：旋转框、精确四点、父子关联和图源比例贯穿流水线，减少“结果看似接近但来源不同”的问题。
- **并发边界清晰**：推理工作在后台执行，界面线程只消费事件；状态写入使用并发安全机制。
- **回归结果可信**：基线不自动修改，差异必定产生失败报告；调试产物与业务输出明确分离。
- **兼容性受控**：公开入口、输出目录和兼容层都有清晰边界，新增能力不依赖历史私有实现。

更完整的设计取舍和问题拆解见[工程实践](docs/engineering.md)与[项目故事](docs/project-story.md)。

## 技术栈

```text
Application     Python · Desktop GUI · Batch CLI
Vision          OpenCV · ONNX Runtime · TensorRT
Pipeline        Event-driven orchestration · Typed requests
Validation      Pytest · Golden baseline · Structured reports
Data            DZI · SQLite · JSON · Image tiles
```

## 仓库说明

本仓库用于作品展示，因此有意不包含：

- 业务源码与私有 Git 历史
- 模型文件、标签字典和运行时配置
- 客户程序、生产图片和真实检测结果
- 内部服务地址、访问凭据与部署脚本

如需深入了解，可在面试或技术交流中进行实时产品演示和私有代码走读。

---

<div align="center">
  <sub>Designed as an engineering portfolio · Source code remains private</sub>
</div>
