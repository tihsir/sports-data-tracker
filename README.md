# Comparison of Classical and Deep Learning-Based Multi-Object Tracking in Sports Video

Final project for CS543. Comparison of classical computer vision techniques versus modern deep learning methods for multi-object tracking (MOT) in sports. The primary goal is to evaluate and contrast the **tracking accuracy**, **computational cost**, and **speed** of these two pipelines. The initial goal is to track soccer players in videos captured from a fixed, side-view camera.

## Methodology

### Classical Method

* **Motion Segmentation:** `cv2.createBackgroundSubtractorMOG2()` is used to isolate moving objects from the static background
* **Object Detection:** Morphological operations (opening/closing) refine the segmentation masks, followed by `cv2.findContours()` to detect individual players
* **State Estimation:** A **Kalman Filter** predicts the motion and velocity of each tracked object into the next frame
* **Data Association:** The **Hungarian algorithm** matches predicted bounding boxes with new detections based on their Intersection over Union distance

<<<<<<< HEAD
### YOLOv11 + BoT-SORT Method
* **Object Detection:** Pre-trained **YOLOv11** model fine-tuned on soccer player images to detect players in each frame
* **State Estimation and Data Association:** **BoT-SORT** tracker combines Kalman filtering with appearance features extracted from a re-identification model to maintain consistent identities across frames

### SSD + DeepSORT Method
* **Object Detection:** Pre-trained **SSD (Single Shot MultiBox Detector)** model fine-tuned on soccer player images to detect players in each frame
* **State Estimation and Data Association:** **DeepSORT** tracker uses Kalman filtering along with appearance features from a CNN-based re-identification model to track players over time

=======
### Modern (Deep Learning) Method

* **Model:** **YOLOv11** pre-trained on the COCO dataset
* **Tracker:** **BoT-SORT**, a high-accuracy tracker integrated with the YOLOv11 framework
>>>>>>> 6643bd1 (repo structure and README based on proposal)

### Evaluation

* **Evaluation Metrics:** `motmetrics` library to calculate standard MOT benchmarks, including **MOTA** (Multi-Object Tracking Accuracy) and **MOTP** (Multi-Object Tracking Precision). We also measure computational cost and inference speed
<<<<<<< HEAD
* **Goal:** Successfully implement and evaluate both pipelines on at least 3 side-view soccer video video clips
=======
* **Minimum Goal:** Successfully implement and evaluate both pipelines on at least 3 side-view soccer video video clips
* **Maximum Goal:** Extend the analysis to other styles of soccer videos or other sports
>>>>>>> 6643bd1 (repo structure and README based on proposal)

## Repo Structure

* `data/`: Holds raw video clips and ground-truth annotations
* `notebooks/`: Jupyter notebooks containing our code
<<<<<<< HEAD
    - `classical.ipynb`: Classical computer vision-based MOT implementation
    - `yolov11_botsort.ipynb`: YOLOv11 + BoT-SORT deep learning-based MOT implementation
    - `ssd_deepsort.ipynb`: SSD + DeepSORT deep learning-based MOT implementation
    - `motmetrics_evaluation.ipynb`: Evaluation of tracking results for all methods using `motmetrics` library
* `results/`: Stores the generated output files, both videos and MOT challenge format text files
    - for classical method, results are in folders for each testing sequence and contain the output video and `.txt` file
    - for the deep learning methods, we store `mot_outputs/` and `videos/` in the respective folders
    - for all methods, we keep a `metrics.json` file summarizing runtime metrics (mix of manual and auto generation here)

## Dataset

The primary dataset is the **TeamTrack Dataset** from Kaggle: https://www.kaggle.com/datasets/atomscott/teamtrack/data. Data is available under the MIT License. 
=======
* `results/`: Stores the generated output files 

## Dataset

The primary dataset is the **TeamTrack Dataset** from Kaggle: https://www.kaggle.com/datasets/atomscott/teamtrack/data
>>>>>>> 6643bd1 (repo structure and README based on proposal)
