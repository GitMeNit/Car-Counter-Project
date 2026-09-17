# Project Statement: Real-Time Vehicle Counter System

## 1. Problem Statement

Traffic monitoring and vehicle volume analysis are fundamental requirements for modern Intelligent Transportation Systems (ITS), urban infrastructure planning, and commercial facility management. Traditional methods of vehicle counting suffer from significant operational and financial limitations:

- **Inflexible Physical Hardware:** In-road induction loops and pneumatic road tubes require costly, intrusive installation, cause traffic disruption during setup/maintenance, and are prone to degradation from road surface wear and adverse weather.
- **High Operational Costs & Human Error:** Manual traffic counts conducted by human observers are labor-intensive, financially unscalable, and susceptible to severe counting errors caused by fatigue, distraction, or poor visibility during night shifts.
- **Limitations of Simple Optical Systems:** Basic motion detection and camera systems without robust object tracking frequently double-count stationary or slow-moving vehicles, struggle with occlusion (vehicles overlapping in frame), and fail under changing ambient lighting conditions or headlight reflections.

To address these limitations, there is a critical need for a lightweight, software-defined computer vision solution that uses standard video infrastructure (IP cameras or recorded feeds) to deliver accurate, automated, single-pass vehicle detection and counting in real time.

---

## 2. Scope of the Project

The **Car Counter Project** encompasses the design, implementation, and deployment of an automated real-time vehicle detection, tracking, and tripwire counting software module using Python and OpenCV.

### In Scope:
- **Video Input Handling:** Ingestion and real-time processing of both pre-recorded video files (`.mp4`, `.avi`, `.mkv`) and live camera feeds (webcams, RTSP IP camera streams).
- **Computer Vision Pipeline:** Frame preprocessing (grayscale conversion, Gaussian blur filtering, noise reduction, and background subtraction / frame differencing).
- **Vehicle Contours & Bounding Box Detection:** Identification of vehicle blobs, filtering out non-vehicle contours based on dynamic minimum area thresholds, and bounding box extraction.
- **Centroid Calculation & Object Tracking:** Tracking spatial centroids across consecutive video frames to track movement vectors and maintain persistent entity recognition.
- **Virtual Tripwire Counting:** Algorithmic evaluation of line-crossing events to ensure each vehicle increments the global counter exactly once upon crossing the defined counting threshold.
- **On-Screen Visualization (OSD):** Real-time rendering of bounding boxes, centroid coordinates, virtual tripwire lines, and dynamic on-screen statistics counters directly on the output video stream.
- **Configuration & Calibration:** Adjustable parameters for detection sensitivity, line positioning, minimum vehicle box dimensions, and Region of Interest (ROI) selection.

### Out of Scope (Current Iteration):
- License plate recognition (ALPR) or speed estimation (planned for future phases).
- Cloud-hosted web dashboard and multi-camera cluster management (focused on edge single-stream processing).
- Complex multi-class vehicle segmentation (e.g., distinguishing lightweight sedans from heavy trucks) using heavy GPU-bound deep learning frameworks.

---

## 3. Target Users

The system is designed to serve a diverse group of stakeholders in traffic management, urban engineering, and commercial analytics:

1. **Traffic Engineers & Urban Planners:**
   - Use traffic volume data to assess road capacity, design signal timing schedules, evaluate intersection performance, and justify road widening or infrastructure expansion projects.

2. **Smart City & Transportation Authorities:**
   - Deploy automated traffic surveillance across municipal networks to monitor real-time road density, detect congestion bottlenecks, and optimize public transit routing.

3. **Commercial Facility Managers & Parking Operators:**
   - Track entry and exit rates for parking garages, shopping malls, toll booths, and logistics hubs to optimize occupancy management and security operations.

4. **Academic Researchers & Computer Vision Practitioners:**
   - Utilize an open-source, lightweight computer vision framework for testing tracking algorithms, background subtraction models, and synthetic traffic data generation.

---

## 4. High-Level Features

| Feature Category | Feature Name | Description |
|---|---|---|
| **Input Processing** | Flexible Stream Ingestion | Supports local video files (`.mp4`, `.avi`) and live video streams (Webcam / RTSP feeds). |
| **Input Processing** | Adaptive Region of Interest (ROI) | Allows masking out non-road areas (e.g., sky, sidewalks, trees) to minimize false positives and lower CPU utilization. |
| **Detection Engine** | Real-Time Contour Extraction | Detects vehicle shapes using adaptive Gaussian blur and background subtraction (MOG2 / KNN). |
| **Detection Engine** | Dynamic Area Thresholding | Filters out noise, shadows, pedestrians, and animals based on configurable width/height/area constraints. |
| **Tracking System** | Centroid Tracking & Velocity Trajectory | Calculates vehicle center points and tracks vector movement across sequential frames to maintain object identities. |
| **Counting Logic** | Virtual Line-Crossing Tripwire | Increments the global vehicle count when a tracked centroid intersects the virtual counting line segment. |
| **Counting Logic** | Duplicate Prevention Algorithm | Employs single-pass state tracking to guarantee stationary or slow-moving vehicles are not double-counted. |
| **Visualization & UX** | Live HUD Overlay | Displays bounding boxes, centroid indicators, color-changing tripwire feedback, and live aggregate vehicle count. |
| **System & Setup** | Lightweight CPU Execution | Runs smoothly on standard CPU hardware without requiring expensive GPU compute infrastructure. |
