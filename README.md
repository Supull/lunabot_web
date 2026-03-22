# TurtleSim Web Controller

> A browser-based ROS robot controller built as a learning platform for **Tennessee NASA Lunabotics** — bridging web interfaces and ROS before deploying to the real thing.

---

## Overview

This project is a lightweight, educational web controller for [TurtleSim](http://wiki.ros.org/turtlesim), the classic ROS simulation environment. It serves as a **proof-of-concept and learning sandbox** for the Tennessee NASA Lunabotics team, exploring how to connect a browser UI to a ROS robot using [roslibjs](https://github.com/RobotWebTools/roslibjs) and [rosbridge](https://github.com/RobotWebTools/rosbridge_suite).
The goal: master web-to-ROS communication in a safe, simulated environment — then apply those patterns to control the actual Lunabotics robot.

---

## Features

- **Real-time robot control** — Move forward, backward, rotate left/right via browser buttons
- **Live pose telemetry** — Subscribe to `/turtle1/pose` and display `x`, `y`, and `theta` in real time
- **WebSocket communication** — Connects to a local rosbridge server over `ws://localhost:9090`
- **Zero-dependency frontend** — Pure HTML/JS, no build tools required

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Robot Simulator | [TurtleSim (ROS)](http://wiki.ros.org/turtlesim) |
| ROS <-> Web Bridge | [rosbridge_suite](https://github.com/RobotWebTools/rosbridge_suite) |
| Browser ROS Client | [roslibjs](https://github.com/RobotWebTools/roslibjs) |
| Frontend | Plain HTML + JavaScript |

---

## Prerequisites

- ROS (Noetic or your target distro) installed and sourced
- `turtlesim` package
- `rosbridge_suite` package

```bash
sudo apt install ros-<distro>-rosbridge-suite
sudo apt install ros-<distro>-turtlesim
```

---

## Getting Started

### 1. Launch ROS Core
```bash
roscore
```

### 2. Start TurtleSim
```bash
rosrun turtlesim turtlesim_node
```

### 3. Start the rosbridge WebSocket Server
```bash
roslaunch rosbridge_server rosbridge_websocket.launch
```
> This starts a WebSocket server on `ws://localhost:9090` that the browser connects to.

### 4. Open the Web Controller

Open `index.html` directly in your browser (no server needed):
```bash
xdg-open index.html # Linux
open index.html # macOS
```
---

## Usage

Once connected, you'll see the controller in your browser:

| Button | ROS Topic | Action |
|--------|-----------|--------|
| **Move Forward** | `/turtle1/cmd_vel` | `linear.x = +1` |
| **Move Backward** | `/turtle1/cmd_vel` | `linear.x = -1` |
| **Rotate Left** | `/turtle1/cmd_vel` | `angular.z = +1` |
| **Rotate Right** | `/turtle1/cmd_vel` | `angular.z = -1` |

The live pose display updates continuously from the `/turtle1/pose` topic, showing real-time `x`, `y`, and heading (`theta`).

---

## ROS Topics

| Topic | Message Type | Direction |
|-------|-------------|-----------|
| `/turtle1/cmd_vel` | `geometry_msgs/Twist` | Publish (browser → ROS) |
| `/turtle1/pose` | `turtlesim/Pose` | Subscribe (ROS → browser) |

---

## Contributing

This is a learning project — contributions, experiments, and improvements are welcome! If you're on the UT Lunabotics team, open a PR or start a discussion.
