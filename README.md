# 연구 목표
![image](https://github.com/user-attachments/assets/5b1945f5-b773-43e7-a2c0-6f09de1fa61d)

- 손글씨 이미지 데이터
    - https://web.archive.org/web/20180211213318/http://yann.lecun.com/exdb/mnist
    - THE MNIST DATABASE of handwritten digits

- 데이터 특징
    - 손글씨 이미지 정답
        - 0 ~ 9
        - 다중분류(활성화함수 softmax)
    - 훈련용
        - 60000
    - 테스트용
        - 10000
    - 이미지 1개
        - h, w = 28, 28 픽셀
        - feature = 28*28 => 784
            - 픽셀 1개를 피처 1개로 인지
        - 색상
            - color
                - 3채널 (RGB) 데이터 존재
                - R,G, B 당 각각 256 색상 제공
            - grayscale
                - 1채널 (흑백, 회색톤)
                - 0 ~ 255, 색상수 256개
                - MNIST은 여기에 해당
                    - 784*1 로 이미지 1장당 데이터 제공

- 방식
    - 텐서플로우 2.x, 케라스 활용
    - 필요시 조기 학습 종료 적용
    - 필요시 GPU 학습 진행

- 결론
    - 서비스
        - 손글씨 이미지 입력 -> CNN 기반 모델 예측 -> 이 글자는 5이다(정확도 x%, 손실값 0.00xx)
    - 학습
        - 이미지를 잘 분류할수 잇는 가중치, 편향을 최적으로 찾는 과정(특정 신경망 형태에서)
    - 최종 산출물
        - 필요시 모델 덤프 -> 서비스와 연계
    - shape 구성은 일부 다를수 있음
![image](https://github.com/user-attachments/assets/df703b52-b21e-4215-910f-50b46f9f11fe)

![image](https://github.com/user-attachments/assets/47541e10-66da-43fe-8be1-944d2ec435ce)

---

# 전이학습 - tensorflow.keras
- 전이 학습 스타일 습득
    - 사전 학습된 업스트림 모델을 사용
        - 가중치 유지
            - **업스트림의 파라미터를 훈련 불가능하게 설정**
    - 다운스트림에서는 CT 사진 주입 학습
        - 추가된 신경망 부분만 학습
            - 이진 분류(정상/치매)
        - 파인튜닝 수행
- 데이터
    - 치매/정상 뇌 스캔 CT 사진(grayscale)

- 활용
    - 환자 -> CT사진촬영 -> x%의 확률로 진단/소견
 
# 데이터
- 비전 데이터
    - 데이터가 소량인 경우 -> 이미지 부풀리기 진행 가능
        - 의료용은 배제
