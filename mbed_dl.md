---
layout: page
title: Embedded Deep Learning & TinyML
subtitle: ECE, Carnegie Mellon University
---
## Course Description  
---  
Embedded or “edge” devices with sensors generate a tremendous amount of data every second. 
Sending these data to the cloud for intelligent decision making by machine learning models 
consumes energy and imposes undesired latency and cost. Processing the data locally on the 
edge lowers latency, energy, and cost. This course introduces deep neural network architectures,
such as dense, convolutional, and recurrent networks, and their respective applications and 
training in the cloud. Students then learn to downsize their trained models so they can deploy 
them for inferencing on microcontrollers running on the edge with power and computation constraints. 
Students are encouraged to create their own projects drawing from such fields as agriculture, 
environment, conservation, health, manufacturing, or home automation. Students are expected to have 
embedded systems knowledge equivalent to 18-349 (Introduction to Embedded Systems). This course is 
cross-listed as **18-448 and 18-848C**.  

## Instructor
---
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
* {
  box-sizing: border-box;
}

/* Create two equal columns that floats next to each other */
.column {
  float: left;
  width: 60%;
  padding: 10px;
  height: 220px; /* Should be removed. Only for demonstration */
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}
</style>
</head>
<div class="row">
  <div class="column">
Ziad Youssfi, PhD <br>    
Associate Teaching Professor, <br> 
Electrical & Computer Engineering,<br>  
(zyoussfi@andrew.cmu.edu)<br>   

I developed this course to help students learn about<br> 
the exiting new opportunities in the field of <br> 
embedded machine learning and tinyML.<br><br>  
  </div>

  <div class="column"><img width="40%" src="/mbed_dl/assets/img/Me.jpg"></div>
</div>
</html>

## Teaching Assistants
---
### Spring 23
* Chao-Peng Liu                                                   
Master Program, Electrical & Computer Engineering                          
(chaopenl@andrew.cmu.edu)                                                
* Yen-Shuo Su   
Master Program, Electrical & Computer Engineering                    
(yenshuos@andrew.cmu.edu)                         
 
### Fall 23
* Eric (Jingxuan) Wu                                     
Master Program, Electrical & Computer Engineering                         
(jingxua5@andrew.cmu.edu)                          
* Netra Trivedi                                 
Master Program, Electrical & Computer Engineering                         
(nptrived@andrew.cmu.edu)                           
* Eion Tyacke                          
Master Program, Electrical & Computer Engineering                         
(etyacke@andrew.cmu.edu)                         

## Topics
---
* Motivation for TinyML or Embedded Machine Learning and its applications
* Fundamental of Deep Neural Networks for dense and convolutional architectures
* Machine learning pipeline for embedded systems
  - Data collection, preprocessing, and data engineering
  - Designing and training a model
  - Model conversion concepts for embedded and mobile devices:  
   post training and training aware quantization
  - Model deployment to embedded systems
* Real-time embedded systems optimization 
* Ethics of ML and embedded ML
* Applications of machine learning pipeline to the following domains:
  - Motion detection using an IMU (inertial management unit) sensor
  - Audio classification using a microphone sensor
  - Computer vision using a camera sensor
  - Anomaly detection using a combination of sensors
* Object detection models such as YOLO v1-8 
* Sensor fusion (if time permits)

## Assginements
1. Concepts and motivations for TinyML
2. Building shallow neural networks with Python and Jupiter Notebook/Google Colab
3. TensorFlow, the Gradient and building deep neural networks
4. Gesture recogntion part 1: data collection
5. Gesture recogntion part 2: Building and doploying a model on the Arduino Nano 33 BLE sense
6. Speech command part 1: data collection for wakeup keywords
7. Speech command part 2: Building and deploying a model on the Arduino Nano 33 BLE sense
8. Object detection part 1: data collection using smartphone camera or the OV7675 camera 
9. Object detection part 2: Building and deploying a model to Arduino Nano 33 BLE sense or smartphone.  
   (Assginment 8 & 9 are subject to time availability in the semester)

## Projects
---
This course engages students with group driven projects and presentations   
[Please visit the project summary listing for Spring 2023](/embed-dl-s23/EmbeddedDL_S23/projects_s23)  
[Please visit the project summary listing for Fall 2023](/embed-dl-s23/EmbeddedDL_S23/projects_s23)

#### Acknowledgment
---
**We acknowledge Edge Impuluse for their donations of Arduino Nano 33 BLE ML kits and the free access to their Design Studio**  
<img src="/embed-dl-s23/assets/img/edge_impulse_1.jpg" width="35%" height="35%">

