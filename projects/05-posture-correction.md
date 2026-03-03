---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## AI-Powered Posture Correction System on Edge Devices

### Introduction

This project focuses on developing an AI-based posture correction system designed to run on edge devices, enabling real-time detection and correction of poor sitting or standing posture. By utilizing Machine Learning models , the system delivers posture-related feedback without depending on cloud computing, ensuring low latency, privacy, and cost-effectiveness. 

Posture-related health problems—such as chronic back pain, spinal dysfunction, and joint degeneration—are increasingly common due to sedentary work environments and prolonged screen time. Traditional methods for posture correction are either manual, intrusive, or expensive. The integration of artificial intelligence with edge computing opens up opportunities for scalable, real-time, and privacy-preserving posture monitoring systems. The motivation for this project is to provide an accessible, low-cost, and intelligent solution for daily posture monitoring using widely available hardware. 

<p align="center">
  <img src="../assets/img/projects25/05-posture-implementation.png" 
       alt="Posture Correction System" 
       width="500"
       style="border-radius: 10px;">
</p>

### Hardware and Software Requirements

**Hardware:**
- 3 × Nano 33 BLE Sense  
- Cables  

**Software:**
- Arduino Lab for MicroPython  
- Arduino IDE  
- Thonny  
- Edge Impulse  
- Google Colab  
- Python  
- TensorFlow Lite  

**Other Materials:**
- Velcro Strips  
- Cloth  
- Stapler  
- Foam  
- 3D printed cases  

---

### Data Collection

- **Approach:** Captured IMU sensor data from accelerometer, gyroscope, and magnetometer readings based on the user’s sitting, standing, and jogging in various postures (good and bad).  
- **Participants:** Youth and adults performing each activity in both good and bad postures.  
- **Sampling Rate:** 10 samples/sec  
- **Dataset Size:** Approximately 24,000 samples per activity, including both good and bad postures.  

---

### Model Development

- Timestamped data collected from three sensors, capturing both good and bad postures using Arduino Lab and Thonny, saved as CSV files.  
- Data synchronized in Google Colab by aligning timestamps from each sensor for accurate alignment.  
- Preprocessed dataset uploaded to Edge Impulse, which split data into training and testing sets at a 4:1 ratio.  
- A Convolutional Neural Network (CNN) model trained using this dataset.  
- Trained model exported in TensorFlow Lite (TFLite) format for edge deployment.  

<!-- **Edge Impulse model link:** [https://studio.edgeimpulse.com/public/683753/live](https://studio.edgeimpulse.com/public/683753/live) -->

---

### Model Deployment

- The downloaded TFLite model was deployed on Google Colab to emulate real-world deployment for posture classification.  
- TensorFlow Lite Interpreter was used to load the model and preprocess input data.  
- Inference performed to classify postures as good or bad, simulating actual application environment.  
- Setup validated model accuracy and responsiveness, ensuring readiness for deployment on edge devices such as wearables or mobile systems.  

---

### Prototype

- **Setup:** Velcro straps stapled to cloth aligned with the backbone.  
- Nano BLE boards fitted into 3D printed cases, adjusted with foam for perfect fit.  
- Velcro straps attached to bottom of cases to secure BLEs in the correct position on the back to measure backbone movements.  

- **User Interface:**  
  Test dataset is fed to the model which classifies posture as good or bad and displays the output.  

---

### Project Resources

- **Sensor Hardware:** Arduino Nano 33 BLE Sense boards (×3) for motion data collection.  
- **Data Collection Setup:** Custom wearable with cloth, foam, velcro straps, 3D printed sensor cases.  
- **Development Tools:** Arduino IDE, Thonny, Arduino Lab for MicroPython.  
- **Machine Learning Platform:** Edge Impulse (training and converting ML models).  
- **Model Testing Platform:** Google Colab (data synchronization, TFLite testing, deployment simulation).  
- **Programming Languages:** Python, MicroPython.  
- **ML Framework:** TensorFlow Lite (for lightweight model deployment and testing).  
- **Dataset:** ~24,000 labeled samples from different postures (sitting, standing, jogging in good/bad form).
- **Supporting Materials:** Cloth, foam, velcro, stapler, 3D printed enclosures for wearable design.  

---

### Challenges and Workarounds

| Challenge                                                 | Workaround                                                      |
|-----------------------------------------------------------|----------------------------------------------------------------|
| Large dataset and large model size                        | Used unoptimized float32 model instead of quantized int8 model |
| Difficulty collecting data for prolonged postures        | Collected data in batches, then synchronized & merged by timestamps |
| BLE sensitivity                                           | Ensured correct posture without slight errors                  |
| Wired BLE connections to laptops during movement         | Moved with the person performing activity while holding laptops for proper BLE connection |

---

### References

- [The Importance of Body Posture in Adolescence](https://journals.lww.com/imsp/fulltext/2023/14040/the_importance_of_body_posture_in_adolescence_and.3.aspx)  
- [PMC Article 1](https://pmc.ncbi.nlm.nih.gov/articles/PMC9465722/)  
- [PMC Article 2](https://pmc.ncbi.nlm.nih.gov/articles/PMC6166197/)  
- [ChatGPT](https://chatgpt.com)  
- [ScienceDirect Article](https://www.sciencedirect.com/science/article/pii/S01698141230013)  

