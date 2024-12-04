#📖 프로젝트 개요
이 프로젝트는 BTAD와 MVTec 데이터셋을 사용하여 **이상 탐지(Anomaly Detection)**를 수행하는 파이프라인입니다.
사전 학습된 MobileNetV2와 WideResNet50 모델을 활용해 특징 벡터를 추출하고, Top-K 이웃 거리 기반으로 이상 점수를 계산합니다.

🚀 주요 기능
BTAD 및 MVTec 데이터셋 지원:
BTAD: 3개의 클래스 (01, 02, 03).
MVTec: 14개의 클래스 (bottle, cable, capsule, ...).
사전 학습된 모델 사용:
MobileNetV2
WideResNet50
Top-K 이웃 거리 기반 점수 계산:
학습 데이터와 테스트 데이터 간 유클리디안 거리 기반 점수 계산.
ROC AUC 계산 및 시각화:
클래스별 ROC AUC 점수와 평균 ROC AUC 출력.
ROC 곡선을 이미지로 저장.
