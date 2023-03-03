# 위치와 사용자 취향을 반영한 데이트 경로 추천 시스템

## 1. 프로젝트 설명

#### (1) 주제 및 배경
- 주제 : 사용자의 위치, 취향을 반영하여 맛집, 카페를 경유하는 경로 추천 시스템 개발
- 사전자료 : 모바일 앱 "완벽한 하루"


<img width = "500" src="https://user-images.githubusercontent.com/102526342/222642175-d06dd936-5e63-4c25-a92e-44acce96d16d.png">


#### (2) 모델
- NFC모델(강남구 예시)
    - 공통 파라미터
        - MLP layers = [64, 32, 16, 8], Activation function = tanh, Optimizer = adam, Call back  = 5patience
    - Random search hyper parameter
        - 레스토랑 : batch_size =  512, learnig_rate = 0.005, number of epochs = 50, number of factors = 8
        - 카페 : batch_size =  128, learnig_rate = 0.007, number of epochs = 200, number of factors = 4      

- CBF 모델(강남구 예시)
    - konlpy의 okt 로 user, item matrix의 명사 태그를 추출 -> word2vec으로 두 매트릭스를 임베딩 -> k-means로 word를 120개로 클러스터링
    - id별 group에 해당하는 총 숫자의 개수가 일정하지 않기 때문에 정규화
    - cbf score : 추천할 id의 user matrix의 벡터와 place matrix를 곱하여 cosine similarity를 측정 -> place에 대한 선호도 구함

- Hybrid 모델 
    - cbf score 와 ncf score 을 곱하여 최종 result score을 구하여 큰 값으로 정렬
 
 #### (3) 결과
 - naver api과 folium을 사용해 지도로 사용자에게 보여주고, 예상거리와 택시비까지 출력하여 제시
 
<img width = "500" src="https://user-images.githubusercontent.com/102526342/222641680-28c3fd0e-aacb-427f-bcb6-74ecf50c71d3.png">
<img width = "500" src="https://user-images.githubusercontent.com/102526342/222641893-e0264d22-a9e4-484a-a4b9-ee3f31e5f53c.png">

 

2. 레퍼런스
#### (1) NCF, CBF
- https://github.com/DAC-KHUPID/seoul-date-course-recommendation
#### (2) Naver API Direction5
- https://velog.io/@choonsik_mom/Naver-API%EB%A1%9C-%EA%B8%B8%EC%B0%BE%EA%B8%B0with-python
