# Tinker Assembly Guide  

## 🏗️ Full Machine Assembly  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/2025040901.PNG" width="300" />
	🔗 Open-source project (V2 version): https://github.com/golaced/OmniBotSeries-Tinker

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
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-2.png" width="300" /> 
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-3.png" width="300" />

### **Step 2: Install Bottom Support**  
Secure the bottom support using **M4 screws**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-4.png" width="300" />

### **Step 3: Install Top Plate & Motors**  
Mount the **top plate** and attach **two 6006 motors (ID 1)**, ensuring the **debug port aligns with the cutout**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-5.png" width="300" /> 

### **Step 4: Install Aluminum Structure**  
Attach the **aluminum structure** onto the **6006 motors**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-6.png" width="300" /> 

### **Step 5: Install Two 8008 Motors**  
Mount **two 8008 motors (ID 2)** along with their **aluminum supports** to connect with the **6006 motors** above.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-7.png" width="300" />

### **Step 6: Install Thigh Motors & Aluminum Structure**  
- Attach **thigh motors (ID 3)** and **aluminum structure**.  
- Ensure the **roll-axis aluminum bends downward**.  
- Use an **independent carbon fiber plate** for thigh motor support.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-8.png" width="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-9.png" width="300" />

### **Step 7: Assemble Thigh & Roll Structure**  
Ensure the **"chicken head" structure** and **aluminum frame** are correctly oriented.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-10.png" width="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-11.png" width="300" />

### **Step 8: Install Battery & Chest Structure**  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/2025assemblingthemiddkeframe.png" width="300" />


### **Step 9: Install Carbon Fiber Beams**  
After installing **six motors**, assemble the **carbon fiber beams** to complete the **middle frame**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-13.png" width="300" />


---

## 🦵 Thigh Assembly  

Following the completion of the middle frame assembly, both thigh modules have been successfully assembled. 
The next step involves mounting the carbon fiber thigh plates. 
Before proceeding, it’s necessary to ensure that all motor cables are correctly connected. 
It’s also crucial to verify the orientation of the “chicken head” in relation to the notch on the thigh arm carbon plate. 
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/2025assemblingthethighs.png" width="300" />


After installing the **thigh carbon plate**, attach the **left and right cable protection structures**. Ensure:  
- **Correct cutout positioning**.  
- **Proper cable routing** for motor wires.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-15.png" width="300" />


---

## 🦿 Shin Assembly  

- Secure the **shin motors**.  
- Route the cables **according to the diagram**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-17.png" width="300" />

Use **protective structures** to route the **foot-end cables** through the **shin carbon plate grooves**. Ensure:  
- **Joint-clamping cable alignment**.  
- **Parallel routing with shin motor cables**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-18.png" width="300" />


### **Final Step: Foot Installation**  
Ensure the **independent carbon fiber support** is properly positioned.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-19.png" width="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-20.png" width="300" />

---

## 🔌 Wiring & Controller Installation  

### **Step 1: Install Air Switch & Fixing Structure**  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-21.png" width="300" />


### **Step 2: Install Main Controller Board**  
Before installation:  
✅ Ensure all **control unit software** is pre-configured.  
✅ Follow the diagram to install:  
   - **Odroid controller**  
   - **Router**  
   - **Servo driver board**  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-22.png" width="300" />


### **Step 3: Install Jetson Nano**  
Attach the **Jetson Nano** to the **back panel** using a **3D-printed support structure**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-22.png" width="300" />


After assembling the **main control system hardware**, mount it onto the **robot body** using the **support frame**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-23.png" width="300" />


Complete **cable routing** using the protective cover.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-24.png" width="300" />


At this stage, **Tinker assembly is complete**!  

---

## 🛠️ Pre-Head Installation Checks  

Before installing the **head**, ensure:  
- **Electrical soldering is complete**.  
- **Gait tests are performed** to prevent failures.  

### **Step 1: Install OLED & IMU Modules**  
For **better gait stability**, an **external IMU module** is recommended.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-25.jpeg" width="300" />


The **OLED module** displays:  
- **Current robot IP**  
- **Module status**  
- **Motor states**  

Install the **OLED module** into the **robot cover cutout**, then connect it to the **main controller UART**.  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-26.png" width="300" />
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250401-27.png" width="300" />


---

## ⚡ Electrical Wiring Diagram  

Once the **mechanical assembly** is completed, begin **electrical soldering**.  

### **Power Supply Diagram**  
The **power supply diagram** below shows **Tinker’s complete electrical system**.  
- **Single-leg CAN & power cables** are merged into **one route** inside the body and connected to the main control board.  

**Diagram:**  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250409whiteboard.png" width="300" />


### **Communication Wiring**  
- The **left and right leg CAN buses** are merged into **one CAN route**.  
- **Left leg → CAN1**, **Right leg → CAN2** on STM32 board.  
- The **servo driver board** is connected via **UART2**.  

**Note:**  
- Refer to **PCB silkscreen** for **IO definitions**.  
- **TX on servo board → TX on control board**  
- **RX on servo board → RX on control board**  

**Diagram:**  
<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/20250409whiteboard(1).png" width="300" />

---

## 🤖 Head Installation  

After completing the **main body assembly**, proceed with **head installation**.  

<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/2025040902.png" width="300" /> 

Additionally, a **camera mount is available in the lower chest area**.  

<img src="https://github.com/Yuexuan9/Tinker/raw/main/docs/images/assemble/2025040903.png" width="300" />

---

## 🔧 Software Configuration  

After hardware assembly, refer to the **Tinker Software User Guide** for software setup.  
