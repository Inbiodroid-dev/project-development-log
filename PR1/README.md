# [Prometheus 1.0]
> **A high-performance humanoid telepresence platform for intuitive remote operation.**

<!-- Navigation Bar (Markdown) -->
### [🏠 Home](./) | [📺 Demo](./demo) | [🏗️ Architecture](./architecture) | [📄 Documentation](./documentation)

---

## 🚀 Project Highlight
<!-- 
  VIDEO EMBED INSTRUCTIONS:
  - 'src': Use 'assets/videos/filename.mp4' (no ../ needed here).
  - 'width="100%"': Makes the video span the full width of the README.
  - 'controls': Adds play/pause/volume buttons.
-->

https://github.com/user-attachments/assets/8f866c88-ca14-45ef-984d-4586b2ca5198

Figure 1: Presentation of the telepresence platform Prometheus 1.0.</em>


### 💡 General Overview
The system enables real-time teleoperation of a humanoid robot using Vive trackers to capture the operator’s motion. Pose data is transmitted via UDP to a single-board computer (SBC), where it is processed and converted into joint commands.

The SBC distributes these commands to multiple MCUs through serial communication, and each MCU controls the actuators via the CAN bus.

### 🛠️ Core Technology
*   **Mechanical:** Modular humanoid structure built with nylon and aluminum components, combining lightweight design with structural rigidity and durability.
*   **Electronics:** Distributed control architecture with a single-board computer (SBC) and multiple MCUs connected via serial communication and CAN bus.
*   **Software:** Real-time pose processing and motion mapping, UDP-based communication, and low-level actuator control over CAN.

---
[View Detailed Demos →](./demo)
