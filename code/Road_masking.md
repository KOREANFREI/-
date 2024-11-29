# 검출하고자 하는 도로영역 분할부분 출력

```python
**import cv2
import numpy as np
import os
from google.colab.patches import cv2_imshow

def segment_road(image):
    """
    이미지에서 도로 영역을 분할합니다.

    Args:
      image: 입력 이미지.

    Returns:
      도로 영역 마스크.
    """
    # HSV 색 공간으로 변환
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

    # 도로 색상 범위 지정 (회색, 검정)
    lower_gray = (0, 0, 25)
    upper_gray = (180, 80, 250)

    # 색상 범위에 해당하는 픽셀 마스크 생성
    mask = cv2.inRange(hsv, lower_gray, upper_gray)

    # 형태학적 연산 (선택 사항)
    kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5, 5))
    mask = cv2.morphologyEx(mask, cv2.MORPH_OPEN, kernel)

    return mask

# 이미지 디렉토리 경로
image_dir = '/content/drive/My Drive/data_road/training/image_2'

# 디렉토리 내의 모든 이미지 파일 처리
for filename in os.listdir(image_dir):
    if filename.lower().endswith(('.png', '.jpg', '.jpeg')):
        # 이미지 로드
        image_path = os.path.join(image_dir, filename)
        image = cv2.imread(image_path)

        if image is None:
            print(f"이미지를 읽을 수 없습니다: {filename}")
            continue

        # 도로 영역 분할
        road_mask = segment_road(image)

        # 색상 정의 (예: 파란색)
        color = (255, 0, 0)  # BGR 순서

        # 마스킹된 이미지 생성 (색상 적용)
        colored_mask = np.zeros_like(image)
        colored_mask[road_mask > 0] = color

        # 결과 출력 (원본 이미지와 색칠된 마스크를 합쳐서 출력)
        result = cv2.addWeighted(image, 0.7, colored_mask, 0.3, 0)
        cv2_imshow(result)**

```
