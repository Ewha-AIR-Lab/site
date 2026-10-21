# Tesla Jr. — Vision-Driven Autonomous Navigation System

> **"See Local. Think Local. Drive Real."**
> 카메라만으로 보고, 로컬에서 판단하고, 실제처럼 주행하는 자율주행 시스템

2026 지능형 로보틱스 (Intelligence Robotics) 최종 프로젝트

---

## 1. 팀 정보

| 항목 | 내용 |
|------|------|
| **팀명** | Tesla Jr. |
| **팀원** | 신우림 (Woorim Shin) |
| **구성** | 1인 프로젝트 |


---

## 2. 프로젝트 소개

**Tesla Jr.** 는 자율주행 차량이 **SLAM과 LiDAR 없이, 오직 카메라만으로** 장애물을
피해 목표점까지 도달하는 비전 기반 자율주행 시스템입니다.

일반적인 자율주행 프로젝트가 차동구동 로봇 + LiDAR + 사전 지도(SLAM)를 사용하는
것과 달리, 본 프로젝트는 "Tesla"가 채택한 카메라 기반의 자율주행 시스템 구축을 목표로 삼았습니다.

| 일반적 접근 | 본 프로젝트 |
|---|---|
| 차동구동 (제자리 회전 가능) | **Ackermann 조향** (자동차형, 제자리 회전 불가) |
| LiDAR | **스테레오 카메라만** (vision-only) |
| 사전 지도 + SLAM | **지도 없음 (mapless)**, odom 프레임 rolling costmap |
| Gazebo + 기성 로봇 | **Isaac Sim + 직접 모델링한 T870 URDF** |

### 핵심 동작 (See → Think → Drive 폐루프)
1. **See** — 전방 카메라 → 포인트클라우드로 장애물 인식 + YOLO로 객체(사람) 탐지
2. **Think** — 포인트클라우드 → Nav2 costmap → Smac Hybrid-A* 경로 계획 → MPPI 제어
3. **Drive** — `/cmd_vel` → Ackermann 변환(조향각·바퀴속도) → 주행 → 위치(`/odom`) 갱신
4. 위 과정을 1초에 수십 회 반복하여 목표점까지 자율 주행

### 달성 결과
- [x] Ackermann 차량의 카메라 기반 mapless 자율주행 (목표점 자율 도달)
- [x] YOLO 실시간 보행자 탐지 + 보행자 정지/재개 데모 (stop-and-go)
- [x] 직접 구현한 ROS2 커스텀 노드 3종 + 가상 범퍼(Virtual Bumper)
- [x] RViz2 전체 시각화 (이미지 · 포인트클라우드 · costmap · 경로 · TF · YOLO)

### 직접 구현한 ROS2 노드
| 노드 | 역할 |
|---|---|
| `ackermann_control` | `/cmd_vel` → Ackermann 조향/구동 변환 + `/odom`·`/tf`·`/clock` 발행 + 가상 범퍼 |
| `yolo_node` | 카메라 이미지 → YOLO 추론 → `/yolo/detections_json` + `/yolo/image` |
| `json_goal_node` | `/goal_json` (JSON) → Nav2 `navigate_to_pose` (VLM→주행목표 연결 다리) |

---

## 3. 역할 분담

| 역할 | 담당 |
|---|---|
| 시스템 설계 / 아키텍처 | 신우림 |
| Isaac Sim 시뮬레이션 환경 구축 | 신우림 |
| ROS2 노드 개발 (ackermann / yolo / json_goal) | 신우림 |
| Nav2 통합 및 튜닝 (Smac Hybrid-A* / MPPI / costmap) | 신우림 |
| T870 URDF 모델링 및 물리 튜닝 | 신우림 |
| 실험 · 검증 · 문서화 | 신우림 |

---

## 4. AI 사용 여부 및 사용 내용

**AI 사용: 예 (보조 도구로 활용)**

본 프로젝트는 개발 보조 도구로 **Claude Code (Anthropic)** 를 사용하였습니다. AI는
**환경 세팅 · 디버깅 · 문서화 · 저장소 관리** 를 보조하는 용도로 활용하였습니다.

### AI를 사용한 영역
| 영역 | 사용 내용 |
|---|---|
| **Isaac Sim 초기 세팅** | Docker GPU 격리 문제, FastDDS(UDP-only) DDS 프로파일 설정, ROS2 브리지 환경변수 구성 등 초기 환경 구축 시 트러블슈팅 보조 |
| **디버깅 보조** | 바퀴 traction(sphere collider), dynamic_control 핸들 충돌, costmap 바닥 오인식 등 문제의 원인 분석 보조 |
| **코드 리뷰 / 문서화** | 코드 정리, 진행 상황·시행착오 문서(`docs/`) 작성 보조 |
| **GitHub 저장소 관리** | 커밋 메시지 정리, 디렉토리 구조 정리, README 작성 보조 |


---

## 5. 참고 자료

### 논문 · 공식 문서
- Macenski, S., et al. (2020). *The Marathon 2: A Navigation System.* IROS 2020. — Nav2
- Nav2 공식 문서 — https://docs.nav2.org
- NVIDIA. (2024). *Isaac Sim Documentation.* — https://developer.nvidia.com/isaac-sim
- Gemma Team, Google. (2024). *Gemma: Open Models Based on Gemini Technology.*

### 알고리즘 · 라이브러리
- Smac Planner (Hybrid-A*) — Nav2 global planner (Ackermann/차량형 경로)
- MPPI Controller — Nav2 local controller (`nav2_mppi_controller`)
- Regulated Pure Pursuit (RPP) — Ackermann 컨트롤러 (초기 적용)
- Ultralytics YOLO (YOLOv8) — 객체 탐지 — https://github.com/ultralytics/ultralytics

### 도구 · AI
- **Claude Code (Anthropic)** — Isaac Sim 초기 환경 세팅, 디버깅, 문서화, 저장소 관리 보조
- NVIDIA Isaac Sim 4.2.0 (Docker) — 시뮬레이션 플랫폼
- ROS2 Humble — 미들웨어

### 하드웨어 참고 (Phase 2/3 실물 플랫폼)
- Henes Broon T870 — 차량 플랫폼
- NVIDIA Jetson Orin Nano Developer Kit
- Pololu Jrk G2 24v21 USB Motor Controller (조향 드라이버)
- Arduino
- NUC

---

## 6. 발표 영상 (YouTube)

📺 **[발표 및 데모 영상 : Tesla-Jr_ver1](https://youtu.be/ZjxjWnA8UcE)**
📺 **[발표 및 데모 영상 : Tesla-Jr_ver2](https://youtu.be/XRJORmt7uws)
> ver1은 유튜브 업로드시 오디오가 밀리는 현상이 발생하여 ver2로 재업로드하였습니다.


---

## 7. GitHub

💻 https://github.com/RainyForest23/tesla-jr

---

## 부록 — 실행 환경 및 구조

### 환경
- Ubuntu 22.04 (Alienware Aurora R12, RTX 3060)
- Isaac Sim 4.2.0 (Docker)
- ROS2 Humble + Nav2

### 디렉토리 구조
```
docker/   Isaac Sim Docker 실행 스크립트 + DDS 프로파일(fastdds.xml)
isaac/    Isaac Sim 측 스크립트(scripts) + RViz 설정(rviz)
nodes/    호스트 ROS2 커스텀 노드 (yolo_node, json_goal_node)
nav2/     Nav2 파라미터 + 실행 스크립트
urdf/     T870 차량 URDF 모델
docs/     진행 상황 런북(PROGRESS.md) + 시행착오 기록(TRIAL_AND_ERROR.md)
```

상세 진행 상황·실행법은 **[`docs/PROGRESS.md`](docs/PROGRESS.md)**,
시행착오·해결 기록은 **[`docs/TRIAL_AND_ERROR.md`](docs/TRIAL_AND_ERROR.md)** 참고.
