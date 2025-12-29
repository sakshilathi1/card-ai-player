# 🃏 AI-Powered Card Game Player

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![YOLOv11](https://img.shields.io/badge/YOLO-v11-green.svg)
![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)

**An intelligent AI system that plays the card game "Judgement" against human opponents in real-time using Computer Vision and Large Language Models.**

[Features](#-features) • [Architecture](#-architecture) • [Installation](#-installation) • [Usage](#-usage) • [Results](#-results)

</div>

---

## 📖 Overview

This project presents a novel approach to AI-powered card gaming that combines **YOLOv11 computer vision** for real-time card detection with **Large Language Models (LLMs)** for strategic decision-making. Unlike traditional reinforcement learning approaches that require extensive training data and computational resources, our system achieves competitive performance through direct perception and strategic reasoning.

The AI successfully competed against human players, winning **52% of games** (26/50) while demonstrating adaptive strategy and real-time responsiveness.

## ✨ Features

- **Real-Time Card Recognition**: YOLOv11-powered detection with 98.5% accuracy across all 52 playing cards
- **Strategic AI Decision Engine**: LLM-based reasoning for bid prediction and optimal card play
- **Live Camera Integration**: Seamless webcam interface for physical card game interaction
- **Human-Like Gameplay**: Natural decision-making that adapts to opponent strategies
- **85% Move Prediction Accuracy**: Anticipates opponent plays for strategic advantage
- **No Reinforcement Learning Required**: Simplified training process with immediate deployment capability

## 🎮 The Game: Judgement

Judgement is a trick-taking card game that requires strategic thinking and prediction skills:

1. **Setup**: Played with a standard 52-card deck over multiple rounds with decreasing card counts
2. **Bidding Phase**: Players predict the exact number of tricks they'll win
3. **Playing Phase**: Cards are played following lead suit rules, with trump cards adding strategic depth
4. **Scoring**: Points awarded for accurate predictions; penalties for over/under-estimating

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      MAIN THREAD                            │
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   CAMERA    │───▶│  YOLO MODEL │───▶│  LLM MODEL  │     │
│  │  (camera.py)│    │  (eyes.py)  │    │  (brain.py) │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                  │                  │             │
│         ▼                  ▼                  ▼             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   DISPLAY   │◀───│ GAME LOGIC  │◀───│  STRATEGY   │     │
│  │  (Renderer) │    │  (main.py)  │    │  DECISIONS  │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Component Overview

| Component | File | Description |
|-----------|------|-------------|
| **Vision System** | `eyes.py` | YOLOv11 card detection and classification |
| **Strategic Engine** | `brain.py` | LLM-powered decision making and bid prediction |
| **Camera Interface** | `camera.py` | Real-time video capture and frame processing |
| **Game Controller** | `main.py` | Game flow management, scoring, and turn coordination |
| **Model Weights** | `weights/` | Pre-trained YOLOv11 model for card recognition |

## 📊 Dataset

The computer vision model was trained on a comprehensive playing card dataset:

| Attribute | Value |
|-----------|-------|
| **Total Images** | 75,000 |
| **Training Split** | 20% (15,000 images) |
| **Testing Split** | 40% (30,000 images) |
| **Validation Split** | 40% (30,000 images) |
| **Classes** | 52 (all standard playing cards) |
| **Suits** | 4 (Hearts, Diamonds, Clubs, Spades) |

## 📈 Results

### Performance Metrics

| Metric | Value |
|--------|-------|
| Card Recognition Accuracy | **98.5%** |
| Opponent Move Prediction | **85%** |
| Win Rate vs Humans | **52%** (26/50 games) |
| mAP@0.5 | **0.993** |
| F1 Score (at 0.470 confidence) | **0.99** |

### Training Curves

The model demonstrates strong convergence with:
- Box loss reduction from 1.0 to ~0.5
- Classification loss reduction from 2.0 to ~0.3
- Precision reaching 0.98
- Recall reaching 0.99

## 🚀 Installation

### Prerequisites

- Python 3.8+
- Webcam for real-time card detection
- CUDA-compatible GPU (recommended for real-time inference)

### Setup

```bash
# Clone the repository
git clone https://github.com/sakshilathi1/card-ai-player.git
cd card-ai-player

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Dependencies

```
ultralytics>=8.0.0
opencv-python>=4.8.0
numpy>=1.24.0
openai>=1.0.0  # or your preferred LLM API
torch>=2.0.0
```

## 💻 Usage

### Running the Game

```bash
python main.py
```

### Configuration Options

```python
# In main.py, configure:
CAMERA_INDEX = 0          # Webcam device index
CONFIDENCE_THRESHOLD = 0.7 # Detection confidence
LLM_MODEL = "gpt-4"       # LLM for strategic decisions
```

### Game Flow

1. **Start**: Launch the application and position your webcam over the playing area
2. **Deal**: Physical cards are dealt to players
3. **Bid**: AI analyzes its hand and makes a bid prediction
4. **Play**: AI detects played cards and responds strategically
5. **Score**: Points are calculated based on bid accuracy

## 📁 Project Structure

```
card-ai-player/
├── main.py              # Main game controller
├── brain.py             # LLM strategic decision engine
├── eyes.py              # YOLO vision system
├── camera.py            # Camera capture interface
├── rough.py             # Development/testing utilities
├── weights/             # Pre-trained model weights
│   └── best.pt          # YOLOv11 trained weights
├── yolo_training/       # Training scripts and configs
├── requirements.txt
└── README.md
```

## 🔮 Future Scope

### Expansion to Other Games
- Adaptation for Poker, Bridge, and Magic: The Gathering
- Generalization across different card game rule systems
- Support for collectible card games with complex interactions

### Robotics Integration
- Physical card manipulation capabilities
- Robotic arm integration for autonomous play
- Fully automated gaming environments for casinos/arcades

## ⚠️ Limitations

1. **Exploration vs Exploitation**: The AI tends to favor proven strategies over exploring new approaches
2. **Computational Requirements**: Real-time LLM inference requires significant resources
3. **Game Specificity**: Currently optimized specifically for Judgement rules

## 📚 References

1. Zha, D., et al. (2021). DouZero: Mastering DouDizhu with self-play deep reinforcement learning. *ICML 2021*
2. Sharma, N., et al. (2021). Machine learning and deep learning applications—A vision. *Global Transitions Proceedings*
3. Gallotta, R., et al. (2024). Large Language Models and Games: A Survey and Roadmap
4. Hu, Z., et al. (2023). Deep learning applications in games: A survey from a data perspective. *Applied Intelligence*


---

<div align="center">

**⭐ Star this repo if you find it useful!**

Made with ❤️ for the intersection of AI and Gaming

</div>
