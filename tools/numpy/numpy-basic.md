# Numpy
## 0. Numpy란?
* Numerical Python
* 행렬 및 벡터 연산에 특화된 python Library
## 1. 특징
  * python List 에 비해 빠르고 효율적 
  * 반복문 없이 데이터배열에 대한 처리를 지원
  * 선형대수 관련된 기능을 제공
  * C나 C++, 포트란 등의 언어와 통합이 가능(C 기반으로 만들어진 Lib)
## 2. Basic numpy
  ### 2.0. 호출
```python
import numpy as np
```
* 호출방법
* 모든 사람들이 np라는 alias 를 사용해서 호출함

### 2.1. array 생성 함수
1. np.array(list, type)
```python
a = np.array([1,3,5,3], float)
# array([1., 3., 5., 3.])
```
* ndarray(배열) 생성함수
* C의 Array를 이용하여 배열을 생성함
* 하나의 데이터 type만 넣을수 있음
* python List와는 다르게 c의 array 구조를 가지기 때문에 메모리 관리 측면에서 효율적임
* 다른 배열(object)이면 pointer 값이 다르기 때문에 비교연산자 is를 사용할때 False가 나옴

2. np.ndarray()
```python
a = np.ndarray([1,3,5,3], float)
a.shape # (4,)
a.dtype # float
```
* 행렬을 나타내는 Class
  * np.array, np.ndarray 둘다 배열을 생성하지만 np.array를 쓰는것이 lowlevel에서 
  * array
* 차원을 알려주는 shape, data의 타입을 알려주는 dtype의 property 등이 존재

3. np.ones, np.zeros, np.empty + *_likes(shape, dtype)

```python
shape = [4, 2]
a = np.ones(shape, int)  # a.shape (4, 2)
b = np.zeros(shape, int)  # b.shape (4, 2)
c = np.empty(shape, int)  # c.shape (4, 2)
d = np.ones_like(shape, int) # d.shape (2,)
```
* ones, zeros, empty -> shape 크기의 배열 생성 (1, 0, 빈 배열)
* some_like -> input으로 넣은 배열의 shape와 같은 배열을 생성

4. np.arange(start, end, step)
```python
np.arange(0, 5, 0.5)
# array([0., 0.5, 1., ... 4.5])
```
* python 의 range와 비슷하게 동작, 배열을 생성

5. np.identity(n), np.eye(shape, k=0), np.diag(ndarray)
* np.identity : n 크기의 단위행렬을 생성
* np.eye(shape, k=0) : shape 모양을 가지고 k번째 행부터 대각선이 1인 행렬을 생성
* np.diag(ndarray) : 대각행렬의 값을 추출

### 2.2 array 기초함수
1. ndarray.reshape(shape)
```python
vector = [[1,3],[3,5]]
a = np.array(vector,int).reshape(-1)
# vector = array([1, 3, 3, 5])
```
* element 개수를 유지한 채로 array의 shape를 변경
* -1을 넣어서 size 기반으로 자동으로 개수를 선정해서 넣는다

2. ndarray.flatten()
* 다차원의 array를 1차원의 array로 변환시킴
* ndarray.reshape(-1)과 같은 기능을 한다.


### 2.3 array index
1. ndarray index
* ndarray에서는 array index를 다음과 같이 쓴다
```python
vector = [[1, 3, 5],[2, 4, 8]]
a = np.array(vector)
# a[1, 2] -> 8
```
2. ndarray slicing

```python
vector = [[1, 3, 5],[2, 4, 8]]
a = np.array(vector)
a[1, 1:2] # [[1, 3]]
a[:, 1:-1] # [[3, 5],[4, 8]]
a[:, ::2] # [[1, 5],[2, 8]]
```
* ndarray에서는 행과 열 부분을 나눠서 slicing이 가능
* range 함수와 비슷하게 step 지정도 가능