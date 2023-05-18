---
layout: post
title: Dog Fitbit
subtitle: Ajith Potluri, Eion Tyacke, and Parker Crain
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/dog_fitbit_1.jpg
# share-img: /assets/img/path.jpg
# tags: [books, test]
---

This project investigates on-device deep learning models paired with an embedded system that can be used to track the movement of a dog for its owner. This valuable insight may help an owner to better understand the activities of the dog while the owner is away. The microcontroller with a battery is small enough that it could easily be attachable to a dog’s collar.

The goal is to classify the movements of the dog into the categories of walking, pacing, playing, sniffing, lying on chest, sitting, and standing. Tracking these activities can offer pet owners an enhanced understanding of their dog's health, well-being, and potential issues, such as stress or discomfort. This information is particularly useful in assessing the effects of new medications or identifying anxiety that may arise when the dog's owner is away.

The project utilizes an Arduino Nano BLE with an onboard IMU, and bluetooth chips for our MCU as seen in Figure 2. This allows for the project to be all on one breakout board, sans the battery, for a compact design. The bluetooth functionality provides seamless data transmission and synchronization with the owner's smartphone.
Leveraging on-device machine learning models can offer significant benefits in this context. By performing all of the computation on-device, the system saves bandwidth and latency.

Additionally, the microcontroller is relatively low cost, allowing this to be an attractive option for a dog owner. This device needs to be physically robust, as dogs often play rough and may break an unprotected microcontroller easily; however, the model itself doesn’t need to be perfect as it only provides the owner with additional insight into the dog’s activities. Lastly, the on-device model will ensure privacy for both the dog and the owner.

In our pursuit to develop a valuable tool for dog owners, we engaged with a knowledgeable group of dog trainers to determine the most essential canine activities to monitor. Through these fruitful discussions, we compiled a comprehensive list of behaviors, including walking and pacing, which can serve as indicators of separation anxiety when dogs are left alone during the day. Additionally, our collaboration highlighted the importance of tracking changes in activity levels as a means to evaluate the effects of new medications on a dog's typical behavior patterns. This valuable input from dog trainers helped us tailor our solution to better address the real-world needs of pet owners. 
<p align="center"> <img src="/assets/img/dog_fitbit_1.jpg" width="50%" height="50%"> </p>
<p align="center"> <img src="/assets/img/dog_fitbit_2.jpg" width="110%" height="110%"> </p>
