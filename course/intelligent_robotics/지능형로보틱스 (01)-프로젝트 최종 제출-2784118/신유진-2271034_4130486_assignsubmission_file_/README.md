# 2026-1-multi-turtle-sim
# 터틀봇 대형 이동 프로젝트

> 4대의 TurtleBot3가 음성 명령에 따라 지정된 대형(Formation)으로 자율 이동하는 ROS2 기반 시스템

---

## 👥 팀 정보

**팀명:** 리신

| 이름 | 학번 | 역할 |
|------|------|------|
| 신유진 | 2271034 | 시뮬레이션 환경 구성, Nav2 연동 및 네임스페이스 설정, 목표 좌표 설정 및 이동 과정 구현, 지휘 파일 구현 및 간소화 |
| 신은지 | 2217015 | 음성 인식 트리거 모듈 개발, 헝가리안 알고리즘 구현, Nav2 환경 설정 및 디버깅, 전체 파이프라인 통합 테스트 |

---

## 📌 프로젝트 설명

Ubuntu 22.04 + ROS2 Humble + Gazebo 환경에서 4대의 TurtleBot3를 운용합니다.
사용자가 음성으로 대형 키워드(`line`, `diamond`, `square` 등)를 발화하면, Whisper STT로 명령을 인식하고 헝가리안 알고리즘으로 봇과 목표 위치를 최적 배정한 뒤 Nav2 스택을 통해 각 봇이 자율 이동합니다.

**지원 대형:** `line` · `side` · `diamond` · `square` · `v` · `scatter`

---

## 🤖 AI 사용 여부 및 사용 내용

본 프로젝트는 개발 전 과정에서 Claude (Anthropic) 및 Gemini (Google)를 활용하였습니다.

| # | 사용 단계 | 사용 내용 |
|---|-----------|-----------|
| 1 | **초안 코드 생성** | 폴더 구조 설계 및 파일별 슈도코드 작성 후, 이를 기반으로 각 모듈의 초안 코드 생성 |
| 2 | **통신 오류 해결** | ROS2 토픽/액션 트리 연결 과정에서 발생한 네임스페이스 불일치 등 커뮤니케이션 오류 디버깅 및 해결 원리 이해 |
| 3 | **모듈 버전 문제 해결** | ROS2 Humble / Nav2 / rclpy 버전 호환성 문제 식별 및 모듈별 수정 방향 확인 |
| 4 | **전체 연결 검토** | 파일 간 의존 관계 최종 점검 및 헝가리안 알고리즘 동작 원리 이해 보조 |

---

## 📚 참고 자료

| 유형 | 제목 / 출처 |
|------|-------------|
| 공식 문서 | [ROS2 Humble Documentation](https://docs.ros.org/en/humble/) |
| 공식 문서 | [Nav2 Documentation](https://navigation.ros.org/) |
| 공식 문서 | [TurtleBot3 e-Manual](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/) |
| 라이브러리 | [faster-whisper](https://github.com/SYSTRAN/faster-whisper) |
| 라이브러리 | [scipy.optimize.linear_sum_assignment](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.linear_sum_assignment.html) |

---

## 🔗 링크

| 항목 | 링크 |
|------|------|
| 🎥 YouTube 시연 영상 | https://www.youtube.com/watch?v=4BI_R_nIsiQ |
| 🎥 YouTube 발표 영상 | https://youtu.be/SVgGvHsyKck |
| 💻 GitHub | https://github.com/hineugene/2026-1-multi-turtle-sim |
