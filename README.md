<h1 align="center">⚙️ SmartAttend AI - Smart Classroom Attendance System ⚙️</h1>

<p align="center">
  <img src="https://i.postimg.cc/zfF24Kw0/image.png" alt="SmartAttend AI Banner">
</p>

---

<p align="center">
  <img src="https://img.shields.io/badge/SmartAttend-AI%20Attendance-6366f1?style=for-the-badge&logo=google-lens&logoColor=white">
  <img src="https://img.shields.io/badge/React-v19-61DAFB?style=for-the-badge&logo=react&logoColor=black">
  <img src="https://img.shields.io/badge/Vite-v7.3.2-646CFF?style=for-the-badge&logo=vite&logoColor=white">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-v3.10-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/Flask-v3.0-000000?style=for-the-badge&logo=flask&logoColor=white">
  <img src="https://img.shields.io/badge/OpenCV-YuNet-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white">
  <img src="https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Vercel-Frontend-000000?style=for-the-badge&logo=vercel&logoColor=white">
  <img src="https://img.shields.io/badge/Render-Backend-46E3B7?style=for-the-badge&logo=render&logoColor=black">
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-6366f1"></a>
  <img src="https://img.shields.io/github/repo-size/Shariar-Ahamed/smart-classroom-attendance-system">
  <img src="https://img.shields.io/github/last-commit/Shariar-Ahamed/smart-classroom-attendance-system">
</p>

<p align="center">
  <img src="https://img.shields.io/github/stars/Shariar-Ahamed/smart-classroom-attendance-system?style=social">
  <img src="https://img.shields.io/github/forks/Shariar-Ahamed/smart-classroom-attendance-system?style=social">
</p>

---

<p align="center">
  <b>SmartAttend AI</b> is a premium, high-performance web-based Smart Classroom Attendance System. Built using a <b>React 19 + Vite</b> frontend and a secure <b>Flask + OpenCV</b> backend, it features a gorgeous custom glassmorphic UI, real-time facial recognition, database activity tracking, role-based access control, and a secure administration panel.
</p>

> **Live Production Demo**: **[smart-attend-diu.vercel.app](https://smart-attend-diu.vercel.app/)**

---

## 🛠️ Complete Technology Stack & Core Tools

This project is built using a modern, lightweight, and high-performance stack that ensures instant real-time AI recognition, data security, and seamless user experiences.

### 🎨 Frontend (Client-Side SPA)
* **React 19 (v19.2.6):** Leverages the latest React core version for blazing-fast component rendering and hook-based state lifecycle management.
* **Vite (v7.3.2):** Serves as the modern build tool and development server, replacing slow Webpack setups with instant HMR (Hot Module Replacement).
* **Tailwind CSS 4 (v4.1.17):** Implements the utility-first CSS styling framework with a custom dark-glassmorphic styling system.
* **Framer Motion (v12.4.2):** Controls the UI animation engine, producing fluid transitions, card animations, and sliding toast notification states.
* **Lucide React (v1.24.0):** Provides a comprehensive library of pixel-perfect vector icons matching the dark sci-fi aesthetic.
* **Vite Plugin SingleFile (v2.3.0):** Bundles all compiled Javascript, CSS, and HTML assets into a single static file to maximize load speed and host compatibility.

### 🐍 Backend (REST API Server)
* **Python 3 (v3.10+):** The backend execution core.
* **Flask (v3.0.0):** The lightweight WSGI web framework routing API calls and serving live video streams.
* **Flask-CORS (v4.0.0):** Standardizes Cross-Origin Resource Sharing rules to allow safe client-server communication.
* **PyMongo (v4.6.1):** The official MongoDB driver linking the python server to the Mongo clusters.
* **PyJWT (v2.8.0):** Handles cryptographic generation and validation of secure JSON Web Tokens (JWT) for secure authentication.
* **Bcrypt (v4.1.2):** Enforces industry-standard Blowfish-based password hashing before database storage.
* **NumPy (v1.26.4):** Manages multi-dimensional array mathematics, coordinates, and face encoding distance metrics.
* **Pillow (v9.0.0+):** Processes uploaded images in-memory for crop, resize, and orientation operations.
* **Gunicorn (v21.2.0):** Production-grade WSGI HTTP Server to deploy the Python backend on Linux servers.

---

## 🧠 AI / Computer Vision Models & Libraries

Face detection and recognition occur across the stack depending on the camera source and hardware constraints:

### 1. Browser-Side AI Model (Standard Webcams)
The React client runs browser-side machine learning using **`@vladmandic/face-api` (v1.7.15)**, a highly optimized, modern fork of face-api.js.
* **SSD MobileNet v1:** A CNN (Convolutional Neural Network) model trained to detect bounding boxes around human faces in real-time camera frames. The weights are dynamically loaded from a CDN (~5.4 MB) and cached by the browser.
* **Face Landmarking Net:** Identifies 68 key facial landmarks (eyes, nose, mouth, jawline) to compute face orientation and align the face crop.
* **Face Recognition Net:** Computes a 128-dimensional FaceNet-style vector descriptor containing the mathematical print of the face.

### 2. Server-Side AI Model (CCTV / RTSP IP Streams)
For 24/7 CCTV surveillance deployments, the Python backend handles recognition directly to offload client hardware.
* **YuNet Face Detector:** A state-of-the-art, CNN-based lightweight face detector optimized for OpenCV. It runs on the server, detecting faces at high frames-per-second (FPS) with robust tolerance for angles, lighting, and occlusion.
* **dlib ResNet Face Recognition:** Evaluates the aligned face crop against the official Python `face_recognition` model weights, producing a 128-dimensional vector encoding conceptually equivalent to the frontend's FaceNet descriptors.

---

## 📂 Core Workflows & Logic Breakdown

Any developer reviewing this codebase should understand these primary workflows:

```
[Webcam Capture] ---> [Face Detector (SSD/YuNet)] ---> [Landmarks Alignment]
                                                                |
                                                                v
[MongoDB Enc] <--- [128-d Vector Average] <--- [Face Recognition Net (128-d)]
```

### 1️⃣ Privacy-First Student Enrolment (`RegisterStudent.jsx`)
To register a student, the administrator captures **5 diverse photos** showing different facial angles (Center, Left, Right, Up, Down).
1. **In-Memory Vectors:** The system extracts the 128-dimensional vector descriptor for each photo.
2. **Descriptor Averaging:** The frontend merges these vectors using the `averageDescriptors` function, producing a single, robust mathematical signature of the student's face.
3. **No Image Saved:** The averaged 128-d array is saved in MongoDB. The raw photos are **completely discarded** from memory and never stored, preserving student privacy.

### 2️⃣ Non-Blocking Multi-Student Scanner (`LiveAttendance.jsx`)
The live scanner is designed for fast, concurrent processing of multiple students passing by a camera:
* **Non-Blocking Loop:** A `setInterval` loop runs at `TICK_MS = 500ms` (2 FPS) to analyze webcam frames. Detections are processed asynchronously, meaning the video feed never pauses or blocks.
* **Session Cache Map (`processedStudentsRef`):** Once a student is successfully matched (either marked present or verified as already marked), they are cached in a local `Set` in-memory. Future frames instantly skip database and API calls for that student, saving server resources.
* **8s Cooldown Alert Map (`lastNotifiedRef`):** Keeps track of when a notification toast was last triggered for each student ID to prevent spamming popups.
* **Horizontal Mirroring Alignment:** Since webcams flip the video feed (`-scale-x-100` class), the overlay bounding boxes are mirrored horizontally in `toOverlayStyle` using the formula `vw - box.x - box.width` so the tracking square aligns perfectly with the student's face.

### 3️⃣ Administrative Analytics Engine (`Dashboard.jsx`)
The dashboard displays aggregated, real-time statistics computed on the database collections:
* **Department Performance:** Gathers students by department and checks who has checked in today, displaying live bar charts.
* **Risk Watchlist:** Compiles overall attendance logs and flags students whose attendance rate is below **75%** (the standard exam eligibility threshold).
* **System Live Logs:** Displays the database latency (`< 15ms`), MongoDB connection status, and model version.
* **Virtual Terminal Console:** Simulates system status updates, showing neural network weights size (~5.4 MB) and `AES-GCM-256` biometric encryption states.

### 4️⃣ DIU Branded Academic Reporting (`AttendanceRecords.jsx`)
Administrators and Faculty can generate official attendance reports directly from the database:
* **Export PDF:** Opens a separate window, injects a styled DIU letterhead (with the Daffodil International University Single Crest Logo), formats active filters (Course, Date, Status), and triggers the browser print engine for clean vector PDF outputs.
* **Export Excel:** Dynamically writes an HTML XML spreadsheet with grid lines enabled (`<x:DisplayGridlines/>`), blue headers, and text formatting tags (`mso-number-format:'\@';`) which prevent Microsoft Excel from stripping leading zeros off student ID numbers.
* **Dynamic File Naming:** Automatically names exports according to active criteria (e.g., `DIU_Attendance_AI401_2026_08_26.pdf`).

---

## 📂 Project Directory Structure

```bash
smart-classroom-attendance-system/
│
├── backend/                     # Python Flask Backend
│   ├── app.py                  # Main API server, JWT controller & REST routes
│   ├── db.py                   # MongoDB initialization & index configuration
│   ├── camera.py               # Video capture & RTSP camera stream wrapper
│   ├── face_service.py         # YuNet face detection & dlib signature matching
│   ├── attendance_service.py   # Attendance rules (checks, overrides, auto-absent)
│   ├── auth.py                 # JWT token generation & bcrypt password verification
│   ├── requirements.txt        # Python dependency manifest
│   └── README.md               # Backend local setup guidelines
│
├── future-plans/                # CCTV Deployment Documentation
│   ├── README.md               # RTSP stream transcoding & server-side plans
│   └── ip-cctv-diagram.png     # System architecture visual flow
│
├── src/                         # React Frontend Source (Vite SPA)
│   ├── assets/                 # Brand assets (DIU logo files)
│   ├── components/             # UI Components
│   │   ├── AttendanceRecords.jsx # PDF/Excel reports, history logs & search
│   │   ├── CoursesManager.jsx  # Course management & teacher allocation
│   │   ├── Dashboard.jsx       # Admin analytics, watchlist & system logs
│   │   ├── LiveAttendance.jsx  # Live webcam scanner, floating toasts & feed
│   │   ├── Login.jsx           # Dark glassmorphic authentication portal
│   │   ├── ManualAttendance.jsx # Grid attendance override interface for teachers
│   │   ├── RegisterStudent.jsx # 5-step capture stepper for new student faces
│   │   ├── Sidebar.jsx         # Navigation menu & Neon pulsing LED state
│   │   ├── StudentDashboard.jsx # Personalized course stats view for students
│   │   └── StudentsList.jsx    # Student profile database directory
│   ├── services/               # API Communication layers
│   │   ├── api.js              # Axios interceptors & backend API hooks
│   │   └── faceModel.js        # face-api.js browser neural net loader & matcher
│   ├── hooks/                  # Custom React hooks (useWebcam)
│   ├── index.css               # Google Font (Poppins) & Tailwind CSS v4 setup
│   ├── App.jsx                 # Routing controller & page layouts
│   └── main.jsx                # React root SPA rendering mount
│
├── index.html                  # Main HTML viewport configuration
├── vite.config.js              # Vite server & bundler configuration
├── package.json                # Frontend package scripts & Node libraries
└── README.md                   # Project documentation (This file)
```

---

## 🚀 Getting Started (Local Development)

### 1️⃣ Clone the Repository
```bash
git clone <repository-url>
cd smart-classroom-attendance-system
```

### 2️⃣ Backend Server Setup
Ensure you have **Python 3.8+** and a running instance of **MongoDB** (local or Atlas cluster).

```bash
# Navigate to backend
cd backend

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

Create a `.env` file in the `backend/` directory:
```env
MONGO_URI=mongodb://localhost:27017
DB_NAME=smartattend
JWT_SECRET=your-secret-key-change-me
CAMERA_SOURCE=0  # Use 0 for webcam, or use RTSP stream link
```

Run the backend server (starts on `http://localhost:5000`):
```bash
python app.py
```

### 3️⃣ Frontend Client Setup
Ensure you have **Node.js (v18+)** installed.

```bash
# Navigate back to the root folder
cd ..

# Install frontend dependencies
npm install

# Run the development server (starts on http://localhost:5173)
npm run dev
```

---

## 👤 Initial Seed User

On its first run, the backend automatically seeds a single administrator account. Faculty and students can sign up using the **Create Account** interface on the front-end login card.

| Role | Username | Password |
|---|---|---|
| **ADMIN** | `admin` | `admin@123` |

*(Note: student usernames must start with `s-` to be identified properly by the authentication schema.)*

---

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
