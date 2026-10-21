# 사용자 손동작 기반 미로 탈출 로봇 게임

## 1. 팀 정보

* 팀명: 머지(Merge)
* 팀원: 서영, 2376126

## 2. 프로젝트 소개

본 프로젝트는 사용자의 손동작을 실시간으로 인식하고, 이를 ROS2 기반 토픽 통신을 통해 로봇 주행 명령으로 변환하여 TurtleBot이 Gazebo 미로 환경을 탈출하도록 제어하는 로봇 프로젝트입니다.

노트북 카메라를 통해 사용자의 손을 인식하고, MediaPipe를 이용해 손 landmark를 추출한 뒤 손동작을 분류합니다. 분류된 손동작은 ROS2 노드 간 통신을 통해 로봇 제어 명령으로 변환되며, TurtleBot은 해당 명령에 따라 전진, 좌회전, 우회전, 정지 동작을 수행합니다.

## 3. AI 사용 여부 및 사용한 곳

본 프로젝트에서는 AI 및 AI 기반 도구를 사용하였습니다.

### 3.1 프로젝트 기능 내 AI 사용

* MediaPipe Hands를 사용하여 카메라 영상에서 손 landmark를 추출하였습니다.
* 추출된 landmark 좌표를 기반으로 엄지 위, 검지 왼쪽, 검지 오른쪽, 손바닥 동작을 분류하였습니다.
* 손동작 인식 결과를 ROS2 명령으로 변환하여 로봇 제어에 활용하였습니다.

### 3.2 개발 과정에서의 AI 도구 사용

* ChatGPT를 활용하여 ROS2 노드 구조 설계, 코드 오류 원인 분석에 참고하였습니다.
* AI가 생성한 내용을 그대로 사용하지 않고, 프로젝트 구조와 실제 구현 내용에 맞게 수정 및 검증하여 반영하였습니다.

## 4. 참고 자료

GitHub 및 기술 공식 문서
* 미로 환경 구축 
  https://github.com/AI-Geniuses/Autonomous-Robot-Obstacle-Avoidance-with-ROS2?tab=readme-ov-file
* MediaPipe Documentation
  https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker


## 5. Youtube 링크
발표 링크: https://www.youtube.com/watch?v=56nJ2ujIl3c

## 6. Github 링크
https://github.com/Jade0728/maze_robotics
