# 🏗️ System Architecture

### [🏠 Home](../) | [📺 Demo](../demo) | [🏗️ Architecture](./) | [📄 Documentation](../documentation)

---

## 🗺️ System Overview
![High Level Diagram](../assets/diagrams/system-overview.png)
*
Figure 2: Interaction between Hardware, Firmware, and Cloud layers.*

## 🔌 Hardware Subsystems
*   **Main Controller:** [e.g., Jetson Nano for Image Processing]
*   **Actuation:** [e.g., 6x High-torque Brushless Motors via CAN Bus]
*   **Power:** [e.g., 6S LiPo with custom BMS]

## 🧠 Software Logic
<!-- 
  You can also use small GIFs for software flows or UI logic 
-->

<!-- IMAGE EMBED TEMPLATE -->
<p align="center"> <!-- OPTIONS: left, center, right -->
  <img 
    src="../assets/images/software-flow.png" 
    alt="Descriptive text for screen readers" 
    title="Tooltip text when hovering"
    width="300" 
    height="auto"
    border="0"
    loading="lazy"
  >
  <br>
  <em>Optional: Add a caption here in italics</em>
</p>

The software stack is built on [ROS2/Arduino/etc]. 

<p align="right">
  <img src="../assets/images/software-flow.png" width="300" align="right" />
</p>

1. **Perception Layer:** Processes IMU and Vision data.
2. **Decision Layer:** Calculates Inverse Kinematics.
3. **Execution Layer:** Sends PWM signals to motor drivers.

<br clear="right"/>

---
[Review Technical Documents →](../documentation)