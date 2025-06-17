# MultiMedia_Offensive-_Content-Blurre
# UniFairNet
**A Multimodal Framework for Fair and Robust Meme Classification**

UniFairNet is a Python-based pipeline designed to detect hate, offensiveness, and harmful content in Internet memes by combining visual, textual, and contextual cues. It integrates state-of-the-art modules for OCR, scene-graph reasoning, bias mitigation, and multimodal fusion, and can optionally inpaint offensive imagery.

---

## Table of Contents
1. [Features](#features)  
2. [Architecture](#architecture)  
3. [Installation](#installation)  
4. [Data Preparation](#data-preparation)  
5. [Preprocessing](#preprocessing)  
6. [Training](#training)  
7. [Evaluation](#evaluation)  
8. [Usage](#usage)  
9. [Results](#results)  
10. [Contributing](#contributing)  
11. [License](#license)  
12. [Contact](#contact)  

---

## Features
- **OCR Text Extraction**  
  Uses PaddleOCR to reliably detect and transcribe text overlaid on memes.
- **Scene Graph Generation**  
  Builds an object–relation graph to capture fine-grained visual context.
- **Bias Mitigation**  
  Employs adversarial attention and contrastive learning to suppress identity-related biases.
- **Multimodal Fusion**  
  Aligns textual embeddings (BERT or CLIP-based) with visual features (CLIP/BLIP) via cross-attention.
- **Optional Inpainting**  
  Automatically conceals harmful imagery by inpainting classified “harmful” regions.
- **Modular & Extensible**  
  Easily swap in new encoders, debiasing strategies, or post-processing blocks.

---

## Architecture

```text
           +------------+
           |  Input     |
           |  Meme      |
           +------------+
                 │
     ┌───────────┼───────────┐
     │           │           │
 OCR/Text   Scene-Graph   Image
Extraction   Generation   Patches
     │           │           │
     │           └───┐       │
     │               │       │
     │        Visual Encoder │
     │               │       │
     │        ┌──────┼───────┘
     └─────┐  │      │
           │  ▼      ▼
      Text Encoder   Bias Attn.
           │          │
           └───┐      │
               ▼      │
         Cross-Modal Fusion
               │
        Classification Head
               │
    ┌──────────┴──────────┐
    │                     │
  Label               (Optional)
  Hateful/           Inpainting
  Offensive 
