---
title: MaixCAM MaixP Where to Find Models and Datasets
---

---

## Where to Find Ready-to-Use Models for MaixPy MaixCAM

Visit the [MaixHub Model Library](https://maixhub.com/model/zoo) and filter by the corresponding hardware platform to find suitable models.

If you only want to verify that the workflow works, start with a built-in model. The system usually includes common models in `/root/models`, so you can reference the corresponding `.mud` file directly in your code without downloading anything.

For more models, open [MaixHub Model Zoo](https://maixhub.com/model/zoo?platform=maixcam2), filter by the MaixCAM2 platform, and download a model package. After downloading, check whether it contains:

- `.mud`: the model description file. MaixPy code usually loads this file.
- `.axmodel`: the actual model file that runs on MaixCAM2.
- Example code or instructions: if the model page provides an example, run that first.

## What Are Datasets Used For?

First, check the [MaixHub Model Library](https://maixhub.com/model/zoo) to see if there’s a model you need. If not, you can train your own model. Training a model requires a dataset, which provides the data needed for training.

## Converting Existing Models for Use with MaixCAM MaixPy

MaixPy natively supports several model frameworks, such as YOLOv8/YOLO11/Mobilenet, etc. Models trained with these frameworks can be exported to ONNX format and then converted to a format supported by MaixCAM for use with MaixPy MaixCAM.

If you don’t want to train your own models, you can find open-source pre-trained models online. For instance, YOLO11/YOLOv8/YOLOv5 have many shared models. For example, from [this link](https://github.com/Eric-Canas/qrdet/releases), you can download YOLOv8 models for QR code detection (`qrdet-*.pt`). Simply export the model to ONNX format and convert it to [MaixCAM’s supported format](https://maixhub.com/model/zoo/480).

Refer to the [MaixCAM Model Conversion Documentation](../ai_model_converter/maixcam.md) for details on the conversion process.

## Where to Find Datasets?

1. **Method 1: Check Official Documentation for Algorithms**  
   For example, for YOLO11/YOLOv8, the [YOLO Official Documentation - Datasets](https://docs.ultralytics.com/datasets/) provides a variety of open-source datasets. You can use a single command to train models following the documentation. Afterward, export the model to ONNX format and convert it for MaixCAM.  

2. **Method 2: Visit Dataset Websites**  
   Platforms like [Kaggle](https://www.kaggle.com/datasets/riondsilva21/hand-keypoint-dataset-26k) or [Roboflow](https://universe.roboflow.com/) host numerous datasets for different applications.

3. **Method 3: Use Open-Source Datasets and Prepare Training Scripts**  
   Search for open-source datasets and format them into scripts compatible with training frameworks like YOLO.

