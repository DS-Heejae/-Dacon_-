# linear-regression-project-dacon
회귀분석 프로젝트로 진행한 dacon_센서 온도 추정 경진대회 관련 내용입니다.

1. 대회
![dacon](https://user-images.githubusercontent.com/60166667/78556644-4ba15a00-784a-11ea-939a-e5862cb13644.png)

2. 데이터 설명
![sensor](https://user-images.githubusercontent.com/60166667/78556685-61af1a80-784a-11ea-9e0d-624f38f94810.png)
 - 대전지역에서 측정한 실내외 19곳의 센서데이터와 주변 지역의 기상청 공공데이터를 semi-비식별화하여 제공합니다.
 - 센서는 온도를 측정하였습니다.
 - 모든 데이터는 시간 순으로 정렬 되어 있으며 10분 단위 데이터 입니다.
 - 예측 대상(target variable)은 Y18입니다.

 - train.csv
    - 30일 간의 기상청 데이터 (X00 - X39) 및 센서데이터 (Y00 - Y17)
    - 이후 3일 간의 기상청 데이터 (X00~X39) 및 센서데이터 (Y18)

 - test.csv
    - train.csv 기간 이후 80일 간의 기상청 데이터 (X00~X39)

 - sample_submission.csv
    - 제출 양식 예시


3. 데이터 상세 소개(공란: 결측치 -> 예측 필요)
![dataset](https://user-images.githubusercontent.com/60166667/78556804-97540380-784a-11ea-86c4-73d3f129e186.png)


4. 코드 파일: 첨부된 주피터 노트북 
