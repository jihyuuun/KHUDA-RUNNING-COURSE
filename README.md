# RUNNING-COURSE
경희대학교 인근 러닝코스 추천

📅 **기간**: Sep 2024 – Nov 2024 

## 📖 프로젝트 개요  

본 프로젝트는 **경희대학교 주변에서 안전하고 최적화된 러닝 코스를 추천하는 것**을 목표로 합니다.  
이를 위해 **횡단보도 수, 경사도, 가로등 수, 혼잡도**를 고려하여  **A*알고리즘**을 활용한 최적 경로 탐색 모델을 개발하였습니다.  

사용자가 원하는 러닝 거리를 입력하면  최소 비용(횡단보도 ↓, 경사 ↓, 조도 ↑, 혼잡도 ↓)인 경로를 추천합니다.  

## 🔍 프로젝트 필요성  

❌ 가파른 언덕 및 횡단보도가 많은 도로가 있어 일정한 페이스 유지가 어렵습니다.  
❌ 가로등이 부족한 구간이 있어 야간 러닝 시 위험 요소가 존재합니다.  
❌ 유동 인구가 많은 구역에서 원활한 러닝이 어려울 수 있습니다.  

사용자들은 자신에게 최적화된 새로운 러닝 코스를 발견할 수 있습니다.

## 🛠 기술 스택 

- **Python**: pandas, numpy, geopandas, networkx, folium  
- **경로 탐색 알고리즘**: A* 알고리즘  
- **데이터**: OpenStreetMap(OSM), OSRM API, QGIS

## 📂 프로젝트 구조  

```
/modeling            # A* 알고리즘 및 최적 경로 탐색 코드
/preprocessing       # 데이터 전처리 코드
README.md            # 프로젝트 설명
```

## 📊 데이터 설명

- **도보거리 및 횡단보도**: OpenStreetMap 데이터와 OSRM API를 이용
- **경사도**: 등고선 데이터를 활용하여 노드별 해발고도 추출
- **주점 여부**: 술집 골목에 해당하는 엣지를 선정, 이진 변수 할당
- **광역버스 정차 정류장 혼잡도**: 광역 버스가 정차하는 정류장이 위치한 엣지 식별
- **가로등 수**: 각 엣지에 인접한 가로등 데이터를 매핑

## 🎯 모델 개발 과정  

### **1️⃣ 데이터 전처리**

- **결측치 처리** 
- **정규성 검증**: Kolmogorov-Smirnov test
- **등분산성 검증**: Levene’s Test
- **정규화&스케일링**: Yeo-Johnson Transform, Robust Scaler, MinMax Scaler, 이진 변수 변환

### **2️⃣ 가중치 설정**  

**설문조사를 통해 변수별 가중치 설정**

<img width="388" alt="image" src="https://github.com/user-attachments/assets/627d3e80-0bbc-49c9-921a-9660e379d494" />

### **3️⃣ 비용 함수 정의**  
$$
\text{cost} = \sum w_i x_i
$$

- \( i \) ∈ {횡단보도, 가로등, 정류장 혼잡도, 술집 밀집 구역, 경사도}  
- \( w_i \) : 각 요소의 가중치  
- \( x_i \) : 해당 요소의 값   

### **4️⃣ A*알고리즘 적용**  
- **목적함수**

<img width="348" alt="image" src="https://github.com/user-attachments/assets/fc2c3b3a-419d-451e-94a0-d64b843d3c78" />

- **휴리스틱 함수**

<img width="152" alt="image" src="https://github.com/user-attachments/assets/ec5f3524-fb0a-418a-be48-79f46322efc4" />

## 🚀 모델 사용자화

- **시간대**
  - 낮: 횡단보도, 경사도, 정류장 혼잡도
  - 밤: 횡단보도, 경사도, 가로등, 술집 밀집 구역

- **출발 위치**: 사용자가 출발 위치 지정

- **거리**: 사용자가 총 거리 지정

## 📈 모델 개발 결과

<img width="422" alt="image" src="https://github.com/user-attachments/assets/1a5ff8bc-292d-4d0d-b09a-a8fcebf206e6" />

<img width="419" alt="image" src="https://github.com/user-attachments/assets/00d939ee-4b34-45bc-a094-0168cc50e818" />
