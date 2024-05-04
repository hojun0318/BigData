# Python 패키지
```
- numpy       : 행렬 연산 패키지
- scipy       : 과학, 기술 계산 패키지
- scipy.stats : 통계 분석 패키지
- pandas      : 데이터 구성 패키지
- matplotlib  : 데이터 시각화 패키지
- seaborn     : 데이터 시각화 패키지
- statsmodels : 통계 분석 패키지
```

```
import numpy as np
from scipy import stats
import scipy.stats
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
from statsmodels.stats.proportion import proportions_ztest
```

## 자동차 연비 데이터 셋에서 기술통계치 구하기 (Data.Set mycars.csv)
- 시내에서 연비(mpg) 통계치 구하기 : 데이터 수, 평균, 중앙값, 표준편차, min, max, Q1, Q3
- 자동차 모델별, mpg 기술통계치 구하기 : 데이터 수, 평균, 중앙값, 표준편차, min, max, Q1, Q3
```
# mycars 데이터 가져오기(데이터 경로 확인: mycars.csv)

-> ds_mycars = pd.read_csv("D:/Work/Data/mycars.csv", engine = "python")
-> ds_mycars.head()
```
```
# 자동차 모델별, mpg 데이터 subset
-> df = ds_mycars[['model', 'mpg']]

# 모델 별 데이터 수 평균 표준편차
-> df.groupby('model').describe()
```

## 제품의 품질을 조사하여, Cabbage 결함과 결함이 발생한 기간을 조사한 Table이다. 범주형 데이터에 대해 counts, percents, cumulative counts, cumulative percents 계산하기 (Data.set Exh_QC1.csv)
```
# Exh_QC1 데이터 가져오기
-> ds_Exh_QC1 = pd.read_csv("D://Work/Data/Exh_QC1.csv", engine = "python")
-> df = ds_Exh_QC1[['Flaws', 'Period']]

# Flaws 변수 Count: value_count, 순서대로 정렬: sort_index
-> count = df['Flaws'].value_counts().sort_index()

# CumCnt 계산: cumsum
-> cumcnt = np.cumsum(count)

# Percent 계산: 직접
-> percent = count / sum(count) * 100

# CumPct 계산: cumsum
-> cumpct = np.cumsum(percent)

# DataFrame으로 취합
-> count_data = pd.DataFrame({'Count': count, 'CumCnt': cumcnt, 'Percent': percent, 'CumPct': cumpct})

# Column의 name(좌측상단 이름) 생성
-> count_data.columns.name = 'Flaws'

# 결과 확인
-> count_data



# Period변수 Count: value_count, 순서대로 정렬: sort_index
-> count2 = df['Period'].value_counts().sort_index()

# CumCnt 계산: cumcnt
-> cumcnt2 = np.cumsum(count2)

# Percent 계산: 직접
-> percent2 = count2 / sum(count2) * 100

# CumPct 계산: cumsum
-> cumpct2 = np.cumsum(percent2)

# DataFrame으로 취합
-> count_data2 = pd.DataFrame({'Count': count2, 'CumCnt': cumcnt2, 'Percent': percent2, 'CumPct': cumpct2})

# Column의 name(좌측상단 이름) 생성
-> count_data2.columns.name = 'Period'

# 결과확인
-> count_data2
```