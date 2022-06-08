# Chat-bot-with-deep-learning
## 국민비서 '국삐' 구현
#### 레퍼런스 레포지토리 : https://github.com/keiraydev/chatbot

### 1. 문제 설정

- 정책 프로그램 신청 시기가 되면 관련하여 많은 문의가 발생함
- 챗봇이 단순 문의에 응답할 수 있다면 업무 부담을 낮출 수 있음

### 2. 목표 설정

- 입력된 문장에서 규칙을 찾아내고, 규칙에 해당하는 답변을 출력하는 롤 베이스 챗봇을 구현함
  - 정해진 답변만 출력할 수 있지만 양질의 데이터가 없어도 설계화 훈련이 비교적 간단함
  - 입력되는 질문의 범위가 한정될 경우 좋은 성능을 보임

### 3. 모델의 구조

<img width="770" alt="Screen Shot 2022-04-28 at 9 48 54 PM" src="https://user-images.githubusercontent.com/93904398/165755631-7a43c229-c8ff-465f-a712-7689b456a5c7.png">

- Konlpy : 입력 문장을 형태소 단위로 토큰화
- CNN : 입력 문장의 의도를 예측(어떤 의도로 말을 건 것인가?)
  - 입력 데이터를 병렬 처리할 수 있는 모델
  - 문장의 지역 정보를 학습하여 예측을 진행하기 때문에 문맥을 고려할 수 있음
- BILSTM : 입력 문장의 개체명을 예측(무엇에 대한 질문인가?)
  - 개체명 예측에는 문장의 순서 정보가 중요함
  - 긴 문장에도 준수한 예측력을 보이는 LSTM을 사용
  - 양방향 LSTM으로 문맥을 입체적으로 고려함

### 4. 모델의 성능

<img width="650" alt="Screen Shot 2022-04-28 at 9 52 59 PM" src="https://user-images.githubusercontent.com/93904398/165756409-b9aaa0bb-6f3f-4de7-a770-0d9dabbcfa28.png">

### 5. 개선 지점

1) 다양한 시나리오 개발 필요
- Intent를 추가하여 시나리오를 다양화
- 개체명을 세분화하여 전달할 수 있는 정보를 풍부화

2) 답변 속도 개선
- Seqeuntial Model인 BILSTM보다 병렬처리 모델인 Transformer를 사용하여 답변 속도를 개선할 필요가 있음

3) 리뷰 데이터 수집 및 활용
- 말뭉치 사전을 만들기 위해 리뷰 데이터를 직접 수집 후 활용할 필요가 있음
