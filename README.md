# Multimodal-Human-Behaviour-Analysis-System
MHBAS is an advanced hardware-accelerated desktop application for real-time biometric analysis, clinical stress monitoring, and behavioral tracking. It integrates computer vision pipelines with deep vocal sentiment analysis to generate a synchronized timeline of physiological and behavioral insights.

🛠️ Tech Stack & Architecture

The system utilizes an asynchronous Producer-Consumer pipeline implemented via PyQt6 threads (QThread) and specialized workers to completely decouple microsecond sensor collection from inference latency.

GUI Framework: PyQt6 (Custom Cyberpunk/Glassmorphism theme layered via standard dynamic QPainters and custom QSS styles).

Computer Vision Frameworks: RetinaFace (High-accuracy structural facial bounding box tracking & landmark segmentation).

DeepFace (Face representation and macro-expression probability tracking).

Audio Pipeline Model: Wav2Vec2 (superb/wav2vec2-base-superb-er fine-tuned for vocal Sequence Classification / Emotion Recognition).

Kinematics Engine: OpenCV + Perspective-n-Point (SolvePnP) vector geometry estimating 3D Euler angles (Yaw, Pitch, Roll) for head tilt and tracking attention.

Backend Computations: PyTorch, TensorFlow (GPU memory growth/CUDA optimization), NumPy, Librosa (Acoustic pitch tracking via piptrack and peak-normalization matrix tracking).

🔍 Core Logic & Calculations
1. Dual-Phase Ambient Calibration:
Before active session analysis, the app locks into a critical 12-second adaptive calibration routine to adjust for the user's specific baseline environment:
Phase 1 (Stillness & Silence): Measures real-time ambient space noise floor levels (RMS) and extracts structural baseline camera alignments.
Phase 2 (Natural Vocalization): Evaluates normal talking speech samples to establish target vocal ranges and extract the user's base neutral emotional state.

2. Behavioral Threat Matrix:
The application runs real-time heuristics across metrics to watch for target stress triggers and user distractions:  Stress Factor Index: Combines face metrics against voice features. Scales raw markers if a negative expression context persists across 5 consecutive tracking loops.  Distraction Heat Tracker: A structural temperature gauge tracking focus. Adds weight points whenever look paths or head orientations veer off-center, while scaling down during periods of direct focal tracking.

🚨 Automated Behavioral Alert Signals:
The platform actively records critical tracking changes directly to the console feed and session reports:  ALERT: Prolonged Gaze Avoidance (>6s) — Fired when gaze arrays deviate from center boundaries continuously.  ALERT: Eye Closure (>3s) — Catches potential drowsiness episodes via prolonged EAR  anomalies.  ALERT: High Distraction Heat — Triggers when real-time head tilts or side looks suggest complete task disengagement.  TRAUMA CARE ASSESSMENT INTERVENTION ALERT — Fires an active 3-beep safety loop (winsound.Beep) when computed stress scales spike beyond critical 85% thresholds for more than 60% of total active recording runs.

📊 Live System Analytics & Session Exporting:
The interface splits operations across four high-density layout panels: Live Feed:Seamless webcam streaming overlay combined with real-time audio waveforms and biometric health pills.  Metrics Dashboard:Aggregates mathematical session peaks, longest high-stress duration streaks, focus averages, and Matplotlib status charts.  Session Log:Displays a historical running clock charting behavioral changes directly alongside real-time log lines.  Reports Desk:Generates assessment documents and clinical guides while providing time-series log exports to standard .csv formatting paths. 
