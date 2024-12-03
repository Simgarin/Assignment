# **Diffusion MakeUp - Face Lab**  
**2020114660 인공지능학과 심가린**

## **1.Project Results and Overview**
1. **Objectives**
이 프로젝트는 Stable Diffusion 기반의 생성형 AI를 활용하여 가상 메이크업 시뮬레이션을 제공하는 시스템을 개발하는 것을 목표로 합니다. 사용자는 메이크업 사진(Reference Image)을 입력하여 자연스럽고 고품질의 메이크업 효과를 적용받을 수 있습니다.
2. **Results and Insights**
- 기존 모델의 한계 극복: 기존 메이크업 생성 모델에서 발생하는 Source 이미지의 얼굴과 다른 결과를 생성하는 문제를 분석하고 전통 CV 방법을 활용하여 간단하고 빠르게 해결책을 제안했습니다.
- 속도 개선 : Text 2 Img 파이프라인에서에서 Img 2 Img 파이프라인으로 수정하여 속도 향상에 기여했습니다. 

## **2.Source Code**
├── assets/               # 참고 및 Readme용 이미지
├── dataset/              # 학습용 dataset
│   ├── facemorpher/           # 학습을 위한 facemorphing
|   ├── ledits_utils/          # Face parsing
├── detail_encoder/       # 메이크업 정보 추출을 위한 encoder 및 clip
├── diffuser/             # Stable Diffusion의 pipeline들
├── models/               # Pretrained model 저장 경로
├── test_imgs/            # test용 이미지 저장 경로
├── gradio_demo_kps.py        # gradio를 이용한 webui 실행
├── infer_kps.py              # pipeline과 gardio_demo_kps 연결
├── pipeline_sd15.py          # FaceLab의 pipeline
├── train.py                  # Train
├── requirements.txt          # Python dependencies

## **3.Performance Metrics**
- 속도 : 8.2s ~ 9.8s
- 결과
### **수정 전**

기존 Stable Makeup
![image](https://github.com/user-attachments/assets/4722f650-2a05-4c0a-9ac6-9641a73ef47f)


### **수정 후**

vae.decode 이전에 detail latent mix
![image](https://github.com/user-attachments/assets/71571431-edc9-422f-a0c0-db9b1f6b8ea3)


![image](https://github.com/user-attachments/assets/07d70741-b59e-40c4-98a3-e92b9e92878e)


### **결과물**

가벼운 데일리 메이크업(메이크업 유지 strength 1.2), 진한 분장(메이크업 유지 strength 2)
![image](https://github.com/user-attachments/assets/1b455e1b-aecd-40d0-905f-9709aa3097c0)


## **4.Installation and Usage**
- Python >= 3.8
- PyTorch >= 1.10
[diffusers](https://github.com/huggingface/diffusers/) version of Stable Diffusion v1-5.
[SPIGA](https://github.com/andresprados/SPIGA)
[facelib](https://github.com/sajjjadayobi/FaceLib)

1. **Installation**
Project Clone
```bash
   git clone https://github.com/Simgarin/diffusion-makeup
   cd diffusion-makeup
```
2. **Requirements installation**
```bash
   pip install -r requirements.txt
```
3. **Usage**
### Gradio demo, Pretrained model

[Google Drive](https://drive.google.com/drive/folders/1397t27GrUyLPnj17qVpKWGwg93EcaFfg?usp=sharing).
다음 링크에서 사전학습된 모델을 받을 수 있습니다
models/stablemakeup 경로에 내려받아주세요.

사전학습된 clip을 이용합니다.
huggingface에서 openai/clip-vit-base-patch32를 내려받아 models 폴더에 넣어주세요

사전학습된 stable diffusion model을 사용합니다.
gradio_demo_kps.py에는 danbrown/RevAnimated-v1-2-2을 이용합니다.
원하는 sd1.5 pretrained model을 입력하시면 됩니다.

Pretrained model을 내려받아 demo버전을 사용할 수 있습니다.
gradio 라이브러리를 이용해 webui로 연결됩니다.
```python
python gradio_demo_kps.py
```

## **5.References and Documentation**
**참고 논문**
Stable-Makeup: When Real-World Makeup Transfer Meets Diffusion Model, Yuxuan Zhang et al., arXiv:2403.07764v1
Toward Tiny and High-quality Facial Makeup with Data Amplify Learning, Qiaoqiao Jin et al., arXiv:2403.15033v1

## **6. Issues and Contributions**
Reference 이미지 품질이 낮을 경우 결과의 품질 저하.
특정 얼굴 구조에서는 메이크업 적용의 일관성이 떨어질 수 있음.
메이크업 종류에 따라 강도 조절 필요.
Detail Latent 추가에 따른 noise 증가.

## **7. Future Work**
**성능 개선**
얼굴 구조에 따라 메이크업 적용을 최적화하는 방법 연구.
Reference 이미지 품질 저하 문제 해결을 위한 보정 알고리즘 추가.
**실시간 처리**
처리 속도를 개선하여 실시간 애플리케이션 가능성 확대.
**사용성 개선**
사용자 인터페이스 추가 및 다양한 플랫폼 지원.
