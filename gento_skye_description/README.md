# Gento Skye Description

轮式人形 **Gento Skye**：Linkhou S2 v2 底盘 + 3-DOF 腰（升降/俯仰/偏航）+ Tianji **M6-CCS** 双臂 + Skye 2-DOF 头。

组件来自本包与 `fiveages_w2_common_description`。末端键与 `m6_ccs` 相同。

```bash
cd ~/ros2_ws
colcon build --packages-up-to gento_skye_description --symlink-install
source install/setup.bash
```

## Visualize

```bash
ros2 launch robot_common_launch humanoid.launch.py robot:=gento_skye collider:=simple
ros2 launch robot_common_launch component.launch.py robot:=gento_skye type:=head
ros2 launch robot_common_launch component.launch.py robot:=gento_skye type:=waist
ros2 launch robot_common_launch component.launch.py robot:=gento_skye type:=body
```

`type:=body` 为腰 + 头。组件默认 `isaac:=true`（不显示相机等 sensor mesh）；要看传感器外形时传 `xacro_isaac:=false`：

```bash
ros2 launch robot_common_launch component.launch.py robot:=gento_skye type:=body xacro_isaac:=false
```

带末端：`type:=rg75`（键名见 m6_ccs README）。

## Control

```bash
ros2 launch ocs2_arm_controller demo.launch.py robot:=gento_skye
ros2 launch ocs2_arm_controller split_body.launch.py robot:=gento_skye
ros2 launch ocs2_arm_controller full_body.launch.py robot:=gento_skye
```

默认 `hardware:=mock_components`。

分体：臂 `ocs2_arm_controller`（home 与 M6-CCS 相同）+ 腰 `body_joint_controller` + 头 `head_joint_controller`。  
全身：`ocs2_wbc_controller`，腰/臂/头与分体同一套 home 对齐。

| Home | 腰 `[lift, pitch, yaw]` | 臂 |
|------|-------------------------|-----|
| 1 | `[0.30, 0, 0]` 作业高度直立 | M6-CCS 预备 |
| 2 | `[0.50, -0.35, 0]` 升高前倾 | M6-CCS 收拢 |
| 3 | `[0.15, 0, 0]` 偏低 | M6-CCS 预备 |
| 4 | `[0, 0, 0]` 最低 | ±90° 肩肘 |
