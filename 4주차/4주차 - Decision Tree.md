### Appendix : 로그(Log)

**Log의 정의**
- 어떤 수를 몇 번 곱해야 목표 수가 되는가를 묻는 연산
- 컴퓨터과학에서 매우 자주 등장하는 개념, $log_2$를 사용

**$Log_2$**
- 정보를 세는 기초 단위
- 어떤 정보를 처리할 때 몇 비트가 필요한지를 묻는 연산

>$log_28$ : 2를 3번 곱하면 8 -> $2^3$ 이 된다. <br>
  8을 표현하기 위해선 $2^3$의 자리수 까지 필요. <br>
  => 1000이 된다.

---

<br>

### Appendix : 정보량(Information)

**정보량의 정의**
- 어떤 사건이 발생했을 때, 그 사건이 주는 **'놀라움' 또는 정보의 양**을 **수치로 표현**한 것

**수학적 정의**

### $I(x) = -log_2P(x)$

>$P(x)$: 사건 x가 발생할 확률 <br>
>$I(x)$: 사건 x가 발생하였을 때 그 사건이 주는 정보의 양

**특징**
- 확률이 낮은 사건일 수록 더 많은 정보가 필요

![로그특징](https://github.com/user-attachments/assets/6fb3e2fa-d0d0-4cf6-ac7e-ec8ed09e90d6)

---

<br>

### Appendix : 엔트로피(Entropy)
**엔트로피의 정의**
- 어떤 확률 분포의 평균 정보량 또는 무작위성(불확실성)의 정도를 나타내는 정도
- 예측이 얼마나 어려운가를 수치로 표현한 값

**수학적 정의**

### $H(x) = E[I(x)] = - \sum P(x_i)log_2P(x_i)$

>$P(x_i)$ : 사건 $x_i$가 발생할 확률 <br>
>$H(x)$ : 확률변수 x의 엔트로피

**특징**
- 확률이 고르게 분포될 수록 엔트로피가 높음 -> 불확실성이 큼
- 확률이 한쪽에 치우칠수록 엔트로피가 낮음 -> 예측이 쉬움

![엔트로피특징](https://github.com/user-attachments/assets/512ced2c-9d6c-4f1c-8dd8-8cc9697b2810)

---

<br>

### Appendix : 엔트로피와 불순도(Impurity)
**불순도란?**
- 불순물이 포함된 정도, 데이터의 혼잡도를 나타내는 지표
- 특정 지표를 기준으로 데이터 셋을 나누었을 때 데이터의 불순 정도가 줄어 들 수록 좋은 질문임

**의사결정 나무와 불순도**
- 의사 결정 나무는 질문을 통해 데이터의 불순도를 낮추는 방향으로 분기하는 모델

![불순도](https://github.com/user-attachments/assets/204a2645-a848-4c0c-8a79-0f77648e0330)

---

<br>

### Appendix : 정보이득(Information Gain)
**정보이득의 정의**
- 의사결정나무에서 사용하는 용어로 어떤 속성을 기준으로 데이터를 분할할 때, 얼마나 불확실성이 줄어드는지 수치로 나타낸 값
- 즉, 분할을 통해 얼마만큼 정보를 얻었는가를 계산하는 것

**수학적 정의**
### $Information \ Gain = H(부모) - H(자식)$

![정보이득](https://github.com/user-attachments/assets/f15e9b91-a30a-4d55-8aca-8cc0dea937aa)

---

<br>
<br>

# 의사 결정 트리
### 의사 결정 트리?
- 기계학습에서 사용되는 지도 학습 알고리즘
- 데이터의 특징과 레이블 간의 관계를 **트리 구조로 표현**하는 모델
- 과정은 스무고개와 비슷함

### 의사 결정 트리의 목적
- 데이터의 특징과 레이블 간의 관계를 학습하고 이를 기반으로 예측 및 분류를 수행하는 것.
### 과정
	1. 예측 및 분류
		- 주어진 입력 값에 대해 예측 값을 생성하고 분류를 수행
	2. 특징의 중요도 파악
		- 트리의 규칙은 if-else 형태로 표현
	3. 과적합 방지
		- 가지치기 기법

### 예시
![의사결정트리](https://github.com/user-attachments/assets/e461440a-7074-496c-b981-b3ac9a838838)

---

<br>

# Dicision Tree - ID3 (Iterative Dichotomiser 3)

### 결정 트리의 궁극적인 목표
- 여러 Decision Tree중 어떤 모델이 좋은지 결정하려는 것
	- 변별력이 좋은 질문을 먼저 던지는 것

### 동작 순서
![ID3동작순서](https://github.com/user-attachments/assets/583b55f7-45c0-433d-9699-6e699757a68a)

### [Dicision Tree 예제]()

---

<br>

# Decision Tree - C4.5

### ID3의 모델의 문제점
- Entropy는 특징 선택에 중요한 지표이만 몇가지 문제점이 있음

|문제점|설명|
|-----|----|
|연속된 변수 처리 문제|ID3 모델은 범주형 변수에 적합|
|다중 속성에 편향됨|속성의 값이 많을수록 정보이득이 유리함|
|다중 클래스 분리가 어려움|클래스 수가 많아질수록 정보이득 차이가 작아지고 불안정한 분할이 발생하기 쉬움|
|이상치에 민감|작은 노이즈도 분리 기준으로 삼아 트리가 복잡해짐|

<br>

## C4.5 알고리즘
- C4.5 알고리즘은 의사결정 트리 학습의 개선된 버전, C로 구현이 되었다.

### 핵심아이디어 1) Information Gain Ratio
- Information Gain Ratio의 단점 중 하나인 분할 수에 따른 정보이득의 편향을 보완하기 위해 개발한 방법
- Information Gain Ratio는 특징 분할 후의 엔트로피 감소를 특징의 분할 정도로 나눈 값으로 계산

### $Information \ Gain \ Ratio = \frac{IG}{IV} = \frac{Information \ Gain}{Intrinsic \ Value} = - \frac{\displaystyle\sum_{j=1}^{C} p_j log p_j}{\displaystyle\sum_{i=1}^{N} p_i log p_i}$

<br>

**Instrinsic Value**
- 특정 지표로 분기했을 때 생성되는 가지의 수에 대한 엔트로피 값

### $Instrinsic Value(IV) = -\displaystyle\sum_{i=1}^{N}P_jlogp_i$

<br>

**Information Gain과 Information Gain Ratio 비교**

![비교](https://github.com/user-attachments/assets/886da8e4-e23e-401b-b67f-429a16c4149a)

<br>

### 핵심아이디어 2) 수치형 변수 처리
- C4.5 알고리즘은 수치형 변수를 입력할 수 있음
	- Threshold를 지정하면 수치형 변수도 범주형 변수처럼 사용 가능

![수치형변수](https://github.com/user-attachments/assets/df41150f-bcf2-4e87-81c9-205daa542552)

**수치형 속성의 분할 원리**
- 임계값을 기준으로 이진 분할
- 분할 기준은 정보이득 또는 정보이득비율 최대화 지점

**수치형 속성 분할 과정**
1) 수치형 속성의 값을 오름차순 정렬
2) 수치형 변수 나누는 기준에 따라 분할 후보 설정
3) 각 임계값에 대해 데이터를 이진 분할
4) 각 분할의 정보이득 계산
5) 정보이득이 가장 큰 임계값을 선택

**수치형 변수 사용 시 데이터 구간을 나누는 방법**
1) 값이 바뀌는 모든 지점을 임계값 후보로 설정
2) Output 클래스가 바뀔 때 임계값 후보로 설정
3) Q1, Median, Q3 값을 임계값 후보로 설정

![데이터구간](https://github.com/user-attachments/assets/e8cbb5e2-355e-4f40-9351-29a28ac9a0d3)

<br>

### 3) 결측치 처리
- C4.5 알고리즘은 결측치 처리에도 유연한 방법을 제공함
- 다음과 같은 처리 방법을 사용
	1. Entropy 계산 시 non-missing value로만 계산
	2. 결측치가 있는 샘플의 가중치 계산 및 적용
	3. Intrinsic Value 계산 시 Missing Value를 하나의 클래스로 보고 계산
