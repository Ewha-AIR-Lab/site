# 다중 로봇 협력 추격 시뮬레이션 (경찰 vs 도둑)

> **지능형로보틱스 최종 프로젝트** | 컴퓨터공학과 공세영 (2371006)

---

## 팀 정보

| 항목 | 내용 |
|------|------|
| 팀명 | 1인 프로젝트 |
| 팀원 | 공세영 (2371006, 컴퓨터공학과) |

---

## 프로젝트 설명

**주제**: 다중 로봇 협력 추격 시뮬레이션 (경찰 vs 도둑)

장애물이 배치된 12×12m Gazebo 맵에서:
- **도둑 로봇 (thief)** 1대 — 플레이어가 키보드(또는 닌텐도 프로콘)로 직접 조종
- **경찰 로봇 (police1, police2)** 2대 — LiDAR 기반 DATMO 추적 + 협력 전략으로 자율 추격

경찰 로봇은 서로 통신하며 역할(추격자/차단자)을 동적으로 분담하고, **120초 이내 도둑을 0.5m 이내로 포위**하면 검거 성공입니다.

### 핵심 기술
- **DATMO 노드** (`datmo_tracker.py`): LaserScan → ABD 클러스터링 → 정적 장애물 필터 → 칼만 필터(CV 모델)로 도둑 위치 추정
- **협력 전략 노드** (`police_coordinator.py`): 두 경찰의 거리 비교로 추격자/차단자 역할 동적 결정, P 제어기 기반 자율 이동 + 장애물 회피
- **게임 매니저 노드** (`game_manager.py`): 검거 판정(≤0.5m) + 120초 타이머 + `/game_status` 발행

### 개발 환경

```
Ubuntu 24.04 LTS (WSL2) / ROS2 Jazzy / Gazebo Harmonic (gz-sim 8) / Python 3.12
```

**주요 패키지**: `ros_gz_bridge`, `teleop_twist_keyboard`, `nav_msgs`, `sensor_msgs`

### 패키지 구조

```
chase_simulation/
├── chase_simulation/
│   ├── datmo_tracker.py        # LiDAR 기반 이동 물체 추적
│   ├── police_coordinator.py   # 협력 전략 + 자율 이동
│   └── game_manager.py         # 검거 판정 + 타이머
├── launch/
├── worlds/chase_world.sdf
└── models/
    ├── thief_robot.sdf
    └── police_robot.sdf
```

---

## 역할 분담

1인 프로젝트로 전체 설계·구현·테스트를 단독 수행하였습니다.

---

## AI 사용 여부 및 사용 내용

- **사용 여부**: 사용함
- **사용 도구**: ChatGPT / Claude
- **사용 내용**:
  - DATMO ABD 클러스터링 파라미터 설계 참고
  - 칼만 필터 Constant Velocity 모델 수식 검토
  - ROS2-Gazebo 브릿지 토픽 매핑 디버깅 보조
  - 코드 전반의 논리 검토 및 리팩토링 제안

---

## 참고 자료

### 논문

| 논문 | 활용 |
|------|------|
| Azim & Aycard (2012), *Detection, Classification and Tracking of Moving Objects in a 3D Environment* | DATMO 전체 파이프라인 설계 참고 |
| Borges & Aldon (2004), *A Split-and-Merge Segmentation Algorithm for Line Extraction in 2D Range Images* | ABD 클러스터링 알고리즘 |
| Welch & Bishop (2006), *An Introduction to the Kalman Filter* (UNC TR 95-041) | 칼만 필터 CV 모델 수식 구현 참고 |
| Mahalanobis (1936), *On the generalised distance in statistics* | 칼만 필터 데이터 연관(Mahalanobis 거리) |
| Vidal et al. (2002), *Pursuit-Evasion Games with Unmanned Ground and Aerial Vehicles* | 다중 로봇 추격-도피 전략 배경 |

### 공식 문서 및 GitHub

| 분류 | 링크 |
|------|------|
| ROS2 Jazzy 공식 문서 | https://docs.ros.org/en/jazzy/ |
| Gazebo Harmonic 공식 문서 | https://gazebosim.org/docs/harmonic/ |
| ros_gz_bridge 패키지 | https://github.com/gazebosim/ros_gz |
| TurtleBot3 모델 (ROBOTIS) | https://github.com/ROBOTIS-GIT/turtlebot3 |
| Nav2 공식 문서 (향후 참고) | https://docs.nav2.org/ |

### 블로그 및 튜토리얼

| 제목 | 링크 |
|------|------|
| *Understanding the Kalman Filter* — Roger Labbe (Jupyter Notebook 형식, 매우 상세) | https://github.com/rlabbe/Kalman-and-Bayesian-Filters-in-Python |

---

## 링크

| 항목 | 링크 |
|------|------|
| 발표 영상 (YouTube, Unlisted) | [https://youtu.be/Ms1-FtOEe7Y] |

---