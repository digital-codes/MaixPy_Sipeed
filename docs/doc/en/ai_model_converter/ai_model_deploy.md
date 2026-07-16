---
title: AI Model Download, Debugging, and Deployment Guide
---

## Choose a Model Deployment Workflow

Before deploying a local model on MaixCAM / MaixCAM-Pro / MaixCAM2, first identify the model source, target device, and deployment path. Choose the workflow that matches your current resources instead of starting with ONNX conversion immediately.

| Goal | Recommended workflow | Documentation |
| --- | --- | --- |
| Use built-in or ready-made models | Use built-in models first. For more resolutions or class sets, choose the matching device platform in [MaixHub Model Zoo](https://maixhub.com/model/zoo). MaixCAM / MaixCAM-Pro model packages usually include `.mud` and `.cvimodel` files, while MaixCAM2 model packages usually include `.mud` and `.axmodel` files. Place the files from the same package in the same directory on the device | [Model and dataset sources](../pro/datasets.md) |
| Train a custom recognition target | Use MaixHub online training to complete data collection, annotation, training, and deployment | [MaixHub online training](../vision/maixhub_train.md) |
| Deploy an ONNX model | Choose the conversion workflow based on the target device: convert to `.mud` + `.cvimodel` for MaixCAM / MaixCAM-Pro, or to `.mud` + `.axmodel` for MaixCAM2 before deployment | [MaixCAM model conversion](./maixcam.md) / [MaixCAM2 model conversion](./maixcam2.md) |

After choosing your workflow, continue with the corresponding document.
