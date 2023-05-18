---
layout: post
title: Bird Feeder
subtitle: Eric Wu, Harry Rosmann, and Blaine Huey
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/bird_feeder.jpg
# share-img: /assets/img/path.jpg
# tags: [books, test]
---
The idea originated from an animal status monitor and evolved into a bird feeder monitoring system with squirrel detection. We are running two models on the Arduino Nano 33 BLE. The first model detects whether the approaching animal is a bird or squirrel. If a squirrel is detected, an alarm is triggered to scare away the squirrel. If a bird is detected, the second model that detects bird type is invoked to identify the type of bird on the feeder. That bird image is then stored in an attached SD card to be downloaded and viewed later.  
We selected two datasets to train our models. For squirrel datasets, we used Roboflow Squirrels and Animals-10 that contains around 4000 squirrel images. For bird datasets, Caltech-UCSD Birds-200-2011 Dataset and iNaturalist Pittsburgh Area Data contains around 4000 bird pictures. We also added around 2500 other pictures with neither a bird or a squirrel.  
<p align="center"> <img src="/embed-dl-s23/assets/img/bird_feeder.jpg" width="50%" height="50%"> </p>
