**프로젝트 소개**

autonomous\_parking은 주차 슬롯의 유형, 점유 상태, 사용자 자격 정보를 바탕으로 적절한 목표 주차 슬롯을 선택하고, Gazebo 시뮬레이션 환경에서 차량을 자율 주행 및 후진 주차시키는 ROS 2 기반 프로젝트입니다.

본 프로젝트는 카메라 기반 차량 감지를 통해 주차 슬롯의 점유 여부를 판단하고, 선택된 목표 슬롯까지 차량을 이동시킨 뒤 후진 주차 동작을 수행하는 것을 목표로 합니다.



**팀 Baymax**

팀원은 다음과 같습니다.

2391007 인공지능학과 김민정

2391017 인공지능학과 이윤지



**역할 분담**

김민정: YOLOv8 기반 차량 감지/점유 판단, 학습 데이터 제작 및 모델 학습, vision node 제작 및 파이프라인 연결

이윤지: ROS 2-Gazebo 연동, 주차 상태 머신, launch 및 맵 기반 실행 구성

그 외 프로젝트 기획, 기능 설계, 테스트, 오류 수정, 최종 시연 준비 및 README 정리는 두 팀원이 함께 진행했습니다.



**AI 사용 여부**

본 프로젝트에서는 AI 도구를 사용했습니다. ChatGPT와 Codex를 활용하여 코드 점검과 README 정리 작업을 보조받았습니다.



**참고 문헌**

\[1] Wong, G. S., Goh, K. O. M., Tee, C., \& Md. Sabri, A. Q. (2023). Review of Vision-Based Deep Learning Parking

Slot Detection on Surround View Images. Sensors, 23(15), 6869. https://www.mdpi.com/1424-8220/23/15/6869

\[2] Grbić, R., \& Koch, B. (2023). Automatic Vision-Based Parking Slot Detection and Occupancy Classification.

Expert Systems with Applications, 225, 120147. https://arxiv.org/abs/2308.08192

\[3] Chen, J., Zhang, L., Shen, Y., Ma, Y., Zhao, S., \& Zhou, Y. (2020). A Study of Parking-Slot Detection with the

Aid of Pixel-Level Domain Adaptation. IEEE ICME 2020, 1–6. https://ieeexplore.ieee.org/document/9102928

\[4] Seo, Y.-W., Urmson, C., Wettergreen, D., \& Lee, J.-W. (2010). Building Lane-Graphs for Autonomous Parking.

IROS 2010, 6052–6057. https://ieeexplore.ieee.org/document/5650331

\[5] Qin, T., Chen, T., Chen, Y., \& Su, Q. (2020). AVP-SLAM: Semantic Visual Mapping and Localization for

Autonomous Vehicles in the Parking Lot. IROS 2020, 5939–5945. https://ieeexplore.ieee.org/document/9340939

\[6] Yang, Y. et al. (2021). Towards Autonomous Parking using Vision-only Sensors. IROS 2021.

https://ieeexplore.ieee.org/document/9636106

\[7] Xiao, A., Doshi, D., Wang, L., Gorantla, H., Heitzmann, T., \& Groth, P. (2023). Parking Spot Classification based

on Surround View Camera System. arXiv:2310.12997. https://arxiv.org/abs/2310.12997

\[8] Li, C., Ji, Z., Chen, Z., Qin, T., \& Yang, M. (2024). ParkingE2E: Camera-based End-to-end Parking Network,

from Images to Planning. IROS 2024, 13206–13212. https://ieeexplore.ieee.org/document/10801763



**참고 문서 및 도구**

Nav2 Documentation: https://docs.nav2.org/

Nav2 Simple Commander API: https://docs.nav2.org/commander\_api/index.html

Gazebo–ROS 2 Interop Guide: https://gazebosim.org/docs/harmonic/ros2\_interop/

ros\_gz GitHub (ros\_gz\_bridge, ros\_gz\_image): https://github.com/gazebosim/ros\_gz

TurtleBot3 Simulation: https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/

Ultralytics YOLOv8 Documentation: https://docs.ultralytics.com/

Ultralytics YOLO Custom Training: https://docs.ultralytics.com/modes/train/



**참고 깃허브**

https://github.com/libero0077/RokeyProjects/tree/main/ParkingLotProject



**YouTube 링크**

https://www.youtube.com/watch?v=fVQgzHXKoww

