# 노트북 실행 및 공개용 변경 사항

`trial_customer_clustering.ipynb`는 제공된 `중급2_1팀_Colab.ipynb`를 바탕으로 만든 공개용 사본입니다. 셀 순서와 분석·모델링 코드를 보존하고 입력 폴더를 `data/private/`로 변경했습니다. 입력이 없을 때 필요한 파일명을 표시하도록 했으며 제공된 원본 CSV로 전체 실행해 출력을 저장했습니다. Colab 등 환경 메타데이터를 정리했고 원본 파일은 수정하지 않았습니다.

## 실행 방법

1. [데이터 안내](../data/README.md)의 원본 CSV 4개를 `data/private/`에 배치합니다.
2. Python 3 환경에서 저장소 루트의 `requirements.txt`로 의존성을 설치합니다. 혼합 날짜 형식 처리 때문에 pandas 2.0 이상이 필요합니다.
3. 저장소 루트 또는 `notebooks/`에서 Jupyter를 열고 이 노트북을 처음부터 순서대로 실행합니다.
4. 한글 글꼴은 맑은 고딕·AppleGothic·나눔고딕 중 하나가 필요합니다. 원본 설정 셀은 Linux에서 글꼴 자동 설치를 시도합니다.

```bash
python -m pip install -r requirements.txt
python -m jupyterlab
```

KMeans는 `random_state=42`, `n_init=10`이며 bootstrap은 난수 20260917로 20회 수행합니다. 검증한 분석 라이브러리 버전은 `requirements.txt`에 기록했고 상세 환경은 [실행 검증 기록](../docs/execution_validation.md)을 참고하세요. 원래 프로젝트 실행 환경의 정확한 버전과는 구분합니다. 군집 ID의 숫자 자체보다 코드에서 붙인 행동 유형과 평가 지표를 비교하세요.

## 검증 범위

제공된 원본 CSV 4개로 공개본을 처음부터 끝까지 실행·재학습했습니다. 모델링 대상 6,202명, 결제 고객 2,394명, 다섯 군집 인원과 주요 평가 지표를 기존 산출물과 대조했습니다. 노트북 구조·코드 문법·파일 링크도 확인했습니다. 공개 노트북 출력은 재실행 결과이며 README의 그래프 4개는 원본 저장 이미지에서 추출해 보존했습니다.

원본 CSV가 준비되면 다음 명령으로 별도 검증 환경에서 전체 실행을 확인할 수 있습니다. 군집 수 탐색과 silhouette·bootstrap 계산에 시간이 걸릴 수 있습니다.

```bash
python -m jupyter nbconvert --execute --to notebook --output trial_customer_clustering.executed.ipynb --ExecutePreprocessor.timeout=1800 notebooks/trial_customer_clustering.ipynb
```
