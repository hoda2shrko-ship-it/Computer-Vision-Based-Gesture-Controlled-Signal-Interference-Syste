# Computer-Vision-Based-Gesture-Controlled-Signal-Interference-Syste
An AI-powered Computer Vision system that uses real-time hand gesture recognition to control external hardware. Using Python, OpenCV, and MediaPipe, the system detects predefined gestures and translates them into commands sent to an ESP32 to activate or deactivate a connected wireless signal interference module.
# AI Gesture Control — Safe Simulation Starter

This is a modular Windows/Python classroom demonstration:
- OpenCV face detection
- MediaPipe Tasks hand tracking
- Index finger raised => simulated ON
- Closed fist => simulated OFF
- Tkinter status dashboard
- Separate modules for each function

## Important safety boundary
The included communication module is **simulation only**. It does not connect to, send commands to, or control RF/jamming equipment. It is intended for on-screen demonstration only.

## Python version
The project is configured for the Python 3.14.8 installation found on the target computer. Use 64-bit CPython on Windows. `requirements.txt` pins MediaPipe 1.2.0, which provides the Tasks API used here, and limits OpenCV to its 4.x series. The hand landmark model is included as `hand_tracking/hand_landmarker.task`.

## Setup (PowerShell)
Run these commands from this project folder:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PowerShell blocks activation, use the environment's Python directly instead:

```powershell
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe main.py
```

## Run

```powershell
python main.py
```

Press `q` in the camera window to quit.

## Gesture rules
- Only index finger extended (other four fingers folded): `INDEX_UP` => ON
- All four fingers folded: `FIST` => OFF
- Other poses: ignored

The classifier uses a simple landmark-height heuristic and may need calibration for camera angle and hand orientation.

## Face authorization limitation
`face_authorization.py` is deliberately a demo gate: it allows processing only when exactly one face is visible. It does **not** identify a person. Do not present this as face recognition or use it for real access control. For a real identity demo, enroll consenting participants and integrate a suitable face-embedding matcher with liveness/anti-spoofing safeguards.

## Project map
- `main.py`: connects the modules
- `face_recognition/face_detection.py`: detects faces
- `face_recognition/face_authorization.py`: demo authorization gate
- `hand_tracking/hand_detection.py`: MediaPipe hand landmarks
- `hand_tracking/hand_landmarker.task`: model used for hand tracking
- `hand_tracking/gesture_classifier.py`: gesture labels
- `communication/esp32_serial.py`: safe local command simulator
- `dashboard/interface.py`: status dashboard
- `config/settings.py`: camera and stability settings

## Troubleshooting
- If the camera does not open, change `CAMERA_INDEX` to 1 in `config/settings.py`.
- If dependency installation reports that no MediaPipe wheel matches, check that Python is 64-bit and that pip is up to date.
- If the dashboard appears sluggish, reduce camera resolution in `settings.py`.
