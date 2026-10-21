# ROS2 기반 미지 실내 환경 자율 탐사 및 맵핑 드론 시스템

> Frontier-Based Autonomous Exploration with a Simulated UAV

지능형 로보틱스 프로젝트 | GitHub: https://github.com/DaeTaChulDong/ROS2

---

## 프로젝트 설명

사전 정보가 없는 미지의 실내 환경에서, 드론이 스스로 탐사할 경계(frontier)를 찾아 자율 비행하고, LiDAR 데이터를 기반으로 환경 지도를 실시간으로 구축하는 시스템이다. 재난 현장이나 사람이 진입하기 어려운 시설의 내부 구조를 원격으로 파악하는 상황을 가정한다.

핵심은 단순히 정해진 경로(waypoint)를 따라가는 것이 아니라, 이미 탐사한 영역(free)과 아직 모르는 영역(unknown)의 경계인 **frontier**를 스스로 판별하고, 그중 가장 유용한 지점을 선택해 이동하는 **자율적 의사결정**이다.

### 동작 파이프라인

```
LiDAR 스캔 → SLAM (맵 생성) → Frontier 탐지 → 클러스터링 →
최적 목표 선택 (가중치 기반) → 드론 비행 제어 → 맵 갱신 → (반복)
```

---

## 팀 정보

| 항목 | 내용 |
|------|------|
| 팀명 | (개인 프로젝트) |
| 팀원 | 이은서 |
| 역할 분담 | 1인 프로젝트로 전체 설계·구현·실험 단독 수행 |

---

## 시스템 구성

### 직접 구현한 ROS2 노드

| 노드 | 역할 |
|------|------|
| **Frontier Detector** | OccupancyGrid에서 free 셀의 이웃에 unknown이 있으면 frontier로 판정. BFS로 인접 frontier를 클러스터링하고 노이즈(최소 크기 미만)를 제거 |
| **Exploration Planner** | 각 클러스터를 `w_size × 정규화 크기 − w_dist × 정규화 거리` 가중치로 평가하여 다음 탐사 목표를 자율 선택. 벽에 막힌 목표는 블랙리스트로 관리 |
| **Drone Controller** | Nav2 없이 cmd_vel로 직접 비행 제어. 이륙 → 고정 고도 유지 → 목표 방향 회전·전진 → 도착 판정을 상태머신으로 관리 |

### 사용한 기존 패키지

| 패키지 | 용도 |
|--------|------|
| `slam_toolbox` | LiDAR 기반 2D SLAM, 실시간 OccupancyGrid 맵 생성 |
| `sjtu_drone` | Gazebo 기반 UAV 시뮬레이션 모델 (360° LiDAR 센서 직접 추가) |
| `octomap_server` | 누적 센서 데이터로 3D 점유 맵(OctoMap) 생성 |

---

## 개발 환경

- **OS / 미들웨어**: Ubuntu 22.04 · ROS2 Humble
- **시뮬레이터**: Gazebo Classic + sjtu_drone
- **SLAM**: slam_toolbox (2D)
- **센서**: 360° 2D LiDAR (드론 URDF에 직접 추가)
- **3D 맵핑**: OctoMap (octomap_server)
- **GPU**: NVIDIA RTX 4060 Ti

---

## 실행 방법

```bash
# 1. 드론 시뮬레이션 (미로 환경)
ros2 launch sjtu_drone_bringup sjtu_drone_bringup.launch.py \
  world:=<경로>/maze.world

# 2. SLAM
ros2 launch slam_toolbox online_async_launch.py \
  slam_params_file:=<경로>/slam_drone.yaml use_sim_time:=true

# 3. (선택) OctoMap 3D 맵 생성
ros2 run octomap_server octomap_server_node --ros-args \
  -p resolution:=0.05 -p frame_id:=map \
  -r cloud_in:=/simple_drone/scan

# 4. Frontier 자율 탐사 노드
ros2 run frontier_exploration drone_frontier_explorer
```

---

## 주요 구현 내용 및 결과

- 드론 모델에 360° LiDAR 센서를 추가하고, `odom → base_link → lidar_link` TF 체인을 구성
- slam_toolbox 연동으로 비행 중 실시간 2D 맵 생성 확인
- Frontier 탐지·클러스터링·가중치 기반 목표 선택 알고리즘을 ROS2 노드로 직접 구현
- 미로형 실내 환경(20×20m)에서 3,000개 이상의 frontier 셀 탐지 및 미탐사 영역 식별 확인
- 고정 고도 비행 제어 및 벽 충돌 회피(블랙리스트·타임아웃) 로직 구현

---

## 어려웠던 점

- **시뮬레이션 환경 셋업**: Isaac Sim / Gazebo의 GPU 렌더링, 드론 모델과 센서 연동에서 다수의 호환성 이슈를 해결
- **드론 비행 제어**: Nav2를 사용할 수 없는 UAV 특성상 cmd_vel 기반 비행, 고도 유지, 장애물 회피를 직접 구현
- **탐사 안정성**: 벽에 막힌 목표를 반복 선택하는 문제를 블랙리스트와 타임아웃 로직으로 완화

## 개선 방향

- OctoMap voxel 공간에서 26-이웃 기반 **3D frontier detection**으로 확장
- 직선 이동 대신 RRT* 등 **경로 계획** 도입으로 복잡 환경 주파 능력 강화
- nearest / largest / weighted **탐사 전략별 성능 비교 실험**
- 중앙 컨트롤러 기반 **멀티 드론 협력 탐사**

---

## AI 사용 여부 및 내용

본 프로젝트는 개발 과정 전반에 걸쳐 AI(Claude)를 활용하였다.

- **환경 구축 지원**: Ubuntu 듀얼부팅, ROS2·Gazebo·드론 시뮬레이터 설치 및 오류 해결 과정에서 단계별 안내를 받음
- **코드 작성 지원**: Frontier Detector / Exploration Planner / Drone Controller 노드의 초기 구현 코드를 AI와 함께 작성하고, 동작 결과를 보며 반복적으로 디버깅·수정
- **알고리즘 이해**: 참고 논문(Batinovic et al.)의 frontier exploration 알고리즘을 이해하고 ROS2 환경에 맞게 재구현하는 과정에서 설명을 받음
- **문서 작성**: 제안서, 발표자료, 본 README 작성에 활용

알고리즘의 최종 설계 판단, 시스템 통합, 실험 수행 및 결과 해석은 직접 수행하였다.

---

## 참고 자료

### 논문
- A. Batinovic, T. Petrovic, A. Ivanovic, F. Petric, S. Bogdan, "A Multi-Resolution Frontier-Based Planner for Autonomous 3D Exploration," *IEEE Robotics and Automation Letters*, vol. 6, no. 3, 2021.
- B. Yamauchi, "A Frontier-Based Approach for Autonomous Exploration," *IEEE CIRA*, 1997.
- A. Hornung et al., "OctoMap: An Efficient Probabilistic 3D Mapping Framework Based on Octrees," *Autonomous Robots*, 2013.

### GitHub
- sjtu_drone (ROS2 Gazebo UAV simulator): https://github.com/NovoG93/sjtu_drone
- larics/uav_frontier_exploration_3d: https://github.com/larics/uav_frontier_exploration_3d
- slam_toolbox: https://github.com/SteveMacenski/slam_toolbox
- octomap_server: https://github.com/OctoMap/octomap_mapping

---

## YouTube 데모 영상


https://youtu.be/5XzmytlQcz4
