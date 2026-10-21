# GestureBot

손동작으로 TurtleBot4를 제어하는 ROS2 기반 모바일 로봇 제어 시스템

---

## 팀명

쿠쿠 

## 팀원

2129032 장한나

---

## 프로젝트 소개

카메라를 통해 사람의 손동작을 실시간으로 인식하고, 이를 로봇 제어 명령으로 변환하여 TurtleBot4를 제어하는 시스템입니다. 
기본적인 수동 제어 외에도 Nav2를 활용한 자율 주행 목표 지점 제어 기능을 구현하였습니다.

---

## 제스처 매핑

### 기본 동작

| 손동작 | 로봇 동작 |
|--------|-----------|
| ✌️ V자 (검지 + 중지) | 직진 |
| 👌 OK 손모양 | 정지 |
| ✋ 손바닥 펼치기 | 후진 |
| ☝️ 검지 → 오른쪽 | 오른쪽 회전 |
| ☝️ 검지 → 왼쪽 | 왼쪽 회전 |
| 손 위로 올리기 | 속도 증가 |
| 손 아래로 내리기 | 속도 감소 |

### 추가 기능 (Nav2)

| 손동작 | 로봇 동작 |
|--------|-----------|
| 검지 + 중지 + 약지 | 목표 지점으로 자율 주행 |

---

## AI 사용 여부 및 사용 내용

- 환경 설정 시 충돌 해결
- 코드 디버깅
- 발표 자료 제작 및 readme 작성 (일부)

---

## 참고자료

[TurtleBot 공식 매뉴얼](https://turtlebot.github.io/turtlebot4-user-manual/software/turtlebot4_simulator.html)
[OpenCV GitHub](https://github.com/ros-perception/vision_opencv)
[MediaPipe GitHub](https://github.com/google-ai-edge/mediapipe)
[MediaPipe 공식 매뉴얼](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker?hl=ko)
[MediaPipe+Turtlebot3](https://github.com/Srikiranrao/ROS-mediapipe-turtlebot3)

---

## YouTube 링크

[GestureBot_발표영상](https://youtu.be/xlbJtlwu1LI)
(유튜브 설명란 확인 부탁드립니다.) 

---

## GitHub 링크

[GestureBot_GitHub](https://github.com/Hanna07111/GestureBot)

