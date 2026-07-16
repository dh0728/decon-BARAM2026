# [데이콘]제3회 풍력발전량 예측 AI 경진대회 - BARAM 2026

LDAPS/GFS 기상 예보 데이터와 SCADA 실측 데이터를 활용하여 3개 KPX 그룹의 시간별 풍력발전량을 예측하는 프로젝트입니다.

## 대회 개요

- **과제**: 2025년 전체 기간에 대한 3개 KPX 그룹(`kpx_group_1`, `kpx_group_2`, `kpx_group_3`)의 시간별 발전량(`kWh`) 예측
- **설비용량**: `kpx_group_1` 21.6 MW / `kpx_group_2` 21.6 MW / `kpx_group_3` 21.0 MW
- **입력 데이터**: LDAPS·GFS 기상 예보(전 지점), VESTAS·UNISON 터빈 SCADA 실측(학습 기간 한정)
- **시간 기준**: 모든 시각은 KST(`YYYY-MM-DD HH:MM:SS`)

## 평가 지표

최종 점수는 예측 오차(NMAE)와 경계 구간 적중률(FICR)을 절반씩 반영합니다.

```
score = 0.5 * (1 - NMAE) + 0.5 * FICR
```

## 데이터 구성

| 구분 | 파일 | 설명 |
|---|---|---|
| 학습 | `datasets/train/ldaps_train.csv` | LDAPS 기상 예보 (16격자) |
| 학습 | `datasets/train/gfs_train.csv` | GFS 기상 예보 (9격자) |
| 학습 | `datasets/train/train_labels.csv` | KPX 그룹별 실제 발전량 |
| 학습 | `datasets/train/scada_vestas_train.csv` | VESTAS 터빈 SCADA (12기) |
| 학습 | `datasets/train/scada_unison_train.csv` | UNISON 터빈 SCADA (5기) |
| 평가 | `datasets/test/ldaps_test.csv`, `datasets/test/gfs_test.csv` | 평가 기간 기상 예보 |
| 제출 양식 | `datasets/sample_submission.csv` | 제출용 CSV 양식 |
| 메타 정보 | `datasets/info.xlsx` | KPX 그룹·터빈·설비용량·위치 정보 |

컬럼 단위의 상세 설명은 [`datasets/data_description.md`](datasets/data_description.md)를 참고하세요.

## 저장소 구조

```
decon-BARAM2026/
├── datasets/   # 대회 제공 원천 데이터 (train/test, 설명 문서)
├── reports/    # EDA 및 실험 리포트
├── result/     # 제출 파일 등 결과물
└── README.md
```

## 주의사항

- 평가 기간의 실제 발전량, SCADA, 비공개 운영 데이터, 사후 보정자료, 재분석자료는 예측에 사용할 수 없습니다.
- 제출 파일은 Excel에서 열어 재저장하지 말고 코드로 생성해야 합니다.
- `sample_submission.csv`의 `forecast_id`, `forecast_kst_dtm` 값은 변경하지 않습니다.
