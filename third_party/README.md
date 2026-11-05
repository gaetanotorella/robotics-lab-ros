# Third-party code

`iiwa_stack` is a copy of [IFL-CAMP/iiwa_stack](https://github.com/IFL-CAMP/iiwa_stack), under the BSD 2-Clause license
in [`iiwa_stack/LICENSE`](iiwa_stack/LICENSE), modified for the simulations of homeworks 2 and 3.

Differences from the original repository:

- **Added**
  - `iiwa_description/urdf/iiwa14.urdf` and `iiwa7.urdf`
  - `iiwa_gazebo/launch/`: `iiwa_gazebo_effort`, `iiwa_gazebo_circular_object`, `iiwa_gazebo_aruco`,
    `iiwa_gazebo_aruco_dynamic`, `iiwa_world_circular_object`, `iiwa_world_aruco`
  - `iiwa_gazebo/models/`: `aruco_marker` and `circular_object`
  - `iiwa_gazebo/worlds/`: `iiwa_aruco.world` and `iiwa_circular_object.world`
- **Modified**
  - `iiwa_control/config/iiwa_control.yaml`
  - `iiwa_description/launch/iiwa14_upload.launch`
  - `iiwa_description/urdf/iiwa14.xacro` and `iiwa.gazebo.xacro`
  - `iiwa_gazebo/launch/iiwa_world.launch`
  - `iiwa_gazebo/worlds/iiwa.world`
- **Removed**
  - `iiwa_ros_java`, the Java application for the real robot, not used in simulation
  - `.circleci` and `.clang-format`
