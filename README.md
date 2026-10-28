<div align="center">

# AIHelper

### PCB/AOI 视觉算法开发与评测工作台

多模型检测 · 浏览器标注 · 交互式可视化 · 评分与版本分析

[产品演示](#产品演示) · [主要功能](#用它可以做什么) · [业务架构](#业务架构) · [技术架构](#技术架构) · [English](README.en.md)

</div>

> 本仓库展示 AIHelper 的产品能力与设计。源码、模型与生产数据保留在私有环境中。

AIHelper 面向电路板自动光学检测（AOI）的算法开发、测试与标注，将图像输入、多模型分析、人工复核和质量报告连接在同一套工作流程中。

## 产品演示

两段动图展示不同工艺下的检测结果。点击动图可查看原尺寸。

<table>
  <thead>
    <tr>
      <th align="left" width="50%">01 · 工艺结果展示</th>
      <th align="left" width="50%">02 · 工艺结果展示</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="assets/process-example-01.gif"><img src="assets/process-example-01.gif" width="100%" alt="工艺示例 01：检测框叠加与元件结果查看"></a></td>
      <td><a href="assets/process-example-02.gif"><img src="assets/process-example-02.gif" width="100%" alt="工艺示例 02：整板检测结果与局部细节查看"></a></td>
    </tr>
    <tr>
      <td align="center"><sub>检测框叠加 · 元件结果查看</sub></td>
      <td align="center"><sub>整板结果浏览 · 局部细节查看</sub></td>
    </tr>
  </tbody>
</table>

## 用它可以做什么

### 运行检测，查看每个元件

从整板缩放到单个元件，查看检测框、类别、内部结构和识别文字。可以按需运行某个阶段或选定区域，也可以批量处理多个程序。

桌面还支持查看软件生成的检测框，并联动对照补框前后的变化。

### 在浏览器里完成标注

绘制和调整旋转框，标注元件、引脚、焊盘与文字。支持多选、复制粘贴、撤销和元件间切换，OCR 标注还可填写文字与阅读方向。

标注页通过本机服务保存标准答案，也可以打包成便携任务，交给另一台 Windows 电脑继续处理。

### 在图上找到问题

HTML 可视化页面可以叠加模型结果与人工标注，按漏检、误检、分类错误或框的位置偏差筛选，并直接定位到对应元件。

检测、分类和文字识别分别评价，帮助你判断问题出在“没找到”“分错类”，还是“框或文字不准确”。

### 用评分报告比较版本

将多个程序的评分汇总成 **HTML 驾驶舱和 Excel 报告**，查看不同版本、程序和元件类别的表现。

开发调试报告会列出需要优先关注的问题，展示位置、尺寸和角度误差分布，并提供返回单程序报告的链接，方便继续检查图像。

[了解综合评分与独立工具](docs/features.md#5-综合评分版本对比与开发诊断)

## 业务架构

![AIHelper 业务架构：图源输入、六个业务模块与成果交付](assets/business-architecture.svg)

**评测数据流：** 模型结果 + 人工标准答案 → 分阶段评分 → 程序与版本汇总。标注由人工维护，评分与汇总读取已有数据。

## 技术架构

![AIHelper 技术架构：交互入口、应用服务、计算与数据基础](assets/technology-stack.svg)

| 层次 | 技术与实现 |
| :--- | :--- |
| 桌面交互 | Python · PySide6 / Qt · Fluent Widgets |
| 浏览器工具 | HTML · JavaScript · Canvas · 本机标注服务 |
| 视觉与推理 | OpenCV · NumPy · SciPy · ONNX Runtime · TensorRT |
| 数据与报告 | SQLite · JSON · DZI / FOV · HTML 报告 · Node.js / Excel 生成 |
| 任务与验证 | 后台任务 · 子进程隔离 · 文件锁与原子保存 · Pytest |

[查看架构设计](docs/architecture.md) · [查看工程实践](docs/engineering.md)

## 扩展工具与交付

| 工具模块 | 产物与接口 |
| :--- | :--- |
| 综合评分工具组 | `综合评分.py` · 版本驾驶舱 · 开发调试指标 · Excel 工作簿 |
| 便携标注 | `.aitask` 任务包 · Windows 标注运行时 · GT 导出 |
| 数据采集 | 板级与普通图片推理接口 · JSON 结果 · 子进程客户端 |
| 样本整理 | 普通图片批处理与断点续跑 · DIP 按类别裁图 |
| 独立算法 | 区域 OCR · 连锡目标检测 / 分割 · C ABI 与 C++ / C# 接入参考 |

[完整功能清单](docs/features.md) · [项目故事](docs/project-story.md)
