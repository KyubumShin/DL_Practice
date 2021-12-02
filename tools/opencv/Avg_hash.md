# 평균 해시 매칭
kaggle 대회를 진행하던중 중복되는 이미지 제거를 위해 무슨 기술이 있을까 찾아보던 중 알게됨

## 1. 개요
두 이미지를 작은 이미지로 hashing 시켜서 비교한뒤에 얼마나 비슷한지를 distance를 계산하는 방식  

## 2. 진행 방법
1. 이미지를 비율과 상관없이 특정 크기로 resize
2. 픽셀 전체의 평균값을 구해서 각 픽셀값이 평균값보다 작으면 0, 크면 1인 배열로 변환
3. 위의 배열을 reshape해서 1차원 행렬로 변환한뒤에 일치하는 숫자의 개수를 구한다.

```python
import cv2
import pandas as pd
import numpy as np
import os
from tqdm import tqdm

data_dir = './dataset/train/'
dataset = pd.read_csv('./dataset/train.csv')

dataset['image_size'] = dataset['Id'].apply(lambda image_id : cv2.imread(os.path.join(data_dir, image_id + '.jpg')).shape[:2])
dataset['image_total_size'] = dataset['image_size'].apply(lambda x: x[0] * x[1])
dataset = dataset.drop("Pawpularity", axis=1)


def img2hash(img):
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    gray = cv2.resize(gray, (16, 16))
    avg = gray.mean()
    bi = 1 * (gray > avg)
    return bi

def hamming_distance(a, b):
    a = a.reshape(1,-1)
    b = b.reshape(1,-1)
    # 같은 자리의 값이 서로 다른 것들의 합
    distance = (a !=b).sum()
    return distance

same_pic = []
pbar = tqdm(dataset.iterrows(), total=len(dataset), desc='test', mininterval=5)
for index, data in pbar:
    for index2, data2 in dataset[index+1:].iterrows():
        if np.all(data.drop('Id') == data2.drop('Id')):
            img = cv2.imread(os.path.join(data_dir, data['Id'] + '.jpg'))
            img_hash = img2hash(img)
            img2 = cv2.imread(os.path.join(data_dir, data2['Id'] + '.jpg'))
            img2_hash = img2hash(img2)
            dist = hamming_distance(img_hash, img2_hash)
            if dist == 0:
                same_pic.append((data['Id'], data2['Id']))
```

* 단점
  * 여러 이미지 그룹안에서 비슷한 사진을 찾을때는 그다지 효율이 좋아보이지 않는다. 시간복잡도가 높다
  * 메모리만 충분하다면 knn쪽이 더 효율이 좋아보임