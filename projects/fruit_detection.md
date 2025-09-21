# Real-Time Fruit Detection & Counting on Mobile Edge Devices

## Abstract

We present a turnkey pipeline for real-time multi-class fruit detection and counting on commodity smartphones. Leveraging a lightweight YOLOv8 model fine-tuned on a custom fruit dataset, we achieve 30–45 FPS on an Android Galaxy F41 via TensorFlow Lite and NNAPI/GPU delegates.

Our end-to-end system includes two-phase transfer learning, quantization, and a modular Android app with live overlay and per-class counters, enabling offline, low-latency inference without external hardware.


## Overview

Real-time fruit detection and counting using smartphone-based edge AI is crucial for numerous agricultural, retail, and nutritional applications. This report details our implementation of a compact yet powerful YOLOv8 model optimized for deployment on mobile edge devices.


## Background and Motivation

Accurate fruit detection traditionally requires dedicated hardware, limiting accessibility and increasing costs. Leveraging smartphones as edge devices provides a scalable, cost-effective, and portable solution. This motivates our exploration of lightweight deep learning models and mobile optimization techniques.


## Methodology

### Hardware Specifications

We employed the Samsung Galaxy F41 smartphone. The specifications are listed below:

| **Component** | **Specification** |
|---------------|-------------------|
| SoC           | Exynos 9611       |
| CPU           | 4×A73 @ 2.3 GHz + 4×A53 @ 1.7 GHz |
| GPU           | Mali-G72 MP3      |
| RAM           | 6 GB LPDDR4x      |
| Storage       | 128 GB UFS 2.1    |
| Display       | 6.4" 2340×1080 Super AMOLED |

### Software Tools

- Python 3.11, PyTorch, TensorFlow Lite, YOLOv8  
- Android Studio (Java/Kotlin), Android NNAPI  
- Google Colab (training), TensorFlow Lite Converter


## Data Collection

Our dataset comprised:

- **2947 images** with annotated fruit instances  
- **182 test images**

Images were collected from various viewpoints, lighting conditions, and backgrounds to ensure robustness. Annotations were generated using **LabelImg**.


## Model Development and Compression

We adopted **YOLOv8** for its efficient CSPDarknet backbone and PANet-based feature fusion.

### Training and Fine-Tuning

We employed a two-phase training strategy:

**Phase 1: Head-only Training**  
   - Backbone frozen  
   - Detection head trained for 20 epochs  
   - Learning rate: 0.01

**Phase 2: Full Fine-tuning**  
   - Entire model unfrozen  
   - Trained for 30 epochs  
   - Learning rate: 0.001

### Model Compression

- Original model size: **11.7 MB (float32)**  
- After INT8 quantization: **2.1 MB**  
- Outcome: Significant latency reduction with minimal accuracy loss


## Model Deployment

The trained model was exported to TensorFlow Lite and integrated into an Android application. Real-time inference was achieved using **CameraX** and **NNAPI** delegates.

### Inference Performance

- Achieved **30–45 FPS** on the Galaxy F41  
- Power consumption: Approximately **1 W**


##  Prototype and Demonstration

The Android application features:

- Real-time camera feed with bounding box overlays  
- Live counting of detected fruits by class  
- Fully offline operation for privacy and responsiveness

![Snapshot of the inference](fruits.png)

## Results and Performance

###  Performance Metrics

| **Class**     | **Precision** | **Recall** | **mAP@50** | **mAP@50–95** |
|---------------|---------------|------------|------------|----------------|
| Apple         | 1.000         | 1.000      | 0.995      | 0.936          |
| Banana        | 0.738         | 0.477      | 0.581      | 0.361          |
| Grapes        | 0.582         | 0.487      | 0.561      | 0.419          |
| Kiwi          | 0.762         | 0.745      | 0.760      | 0.659          |
| Mango         | 0.697         | 0.621      | 0.723      | 0.579          |
| Orange        | 0.750         | 0.757      | 0.786      | 0.706          |
| Pineapple     | 0.751         | 0.742      | 0.736      | 0.505          |
| Sugarapple    | 0.653         | 0.833      | 0.815      | 0.599          |
| Watermelon    | 0.785         | 0.698      | 0.743      | 0.564          |
| **Average**   | **0.746**     | **0.707**  | **0.744**  | **0.592**      |


##  Challenges and Workarounds

### Key Issues and Solutions

- **Limited Dataset Size**  
  ➤ Solved through data augmentation and transfer learning.

- **Accuracy Drop from Quantization**  
  ➤ Mitigated with post-quantization fine-tuning.

- **Mobile Inference Latency**  
  ➤ Resolved using NNAPI and GPU delegates for hardware acceleration.


## Novelty and Conclusion

### Main Contributions

- Real-time (30–45 FPS) fruit detection using YOLOv8 on mobile devices  
- Lightweight two-phase training and compression pipeline  
- End-to-end Android app with efficient on-device inference and live fruit counting

This work demonstrates a practical edge AI solution with applications in agriculture, retail, and nutrition. It shows how widely available smartphones can be leveraged for cost-effective, scalable AI deployments.

## References

- [TensorFlow Lite](https://www.tensorflow.org/lite)  
- [YOLOv8 Documentation](https://docs.ultralytics.com)  
- [Android NNAPI](https://developer.android.com/ndk/guides/neuralnetworks)
