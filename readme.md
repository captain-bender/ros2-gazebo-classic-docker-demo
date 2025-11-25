# ROS 2 Humble with Gazebo Classic - Docker Development Environment

A complete Docker-based development environment for ROS 2 Humble with Gazebo Classic, optimized for Windows 11 with VS Code integration.

## Prerequisites

- Windows 11
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (with WSL2 backend)
- [VcXsrv Windows X Server](https://sourceforge.net/projects/vcxsrv/)
- [Visual Studio Code](https://code.visualstudio.com/)
- VS Code Extension: [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Features

- **ROS 2 Humble Desktop Full** - Complete ROS 2 installation
- **Gazebo Classic 11** - Traditional Gazebo simulator
- **RViz2** - 3D visualization tool
- **Full Development Tools** - Git, CMake, GDB, Python linting/formatting
- **VS Code Integration** - Seamless development experience with IntelliSense

## Quick Start

### 1. Setup X Server (VcXsrv)

1. Launch **XLaunch** from Start menu (or install from [SourceForge](https://sourceforge.net/projects/vcxsrv/))
2. Configure settings:
   - Display: **Multiple windows**, Display number: **0**
   - Client startup: **Start no client**
   - Extra settings: **☑ Disable access control** (Important!)
3. Click Finish
4. **Keep VcXsrv running** (you'll see it in system tray)
5. Select to save the configuration, and next time double-click to the config file in order to start automatically.

### 2. Build Docker Image
```bash
docker build -f Dockerfile.classic -t ros2-humble-gazebo-classic:dev .
```

### 3. Open the container
For the first time run the ps1 file and start your container in the powershell. When you want to terminate its operation press CTRL+D.

Then you can use the VS code:

1. Open this folder in VS Code
2. Press `F1` or `Ctrl+Shift+P`
3. Type: **"Dev Containers: Reopen in Container"**
4. Wait for container to build and start

You're now inside the container!

## Usage

### Testing the Setup

Open a terminal in VS Code and test:
```bash
# Test X server connection
xclock

# Launch RViz2
rviz2

# Launch Gazebo Classic
gazebo

# Launch Gazebo with ROS 2 integration
ros2 launch gazebo_ros gazebo.launch.py
```

### Creating Your First Package
```bash
# Navigate to source directory
cd src

# Create a Python package
ros2 pkg create --build-type ament_python my_robot_package --dependencies rclpy

# Or create a C++ package
ros2 pkg create --build-type ament_cmake my_robot_cpp --dependencies rclcpp

# Build the workspace
cd ..
colcon build

# Source the workspace
source install/setup.bash

# Run your node
ros2 run my_robot_package my_node
```

### Working with Gazebo Classic
```bash
# Launch empty world
gazebo

# Launch with specific world
gazebo worlds/willowgarage.world

# Spawn a model
ros2 run gazebo_ros spawn_entity.py -entity my_robot -file model.sdf

# List Gazebo topics
ros2 topic list | grep gazebo
```

### Common ROS 2 Commands
```bash
# List nodes
ros2 node list

# List topics
ros2 topic list

# Echo a topic
ros2 topic echo /topic_name

# Show topic info
ros2 topic info /topic_name

# Run rqt (graphical tools)
rqt

# View TF tree
ros2 run tf2_tools view_frames
```

## Returning to Local Environment

To exit the container and return VS Code to local:

1. Press `F1` or `Ctrl+Shift+P`
2. Type: **"Dev Containers: Reopen Folder Locally"**

Or simply close VS Code and reopen normally.

## Performance Tips

- **For better Gazebo performance**: Consider using the Gazebo Fortress version
- **Reduce simulation load**: Use simpler models and worlds
- **Split workload**: Run Gazebo headless, visualize with RViz2
- **Allocate more resources**: Docker Desktop → Settings → Resources

## License

This project is provided as-is for educational and development purposes.

## Contributing

Feel free to submit issues and enhancement requests!
