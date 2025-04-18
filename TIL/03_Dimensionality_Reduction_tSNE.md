# Dimensionality Reduction 02: t-SNE

### [t-SNE 실습](https://github.com/Do-heewan/Big_Data_Analysis/blob/main/03_tSNE/TSNE.ipynb)

<br>

**시각화?**
- 눈으로 보이게 하는 기법

### PCA 기반 차원 축소의 한계점
- 공분산을 기반으로 함
- 분산은 선형성을 기초로 함
- 비선형 데이터에서 올바르게 동작하기 어렵다.

>거리값을 기반으로 함 -> TSNE의 기초, 대신 정보량은 무시 <br>
>해석 관점에서는 별로일 수 있으나, 시각화 관점에서는 좋음

<br>

# t-SNE, T-distribute Stochastic Neighbor Embedding 
### t-SNE란?
- 높은 차원의 복잡한 데이터를 저차원으로 차원 축소하는 기법
- 비선형 데이터에 대해서도 잘 동작
- 오직 데이터 시각화가 목적

### 핵심 아이디어
- 고차원에서 특정 데이터와 가까운 데이터는 저차원에서도 가까울 것이며, 멀리 떨어진 데이터는 저차원에서도 멀리 떨어져 있을 것이다.

<br>

	- 가깝다/멀다 -> 이웃하다 (Neighbor Embedding)
	- 어떻게 판단? -> 확률적 (Stochastic)
	- 어떤 확률 분포? -> T분포

### 동작 아이디어

1. 고차원 데이터에서 유사점 찾기
2. 저차원 공간에서 유사한 점 배치하기
3. 두 확률 분포(P, Q) 차이를 줄이기 (KL Divergence 최소화)
4. 최적화가 완료되면 데이터 구조를 시각화

<br>

## 1. Stochastic Neighbor Embedding
- **Probability `P`** : 고차원 데이터에서 유사도 확률 분포
- **Perplexity** : 하나의 데이터 포인트가 평균적으로 몇 개의 이웃을 갖도록 할 것인가를 결정하는 값

### Perplexity와 표준편차 조정
	1) 초기값 설정
		- 표준편차의 초기값 (보통 1) 설정
		- Perplexity의 값을 설정, 조건부 확률의 엔트로피가 Perplexity와 맞아야 함

	2) 조건부 확률 계산

	3) 이진 탐색을 통한 표준편차 조정
		- 확률 P에 대한 엔트로피와 Perplexity의 이진 값 비교

### SNE의 목표
- 고차원에서의 데이터 분포와 저차원에서의 데이터 분포를 같게 만드는 것
>같게 하는 법 : Gradient Descent 기반 학습

### SNE에서 비용 함수

**Kullback-Leibler Divergence (KL Divergence)**
- 고차원 공간과 저차원 공간ㅇ의 두 확률 분포 P와 Q가 얼마나 비슷한지 측정하는 지표

#### $Cost = \sum D_{KL}(P_i|Q_i)=\sum_i \sum_j p_{\frac{j}{i}}log\frac{p{\frac{j}{i}}}{q\frac{j}{i}}$

<br>

## 2. T-distribute Stochastic Neighbor Embedding

### SNE의 문제점
	1) KL Divergence의 비대칭 문제
	2) 가우시안 확률분포를 가정하여 발생하는 문제

>이 두가지 문제를 해결한 것이 TSNE이다.

<br>

### KL Divergence의 비대칭 문제 해결법
	KL Divergence는 대칭적이지 않아서 다음과 같은 문제가 발생할 수 있음
	- P가 높고 Q가 낮을 때에는 Cost가 높지만, P가 낮고 Q가 높을 때에는 Cost가 낮음

*이 문제를 해결하기 위해 목적함수를 재설정*