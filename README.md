# Hypergraph Contrastive Sensor Fusion for Multimodal Fault Diagnosis in Induction Motors

[![IEEE Sensors Journal](https://img.shields.io/badge/IEEE%20Sensors%20Journal-2026-00629B.svg)](https://arxiv.org/abs/2510.15547)
[![arXiv](https://img.shields.io/badge/arXiv-2510.15547-b31b1b.svg)](https://arxiv.org/abs/2510.15547)
[![PDF](https://img.shields.io/badge/Paper-PDF-blue.svg)](https://arxiv.org/pdf/2510.15547)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Official PyTorch implementation of **MM-HCAN** (Multimodal Hypergraph Contrastive Attention Network), from the IEEE Sensors Journal paper
[*Hypergraph Contrastive Sensor Fusion for Multimodal Fault Diagnosis in Induction Motors*](https://arxiv.org/abs/2510.15547).

> ### ✨ Authors
> 
> • [**Usman Ali**](https://scholar.google.com/citations?user=2A32xVQAAAAJ&hl=en) • [**Ali Zia**](https://ali-zia.me/) • [**Waqas Ali**](https://scholar.google.com/citations?user=J8_Ko78AAAAJ&hl=en) • [**Umer Ramzan**](https://scholar.google.com/citations?user=D3AhoccAAAAJ&hl=en) • [**Abdul Rehman**](https://scholar.google.com/citations?user=ZTuS-yUAAAAJ&hl=en) • [**Muhammad Tayyab Chaudhry**](https://scholar.google.com/citations?user=-mECuFEAAAAJ&hl=en) • [**Wei Xiang**](https://scholar.google.com/citations?user=VxQUr90AAAAJ&hl=en)

## 🧠 Overview

Reliable induction motor (IM) fault diagnosis is vital for industrial safety and operational continuity, mitigating costly unplanned downtime. Conventional approaches often struggle to capture complex multimodal signal relationships, are constrained to unimodal data or single fault types, and exhibit performance degradation under noisy or cross-domain conditions. This paper proposes the Multimodal Hypergraph Contrastive Attention Network (MM-HCAN), a unified framework for robust fault diagnosis. To the best of our knowledge, MM-HCAN is the first to integrate contrastive learning within a hypergraph topology specifically designed for multimodal sensor fusion, enabling the joint modelling of intra- and inter-modal dependencies and enhancing generalisation beyond Euclidean embedding spaces. The model facilitates simultaneous diagnosis of bearing, stator, and rotor faults, addressing the engineering need for consolidated diagnostic capabilities. Evaluated on three real-world benchmarks, MM-HCAN achieves up to 99.82% accuracy with strong cross-domain generalisation and resilience to noise, demonstrating its suitability for real-world deployment. An ablation study validates the contribution of each component. MM-HCAN provides a scalable and robust solution for comprehensive multi-fault diagnosis, supporting predictive maintenance and extended asset longevity in industrial environments.

---

## 🏗️ Architecture Overview

Below is the overall architecture of **MM-HCAN**:

![MM-HCAN Architecture](fig/arch.png)

---

## ⚙️ System Specifications

- **OS:** Ubuntu 22.04  
- **GPU:** NVIDIA RTX 4080  
- **Python:** 3.10  
- **Torch:** 2.7.1  

---

## 🧩 Environment Setup

Create and activate the environment:
```bash
conda create --name MMHCAN --file requirements.txt
conda activate MMHCAN
```

---

## 📊 Data Layout

The data loaders expect a `Dataset/` folder in the repository root, with one sub-folder per class for each modality:

```
Dataset/
├── temporal_features/
│   ├── Healthy/output1.csv
│   └── <FaultClass>/output1.csv
└── spectral_features/
    ├── Healthy/*.png
    └── <FaultClass>/*.png
```

## 🚀 Usage

```bash
# 1. Pre-train the temporal and spectral feature extractors
python -m utils.train_extractors      # saves best_temporal.pth and best_spectral.pth

# 2. Place the extractor weights where the pipeline expects them
mkdir -p checkpoints
mv best_temporal.pth checkpoints/temporal.pth
mv best_spectral.pth checkpoints/spectral.pth

# 3. Train MM-HCAN (hypergraph + contrastive fusion)
python main.py

# 4. Evaluate the best validation model on the test split
python eval.py
```

---

## 📖 Citation

If you find this code useful, please cite:

```bibtex
@article{ali2026mmhcan,
  title   = {Hypergraph Contrastive Sensor Fusion for Multimodal Fault Diagnosis in Induction Motors},
  author  = {Ali, Usman and Zia, Ali and Ali, Waqas and Ramzan, Umer and Rehman, Abdul and Chaudhry, Muhammad Tayyab and Xiang, Wei},
  journal = {IEEE Sensors Journal},
  year    = {2026},
  note    = {arXiv:2510.15547}
}
```

## 📄 License

Released under the [MIT License](LICENSE).
