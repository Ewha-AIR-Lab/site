# 촉각 센서 기반 미끄러짐 예측을 이용한 변형 가능 물체의 최소 안정 그립력 제어

> Slip Prediction & Adaptive Grip Force Control for Deformable Objects using Vision-based Tactile Sensing

## 팀 소개

**팀명:** 김앤팍

**팀원:** 김민지, 박윤형 (이화여자대학교 소프트웨어학부 컴퓨터공학전공)

## 프로젝트 설명

로봇 파지는 본질적으로 **Slip(미끄러짐)** 과 **Damage(손상)** 사이의 trade-off를 가집니다. Grip force가 너무 작으면 물체가 미끄러져 작업이 실패하고, 너무 크면 물체가 변형·손상됩니다. 특히 계란, 종이컵, 플라스틱 병과 같은 변형 가능 물체(deformable object)는 과도한 힘에 매우 민감합니다.

본 프로젝트의 목표는 촉각 센서를 활용해 **미래의 slip을 사전에 예측**하고, 그 예측을 이용해 로봇의 grip force를 능동적으로 조절하여 **slip과 손상을 동시에 방지하는 최소 안정 그립력(Minimum Stable Grip Force)** 을 유지하는 것입니다.

slip은 물체가 눈에 띄게 움직이기 전에 접촉면에서 먼저 시작됩니다. 시각 모달리티는 물체 전체의 움직임을 관찰하므로 초기 징후를 포착하기 어렵지만, 촉각 센서는 접촉면의 변형, marker motion, 접촉 영역 변화를 직접 관찰해 slip 직전의 미세한 변화를 감지할 수 있습니다.

### 파이프라인

1. **데이터 수집** — Isaac Sim + TacEX(UIPC soft-body) 기반 시뮬레이션에서 tactile, vision, proprioception 데이터 수집
2. **Stage 1 — Future Slip Prediction** — 멀티모달 관측으로부터 향후 15-step 내 slip 발생 확률 P(slip) 예측
3. **Stage 2 — Adaptive Force Control** — P(slip)을 실시간 제어 신호로 활용해 grip force를 선제적으로 조절하는 closed-loop 제어

### 주요 구성

- **시뮬레이션:** Isaac Sim, 7-DoF Franka, TacEX 기반 GelSight Mini 촉각 센서(양쪽 그리퍼), UIPC soft-body physics
- **물체:** Bottle, Can, HDMI (density·초기 grip force·random seed를 다양하게 조합)
- **Slip 라벨링:** gripper center frame 기준 bottle neck의 상대 속도(relative velocity)가 0.03 mm/step 초과 시 slip으로 판단. drop(수직 거리 1.5 mm 초과) 이후 프레임은 학습에서 제외
- **모델:** tactile(ViT-Small) + vision(ResNet-18, ImageNet 사전학습) + proprioception(10차원) → fusion(modality dropout 적용) → 2-layer LSTM → slip 확률 분류기

### 주요 결과

- **Occlusion robustness:** 카메라 손상(blackout/noise/patch) 시 vision은 AUC가 급락하지만, tactile은 영향을 받지 않아 안전망 역할을 수행. multimodal(full)이 가장 robust
- **Unseen-object generalization:** 처음 보는 물체(can, hdmi)에 대해 multimodal fusion(full)이 가장 안정적으로 일반화
- **Adaptive control:** P(slip)에 따라 tighten / hold / relax 행동을 선택해 slip 발생 전 선제적으로 grip force 조절. 센서 과변형으로 인한 오인을 막는 safety_relax 안전장치 포함

## 역할 분담

| 팀원 | 역할 |
|---|---|
| 김민지 | Isaac Sim 환경 구축, 데이터 수집 파이프라인 구현, tactile/vision/proprioception 데이터 수집, 데이터 분석 및 시각화, 모델 아키텍처 설계, 발표자료 및 대본 작성, 영상 편집 |
| 박윤형 | Project proposal 작성, 모델 아키텍처 설계 및 구현, 중간 보고서 작성, Slip prediction 모델 학습, Adaptive force control 로직 구현 및 시뮬레이션 실험 수행, 발표자료 및 대본 작성|


## AI 사용 여부 및 사용 내용

본 프로젝트는 개발 과정에서 AI 도구(Claude, ChatGPT)를 보조적으로 활용하였습니다.

- **코드 작성·디버깅:** 학습/평가 스크립트, 데이터 전처리, adaptive controller 구현 보조
- **실험 설계 검토:** threshold 고정, 클래스 balancing(undersampling), unseen-object 평가 조건 등에 대한 검토
- **결과 정리·시각화:** 실험 결과 표·그래프 생성 및 발표 자료(스크립트) 작성 보조

모든 실험 설계, 데이터 수집, 최종 의사결정 및 결과 해석은 팀원이 직접 수행하였습니다.

## 참고 자료

- **UniVTAC** — 시뮬레이션 환경 및 scene 설정 참고 (https://arxiv.org/abs/2602.10093)
- **TacEX / GelSight Mini** — 촉각 센서 시뮬레이션 (UIPC soft-body physics) (https://github.com/DH-Ng/TacEx)
- **Isaac Sim** — NVIDIA 시뮬레이션 플랫폼 (https://developer.nvidia.com/isaac/sim)
- **TVL / UniTouch** — 촉각-비전-언어 모델 (https://arxiv.org/abs/2402.13232), (https://arxiv.org/abs/2401.18084)
- **ViT (Vision Transformer)** — for tactile encoder
- **ResNet-18 (ImageNet pretrained)** — for vision encoder
- **Tactile-Force Alignment in Vision-Language-Action Models for Force-aware Manipulation** (https://arxiv.org/pdf/2601.20321)
- **Learned Slip-Detection-Severity Framework using Tactile Deformation Field Feedback for Robotic Manipulation** (https://arxiv.org/pdf/2411.07442)

## YouTube 링크

