[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/FVjNDCrt)
# CV1 - Document Type Classification Competitions
## Team

| ![박패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![최패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![오패캠](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [최제우](https://github.com/UpstageAILab)             |            [이아윤](https://github.com/UpstageAILab)             |            [이승현](https://github.com/UpstageAILab)             |            [이한국](https://github.com/UpstageAILab)             |            [현재호](https://github.com/UpstageAILab)             |
|                            팀원                             |                            팀원                             |                            팀원                             |                            팀원                             |                            팀원                             |

## 0. Overview
### Environment
- VSC, server RTX 3090
- 협업 환경 : Notion, Slack
- 소통 환경 : Zoom, Slack

## 1. Competiton Info
- Document Type Classification / 17종 문서 타입 분류
  
### Overview

![image](https://github.com/user-attachments/assets/2dbfea5b-b253-4fd1-b612-43dbc684a6d1)


### Timeline

- July 30, 2024 - Start Date
- August 11, 2024 - Final submission deadline

### Evaluation 
- Macro F1
- ![image](https://github.com/user-attachments/assets/bf58d333-afcc-4669-8fd9-d03a4ca64857)


## 2. Components

### Directory
```bash
├── code(.ipynb)
│   ├── EDA
│   ├── Augmentation
│   ├── Modeling
│   └── train.py
├── docs
│   ├── pdf
│   │   └── (Template) [패스트캠퍼스] Upstage AI Lab 1기_그룹 스터디 .pptx
│   └── Notion
└── input
    └── data
        ├── test
        ├── valid
        └── train
```

## 3. Data descrption

### Dataset overview

- ![image](https://github.com/user-attachments/assets/b18505d3-e72f-45d2-9b89-b6cf05dff381)


### EDA
- 데이터 기본정보 확인, 이미지 샘플 시각화, 클래스 분포 시각화, 이미지 크기 확인, 클래스 불균형 확인 
- ![image](https://github.com/user-attachments/assets/440c81b4-561d-40cf-ad6e-2f34521dfdb7)
- ![image](https://github.com/user-attachments/assets/d438536b-6f44-46f8-a252-6a9a578c9385)
- ![image](https://github.com/user-attachments/assets/f98266f3-6d5e-4c72-93a6-dde55b72e0da)
- ![image](https://github.com/user-attachments/assets/2db44821-f42b-4da5-823c-c33f9323976d)
- 

### Data Processing

- ![image](https://github.com/user-attachments/assets/cb42186b-7a3c-4eb7-abe0-e92561e28ebe)

## 4. Modeling

### Model descrition
#### 최제우
- EfficientNet(efficientnet_b0), ResNet(resnet34, resnet50)을 활용
- 모델 별로 image_size, batch_size를 병경
#### 이아윤
- timm - resnet34, resnet50, efficientnet_b0, efficientnet_b4 모델로 실험
  - 시간과 성능 고려하여 efficientnet_b0 고정 

### Modeling Process

-timm을 사용하여 미리 학습된 모델을 로드
<code>
model = timm.create_model(
    model_name,
    pretrained=True,
    num_classes=17
).to(device)
</code>
#### 최제우
- backbone : resnet34, resnet50, efficientnet_b0
- image_size : 224, 256, 521
- batch_size : 16, 32
- scheduler를 사용하여 learning rate 조절
  <code>
  scheduler = optim.lr_scheduler.LambdaLR(optimizer=optimizer,
                                      lr_lambda=lambda epoch: 0.95 ** epoch,
                                      last_epoch=-1,
                                      verbose=False)
  </code>
#### 이아윤
- 가중치 : 시각화를 통해 양식이 유사한 3, 7, 14 클래스에 대한 예측 성능이 떨어진다는 것을 확인 -> 가중치 증가를 통해 성능 향상
- 학습률 : 0.001 ~ 0.005 실험 통해 -> 0.001
- Earlystopping : patience 3
- Loss function : Cross-Entropy Loss, Adam 

## 5. Result
- Train Accuracy: 0.8797, Train F1 Score: 0.8526, Validation Accuracy: 0.8604, Validation F1 Score: 0.8224

### Leader Board
- Leaderboard_mid
  - ![image](https://github.com/user-attachments/assets/664528d7-cdfc-4e77-ac84-d9ebdbb5bb73)

- Leaderboard_final
  - ![image](https://github.com/user-attachments/assets/bd911d2d-81c1-4d14-ab8a-0429ce327856)

### Presentation

- _Insert your presentaion file(pdf) link_

## etc

