---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Smart Retail Verification using FOMO model on Nicla Vision

---

### Introduction

Retail businesses rely heavily on manual checkout processes prone to human errors in billing and inventory management. These errors lead to financial losses and poor customer experience. Traditional operations involve time-consuming manual product identification that impacts both operational efficiency and customer satisfaction.

Our **Smart Retail Verification** system addresses these challenges through an **Edge AI solution** that automatically verifies items at checkout. The system consists of a **Nicla Vision device** running a lightweight object detection model and a **Python GUI application** for verification. This combination creates an efficient system that compares billed items against AI-detected items.

---

### System Architecture

The Smart Retail Verification system consists of two main components:

- **Nicla Vision**
- **UART Communication** (115200 baud rate)
- **PC Application**

### A. Edge Device - Nicla Vision

#### Table I: Key Challenges in Traditional Retail Checkout

| Challenge                   | Impact                        |
|----------------------------|-------------------------------|
| Manual item identification | Slow checkout process         |
| Human error in billing     | Financial losses              |
| Incorrect inventory tracking | Stock management issues    |
| Labor-intensive verification | Increased operational costs |
| Theft and fraud            | Revenue leakage               |

#### Motivation:
- Manual processes leading to billing and inventory errors  
- Growing demand for efficient checkout experiences  
- Need for effective loss prevention methods  
- Operational inefficiencies affecting business profitability  

#### Table II: Nicla Vision Hardware Specifications

| Component   | Specification             |
|------------|---------------------------|
| Processor  | Dual ARM Cortex-M7 (480MHz) |
| Memory     | 1MB RAM, 2MB Flash        |
| Camera     | 2MP Color Camera          |
| Connectivity | UART, USB               |
| Dimensions | 22.86 × 22.86 mm          |
| Power      | 3.3V, USB powered         |

Nicla Vision serves as the core sensing and processing unit:
- Runs **FOMO** object detection model  
- Merges nearby objects from same class  
- Sends detection data via **UART (115200 baud)**  

### B. PC Application

Python-based GUI application for Windows (tkinter, Python 3.13.2) providing:
- Product catalog  
- Manual billing  
- Visual verification of detected items  

### C. Communication Protocol

Custom message format:

`DETECTION|ItemName:Quantity:Confidence|...`


This allows efficient, multiple detections in a single message, compatible with UART bandwidth constraints.

---

### Data Collection and Model Development

#### Dataset and Preprocessing

- **4 classes**: KitKat, Goodday, Hide-n-Seek, Unibic  
- **Total samples**: 4050 (after augmentation)  
- **Preprocessing**:  
  - Resize to **96×96**  
  - Convert to grayscale  
  - Normalize  
- **Augmentation**: flip, rotate, brightness, exposure, blur, shear  

#### Model Selection and Optimization

- Trained **FOMO** model for 100 epochs  
- Applied **INT8 quantization**

#### Table III: Model Characteristics Before and After Optimization

| Characteristic      | Before (float32) | After (int8)  |
|---------------------|------------------|---------------|
| Flash Usage         | 113.8 KB         | 91 KB         |
| Quantization        | Float32          | INT8          |
| F1 Score            | 92%              | 91.3%         |
| Inference Time      | 115 ms           | 60 ms         |
| Peak Memory Usage   | 363.2 KB         | 119.4 KB      |

### Post-Processing

To reduce duplicate detections for large objects:
- Applied class-specific merging
- Used distance thresholds to merge close detections
- Improved detection reliability significantly

---

### mplementation

#### Object Detection Implementation

Features:
- Camera initialization
- Real-time display of detections
- FOMO inference
- Class-specific post-processing
- UART communication of results

#### PC Application Features

- Device connection management  
- Manual entry of billed items and pricing  
- Automatic verification against detected items  
- Visual alerts for matches/mismatches  

#### Verification Workflow

Steps:

1. Place items in camera’s field of view (~45cm distance)  
2. Detected items appear in **Detected Items** panel  
3. User enters items in **Biller Items** panel  
4. System compares both lists  
5. Matches or mismatches reported  

This provides immediate feedback and prevents billing errors.

---

### hallenges and Lessons Learned

#### Challenges

- Optimizing model for Nicla’s limited 1MB RAM & 2MB Flash  
- Achieving accuracy under varied lighting  
- Designing reliable communication protocols  
- Creating user-friendly yet functional GUI  
- Debugging embedded systems with limited logs  
- Ensuring consistent camera setup  
- Maintaining minimum confidence (0.6)  
- Real-world usability in constrained environments  

#### Lessons Learned

- INT8 quantization reduced model size from **887KB → 240KB**  
- Post-processing improved reliability  
- Camera height/position critical for accuracy  
- Debug logs helped troubleshooting  
- Real-time protocols require robust design  
- Augmentation improves model robustness  
- Real-world testing is essential  

---


### Conclusion and Future Work

#### Conclusion

The **Smart Retail Verification** system proves the feasibility of Edge AI in retail settings. With optimized object detection on Nicla Vision and a user-friendly GUI, the system helps reduce billing errors.

**Key Achievements:**
- End-to-end Edge AI implementation  
- Effective model compression  
- Real-time detection + GUI-based verification  
- Potential uses: checkout, inventory, loss prevention  

#### Future Work

- Expand product catalog  
- Improve lighting robustness  
- Enhance GUI (e.g. analytics)  
- Add barcode integration  
- Build standalone embedded system  

**Ultimate vision:**  
An end-to-end **automated checkout** system:
- Conveyor belt scanning  
- Auto-billing  
- Auto-packing with RFID  
- Alarm for unpaid items  

Such a system would revolutionize retail automation.

---

### References

1. "Edge Impulse Documentation," Edge Impulse, 2023. [Online]. Available: [link](https://docs.edgeimpulse.com)  
2. D. Barry, et al., “FOMO: Fast Objects, More Objects for Embedded Machine Vision,” *Conference on Machine Learning and Systems*, 2022.  
3. "Arduino Nicla Vision Documentation," Arduino, 2023. [Online]. Available: [link](https://docs.arduino.cc/hardware/nicla-vision)  
4. "Roboflow Documentation," Roboflow, 2023. [Online]. Available: [link](https://docs.roboflow.com)  
5. J. Smith, M. Johnson, "Applications of AI in Retail: A Comprehensive Survey," *Journal of Retail Technology*, vol. 15, no. 3, pp. 234–250, 2023  
