---
title: "import torch 에러 해결"

categories:
  - python
tags: 
  - install
  - Error
last_modified_at: 2020-08-04
---

퀵드로우 관련해서 여러가지 세팅하면서 오류가 자잘자잘하게 난다.

## pip Error

   ```ruby
(tensorflow) C:경로>pip install torchvision

Collecting torchvision
  Using cached torchvision-0.5.0-cp36-cp36m-win_amd64.whl (1.2 MB)
Requirement already satisfied: pillow>=4.1.1 in d:\program_files\anaconda3\envs\tensorflow\lib\site-packages (from torchvision) (7.2.0)
Requirement already satisfied: six in d:\program_files\anaconda3\envs\tensorflow\lib\site-packages (from torchvision) (1.15.0)
ERROR: Could not find a version that satisfies the requirement torch==1.4.0 (from torchvision) (from versions: 0.1.2, 0.1.2.post1, 0.1.2.post2)
ERROR: No matching distribution found for torch==1.4.0 (from torchvision)
   ```

## 해결법

   ```ruby
pip install torch==1.4.0 torchvision===0.5.0 -f https://download.pytorch.org/whl/torch_stable.html
   ```

   ```ruby
(tensorflow) C:경로>pip install torch==1.4.0 torchvision===0.5.0 -f https://download.pytorch.org/whl/torch_stable.html

Looking in links: https://download.pytorch.org/whl/torch_stable.html
Collecting torch==1.4.0
  Downloading https://download.pytorch.org/whl/cu92/torch-1.4.0%2Bcu92-cp36-cp36m-win_amd64.whl (641.8 MB)
     |████████████████████████████████| 641.8 MB 1.5 kB/s
Collecting torchvision===0.5.0
  Using cached torchvision-0.5.0-cp36-cp36m-win_amd64.whl (1.2 MB)
Requirement already satisfied: numpy in d:\program_files\anaconda3\envs\tensorflow\lib\site-packages (from torchvision===0.5.0) (1.18.5)
Requirement already satisfied: six in d:\program_files\anaconda3\envs\tensorflow\lib\site-packages (from torchvision===0.5.0) (1.15.0)
Requirement already satisfied: pillow>=4.1.1 in d:\program_files\anaconda3\envs\tensorflow\lib\site-packages (from torchvision===0.5.0) (7.2.0)
Installing collected packages: torch, torchvision
Successfully installed torch-1.4.0+cu92 torchvision-0.5.0
   ```

## 참고 사이트

[torchvision 공식 사이트](https://pypi.org/project/torchvision/)

[참고 - No matching distribution found for torch===1.4.0](https://stackoverflow.com/questions/60137572/issues-installing-pytorch-1-4-no-matching-distribution-found-for-torch-1-4)