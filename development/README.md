# Tinker
## Flexible, and Ready to Move: Your Cartoon-Style Bipedal Robot! 

Tinker is driven by reinforcement learning, where neural networks execute gaits, achieving stable walking and standing. During testing, software is required to train the neural network. 

## Acknowledgements
This project is based on the original code from [LocomotionWithNP3O](https://github.com/zeonsunlightyu/LocomotionWithNP3O). Special thanks to the contributors of the original repository for their work and contributions.

**Performance on the real robot**: Please check out the link below:  
[Code Repository Update Series 1: Check it out! GitHub: LocomotionWithNP3O - Bilibili](https://b23.tv/haLM4jg)

## Coordinate System Definition
First, export the URDF and use RViz to review the coordinate system and angles, mainly to increase joint limits, angular velocities, and maximum torque. The URDF and XML files for Tinker are as follows:  
Content not available outside Feishu documents.

To view the URDF in RViz, use the following command:
```bash
roslaunch urdf_tutorial display.launch model:=/home/pi/Downloads/LocomotionWithNP3O-master/resources//tinker/urdf/tinker_urdf.urdf
```

## Environment Setup
Follow the commands below to set up the environment, and refer to online tutorials to install IsaacGym in the virtual environment:
```bash
conda create -n Tinker python=3.8.10
conda activate Tinker
pip install torchvision -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install torch -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pyquaternion -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pyyaml -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install rospkg -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pexpect -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install mujoco==2.3.7 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install mujoco-py -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install mujoco-python-viewer -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install dm_control==1.0.14 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install opencv-python -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install einops -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install tqdm -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install packaging -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install h5py -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install ipython -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install getkey -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install wandb -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install chardet -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install numpy==1.23.2 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install h5py_cache -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install opencv-python -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install tensorboard -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install lcm -i https://pypi.tuna.tsinghua.edu.cn/simple
```

Download IsaacGym from the official website:
```bash
cd isaccgym/python && pip install -e .
```

Activate the virtual environment:
```bash
conda activate Tinker
```

Add shortcuts to `.bashrc` for refreshing environment variables:
```bash
alias sd="source devel/setup.bash"
alias ss="source ~/.bashrc"
alias a1="conda activate Tinker"
```

## Software Usage

### Train the Model:
After setting up the environment and activating the virtual space, run the script for training:
```bash
python train.py
```
The trained model will be updated here:  
![Image6](#)

To test the model, first modify the model file used in `simple_play.py`:
```python
model_dict = torch.load(os.path.join(ROOT_DIR, '/home/pi/Downloads/back_good/LocomotionWithNP3O-masteroldx/logs/rough_go2_constraint/Oct09_10-35-52_test_barlowtwins/model_3000.pt'))
```
Then run the script:
```bash
python simple_play.py
```

### Sim2Sim Testing
After training with Isaac, the model must be transferred. Sim2Sim involves building a framework on the controller side to run the neural network and feed the necessary feedback data. Using the Human-Gym as a reference, Mujoco simulator enables Sim2Sim transfer. For real-world transfer, additional software in C++ may be required. Typical transfer frameworks can be:
- **a. Using Mujoco Python/C++ simulation**: Embedding the network I/O in the Mujoco interface, preferred for semi-physical transfer.
- **b. Using Mujoco C++ simulation with LCM/ROS**: Running the Mujoco simulation asynchronously, interacting with C++ and Pytorch via LCM, suited for real-world transfer.

Before transfer, ensure the `default_dof_pos` matches the Isaac simulation:
```python
default_dof_pos = [0.0,-0.0,0.56,-1.12,0.57,0.0,0.0,0.56,-1.12,0.57]
```
Match the model path:
```bash
parser.add_argument('--load_model', type=str, default='/home/pi/Downloads/LocomotionWithNP3O-masteroldx/modelt.pt')
```
Update KP and KD to match training:
```python
class robot_config:
    kp_all = 9.0
    kd_all = 0.6
    kps = np.array([kp_all]*10, dtype=np.double)
    kds = np.array([kd_all]*10, dtype=np.double)
    tau_limit = 12. * np.ones(10, dtype=np.double)
```
Then run the transfer script:
```bash
python sim2sim_tinker.py
```

### Prototype Inference Test
For prototype testing, connect the robot to the training server via Ethernet, or deploy the model on Jetson Nano for edge deployment.

First, compile the `sim2sim_lcm` build folder, ensuring that **libtorch** and **cuDNN** are installed. Then, modify the `udp_publisher_tinker.cpp` to set the robot's IP address:
```cpp
string UDP_IP="192.168.1.242";
int SERV_PORT= 10000;
```
Modify the model path:
```cpp
model_path = "/home/pi/Downloads/back_good/LocomotionWithNP3O-master/model_jitt.pt";
load_policy();
```
Run the publisher:
```bash
./udp_publisher_tinker
```

### Robot Operation
Once the model is trained, the robot assembled, and the migration software compiled, gait testing can begin.

1. **Power on the robot**: Ensure joint calibration is done. Lift the robot in a vertical leg position and press the X button. The robot should squat and lock into place.
   - In case of issues, press ↓ to cut power.

2. **Start the RL Program**: Activate the transfer software on the server or Jetson Nano, and confirm data refresh.

3. **Gait Driving**: In standing mode, press X to drive the robot using RL data. The left joystick controls XY velocity, the rear triggers control heading, and the right joystick adjusts head position. Press B to return to standing lock mode, and ↓ to cut power.
```
