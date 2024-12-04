# 🚀 **PaDiM 기반 BTAD 및 MVTec 데이터셋 이상 탐지**

## 📖 **프로젝트 개요**
이 프로젝트는 **BTAD**와 **MVTec** 데이터셋을 활용하여 **사전 학습된 특징 추출 모델**과 **유클리디안 거리 기반** 이상 점수 계산 방식을 결합한 **이상 탐지(Anomaly Detection)**를 수행합니다.  
PaDiM(Patch Distribution Modeling)을 기반으로, 학습 데이터의 정상 특징 벡터를 활용해 테스트 이미지의 이상 점수를 산출합니다.

**Google Colab에서 실행하기** 
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/12qrIF3lPCsk0QGX_n5iFEd_Q1WHu-_JT?usp=sharing)
- 위 버튼을 클릭하면 Google Colab에서 바로 코드를 실행할 수 있습니다.
- 데이터를 준비한 뒤 모든 셀을 순서대로 실행할 수 있습니다.

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
▶️ 아래 명령어를 사용해 필수 라이브러리를 설치:
```bash
pip install torch torchvision numpy scikit-learn matplotlib tqdm pillow
```

---

## 🗂️ **데이터 셋**
### **BTAD(Btech Anomaly Detection Dataset)**
- 3개의 클래스('01', '02', '03')로 구성되어 있습니다.
- 각 클래스는 학습용 정상 데이터와 테스트용 정상/결함 데이터를 포함합니다.
  
- **데이터 다운로드 링크**
  [https://avires.dimi.uniud.it/papers/btad/btad.zip]

### **MVTec AD (MVTec Anomaly Detection Dataset)**
- 15개의 클래스(`bottle`, `cable`, `capsule` 등)로 구성되어 있습니다.
- 클래스별로 다양한 종류의 결함 데이터(스크래치, 파손 등)와 정상 데이터를 포함합니다.
  
- **데이터 다운로드 링크**
  [https://www.mydrive.ch/shares/38536/3830184030e49fe74747669442f0f282/download/420938113-1629952094/mvtec_anomaly_detection.tar.xz]

▶️ 데이터 준비 방법
1. 아래 링크에서 **BTAD**, **MVTec** 데이터셋 다운로드할 수 있습니다.
2. 다운로드한 데이터를 다음 디렉토리 구조에 배치:
 - BTAD: `/content/drive/MyDrive/BTech_Dataset_transformed`
 - MVTec: `/content/drive/MyDrive/mvtec`

---

## 📊 **ROC Curve 결과**
### **MVTec 데이터셋**
- 아래는 MVTec 데이터셋에서 얻은 ROC 곡선입니다:
![MVTec ROC Curve](https://drive.google.com/uc?id=1mVNLymYeTg8ri6Q1wzsFmp1mZTIWx-M5)

### **BTAD 데이터셋**
- 아래는 BTAD 데이터셋에서 얻은 ROC 곡선입니다:
![BTAD ROC Curve](https://drive.google.com/uc?id=1mVNLymYeTg8ri6Q1wzsFmp1mZTIWx-M5)

---

## 🧠 **주요 로직** :

### 1️⃣ 특징 벡터 추출
- MobileNetV2와 WideResNet50 모델의 특정 레이어에서 특징 벡터를 추출합니다.
- PyTorch Hook을 사용하여 모델의 중간 출력을 저장합니다.
- 학습 데이터에서는 추출된 특징 벡터를 저장하고, 테스트 데이터에서는 이를 활용해 이상 점수를 계산합니다.

### 2️⃣ **유클리디안 거리 기반 계산**
- 학습 데이터와 테스트 데이터의 특징 벡터 사이의 **유클리디안 거리**를 계산합니다.

- **calc_dist_matrix 함수**:
  - 학습 데이터와 테스트 데이터 간의 거리 행렬을 생성합니다.
  - 거리는 아래 수식으로 계산됩니다:

  - ![유클리디안 거리 공식](https://latex.codecogs.com/png.latex?d(x,y)%20=%20\sqrt{\sum_{i}(x_i%20-%20y_i)^2})


### 3️⃣ Top-K 평균 거리 계산
- 테스트 데이터의 각 패치에 대해 학습 데이터의 특징 벡터와의 거리를 계산합니다.
- 가장 가까운 K개의 이웃 거리 평균을 이상 점수로 사용합니다.
- 이상 점수가 높을수록 이상 가능성이 높습니다.

