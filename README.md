This repository provides the official implementation and pretrained models for the paper:

FFDNet: An End-to-End Lightweight Real-Time Fire Detection Model for Forest Fire Environments
(Elsevier, under review)

FFDNet is a task-oriented, lightweight, single-stage fire detection framework specifically designed for real-time forest fire monitoring under resource-constrained conditions, such as edge devices, UAV platforms, and portable monitoring terminals.

🔍 Overview

Forest fire detection in real-world environments faces multiple challenges:

🔥 Small and distant fire targets

🌲 Complex forest backgrounds

🌫️ High visual interference (sunlight, smoke, reflections)

⚙️ Limited computational resources on edge devices

To address these challenges, FFDNet adopts an end-to-end lightweight design philosophy, jointly optimizing:

Backbone → efficient multi-scale feature extraction

Neck → context-aware multi-dilated feature fusion

Detection head → stable training under small-batch and high-variance data

FFDNet is developed and evaluated on a hybrid forest fire dataset (BDF-18K) and demonstrates strong performance both on CPUs and low-cost NPU-based edge devices.

🧠 Model Architecture

FFDNet follows a three-stage single-stage detection architecture:

1. DWFireNet (Backbone)

Depthwise separable convolutions for lightweight feature extraction

Designed to preserve multi-scale fire characteristics

Significantly reduces parameters and GFLOPs compared to standard backbones

2. DWRNeck (Neck)

Multi-dilated context fusion with dilation-wise residual connections

Enhances receptive-field modeling for small and long-distance fire targets

Improves robustness in cluttered forest environments

3. FFDHead (Detection Head)

Lightweight shared convolutions

Group Normalization (GN) for stable training under small-batch settings

Improves recall and reduces false negatives in complex scenes

📌 Design principle:

Rather than pursuing extreme lightweight design, FFDNet emphasizes a balanced trade-off between detection accuracy, efficiency, and deployability.

Edge deployment (RK3588S, INT8):

🚀 92.6 FPS (NPU)

🎯 68.7% mAP50

📦 Pretrained Weights

This repository currently provides five pretrained models, all trained on the BDF-18K dataset under identical settings for fair comparison:

Model	Description
FFDNet	Proposed lightweight fire detection model
YOLO11n	Latest YOLO baseline (nano version)
YOLOv10n	End-to-end YOLOv10 nano
YOLOv8n	Widely used lightweight YOLO baseline
YOLOv5n	Early lightweight YOLO baseline

📁 Pretrained weights can be found in the weights/ directory.

🗂 Dataset

📌 Important note on data availability

The BDF-18K dataset is NOT hosted in this repository

Dataset access details are provided in the paper

Please refer to the paper for:

Dataset construction methodology

Data sources (self-collected + public datasets)

Annotation protocol

Train/validation/test splits

📖 Paper reference:

FFDNet: An End-to-End Lightweight Real-Time Fire Detection Model for Forest Fire Environments

After paper acceptance, the self-collected subset of BDF-18K will be publicly released with a DOI.

⚙️ Training & Evaluation

This codebase is built upon the Ultralytics YOLO framework and follows the experimental protocol described in the paper.

Environment

Python ≥ 3.9

PyTorch ≥ 1.13

CUDA ≥ 12.1 (optional, GPU training)

Training Configuration (Paper Default)

Input size: 640 × 640

Batch size: 8

Epochs: 400

Optimizer: SGD

Learning rate: 0.01

⚠️ For reproducible results, please follow the exact settings reported in the paper.

🧩 Edge Deployment (Optional)

FFDNet supports deployment on RK3588S-based edge devices:

FP32 training in PyTorch

Export to ONNX

INT8 post-training quantization (PTQ)

RKNN inference with NPU acceleration

Deployment details and accuracy analysis are fully described in the paper.
