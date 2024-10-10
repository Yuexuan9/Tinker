# Tinker: An Open-Source Bipedal Robot

## Key Features:
- **Reinforcement Learning-Based Control**: Tinker primarily operates using reinforcement learning.
- **Step-by-Step Assembly Instructions**: Detailed instructions, including hardware assembly, software setup, and motor configuration.
- **Customization and Expansion**: Comprehensive resources for further development and integration with external sensors and controllers.

## Recommended Setup and Debugging Steps for Tinker:
1. **Prepare Materials**: Follow the Tinker BOM checklist.
2. **Configure Odroid Operating System**.
3. **Flash STM32 Firmware**.
4. **Configure STM32 Parameters**.
5. **Download and Configure Odroid Motion Control Program** and set up auto-start.
6. **Motor Configuration**: Modify motor ID and parameters.
7. **Servo Configuration**: Reset servo IDs to 0.
8. **Assemble Tinker V1**: Follow the Tinker V1 assembly guide.
9. **Gait Test - Leg Retraction**.
10. **Run RL Model**: Set up training and deployment environment.
11. **Gait Test - RL Server Mode**.
12. **Configure Jetson Nano Deployment Environment**.
13. **Gait Test - Onboard RL Mode**.
14. **Further Development**: Explore Tinker's extensibility with external sensors and hardware.

## Odroid Controller System Configuration

This guide provides the steps to install the 5.10 RT kernel on the Odroid C4 for real-time communication with the STM32 control board. The steps involve downloading the required image, burning it to an SD card, updating the system, and installing the necessary development tools.

### Requirements
- Odroid C4
- SD card (at least 16GB)
- Ethernet connection (Odroid C4 does not have built-in Wi-Fi)
- Access to a router for IP configuration

### Steps

  ### 1. Download and Install the RT Kernel Image
  To set up the system, use the provided instructions to install the RT real-time patch for the 5.10 kernel version. Reference [this forum post](https://forum.odroid.com/viewtopic.php?f=55&t=41129) for more details.
  
  Since the RT patch is only compatible with the 5.10 kernel version, you will need to download the 1218 version of the image (as the original post linked the 5.11 version, which is not supported). 
  
  Download the image from the following URL:
  [http://ppa.linuxfactory.or.kr/images/raw/arm64/focal/](http://ppa.linuxfactory.or.kr/images/raw/arm64/focal/)
  
  Once downloaded, burn the image to your SD card and insert it into the Odroid system.
  
  ### 2. Default Login Credentials
  - **Username:** `odroid`
  - **Password:** `odroid`
  
  ### 3. Update the System and Install Basic Tools
  Since the system is a server version without any pre-installed network or text editing tools, you need to update the system and install essential development tools. Here’s how to do it:

  - **Download and Install the RT Kernel Image**  
      To set up the system, use the provided instructions to install the RT real-time patch for the 5.10 kernel version. Reference [this forum post](https://forum.odroid.com/viewtopic.php?f=55&t=41129) for more details.  
      Since the RT patch is only compatible with the 5.10 kernel version, you will need to download the 1218 version of the image (as the original post linked the 5.11 version, which is not supported).
  
      Download the image from the following URL:  
      [http://ppa.linuxfactory.or.kr/images/raw/arm64/focal/](http://ppa.linuxfactory.or.kr/images/raw/arm64/focal/)
  
      Once downloaded, burn the image to your SD card and insert it into the Odroid system.

  - **Default Login Credentials**
    Username: `odroid`
    Password: `odroid`

  - **Update the System and Install Basic Tools**  
    Since the system is a server version without any pre-installed network or text editing tools, you need to update the system and install essential development tools. Here’s how to do it:

    1. **Update the package list:**
       ```bash
       sudo apt update
       sudo apt dist-upgrade
       ```

    2. **Install the 5.10 RT kernel:**
       ```bash
       sudo apt install linux-image-5.10.0-odroid-rt-arm64
       sudo reboot
       ```

    3. **Verify the RT Kernel:**  
       After reboot, check if the RT kernel is running:
       ```bash
       uname -a
       ```
       You should see output similar to:  
       ```
       Linux focal-server 5.10.0-odroid-rt-arm64 #1 SMP PREEMPT_RT Ubuntu 5.10.0-202012062208~focal (2020-12-06) aarch64 aarch64 aarch64 GNU/Linux
       ```

  - **Install Development Tools**  
    Now, install the necessary development tools such as `nano`, `ifconfig`, `cmake`, and others:
    ```bash
    sudo apt-get install g++
    sudo apt-get install cmake
    sudo apt install net-tools
    ```

  - **Network Setup (For Ethernet)**  
    Since Odroid C4 does not have built-in Wi-Fi and lacks `ifconfig` to check its IP, you can use a router in relay mode to set up the network. After connecting the Ethernet cable, the system should obtain an IP address automatically.

---

Following these steps will set up your Odroid C4 with the real-time kernel and necessary tools to start working on your robotics projects.
```
