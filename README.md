# 개요
이 코드는 Anomaly Detection 기술을 사용하여 도로 이미지에서 이상 현상(예: 포트홀)을 탐지하는 시스템을 구현합니다. OpenCV를 사용하여 이미지를 전처리하고, HSV 색상 공간을 기반으로 도로 영역을 분할합니다. Hough Circle Transform을 사용하여 포트홀을 감지하고, Canny Edge Detection을 통해 이미지의 가장자리를 검출하여 분석합니다.

## 주요 결과:
Anomaly Detection 기반 객체 감지: 도로 파손(포트홀)과 같은 위험 요소를 실시간으로 감지
FCN 기반 도로 파손 분할: 도로 표면 문제 탐지를 위한 추가적인 기술 적용

### 데이터셋 
https://www.cvlibs.net/datasets/kitti/의 무료제공 데이터셋 사용(상업적 목적 사용불가)

### 주요 기술
1. 이미지 전처리:

이미지 크기 조정: cv2.resize 함수를 사용하여 이미지 크기를 조정합니다.
도로 영역 분할: HSV 색상 공간에서 도로 색상 범위를 지정하고, cv2.inRange 함수를 사용하여 마스크를 생성합니다.
형태학적 연산: cv2.morphologyEx 함수를 사용하여 노이즈를 제거하고 마스크를 개선합니다.

2. 포트홀 감지:
Hough Circle Transform: cv2.HoughCircles 함수를 사용하여 이미지에서 원형 포트홀을 감지합니다.
Canny Edge Detection: cv2.Canny 함수를 사용하여 이미지에서 가장자리를 검출합니다.
가우시안 블러: cv2.GaussianBlur 함수를 사용하여 이미지를 부드럽게 처리합니다.

3. Anomaly Detection:
대신, Hough Circle Transform을 사용하여 포트홀을 감지하고, 이를 Anomaly로 간주합니다.
좀 더 정교한 Anomaly Detection 시스템을 구축하려면 Autoencoder, One-Class SVM 등의 Anomaly Detection 모델을 추가적으로 사용할 수 있습니다.
코드 분석

Google Colab 환경 설정
OpenCV, NumPy 등 필요한 라이브러리 설치
Google Drive 마운트 및 데이터 디렉토리 연결
코드 실행

## 코드 분석
segment_road 함수: 이미지에서 도로 영역을 분할합니다.
load_and_preprocess_image 함수: 이미지를 로드하고 전처리합니다.
detect_potholes 함수: 이미지에서 포트홀을 감지합니다.
preprocess_training_images 함수: training 데이터셋의 이미지를 전처리하고 포트홀을 감지합니다.

### 추가 정보
이 코드는 Google Colab 환경에서 실행되도록 설계되었습니다.
이미지 데이터는 Google Drive에 저장됩니다.
OpenCV, NumPy 등의 라이브러리가 필요합니다.

## 설치 및 사용법
Google Colab에서 코드를 실행합니다.(jupyter노트북에서만 사용가능한 함수가 포함되어있음)
Google Drive를 마운트하고 데이터 디렉토리를 연결합니다.
preprocess_training_images 함수를 호출하여 이미지 전처리 및 포트홀 검출을 수행합니다.
결과 이미지를 확인하고 분석합니다

## 참고 문헌 및 문서
Development and Evaluation of Automatic Pothole Detection Using Fully Convolutional Neural Networks
딥러닝을 이용한 고속도로 포장파손 탐지 연구
Pothole Detection Method in Asphalt Pavement
Neural Network Hardware Architecture for Pothole Detection

### 문제 및 기여
추가적으로 필요한 연구:

조명 변화, 그림자 등 환경 요인에 따라 탐지 성능이 영향을 받을 수 있습니다.
다양한 유형의 도로 파손에 대한 탐지 성능을 향상시키기 위한 추가 연구가 필요합니다.

### 향후 작업
다양한 도로 위험 요소 (예: 로드킬, 차선 표시) 감지 기능 추가
실시간 경고 시스템 개발 및 연동
딥러닝 모델 성능 개선 및 최적화
