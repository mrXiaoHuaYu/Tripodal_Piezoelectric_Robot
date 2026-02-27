# Tripodal_Piezoelectric_Robot

<img width="2545" height="1364" alt="14bf23b6-1cb8-4939-a44e-f2bd1102ed04" src="https://github.com/user-attachments/assets/2bc7a6dd-ed97-44f7-a188-e090f5443cf2" />




This repository contains the software for controlling a custom three-legged robot and performing real-time panoramic image stitching, as described in our submission to *Nature Communications*. The software integrates robotic gait modulation with automated visual data collection.

## 1. Overview
The application is designed for Windows and provides a unified interface for:
* **Remote Robot Control**: Low-latency movement commands via HTTP protocol.
* **Gait Parameter Tuning**: Precise control over voltage, pulse frequency, and duty cycles.
* **Automated Imaging**: Time-interval-based frame capture and panoramic stitching using feature-matching algorithms.

---

## 2. System Requirements
* **Hardware**: 
    * Custom Three-Legged Robot (compatible with the documented HTTP API).
    * Standard USB Camera (720P or 1080P recommended).
* **Software**: 
    * Windows 10/11 (for the `.exe` version).
    * (Optional for Source) Python 3.10+ with `opencv-python`, `Pillow`, `requests`, and `numpy`.

---

## 3. Key Features

### Robotic Gait & Motion
The software supports 6-directional movement through a hexagonal UI layout and keyboard hotkeys (`W`, `A`, `S`, `D`, `Q`, `E`, `Space`).
* **Voltage Control**: Adjustable power levels (0–80).
* **Frequency Modulation**: Independent frequency settings for Leg 1 (Left), Leg 2 (Forward), Leg 3 (Backward), and friction reduction.
* **Pulse Mode**: A high-precision "Pulse" mode for micro-stepping, where frequency ($f$) in Hz is converted to pulse periods ($T$) in microseconds ($\mu s$) for the microcontroller: 
$$T(\mu s) = \frac{1,000,000}{f(Hz)}$$

### Image Processing & Stitching
* **Real-time Preview**: Live camera feed with adjustable FPS and resolution settings.
* **Automated Capture**: Users can set an "Auto-interval" (e.g., 2.0s) to save frames during robot movement.
* **Stitching Engine**: Utilizes the OpenCV `Stitcher_SCANS` mode, optimized for planar surfaces and translational robotic movement.

---

## 4. Operation Guide
1.  **Connection**: Ensure the robot and PC are on the same network. Enter the robot's IP (default: `172.20.10.2`) and click **Connect**.
2.  **Calibration**: Set the operating voltage and frequencies for the specific terrain.
3.  **Camera Initialization**: Select the camera device and click **Start Camera**.
4.  **Data Collection**:
    * Click **Start Capture**.
    * Manuever the robot using the UI or keyboard.
    * The software saves individual frames to the `./stitching_projects` directory.
5.  **Finalization**: Click **End and Generate** to run the stitching algorithm and view the final result.

---

## 5. Directory Structure
```text
/stitching_projects
  /YYYYMMDD_HHMMSS     <-- Timestamped project folder
    /raw               <-- Captured original frames
    result.jpg         <-- Final stitched panoramic image
