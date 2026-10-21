# Baby Safety Robot

## 팀명

로틱

## 팀원

* 김휘서

## 프로젝트 설명

본 프로젝트는 영아가 위험한 콘센트에 접근하는 상황을 ROS2와 Gazebo 환경에서 시뮬레이션하고, 로봇이 영아를 탐지한 뒤 가장 가까운 콘센트 앞 차단 위치로 이동하는 시스템을 구현한다. 시스템은 RGB 카메라 기반 YOLO 탐지, 영아 위치 기반 최근접 콘센트 선택, Nav2 기반 자율 주행, RViz 시각화로 구성된다.

## 추가한 ROS2 Node

* yolo_detector / yolo_node.py
  RGB 카메라 이미지를 입력받아 YOLOv8n CPU 추론을 수행 + 영아 탐지 여부를 /baby_detected topic으로 publish

* baby_safety_robot / outlet_selector.py
  영아 위치와 탐지 여부를 기반으로 최근접 콘센트를 선택 + Nav2 NavigateToPose goal을 전송하여 로봇을 차단 위치로 이동시킨다. 탐지 실패 시 navigation cancel 및 제자리 회전 탐색을 수행.

* blocking_arm / arm_controller_node.py
  feature/blocking-arm branch에서 구현한 독립 프로토타입이다. revolute joint 기반 arm을 fold / extend 형태로 제어한다. main 주행 시스템과의 연동까지는 구현하지 못했다. 사람의 팔 구조에서 아이디어를 받아 로봇에 팔처럼 관절을 구현하는 것에 그침.

## AI 사용 여부 및 사용 내용

Claude를 사용하여 ROS2 오류 해결 방향 검토, README 구성 & 코드 구조 설명 보조에 활용함. 최종 코드 실행 및 프로젝트 구성은 직접 확인하며 진행함.

## 참고 자료

* [전기 안전사고 관련 배경 기사](https://www.khan.co.kr/article/202509041440001)

* [ROS 2 Humble Documentation](https://docs.ros.org/en/humble/index.html)

* [ROS 2 Python Publisher / Subscriber Tutorial](https://docs.ros.org/en/humble/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Py-Publisher-And-Subscriber.html)

* [ROS 2 Launch Tutorial](https://docs.ros.org/en/humble/Tutorials/Intermediate/Launch/Creating-Launch-Files.html)

* [ROS 2 URDF Tutorial](https://docs.ros.org/en/humble/Tutorials/Intermediate/URDF/URDF-Main.html)

* [Gazebo Fortress ROS 2 Integration](https://gazebosim.org/docs/fortress/ros2_integration/)

* [Gazebo Actors Documentation](https://gazebosim.org/docs/latest/actors/)

* [Nav2 NavigateToPose Action](https://api.nav2.org/actions/humble/navigatetopose.html)

* [Nav2 Regulated Pure Pursuit Controller](https://docs.nav2.org/configuration/packages/configuring-regulated-pp.html)

* [Ultralytics YOLO Documentation](https://docs.ultralytics.com/)


## YouTube 링크

* presentation link: https://youtu.be/iWbN6U9TTzk
* 메인 데모 영상: https://youtu.be/9_15_NOpqW4
* blocking_arm 프로토타입 데모: https://youtu.be/EJggRxzyxpA
