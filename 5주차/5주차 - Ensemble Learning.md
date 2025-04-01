# 앙상블 러닝
>**Decision Tree의 확장판**

### 정의
- 여러 개의 모델을 조합하여 더 강력하고 안정적인 예측 모델을 생성하는 기법
- 개별 모델들이 서로 다른 학습 알고리즘을 사용 할 수도 있고, 동일한 알고리즘을 서로 다른 데이터로 학습하여 서로 다른 모델로써 활용할 수도 있다.

![앙상블러닝정의](https://private-user-images.githubusercontent.com/139729135/428872966-6c473bfa-06d8-4386-887f-32ffd7ea287a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODExODAsIm5iZiI6MTc0MzQ4MDg4MCwicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODcyOTY2LTZjNDczYmZhLTA2ZDgtNDM4Ni04ODdmLTMyZmZkN2VhMjg3YS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNDE0NDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jYzNhNmVhYmE5Zjg4MWNjNDQzOGYzNjhkNTFlNWJlOWU3ZTA4YmU3MTliZTA0MDM3MmE4YzA3OWJmZDcyMGYzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.l9kbhWpopqYW2H7J5NzJNXO7qxbcH0oXrgneQ_kz0lg)

### 목적
- **편향과 분산을 줄이고 일반화 성능 향상**

### 유형
- 앙상블 학습은 크게 **4가지** 방식으로 구성
	> 보팅(Voting), 배깅(Bagging), 부스팅(Boosting), 스태킹(Stacking)

### 장점
1. 예측 성능 향상 
	- 다양한 모델들의 예측 결과를 결합함으로써 편향과 분산을 줄이고 일반화 성능 향상
2. 안정성 
	- 오류나 노이즈에 덜 민감, 안정적인 예측 결과를 얻을 수 있음
3. 모델의 다양성 
	- 다양한 종류의 모델을 사용하거나, 동일한 알고리즘을 다른 하이퍼파라미터 설정 또는 다른 학습 데이터로 학습시킬 수 있음

### 단점
1. 높은 계산 비용 
	- 모델의 수가 많아질수록 학습 시간과 메모리 사용량이 증가함
2. 해석의 어려움 
	- 앙상블 학습에서는 다양한 모델들을 결합하여 예측 결과를 도출하기 때문에 개별 모델의 기여도를 해석하는 것이 어려울 수 있음
3. 데이터 불균형 문제 
	- 일부 모델이 학습 데이터를 무작위로 샘플링하거나 가중치를 부여하는 경우가 있어 데이터의 불균형이나 과적합 문제가 발생할 수 있음

<br>

> #### 앙상블 러닝은 적절한 앙상블 기법과 매개변수를 선택하여 성능을 극대화하고 단점을 최소화 하도록 고려해야 함

---

<br>

# 1. Voting

### 정의
- 다양한 예측 모델들의 결과에 대해 투표하여 최종 예측을 수행하는 방법
	>여러개의 예측 모델이 독립적으로 학습되고 예측을 수행 -> 각 모델의 예측 결과를 투표하여 다수결의 원칙에 따라 최종 예측 결정

![보팅정의](https://private-user-images.githubusercontent.com/139729135/428882489-05646a1b-2035-4aae-a481-639b58cb9c63.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODQyMDYsIm5iZiI6MTc0MzQ4MzkwNiwicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODgyNDg5LTA1NjQ2YTFiLTIwMzUtNGFhZS1hNDgxLTYzOWI1OGNiOWM2My5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNTA1MDZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jYmJjNzY3MzM4Nzc5NjczNGJkM2YyNzc5MmM3MzM2ZThhY2FlZTIzMDBjNGNlY2YxYzQzMjIyYmExOGYwNjhmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.UPBk8zVsxp-SFNqqySR30WHpRXID501EwakcUpN5SQQ)

### 특징
- **예측 성능 향상** : 모델들 사이의 오류를 상쇄시킴으로써 예측 성능 향상
- **일반화 성능 향상** : 다양한 모델들의 결합으로 인해 모델의 일반화 성능 향상
- **과적합 방지**

### Hard Voting
- 각 모델의 예측 결과 중 가장 많이 예측된 클래스를 최종 예측으로 선택하는 방식

### Soft Voting
- 각 모델의 예측 결과에 대한 확률 값을 평균하여 최종 예측을 수행하는 방식

![하드소프트보팅](https://private-user-images.githubusercontent.com/139729135/428882900-c51cc24d-809c-42df-bcc8-81327c292594.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODQzNDMsIm5iZiI6MTc0MzQ4NDA0MywicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODgyOTAwLWM1MWNjMjRkLTgwOWMtNDJkZi1iY2M4LTgxMzI3YzI5MjU5NC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNTA3MjNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0xMTI5MTEwNmIwYTIyNTY5NmI1ODUwZDUzY2RiM2U0MjgyZmJkM2VmMDhmNDA2N2FmYWVkZmQyNTMyODNjODZiJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ugqZOCy8XUEuxUq9509vLQE9PK9ytUM4DEUIGnzq4Wk)

<br>

>**일반적으로 Hard Voting보다 Soft Voting의 성능이 더 좋음**

<br>

[**Voting Model 실습**]()

---

<br>

# 2. Bagging (Random Forest)

### 정의
- **Bootstrap Aggregating**의 약자
	- 랜덤으로 데이터를 수집하여 합친다.
- Bootstrap을 이용하여 주어진 데이터셋을 Resampling하여 여러 학습 모델을 훈련시킨 뒤 Voting하는 법
- 기존 Voting과는 다르게 **동일한 알고리즘으로 여러 분류기를 만든 후** 보팅으로 최종 결과를 결정한다는 차이
>Bootstrap 랜덤 샘플링으로 각각이 다른 데이터셋 -> 동일한 알고리즘으로 학습 하여도 데이터셋이 다르기에 각 모델은 성능이 다르다는 점을 이용.

![배깅](https://private-user-images.githubusercontent.com/139729135/428883482-256c791f-8e47-4eba-9380-86d3512c9db7.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODQ0ODcsIm5iZiI6MTc0MzQ4NDE4NywicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODgzNDgyLTI1NmM3OTFmLThlNDctNGViYS05MzgwLTg2ZDM1MTJjOWRiNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNTA5NDdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lYmM1OWY2MDFiNzhmNzRmYWFhMWFkZjEyNjUxMzZhZDI4MjZmMmJlZmEyMzM3YjA3MjY0MDNhNDI3NWI1MmVkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.CGgi4NTWkPPXW3woWTB0hLx_61qzVadi66vaBLz2doA)

### 특징
- 랜덤 샘플링과 앙상블 방법을 통해 모델의 분산을 줄이고, 일반화 성능을 향상시킴

### 장점
1. 분산 감소
	- 여러 개의 모델을 학습하고 결합함으로써 모델의 분산을 줄임
	- 개별 모델들은 서로 독립적으로 학습되므로 각각의 모델은 원래 데이터셋에서 발생할 수 있는 이상치나 노이즈에 덜 민감해짐
2. 과적합 감소
	- 각 모델들은 다른 데이터 부분집합을 사용하여 학습되므로 과적합을 감소시키고 일반화 성능을 향상시킬 수 있음
3. 예측 성능 향상
	- 다수의 모델을 결합하여 예측 결과를 조합함으로써 예측 성능을 향상시킬 수 있음

### 단점
1. 높은 계산 비용
	- Bagging은 여러 개의 모델을 학습하고 조합해야 하므로 높은 계산 비용이 요구됨
2. 데이터 불균형 문제
	- Bagging에서는 일부 모델이 학습 데이터를 무작위로 샘플링하거나 가중치를 부여하는 경우가 있어 데이터의 불균형이나 소수 클래스에 대한 적은 데이터 수가 문제가 될 수 있음
	- 이를 해결하기 위해 샘플링 방법이나 가중치 조정등의 추가적인 처리가 필요할 수 있음

### Bagging Vs Voting

||Voting|Bagging|
|----|-------|------|
|결합방식|다수의 개별 모델의 예측 결과를 다수결 방식으로 결합|동일 모델을 독립적으로 학습하여 예측을 수행하고 예측 결과의 평균 또는 다수결 방식으로 결합|
|모델 다양성|서로 다른 여러 모델을 조합|동일 모델 사용|
|데이터 샘플링 방식|단일 데이터 사용|Bootstrap Sampling|

<br>

## Random Forest
- 여러 개의 의사결정 트리를 생성하고, 각 트리의 예측 결과를 조합하여 최종 결과를 예측하는 방식

### 작동 방식
	1. 부트스트랩 샘플링 : 원본데이터에서 중복을 허용하여 임의로 샘플링
	2. 랜덤 특성 선택 및 모델 학습 : 각 의사결정트리의 특성을 랜덤하게 하여 각 트리 모델 간 상관관계를 줄이고 다양성을 높여 학습
	3. 앙상블 예측 : 모든 트리의 예측 결과를 조합하여 최종 결과 예측, 분류 문제의 경우 투표방식을 사용하며 회귀문제의 경우 평균으로 계산

![Random Forest](https://private-user-images.githubusercontent.com/139729135/428887849-93410ceb-79fb-419e-905d-088bd301ff43.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODU4MzMsIm5iZiI6MTc0MzQ4NTUzMywicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODg3ODQ5LTkzNDEwY2ViLTc5ZmItNDE5ZS05MDVkLTA4OGJkMzAxZmY0My5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNTMyMTNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01NDllYzI2OGM1NzY0MWY3ZGJmYzA1ODdiN2FhZDkzNTU2Yjk1YTg2YmE3ODE4MjQwODA3OTJjZjkzYzg2YTIzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.sg0PTwGfY42s1j7Ha1YlidZHsPA-E9GuhgN7NKT2-8E)

### 장점
	- 결정 트리의 쉽고 직관적인 장점을 그대로 가지고 있음
	- 앙상블 알고리즘 중 비교적 빠름
	- 다양한 분야에서 좋은 성능을 나타냄

### 단점
	- 하이퍼파라미터가 많아서 튜닝을 위한 시간이 많이 소요됨

[**Random Forest 실습**]()

---

<br>

# 3. Boosting

### 정의 
- 앙상블 학습의 한 종류로, **약한 모델(weak model)을 여러 개 결합하여 강한 모델(strong model)을 만드는 방법**

![부스팅정의](https://private-user-images.githubusercontent.com/139729135/428888245-01d86d9c-ba33-4c1f-bb3c-78adeee5dbf7.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODU5NTcsIm5iZiI6MTc0MzQ4NTY1NywicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODg4MjQ1LTAxZDg2ZDljLWJhMzMtNGMxZi1iYjNjLTc4YWRlZWU1ZGJmNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNTM0MTdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02MmE4ZDI5MmM3Yzk2MDdjMjA2NjliYzhlN2YxZjM4MzIxZmM0ODRlNjE2YzNiMWYwMjM3MTNkYTBhN2VlMmYwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.rTiQmECJ0_XCIY5flSzISc71UonoGsBaAe9Kx_pjtp8)

### 특징
- 학습 데이터에서 잘못 예측된 샘플에 집중하여 반복적으로 학습하여 각각의 약한 모델이 상호 보완하도록 학습함

### Bagging VS Boosting

||구동방식|특징|
|---|-----|--------|
|Bagging|Random Forest|과적합 방지, 분산 감소, 독립적 학습기|
|Boosting|Gradient Boosting|과적합 가능, 분산, 편차 감소, 순차적 학습기| 

<br>

## Boosting : AdaBoost

### 정의
- 오분류된 샘플에 집중하여 학습하는 방식으로 약한 학습기들을 결합해서 강력한 학습기로 만드는 알고리즘

### 특징
- 오분류된 샘플에 집중하여 학습하므로, 이전 학습기의 오류를 보완하도록 학습됨
- 이를 통해 성능이 개선되고 학습 데이터에서 어려운 샘플에 대한 예측력이 향상될 수 있음
- 약한 학습기의 중요도를 기반으로 모델의 예측 설명력을 제공할 수 있음

>언제 사용하는 것이 좋은가? -> 분류 문제에 주로 사용, 데이터셋의 불균형 문제를 다루는데 효과적

### 동작 방식
	1. 초기화 : 모든 샘플에 동일한 가중치 할당
	2. 약한 모델 학습
		2-1. 약한 분류기 학습
		2-2. 분류기 중요도 계산
		2-3. 샘플 가중치 업데이트
		2-4. 가중치 정규화
	3. 데이터 Resampling 및 약한 모델 학습 : 순차적으로 약한 모델 학습
	4. 최종 예측 : 모든 약한 학습기의 예측 결과를 결합하여 최종 예측 수행

![아다부스트](https://private-user-images.githubusercontent.com/139729135/428891831-b3310b76-dc8e-467b-b6a7-0ad9a2abeb98.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODY5NDksIm5iZiI6MTc0MzQ4NjY0OSwicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODkxODMxLWIzMzEwYjc2LWRjOGUtNDY3Yi1iNmE3LTBhZDlhMmFiZWI5OC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNTUwNDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yM2ExMjVmNDk4NjYxYzdlZmI3NGM3OTFjNDBlYmMxYzBkNmM4MDA4ZjNlYmIzOWU5MjBkNzczZWNhMDgyOGM2JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Z9EWuO-FUMBRU-ZBSQmqzkCCaZX5b4MIew1NTksk9a8)

[**Ada Boost 동작 방식 예제**]()

### 장점
	- 과적합의 영향을 덜 받음
	- 구현이 쉬움

### 단점
	- 이상치에 민감
	- 해석의 어려움
	- 계산 복잡성
	- 하이퍼파라미터 설정 필요

<br>

## Boosting : Gradient Boost
> ### GBM : Gradient Boost Machine

### 정의
- 부스팅 알고리즘의 한 종류로 이전 학습기의 오차를 보완하여 모델을 강화하는 방식으로 동작하는 알고리즘

![Gradient Boost](https://private-user-images.githubusercontent.com/139729135/428892869-37892cd2-e410-4449-bad1-0db80433d323.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODcxMjgsIm5iZiI6MTc0MzQ4NjgyOCwicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODkyODY5LTM3ODkyY2QyLWU0MTAtNDQ0OS1iYWQxLTBkYjgwNDMzZDMyMy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNTUzNDhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT04MjE4MmFkNmZiNDZmNjg2ODEyYjAxZDc0YWUyOWMzOWEwNGZkY2YxZTM0MjUxOTlhMzM3YWRiOTI2OTAyZTAwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ZkXEYTY7MtbgN3XMCi5p0sgn8HRO59F7iqTKNjAHH-g)

### 특징
- **이전 학습기의 예측 오차에 집중하여 학습**
- 예측 성능이 높고 다양한 유형의 데이터에 적용할 수 있으며 다양한 약한 학습기를 사용할 수 있음

### 동작 방식
	1. 초기 모델 설정 (보통 평균 예측)
	2. 반복 학습
		2-1. 잔차(모델의 오류) 계산
		2-2. 잔차를 예측하는 모델 학습
		2-3. 모델 업데이트

![Gradient Boosting 동작 방식](https://private-user-images.githubusercontent.com/139729135/428893083-0d64a4d3-a398-4c3f-99d8-8572ec9c94c2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDM0ODcxNTksIm5iZiI6MTc0MzQ4Njg1OSwicGF0aCI6Ii8xMzk3MjkxMzUvNDI4ODkzMDgzLTBkNjRhNGQzLWEzOTgtNGMzZi05OWQ4LTg1NzJlYzljOTRjMi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDQwMVQwNTU0MTlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02Yzk3NzkzMThlMzRhOGQyM2Y5ODY5M2EwMzhlOGJmMzQ2ZGU5N2FmOGZiZGY3NmI4ZWI1ZjhmYjRkMDFiZTZkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.W-AvDRL0sY8pJRwxetfSsKvZbyEtkoU40FxLJ7BXYmI)

모델이 loss에 미치는 영향?

[**Gradient Boostring 동작 방식 예제**]()

### 장점
	- 구현이 쉽다
	- 높은 정확도
	- 모델의 유연함
### 단점
	- 과적합 문제
	- 메모리 문제

<br>

## Boosting : Extreme Gradient Boost (XGBoost)

### GB의 문제점
- 잔차에 너무 집중하게 되어 과적합이 발생하기 쉽다

### XG Boost
- 기존 Gradient Tree Boosting 알고리즘에 **과적합 방지를 위한 기법이 추가**된 지도 학습 알고리즘
- 기본 학습기를 의사결정트리로 하며 Gradient Boosting과 같이 Residual을 이용하여 이전 모형의 약점을 보완하는 방식으로 학습

### Regularization
- 과적합을 방지하고 일반화 성능을 개선하기 위해 사용
- 모델의 복잡성을 제어하여 과적합을 방지

![[Pasted image 20250401123426.png]]

### 실행 과정
	1. 초기 모델 설정
	2. 분기 기준 찾기 및 분기 실행
		2-1. 각 Root/Leaf에 대해 Similarity Score 계산
		2-2. Gain 계산 및 가장 큰 값으로 분기

[**XGBoost 실행 과정 예제**]()

### Pruming (가지치기)
- Depth가 깊어질 수록 Training Data에 집중적으로 Fitting됨 -> Over Fitting 발생

>**Overfitting을 방지하기 위해 depth가 더 이상 깊어지지 않도록 가지치기를 실행** 

#### 가지치기 방법
1) $\lambda$값의 크기 조절
	$\lambda$값이 커질수록 Gain이 빠르게 작아짐
2) Gain에 가지치기 기준 $\gamma$값 적용
	Gain이 $\gamma$값보다 작을 경우 분기를 실행하지 않음
