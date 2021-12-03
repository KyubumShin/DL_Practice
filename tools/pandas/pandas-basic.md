# Pandas
## 1. Pandas란?
* panel data -> pandas
* 구조화된 데이터의 처리를 지원하는 Python 라이브러리
* 데이터 처리 및 통계분석을 위해 사용함
* 기본적으로 2차원 배열 형태의 Series(하나의 column)와 Dataframe(전체 column을 포함) 두가지의 type을 가지고 조작함

## 2. pandas 기본
### 0. pandas 호출
* pandas는 pd라고 alias를 지정함
* read_* 계열의 함수로 파일을 pandas object로 불러옴
```python
import pandas as pd # 약속임
data = pd.read_csv(file_dir) # csv 파일 호출
```

### 1. 기본함수
1. Dataframe.head(n)
* 처음 n개의 줄의 데이터를 출력
* 기본적으로는 5개를 출력한다
2. Dataframe.tail(n)
* 뒤에서부터 n개의 데이터를 출력
* head와 같이 5개를 기본으로 한다
3. Dataframe.describe()
* 수치형 데이터에 대해 요약을 해준다
* 평균 분산, max, min, count 등의 정보를 보여줌

4. Dataframe.info()
* column의 타입, count, 등의 전반적인 정보를 나타냄