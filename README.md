# LoanDefaultPrediction
23-1 Data Science Term Project

1. 전처리
    - 불필요한 피처 제거 - ID , unnamed
    - 대소문자 다른 거 통합 ( loan title )
    - 결측값 확인 - 없음.
    - 중복값 확인 - 없음.
    - 이상치 처리
        - numerical
            - 통계적 기법: 42000개 중에 37000 개 데이터가 하나 이상의 피처 에서 이상치가 있었음
            - isolate forest 라이브러리: 3000개 데이터에서 이상치 발견, 제거
        - objective
            - 빈도수를 통해서 수치형 데이터로 변환 ( 빈도 같은 게 없었음 )
            - IQR로 했는데
            - 클래스를 삭제해버리면 문제 생길 듯 ? 안함
            - !!! 한번 더 생각해보기 !!!
    - 상관계수 확인 - 상관계수 높은 거 없어서 (피처 다 독립)이라 상관계수 기반 삭제 안함
    - feature importance 확인
        - 우선 objective type을 label encoding 진행
        - RandomForest로 feature Importance 추출
        - threshhold 값 이하는 제거하기
        - label된 것들 중에서, 원래 one-hot 하려고 했던 feature는 one-hot하기
    - 범주형 변수 인코딩
        - 클래스 많은 거는 label 인코딩
        - 나머지는 onehot 인코딩
        - grade(0-6), subgrade(0-34)는 순서 있으니까 각각 오디널 인코딩.
2. 불균형 처리
    - ~~SMOTE  → 업샘플링. 너무 많은 데이터 생성~~
    - SMOTE+Tomek Link → 일부 줄이고 일부 늘리는 방법 선택
3. 하이퍼파라미터 서치
    - 랜덤 서치 f1 score 다 0 나와서 안 씀
4. train (모델링)
    - 방법 : 각 모델의 장점 파악. 모델마다 ROC / 혼동행렬
    - 보팅: 상위 3개 or 정확도 확 차이나는 부분 있으면 거기서 자르기
