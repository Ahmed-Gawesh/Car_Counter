# Vehicle Counting System with YOLOv12 and SORT Tracking
Overview
This project implements a real-time vehicle counting system using the YOLOv12 object detection model and the SORT (Simple Online and Realtime Tracking) algorithm. It processes a video file (cars.mp4) to detect and track vehicles (cars, motorbikes, buses, and trucks), counting them as they cross a predefined line in the video frame. A mask (mask.png) is applied to focus detection on a specific region of interest.
Features

Real-time vehicle detection using YOLOv12.
Object tracking with the SORT algorithm to assign unique IDs to vehicles.
Counts vehicles crossing a user-defined line in the video.
Region of interest (ROI) masking to focus detection on specific areas.
Visualizes bounding boxes, tracking IDs, and vehicle counts.
Configurable detection threshold and tracking parameters.

# Requirements

Python 3.8+
OpenCV (opencv-python)
Ultralytics YOLO (ultralytics)
cvzone
numpy
sort (SORT tracking library)
math

# Installation

Install dependencies:
pip install opencv-python ultralytics cvzone numpy


Install the SORT tracking library:
pip install sort


Download the YOLOv12 weights (weights_yolo12n.pt) and place them in the project directory. Weights can be obtained from the Ultralytics YOLO repository.

Ensure the input video file (cars.mp4) and mask image (mask.png) are in the project directory.


# Usage

Place the cars.mp4 video file and mask.png in the project directory.
Run the script:python vehicle_counting.py


The script will display a window showing the video feed with:
Bounding boxes around detected vehicles.
Tracking IDs and vehicle class names.
A red line indicating the counting zone (turns green when a vehicle is counted).
A counter displaying the total number of vehicles counted.



Input Files

Video File: cars.mp4 (replace with your own video file if needed).
Mask Image: mask.png (a binary mask to define the region of interest).
YOLO Weights: weights_yolo12n.pt (pre-trained YOLOv12 model weights).

Controls

Press any key to exit the video feed window.

# Code Explanation

Video Capture: Loads the video file (cars.mp4) using OpenCV.
Masking: Applies a binary mask (mask.png) to focus detection on a specific region using cv2.bitwise_and.
YOLO Model: Uses YOLOv12 to detect objects in the masked region.
Object Filtering: Only processes vehicles (car, motorbike, bus, truck) with a confidence score above 0.3.
SORT Tracking: Tracks detected vehicles, assigning unique IDs using the SORT algorithm (max_age=20, min_hits=3, iou_threshold=0.3).
Counting Logic: Counts vehicles when their center point crosses a predefined line (limits=[400, 297, 673, 297]).
Visualization:
Draws bounding boxes with cvzone.cornerRect.
Displays class names and tracking IDs with cvzone.putTextRect.
Shows a counting line and the total vehicle count in the top-left corner.



# Configuration

Video Input: Replace cars.mp4 with your video file or modify the code to use a webcam (cv2.VideoCapture(0)).
Mask: Ensure mask.png matches the video resolution and highlights the region of interest in white.
Counting Line: Adjust limits=[x1, y1, x2, y2] to change the position of the counting line.
Tracking Parameters: Modify max_age, min_hits, and iou_threshold in the SORT tracker for different tracking behaviors.
Confidence Threshold: Adjust the confidence threshold (conf > 0.3) to filter detections.

Example Output
The output window displays:

A video feed with a masked region of interest.
Bounding boxes around detected vehicles with class names and tracking IDs.
A red line (turns green when a vehicle is counted) at the specified coordinates.
A counter in the top-left corner showing the total number of vehicles counted.

# Notes

Ensure cars.mp4 and mask.png are compatible (same resolution).
The weights_yolo12n.pt file must be in the project directory.
For better performance, use a GPU-enabled environment if available.
The counting line’s position and the mask should be adjusted based on the video content.
