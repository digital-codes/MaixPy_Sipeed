---
title: MaixHub 在线训练 AI 模型
update:
  - date: 2024-04-03
    author: neucrack
    version: 1.0.0
    content: 初版文档
  - date: 2026-07-10
    author: kingo0807
    version: 1.1.0
    content: 优化 MaixHub 在线训练流程、截图说明和手动部署指引
---

## 简介

[MaixHub](https://maixhub.com/) 提供在线训练 AI 模型的功能，可以在浏览器中完成数据采集、上传、标注、训练和部署，不需要本地安装训练环境，也不需要自行配置 GPU。

本文按官方示例视频的流程整理，以 **图像检测模型** 为例说明完整操作步骤。若只是想快速体验 AI 功能，可先到 [MaixHub 模型库](https://maixhub.com/model/zoo) 查找是否已有可直接使用的模型；若需要识别自定义目标，再使用在线训练功能。

![MaixHub 首页](../../assets/maixhub_home.png)

> 下方截图仅用于说明操作流程，账号、项目、数据集、图片文件名、二维码和训练任务编号等隐私信息已做模糊处理。

## 官方视频演示

MaixHub 首页提供两段官方视频。建议先观看“快速上手”，了解在线训练的整体流程；需要跟随页面逐步操作时，再观看“详细教程”。登录 [MaixHub](https://maixhub.com/) 后，在首页顶部的视频区域点击“立即观看”即可观看。

![MaixHub 官方视频演示入口](../../assets/maixhub_train_video_entries.png)

## MaixHub 训练模型流程

本节将完整流程放在同一个教程分类下，按实际操作顺序完成项目创建、数据准备、标注、训练和部署。

| 步骤 | 操作内容 |
| --- | --- |
| 创建项目 | 选择模型类型和目标硬件平台 |
| 准备数据集 | 使用设备或本地图片上传训练集、验证集 |
| 标注图片 | 检测模型需要逐张框选目标 |
| 创建训练任务 | 选择模型、图像增强和训练参数 |
| 查看训练结果 | 查看训练曲线和验证集抽样结果 |
| 部署到设备 | 下载模型包，并通过 MaixVision 手动上传到设备 |

### 创建训练项目

进入 MaixHub 首页后，选择“模型训练”，创建新的训练项目。创建项目时需要选择模型类型和硬件平台：

![MaixHub 选择训练项目类型](../../assets/maixhub_train_model_type.png)

本文后续以 **图像检测模型** 为例进行说明，适用于需要在画面中定位目标位置的场景。

项目创建完成后，按页面左侧导航依次完成数据集、标注、训练和部署。

### 准备数据集

进入项目后先创建数据集。数据类型和标注类型需与项目一致，例如检测模型应选择图像数据和检测标注。

推荐使用设备端 MaixHub 应用采集图片。设备采集的数据更接近实际部署时的镜头、分辨率和光照条件，训练后的模型更容易在设备上稳定运行。

网页端进入“采集数据”页面，选择采集到训练集或验证集，然后生成二维码：

![MaixHub 设备扫码采集](../../assets/maixhub_train_device_qrcode.png)

基本流程：

1. 确认设备已连接 WiFi。
2. 在网页端创建并选择数据集。
3. 选择采集到训练集或验证集，生成二维码。
4. 在设备端 MaixHub 应用中扫码采集并上传图片。

训练集用于学习目标特征，验证集用于评估训练效果。检测模型建议每个标签在验证集中至少保留 5 张图片，否则可能无法开始训练。验证集不要与训练集重复，并尽量使用真实场景图片。

可在数据集页面批量选择图片，并移动到训练集或验证集：

![MaixHub 整理训练集和验证集](../../assets/maixhub_train_split_validation.png)

### 标注数据

图像分类模型只需为图片选择类别。图像检测模型需要逐张框选目标，并为每个框选择标签。

进入“标注数据”页面后，创建标注、框选目标并保存：

![MaixHub 标注数据页面](../../assets/maixhub_train_annotate_page.png)

标注时注意：

* 边框尽量贴合目标主体，不要包含过多背景。
* 同一类目标使用一致的框选标准。
* 图片中出现了需要识别的目标时，不要漏标。
* 模糊、遮挡严重或无法判断类别的图片，可先不放入训练集。

数据较多时，建议先用少量图片跑通一次完整流程，再逐步增加数据优化效果。

### 创建训练任务

数据和标注检查完成后，进入“创建任务”页面。页面主要包含图像增强、选择模型和训练参数三部分：

![MaixHub 配置训练参数](../../assets/maixhub_train_parameters.png)

新手可以按下表选择，先跑通一次完整流程，再根据实际效果调整：

| 页面选项 | 新手推荐选择 | 什么时候需要调整 |
| --- | --- | --- |
| 部署平台 | 选择实际使用的设备，例如 MaixCAM 或 MaixCAM2 | 只有更换硬件平台时才修改 |
| 模型网络 | 保持页面默认推荐项 | 默认模型速度或精度不满足需求时，再尝试其它网络 |
| 图像增强 | 先保持默认设置 | 实际场景光照、角度变化较大时，再按页面选项增加增强 |
| 数据均衡 | 各类别图片数量差异较大时开启 | 每类图片数量接近时可保持关闭 |
| 负样本 | 误检背景时添加不含目标的图片 | 没有明显误检时可先不添加 |

确认模型信息和参数后，点击“创建训练任务”，输入任务名称并开始训练。

### 查看训练结果

训练开始后，可在“训练记录”中查看进度、日志、数据集统计和训练参数。训练完成后，结果页会显示损失曲线、准确率曲线和验证集抽样结果：

![MaixHub 训练完成结果](../../assets/maixhub_train_result.png)

优先检查：

* 曲线是否稳定，是否出现明显异常。
* 验证集示例是否识别正确。
* 错误结果是否集中出现在某些角度、光照或背景条件下。

如果训练失败，先查看右侧训练日志。如下示例中，失败原因是验证集中某个标签的图片数量不足 5 张，需要回到数据集补充验证图片后重新训练。

![MaixHub 验证集数量不足导致训练失败](../../assets/maixhub_train_validation_failed.png)

### 部署到 MaixCAM / MaixCAM-Pro / MaixCAM2

训练完成并确认验证效果后，进入项目的“部署模型”页面，选择需要部署的训练记录。部署方式选择“手动部署”，点击“下载模型”获取模型压缩包。

<img src="../../assets/maixhub_train_manual_deploy_page.png" alt="MaixHub 手动部署页面" style="max-width: 560px; width: 100%; height: auto;">

模型包下载完成后先解压。不同设备平台生成的模型文件后缀不同，手动部署时按实际设备选择需要上传的文件：

| 设备平台 | 需要上传的模型文件 | 说明 |
| --- | --- | --- |
| MaixCAM / MaixCAM-Pro | `model_xxx.mud` 和对应的 `.cvimodel` 文件 | `.mud` 记录模型类型、标签和 `.cvimodel` 文件名 |
| MaixCAM2 | `model_xxx.mud`、`model_xxx_npu.axmodel` 和 `model_xxx_vnpu.axmodel` | 两个 `.axmodel` 分别用于普通 NPU 和 AI-ISP 预留算力场景 |

解压目录中通常还会包含 `main.py`、`app.yaml` 和 `report.json` 等文件。`main.py` 可作为运行示例参考，`app.yaml` 可作为应用配置参考，`report.json` 可用于查看训练和导出信息。

<img src="../../assets/maixhub_train_manual_deploy_package.png" alt="MaixHub 模型压缩包内容" style="max-width: 560px; width: 100%; height: auto;">

打开 MaixVision 并连接设备，进入左侧“设备文件管理器”。在设备端进入 `/root/models` 目录，用于存放模型文件。

<img src="../../assets/maixhub_train_manual_deploy_maixvision.png" alt="MaixVision 设备文件管理器" style="max-width: 420px; width: 100%; height: auto;">

点击 MaixVision 中的上传文件按钮，从解压目录选择对应设备平台的模型文件并上传到设备的 `/root/models` 目录。MaixCAM / MaixCAM-Pro 上传 `.mud` 和 `.cvimodel`；MaixCAM2 上传 `.mud` 和对应的两个 `.axmodel`。

<img src="../../assets/maixhub_train_manual_deploy_upload.png" alt="上传 MaixHub 模型文件" style="max-width: 560px; width: 100%; height: auto;">

上传完成后，按下面步骤先跑通示例程序：

1. 在电脑端打开解压目录中的 `main.py`，检查代码里的模型路径是否指向 `/root/models/model_xxx.mud`。如果文件名不同，请改成刚上传到设备的实际 `.mud` 文件名。
2. 在 MaixVision 中打开这个 `main.py`，确认设备已连接。
3. 点击运行，将摄像头对准训练目标。如果屏幕或预览窗口中出现目标框和置信度，说明模型已经可以在设备端运行。
4. 如果没有检测框，先确认 `/root/models` 中是否已经上传 `.mud` 和对应模型文件（MaixCAM / MaixCAM-Pro 为 `.cvimodel`，MaixCAM2 为 `.axmodel`），再回到训练结果页面检查验证集效果。

需要集成到自己的项目时，将项目代码中的模型路径替换为 `/root/models/model_xxx.mud`，并参考 [YOLO 物体检测](./yolov5.md) 中的检测代码结构读取摄像头、执行检测和显示结果。完成后仍需在真实场景中复测检测框位置、置信度和误检情况。

<img src="../../assets/maixhub_train_manual_deploy_result.png" alt="MaixHub 模型设备端运行效果" style="max-width: 520px; width: 100%; height: auto;">
