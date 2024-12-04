# 🚀 **BTAD 및 MVTec 데이터셋을 활용한 이상 탐지**

## 📖 **프로젝트 개요**
이 프로젝트는 **BTAD**와 **MVTec** 데이터셋을 활용하여 **이상 탐지(Anomaly Detection)**를 수행하는 파이프라인입니다.  
사전 학습된 **MobileNetV2**와 **WideResNet50** 모델을 활용해 특징 벡터를 추출하고, **Top-K 이웃 거리 기반**으로 이상 점수를 계산합니다.

---

## 🛠️ **요구사항**
### **필수 라이브러리**
- `torch`
- `torchvision`
- `numpy`
- `scikit-learn`
- `matplotlib`
- `tqdm`
- `Pillow`

### **설치 방법**
▶️ 아래 명령어를 사용해 필수 라이브러리를 설치하세요:
```bash
pip install torch torchvision numpy scikit-learn matplotlib tqdm pillow
```

---
## 🗂️ **데이터 셋**
### **BTAD(Btech Anomaly Detection Dataset)**
- 3개의 클래스('01', '02', '03')로 구성
- 각 클래스는 학습용 정상 데이터와 테스트용 정상/결함 데이터를 포함합니다.
  
- **데이터 다운로드 링크**
  [https://avires.dimi.uniud.it/papers/btad/btad.zip]

### **MVTec AD (MVTec Anomaly Detection Dataset)**
- 15개의 클래스(`bottle`, `cable`, `capsule` 등)로 구성되어 있습니다.
- 클래스별로 다양한 종류의 결함 데이터(스크래치, 파손 등)와 정상 데이터를 포함합니다
  
- **데이터 다운로드 링크**
  [https://www.mydrive.ch/shares/38536/3830184030e49fe74747669442f0f282/download/420938113-1629952094/mvtec_anomaly_detection.tar.xz]

---

## ⚙️ **사용법**
1️⃣ BTAD 데이터셋 실행
```bash
python main.py --dataset BTAD --save_path ./btad_results
```
2️⃣ MVTec 데이터셋 실행
```bash
python main.py --dataset MVTec --root_path /path/to/mvtec --save_path ./mvtec_results
```

## 📊 **주요 결과**
1️⃣ ROC AUC 점수

2️⃣ ROC 곡선 시각화

## 📜 **프로젝트 주요 로직**

### 1️⃣ **특징 추출**
- **MobileNetV2**와 **WideResNet50** 모델의 특정 레이어 출력을 **후크(Hook)**를 통해 저장합니다.
- 사전 학습된 모델을 사용하여 학습 데이터와 테스트 데이터의 특징 벡터를 추출합니다.

### 2️⃣ **거리 계산**
- `calc_dist_matrix` 함수를 사용하여 학습 데이터와 테스트 데이터 간의 **유클리디안 거리**를 계산합니다.
- 거리 행렬을 통해 데이터 포인트 간의 유사성을 평가합니다.

### 3️⃣ **이상 점수 계산**
- **Top-K 이웃 거리 평균**을 이상 점수로 활용합니다.
- 테스트 데이터의 특징 벡터와 학습 데이터의 특징 벡터 간 거리를 기반으로 이상 여부를 판단합니다.

### 4️⃣ **ROC AUC 평가**
- 테스트 데이터의 이상 점수와 실제 라벨을 사용하여 **ROC AUC 점수**를 계산합니다.
- 결과를 기반으로 **ROC 곡선 이미지를 저장**합니다.




