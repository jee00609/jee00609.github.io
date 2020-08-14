---
title: "QuickDraw로 플레이 : 실시간 애플리케이션 - 코드 설명"

categories:
  - QuickDraw
tags: 
  - QuickDraw
  - Error
  - Hanium
last_modified_at: 2020-08-14
---

이번 시간엔 import 에러를 해결하는 법에 대해서 설명할 것이다.

[gautamkumarjaiswal](https://github.com/gautamkumarjaiswal/QucikDraw) 개발자님의 프로젝트에 도움을 받아 나 또한 QuickDraw 데이터셋을 어떻게 사용해야하는지 조금 감을 잡을 수 있었다.

참고한 프로젝트가 1년전 프로젝트란 버전 차이가 있어서 바로 실행이 되지 않는다는 점과 코드에 주석이 하나도 없다는 점에서 아쉬움이 있었다.

혹시나 나와 같이 QuickDraw 기능에 관심이 있고 사용해 보고 싶은 사람이 있을 수 있기에, 내가 기억나는 선에서 에러 해결법과 코드 해석을 하고자 한다.

이번 시간엔 import 에러를 해결하는 법에 대해서 설명할 것이다.

다음 시간엔 어떤 코드들을 고쳐야 하는지 설명하겠다.

## QuickDraw 문서

   * Step 1. [QuickDraw로 플레이 : 실시간 애플리케이션 - 번역](https://jee00609.github.io/quickdraw/QuickDraw-Translation/)
   * Step 2. [QuickDraw로 플레이 : 실시간 애플리케이션 - 코드 설명](https://jee00609.github.io/quickdraw/QuickDraw-import-error/)

## QuickDraw 하기 전 알아야 할 것!

   * Tensorflow 를 사용하기에 따로 가상환경을 만들어 주는 것이 좋다.
      * [가상 환경이 필요한 이유](https://chancoding.tistory.com/85)
   * [Akshay Bahadur](https://github.com/akshaybahadur21/QuickDraw) 의 프로젝트르 fork 또는 zip 파일로 다운받을 것
      * 이 포스팅 자체가 Akshay Bahadur 님의 코드를 기반으로 한다.

   ```ruby
/*
간단하게 텐서플로우 위한 가상환경 설치 실행 법을 작성했다.

conda create -n 가상환경이름 python=버전 //설치
activate 가상환경이름 //실행
deactive //종료
*/

conda create -n tensorflow python=3.6 anaconda 
activate tensorflow 
pip install tensorflow 
   ```

## 프로젝트 실행 순서

   1. 필수 패키지를 먼저 설치합시다
      * pip install tensorflow 
      * pip install matplotlib 
      * pip install opencv-python 
      * pip install keras 
      * pip install pandas 
      * pip install sklearn 
      * pip install scipy
   2. [데이터셋](https://github.com/googlecreativelab/quickdraw-dataset)에서 .npy 파일을 저장하여 /data 폴더안에 넣어라
   3. data 폴더에서 데이터를 가져오는 readDataset.py 를 실행시키자.
   4. LoadData.py 가 제대로 실행되면 trainModel.py 를 실행시켜 학습 시키고 학습 모델을 만든다.
   5. 모든 작업이 끝나면 runWebCam.py 를 실행시키자

## 원본 코드

   ```ruby
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.utils import shuffle
from keras.layers import Dense,Flatten, Conv2D
from keras.layers import MaxPooling2D, Dropout

from keras.utils import np_utils, print_summary
import tensorflow as tf
from keras.models import Sequential
from keras.callbacks import ModelCheckpoint
import pickle
from keras.callbacks import TensorBoard
   ```

## 에러

   ```ruby
// from keras.utils import np_utils, print_summary - 에러 구문
ImportError: cannot import name 'np_utils'
ImportError: cannot import name 'print_summary'
   ```

## 해결책

   ```ruby
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.utils import shuffle
from keras.layers import Dense,Flatten, Conv2D
from keras.layers import MaxPooling2D, Dropout

# from keras.utils import np_utils, print_summary - 에러
from keras.utils import np_utils
from tensorflow.python.keras.utils.layer_utils import print_summary
from tensorflow.keras.layers import Layer

import tensorflow as tf
from keras.models import Sequential
from keras.callbacks import ModelCheckpoint
import pickle
from keras.callbacks import TensorBoard
   ```

##비고

현재 import 에러만 고친 것이라 코드 부분에서 에러나는 것을 고쳐야 한다.

## 사이트

[이 포스팅의 기반이 되는 프로젝트 - gautamkumarjaiswal](https://github.com/gautamkumarjaiswal/QucikDraw)
[참고하면 좋은 사이트 - 퀵드로우 데이터셋](https://github.com/googlecreativelab/quickdraw-dataset)
[참고하면 좋은 사이트 - 가상환경](https://chancoding.tistory.com/85)