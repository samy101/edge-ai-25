---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## Enhancing Plan-Seq-Learn with Activation-aware Weight Quantization for Efficient Robotic Manipulation

### Introduction

This project demonstrates the development, quantization, and deployment of a **Large Language Model (LLM)** using the **Activation-aware Weight Quantization (AWQ)** technique to optimize inference for edge devices with limited computational and memory resources. 

We benchmark the model's performance in terms of **size**, **latency**, and **accuracy** before and after compression.
<!-- 
> _AI-generated content may be incorrect._ -->

With the rise of transformer-based language models, deploying these models on **edge devices** remains a challenge due to their high memory and compute requirements. **AWQ** offers a promising solution by enabling quantization while preserving performance.

### Objective

Compress a model like **LLaMA 2** or **Mistral 7B** using AWQ and deploy it efficiently on **consumer-grade hardware**, validating its usability for downstream tasks **without cloud dependence**.

---

### Methodology

We follow a pipeline starting from:

1. Selecting a base model
2. Quantizing it using AWQ
3. Evaluating real-world performance across various metrics

---

#### Hardware Specifications

| Component         | Specification                                                                 |
|------------------|---------------------------------------------------------------------------------|
| **Edge Device**   | NVIDIA Jetson Orin NX                                                          |
| **GPU**           | 1024-core NVIDIA Ampere GPU with 32 Tensor Cores                               |
| **CPU**           | 6-core Arm Cortex-A78AE v8.2 64-bit                                            |
| **RAM**           | 16 GB 128-bit LPDDR5                                                           |
| **Storage**       | 128 GB NVMe SSD (expandable via M.2 Key M slot)                                |
| **Power**         | Configurable: 10W to 25W                                                       |
| **OS**            | Ubuntu 20.04-based JetPack SDK (v5.1 or later)                                 |
| **Connectivity**  | Gigabit Ethernet, USB 3.1, PCIe Gen4, DisplayPort                              |

---

#### Software Used

- Python 3.9  
- PyTorch 2.0  
- Hugging Face Transformers  
- Hugging Face `awq` quantization package  
- CUDA 11.7  
- Hydra (configuration management)  
- Mujoco (for simulated environments)

---

### Data Collection

Task prompts were collected from a variety of **standard NLP benchmarks**, such as:

- HELM  
- MMLU  
- Custom domain-specific prompts

These were used to evaluate **accuracy**, **latency**, and **usability** before and after quantization.

---

### Model Development and Compression

We started with a pre-trained **7B model** (either **LLaMA 2** or **Mistral 7B**) and performed **4-bit AWQ quantization**. The quantization steps included:

- Identifying high-activation outliers via calibration  
- Applying per-channel symmetric quantization  
- Reordering weights and applying bias correction  
- Saving quantized weights via Hugging Face AWQ utilities  

### Compression Results:

- Reduced memory usage by **>80%**
- Only **~2% drop** in task success rate

| Metric              | Full-Precision LLM | AWQ-Quantized LLM |
|---------------------|--------------------|-------------------|
| **Model Size**       | 13 GB              | 3.2 GB            |
| **Memory Usage**     | 7 GB VRAM          | 1.1 GB VRAM       |
| **Inference Latency**| 500 ms             | 180 ms            |
| **Task Success Rate**| 96%                | 94%               |

---

### Model Deployment

The quantized model was deployed using the **Hugging Face AutoAWQ inference pipeline** on a local GPU machine.

Features of the deployment:

- Real-time interaction support  
- Lightweight configuration and weights for edge compatibility  
- Uses `torch.no_grad()` to minimize memory footprint  

---

### Prototype and Demo

A working prototype was deployed on the **NVIDIA Jetson Orin NX**, running the quantized model locally.

### Demo Highlights:

- **Fast Response Time**: ~180 ms latency
- **Low Power Consumption**: Operated within **15W** during inference
- **Offline Capability**: No internet required for inference
- **Use Cases Demonstrated**:
  - Question Answering
  - Summarization
  - Instruction Following

<!-- > _AI-generated content may be incorrect._ -->

### Link to Demo Assets:

[Code, Demo, and Resources](https://drive.google.com/drive/folders/1Jz_NLxdxyLBHWQLxSooZtBt3TQA4EJ_U?usp=sharing)

---

### Challenges and Workarounds

**1. Limited GPU Memory on Edge Devices**
- **Challenge**: Full-precision LLMs caused OOM (Out-of-Memory) errors on Jetson Orin NX  
- **Workaround**: Used **AWQ quantization**, reducing VRAM usage to <2 GB with negligible accuracy drop

**2. Lack of AWQ Support for Some Architectures**
- **Challenge**: Some models lacked official AWQ support  
- **Workaround**: Used community forks (e.g., from **TheBloke**), manually aligned config files and loaders

**3. Debugging Memory Leaks During Deployment**
- **Challenge**: RAM usage grew unexpectedly during Flask API deployment  
- **Workaround**: 
  - Used `torch.no_grad()` consistently  
  - Monitored GPU with `tegrastats`  
  - Restarted service periodically to prevent leaks

---

### Learnings and Insights

- **AWQ’s outlier-aware quantization** provides a superior trade-off between compression and quality than naive 4-bit quantization
- The **Jetson Orin NX** is capable of real-time LLM inference with proper optimization
- Alignment between model weights, tokenizers, and quant loaders is **critical** when using open-source models from Hugging Face

---

### References

1. Y. Lin, S. Liu, Z. Liu, and H. Zhang, “AWQ: Activation-aware Weight Quantization for LLM Compression and Acceleration,” arXiv preprint, 2023. [arXiv:2306.00978](https://arxiv.org/abs/2306.00978)

2. NVIDIA, “Jetson Orin NX Series,” [NVIDIA Official Website](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-orin/)

3. D. Pal, S. Ghosh, and V. P. Namboodiri, “Plan-Seq-Learn: Plan your Prompt before you Roll the LLM,” arXiv preprint, 2024. [arXiv:2403.09087](https://arxiv.org/abs/2403.09087)
