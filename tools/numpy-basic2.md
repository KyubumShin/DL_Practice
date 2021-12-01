# Numpy

### 1. numpy random
1. np.random.uniform(start, end, n)
* 균등분포에 따라서 n개의 랜덤 수를 뽑아서 배열 생성
2. np.random.normal(start, end, n)
* 가우스분포(정규분포)에 따라서 n개의 랜덤 수를 뽑아서 배열 생성

### 2. numpy 연산
1. np.sum(ndarray, axis)
* 행렬의 합을 구하는 함수
* axis로 특정 차원에 대한 합을 구하는게 가능
```python
a = np.arange(30).reshape((2, 3, 5))
# array([[[ 0,  1,  2,  3,  4],
#         [ 5,  6,  7,  8,  9],
#         [10, 11, 12, 13, 14]],
# 
#        [[15, 16, 17, 18, 19],
#         [20, 21, 22, 23, 24],
#         [25, 26, 27, 28, 29]]])
np.sum(a, axis=0)
# array([[15, 17, 19, 21, 23],
#        [25, 27, 29, 31, 33],
#        [35, 37, 39, 41, 43]])
np.sum(a, axis=1)
# array([[15, 18, 21, 24, 27],
#        [60, 63, 66, 69, 72]])
np.sum(a, axis=2)
# array([[ 10,  35,  60],
#        [ 85, 110, 135]])
```
2. np.mean(ndarray, axis)
* 행렬의 평균을 구하는 함수
* sum과 똑같이 특정차원에 대한 평균을 구하는게 가능
```python
np.mean(a, axis=0)
# array([[ 7.5,  8.5,  9.5, 10.5, 11.5],
#        [12.5, 13.5, 14.5, 15.5, 16.5],
#        [17.5, 18.5, 19.5, 20.5, 21.5]])
np.mean(a, axis=1)
# array([[ 5.,  6.,  7.,  8.,  9.],
#        [20., 21., 22., 23., 24.]])
np.mean(a, axis=2)
# array([[ 2.,  7., 12.],
#        [17., 22., 27.]])
```
3. np.exp, np.sqrt, np.log, np.power, np.sin(ndarray)
* 각각 원소에 대해 해당하는 연산을 하는 함수

4. +, -, *, / (일반 연산)
* 각각 원소에 대해 연산을 할수 있다.
* 같은 shape을 가질때는 각각의 원소끼리 연산됨
* 다른 shape를 가질때는 broadcasting 연산
  * Matrix - scalar, scalar - vector, Matrix - vector 간의 연산 지원

5. np.dot, np.matmul
* 행렬 곱을 수행하는 함수
* 2차원까지는 두 함수가 같은 결과를 주지만, 3차원 이상의 고차원에서는 서로 다른 결과를 가짐
[https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=cjh226&logNo=221356884894](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=cjh226&logNo=221356884894)

6. transpose
* 전치행렬을 만듬
```python
a = np.arange(30).reshape((3, 5))
a.T.shape # (5,3)
```
### 3. numpy 배열 합치기
1. np.vstack, np.hstack(tuple)
* 배열을 합치는 함수
* vstack은 1-D, hstack은 2-D를 기준으로 합친다.
```python
a = np.arange(30).reshape((2, 3, 5))
b = np.arange(30).reshape((2, 3, 5))
np.vstack((a,b)).shape # (4, 3, 5)
np.hstack((a,b)).shape # (2, 6, 5)
```

2. np.concatenate(tuple, axis)
* 배열을 합치는 함수
* axis를 이용하여 기준이 되는 차원을 고를수 있음
```python
a = np.arange(30).reshape((2, 3, 5))
b = np.arange(30).reshape((2, 3, 5))
np.concatenate((a,b), axis=0).shape # (4, 3, 5)
np.concatenate((a,b), axis=1).shape # (2, 6, 5)
np.concatenate((a,b), axis=2).shape # (2, 3, 10)
```
### 4. boolean array
1. numpy에서는 조건문을 통해서 boolean array를 생성가능
```python
a = np.arange(30).reshape((2, 3, 5))
a < 5
# array([[[ True,  True,  True,  True,  True],
#         [False, False, False, False, False],
#         [False, False, False, False, False]],
# 
#        [[False, False, False, False, False],
#         [False, False, False, False, False],
#         [False, False, False, False, False]]])
```
2. np.all, np.any 로 전체에 대해서 판단 가능
```python
np.all(a < 3) # False
np.any(a < 15) # True
```
3. 배열끼리의 비교연산자 또한 연산 가능
```python
a = np.array([1, 3, 5])
b = np.array([5, 3, 1])
a == b
# array([False,  True, False])
```
4. np.where(조건문)
* 조건문에 해당하는 index값의 배열 출력
```python
a = np.arange(10)
np.where(a < 5)
# (array([0, 1, 2, 3, 4], dtype=int64),)
```

5. np.isfinite, np.isnan
* 발산하지 않은 값을 찾는 함수, nan 값을 찾는 함수