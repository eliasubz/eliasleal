---
layout: post
title: "Recreating 4DFlowNet"
date: 2026-06-20
description: "A small reproduction of 4D flow MRI super-resolution with synthetic velocity fields."
---

This post will 1. Analyze the approach from 2020 and 2. Recreate the paper and results in a minimal setup.

The simple goal of this paper is to improve the MRI imaging resolution of the bloodflow, especially for patients with abnormal flows, by increasing imaging time.
Because datasets from imaging from real patients and they created high-quality simulations of the **thoracic aorta** using computational fluid dynamics (CFD) and sampled low-grade 16x16x16 patches. Fun Fact: They use blender to modify the 3D models and create more datasamples. The output of the 4DFlowNet is then a 2x upsampled (32x32x32) velocity field of the bloodflows, which achieved a relative errorr of 0.6-3.8%.

This paper was not the first to adopt image super resolution using deep learning methods in the medical domain, but it was the first paper to work with velocity fields and 4D flow MRI representations.

**The Network architecture** is based on a the generator of the super-resolution residual network (ResNet) paper [[2]](https://arxiv.org/abs/1609.04802). The input has one path for the raw noisy velocity maps (16^3) and one that accepts calculated context: Magnitude, Velocities and PC-MRA (=Mag*Speed). Both of them pass through two convolutional maps and are then concatenated, after which they are passed through 8 residual blocks (RB). Each RB consist of two conv layer with a nonlinear layer inbetween and a skip-connection after which another Leaky ReLU is used. After the 8 RB-layers we have 64 sematincally rich feature maps that are upsampled using a simple bilinear resize, after which we pass them through 4 more RBs and pass it through three two-layer convolutional heads that convolve the 64 channels back into 1 for the xyz-compontents of the velocities.

![4DFlowNet architecture]({{ '/assets/img/4dflownet_architecture.webp' | relative_url }})

**The loss function** consist of a simple mean-squared error (MSE) loss, compares the upsampled velocity components with their ground-truth, added with a velocity gradient (VG) term. While the MSE loss is used to vector maginude error it can lead to blurry images by missing high-frequency spatial velocity shifts, which leads to poor performance close to the vessel walls. The VG loss counter-acts that by rewarding accurate directional derivatives between adjacent velocity vectors.

$$L_{total} = l_{MSE} + 10^{-3} \cdot l_{VG}$$

**Generating accurate 4D MRI images** needed much more than just down-sampling the mesh from a perfect CFD simulation. In order to model the *Rayleigh noise* that MRI images are subject to, the researchers added noise in the frequency domain using fast fourier transform. Specifically, they did that by calculating the complex numbers from the phase and magnitude images, converting the complex numbers into frequency domain (k-space) and truncating the high-frequency information along all three axes. In addition, they added some white noise to the frequencies and converted them back to the spatial domain.

## Paper Results

In the recreation, the learned model is compared against trilinear interpolation. The important part is not only whether the voxel-wise MAE goes down, but whether peak velocity and flow-rate errors improve as well.

![A100 final metrics]({{ '/assets/img/a100_quick_final_metrics.png' | relative_url }})

The training curves show that MAE improves quickly, while peak velocity and flow-rate errors are noisier. This is expected: preserving hemodynamic quantities is not identical to minimizing voxel-wise reconstruction error.

![A100 training curves]({{ '/assets/img/a100_quick_training_curves.png' | relative_url }})

The cleaned experiment CSV is available here: [a100_quick_summary_clean.csv]({{ '/assets/data/a100_quick_summary_clean.csv' | relative_url }}).
