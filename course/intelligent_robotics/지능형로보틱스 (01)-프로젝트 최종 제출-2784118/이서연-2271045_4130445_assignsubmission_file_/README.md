# ROS2 기반 고속버스터미널 자율주행 안내 로봇

## 1-1. 팀 정보, 프로젝트 설명

### 팀명
- 내내

### 팀원
- 이서연(2271045)

---

## 1-2. 프로젝트 설명

이 프로젝트는 고속버스터미널에서 이용자가 원하는 버스 승차홈을 쉽게 찾을 수 있도록 돕는 ROS2 기반 자율주행 안내 로봇 시스템이다.

고령자, 초행 이용자, 짐이 많은 이용자처럼 복잡한 터미널 환경에서 이동에 어려움을 겪는 사람들에게 더 직관적인 승차 안내를 제공하는 것을 목표로 한다. 승객이 원하는 버스(색상으로 구분)를 선택하면 로봇이 해당 버스 정류장까지 자율 주행하여 안내한다. 

시뮬레이션 환경은 Gazebo에서 구현했고, 로봇은 LiDAR를 이용해 장애물을 감지하고 Nav2를 통해 경로를 계획하며 이동한다. 또한 RGB 카메라를 활용해 버스 색상을 인식하고, GUI를 통해 사용자가 원하는 버스를 선택할 수 있도록 구성했다.

---

## 2. AI 사용 여부 및 사용 내용

이 프로젝트에서는 ROS2 Gazebo 환경 구축과 오류 해결 과정에서 **Claude Code**를 활용하였다.

주요 활용 내용은 다음과 같다.

- 패키지 설치 오류 해결
- 워크스페이스 구조 확인
- 빌드 과정에서 발생한 에러 메시지 해석
- 개발 환경 설정 및 디버깅 보조

---

## 3. 참고 자료

- [ROS2 센서 데이터 처리 - 이미지, 거리, 모션 분석](https://wikidocs.net/300861)
- [ROS 2 Humble Documentation](https://docs.ros.org/en/humble/)
- [Robotics Backend - ROS2](https://roboticsbackend.com/category/ros2/)
- [Ultralytics YOLO Detection/Tracking](https://docs.ultralytics.com/tasks/detect/)
- [ROS 2로 시작하는 로봇 프로그래밍](https://www.yes24.com/product/goods/102949767)
- [실내, 실외 자율주행 로봇 프로젝트](https://kimbrain.tistory.com/410)

---

## 4. YouTube 링크

https://youtu.be/brR_PzgY52o

---
