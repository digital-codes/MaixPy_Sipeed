---
title: AI 模型下载、调试和部署指南
---

## 选择模型部署方式

首次进行 MaixCAM / MaixCAM-Pro / MaixCAM2 本地模型部署时，建议先明确模型来源、目标设备和部署方式。请根据当前已有资源选择对应流程，避免一开始就直接进行 ONNX 转换。

| 使用目标 | 建议流程 | 查看文档 |
| --- | --- | --- |
| 使用预置或现成模型 | 优先使用系统预置模型；如需更多分辨率或类别，可在 [MaixHub 模型库](https://maixhub.com/model/zoo) 选择对应设备平台。MaixCAM / MaixCAM-Pro 模型包通常包含 `.mud` 与 `.cvimodel`，MaixCAM2 模型包通常包含 `.mud` 与 `.axmodel`，部署时放入设备同一目录 | [模型与数据集来源](../pro/datasets.md) |
| 训练自定义识别目标 | 使用 MaixHub 在线训练完成数据采集、标注、训练与部署 | [MaixHub 在线训练](../vision/maixhub_train.md) |
| 部署 ONNX 模型 | 根据目标设备选择转换流程：MaixCAM / MaixCAM-Pro 转换为 `.mud` + `.cvimodel`，MaixCAM2 转换为 `.mud` + `.axmodel` 后再部署 | [MaixCAM 模型转换](./maixcam.md) / [MaixCAM2 模型转换](./maixcam2.md) |

选定流程后，进入对应文档继续操作即可。
