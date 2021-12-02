# Numpy
## 자주 사용했던 함수
* 계속 업데이트 예정
### 1. argmin, argmax
* array 내 최대값 또는 최소값의 index를 반환
 ```python
a = np.random.uniform(1, 30, 10)
a.argmax(), a.argmin()
# (3, 8)
```

### 2. np.argsort()
* 크기순서로 정렬할때 필요한 index의 배열을 반환
```python
a = np.random.uniform(1, 30, 10)
a.argsort()
# array([8, 6, 7, 4, 2, 0, 5, 1, 9, 3], dtype=int64)
a[a.argsort()]
# array([ 3.39883601,  4.99736689,  5.41667815,  6.08973134,  9.27541406,
#        15.64000579, 16.15427086, 19.35087261, 26.52980126, 29.75701383])
```
