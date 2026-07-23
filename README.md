# ship-detection-yolo-thesis

# Ship Detection in Drone Imagery using YOLO Series Algorithms
# Ship Detection in Drone Imagery using YOLO Series Algorithms

This repository contains the official implementation and comparative analysis of various YOLO architectures (v8m, v10m, 11m, and 26m) for ship detection, as part of my Master's thesis at the University of Qom.

## 📌 Project Overview
- **Dataset:** SeaShips (7,000 images, 6 classes: Ore Carrier, Bulk Cargo Ship, General Cargo Ship, Container Ship, Fishing Boat, and Passenger Ship).
- **Focus:** Evaluation of detection stability and accuracy in maritime environments using drone-proxy perspectives.
- **Key Contribution:** Comparative performance analysis across four generations of YOLO models.

## 🚀 Model Performances (Final Results)
The models were evaluated using a 70/20/10 split. The following table summarizes the performance on the Test set:

| Model    | mAP@50-95 | Recall | Precision | Params (M) |
|----------|-----------|--------|-----------|------------|
| YOLOv8m  | 0.7963    | 0.9576 | **0.9856**| 25.9       |
| YOLOv10m | 0.8035    | 0.9598 | 0.9782    | **15.4**   |
| **YOLO11m** | **0.8101** | **0.9792** | 0.9754 | 20.1       |
| YOLO26m  | 0.7940    | 0.9412 | 0.9688    | 26.2       |

*All evaluations were performed with `seed=42` and a fixed checkpoint to ensure statistical stability ($\sigma=0.0000$).*

## 🛠️ Installation & Environment
- **OS:** Linux
- **Python:** 3.12.9
- **Hardware:** NVIDIA RTX 3080 Ti (12GB VRAM)
- **Frameworks:** 
  - `ultralytics==8.4.92`
  - `torch==2.6.0+cu126`
  - `albumentations==2.0.8`

### Setup
```bash
pip install -r requirements.txt



@mastersthesis{Foroutan2025ShipDetection,
  author = {Mahnaz Foroutan},
  title  = {Ship Detection Using Drones with YOLO-Series Algorithms},
  school = {University of Qom},
  year   = {2025},
}










