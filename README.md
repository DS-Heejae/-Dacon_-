# 회귀분석 프로젝트

> Dacon - AI프렌즈 시즌1 온도 추정 경진 대회
![dacon](https://user-images.githubusercontent.com/60166667/78556644-4ba15a00-784a-11ea-939a-e5862cb13644.png)


## 1. 데이터 설명
![sensor](https://user-images.githubusercontent.com/60166667/78556685-61af1a80-784a-11ea-9e0d-624f38f94810.png)
 - 대전지역에서 측정한 실내외 19곳의 센서데이터와 주변 지역의 기상청 공공데이터를 semi-비식별화하여 제공합니다.
 - 센서는 온도를 측정하였습니다.
 - 모든 데이터는 시간 순으로 정렬 되어 있으며 10분 단위 데이터 입니다.
 - 예측 대상(target variable)은 Y18입니다.

 - train.csv
    - 30일 간의 기상청 데이터 (X00 - X39) 및 센서데이터 (Y00 - Y17)
    - 이후 3일 간의 기상청 데이터 (X00 - X39) 및 센서데이터 (Y18)

 - test.csv
    - train.csv 기간 이후 80일 간의 기상청 데이터 (X00 - X39)

 - sample_submission.csv
    - 제출 양식 예시


## 2.분석 과정
![dataset](https://user-images.githubusercontent.com/60166667/78556804-97540380-784a-11ea-86c4-73d3f129e186.png)

- (1) train data
 - a. 데이터 전처리
   - id: 10분 단위의 수치 값이 입력되어 있어서, 시간으로 변환
   
   - 풍향["X13","X15","X17","X25","X35"]: 북동(0), 남동(1), 남서(2), 북서(3)로 카테고리 변수로 변경
    
   - 일일 누적 강수량["X04","X10","X21","X36","X39"]: 
     -  현재 데이터는 누적강수량 데이터로 측정시각 이전에 내린 강수량의 합.
     -  현재 온도에 미래의 강수량이 영향을 주지 못하므로, 온도 측정 시각의 누적강수량에서 이전 온도 측정 시각의 누적강수량을 빼서 계산. 
     - 실수형 데이터로 예측모델을 만든 결과보다 카테고리형 데이터로 예측모델을 만들었을 경우 성능이 더 좋아 카테고리 변수로 변경. 
     - 강수량에 따라 0, 1, 2, 3으로 나눈 모델과 강수가 있었을 경우 1, 없었을 경우 0으로 나눈 모델 중 후자가 더 성능이 좋았음.
   
 - b. 결측치(위의 이미지에서 공란) 예측
    - Y00~Y17의 이후 3일치 먼저 예측: OLS 활용, KFold 교차검증(성능: 대부분 95%이상)
    - 33일치의 값이 채워진 Y00~Y17로 Y18의 이전 30일 예측: 
      - 스케일링, OLS : accuracy_score와 mse가 좋게 나왔으나, 이를 활용해 구한 전체 데이터로 예측 모델을 만들 경우 성능이 좋지 못함.
      <img width="866" alt="스크린샷 2020-05-08 오후 6 08 24" src="https://user-images.githubusercontent.com/60166667/81390776-fb722c00-9156-11ea-9b20-a0bc6b903354.png">
      
      - 정규화(Lasso, Ridge, Elastic Net), KFold 교차 검증: Lasso가 가장 좋은 성능을 가짐.
   <img width="861" alt="스크린샷 2020-05-08 오후 6 09 21" src="https://user-images.githubusercontent.com/60166667/81390824-0cbb3880-9157-11ea-8069-160b28316f6a.png">
   

- (2) test data(이후 80일): 전체 X 변수를 활용하여 Y18 예측
  
## 3. test 데이터의 Y18 예측 위해 시도해본 모델
  - 성능 향상을 위해 머신러닝 기법 적용: LGBM, RandomForestRegressor
    - RandomForestRegressor의 성능이 가장 좋았음. (MSE: 3.94)
    
 - 각 변수 그룹 별 평균 값으로 OLS 적용 MSE : 4.60(좋지 못한 방법) 
 - OLS 모델: MSE 5.46
 - Lasso 모델: MSE 6.75
 - OLS + Lasso + OLS 모델: MSE 3.99
 - OLS + Lasso + Lasso 모델: MSE 5.30
    
## 4. 목표 성능
- test MSE 3.5 이하로 만들기 -> 결과: 3.94
- 최종 순위 20등 이내 -> 40위(총 378명 참가) 

## 5. 분석에 필요한 패키지
 - requirements.txt
