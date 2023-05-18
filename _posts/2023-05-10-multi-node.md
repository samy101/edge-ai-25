---
layout: post
title: Multinode Embedded Deep Learning
subtitle: Jong-Ik Park, Chad Taylor, and Anudeep Bolimera
# cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/multi_node_1.jpg
# share-img: /assets/img/path.jpg
# tags: [books, test]
---


The rapid expansion of the Internet of Things (IoT) and the growing number of edge devices have significantly increased the amount of data generated and processed. This shift has led to a rising demand for efficient and cost-effective embedded systems to handle various tasks, including anomaly detection. High-specification devices, while providing substan- tial computing power and memory, often come with a steep price tag, which may be challenging for many applications. As such, there is a pressing need to explore alternative methods to utilize low- specification devices without compromising perfor- mance or accuracy.  

Embedded deep learning has emerged as a pow- erful approach to anomaly detection, particularly in image-based applications, where rich visual in- formation can provide valuable insights not avail- able in tabular data. Images offer spatial, tempo- ral, color, and texture information that can detect subtle changes and anomalies that may not be found in tabular data, thereby increasing test perfor- mance. Despite its potential, implementing image- based anomaly detection in embedded deep learning presents challenges due to the inherent limitations of edge devices, including restricted computing power, memory, and storage capacities.  

In this project, we propose a method to overcome these constraints by distributing the training and inference of a single model across multiple low- specification devices. This approach enables the use of a large rather than a small model for a single edge device, improving test accuracy and efficiently utilizing the resources of edge devices, as they all participate in the training and inference process. By leveraging the collective power of several low- specification devices, we can achieve a performance comparable to that of high-specification devices at a significantly lower cost.
<p align="center"> <img src="/embed-dl-s23/assets/img/multi_node_1.jpg" width="100%" height="100%"> </p>

