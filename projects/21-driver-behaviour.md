---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

# Driver Drowsiness and Distraction Detection System

## Overview

The Driver Drowsiness and Distraction Detection System is designed to enhance road safety by continuously monitoring drivers and alerting them when signs of drowsiness or distraction are detected. Using computer vision and machine learning techniques, our system analyzes facial features, eye movements, head position, hand positions and other behavioural patterns to classify driver states into:

- Normal driving
- Mild drowsiness
- Moderate drowsiness
- Severe drowsiness (sleeping)
- Distracted driving

This report details the implementation of our project, from data collection through model deployment on embedded hardware.

**Fig1: Mediapipe facial landmark detection**

---

## Background and Motivation

Road accidents caused by driver drowsiness and distraction are a growing public safety concern in India. According to the Ministry of Road Transport and Highways (MoRTH):

- Over 4.6 lakh (460,000) road accidents have been reported annually
- More than 1.5 lakh (150,000) fatalities occur every year
- In 2022:
  - Driver distraction caused over **10,000** crashes
  - Driver fatigue or sleep caused over **12,000** crashes

Our motivation for this project stems from creating an accessible, real-time monitoring system that can be implemented in commercial and personal vehicles. By providing timely alerts when drowsiness or distraction is detected, our system aims to prevent accidents and save lives. The integration with Raspberry Pi makes our solution cost-effective and easily deployable across various vehicle types.

---

## Methodology

### 1. List of Hardware Required and Their Specifications

| Hardware Component  | Specifications                                                                 | Purpose                                |
|---------------------|----------------------------------------------------------------------------------|----------------------------------------|
| Raspberry Pi 4 B    | Broadcom BCM2711 Quad-core Cortex-A72 (ARM v8) 64-bit SoC @ 1.5GHz<br>4GB LPDDR4-3200 SDRAM<br>2.4 GHz and 5.0 GHz IEEE 802.11ac wireless | Main processing unit for running the detection model |
| MicroSD Card        | 32GB Class 10                                                                   | Operating system and model storage     |

### 2. List of Software Used

| Software     | Version     | Purpose                                                                 |
|--------------|-------------|-------------------------------------------------------------------------|
| Raspberry Pi OS | -         | Operating system for Raspberry Pi                                       |
| Python       | 3.10.12     | Programming language for model development and implementation           |
| OpenCV       | 4.11.0.86   | Computer vision library for image processing and feature extraction     |
| MediaPipe    | 0.10.21     | Face and landmark detection framework                                  |
| NumPy        | 1.26.4      | Numerical computing for data manipulation                              |
| Pandas       | 2.2.3       | Data analysis and CSV handling                                         |
| Scikit-learn | -           | Machine learning library for decision tree implementation              |
| m2cgen       | -           | Model code generation                                                  |
| Git          | -           | Version control                                                        |

> **Note**: Table only refers to core software stack (full pinned list in `requirements.txt`).

---

## Data Collection

Our dataset consists of **115 video recordings** of drivers (30s, 30 fps, 900 frames each) covering six driver states:

1. **Normal driving** – 18 samples  
2. **Mild drowsiness (increased blinking)** – 18 samples  
3. **Moderate drowsiness (yawning)** – 20 samples  
4. **Severe drowsiness (sleeping)** – 20 samples  
5. **Distracted (looking away)** – 21 samples  
6. **Distracted (phone usage)** – 18 samples  

### Data Collection Process

- **Recording Setup**: Controlled environment, HD camera positioned similar to real deployment.
- **Protocol**:
  - Normal: Eyes on road
  - Mild drowsiness: Blinking more frequently
  - Moderate: Yawning
  - Severe: Eyes closed, head nodding
  - Distraction: Looking away
- **Data Augmentation**:
  - Random rotation (±10°)
  - Scaling (0.9–1.1x)
  - Translation (±5%)
  - Horizontal mirroring (50% chance)

---

## Feature Extraction

18 key features were extracted:

1. Eye Aspect Ratio (EAR)  
2. Mouth Aspect Ratio (MAR)  
3. Head Pose Estimation (yaw, pitch, roll)  
4. Hand Position Coordinates  
5. Hand-Eye Depth Difference  
6. No Visible Eye (boolean)  
7. Variance in Head Pose Angles  
8. Variance in Pupil Movement  
9. Number of Blinks  
10. Eye Pupil Distance from Center  
11. PERCLOS  
12. Variance in EAR over Time  
13. Duration of Head Pose Away  
14. Number of Times Head Pose Away  
15. Shoulder/Upper Body Pose Metrics  
16. Hands off Steering Wheel Detection  
17. Hand Proximity to Face Duration  
18. Eye Closure during Yawn  

### Pipeline:

1. Frame extraction  
2. Landmark detection (MediaPipe)  
3. Feature calculation  
4. Temporal feature aggregation  
5. Normalization  
6. Export to CSV  

---

## Key Code Modules

- `base.py`: Orchestrates frame processing  
- `eye.py`: EAR, blink detection  
- `hand_1.py`: Hand-eye depth, arm angle  
- `head_pose.py`: Pitch, yaw, roll estimation  
- `datacreator.py`: Converts labeled videos to data  
- `augument.py`, `preprocessing.py`: Augmentation & cleanup  
- `inference_recorded.py`: Inference on recorded/live feed  

---

## Model Development

### Model Selection: Decision Tree

Chosen for its ease of deployment on constrained devices.

#### Hyperparameters (RandomGridSearchCV, 5-fold, 60 iterations):

| Hyper-parameter      | Optimal Value |
|----------------------|---------------|
| Criterion            | entropy       |
| Max depth            | 40            |
| Max features         | 20            |
| Min samples / leaf   | 2             |
| Min samples / split  | 2             |

#### Final Performance:

| Metric        | Value   |
|---------------|---------|
| Accuracy      | 96.35%  |
| Macro-F1      | 0.963   |
| Weighted-F1   | 0.964   |
| # Leaves      | 472     |
| Model Size    | 500 KB  |

#### Confusion Matrix (Excerpt):

| Actual \ Predicted | Blink | Distraction | Normal | Phone | Sleep | Yawn |
|--------------------|-------|-------------|--------|-------|-------|------|
| Blink              | 2540  | 7           | 26     | 8     | 26    | 36   |
| Distracted         | 20    | 2721        | 14     | 3     | 5     | 13   |
| Normal             | 23    | 32          | 2844   | 6     | 3     | 21   |
| Phone              | 9     | 12          | 11     | 2466  | 8     | 22   |
| Sleep              | 41    | 16          | 4      | 17    | 1998  | 28   |
| Yawn               | 49    | 18          | 31     | 33    | 36    | 2709 |

#### Evaluation:

| Metric          | Value     |
|-----------------|-----------|
| Accuracy        | 96.82%    |
| F1 Score        | 0.9635    |
| Training Time   | 15 sec    |
| Inference (PC)  | 30 fps    |
| Inference (Pi4) | 6-7 fps   |

#### Dataset:

| Partition | Samples | Features |
|-----------|---------|----------|
| Train     | 63,424  | 55       |
| Test      | 15,856  | 55       |

---

## Model Deployment

### Architecture

1. **Data Acquisition Module**:
   - Uses DroidCAM over TCP
   - Performs face detection, landmark extraction
2. **Real-Time Processing Pipeline**:
   - Live frame capture → Landmark detection → Feature extraction → Model inference

### Prototype & Demo

- Camera mounted near rearview mirror, facing driver
- Initial 30-60 frames build time window buffer
- Real-time driver state prediction

**Fig2: Real-time annotated driver state output**

---

## Project Resources

- **Repository**: [GitHub](https://github.com/harsh-kmr/edge-ai)  
- **Demo Video**: [OneDrive Share](https://indianinstituteofscience.my.sharepoint.com/:f:/g/personal/harshkumar1_iisc_ac_in/Eo_0ujCKjClPmhYjkk5YbucBN1_mPig8EBLInQfk-A8XeA?e=dUtcjh)  
- **Dataset**: Shared via email  
- **Model Files**: [model.py](https://github.com/harsh-kmr/edge-ai/blob/main/model.py)

---

## Unique Contributions

- Empirical bounding box using body landmarks for steering detection
- High-quality labeled dataset with 100k+ images
- Real-time inference on edge devices
- Optimized feature extraction pipeline
- 29-30 fps video streaming at 960x540 resolution
- Created custom pose estimation dataset & model
- Replaced heavy MediaPipe model with custom lightweight CNN

---

## Challenges and Workarounds

- **Computational Constraints**:
  - Removed heavy PyTorch phone-detection model (~800MB)
  - Used alternative features (e.g., hand near face)

- **Major Bottleneck**:
  - MediaPipe restricts weight access & optimization
  - Addressed with model distillation to smaller CNN

- **Feature Calculation**:
  - Implemented running statistics instead of full-buffer processing

---

## Pose Estimation Model

- **Dataset**:
  - ~100,000 frames
  - 48 annotated keypoints (x, y, z)

- **Model**:
  - Lightweight CNN
  - Reduced Mediapipe model (500MB) → CNN (122MB)

---

## Future Work

- Model quantization (~30.5 MB size)
- Transition to PyTorch for better maintainability
- Benchmark custom pose model vs. MediaPipe
- Streamline pipeline for improved performance

---

## References

1. Soukupova, T., & Cech, J. "Real-Time Eye Blink Detection using Facial Landmarks", CVPRW, 2016.  
2. [Google MediaPipe Documentation](https://developers.google.com/mediapipe)  
3. [PMC Article](https://pmc.ncbi.nlm.nih.gov/articles/PMC10384496/)