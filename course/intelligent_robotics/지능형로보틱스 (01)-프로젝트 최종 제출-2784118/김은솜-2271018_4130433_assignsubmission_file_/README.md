# 소은솜 | 우주 실험실 복구 로봇 ‘Rocky’

## 프로젝트 정보

- **팀명:** 소은솜
- **팀원:** 2271018 김은솜, 2271053 정소은

## 프로젝트 설명

《프로젝트 헤일메리》의 세계관을 모티브로 한 **우주 실험실 복구 로봇 프로젝트**입니다.

아스트로파지 유출로 메인 시스템이 마비된 우주 실험실에서 사용자는 손 제스처를 통해 Rocky에게 `START`와 `STOP` 명령을 전달합니다. `START` 명령은 복구 미션을 시작하고, `STOP` 명령은 진행 중인 로봇을 정지시키는 데 사용됩니다.

Rocky는 ROS2 Nav2 기반 자율주행을 통해 움직이는 아스트로파지 장애물을 회피하면서 두 개의 작업 구역을 순차적으로 방문합니다. 먼저 **A구역인 에너지 스테이션**에서 충전을 0%부터 100%까지 충전한 뒤, **B구역인 배양기**로 이동하여 제자리에서 회전함으로써 장비를 가동합니다. 모든 작업이 완료되면 로봇을 안전하게 정지하고 복구 미션을 종료합니다.

또한 Isaac Sim Script Editor를 이용하여 여러 개의 실린더 장애물이 서로 다른 속도와 방향으로 이동하도록 구성해, 동적 장애물(아스트로파지)이 존재하는 우주 실험실 환경을 구현하였습니다.

## 미션 수행 과정

`제스처 인식` → `A구역 자율주행` → `에너지 충전 미션` → `B구역 자율주행` → `배양기 가동 회전 미션` → `미션 완료`

## 역할 분담

- **김은솜**
  - Rocky Coordinator 및 전체 미션 제어 로직 구현
  - Nav2 기반 자율주행과 A·B 구역 목표 지점 이동 구현
  - 에너지 충전 및 배양기 가동 미션 구현
  - Isaac Sim 실험실 환경 구성
  - Script Editor 기반 동적 장애물 구현
  - 프로젝트 데모 진행

- **정소은**
  - OpenCV·MediaPipe 기반 손 제스처 인식 구현
  - `START`, `STOP`, `NONE` 제스처 분류
  - `/gesture_cmd` ROS2 토픽 발행 및 중복 명령 방지 기능 구현
  - 제스처 인식 결과 실시간 시각화
  - 발표 자료 및 발표 영상 제작

## 오픈소스 라이브러리 및 AI 활용 내역

**생성형 AI - 동적 장애물 구축**

- 장애물을 random하게 움직이게 하는 python 코드 작성 시, 생성형 AI를 일부 활용함.

- **OpenCV**
  - 동영상 프레임 입력 및 전처리
  - 손 랜드마크와 제스처 인식 결과 시각화

- **MediaPipe Hands**
  - 영상 속 손 검출
  - 손가락 관절을 나타내는 21개 랜드마크 추출

- **제스처 분류**
  - 손가락 끝점과 중간 관절의 좌표 비교
  - 주먹은 `START`, 손바닥은 `STOP`, 그 외 동작은 `NONE`으로 분류
  - 이전 명령과 달라진 경우에만 ROS2 토픽 발행

## 주요 사용 기술

`Python` `OpenCV` `MediaPipe Hands` `ROS2 Humble` `Nav2` `RViz` `SLAM` `LiDAR` `Isaac Sim 5.1`

## 참고 자료

- [NVIDIA Isaac Sim Quick Install](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/installation/quick-install.html)
- [MediaPipe Hands](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker)
- [ROS2 Humble](https://docs.ros.org/en/humble/index.html)
- [Nav2 Documentation](https://docs.nav2.org/)
- [NVIDIA ROS 2 Tutorials](https://docs.isaacsim.omniverse.nvidia.com/latest/ros2_tutorials/tutorial_ros2_navigation.html)

## YouTube 링크

https://youtu.be/nVyeOlpvwdw
