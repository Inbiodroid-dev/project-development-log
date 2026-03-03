# [Prometheus 3.0]
> **A high-performance humanoid telepresence platform for intuitive remote operation.**

### [🏠 Home](./) | [📺 Demo](./demo) | [🏗️ Architecture](./architecture) | [📄 Documentation](./documentation)

---

## 🚀 Project Highlight
<<<<<<< HEAD
<p align="center">
  <video src="assets/videos/pr3.mp4" width="80%" controls>
    Your browser does not support the video tag.
  </video>
  <br>
  <em>Figure 1: Presentation of the telepresence platform Prometheus 3.0.</em>
</p>
=======
<!-- 
  VIDEO EMBED INSTRUCTIONS:
  - 'src': Use 'assets/videos/filename.mp4' (no ../ needed here).
  - 'width="100%"': Makes the video span the full width of the README.
  - 'controls': Adds play/pause/volume buttons.
-->
https://github.com/user-attachments/assets/a3059b52-39cb-423c-a9ad-503aea494c89

Figure 1: Presentation of the telepresence platform Prometheus 3.0.</em>

>>>>>>> da6ad9fd92e900739c752d0209b6eab0aa1f1628

### 💡 General Overview
Prometheus 3.0 is a humanoid robot designed for real-time teleoperation. Using the **Hermes-Avatar** architecture, the system translates a human operator's movements into precise robot actions over a UDP network, allowing for immersive remote interaction and task execution.

### 🛠️ Core Technology
*   **Mechanical:** Lightweight structural design featuring high-performance actuators: **eRob (ZeroErr)** for the arms, **AK10-9 (CubeMars)** for the torso, and **RMD (MyActuator)** for the neck and gripper.
*   **Electronics:** Distributed control system powered by **Teensy 4.1** microcontrollers for the robot (Avatar) and **ESP32** (DFRobot Beetle C3) for the operator (Hermes).
*   **Software:** Real-time firmware developed in C++ using **PlatformIO**, featuring **SimpleFSM** for state management and a custom UDP protocol for low-latency communication.

---
[View Detailed Demos →](./demo)
