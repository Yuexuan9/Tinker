# Tinker  
## _Flexible, and Ready to Move: Your Cartoon-Style Bipedal Robot!_
<div align="center">
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/t01.JPG" height="300" />
</div>

**Tinker** 是一款开源的双足小机器人，旨在为机器人爱好者和开发者提供一个可操作的平台。该项目将详细提供所需的硬件材料、软件资源及完整的安装步骤，帮助用户轻松搭建和编程自己的机器人。通过Tinker，用户不仅能深入了解机器人运动和控制的基本原理，还能在此基础上进行个性化的扩展和改进。我们希望通过这个项目激发更多人对机器人技术的兴趣与探索，同时Tinker采用了OmniBotLab通用具身控制方案OmniBotLab介绍加速算法开发与模型部署

## 🌟 主要特点
- **🛠️ 简单**：无传动机构，使用 3D 打印和碳板切割即可完成组装。  
- **💰 低成本**：整机 BOM 价格低于 2W，90% 组件（电机、控制器）采用货架产品，支持二次开发。  
- **🤖 具身智能开发**：采用 **OmniRobLab 框架**，简化伺服驱动部署，使开发者专注于算法。  

**Tinker** is an open-source bipedal robot designed to provide robotic enthusiasts and developers with a hands-on platform. This project includes a detailed list of required hardware materials, software resources, and comprehensive installation steps to help users easily build and program their own robot.

Through Tinker, users will not only gain insights into the fundamental principles of robot movement and control, but also have the opportunity to personalize and enhance their projects. We aim to inspire more people to explore and engage with robotics technology through this initiative.

## 🌟 Key Features
- **🛠️ Simplicity**: No transmission mechanism required; assembly can be completed using 3D printing and carbon plate cutting.
- **💰 Low Cost**: The total BOM cost is under 20,000 RMB, with 90% of components (motors, controllers) being off-the-shelf products, supporting secondary development.
- **🤖 Embodied Intelligence Development**: Utilizes the OmniRobLab framework to simplify servo drive deployment, allowing developers to focus on algorithms.

---

## Core Technologies

1. Reinforcement Learning Algorithm Adaptation

The robot is specifically designed for reinforcement learning algorithms, enabling autonomous learning and continuous optimization of action strategies in complex and dynamic environments. Through deep integration with reinforcement learning, it demonstrates outstanding performance in motion control, task execution, and action planning. For example, when facing unknown terrains or complex tasks, the robot can quickly adapt and make reasonable decisions to efficiently complete tasks.

2. Direct Deployment and Testing

This system features a convenient direct deployment and testing function, making it widely applicable to various task scenarios. By simply connecting the device, users can quickly initiate robot testing, significantly reducing the R&D cycle and improving work efficiency. Compared to traditional deployment methods, it offers significant advantages in autonomy, flexibility, cost control, adaptability, and safety.

3. Complete Solution from Simulation to Real-World Deployment

The solution includes IsaacGym-based RL simulation, sim-to-sim transfer, real-world deployment, and secondary development tutorials.


4. Open-Source Training Software

The system is equipped with open-source training software that provides a wide range of functional modules, including model training settings, data visualization, and algorithm debugging interfaces. Users can freely adjust training parameters, monitor data changes in real-time during training, and optimize algorithms while troubleshooting issues. The open-source nature offers great flexibility and scalability, allowing users to customize training plans according to their needs. Additionally, the open-source community provides valuable resources and technical exchange opportunities to accelerate development.


5. Integrated Solution: Physical Robot + Reinforcement Learning

This solution combines real-world robotics with reinforcement learning to provide a comprehensive development and deployment framework.

---

## Performance Parameters

1. Motion Performance

	1.	Maximum Walking Speed: The robot can achieve a stable walking speed of up to 1m/s and a normal walking speed of 0.5m/s, demonstrating excellent mobility. It can move quickly through various environments, meeting the speed requirements for multiple application scenarios.
	2.	Load Capacity: The robot has a load capacity of 1kg, allowing it to carry tools or objects and perform tasks such as item transportation and equipment operation.

2. Battery Life

	1.	Battery: The robot is powered by a 21.6V 5Ah 108Wh battery with a charging voltage of 25.2V and comes with a dedicated charger. The battery life is yet to be measured, aiming to provide stable power for long-duration operations.
	2.	Energy-Saving Design: The system incorporates energy-saving optimizations at both hardware and software levels to reduce power consumption, extend battery life, and improve overall efficiency.
    
3. Control System
   
	1.	Controller: Equipped with high-performance controllers such as NVIDIA Jetson Nano, Odroid, and STM32, enabling fast data processing for real-time response and precise control.
	2.	Sensors: The system integrates advanced sensors, including a gyroscope, accelerometer, and electronic compass, to continuously monitor the robot’s posture, motion state, and surrounding environment. This provides essential data for accurate control and intelligent decision-making. Additionally, it supports Wi-Fi and 2.4G wireless Bluetooth, ensuring convenient data transmission and remote control capabilities.

---

## 整机搭载了如下的传感器：
- **📷 深度相机**  
  身体和头部配备两个深度相机，用于采集模仿数据。  

- **🗺️ 多样化导航**  
  可部署 **Mid360** 或使用深度相机实现自主导航和地图构建。  

- **🎥 FPV 头部操控**  
  具备头部自由度控制功能，可用于 **FPV 室内场景查看**。  

- **💡 高性能具身计算**  
  **控制+感知计算双单元** 支撑运动控制与模仿学习部署。  

- **🎬 动画编辑二次开发**  
  通过示教完成动画编辑并播放，支持 **RL（强化学习）** 和 **Python 二次开发**。  

- **🗣️ 多模态交互**  
  搭载 **语音和灯光功能**，可部署 **大模型** 实现语音交互。

## Integrated Sensors  

- **📷 Depth Cameras**  
  Equipped with two depth cameras on the body and head for imitation data collection.  

- **🗺️ Versatile Navigation**  
  Supports **Mid360** deployment or depth camera-based autonomous navigation and mapping.  

- **🎥 FPV Head Control**  
  Head movement freedom allows **FPV indoor scene observation**.  

- **💡 High-Performance Embodied Computing**  
  **Dual-unit control + perception computing** supports motion control and imitation learning deployment.  

- **🎬 Animation Editing & Secondary Development**  
  Enables animation editing and playback via demonstration, supporting **RL (Reinforcement Learning)** and **Python-based secondary development**.  

- **🗣️ Multimodal Interaction**  
  Integrated **voice and lighting functions**, capable of deploying **large models** for voice interaction.  

---

## Table of Contents
- [Tinker Usage Guide](https://github.com/Yuexuan9/Tinker/tree/main/guide)
- [Tinker BOM List](https://github.com/Yuexuan9/Tinker/tree/main/bom)
- [Tinker Assembly Guide](https://github.com/Yuexuan9/Tinker/tree/main/assemble)
- [Tinker Development](https://github.com/Yuexuan9/Tinker/tree/main/development)

---

## Tinker Usage Guide
This section will provide a step-by-step guide on how to operate and interact with the Tinker robot once assembled.

## Tinker BOM List
A detailed Bill of Materials (BOM) required to build the Tinker robot will be listed here. It includes hardware components, sensors, and other necessary parts.

## Tinker Assembly Guide
Comprehensive instructions on how to assemble Tinker from scratch, complete with images, will be made available in this section.

## Tinker Custom Development
Explore how to extend and enhance Tinker’s functionalities through custom development. This section will cover software development.

---

## 🔄 软件版本更新

### V1.0
- **固件更新方法:** 详见 [详细教程](https://github.com/Yuexuan9/Tinker/tree/main/assemble/README.md)。

### V1.1
**更新内容:** 详见 [详细教程](https://github.com/Yuexuan9/Tinker/tree/main/assemble/README_V1.1.md)。
1. **URDF 结构优化**，使仿真模型与实际机器人保持一致。
2. **训练软件架构优化**，提升强化学习训练效率。
3. **新增多种头部设计方案**，增强扩展性。
4. **嵌入式软件升级** 至 **OmniRobLabV1.0**。

---

## Video

YouTube:

<a href="https://youtu.be/nC0g2TXLNzI">
  <img src="https://img.youtube.com/vi/nC0g2TXLNzI/0.jpg" width="500" />
</a>

bilibili:

<a href="https://b23.tv/GL5qTvX">
  <img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/videos/24fp.png" width="500" />
</a>

Find more process videos [here](https://youtu.be/ASK_Aj-35oE).
## License

AGPL-3.0

---
✨Feel free to customize this further based on specific content for each section!✨

For more open-source information, visit [OpenLoong](https://www.openloong.org.cn/cn).
