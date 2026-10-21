# 로보치즈 — 자율 순찰 주차 단속 시스템

> LiDAR 기반 자율 순찰 로봇을 활용한 주차 단속 시스템 (지능형 로보틱스 프로젝트)

## 팀 정보

- **팀명:** 로보치즈 (RoboChz)
- **팀원:** 최다현 (2277032)

## 프로젝트 설명

외부 차량 금지 시간대에 순찰 로봇 **치즐봇**(TurtleBot3 Waffle Pi)이 아파트 주차장을
자율 순찰하며, 측면 카메라로 차량 번호판을 인식하고 등록 차량 DB와 대조해 **미등록
차량을 자동으로 단속·기록**하는 시스템이다. 스티커 부착·차단기 같은 기존 방식의
분쟁·비용 문제를 디지털 증거 기반 단속으로 대체하는 것을 목표로 한다.

애자일 방식으로, 순찰 → 인식 → 기록의 전체 흐름이 한 바퀴 도는 최소 버전(walking
skeleton)을 먼저 만들고 가짜 구현을 진짜로 하나씩 교체하며 4번의 Iteration으로
완성했다.

| Iteration | 내용 |
|---|---|
| 0. Walking Skeleton | 5개 패키지·인터페이스 계약 고정 → 가짜 OCR로 파이프라인 한 바퀴 |
| 1. Real Navigation | 주차장 world·점유격자 지도 제작 + Nav2/AMCL 자동 순찰·장애물 회피 |
| 2. Real Perception | 카메라 90° 마운트 + PaddleOCR 번호판 인식 + 등록 DB 대조 |
| 3. Advanced | Monitor 발전(알림·리포트) + 동적 차량 회피 + DWB vs MPPI 플래너 비교 |

**기술 스택:** ROS2 Humble · Gazebo Classic · Nav2 · slam_toolbox · AMCL · PaddleOCR(korean)

## AI 사용 여부 및 사용 내용

**사용함 — Anthropic Claude (Claude Code).**

ROS2를 직접 학습하는 것을 목표로, 코드 생성기가 아닌 **튜터·페어 프로그래밍 상대**로
사용했다. `CLAUDE.md`에 동작 규칙을 고정해 다음과 같이 운용했다.

- **직접 작성:** 노드 구조, 퍼블리셔/서브스크라이버/액션 클라이언트, Nav2 액션 호출부,
  launch·파라미터(yaml) 설계, 노드 간 통신 인터페이스 등 ROS2 핵심 코드.
  → Claude는 개념 설명·힌트·코드 리뷰만 담당.
- **위임:** SDF 주차칸 좌표 생성기, JSON 등록 차량 더미 DB, PaddleOCR 추론 래퍼,
  한국 번호판 텍스처 이미지 등 ROS2 본질이 아닌 보조 작업 (생성 코드도 한 줄씩 설명 요구).
- 그 외 진행상황 기록 정리 및 디버깅 보조에 활용했다.

## 참고 자료

**프레임워크 / 오픈소스**
- ROS2 Humble · Nav2 · Gazebo Classic
- TurtleBot3 — ROBOTIS (https://github.com/ROBOTIS-GIT/turtlebot3)
- slam_toolbox (https://github.com/SteveMacenski/slam_toolbox)
- PaddleOCR — PaddlePaddle (https://github.com/PaddlePaddle/PaddleOCR)

**참고 GitHub 레포지토리**
- Patrol-Robot — 유사 주차장 순찰 로봇, 시뮬레이션·SLAM 셋업과 world 구조 참고
  (https://github.com/AjaySurya-018/Patrol-Robot)
- korean_ocr_using_paddleOCR — 한국어 번호판 OCR 환경 구성·추론 래퍼 참고
  (https://github.com/yunwoong7/korean_ocr_using_paddleOCR)
- intelligent-robotics-ros2 — 수업 실습 자료(동적 actor, collision plugin 등) 참고
  (https://github.com/Ewha-AIRLab/intelligent-robotics-ros2)

**에셋**
- Gazebo Fuel — Distribution Warehouse(실내 창고 셸), Construction Cone / Stop Sign /
  Jersey Barrier / Electrical Box / Shelf(랜드마크 모델)

## 링크

- **시연 영상 (YouTube):** : https://cheddar4135.github.io/robochz-parking-patrol/final-video/, https://youtu.be/P7uWxPjPnxg
- **GitHub:** https://github.com/Cheddar4135/robochz-parking-patrol
