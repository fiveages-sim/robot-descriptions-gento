# Gento Luna Description

轮式人形 **Gento Luna**：Linkhou S2 v2 底盘 + 6-DOF 躯干 + Tianji **M6S Lite CCS** 双臂 + Luna 2-DOF 头。

组件来自本包与 `fiveages_w2_common_description`。第一期末端仅为 `left_tcp` / `right_tcp`。

```bash
cd ~/ros2_ws
colcon build --packages-up-to gento_luna_description --symlink-install
source install/setup.bash
```

## Visualize

```bash
ros2 launch robot_common_launch humanoid.launch.py robot:=gento_luna collider:=simple
ros2 launch robot_common_launch component.launch.py robot:=gento_luna type:=head
ros2 launch robot_common_launch component.launch.py robot:=gento_luna type:=torso
```

## Control

```bash
ros2 launch ocs2_arm_controller demo.launch.py robot:=gento_luna
ros2 launch ocs2_arm_controller split_body.launch.py robot:=gento_luna
ros2 launch ocs2_arm_controller full_body.launch.py robot:=gento_luna
```

默认 `hardware:=mock_components`。

分体：臂 `ocs2_arm_controller`（home 参考 M6-CCS）+ 躯干 `body_joint_controller` + 头 `head_joint_controller`。  
全身：`ocs2_wbc_controller`，躯干/臂/头与分体同一套 home 对齐。

| Home | 躯干 `[j1…j6]` | 臂 |
|------|----------------|-----|
| 1 | 直立零位 | M6-CCS 预备 |
| 2 | `[0, 0.40, -0.80, 0.40, 0, 0]` 下蹲 | M6-CCS 收拢 |
| 3 | `[0, 0.20, -0.40, 0.20, 0, 0]` 浅蹲 | M6-CCS 预备 |
| 4 | 直立零位 | ±90° 肩肘 |
