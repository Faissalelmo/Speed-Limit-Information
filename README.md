# 🚦 Speed Limit Detection System using YOLOv8 and PyQt5

This project is an AI-powered speed limit detection system that uses real-time object detection to identify speed limit traffic signs, analyze their type and distance from the vehicle, and determine the appropriate speed quality feedback. It combines computer vision with a user-friendly graphical interface.

## 🎯 Objectives

- Detect **speed limit traffic signs** in real time from a camera feed or video.
- Classify the **type of traffic sign** (e.g., 30, 50, 80 km/h, etc.).
- Measure the **distance** between the traffic sign and the vehicle.
- Display **speed limit**, **sign type**, and **speed quality feedback** (e.g., OK, Slow down).
- Provide a **GUI** for live visualization using **PyQt5**.

## 🧠 Technologies Used

- **YOLOv8 (Ultralytics)** for object detection
- **Roboflow** for data labeling and annotation
- **PyQt5** for GUI development
- **OpenCV** for image processing and camera access
- **Python** (main programming language)

## 🗂️ Project Structure

```bash
├── main.py               # PyQt5 application
├── yolov8_model/         # Trained YOLOv8 model (.pt)
├── utils/                # Helper functions for detection, distance estimation
├── assets/               # Icons and media files
├── README.md             # This file
├── requirements.txt      # Python dependencies
└── data/                 # Sample images/videos or dataset preview
```

## 🧪 How It Works

### Dataset Preparation

- Annotated speed limit signs with Roboflow.
- Exported dataset in YOLO format and trained it with YOLOv8 using Ultralytics.

### Model Training

```bash
yolo task=detect mode=train model=yolov8n.pt data=data.yaml epochs=100 imgsz=640
```

### Real-Time Detection

The trained model detects traffic signs via webcam/video input and classifies the speed limit type.

### Distance Estimation

A function estimates the distance between the detected sign and the vehicle based on the sign size in the frame.

### Speed Quality Evaluation

Based on the current vehicle speed (input or simulated), the system determines whether the driver is within the legal limit.

### Graphical Interface (GUI)

The interface is developed using PyQt5 and includes:
- Live camera feed
- Detected sign and speed limit
- Estimated distance to sign
- Speed quality feedback (e.g., OK, TOO FAST)

## 💻 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/your-username/speed-limit-detection.git
cd speed-limit-detection
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the application

```bash
python main.py
```

## 📦 Dependencies

See `requirements.txt` for full list.

Main libraries:
- ultralytics
- opencv-python
- pyqt5
- numpy

Install Ultralytics if not already:

```bash
pip install ultralytics
```

## 📊 Features

- ✅ Real-time detection of speed limit signs
- ✅ GUI with PyQt5
- ✅ Distance estimation between sign and camera
- ✅ Speed quality alert
- ✅ Works on webcam or video input

## 📷 Screenshots
![Uploading gui_tsr.png…]()

## 🔮 Future Improvements

- Integrate vehicle's real speed from GPS or CAN bus
- Add voice alerts for over-speeding
- Expand to detect other traffic signs (Stop, Yield, etc.)
- Deploy on edge devices (Jetson Nano, Raspberry Pi)

## 👤 Author

Developed by **Faissal Elmokaddem**  
📧 Contact: faissal.elmokaddem@gmail.com  
🔗 LinkedIn: [linkedin.com/in/faissal-elmokaddem](https://linkedin.com/in/faissal-elmokaddem)  
💻 GitHub: [github.com/FaissalElmokaddem](https://github.com/FaissalElmokaddem)

## 📜 License

This project is licensed under the MIT License.

---

🚗 *"Driving safely with AI-powered vision."*
