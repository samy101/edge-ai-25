---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

# Real-Time Vehicle Monitoring and Number Plate Recognition System on Edge Devices

## Introduction and Objectives

### Project Overview

This project is focused on designing and deploying a comprehensive **real-time vehicle monitoring and number plate recognition system** using **edge computing**. The entire pipeline is optimized for hardware with limited resources using **four lightweight deep learning models** trained with **YOLOv8** and **PaddleOCR**. These models are deployed on an edge device (e.g., **NVIDIA Jetson Orin Nano**), making the system suitable for **smart gates, parking management, and surveillance**.

### Key Objectives

- Develop an end-to-end pipeline for real-time vehicle monitoring and license plate recognition.
- Use YOLOv8 and PaddleOCR models to maintain **high accuracy with small model sizes** (~200MB combined).
- Ensure **low-latency, real-time performance** on embedded edge devices.
- Record and store inference results **locally** in CSV or SQLite format.
- Design the system to be **modular and scalable** for deployment in toll gates, checkpoints, etc.

---

## System Architecture and Inference Pipeline

### Pipeline Components

| **Task**                  | **Model**   | **Format** | **Size**    |
|---------------------------|-------------|------------|-------------|
| Vehicle Detection         | YOLOv8      | `.pt`      | 21.4 MB     |
| Vehicle Type Classification | YOLOv8   | `.pt`      | 9.79 MB     |
| Number Plate Detection    | YOLOv8      | `.pt`      | 21.4 MB     |
| Character Recognition     | PaddleOCR   | `.pt`      | 96.5 MB     |

### Inference Pipeline Workflow

1. **Frame Capture**: Real-time video stream from webcam or CCTV.
2. **Vehicle Detection**: Detect vehicles using YOLOv8 object detector.
3. **Vehicle Type Classification**: Classify each detected vehicle (e.g., car, truck, bike).
4. **Number Plate Detection**: Detect plate region from cropped vehicle area.
5. **Character Recognition**: Use PaddleOCR to recognize text from number plate.
6. **Record Results**: Save timestamp, vehicle type, and plate number into a local CSV or database.

### Sample Data Output Format

| **Timestamp**           | **Vehicle Type** | **Plate Number** |
|--------------------------|------------------|------------------|
| 2025-04-30 10:25:43     | Truck            | KA01AB1234       |
| 2025-04-30 10:25:45     | Bike             | MH12XY9876       |

---

## Edge Device Deployment

### Device Selection for Deployment

**Primary Recommendation: NVIDIA Jetson Orin Nano**

- Supports **GPU acceleration** for PyTorch models.
- Compact and efficient for **real-time edge AI inference**.
- Easily handles **4 models** totaling ~200MB in memory.

---

## Implementation, Performance, and Future Scope

### Deployment and Performance

- Models exported in **PyTorch `.pt`** format.
- Inference run using **Ultralytics Python package**.
- Optimized preprocessing and post-processing for **batch size = 1**.
- Local result storage using **CSV** (extendable to SQLite/JSON).

### System Performance Metrics

| **Metric**                    | **Value**    |
|-------------------------------|--------------|
| Inference Speed               | ~5 FPS       |
| Avg Latency per Frame         | ~200 ms      |
| Vehicle Detection Accuracy    | > 90%        |
| Vehicle Classification        | ~88%         |
| Plate Detection Accuracy      | > 92%        |
| OCR Accuracy                  | ~85–90%      |

---

### Future Improvements

- Add **blacklisted vehicle alert** system with local alarms.
- **Quantize models** for faster inference and reduced size.
- Build a **simple GUI dashboard** for visual feedback.
- Enable **batch inference** using stream queue architecture.

---

## Conclusion

This project demonstrates a **robust**, **real-time**, and **modular edge AI system** for vehicle monitoring without relying on cloud infrastructure. It is optimized for **cost-effective deployment**, **local data storage**, and achieves **high accuracy** across all subtasks.

---

## 🔗 GitHub Repository

[https://github.com/prabhat51/vehicle-monitoring-system](https://github.com/prabhat51/vehicle-monitoring-system)
