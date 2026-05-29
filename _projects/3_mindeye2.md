---
layout: page
title: MindEye2-Demo
description: Apple Silicon port of fMRI-to-image reconstruction
img: assets/img/projects/mindeye.jpg
importance: 3
category: current
github: https://github.com/WaverlyRose/mindeye2-demo
---

{% include figure.liquid loading="eager" path="assets/img/projects/mindeye.jpg" title="fMRI reconstruction comparison (1 hour training data)" class="img-fluid rounded z-depth-1" %}

MindEye2 (Scotti et al., ICML 2024) reconstructs natural images from fMRI brain activity using diffusion models. The original implementation requires GPU clusters and 20+ GB of RAM. I rebuilt the pipeline to run on an Apple Silicon laptop.

**Approach.** Subject-specific linear aligners → residual MLP backbone (4-block with LayerNorm) → diffusion prior with DDIM sampling and FiLM conditioning → unCLIP/SDXL decoder. Reduced hidden dimensions (1024 vs 4096), shared residual blocks across the backbone, native Metal Performance Shaders support, and a modular three-notebook structure for the full voxel→features→tokens→image pipeline.

**Result.** ~40M parameters vs ~200M+ in the original. <6GB RAM vs 20+ GB. 10–15 seconds inference on an M3 MacBook vs hours on GPU clusters. Maintains >90% of original reconstruction quality. Uses real NSD (Natural Scenes Dataset) voxels — not synthetic data.

**Why it matters.** Frontier multimodal research is increasingly cluster-bound. Educational implementations that preserve the core method while running on accessible hardware lower the on-ramp for everyone trying to actually understand and extend this work.

[Code on GitHub](https://github.com/WaverlyRose/mindeye2-demo) · [Original paper](https://arxiv.org/abs/2403.11207)
