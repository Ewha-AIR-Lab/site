# ROS2 기반 실내 자율 배송 로봇 시스템 구현

### Implementation of an Autonomous Indoor Delivery Robot using ROS2

## 1. 팀 정보

* 학과 : 이화여자대학교 인공지능학과
* 학번 : 2277042
* 이름 : 안다희

---

## 2. 프로젝트 소개

본 프로젝트는 ROS2 기반 모바일 로봇인 TurtleBot3를 활용하여 실내 환경에서 자율 배송 시스템을 구현하는 것을 목표로 한다.

프로젝트의 최종 목표는 사용자가 목적지를 입력하면 로봇이 스스로 경로를 계획하고 목적지까지 이동하는 자율 배송 시스템을 구현하는 것이다.

이번 프로젝트에서는 Gazebo 시뮬레이션 환경을 구축하고, Cartographer SLAM을 이용하여 실시간 지도를 생성하는 기능을 구현하였다. 또한 teleop_keyboard를 이용하여 로봇을 직접 제어하면서 LiDAR 데이터를 수집하고 Occupancy Grid Map을 생성하였다.

---

## 3. 프로젝트 목표

* Gazebo 기반 실내 시뮬레이션 환경 구축
* TurtleBot3 모바일 로봇 실행
* Cartographer SLAM을 이용한 지도 생성
* Occupancy Grid Map 저장 및 확인
* 향후 AMCL Localization 구현
* 향후 Nav2 기반 자율주행 및 배송 기능 구현

---

## 4. 사용 기술

* ROS2 Humble
* Gazebo Simulator
* TurtleBot3 Burger
* Cartographer SLAM
* RViz2
* teleop_keyboard

---

## 5. 시스템 구성

```text
Gazebo Environment
        ↓
TurtleBot3 Spawn
        ↓
teleop_keyboard
        ↓
LiDAR Data Acquisition
        ↓
Cartographer SLAM
        ↓
Occupancy Grid Map
        ↓
Map Save
(my_map.pgm, my_map.yaml)
```

---

## 6. 실행 방법

### 1) Gazebo 실행

```bash
export TURTLEBOT3_MODEL=burger

ros2 launch turtlebot3_gazebo world.launch.py
```

### 2) Cartographer SLAM 실행

```bash
export TURTLEBOT3_MODEL=burger

ros2 launch turtlebot3_cartographer \
cartographer.launch.py \
use_sim_time:=true
```

### 3) Teleop Keyboard 실행

```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

### 4) 생성된 지도 확인

```bash
eog my_map.pgm
```

---

## 7. 결과

프로젝트 수행 결과 다음 파일이 성공적으로 생성되었다.

* my_map.pgm
* my_map.yaml

생성된 지도는 Occupancy Grid Map 형태로 저장되며,

* 검정색 : 벽 및 장애물
* 흰색 : 이동 가능한 영역

을 의미한다.

Gazebo 환경에서 TurtleBot3를 조작하며 실시간으로 지도를 생성하는 과정을 확인할 수 있었다.

---

## 8. 역할 분담

개인 프로젝트

* Gazebo 시뮬레이션 환경 구축
* TurtleBot3 실행 및 설정
* Cartographer SLAM 실행
* teleop_keyboard를 이용한 로봇 제어
* Occupancy Grid Map 생성 및 결과 확인
* 발표 자료 제작 및 데모 영상 제작

---

## 9. AI 사용 여부 및 사용 내용

### AI 사용 여부

사용함

### 사용 내용

* ChatGPT를 이용한 발표 자료(PPT) 구성 아이디어 정리
* README 문서 초안 작성
* 발표 대본 작성 및 문장 다듬기
* 프로젝트 설명 및 ROS2 관련 개념 정리

---

## 10. 참고 자료

### ROS2

* https://docs.ros.org/en/humble/

### TurtleBot3 e-Manual

* https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/

### Cartographer SLAM

* https://google-cartographer.readthedocs.io/

### Gazebo

* https://gazebosim.org/home

### Navigation2 (Nav2)

* https://docs.nav2.org/

---

## 11. YouTube 발표 영상

https://www.youtube.com/watch?v=rZ8iJHdLa34


```
```
