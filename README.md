# Comparison of Classical and Deep Learning-Based Multi-Object Tracking in Sports Video

Final project for CS543. Comparison of classical computer vision techniques versus modern deep learning methods for multi-object tracking (MOT) in sports. The primary goal is to evaluate and contrast the **tracking accuracy**, **computational cost**, and **speed** of these two pipelines. The initial goal is to track soccer players in videos captured from a fixed, side-view camera.

## Methodology

### Classical Method

* **Motion Segmentation:** `cv2.createBackgroundSubtractorMOG2()` is used to isolate moving objects from the static background
* **Object Detection:** Morphological operations (opening/closing) refine the segmentation masks, followed by `cv2.findContours()` to detect individual players
* **State Estimation:** A **Kalman Filter** predicts the motion and velocity of each tracked object into the next frame
* **Data Association:** The **Hungarian algorithm** matches predicted bounding boxes with new detections based on their Intersection over Union distance

### YOLOv11 + BoT-SORT Method
* **Object Detection:** Pre-trained **YOLOv11** model fine-tuned on soccer player images to detect players in each frame
* **State Estimation and Data Association:** **BoT-SORT** tracker combines Kalman filtering with appearance features extracted from a re-identification model to maintain consistent identities across frames

### YOLOv11 + DeepSORT Method
* **Object Detection:** Same as above, using **YOLOv11**
* **State Estimation and Data Association:** **DeepSORT** tracker uses Kalman filtering and a deep appearance descriptor to track players over time

### Evaluation

* **Evaluation Metrics:** `motmetrics` library to calculate standard MOT benchmarks, including **MOTA** (Multi-Object Tracking Accuracy) and **MOTP** (Multi-Object Tracking Precision). We also measure computational cost and inference speed
* **Goal:** Successfully implement and evaluate both pipelines on at least 3 side-view soccer video video clips

## Repo Structure

* `data/`: Holds raw video clips and ground-truth annotations
* `notebooks/`: Jupyter notebooks containing our code
    - `classical.ipynb`: Classical computer vision-based MOT implementation
    - `yolov11_botsort.ipynb`: YOLOv11 + BoT-SORT deep learning-based MOT implementation
    - `yolov11_deepsort.ipynb`: YOLOv11 + DeepSORT deep learning-based MOT implementation
    - `motmetrics_evaluation.ipynb`: Evaluation of tracking results for all methods using `motmetrics` library
* `results/`: Stores the generated output files, both videos and MOT challenge format text files
    - for classical method, results are in folders for each testing sequence and contain the output video and `.txt` file
    - for the deep learning methods, we store `mot_outputs/` and `videos/` in the respective folders
    - for all methods, we keep a `metrics.json` file summarizing runtime metrics
    
## Dataset

The primary dataset is the **TeamTrack Dataset** from Kaggle: https://www.kaggle.com/datasets/atomscott/teamtrack/data. Data is available under the MIT License. 
