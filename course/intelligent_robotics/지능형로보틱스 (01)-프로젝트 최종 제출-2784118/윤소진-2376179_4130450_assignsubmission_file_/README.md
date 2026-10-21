# 안경 탐색 및 전달 로봇 (Glasses Detection & Delivery Robot)

26-1 지능형 로보틱스 프로젝트

---

## 팀 정보

- **팀명:** EVE
- **팀원:** 2376179 윤소진 (1인)

---

## 프로젝트 설명

외출 전에 갑자기 안경을 어디 두었는지 잊어버려 찾는 데 적지 않은 시간을 쓴 경험이 
있다. 특히 시력이 나쁜 사람에게는 안경을 찾으려면 안경이 필요한 모순적 상황이 발생한다. 본 프로젝트에서는 로봇의 카메라가 사람의 눈을 대신하여, 어질러진 책상 위에서 안경을 탐지하고, 로봇팔로 장애물을 피해 안전하게 집어 지정된 위치로 전달하는 시스템을 ROS2 기반으로 구현했다.

### 시스템 구성

천장에 고정된 카메라가 책상을 관측하면, 색 기반 검출 노드가 안경의 위치를 찾아 테이블 좌표로 변환하여 발행한다. 파지 노드는 이 좌표를 받아 MoveIt2를 통해 경로를 계획하고, 책상 위 장애물과의 충돌을 회피하며 안경을 집어 배달 위치로 옮긴다.

**작동 흐름:** 천장 카메라 → ros_gz_bridge → 색 기반 검출 노드 → (좌표 발행) → 파지 노드 → MoveIt2 → 로봇팔 동작

### 주요 노드

| 노드 | 역할 |
|------|------|
| `overhead_camera` | 천장 카메라 (Gazebo 센서), 책상 관측 |
| `ros_gz_bridge` | Gazebo 영상을 ROS 토픽으로 변환 |
| `glasses_color_detector` | 영상에서 안경 검출, 좌표 발행 (`/glasses_position`) |
| `glasses_pick_auto` | 검출 좌표 수신 → 파지 동작 계획/실행 |
| `move_group` (MoveIt2) | 경로 계획 및 충돌 회피 |
| `controller_manager` | 로봇팔/그리퍼 제어 |

### 개발 환경

- Ubuntu 22.04 (WSL2)
- ROS2 Humble
- Gazebo Fortress
- MoveIt2
- OpenCV (색 기반 검출)
- Franka Emika Panda (7-DOF 로봇팔)

---

## AI 사용 여부 및 사용 내용

본 프로젝트는 AI(Claude)의 다음과 같은 도움을 받아 진행하였다. 

- ROS2 / Gazebo / MoveIt2 개발 환경 설정 및 오류 해결 (WSL GPU 렌더링 충돌, 의존성 설치 등)
- Gazebo 시뮬레이션 월드(SDF) 작성: 책상, 장애물, 안경, 천장 카메라 배치
- 색 기반 검출 노드(`glasses_color_detector`) 및 픽셀-좌표 캘리브레이션 코드 작성
- 파지 노드(`glasses_pick_auto`): 강의 예제 `pick_and_place.py`를 기반으로, 검출 좌표를 수신해 동작하도록 수정
- 디버깅 과정 전반 (노드 충돌, 파지 실패, 좌표 변환 오차 등)에 대한 원인 분석 및 해결 방안 논의

---

## 참고 자료

- **강의 자료:** Ewha-AIRLab/intelligent-robotics-ros2
  https://github.com/Ewha-AIRLab/intelligent-robotics-ros2
  (Gazebo 시뮬레이션, SLAM, Nav2, MoveIt2 실습 코드 기반)
- **MoveIt2 공식 문서:** https://moveit.picknik.ai/main/index.html
- **MoveIt2 GitHub:** https://github.com/moveit/moveit2
- **Nav2 (Navigation2):** https://github.com/ros-navigation/navigation2
- **YOLOv8 (Ultralytics):** https://docs.ultralytics.com/
- **OpenCV:** https://docs.opencv.org/

---

## YouTube 링크

데모 영상 (일부공개): https://youtu.be/tMus8JyoADk

---

