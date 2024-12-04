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
