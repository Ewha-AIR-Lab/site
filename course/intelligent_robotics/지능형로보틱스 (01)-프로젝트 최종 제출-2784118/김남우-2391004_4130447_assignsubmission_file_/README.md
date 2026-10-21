# 카페 순찰 로봇 시스템 🤖☕

## 팀 정보

| 항목 | 내용 |
|------|------|
| 팀명 | 투들스 |
| 팀원 | 김남우 |
<br />

## 프로젝트 개요

TurtleBot3가 카페 내 테이블을 waypoint 기반으로 순회하며 YOLOv8을 이용해 방치된 물건을 감지하고, 일정 횟수 이상 감지되면 알림을 발행합니다.
<br />

## 기술 스택

- **ROS2 Humble**
- **Gazebo Classic 11** - 시뮬레이션 환경
- **TurtleBot3 Burger** - 로봇 플랫폼
- **Nav2** - 자율 주행
- **YOLOv8n** - 객체 감지
- **Python 3.10**
<br />

## 개발 환경

- Ubuntu 24.04 (WSL2)
- ROS2 Humble Hawksbill
- Python 3.10
<br />

## AI 사용 여부

### AI Tool
- Claude

### Usage
- ROS2 topic 및 node 구조 설계 아이디어 검토
- Tracking 알고리즘 구현 방법 조사
- 코드 디버깅, 에러 상황 분석 및 해결 보조
- README 작성 보조

AI는 코드 작성 및 설계 과정에서 큰 틀 설계, 참고 자료와 디버깅 도구로 활용하고 상세 기능 구현, 테스트 및 검증은 예시 코드를 참고하여 직접 수행하였습니다.
<br />

## 참고 자료

- [ROS2 Humble 공식 문서](https://docs.ros.org/en/humble/)
- [Nav2 공식 문서](https://navigation.ros.org/)
- [YOLOv8 (Ultralytics)](https://github.com/ultralytics/ultralytics)
- [TurtleBot3 공식 문서](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- [Gazebo Classic 공식 문서](http://gazebosim.org/tutorials)
<br />

## Youtube Link
[youtube_link](https://youtu.be/QFCUIRvmi4I)
<br />

## Github Link
[github link](https://github.com/namwoooo/cafe_robot_ws)
