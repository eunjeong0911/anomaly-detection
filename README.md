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
아래 명령어를 사용해 필수 라이브러리를 설치하세요:
```bash
pip install torch torchvision numpy scikit-learn matplotlib tqdm pillow
```

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
1️⃣ 특징 추출
- MobileNetV2와 WideResNet50 모델의 특정 레이어 출력을 후크(Hook)를 통해 저장.
- 사전 학습된 모델을 사용하여 학습 및 테스트 데이터의 특징 벡터를 추출.
2️⃣ 거리 계산
- calc_dist_matrix 함수를 활용해 학습 데이터와 테스트 데이터 간 유클리디안 거리 계산.
3️⃣ 이상 점수 계산
- 거리 행렬에서 Top-K 이웃 거리 평균을 이상 점수로 사용합니다.
4️⃣ ROC AUC 평가
- ROC AUC 점수를 계산하고, ROC 곡선을 이미지로 저장.


