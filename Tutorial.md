# Tutorial 

## 구글 drive 연결 및 data directory연결

```python
from google.colab import drive
drive.mount('/content/drive')  # Google Drive 마운트

# 올바른 data_dir 경로를 설정
data_dir = '/content/drive/My Drive/data_road'  # 실제 데이터셋 위치에 맞게 수정
```

## data 파일 내 구조 확인 및 폴더 확인 

```python
import os

# data_road 폴더가 존재하는지 확인
if os.path.exists(data_dir):
    print("data_road 폴더가 존재합니다.")
else:
    print("data_road 폴더를 찾을 수 없습니다.")

# training 폴더 내 구조 확인
training_dir = os.path.join(data_dir, 'training')
if os.path.exists(training_dir):
    print("training 폴더가 존재합니다.")
    print("training 폴더 내용:", os.listdir(training_dir))
else:
    print("training 폴더를 찾을 수 없습니다.")

# training/image_2 폴더 확인
image_2_dir = os.path.join(training_dir, 'image_2')
if os.path.exists(image_2_dir):
    print("image_2 폴더 내용:", os.listdir(image_2_dir))
else:
    print("image_2 폴더를 찾을 수 없습니다.")
```
