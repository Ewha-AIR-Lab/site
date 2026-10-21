# ROS2 Security Patrol Robot

## Team

말차 Team

### Member

- Karina Bezverkhaia

---

## Project Description

This project implements an autonomous security patrol robot using ROS2.

The robot patrols an office environment, creates a map using SLAM, detects intruders, and generates alerts when a forbidden zone is violated.

---

## Features

### SLAM Mapping

- Cartographer
- Occupancy Grid Map

### Patrol

- Waypoint Patrol

### Human Detection

- OpenCV-based detection

### Alert System

- Intrusion Alert

### Mission Logger Node

Custom ROS2 node that records patrol events.

---

## ROS2 Nodes

### patrol_node

Controls robot patrol behavior.

### vision_node

Performs object detection.

### alert_node

Handles intrusion alerts.

### mission_logger_node

Stores mission logs and patrol events.

---

## Role Distribution

Karina Bezverkhaia

- Office world design
- SLAM mapping
- ROS2 node implementation
- Documentation

---

## AI Usage

ChatGPT was used for:

- ROS2 code assistance
- Documentation writing
- Debugging support

All implementation, testing, and integration were performed by the team.

---

## References

ROS2 Documentation:
https://docs.ros.org

Gazebo:
https://gazebosim.org

Cartographer:
https://google-cartographer.readthedocs.io

TurtleBot3:
https://emanual.robotis.com/docs/en/platform/turtlebot3

OpenCV:
https://opencv.org

---

## YouTube Link

https://youtu.be/yL8FB6wgd9w?si=R9-xYlT057h0Vil4
