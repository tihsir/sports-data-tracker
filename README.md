# Comparison of Classical and Deep Learning-Based Multi-Object Tracking in Sports Video

Final project for CS543. Comparison of classical computer vision techniques versus modern deep learning methods for multi-object tracking (MOT) in sports. The primary goal is to evaluate and contrast the **tracking accuracy**, **computational cost**, and **speed** of these two pipelines. The initial goal is to track soccer players in videos captured from a fixed, side-view camera.

## Methodology

### Classical Method

* **Motion Segmentation:** `cv2.createBackgroundSubtractorMOG2()` is used to isolate moving objects from the static background
* **Object Detection:** Morphological operations (opening/closing) refine the segmentation masks, followed by `cv2.findContours()` to detect individual players
* **State Estimation:** A **Kalman Filter** predicts the motion and velocity of each tracked object into the next frame
* **Data Association:** The **Hungarian algorithm** matches predicted bounding boxes with new detections based on their Intersection over Union distance

### Modern (Deep Learning) Method

* **Model:** **YOLOv11** pre-trained on the COCO dataset
* **Tracker:** **BoT-SORT**, a high-accuracy tracker integrated with the YOLOv11 framework

### Evaluation

* **Evaluation Metrics:** `motmetrics` library to calculate standard MOT benchmarks, including **MOTA** (Multi-Object Tracking Accuracy) and **MOTP** (Multi-Object Tracking Precision). We also measure computational cost and inference speed
* **Minimum Goal:** Successfully implement and evaluate both pipelines on at least 3 side-view soccer video video clips
* **Maximum Goal:** Extend the analysis to other styles of soccer videos or other sports

## Repo Structure

* `data/`: Holds raw video clips and ground-truth annotations
* `notebooks/`: Jupyter notebooks containing our code
* `results/`: Stores the generated output files 

## Dataset

The primary dataset is the **TeamTrack Dataset** from Kaggle: https://www.kaggle.com/datasets/atomscott/teamtrack/data