# Pixel‑Based Deep Reinforcement Learning for **Flappy Bird** <img src="https://img.shields.io/badge/rl-QR--DQN-blue"> <img src="https://img.shields.io/badge/license-MIT-green">

> **One tiny Inception block → +135 % average score**

Train a Flappy Bird agent **directly from raw pixels** with [QR‑DQN](https://arxiv.org/abs/1710.10044).
Two CNN back‑bones, Colab‑one‑click, and GPU‑friendly code—because flapping shouldn’t be a hassle.

---

## Table of Contents

1. [Features](#features)
2. [Demo](#demo)
3. [Quick Start](#quick-start)
4. [Repository Layout](#repository-layout)
5. [Hyper‑parameters](#hyper-parameters)
6. [Results](#results)
7. [License](#license)
8. [Citing & Thanks](#citing--thanks)

---

## Features

* **Pixel‑only input** – zero hand‑engineered signals.
* **Distributional QR‑DQN** – robust value estimates.
* **Swappable CNNs** – Atari baseline vs Inception upgrade.
* **One‑command Colab** – GPU training & MP4 demo in minutes.
* Clean, modular Python package—drop it into your own RL projects.

---

## Demo

<p align="center">
  <img src="docs/demo.gif" alt="Demo GIF" width="600">
</p>

---

## Quick Start

### ▶️ Run in Colab

Hit the **“Run in Colab”** badge in the notebook. It installs deps, trains, and plays a demo video—done.

### 🖥️ Run Locally

```bash
git clone https://github.com/<your-user>/flappy-pixel-drl.git
cd flappy-pixel-drl

# (Optional) isolate packages
python -m venv .venv && source .venv/bin/activate

pip install -r requirements.txt        # ships with PyTorch‑cu11 wheels

# Train Inception model for 2 M steps
python train.py --model inception --steps 2_000_000

# Evaluate the trained checkpoint
python evaluate.py checkpoints/inception_2M.zip
```

---

## Repository Layout

```
.
├─ flappy/                 # game + Gym wrapper
│  ├─ core.py              # Flappy physics
│  ├─ env_pixel.py         # FlappyPixelEnv (Gym API)
│  └─ extractor.py         # Atari & Inception CNNs
├─ train.py                # CLI trainer
├─ evaluate.py             # CLI evaluator
├─ play.py                 # records MP4 demo
├─ notebook.ipynb          # tutorial / slides
├─ requirements.txt
└─ checkpoints/
   ├─ atari_qrdqn.zip
   └─ inception_qrdqn.zip
```

---

## Hyper‑parameters

| Group                 | Value          | Why                                      |
| --------------------- | -------------- | ---------------------------------------- |
| Replay buffer / batch | 50 k / 32      | Fits a 16 GB GPU, mirrors Atari configs  |
| Learning rate         | 5 × 10⁻⁴       | Stable sweet‑spot for QR‑DQN             |
| Target‑net update     | 1 k steps      | Keeps learning steady, avoids divergence |
| ε‑schedule            | 1 → 0.1 (15 %) | Heavy exploration early when it matters  |
| Reward shaping        | +0.2 / frame   | Survival bonus fights sparse rewards     |

Full table lives in `docs/hparams.md`.

---

## Results – 2 M steps on a single A100

| Backbone      | Avg pipes ↑ | Best pipes | Avg frames ↑ |     TTFP ↓ |
| ------------- | ----------: | ---------: | -----------: | ---------: |
| Atari CNN     |         5.6 |         22 |          299 |     1.30 M |
| **Inception** |    **13.2** |     **61** |      **606** | **0.78 M** |

*TTFP = frames until clearing the first pipe.*

TensorBoard logs are in `tb/`.

---

## License

MIT © 2025 \<Your Name / University>

---

## Citing & Thanks

If this repo flaps its way into your research, please cite:

```bibtex
@misc{flappy_pixel_drl_2025,
  author       = {<Your Name>},
  title        = {Pixel-Based Deep Reinforcement Learning for Flappy Bird},
  year         = {2025},
  howpublished = {\url{https://github.com/<your-user>/flappy-pixel-drl}}
}
```

Inspired by the Atari Zoo and DeepMind Control Suite work.
Happy flapping! 🐦
