---
layout: post
title: Motor Care - Condition Based Monitoring
subtitle: Abhishek Basrithaya and Yuyang Xu
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/motor_care_1.jpg
# share-img: /assets/img/path.jpg
# tags: [books, test]
---

An electric motor is a rudimentary electro-mechanical device that is ubiquitous from wheels of an automobile, fans, automatic windows shades to magnetic disks for memory storage etc. Efficient operation of these fundamental devices is imperative for the smooth operation of the overarching device in question. Timely maintenance of these motors are essential to maintain the desired efficiency levels. Introducing “Motor Care”, a data driven system that continuously monitors the target motor with the help of sensors attached to the motor. Providing feedback and analytics on the motor performance and maintenance of critical motor parts. Developing such a model requires apprehension of sensors needed, collecting meaningful data, extracting important features, training our model and final deployment on an embedded platform.  

In this project, we employed embedded deep learning techniques to detect specific structural defects such as cracks and imbalances that arise due to wear and tear of motor parts during its operation using onboard IMU sensor on the Arduino Nano 33 BLE for vibrational data and an add-on camera module to capture on-surface cracks. Vibration and image data was collected both under normal operating conditions and faulty conditions under strict supervision of the motor environment.  

To simulate faulty operating conditions in vibrational data, we added custom weights to the motor shaft gears, 3D printed custom shaft gears with deformities of varying magnitude to create imbalanced conditions. As for the images, we used doctored images to emulate structural deformities both in static and dynamic conditions. Our project architecture diagram is shown in Figure 1, and our setup for the experiment in Figure 2.label are not overwritten.)
<p align="center"> <img src="/assets/img/motor_care_2.jpg" width="100%" height="100%"> </p>
<p align="center"> <img src="/assets/img/motor_care_4.jpg" width="100%" height="100%"> </p>
<p align="center"> <img src="/assets/img/motor_care_3.jpg" width="100%" height="100%"> </p>
