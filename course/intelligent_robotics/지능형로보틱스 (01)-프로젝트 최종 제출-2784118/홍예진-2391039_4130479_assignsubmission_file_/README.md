# OpenCV HSV 기반 손님 자동 인식 자율 서빙 로봇 시스템

## 1. 프로젝트 팀 및 멤버 소개
* **[클로버]** 인공지능학과 2391039 홍예진

## 2. 프로젝트 설명
본 프로젝트는 주문 정보와 연동된 카메라 기반 객체 인식을 통해, 좌석에서 대기 중인 손님들 중 올바른 손님을 자동으로 식별하고 음식을 서빙하는 로봇 시스템을 ROS2 Gazebo Simulation 환경에서 구현하는 것을 목표로 합니다.
* **주요 기능:** 
    * ROS2 노드 간 토픽 통신으로 주문 접수부터 조리, 픽업, 서빙, 복귀까지의 전체 서빙 흐름 자동화
  * 카메라 기반 색상 감지(OpenCV HSV)를 통한 손님 좌석 자동 식별
  * SLAM 및 Nav2 기반 자율주행 (pickup → scan → 서빙 → 복귀 자동화)

## 3. AI 사용 여부 및 사용 내용
본 프로젝트는 **Claude (Anthropic)**를 활용하여 개발되었습니다.
* **AI 활용 내용:**
  * 환경 구성 및 일부 노드 작성 (`restaurant.sdf`,`order_node.py`, `kitchen_node.py`
  * 발생 오류 디버깅 (SLAM 드리프트, Nav2 경로 실패, 오탐지 문제 등)

## 4. 참고 자료
* **실습 코드:** 01_basics~08_extra (GitHub: Ewha-AIRLab/intelligent-robotics-ros2)
* **튜토리얼 및 레퍼런스:**
  * How to Use YOLOv8 with ROS2: https://www.youtube.com/watch?v=XqibXP4lwgA
  * ROS2 Nav2 Tutorial: https://roboticsbackend.com/ros2-nav2-tutorial/
  * 유사 사례(사내 카페 서빙 로봇): https://github.com/Hyuna319/office_cafe_servingbot
  * (YOLO) Gazebo Fuel 모델: https://app.gazebosim.org/fuel/models

## 5. 데모 영상 및 링크
* **YouTube 링크** 
  * https://youtu.be/BIJlacqeA-U (발표 영상)
  * https://youtu.be/GLN1vF51s7U (데모 영상)