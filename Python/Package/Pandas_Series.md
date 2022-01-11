

# pandas

- Python Data Analysis Library
- 데이터 분석 및 가공을 위한 파이썬 라이브러리
- Series, DataFrame 등의 자료구조를 활용
- R의 데이터프레임을 모방
- 데이터를 수정하고 목적에 맞게 변경하기 위해 사용
- 데이터프레임은 엑셀과 유사
- Numpy를 사용하고 있어 계산이 빠름
- 라이브러리 구성
  - 여러종류의 클래스와 다양한 함수로 구성
  - 시리즈와 데이터 프레임의 자료 구조 제공
  - 시리즈(1차원 배열), 데이터프레임(2차원 배열)





## pandas 데이터구조

- 시리즈 데이터(1차원)

- 데이터 프레임(2차원)

https://www.kdnuggets.com/2017/01/pandas-cheat-sheet.html

### Series

- pandas 기본 객체 중하나
- numpy의 ndarray를 기반으로 인덱싱 기능을 추가해 1차원 배열을 나타냄
- index를 지정하지 않을 시, 기본적으로 ndarray와 같이 0-based 인덱스 생성, 지정할 경우 명시적으로 지정된 index를 사용
- 같은 타입의 0개 이상의 데이터를 가질 수 있음



1. 자료구조: 시리즈
   - 데이터가 순차적으로 나열된 1차원 배열 형태
   - 인덱스와 테이터 값이 일대일로 대응
   - 딕셔너리와 비슷한 구조: {key(index):value}

2. 시리즈의 인덱스
   - 데이터 값의 위치를 나타내는 이름표 역할

3. 시리즈 생성: 판다스 내장함수인 Series()이용
   - 리스트로 시리즈 만들기
   - 딕셔너리로 시리즈 만들기
   - 튜플로 시리즈 만들기



```python
import pandas as pd
import numpy as np
```




```python
s1 = pd.Series([10,20,30,40,50])
s2
```


    0    10
    1    20
    2    30
    3    40
    4    50
    dtype: int64




```python
s2 = pd.Series(['A','B','C'])
s2
```


    0    A
    1    B
    2    C
    dtype: object




```python
s2 = pd.Series('A B C'.split())
s2
```


    0    A
    1    B
    2    C
    dtype: object




```python
s3 = pd.Series(range(10,14))
s3
```


    0    10
    1    11
    2    12
    3    13
    dtype: int64




```python
s = pd.Series(np.arange(200))
s
```


    0        0
    1        1
    2        2
    3        3
    4        4
          ... 
    195    195
    196    196
    197    197
    198    198
    199    199
    Length: 200, dtype: int32




```python
s = pd.Series([1,2,3,np.nan,6.8])
s
```


    0    1.0
    1    2.0
    2    3.0
    3    NaN
    4    6.8
    dtype: float64




```python
# 숫자 인덱스 지정
s1 = pd.Series([10,20,30], index=[1,2,3])
s1
```


    1    10
    2    20
    3    30
    dtype: int64




```python
# 문자 인덱스 지정
s2 = pd.Series([95,100,88], index=['홍길동', '유관순', '김유신'])
s2
```


    홍길동     95
    유관순    100
    김유신     88
    dtype: int64




```python
# 시리즈.index
s1.index
```


    Int64Index([1, 2, 3], dtype='int64')




```python
s2.index
```


    Index(['김순복', '김초향', '김진춘'], dtype='object')




```python
s= pd.Series([9904312, 3448737, 289045, 2466052],
             index=["서울","부산","인천","대구"])
s.index
```


    Index(['서울', '부산', '인천', '대구'], dtype='object')




```python
# index도 마치 객체처럼
s.index.name = '도시'
s
```


    도시
    서울    9904312
    부산    3448737
    인천     289045
    대구    2466052
    dtype: int64




```python
# 시리즈 값
s.values
```


    array([9904312, 3448737,  289045, 2466052], dtype=int64)




```python
print(s.name)
```

    None




```python
s.name = '인구수'
s
```


    도시
    서울    9904312
    부산    3448737
    인천     289045
    대구    2466052
    Name: 인구수, dtype: int64




```python
# 정수형 인덱스 접근
print(s.index)
s[0]
```

    Index(['서울', '부산', '인천', '대구'], dtype='object')
    
    9904312




```python
# 문자형 인덱스 접근
s['서울']
```


    9904312




```python
# 한 줄에 위치 인덱스와 문자인덱스를 동시에 접근
s[2], s['인천']
```


    (289045, 289045)




```python
s
```


    서울    9904312
    부산    3448737
    인천     289045
    대구    2466052
    dtype: int64




```python
## 여러 개 접근시 리스트로
s[[1,3]]
```


    부산    3448737
    대구    2466052
    dtype: int64


```python
s[['서울','대구']]
```


    도시
    서울    9904312
    대구    2466052
    Name: 인구수, dtype: int64




```python
# 인덱스를 문자값으로 지정한 시리즈
s.서울
```


    9904312




```python
s1 = pd.Series(range(3), index=['a','b','c'])
s1
```


    a    0
    b    1
    c    2
    dtype: int64


```python
s1.a
```


    0




```python
s
```


    도시
    서울    9904312
    부산    3448737
    인천     289045
    대구    2466052
    Name: 인구수, dtype: int64




```python
s[1:3]
```


    도시
    부산    3448737
    인천     289045
    Name: 인구수, dtype: int64




```python
# 문자 인덱스를 이용한 슬라이싱은 표시된 라벨까지 다 가져온다
s['부산':'대구']
```


    도시
    부산    3448737
    인천     289045
    대구    2466052
    Name: 인구수, dtype: int64




```python
# '서울' 데이터 변경
s['서울'] = 10000000  # s.서울 = 10000000, s[0] = 1000000
s
```


    서울    10000000
    부산     3448737
    인천      289045
    대구     2466052
    dtype: int64




```python
pd.Series([1,2,3]) + 4
```


    0    5
    1    6
    2    7
    dtype: int64




```python
s/1000000
```


    도시
    서울    10.000000
    부산     3.448737
    인천     0.289045
    대구     2.466052
    Name: 인구수, dtype: float64




```python
s
```


    서울    10000000
    부산     3448737
    인천      289045
    대구     2466052
    dtype: int64




```python
s[(s > 2500000) & (s < 5000000)]
# s[(s > 25e5) & (s < 50e5)]   숫자 0이 너무 많을 때
```


    부산    3448737
    dtype: int64




```python
s0 = pd.Series(np.arange(10), np.arange(10)+1)
s0
```


    1     0
    2     1
    3     2
    4     3
    5     4
    6     5
    7     6
    8     7
    9     8
    10    9
    dtype: int32




```python
s0 > 5
```


    1     False
    2     False
    3     False
    4     False
    5     False
    6     False
    7      True
    8      True
    9      True
    10     True
    dtype: bool




```python
s0[(s0 % 2 == 0)&(s0 != 0)]
```


    3    2
    5    4
    7    6
    9    8
    dtype: int32




```python
# 인덱스가 5보다 큰가?
s0.index > 5
```


    array([False, False, False, False, False,  True,  True,  True,  True,
            True])




```python
# 값이 5보다 크고 8보다 작은 요소 추출
s0[(5 < s0) & (s0 < 8)]
```


    7    6
    8    7
    dtype: int32




```python
# 값이 7이상인 수들의 합 구하기
s0[s0 >= 7].sum()
```


    24




```python
# 값이 7이상인 수들의 갯수를 더한 값. True의 갯수
(s0 >= 7).sum()
```


    3




```python
num_s1 = pd.Series([1,2,3,4], index=['a','b','c','d'])
num_s1
```


    a    1
    b    2
    c    3
    d    4
    dtype: int64




```python
num_s2 = pd.Series([5,6,7,8], index=['b','c','d','a'])
num_s2
```


    b    5
    c    6
    d    7
    a    8
    dtype: int64




```python
num_s1 + num_s2
```


    a     9
    b     7
    c     9
    d    11
    dtype: int64




```python
num_s3 = pd.Series([5,6,7,8], index=['e','b','f','g'])
num_s4 = pd.Series([1,2,3,4], index=['a','b','c','d'])
num_s3, num_s4
```


    (e    5
     b    6
     f    7
     g    8
     dtype: int64,
     a    1
     b    2
     c    3
     d    4
     dtype: int64)




```python
num_s3 + num_s4
```


    a    NaN
    b    8.0
    c    NaN
    d    NaN
    e    NaN
    f    NaN
    g    NaN
    dtype: float64




```python
num_s3 - num_s4
```


    a    NaN
    b    4.0
    c    NaN
    d    NaN
    e    NaN
    f    NaN
    g    NaN
    dtype: float64




```python
# 두 시리즈 values간의 연산(인덱스와 무관하게 연산하고 싶을 때)
num_s3.values - num_s4.values 
```


    array([4, 4, 4, 4], dtype=int64)




```python
s
```


    도시
    서울    10000000
    부산     3448737
    인천      289045
    대구     2466052
    Name: 인구수, dtype: int64




```python
'서울' in s
```


    True




```python
'대전' in s
```


    False




```python
'대전' not in s
```


    True




```python
# 딕셔너리 item()과 같은 함수가 시리즈에도 있음
list(s.items())   # zip 객체
```


    [('서울', 10000000), ('부산', 3448737), ('인천', 289045), ('대구', 2466052)]




```python
for k, v in s.items():
    print(f'{k}={v}')
```

    서울=10000000
    부산=3448737
    인천=289045
    대구=2466052




```python
# 딕셔너리 키가 인덱스가 됨. 별도로 인덱스 안만들려면 딕셔너리를 쓰면 됨
scores = {'홍길동':96, '이몽룡':100, '성춘향':88}
s = pd.Series(scores)
s
```


    홍길동     96
    이몽룡    100
    성춘향     88
    dtype: int64




```python
s = pd.Series(scores, index=['이몽룡', '홍길동', '성춘향'])
s
```


    이몽룡    100
    홍길동     96
    성춘향     88
    dtype: int64




```python
s= pd.Series([9904312, 3448737, 289045, 2466052],
             index=["서울","부산","인천","대구"])
s
```


    서울    9904312
    부산    3448737
    인천     289045
    대구    2466052
    dtype: int64




```python
s.서울 = 10000000
s
```


    서울    10000000
    부산     3448737
    인천      289045
    대구     2466052
    dtype: int64




```python
# 데이터를 삭제할 때도 딕셔너리처럼 del 명령을 사용
# del s['부산']
```




```python
s1 = pd.Series([1, 1, 3, 1, 2, 2, 2, 1, 1, 3, 3, 4, 5, 5, 7, np.NaN])
s1
```


    0     1.0
    1     1.0
    2     3.0
    3     1.0
    4     2.0
    5     2.0
    6     2.0
    7     1.0
    8     1.0
    9     3.0
    10    3.0
    11    4.0
    12    5.0
    13    5.0
    14    7.0
    15    NaN
    dtype: float64




```python
# 시리즈 원소 개수 반환
s1.size
```


    16




```python
# 시리즈 원소 개수 반환
len(s1)
```


    16




```python
# 결과가 튜플형태로 (차원,)
s1.shape
```


    (16,)




```python
# 유일한 값만 ndarray로 반환
s1.unique()
```


    array([ 1.,  3.,  2.,  4.,  5.,  7., nan])




```python
# NaN을 제외한 개수를 반환
s1.count()
```


    15




```python
# NaN을 제외한 평균
s1.mean()
```


    2.7333333333333334




```python
# numpy의 1차원 데이터 생성하고 평균을 계산
a = np.array([2,2,2,2,np.NaN])
print(a.mean())
```

    nan



```python
# 시리즈 경우 평균은 NaN을 제외하고 계산
b = pd.Series(a) # numpy 데이터를 시리즈로 변경
b
```


    0    2.0
    1    2.0
    2    2.0
    3    2.0
    4    NaN
    dtype: float64




```python
b.mean()
```


    2.0




```python
# 각 원소들의 그룹별 개수를 셈(빈도계산)
s1.value_counts()
```


    1.0    5
    3.0    3
    2.0    3
    5.0    2
    4.0    1
    7.0    1
    dtype: int64




```python
date = pd.date_range(start='2021-10-01', end='2021-10-20')
date
```


    DatetimeIndex(['2021-10-01', '2021-10-02', '2021-10-03', '2021-10-04',
                   '2021-10-05', '2021-10-06', '2021-10-07', '2021-10-08',
                   '2021-10-09', '2021-10-10', '2021-10-11', '2021-10-12',
                   '2021-10-13', '2021-10-14', '2021-10-15', '2021-10-16',
                   '2021-10-17', '2021-10-18', '2021-10-19', '2021-10-20'],
                  dtype='datetime64[ns]', freq='D')


```python
type(date)
```


    pandas.core.indexes.datetimes.DatetimeIndex




```python
date = pd.date_range(start='2021-10-01', end='2021-10-20', freq = 'D')
date
```


    DatetimeIndex(['2021-10-01', '2021-10-02', '2021-10-03', '2021-10-04',
                   '2021-10-05', '2021-10-06', '2021-10-07', '2021-10-08',
                   '2021-10-09', '2021-10-10', '2021-10-11', '2021-10-12',
                   '2021-10-13', '2021-10-14', '2021-10-15', '2021-10-16',
                   '2021-10-17', '2021-10-18', '2021-10-19', '2021-10-20'],
                  dtype='datetime64[ns]', freq='D')




```python
date = pd.date_range(start='2021-10-01', end='2021-10-20', freq = '3D')
date
```


    DatetimeIndex(['2021-10-01', '2021-10-04', '2021-10-07', '2021-10-10',
                   '2021-10-13', '2021-10-16', '2021-10-19'],
                  dtype='datetime64[ns]', freq='3D')




```python
# 2021-10-01일을 기준으로 1주일씩 증가하는 일자 생성 : 시작일(일요일)

date = pd.date_range(start='2021-10-01', end='2021-10-20', freq = 'W')
date
```


    DatetimeIndex(['2021-10-03', '2021-10-10', '2021-10-17'], dtype='datetime64[ns]', freq='W-SUN')




```python
# 2021-10-01일을 기준으로 1주일씩 증가하는 일자 생성 : 시작일(일요일)
date = pd.date_range(start='2021-10-01', end='2021-10-20', freq = 'W-SUN')
date
```


    DatetimeIndex(['2021-10-03', '2021-10-10', '2021-10-17'], dtype='datetime64[ns]', freq='W-SUN')




```python
# 2021-10-01일을 기준으로 1주일씩 증가하는 일자 생성 : 시작일(금요일)
date = pd.date_range(start='2021-10-01', end='2021-10-20', freq = 'W-FRI')
date
```


    DatetimeIndex(['2021-10-01', '2021-10-08', '2021-10-15'], dtype='datetime64[ns]', freq='W-FRI')




```python
# 2021-10-07일을 기준으로 1주일씩 증가하는 4개의 주 일자 생성 : 시작일(월요일)
date = pd.date_range(start='2021-10-07', periods = 4, freq = 'W-MON')
date
```


    DatetimeIndex(['2021-10-11', '2021-10-18', '2021-10-25', '2021-11-01'], dtype='datetime64[ns]', freq='W-MON')




```python
# 2021-10-07일을 기준으로 한 달 간격의 일자 4개 생성 : 월말기준
date = pd.date_range(start='2021-10-07', periods = 4, freq = 'M')
date
```


    DatetimeIndex(['2021-10-31', '2021-11-30', '2021-12-31', '2022-01-31'], dtype='datetime64[ns]', freq='M')




```python
# 2021-10-07일을 기준으로 한 달 간격의 일자 4개 생성 : 월초기준
date = pd.date_range(start='2021-10-07', periods = 4, freq = 'MS')
date
```


    DatetimeIndex(['2021-11-01', '2021-12-01', '2022-01-01', '2022-02-01'], dtype='datetime64[ns]', freq='MS')




```python
# 2021-10-01일을 기준으로 세 달 간격의 일자 4개 생성 : 월말기준
date = pd.date_range(start='2021-10-01', periods = 4, freq = '3M')
date
```


    DatetimeIndex(['2021-10-31', '2022-01-31', '2022-04-30', '2022-07-31'], dtype='datetime64[ns]', freq='3M')




```python
# 2개월 월초주기로 12개의 날짜 생성
date = pd.date_range(start='2021-10-01', periods = 12, freq = '2MS')
date
```


    DatetimeIndex(['2021-10-01', '2021-12-01', '2022-02-01', '2022-04-01',
                   '2022-06-01', '2022-08-01', '2022-10-01', '2022-12-01',
                   '2023-02-01', '2023-04-01', '2023-06-01', '2023-08-01'],
                  dtype='datetime64[ns]', freq='2MS')




```python
# 분기 시작일 기준으로 4개의 분기 시작일 생성
date = pd.date_range(start='2021-10-01', periods = 4, freq = 'QS')
date
```


    DatetimeIndex(['2021-10-01', '2022-01-01', '2022-04-01', '2022-07-01'], dtype='datetime64[ns]', freq='QS-JAN')



```python
# 연도 첫날 기준으로 4개의 연도 첫날짜 생성
date = pd.date_range(start='2021-10-01', periods = 4, freq = 'AS')
date
```


    DatetimeIndex(['2022-01-01', '2023-01-01', '2024-01-01', '2025-01-01'], dtype='datetime64[ns]', freq='AS-JAN')




```python
# 연도 마지막날 기준으로 4개의 연도 첫날짜 생성
date = pd.date_range(start='2021-10-01', periods = 4, freq = 'A')
date
```


    DatetimeIndex(['2021-12-31', '2022-12-31', '2023-12-31', '2024-12-31'], dtype='datetime64[ns]', freq='A-DEC')




```python
# 2022-01-07일 08:00시 부터 시간 기준으로 10개의 날짜 생성
date = pd.date_range(start='2022-01-07 08:00', periods = 10, freq = 'H')
date
```


    DatetimeIndex(['2022-01-07 08:00:00', '2022-01-07 09:00:00',
                   '2022-01-07 10:00:00', '2022-01-07 11:00:00',
                   '2022-01-07 12:00:00', '2022-01-07 13:00:00',
                   '2022-01-07 14:00:00', '2022-01-07 15:00:00',
                   '2022-01-07 16:00:00', '2022-01-07 17:00:00'],
                  dtype='datetime64[ns]', freq='H')




```python
# 2022-01-07일 08:00시 부터 업무시간 기준으로 10개의 날짜 생성
# 업무시간기준 : 9 TO 5로 설정
date = pd.date_range(start='2022-01-07 08:00', periods = 10, freq = 'BH')
date
```


    DatetimeIndex(['2022-01-07 09:00:00', '2022-01-07 10:00:00',
                   '2022-01-07 11:00:00', '2022-01-07 12:00:00',
                   '2022-01-07 13:00:00', '2022-01-07 14:00:00',
                   '2022-01-07 15:00:00', '2022-01-07 16:00:00',
                   '2022-01-10 09:00:00', '2022-01-10 10:00:00'],
                  dtype='datetime64[ns]', freq='BH')




```python
#30분 단위 : 30T 
date = pd.date_range(start='2022-01-07 08:00', periods = 10, freq = '30min')
date
```


    DatetimeIndex(['2022-01-07 08:00:00', '2022-01-07 08:30:00',
                   '2022-01-07 09:00:00', '2022-01-07 09:30:00',
                   '2022-01-07 10:00:00', '2022-01-07 10:30:00',
                   '2022-01-07 11:00:00', '2022-01-07 11:30:00',
                   '2022-01-07 12:00:00', '2022-01-07 12:30:00'],
                  dtype='datetime64[ns]', freq='30T')


