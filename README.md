# NetFlow 기반 악성 IP 탐지 프로젝트

## 프로젝트 소개
이 프로젝트는 국민대학교와 통신하는 외부 악성 IP를 탐지하는 시스템을 개발하는 것을 목표로 합니다. 네트워크 플로우 데이터를 분석하여 악성 IP를 식별하고, 탐지 성능을 향상시키기 위한 특징(feature) 엔지니어링을 수행합니다. 지도 학습 기반의 모델을 활용하여 악성 IP를 효과적으로 탐지하는 방법을 연구합니다.

## 주요 내용
- 네트워크 플로우 데이터를 활용하여 악성 IP 탐지
- 지도 학습 기반 모델을 학습 및 적용
- 네트워크 플로우의 특징을 분석하고, 탐지 성능을 높이기 위한 새로운 feature 생성
- 실제 악성 행위를 나타내는 네트워크 패턴을 분석하여 탐지 기법 개선
- 보호 대상 네트워크에 대한 침입 차단 개념 이해 및 적용

## 데이터셋 구성
- **네트워크 플로우 데이터 (총 1,302,830개)**
  - 내부 국민대 IP: 12,523개
  - 외부 정상 IP: 457개
  - 외부 악성 IP: 590개

### 특징
- 국민대학교 외부 통신 트래픽 데이터셋 (국민대학교 정보기획처 제공)
- 5시간 분량 네트워크 플로우 데이터
- 국민대학교 모든 건물 통신 (정보처 관리 서버 제외)
- 익명화된 Source IP 및 Destination IP
- 플로우 라벨링 기준: Source IP 또는 Destination IP의 악성 여부 (AbuseIPDB 참조)

## 기술 스택
- **프로그래밍 언어**: Python
- **머신러닝 프레임워크**: LightGBM
- **데이터 처리**: Pandas, NumPy
- **시각화**: Matplotlib, Seaborn

## 모델 성능 및 접근 방식
본 프로젝트에서는 LightGBM을 활용하여 악성 IP 탐지 모델을 구축하였습니다. 모델의 성능은 다음과 같습니다:

- **Train F1-Score**: 0.99918
- **Validation F1-Score**: 0.99563
- **Test F1-Score**: 0.994

모델의 고질적인 문제인 **False Negative**(탐지를 놓치는 경우)를 해결하기 위해 **IP Voting** 기법을 도입하였습니다. 특정 IP가 여러 번 이상 탐지될 경우에만 악성으로 판단하는 방식을 적용하여, 높은 신뢰도를 가지는 이상치에만 반응하도록 설계하였습니다. 이를 통해 오탐(false positive)을 줄이고, 실제 악성 IP 탐지 성능을 높일 수 있었습니다.
