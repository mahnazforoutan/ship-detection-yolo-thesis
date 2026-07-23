# ship-detection-yolo-thesis

# Comparative Analysis of YOLO Architectures for Ship Detection on SeaShips Dataset

An academic and empirical evaluation of modern YOLO variants (YOLOv8m, YOLOv10m, YOLO11m, and YOLO26m) for marine vehicle detection, utilizing the **SeaShips** dataset. This repository contains the official implementation, training pipelines, and evaluation metrics used in the Master's thesis.

---

## 📌 Project Overview
Ship detection is a critical task in maritime surveillance, autonomous navigation, and port management. This project provides a rigorous, comparative performance analysis of four state-of-the-art object detection models. 

### Key Features
*   **Models Evaluated:** YOLOv8m, YOLOv10m, YOLO11m, YOLO26m.
*   **Dataset:** SeaShips (7,000 precisely annotated images, 6 distinct ship classes).
*   **Evaluation Methodology:** Systematic 5-Fold cross-validation (utilizing a fixed 70/20/10 split for training, validation, and testing).
*   **Key Metrics:** mAP50-95, Precision, Recall, F1-Score, Inference Speed (ms), and Parameter/GFLOP footprint (Pareto Frontier Analysis).

---

## 📊 Experimental Setup & Hardware
*   **Operating System:** Linux
*   **Language & Runtime:** Python 3.12.9
*   **Deep Learning Frameworks:** PyTorch 2.6.0+cu126, Ultralytics 8.4.92
*   **Augmentation Library:** Albumentations 2.0.8
*   **GPU Hardware:** NVIDIA GeForce RTX 3080 Ti (12GB VRAM)
*   **Host System:** 64GB RAM

---

## 📁 Repository Structure
```text
├── data/
│   └── SeaShips/               # Dataset directory (Excluded via .gitignore)
├── src/
│   ├── dataloader.py           # Custom data loading & Albumentations pipeline
│   ├── train.py                # Model training script (5-Fold setup)
│   ├── evaluate.py             # Inference & metric evaluation
│   └── utils.py                # Pareto frontier plotting & helper functions
├── configs/
│   └── hyperparams.yaml        # Training hyperparameters (seed=42)
├── README.md
└── .gitignore

1. Clone the Repository
git clone https://github.com/mahnazforoutan/ship-detection-yolo-thesis.git
cd ship-detection-yolo

2. Set Up Environment
python3.12 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

3. Running the Training & Evaluation
python src/train.py --model yolo11m   --seed 42


📈 Performance Summary
Below is a consolidated summary of the empirical results obtained across the final model checkpoints:

Model	Parameters (M)	GFLOPs	mAP50-95	Precision	Recall	F1-Score	Inference Time (ms)
YOLOv8m	25.90	     79.10   	0.8012	  0.9856	   0.9610 	0.9731   	8.40
YOLOv10m	15.40    	59.10	   0.7995	  0.9780   	0.9598	 0.9688   	6.20
YOLO11m	20.10	     68.00   	0.8101  	0.9810   	0.9680 	0.9745   	7.10
YOLO26m	20.35	     67.90   	0.7940	  0.9760   	0.9640	 0.9700	   7.30

@mastersthesis{Foroutan2025ShipDetection,
  author = {Mahnaz Foroutan},
  title  = {Ship Detection Using Drones with YOLO-Series Algorithms},
  school = {University of Qom},
  year   = {2025},
}










