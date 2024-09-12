# numpy

numpy → 배열 생성&조작

```python
import numpy as np # 주로 np
```

## 생성

`np.array(data)`

고차원의 배열 생성 가능 → 이 차원의 크기를 shape으로 확인

## 연산

대부분의 연산자들은 오버라이딩되어 각 요소에 대해 계산을 취하도록 설정되어 있다.

```      
a = np.array([1,2,3])
b = np.array([4,5,6])
print(a+b) # 결과 : [5 7 9]
print(a*b) # 결과 : [4 10 18]
print(a**2) # 결과 : [1 4 9]
print(a % 2 == 0) # 결과 : [False True False]
```

## dimension 확인

arr.ndim  : 차원 수 확인

arr.shape : 각 차원의 크기 확인

arr.reshape()  : 데이터의 크기 변환


## Indexing

C++, Java, Python list 처럼 대괄호 안에 인덱스를 적어서 사용한다

```py

a = np.array([
	[1,2,3],
	[4,5,6],
])
print(a[0])

```

고차원인 경우에는 하나의 대괄호 안에 순서대로 인덱싱을 한다


원하는 그룹을 배열로 묶어서 선택할 수도 있다
```py
a= np.array([
	list(range(10)),
	list(range(10,20))
])
print(a)
print(a[1, [2,3,4]])
```

이를 응용해 : 을 사용해서 해당 축 방향으로 전체를 선택할 수 있다(MATLAB과 같은 용법). 

```py
print(a[:,2]) # 결과 : [3,6]
```


### 조건을 사용한 인덱싱
numpy.array 에 직접적으로 부등호를 사용하여 각 요소에 대해 조건을 검사할 수 있다. 또 이 조건으로 인덱싱 하여 해당 조건을 만족시키는 요소만 추출할 수 있다.
```py
array1d = np.arange(1,10)
print(array1d>5)
print(array1d[array1d>5])
```

#### 배열끼리 결합
np.hstack(a1,a2)  : 좌우로 붙임

np.vstack(a1,a2)  : 위아래로 붙임

np.dstack(a1,a2)  : 가장 안쪽 차원에 대해 붙임

np.stack(a1,a2,axis) : 지정한 축에 대해서 붙임

#### 간단한 배열 쉽게 만들기
np.ones(shape) : 지정된 shape을 가지는 1로 이루어진 배열

np.zeros(shape)  : 위와 같지만 0으로 이루어짐

np.empty(shape) : 위와 같지만 값을 초기화하지 않음. 값 자체는 상관없지만 큰 배열을 만들 때 사용

np.arange(start,end,step)  : python의 range와 같은 문법

np.linspace(start, end , count) : start 에서 end 까지의 구간을 count 개로 등분

#### 난수 배열들

`np.random.seed(seed)` : RNG의 seed 값 설정

`np.random.rand(차원1, 차원2, ...)` : 각 차원의 크기를 가진 0~1 사이 난수 배열

`np.random.randn(차원1, 차원2, ...)` : 각 인자에 해당하는 크기의 표준정규분포를 따르는 난수 배열

`np.random.randint(low, high, shape)` : shape 형태의 low~high 사이의 정수를

 가진 배열


### pandas

Table의 형태를 가지는 데이터를 다루는데에 많이 사용됨

```py
import pandas as pd #pd를 축약으로 많이 사용
```

## DataFrame

pandas를 사용하면서 가장 많이 볼 클래스. 테이블 형태이며, 각 열을 이루는 데이터들의 타입은 같아야 하지만 열 간의 데이터 타입은 달라도 된다.

```py
data = {
    "2015": [9904312, 3448737, 2890451, 2466052],
    "2010": [9631482, 3393191, 2632035, 2431774],
    "2005": [9762546, 3512547, 2517680, 2456016],
    "2000": [9853972, 3655437, 2466338, 2473990],
    "지역": ["수도권", "경상권", "수도권", "경상권"],
    "2010-2015 증가율": [0.0283, 0.0163, 0.0982, 0.0141]
}
columns = ["지역", "2015", "2010", "2005", "2000", "2010-2015 증가율"]
index = ["서울", "부산", "인천", "대구"]
df = pd.DataFrame(data, index=index, columns=columns)
```
각 행의 이름인 index 가 존재하며, 각 열에 대한 이름으로 columns 인자 또한 존재한다.


### CSV에서 DataFrame 읽어오기

```py
titanic_df = pd.read_csv(CSV파일경로)
titanic_df.info()

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 891 entries, 0 to 890
Data columns (total 12 columns):
 #   Column       Non-Null Count  Dtype  
---  ------       --------------  -----  
 0   PassengerId  891 non-null    int64  
 1   Survived     891 non-null    int64  
 2   Pclass       891 non-null    int64  
 3   Name         891 non-null    object 
 4   Sex          891 non-null    object 
 5   Age          714 non-null    float64
 6   SibSp        891 non-null    int64  
 7   Parch        891 non-null    int64  
 8   Ticket       891 non-null    object 
 9   Fare         891 non-null    float64
 10  Cabin        204 non-null    object 
 11  Embarked     889 non-null    object 
dtypes: float64(2), int64(5), object(5)
memory usage: 83.7+ KB
```
### 인덱싱

원하는 열의 이름으로 인덱싱할 수 있다

```py
print(titanic_df['Age'].head())
"""결과
0    22.0
1    38.0
2    26.0
3    35.0
4    35.0
Name: Age, dtype: float64
"""
```
행과 열에 모두 인덱싱을 하기 위해서는 `.loc[]` 이나 `.iloc[]` 을 사용

`.loc[행, 열]` : index와 columns 명을 사용하여 인덱싱

`.iloc[행,열]` : 데이터의 값과 상관없이 순서를 통해 인덱싱
