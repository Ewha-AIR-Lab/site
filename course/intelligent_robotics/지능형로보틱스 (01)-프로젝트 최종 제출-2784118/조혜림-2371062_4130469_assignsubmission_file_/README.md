# 대화형 HRI를 활용한 맞춤형 샌드위치 조립 로봇 시스템

26-1 지능형로보틱스(01)

## 팀명 / 팀원
- 팀명: [로보]
- 팀원: 2371062 조혜림

## 프로젝트 설명
서브웨이 프랜차이즈 아르바이트생의 주문 및 제조 프로세스를 모사하여, 사용자와 채팅 인터페이스로 소통하며 취향에 맞는 샌드위치를 자율 제작하는 로봇 시스템이다.

- 사용자가 채팅 GUI에서 빵 · 채소 · 추가 재료 · 소스를 단계별로 주문
- LLM 기반 파서가 자연어 입력을 재료 JSON으로 파싱(모호하거나 재고 소진 시 재질문)
- Franka Panda 로봇이 ROS2 + Gazebo + MoveIt2 환경에서 재료 트레이의 재료를 Pick하여 조립판에 Place
- 조립 완료 후 YOLOv8n 기반 품질 검증(QC)으로 누락 재료를 감지하고 자율적으로 재조립

## 역할 분담
1인 프로젝트로 전체 과정 수행

## 시스템 구조 (ROS2 Node 구성)

| 토픽명 | Publisher | Subscriber | 내용 |
|---|---|---|---|
| /order_in | Chat GUI | LLM Parser | 고객 주문 입력 |
| /order_llm | LLM Parser | Action Planner | 파싱된 주문 JSON |
| /yolo | Action Planner | YOLO QC | 조립 완료 및 QC 요청 |
| /llm_request | LLM Parser | Chat GUI | 오류 주문 재질문 |
| /robot_status | Action Planner | Chat GUI | 로봇 동작 상태 표시 |
| /qc_result | YOLO QC | Action Planner | QC 결과 |
| /qc_replan | YOLO QC | Action Planner, Chat GUI | QC 오류 작업 재실행 요청 |

## 구현 환경
- WSL2 (Ubuntu 22.04)
- ROS2 Humble
- Gazebo Fortress
- MoveIt2
- Franka Panda

## 구현 내용
1. **환경 설정**: ROS2 + Gazebo + Franka Panda 설치 및 동작 확인
2. **SDF 제작**: 고객 공간(테이블 6개·의자 2개), 투명 파티션으로 주방/고객 분리, 재료 트레이 2열 배치(빵 3종, 채소 3종, 추가재료 3종, 소스 3종), 조립판 위 YOLO 카메라 배치. 재료는 Pick-and-Place 난이도를 고려해 블록 형태로 단순화
3. **Pick-and-Place 구현**: MoveIt2 기반으로 요구 재료 위치로 이동 → Pick → 조립판으로 이동 → Place. 조립 순서는 빵 → 채소 → 추가재료 → 소스 → (QC) → 빵. 재고 수량 딕셔너리를 참고해 스택이 줄어들수록 z 좌표를 보정
4. **Chat GUI 구현**: PyQt5 기반, 사용자 주문 입력 및 로봇 상태·재질문·QC 알림을 실시간 표시
5. **LLM Parser 구현**: 주문 문장을 재료 JSON으로 파싱. 오타·모호한 입력 시 재질문, 재고 0인 재료 주문 시 재고 소진 안내 후 재주문 요청
6. **YOLO QC 구현**: 사전학습 YOLOv8n으로 조립판의 재료 존재 여부 판정 → 주문 리스트와 비교해 누락 재료 추출 → 누락 재료만 재실행 → 재검증까지 반복
7. **노드 통합·점검**: 전체 노드 토픽 연결 및 점검
8. **최종 테스트**: 데모 시나리오 실행 및 발표자료 제작

## 어려웠던 점
- Pick-and-Place 과정에서 그리퍼와 블록 간 접촉 마찰력 설정이 까다로워 블록을 정확히 들어 올리지 못하고 미끄러지거나 떨어지는 문제가 반복됨
- manipulator의 경로 계획 시 충돌 회피가 정밀하지 않아 로봇 팔이 주변 물체와 부딪혀 쌓아둔 블록 구조가 무너지는 문제 발생

## 개선할 점
- 그리퍼-물체 간 접촉 모델을 정교화하여 안정적인 pick-and-place가 가능하도록 개선 필요
- 단순 블록 형태가 아닌 다양한 모양·질감·크기의 물체도 안정적으로 조작할 수 있도록 그리퍼 제어 및 인식 성능 개선 필요

## AI 사용 여부 및 사용 내용
- Claude(Anthropic) Chat과 Claude CLI를 활용하여 환경 설정 오류 해결, ROS2 노드 구조 설계, MoveIt2 Pick-and-Place 로직 구현에서의 디버깅 등에 도움을 받음

## 참고 자료
- Ultralytics YOLO Detection: https://docs.ultralytics.com/ko/
- YOLO-ROS: https://docs.ultralytics.com/guides/ros-quickstart/#key-features-of-ros
- MoveIt2 로봇 팔 제어: https://moveit.picknik.ai/main/index.html
- Pick-and-Place (MoveIt Task Constructor): https://automaticaddison.com/pick-and-place-with-the-moveit-task-constructor-for-ros-2/
- Franka Panda: https://github.com/frankarobotics/franka_ros2
- PyQt5: https://www.riverbankcomputing.com/static/Docs/PyQt5/
- 서브웨이 샌드위치 메뉴: https://www.subway.co.kr/menuList/sandwich
- PyQt5-ROS2: https://github.com/tasada038/pyqt_ros2_app
- LLM-ROS2: https://github.com/aniskoubaa/rosgpt
- 지능형로보틱스 강의자료: https://github.com/Ewha-AIRLab/intelligent-robotics-ros2
- 텍스처 PNG 리소스: https://polyhaven.com/textures
- 텍스처 추가 방법: https://ibrahimmansur4.medium.com/enhancing-your-gazebo-models-with-custom-textures-in-ros-2-a20670e19bef
- SDF 작성: https://gazebosim.org/docs/fortress/sdf_worlds/

## YouTube 링크
- https://youtu.be/a7L00mWXass
