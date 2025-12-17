# ImgGeneration
This repository explores generative modeling using DCGANs, Progressive GANs, and Denoising Diffusion Probabilistic Models (DDPMs). Experiments include training on synthetic geometric datasets and real-world animal image datasets, analyzing training stability, latent space interpolation, and visual quality.
# GANs vs Diffusion Models: A Comparative Study

This repository contains experiments comparing **DCGAN**, **Progressive GAN**, and **Denoising Diffusion Probabilistic Models (DDPM)** for image generation. The goal of this project is not to achieve state-of-the-art image synthesis, but to empirically study training behavior, stability, loss dynamics, and perceptual quality across different generative paradigms.

The experiments were conducted as part of a graduate-level deep learning assignment and emphasize hands-on exploration, dataset scaling, and architectural trade-offs.

---

## Overview of Experiments

The project is divided into three major experimental phases:

### 1. DCGAN on Synthetic Colored Squares
A custom dataset of **64×64 RGB images** was generated, consisting of colored squares on black backgrounds with varying:
- Colors
- Sizes
- Orientations

Initial experiments with **1,000 images** failed to produce meaningful structure, as evidenced by rapidly increasing generator loss and mode collapse. The dataset size was gradually increased in increments of 10,000 images. Only after reaching **80,000 samples** did the DCGAN begin to consistently generate square-like structures, highlighting the strong data dependency of adversarial training.

---

### 2. GANs on Real-World Animal Images
A real-world image dataset was constructed using the **Kaggle Panda Image Dataset**. Since the dataset originally contained only 144 images, data augmentation was applied (horizontal flips and rotations) to expand it to **5,000 samples**, and later to **25,000 samples**.

Two GAN architectures were trained and compared:
- **DCGAN**
- **Progressive GAN**

Multiple architectural and training variations were explored, including:
- Increasing latent vector dimensionality (`nz`)
- Training for longer durations
- Adjusting learning rates
- Modifying feature map sizes

The DCGAN achieved its best performance with a larger latent space (`nz = 500`), while the Progressive GAN demonstrated better generator–discriminator balance at intermediate resolutions (e.g., 16×16). However, Progressive GANs showed instability as resolution increased.

---

### 3. Latent Space Interpolation
Latent space interpolation was performed using the best-performing GAN configuration. Smooth semantic transitions between generated samples were observed, particularly for the Progressive GAN at lower resolutions, indicating a well-structured latent space at those stages.

---

### 4. Diffusion Model (DDPM)
An unconditional **DDPM** was implemented using a **U-Net backbone**, adapted for **64×64 RGB images**. The diffusion model was trained in two stages:
- Short training (5 epochs)
- Extended training (15 epochs forward diffusion, 50 epochs reverse diffusion)

The DDPM exhibited:
- Significantly more stable training compared to GANs
- Lower numerical loss values
- Clear forward (noising) and reverse (denoising) trajectories

However, despite lower losses, the visual quality of DDPM-generated images lagged behind GAN outputs for this dataset size and model capacity.

---

## Key Observations

- **GANs** produce sharper and more visually appealing images, even when loss values are unstable.
- **Diffusion models** are easier to train and more stable but require larger datasets and higher-capacity networks to match GAN-level perceptual quality.
- Adversarial losses align better with human perception than pixel-wise diffusion objectives.
- Dataset size plays a critical role in GAN performance, especially for structured image generation.

---

## References

- Radford et al., *Unsupervised Representation Learning with Deep Convolutional GANs*
- Karras et al., *Progressive Growing of GANs for Improved Quality, Stability, and Variation*
- Ho et al., *Denoising Diffusion Probabilistic Models*
- PyTorch DCGAN Tutorial

---

## Notes

This repository reflects exploratory experimentation rather than optimized production models. The focus is on understanding generative learning dynamics, failure modes, and architectural trade-offs through empirical analysis.



