# GitHub 发布清单

## 仓库信息

建议仓库名称：`AIHelper-showcase`

当前账号已经使用 `AIHelper` 和 `AIHelper_linux` 作为源码/归档仓库，因此展示仓库单独命名可以避免访问者误入源码仓库。README 首页仍以产品名 **AIHelper** 展示。

建议 Description：

> PCB/AOI vision workbench for inference debugging, browser annotation, interactive visualization, quality scoring and version comparison.

建议 Topics：

```text
aoi
computer-vision
machine-learning
onnx-runtime
tensorrt
desktop-application
inference-pipeline
model-validation
image-annotation
data-visualization
model-evaluation
benchmarking
```

## 发布步骤

1. 在 GitHub 新建一个空的公开仓库，不勾选自动生成 README、License 或 `.gitignore`。
2. 将本目录初始化为独立 Git 仓库。
3. 添加远端并推送 `main`。
4. 在仓库 Settings → General → Social preview 上传 `assets/social-preview.jpg`（1280 × 640，低于 1 MB）。
5. 填写 Description、Website（如有）和 Topics。
6. 在个人 GitHub Profile 中将该仓库置顶。
7. 为最新版本标签创建 GitHub Release，并用简短要点说明本次展示更新。

## 公开前检查

- 逐帧检查演示 GIF 中的路径、程序名和图像，确认允许公开。
- 确认 Git 历史中只存在本展示目录的文件。
- 确认没有模型、配置、日志、数据库、令牌或源码。
- 从全新目录 clone 一次公开仓库，检查 README 图片和链接。
- 不要将私有源码仓库设置为该公开仓库的其他分支。

## 展示内容维护

- 中英文首页同步维护推理、标注、可视化、评分、版本分析和数据交付六个方向。
- 功能细节与独立脚本统一登记在 `docs/features.md`，明确主程序、脚本工具和接入参考的边界。
- 当前 GIF 只演示桌面推理与批处理；新增标注或评分演示应使用允许公开的数据，不将功能关系图标成实际截图。
- 汇总报告链接到源报告时需要保留关联资源；公开展示前另外检查其路径与数据内容。
- 测试数量与性能数据保留采集日期和范围，不将历史数据写成当前设备验收结论。

## 推荐提交节奏

后续更新保持真实、清晰即可：

```text
docs: refine architecture narrative
assets: update product demo
docs: add validation case study
release: publish showcase v1.1
```

不要制造空提交、伪造日期或把私有仓库的历史合并进来。
