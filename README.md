# 회귀분석 프로젝트

> Dacon - AI프렌즈 시즌1 온도 추정 경진 대회
- 팀원: 양준, 오진경, 윤예슬, 이희재
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


## 2.결과
 - MSE 3.94, 상위 11%(총 378명 참가) 

## 3. 데이터 전처리 & 분석 과정
<img width="880" alt="스크린샷 2020-06-04 오후 10 12 06" src="https://user-images.githubusercontent.com/60166667/83760886-88ee6080-a6b0-11ea-9ac8-b3f4d2c8d6aa.png">
<img width="883" alt="스크린샷 2020-06-04 오후 10 12 13" src="https://user-images.githubusercontent.com/60166667/83760887-8a1f8d80-a6b0-11ea-839e-b7b81f0b13c7.png">


## 4.프로젝트 결과물

[회귀분석프로젝트.pdf](https://github.com/DS-Heejae/linear-regression-project-dacon/files/4725256/default.pdf)


## 5. 분석에 필요한 패키지
 - requirements.txt
