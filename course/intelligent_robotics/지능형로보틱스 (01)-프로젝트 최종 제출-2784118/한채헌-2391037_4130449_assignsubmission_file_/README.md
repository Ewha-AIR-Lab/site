# Camera-Based BEV Occupancy Map Generation and Autonomous Mobile Robot System

## 1. 팀 정보

- 팀명: F40
- 팀원: 2391037 한채헌

## 2. 프로젝트 설명

본 프로젝트는 RGB-D 카메라의 Depth 정보를 이용하여 실내 환경의 장애물을 인식하고, 이를 Bird's Eye View(BEV) Occupancy Map으로 변환한 뒤 ROS2 Nav2 기반 자율주행에 활용하는 로봇 시스템이다.

Gazebo 시뮬레이션 환경에서 TurtleBot3 Waffle 로봇에 RGB-D 카메라를 장착하고, 카메라로부터 들어오는 Depth 이미지를 전처리하여 3D 포인트로 변환한다. 이후 robot coordinate로 변환한 뒤 높이 필터링과 2D 투영을 수행하여 BEV Occupancy Grid와 PointCloud를 생성한다.

생성된 BEV 정보는 Nav2의 local costmap에 반영되어 로봇이 실시간 장애물을 회피하며 목표 지점까지 이동할 수 있도록 한다. 전체 시스템은 ROS2 Humble, Gazebo, RViz2, SLAM Toolbox, Nav2를 연동하여 구현하였다.


## 3. AI 사용 여부 및 사용 내용

- AI 사용 여부: 사용함
- 사용 도구: Claude code
- 사용 내용:
  - 프로젝트 폴더 구성 방향 정리
  - Depth 이미지 기반 BEV Occupancy Grid 변환 로직 검토
  - Nav2, Gazebo, RViz2 연동 오류 해결 보조


## 4. 참고 자료

- ROS2: https://docs.ros.org/
- Nav2: https://docs.nav2.org/
- TurtleBot3 e-Manual: https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/
- Gazebo: https://gazebosim.org/docs
- SLAM Toolbox GitHub: https://github.com/SteveMacenski/slam_toolbox
- Navigation2 GitHub: https://github.com/ros-navigation/navigation2
- BEVFormer: Learning Bird’s-Eye-View Representation from Multi-Camera Images via Spatiotemporal Transformers (ECCV 2022): https://arxiv.org/pdf/2203.17270

## 5. YouTube 링크

- https://youtu.be/69l4I_MiCdY
데모 영상 부분에서 좌측 상단 이미지는 실시간으로 변하는 bev map을 시각화한 것이다.

## 6. GitHub 링크

- https://github.com/chehun16/ROS2-2026

