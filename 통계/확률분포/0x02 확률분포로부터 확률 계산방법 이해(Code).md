## 정규분포의 확률계산
- A/S 작업을 수행하는데 걸리는 시간을 측정해 본 결과 평균 115분, 표준편차 20분이 소요된다.
- 만일 A/S 작업시간의 허용 범위가 135분 이내라면, 135분 이상 걸리는 A/S 작업 비율은 얼마일까?
```
# 누적활률 값 계산
mu = 115
sigma = 20
x = 135
prob = stats.norm.cdf(x, mu, sigma)
print("{0}분 이상 걸리는 A/S 작업 비율 : {1:.1f}%".format(x, 1 - prob) * 100)

=> 135분 이상 걸리는 A/S 작업 비율 : 15.9%
```

- 어떤 자동차 1리터당 주행거리가 평균 12km, 표준편차 3km인 정규분포를 이룬다.
- 1리터를 가지고 12km 이상 15km이하를 달릴 확률은 얼마일까?
```
# 누적확률 값 계산
mu = 12
sigma = 3
x1 = 15

# prob1 : 누적확률 15이하 값 계산
prob1 = stats.norm.cdf(x1, mu, sigma)
print("{0}km 이상 {1}km 이하를 달릴 확률은 {2:.1f}% 에 해당함".format(mu, x1, (prob1 - 0.5) * 100))

=> 12km 이상 15km이하를 달릴 확률은 34.1%에 해당함
```

## t-분포
- 확률변수 t는 자유도가 5인 t-분포를 따른다.
- t 값이 1.53일 때, P(T ≤ t)을 계산하면?
```
t = 1.53
df = 5

# 누적확률 값 계산
prob = stats.t.cdf(t, df)
print("P(T ≤ F): {:.3f}".format(prob))

=> P(T ≤ F) : 0.907
```

## 카이제곱(χ^2) 분포
- χ^2 분포(자유도 변화에 따른 분포 변화 확인)
- Random Data 생성: n = 1,000 , degree of freedom = 10
```
# seed 선택을 하여 매번 실행 시 동일한 값이 나오도록 설정
np.random.seed(seed = 1234)

# 자유로: 10, 데이터 수: 1000개의 χ^2 분포를 따르는 데이터 생성
chisq_df10 = np.randeom.chisquare(df = 10, size = 1000)

# histogram, fit: 정규분포 선 생성, kde: χ^2 분포의 kde 생성 안함
sns.distplot(chisq_df10, fit = stats.norm, ked = False)
```
- Random Data 생성: n = 1,000 , degree of freedom = 40
```
# seed 선택을 하여 매번 실행 시 동일한 값이 나오도록 설정
np.random.seed(seed = 1234)

# 자유로: 40, 데이터 수: 1000개의 χ^2 분포를 따르는 데이터 생성
chisq_df40 = np.randeom.chisquare(df = 40, size = 1000)

# histogram, fit: 정규분포 선 생성, kde: χ^2 분포의 kde 생성 안함
sns.distplot(chisq_df40, fit = stats.norm, ked = False)
```
- 확률변수 χ^2 는 자유도가 30인 χ^2-분포를 따른다.
- χ^2 값이 10일 때, P(X ≤ χ^2)을 계산하면?
```
chisq = 10
df = 30

# 누적확률 값 계산
prob = stats.chi2.cdf(chisq, df)
print("P(X ≤ {0}) : {1:4f}".format(chisq, prop))

=> P(X ≤ 10) : 0.0002
```

## F-분포
- 확률변수 F는 각각 자유도가 15, 15인 F-분포를 따른다.
- F 값이 2.0일 때 P(X ≤ F)을 계산하면?
```
f = 2.0
dfnum = 15
dfden = 15

# 누적확률 값 계산
prob = stats.f.cdf(x = f, dfn = dfnum, dfd = dfden)
print("P(X ≤ F): {:.3f}".format(prob))

=> P(X ≤ F) : 0.904
```

## 와이블(Weibull) 분포
- 어떤 제품의 수명시간 x가 형상모수 2.2, 척도모수 1,200인 와이블 분포를 따른다고 할 때, 이 제품이 적어도 1,500시간 이상 작동할 확를을 구하면?
```
x = 1500
alpha = 2.2
beta = 1200

# 누적확률 값 계산
prob = stats.weibull_min.cdf(x, alpha, scale = beta)
print("P(X ≤ x): {:.3f}".formal(1 - prob))
```

## 이항분포
- 도장공정에서 광택도 불량이 40% 정도 된다고 한다.
- 3대의 차량을 임의로 선택했을 때 불량대수가 0, 1, 2, 3대 각각의 나올 확를은?
```
# n의 수
n = 3
for i in range(n + 1):
  # 이항분포 Probability Mass Function
  prob = stats.binom.pmf(k = i, n = n, p = 0.4)
  print("P(X = {0}) = {1:.3f}".format(i, prob))

=> P(X=0) : 0.216
=> P(X=1) : 0.432
=> P(X=2) : 0.288
=> P(X=3) : 0.064
```

## 포아송 분포
- 어느 전화 교환대에는 1분당 평균 2회의 전화가 걸려오고 있다. 전화의 도착 횟수가 포아송 분포를 따른다면,
  - 이 교환대에 1분당 3번의 전화가 거려올 확를은?
  - 이 교환대에 1분당 최대 2회 이하의 전화가 걸려올 확를은?
```
# 평균
mu = 2

# 1분당 3번의 전화가 걸려올 확률
prob = stats.poisson.pmf(3, mu)

# 1분당 최대 2회 이하의 전화가 걸려올 확률
cdf_prob = stats.poisson.cdf(2, mu)
print("1분당 {0}번의 전화가 걸려올 확률: {1:.1f}".format(3, prob * 100))
print("1분당 최대 {0}회 이하의 전화가 걸려올 확률: {1:.1f}".format(2, cdf_prob * 100))

=> 1분당 3번의 전화가 걸려올 확률 : 18.0%
=> 1분당 최대 2회 이하의 전화가 걸려올 확률 : 67.7%
```