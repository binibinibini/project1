# project1

## 렌터카 결함 탐지

1. 프로젝트 개요 <br>
  딥러닝 기술을 활용하여 렌터카의 외관 결함을 자동으로 식별하고 분류하는 시스템을 개발하는 것을 목표로 합니다. <br>
  수동 검사 과정에서 발생하는 시간 낭비와 고객-업체 간의 분쟁을 최소화하고, 차량 검사 시간을 줄여 관리 효율을 극대화하고자 합니다.<br>

     - 결함 분류 :  입력된 차량 이미지를 손상(Damaged), 비손상(Undamaged), 무관(Unrelated)의 3가지 클래스로 분류합니다.
     - 웹 기반 서비스 : Flask 서버와 연동하여 웹 인터페이스를 통해 사용자가 이미지를 업로드하고 즉시 탐지 결과를 확인할 수 있습니다.

<br>

2. 기술 스택<br>
   - 딥러닝 프레임워크 : PyTorch
   - 백엔드/서버 : Python, Flask
   - 프론트엔드 : JavaScript(JS)
   - 데이터베이스 : SQLite3
   - 모델 : EfficientNet B0

<br>

3. 모델 개발 및 학습<br>
   - 모델 선정 근거<br>
   빠른 추론 시간과 높은 정확도를 동시에 고려했습니다. EfficientNet B0는 MobileNet V2 대비 정확도가 높고, ResNet-50 대비 파라미터 수가 적어 최종 개발 모델로 채택되었습니다.<br>
   
     ResNet-50
     - Inference Time : 0.0783
     - Parameters : 25557032
     - Top-1 Accuracy : 76.1%
     <br>
     
     EfficientNet B0
      - Inference Time : 0.0331
      - Parameters : 5288548
      - Top-1 Accuracy : 77.1%
     <br>
     
     MobileNet V2
      - Inference Time : 0.0267
      - Parameters : 3504872
      - Top-1 Accuracy : 71.8%

<br>

4. 역할
   - 데이터셋 수집
     모델 학습을 위해 데이터셋은 3가지 클래스로 레이블링 되었습니다.
     - Damaged (결함이 있는 차량 이미지)
     - Undamaged (결함이 없는 차량 이미지)
     - Unrelated (차량이 아닌 일반 이미지)
       
   - 데이터 전처리
     - 이미지 표준화 : 모든 이미지를 (224, 224) 픽셀 크기로 통일하여 모델의 입력 형식에 맞추었습니다.
     - 정규화 : 데이터 모두에 표준 정규화(Normalize)를 적용했습니다.
     - 클래스 정의 및 조정 : 최종적으로 데이터셋의 클래스 수에 맞춰 모델의 마지막 레이어를 3개 클래스로 설정했습니다. <br>
                            이 3-Class 모델은 초기 2-Class 모델 대비 정확도 3.61% 개선, F1 Score 3.67% 개선, Loss 66.51% 감소의 성능 향상을 가져왔습니다.

   - 데이터 증강 <br>
     - RandomHorizontalFlip : 이미지를 무작위로 수평 뒤집기 <br>
     - RandomRotation : 이미지를 200도 내외로 무작위 회전 <br>
     - ColorJitter : 밝기, 대비, 채도, 색조 등 변경 <br>

     <img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/704a7093-fcd4-42bb-afe4-3208d89ce366" />

     
     
     
