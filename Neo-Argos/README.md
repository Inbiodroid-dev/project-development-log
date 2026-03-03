# Neo-Argos
> **A high-performance R&D differential drive platform for mastering ROS 2, autonomous navigation, and mobile robotics.**

### [🏠 Home](./) | [📺 Demo](./demo) | [🏗️ Architecture](./architecture)

---

## 🚀 Project Highlight

https://github.com/user-attachments/assets/44ac5a3f-6cdc-409b-b6c2-094af1129471

Figure 1: Neo-Argos during a Navigation Test.</em>

### 💡 The R&D Mission
Neo-Argos is the spiritual and technical successor to **Argos**, the mobile base of the Prometheus humanoid. While the original Argos was designed as a heavy-duty platform, Neo-Argos serves as a "battle-hardened" prototype and testbed.

The primary goal is to bridge the gap between simulation and real-world implementation of the **ROS 2** ecosystem. By using Neo-Argos, our team explores professional-grade tools like **Nav2** and **SLAM Toolbox**, perfecting the logic before migrating it back to the full-scale Prometheus platform.

### 🛠️ Core Technology
*   **Mechanical:** 10mm CNC-cut aluminum chassis with weight-reduction cutouts. Differential drive system (2x rear motors, 2x front caster wheels) for simplified but robust kinematics.
*   **Electronics:** 
    *   **High-Level:** NVIDIA Jetson Orin Nano (8GB) for intensive computing.
    *   **Low-Level:** ESP32 via **micro-ROS** for real-time motor control.
    *   **Actuation:** 2x high-torque **AK10 motors** communicating via CANopen.
*   **Software:** Full ROS 2 Humble/Iron stack featuring **Nav2**, **slam_toolbox**, and custom micro-ROS firmware.

---
[View Technical Architecture →](./architecture)
