# UR5 Pick and Place with PyBullet Simulation

This repository contains a robotic pick-and-place implementation using a UR5 robot arm with a Robotiq gripper in PyBullet simulation. The system uses computer vision and pose estimation for object manipulation.

## Environment Setup

### Dependencies
Create a conda environment using the provided `environment.yaml`:
```bash
conda env create -f environment.yaml
```

This will set up a Python 3.9 environment with the following key dependencies:
- PyBullet 3.21
- NumPy 1.23.5
- OpenCV 4.5.5
- Trimesh 4.0.4
- Additional scientific computing and computer vision libraries

## Project Structure

### Main Components

- `env.py`: Contains the `UR5PickEnviornment` class that manages the PyBullet simulation environment
- `pose_based_pnp.py`: Main script for running pick-and-place operations
- `preception.py`: Implements pose estimation methods using state information and ICP
- `environment.yaml`: Conda environment configuration file

### Key Features

1. **Simulation Environment** (`env.py`):
   - UR5 robot arm with Robotiq gripper
   - Configurable workspace with two totes
   - Top-down camera for perception
   - YCB object loading and manipulation
   - Grasp execution and planning

2. **Pose Estimation** (`preception.py`):
   - Ground truth state-based pose estimation
   - ICP-based pose estimation using depth images
   - Point cloud processing and alignment

3. **Pick and Place Pipeline** (`pose_based_pnp.py`):
   - Object detection and pose estimation
   - Grasp pose computation
   - Pick and place execution
   - Visual feedback with matplotlib

## Usage

Run the pick and place system with:

```bash
# Run with state-based pose estimation
python pose_based_pnp.py --use_state

# Run with ICP-based pose estimation
python pose_based_pnp.py

# Check simulation environment setup
python pose_based_pnp.py --check_sim
```

### Command Line Arguments
- `--use_state`: Use ground truth state for pose estimation
- `--check_sim`: Run simulation environment check without pick and place execution

## Implementation Details

### UR5 (with 140 gripper) Robot Control
- Joint position control with trajectory planning
- IK-based end-effector pose control
- Gripper control with force feedback

### Vision System
- 128x128 resolution camera, pictured from top of source bin
- Depth and RGB imaging passed to UNET model
- Mask-based object segmentation and pose estimation using ICP

### Grasp Planning
- Top-down grasping strategy
- Object pose to grasp pose conversion
- Success detection based on gripper state

## Debug Features
- Point cloud visualization in PLY format
- Visual feedback during execution
- Simulation state inspection

## Notes
- The system uses a fixed offset for z-axis pose estimation due to partial observation limitations
- The camera is mounted in a top-down configuration for better object visibility
- Grasp success is determined by gripper joint positions
- Debug visualizations are saved in a `./debug` directory


