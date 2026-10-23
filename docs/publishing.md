# GitHub 发布清单

## 仓库信息

建议仓库名称：`AIHelper-showcase`

当前账号已经使用 `AIHelper` 和 `AIHelper_linux` 作为源码/归档仓库，因此展示仓库单独命名可以避免访问者误入源码仓库。README 首页仍以产品名 **AIHelper** 展示。

建议 Description：

> AOI vision pipeline validation, debugging and baseline comparison workbench.

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
```

## 发布步骤

1. 在 GitHub 新建一个空的公开仓库，不勾选自动生成 README、License 或 `.gitignore`。
2. 将本目录初始化为独立 Git 仓库。
3. 添加远端并推送 `main`。
4. 在仓库 Settings → General → Social preview 上传 `assets/hero.png`。
5. 填写 Description、Website（如有）和 Topics。
6. 在个人 GitHub Profile 中将该仓库置顶。
7. 创建 `v1.0.0` Release，标题建议为 `Public Portfolio Launch`。

## 公开前检查

- 逐帧检查演示 GIF 中的路径、程序名和图像，确认允许公开。
- 确认 Git 历史中只存在本展示目录的文件。
- 确认没有模型、配置、日志、数据库、令牌或源码。
- 从全新目录 clone 一次公开仓库，检查 README 图片和链接。
- 不要将私有源码仓库设置为该公开仓库的其他分支。

## 推荐提交节奏

后续更新保持真实、清晰即可：

```text
docs: refine architecture narrative
assets: update product demo
docs: add validation case study
release: publish showcase v1.1
```

不要制造空提交、伪造日期或把私有仓库的历史合并进来。
