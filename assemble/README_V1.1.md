# Tinker Assembly Guide  

## 🏗️ Full Machine Assembly  
![Full Machine Assembly](path/to/image)  

## ⚙️ Basic Configuration  
- **Router Name**: `Tinker-2.4G-ID`  
- **Password**: `11111111`  

### 🔩 Motor Configuration  

#### **Left Leg (STM32 CAN1)**  
| Joint      | Motor Type | CAN ID |
|------------|------------|--------|
| Yaw        | 6006       | 1      |
| Roll       | 8006       | 2      |
| Thigh      | 8006       | 3      |
| Shin       | 8006       | 4      |
| Foot       | 6006       | 5      |

#### **Right Leg (STM32 CAN2)**  
| Joint      | Motor Type | CAN ID |
|------------|------------|--------|
| Yaw        | 6006       | 1      |
| Roll       | 8006       | 2      |
| Thigh      | 8006       | 3      |
| Shin       | 8006       | 4      |
| Foot       | 6006       | 5      |

#### **Head (STM32 CAN1)**  
| Joint          | Motor Type | CAN ID |
|---------------|------------|--------|
| Head Yaw      | 3507       | 6      |
| Head Pitch    | 3507       | 7      |

---

## 🏗️ Frame Assembly  

### **Step 1: Install Power Board & Base**  
Ensure the **battery slot** is positioned correctly at the back of the baseplate. The **24V DC power terminal** should align with the power board PCB.  
![Power Board Installation](path/to/image)  
![Base Assembly](path/to/image)  

### **Step 2: Install Bottom Support**  
Secure the bottom support using **M4 screws**.  
![Bottom Support](path/to/image)  

### **Step 3: Install Top Plate & Motors**  
Mount the **top plate** and attach **two 6006 motors (ID 1)**, ensuring the **debug port aligns with the cutout**.  
![Top Plate & Motors](path/to/image)  

### **Step 4: Install Aluminum Structure**  
Attach the **aluminum structure** onto the **6006 motors**.  
![Aluminum Structure](path/to/image)  

### **Step 5: Install Two 8008 Motors**  
Mount **two 8008 motors (ID 2)** along with their **aluminum supports** to connect with the **6006 motors** above.  
![8008 Motor Installation](path/to/image)  

### **Step 6: Install Thigh Motors & Aluminum Structure**  
- Attach **thigh motors (ID 3)** and **aluminum structure**.  
- Ensure the **roll-axis aluminum bends downward**.  
- Use an **independent carbon fiber plate** for thigh motor support.  
![Thigh Motor Installation](path/to/image)  
![Carbon Fiber Support](path/to/image)  

### **Step 7: Assemble Thigh & Roll Structure**  
Ensure the **"chicken head" structure** and **aluminum frame** are correctly oriented.  
![Thigh & Roll Assembly](path/to/image)  
![Orientation Check](path/to/image)  

### **Step 8: Install Battery & Chest Structure**  
![Battery & Chest Assembly](path/to/image)  

### **Step 9: Install Carbon Fiber Beams**  
After installing **six motors**, assemble the **carbon fiber beams** to complete the **middle frame**.  
![Carbon Fiber Beams](path/to/image)  

---

## 🦵 Thigh Assembly  

Once the **middle frame** is completed:  
1. Connect **all motor cables properly**.  
2. Align the **"chicken head" structure** with the **thigh arm carbon plate cutouts**.  
![Thigh Assembly](path/to/image)  

After installing the **thigh carbon plate**, attach the **left and right cable protection structures**. Ensure:  
- **Correct cutout positioning**.  
- **Proper cable routing** for motor wires.  
![Cable Protection Installation](path/to/image)  

---

## 🦿 Shin Assembly  

- Secure the **shin motors**.  
- Route the cables **according to the diagram**.  
![Shin Motor Installation](path/to/image)  

Use **protective structures** to route the **foot-end cables** through the **shin carbon plate grooves**. Ensure:  
- **Joint-clamping cable alignment**.  
- **Parallel routing with shin motor cables**.  
![Cable Routing](path/to/image)  

### **Final Step: Foot Installation**  
Ensure the **independent carbon fiber support** is properly positioned.  
![Foot Installation](path/to/image)  
![Final Foot Assembly](path/to/image)  

---

## 🔌 Wiring & Controller Installation  

### **Step 1: Install Air Switch & Fixing Structure**  
![Air Switch & Fixing](path/to/image)  

### **Step 2: Install Main Controller Board**  
Before installation:  
✅ Ensure all **control unit software** is pre-configured.  
✅ Follow the diagram to install:  
   - **Odroid controller**  
   - **Router**  
   - **Servo driver board**  
![Controller Installation](path/to/image)  

### **Step 3: Install Jetson Nano**  
Attach the **Jetson Nano** to the **back panel** using a **3D-printed support structure**.  
![Jetson Nano Installation](path/to/image)  

After assembling the **main control system hardware**, mount it onto the **robot body** using the **support frame**.  
![Main Control Mounting](path/to/image)  

Complete **cable routing** using the protective cover.  
![Cable Routing](path/to/image)  

At this stage, **Tinker assembly is complete**!  

---

## 🛠️ Pre-Head Installation Checks  

Before installing the **head**, ensure:  
- **Electrical soldering is complete**.  
- **Gait tests are performed** to prevent failures.  

### **Step 1: Install OLED & IMU Modules**  
For **better gait stability**, an **external IMU module** is recommended.  
![IMU Module](path/to/image)  

The **OLED module** displays:  
- **Current robot IP**  
- **Module status**  
- **Motor states**  

Install the **OLED module** into the **robot cover cutout**, then connect it to the **main controller UART**.  
![OLED Installation](path/to/image)  
![UART Connection](path/to/image)  

---

## ⚡ Electrical Wiring Diagram  

Once the **mechanical assembly** is completed, begin **electrical soldering**.  

### **Power Supply Diagram**  
The **power supply diagram** below shows **Tinker’s complete electrical system**.  
- **Single-leg CAN & power cables** are merged into **one route** inside the body and connected to the main control board.  

**Diagram:**  
![Power Supply Diagram](path/to/image)  

### **Communication Wiring**  
- The **left and right leg CAN buses** are merged into **one CAN route**.  
- **Left leg → CAN1**, **Right leg → CAN2** on STM32 board.  
- The **servo driver board** is connected via **UART2**.  

**Note:**  
- Refer to **PCB silkscreen** for **IO definitions**.  
- **TX on servo board → TX on control board**  
- **RX on servo board → RX on control board**  

**Diagram:**  
![Communication Wiring](path/to/image)  

---

## 🤖 Head Installation  

After completing the **main body assembly**, proceed with **head installation**.  

### **Step 1: Fixed-Angle Head Installation**  
The current **fixed-angle head design** supports:  
- **LiDAR mounting**  
- **Monocular camera mounting**  

Additionally, a **camera mount is available in the lower chest area**.  
![Head Installation](path/to/image)  
![Camera Mount](path/to/image)  

---

## 🔧 Software Configuration  

After hardware assembly, refer to the **Tinker Software User Guide** for software setup.  
