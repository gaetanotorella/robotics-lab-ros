# Vision-Based Control for a 7-DOF Manipulator

This project implements a **vision-based control task** for a 7-DOF robotic manipulator simulated in **ROS** and **Gazebo**, building upon the dynamic and kinematic tools provided by the **Kinematics and Dynamics Library (KDL)**. The robot is equipped with a simulated RGB camera, which is used to detect a visual target and regulate the end-effector motion so that the camera maintains a desired geometric relationship with respect to the observed object in the scene.

---

## Objective

The goal is to use visual feedback to guide the pose of the robot’s end-effector based on the image position of an object. The work proceeds through three phases:

1. **Scene construction and visual perception**  
   - A static colored circular object is introduced into the Gazebo environment.
   - The onboard camera mounted on the robot captures images of the object.
   - Image processing is carried out using OpenCV (via a ROS interface) to detect the object and provide its 2D location in the camera frame.

2. **Vision-based alignment control**  
   - The visual target is used to define a geometric reference direction in the camera frame.
   - The robot is controlled so that its camera aligns toward the object.
   - Both linear and angular alignment components are regulated in task space.

3. **Dynamic vision-based inverse dynamics control**  
   - The previously developed inverse dynamics controllers (joint-space and operational-space from Homework 2) are combined with the visual alignment task.
   - The robot is commanded to track spatial trajectories while simultaneously maintaining visual alignment.
   - Performance is evaluated in terms of Cartesian tracking error and commanded torques.

---

## Environment and Modeling

- The simulation environment uses the **Gazebo** physics engine.
- The robot model is based on the **KUKA iiwa**, controlled through standard ROS control interfaces.
- A custom **world** file is created to introduce the target object at a fixed location.
- Object detection is performed by processing the simulated camera feed using **OpenCV**.
- Task kinematics and dynamics rely on **KDL** for:
  - Forward and inverse kinematics
  - Jacobian computation
  - Dynamic model estimation (inertia, Coriolis, gravity)

---

## Vision-Based Task

The task relies on interpreting the detected object as a **point or direction** in the camera coordinate frame.  
The control objective is formulated as:

- Maintain the camera optical axis aligned with the object.
- Optionally impose a fixed relative displacement (offset) to achieve a desired viewing position.

This is a **visual servoing strategy** operating in **Cartesian space**, where the robot motion is generated to reduce the geometric error in the camera frame.

An extended formulation considers the **unit-normalized viewing direction**, allowing the task to be represented on the **sphere (S²)**.  
This enables control strategies that exploit the geometry of directional constraints and null-space projections.

---

## Combined Dynamic Control

The project merges:
- **Vision-based task regulation** (task space alignment)
- **Inverse dynamics control** (joint or operational space tracking)

This results in a controller that:
- Executes linear or circular spatial trajectories
- Ensures the camera maintains alignment with the object during motion
- Uses torque-level commands consistent with the underlying robot dynamics

Performance analysis is carried out by:
- Monitoring commanded joint efforts
- Computing time evolution of Cartesian error norms
- Comparing results across trajectory types and control schemes

---

## Evaluation and Results

- The robot successfully aligns its camera with the object during static and dynamic motion.
- The **S²-based formulation** provides improved directional stability and null-space exploitation.
- The dynamic controller enables smooth torque behavior and stable tracking of the end-effector trajectory while maintaining visual alignment.
- Plots of:
  - Cartesian error norms (position and orientation)
  - Joint torque commands
  demonstrate correct convergence and feasible control effort.

---

## Dependencies

- **ROS**
- **Gazebo**
- **KDL (Kinematics and Dynamics Library)**
- **OpenCV** (via ROS image transport and cv_bridge)
- **iiwa** ROS model and controllers
- **rqt_image_view** and **rosbag** (for visualization and logging)
- **MATLAB** (optional, for offline signal and torque analysis)

---

## Demo Video

### Circular Trajectory
[cicular_trajectory.webm](https://github.com/user-attachments/assets/c1ab27cd-d385-4cbe-b371-16cdc678c41c)

### Fixed Relative Displacement mooving the object
[fixed_relative_displacement.webm](https://github.com/user-attachments/assets/7253b493-935f-4201-8086-c2c3c23dd125)
