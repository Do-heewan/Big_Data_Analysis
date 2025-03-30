### 노이즈 제거

#### 노이즈
- 노이즈란 실제 입력되지 않은 신호
- 실제 입력되지 않았지만, 입력 되었다고 잘못 판단한 값
- 화이트 노이즈, 통계적 노이즈
#### 노이즈 처리방법
- Moving Average Filter : 이동하면서 주위 값들에 비해 너무 높거나 낮을 경우 평균값으로 대체
- Median Filter : 일정 범위의 중간값으로 지정
- Bandpass Filter : 주파수 기반의 필터
#### Smooth Filter
- 특정 윈도우 영역 내에 포함되는 값들의 평균으로 필터링
- **스무딩 선형 필터, 평균 필터, 저역통과** 필터라고 부름
- 주어진 영역에 무의미한 디테일들을 축소시키는데 사용
- 필터의 크기가 커질수록 블러링 효과가 커짐

<br>
<br>

# Dimensionality Reduction 01: PCA
#### 차원의 저주
- 차원이 증가하면서 문제 공간이 지수적으로 커지는 현상
	- 차원이 커질수록 공간은 많이 필요하면서, 사용할 수 있는 정보량은 상대적으로 작아지는 현상
#### 차원 축소
- 고차원의 데이터를 저차원의 데이터로 변환하는 방법
#### 차원 축소를 하는 이유
- 비용, 시간, 자원, 용량 문제 해결
- 과적합 문제 해결
- 설명력 증가
#### 차원 축소의 단점
- 정보의 손실
#### 알고리즘
- **주성분 분석(PCA)**
- LDA
- LLE
- MDS
- Isomap
- **t-SNE**

<br>
<br>

# PCA를 배우기전에 알아야 할 개념
**1. 정사영 / 투영(projection)** <br>
**2. 차원축소와 분산** <br>
**3. 공분산**

### 1. 정사영/투영
3차원 -> 2차원 투영 (약간의 정보 손실)
3차원 -> 1차원 (기저(basis) or 초평면(hyperplane))

<br>

### 2. 차원축소와 분산
- 분산의 정의 : 데이터가 (평균으로 부터) 퍼져있는 정도
- 정보이론적 관점 : 정보량을 의미

**엔트로피(Entropy)**
- 정의 : 물질이 분산되는 정도 / 분포가 가지는 정보의 확신도 (=정보량)

**차원축소와 분산**
- 두 개 이상의 feature를 합쳐 하나로 만들 때 **데이터의 분산을 유지하면 데이터의 특성을 유지할 수 있다.**
- 고차원의 분산과 저차원의 분산이 같다면, 두 데이터는 같은 데이터다.
	- 데이터 간의 분산을 최대로 한다면 정보의 손실을 최소화 할 수 있다.

<br>

### 3. 공분산
- 정의 : 2개의 확률변수의 **선형관계/상관정도(correlation)** 을 나타내는 값 <br>
증, 증 -> True (증가) <br>
증, 감 -> False (감소) <br>
감, 증 -> False <br>
감, 감 -> True <br>

**공분산 법칙**

![공분산 법칙](https://private-user-images.githubusercontent.com/139729135/428409284-51724301-da9d-4ff4-82bf-a1e0eae5499b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDMzNTA4NzAsIm5iZiI6MTc0MzM1MDU3MCwicGF0aCI6Ii8xMzk3MjkxMzUvNDI4NDA5Mjg0LTUxNzI0MzAxLWRhOWQtNGZmNC04MmJmLWExZTBlYWU1NDk5Yi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMzMFQxNjAyNTBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jNmUxN2VjZDQxZjI1YWFhMWJhYjlhYzJlZDllZmU3NjI3ZDczYzRmZTAyYWI3NmM2MzQ4MmMyZWM2OTdkZTI0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.YClUAacRTxVSbxD7P3AexfwcZ6B_aLNfqboCo0jjeAg)

<br>
<br>

## 주성분 분석 개요
- 분산이 가장 큰 방향으로 첫 번째 축을 생성하여 사영
- 첫 번째 축에 직각이 되는 벡터를 두 번째 축으로 하여 사영 (두번째 feature)
- 두 번째 축에 직각이 되는 벡터를 세 번째 축으로 하여 사영 (세번째 feature)
#### 목적
- 고차원의 데이터를 분산이 최대로 보존되는 저차원의 축 평면으로 투영하여 차원 축소
#### 해결하고자 한 것
- 분산이 최대로 보존되는 축을 어떻게 찾을 것인가
#### 방법
- 입력 데이터들의 공분산 행렬에 대한 고유벡터, 고유값을 구하고 그 값으로 선형 변환(투영)을 취한다.

## 고유값과 고유벡터

#### 정의 
어떤 행렬 A에 대하여 상수 `lambda`와 벡터 `x`가 다음 식을 만족한다면,
![고유벡터](https://private-user-images.githubusercontent.com/139729135/428409283-2a19c067-0142-4607-a092-843eada03b2c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDMzNTA4NzAsIm5iZiI6MTc0MzM1MDU3MCwicGF0aCI6Ii8xMzk3MjkxMzUvNDI4NDA5MjgzLTJhMTljMDY3LTAxNDItNDYwNy1hMDkyLTg0M2VhZGEwM2IyYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMzMFQxNjAyNTBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02ZjYwZTZiMmE2ZmFkZGQ5M2UxNzA3ZDc3NmQ5MmE0ZjdhMzU3ZTI4Y2QzYmQxMjU1MTc1MTRkM2Q0ZjlkNTc5JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.2DKyc1d679j72UnVP57xdZaBz2RTGgzik39Fgf4sEcA) <br>
이때 `lambda`와 `x`를 각각 행렬 A의 고유값 및 고유벡터라고 한다.

#### 선형 변환의 결과가 다음과 같다면
![선형변화](https://private-user-images.githubusercontent.com/139729135/428409285-fcb028e2-4f73-41ec-abaa-8c0942fc18ea.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDMzNTA4NzAsIm5iZiI6MTc0MzM1MDU3MCwicGF0aCI6Ii8xMzk3MjkxMzUvNDI4NDA5Mjg1LWZjYjAyOGUyLTRmNzMtNDFlYy1hYmFhLThjMDk0MmZjMThlYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMzMFQxNjAyNTBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02YjA5OTk4M2Q5ZGFlMTRjOWQ2NTJjNzBkOGFmOTc5NmU2MDVjZmY3YzRmNzQzZGRhZTNiMWJhOTA4YzdiODgzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Clw5vhcLcnhFkzn4kYEmADMDycCW5IPBLurkwCjbTWQ)

- 벡터의 방향은 유지, 크기만 변경
- 고유벡터는 선형 변환을 할 때 어떤 방향으로 얼마나 힘이 가해지는지를 표현
- *어떤 방향으로 분산이 커지는지를 구하는 것*

#### 고유 벡터(x)
- 행렬이 벡터의 변화에 작용하는 주축의 방향을 나타냄
- 공분산 행렬의 고유벡터는 데이터가 어떤 방향으로 분산되어 있는지 나타냄

#### 고유 값
- 고유벡터 방향으로 얼마 만큼의 크기로 벡터공간이 늘려지는지를 나타냄
- 고유값은 여러 해가 존재할 수 있으며, 값이 큰 순서대로 고유 벡터를 정렬하면 결과적으로 중요한 순서대로 주성분을 구할 수 있음

<br>
<br>

<!--
# PCA 개요
#### PCA란?
- 고차원 데이터를 저차원으로 변환하는 차원 축소 기법
- 데이터의 분산을 최대한 보존하는 방향으로 새로운 축(주성분)을 생성
- 데이터의 시각화 및 노이즈 제거
-->