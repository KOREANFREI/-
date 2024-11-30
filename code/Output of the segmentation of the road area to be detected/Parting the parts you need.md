###    이미지에서 포트홀(원)을 검출합니다.
```
def detect_potholes(img):
    """
    이미지에서 포트홀(원)을 검출합니다.

    Args:
        img: 입력 이미지.

    Returns:
        tuple: 포트홀 검출 결과 이미지와 검출된 원의 개수.
    """
    # 이미지 복사
    img_with_circles = img.copy()

    # 가우시안 블러 처리
    blurred = cv2.GaussianBlur(img, (5, 5), 0)

    # Canny Edge Detection 적용
    edges = cv2.Canny(blurred, 50, 150)

    # Hough Circle Transform을 사용하여 원 검출
    circles = cv2.HoughCircles(edges, cv2.HOUGH_GRADIENT, dp=1, minDist=20, param1=50, param2=30, minRadius=10, maxRadius=50)

    detected_circles = 0  # 검출된 원의 개수

    # 원 그리기
    if circles is not None:
        circles = np.round(circles[0, :]).astype("int")
        detected_circles = len(circles)  # 검출된 원의 개수 저장
        for (x, y, r) in circles:
            # 원 주위에 초록색 원 그리기
            cv2.circle(img_with_circles, (x, y), r, (0, 255, 0), 4)

    return img_with_circles, detected_circles  # 원이 그려진 이미지 반환
```
###    이미지를 로드하고 전처리합니다.

```
def load_and_preprocess_image(img_path, img_size=(256, 256)):
    """
    이미지를 로드하고 전처리합니다.

    Args:
        img_path (str): 이미지 파일 경로.
        img_size (tuple): (width, height) 크기로 이미지를 조정. 기본값은 (256, 256).

    Returns:
        tuple: 전처리된 이미지 배열과 레이블.
    """
    try:
        img = cv2.imread(img_path)
        if img is None:
            print(f"이미지를 읽을 수 없습니다: {img_path}")
            return None, None

        # 이미지 높이, 너비 가져오기
        height, width = img.shape[:2]

        # 이미지 아래 절반 자르기
        cropped_img = img[height//2:height, 0:width]

        # 이미지 크기 조정
        img_resized = cv2.resize(cropped_img, img_size)

        # --- 도로 마스크 적용 ---
        road_mask = segment_road(img_resized)  # 도로 영역 분할 함수 호출
        masked_img = cv2.bitwise_and(img_resized, img_resized, mask=road_mask)  # 마스크 적용

        return masked_img, 1

    except Exception as e:
        print(f"오류 발생 {img_path}: {e}")
        return None, None

```
