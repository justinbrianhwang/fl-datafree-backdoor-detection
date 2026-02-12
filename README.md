# Federated Backdoor Forensics
Data-free backdoor detection in Federated Learning via reverse engineering.

---

## Overview

This repository contains experimental code for detecting backdoor attacks in Federated Learning (FL) settings **without access to client data**.

We demonstrate that:

- Backdoor attacks can remain hidden under high clean accuracy.
- Data-free reverse engineering can expose backdoor vulnerability.
- Reverse Engineering (RE) score correlates strongly with ASR.
- Experiments were conducted on NVIDIA H100 GPU.

---

## Motivation

Federated Learning preserves privacy by keeping data on client devices.

However, it introduces a critical vulnerability:

> A single malicious client can inject a backdoor into the global model.

Since the server cannot access client data, detecting such attacks is challenging.

This project explores a **data-free forensic approach** to detect backdoors.

---

## Experimental Setup

- Dataset: CIFAR-10
- Model: ResNet-18
- Clients: 5
- Malicious Clients: 1
- Aggregation: FedAvg
- Poison Rate: 0.2 ~ 0.3
- GPU: NVIDIA H100

---

## Attack Setting

The malicious client:

- Inserts a square trigger into a subset of training samples
- Changes labels to a target class (e.g., airplane)

Metrics:

- Clean Accuracy
- Attack Success Rate (ASR)

---

## Data-Free Reverse Engineering

We optimize a trigger patch δ via:

min_δ  L(f(x ⊕ δ), y_t) + λ||δ||²

Where:
- x is random noise
- y_t is target class

If the model is backdoored:
- δ converges quickly
- Final loss is low
- RE score is low

---

## Results Summary

- Clean accuracy remains stable.
- ASR increases significantly under attack.
- RE score decreases as ASR increases.
- Strong negative correlation between ASR and RE score.

---

## Reproducibility

### Requirements

- Python 3.10+
- PyTorch
- torchvision
- CUDA 11+
- GPU (A100 or H100 recommended)

Install dependencies:

```bash
pip install torch torchvision matplotlib pandas tqdm
```

Repository Structure
```
.
├── DataFree_Backdoor_FL.ipynb
├── ablation_results.csv
├── README.md
└── figures/
```


Future Work
- Robust aggregation (Krum, Trimmed Mean)
- Adaptive attackers
- Representation-level reverse engineering
- Autonomous driving extension
- Real-time FL forensic monitoring

![Python](https://img.shields.io/badge/Python-3.10-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-red)
![CUDA](https://img.shields.io/badge/CUDA-11%2B-green)
![License](https://img.shields.io/badge/License-MIT-yellow)





