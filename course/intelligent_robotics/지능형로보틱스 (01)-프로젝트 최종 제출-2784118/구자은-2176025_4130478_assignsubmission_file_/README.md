# 실내 화재 감지 및 위치 알림 시스템

## 팀명 및 팀원
- **팀명**: GAMJA
- **팀원**: 구자은 (2176025)

## 프로젝트 설명
단일 카메라 센서의 이미지 데이터를 활용하여 실내 화재 발생 여부를 실시간으로 모니터링하고 판단하며, 화재 발생 위치를 RViz2 상에서 시각적으로 확인할 수 있는 시스템입니다. 
비전 데이터 기반으로 HSV 색상 필터링을 거쳐 붉은색 픽셀이 500개 이상 인식될 경우 화재로 판별하고, 로봇 본체(base_link)를 기준으로 전방 1.0m, 높이 0.25m 위치에 경고 마커를 표시합니다.

## AI 사용 여부 및 사용 내용
- 시스템 아키텍처 설계 및 ROS 2 통신 브리지 설정 보조
- OpenCV HSV 색상 필터링 알고리즘 최적화 및 시각화(Marker) 로직 구현
- WSL2 그래픽 충돌 해결을 위한 환경 변수 및 렌더링 설정 디버깅

## 참고한 자료
- ROS 2 Humble Docs: https://docs.ros.org/en/humble/
- OpenCV Color Masking: https://docs.opencv.org/4.x/df/d9d/tutorial_py_colorspaces.html
- Gazebo Tutorial: https://gazebosim.org/docs

## 링크
- **YouTube 링크**: https://youtu.be/Kfgbvifb7FM