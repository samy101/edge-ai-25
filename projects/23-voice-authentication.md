---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Voice Authentication and Command Classification for Two-Wheelers Using Machine Learning and AI

### Introduction

This voice authentication and bike command classification works by first registering users using a 27-second voice clip during the registration process. It also collects a 2-second audio clip of “Hey TVS” as a wake word from the user during the registration phase. During the login phase, it collects a 10-second audio clip from the user. It then finds the similarity score of the login user with all the registered users one by one. The same person who had previously registered and is now trying to login will have the maximum similarity score, and that score should also be more than 0.7.

For registration purposes, we used **speechbrain**, a Python package and an open-source toolkit designed for developing, training, and deploying speech and audio processing systems. It’s built on top of PyTorch and is widely used in research and real-world applications.

---

### Data Collection

#### Part 1 – User_Voice_Authentication_DataSet

- **Registration:** For user registration, a 27-second audio clip is recorded and stored in the *Registration* folder for the person who wants to register.  
- **Login:** A 10-second audio clip of a registered user who wants to login is stored in the folder named *Login*.  

Since we are using SpeechBrain which is a pretrained model, we do not need to train it externally to compute similarity scores of speech. For demonstration purposes, we are providing 3 users’ samples here, each for Registration, Login, HeyTVS wake word, and Command folders.

#### Part 2 – NLP_Bike_Command_DataSet

This folder contains a CSV file with:

- 1495 bike commands labeled as `1`  
- 1495 non-bike commands labeled as `0`  

This dataset has been built from scratch with a total of **2990 data points**. Each bike command can be further subclassified as **EDGE**, **CLOUD**, and **UPDATE**.

Once a user is registered and logs in, they can use their own voice commands to control the bike, enhancing the user experience.

---

### Models

We have built 4 LSTM models:

1. **Main model:** Classifies a command as bike or non-bike and into subclasses EDGE, CLOUD, or UPDATE.  
2. If it is a bike command and falls in one of these subclasses, it is further classified into its respective subclass category.

Accordingly, appropriate responses can be generated, and the bike can be controlled.

**Example:**  
“Show me the shortest route to Goa”  
- **Classification:** Bike Command  
- **Subclass:** CLOUD  
- **Subclass Category:** Traffic Maps

---

### Dataset Information [Bike vs Non Bike Command DataSet]

| Command Type | Subclass          | No. of Data Points | Subclass Category           | No. of Data Points |
|--------------|-------------------|--------------------|----------------------------|--------------------|
| **Bike**     | Edge              | 551                | Basic                      | 287                |
|              |                   |                    | Battery Fuel               | 144                |
|              |                   |                    | Tyres                      | 120                |
|              | Cloud             | 450                | Traffic/Maps               | 145                |
|              |                   |                    | Songs/Media                | 102                |
|              |                   |                    | News/Notifications         | 102                |
|              |                   |                    | Weather                    | 101                |
|              | Update            | 319                | Check                      | 120                |
|              |                   |                    | Perform                    | 103                |
|              |                   |                    | Cancel                     | 100                |
| **Non-bike** | Non-Bike          | 1495               | N.A                        |                    |
| **Total**    |                   | **2990**           |                            | **2990**           |

---

### Deployment

All LSTM models are converted to **tflite** with `tf.default` optimization which applies quantization of models to `int8`, achieving approximately **10x compression reduction**.

- Original model size: **40 MB**  
- After compression and quantization: approximately **4.1 MB** (~10x reduction)

---

### Flowcharts

1. Speaker Registration Flowchart  
2. Speaker Login Flowchart  
3. Threshold Optimization Flowchart  
4. Speaker Validation Flowchart  
5. NLP MAIN MODEL FLOWCHART  

<!-- *(Flowchart images/diagrams should be inserted here)* -->

---

### Conclusion

We successfully demonstrated a voice authentication and bike command classification system deployed on an edge device, specifically the Raspberry Pi 5.

To optimize performance and memory usage, the NLP models were quantized to **INT8** format with weight quantization. Additionally, audio clips used for voice authentication were stored in `.wav` format to minimize memory consumption.

Through these optimizations, we achieved a **10x reduction in model size**, bringing it down from 40 MB to just 4 MB. Despite significant compression, the system maintained high performance, achieving an accuracy of **98.78%** in classifying registered users after deployment on the Raspberry Pi.

The novelty of the system lies in its ability to effectively filter out unwanted noise and accurately detect the registered user, ensuring robust performance in real-world, noisy environments.

Finally, the entire solution was integrated with the bike’s instrument cluster via an Android application, enabling seamless end-to-end deployment for practical use.
