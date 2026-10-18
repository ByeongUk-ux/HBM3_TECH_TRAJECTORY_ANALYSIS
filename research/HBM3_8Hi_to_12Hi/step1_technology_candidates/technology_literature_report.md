# HBM3 8-Hi → 12-Hi 후공정 기술 후보 조사
작성일: 2026-10-18 (한국시간 기준)  
분석기업: SK하이닉스 · 단계: 전문가 검증 전 문헌 기반 후보 도출  
버전: 1.0

## 1. 연구목적 및 범위

이 조사의 목적은 SK하이닉스 HBM3 8단에서 12단으로 적층 수가 증가하는 과정에 관련된 후공정 기술을 추출하고, 이후 교차영향분석에 사용할 수 있도록 근거를 연결하는 것이다. 중요도 점수, 영향계수, 인과효과 추정 및 공진화 경로는 산출하지 않았다.

비교 기준은 **2022년 초기 양산 8단 16GB와 2023년 샘플 공개·공급 단계의 12단 24GB**이다. 제품 revision을 완전히 일치시킨 제조 이력 자료는 확보하지 못했다. HBM3E·HBM4의 기술이나 성능을 두 제품의 차이로 사용하지 않는다. 후속 자료에서도 HBM3의 과거 적용을 명시한 구간만 사용했다. [S02] [S03] [S05] [S06]

분석의 중심은 DRAM 다이 박막화, 분리, 수직 접속, 적층·접합, 충전·봉지, 검사·시험이다. 다음 경계를 함께 기록한다.

- **TSV 형성:** FEOL/MEOL 경계 후보 T33. 실제 공정 소관이 확인되기 전에는 순수 후공정과 합쳐 해석하지 않는다.
- **후면 TSV 노출·금속화:** 일반적으로 MEOL에 해당하므로 조사에 포함한다. Amkor의 공정 설명을 SK하이닉스의 공정순서로 사용하지 않는다. [S12]
- **DFT·시험체·해석:** 제조를 지원하지만 설계/검증 영역과 겹치는 T22·T23·T29·T31은 경계 후보이다.
- **더미 범프:** T34는 범프 제조와 배치 설계의 경계이다.
- **HBM–GPU/CPU 시스템 패키징:** 인터포저 제조, CoWoS/EMIB, 기판·보드 조립, 외부 냉각계는 이번 내부 HBM 적층 기술 후보의 중심 범위에서 제외한다. 시험환경을 이해할 때만 참고한다.

### Follow Paper 확인 결과

`Target_Paper.pdf`의 존재는 확인했다. 그러나 텍스트/페이지 읽기에서 본문이 반환되지 않았고, 파일 다운로드에도 실패했다. 따라서 **Ⅲ장과 Ⅳ장 1절을 직접 읽었다고 할 수 없다.** KCI에서 제목, 저자, 권호, DOI 및 초록을 확인했다. [S00]

이번 절차는 사용자가 제공한 “범위 설정 → 공정별 세부기술 도출 → 이후 전문가 검증” 설명을 기준으로 구성했다. 원논문의 세부 코딩 규칙이나 전문가 평가를 재현한 결과는 아니다. 기술트리·기술–공정 매트릭스를 최종 분류체계로 확정하지 않았다.

## 2. 문헌 검색 전략 및 자료 수집 결과

### 2.1 검색과 선별

한국어·영어로 기업/제품명, 공정명, 제조 문제를 조합해 검색하고, 검색 결과에서 공식 문서·출판사 페이지·특허 명세서로 이동했다. 새로운 용어가 나타나면 chip fixation, TSV reveal, KGD, RST, proxy package 등으로 확장했다.

실제로 실행한 **32개 검색식과 30개 접근 기록**을 `search_log.csv`에 보관했다. 이는 통합 웹 검색을 이용한 표적 문헌조사이다. Google Scholar·IEEE Xplore·KIPRIS·USPTO 각각의 내부 검색을 전수 수행한 체계적 문헌고찰이라고 주장하지 않는다. 유료 DB의 모든 검색 결과, 비공개 자료 및 특허 family 전체를 포괄하지 않는다.

문헌 DB는 **29개 기록**으로 구성된다. 이 중 S00은 방법론 논문이고, 나머지 28개는 기술 조사·선별 과정에서 유지한 자료이다. 검색에 우연히 등장한 무관한 모든 웹페이지를 문헌으로 집계하지 않았다. 번역판·동일 특허 family는 독립 실증 근거로 중복 계산하지 않는다.

| 자료 상태 | 건수 | 사용 원칙 |
|---|---:|---|
| 관련 본문 또는 해당 절 확인 | 23 | 확인한 구간의 범위 안에서만 사용 |
| 공식 검색 색인 초록/일부 텍스트만 확인 | 4 | S08·S20·S21·S27. 원문 미확인을 명시 |
| 방법론 서지·초록만 확인 | 1 | S00. 지정 절 미독 |
| 기술자료 본문을 확인하지 못함 | 1 | S28. 직접 증거로 미채택 |

23건은 “문헌 전체를 정독한 수”가 아니라, 이 과제에 필요한 본문 구간을 열람한 기록 수이다. 검색 서비스가 표시하는 상대 발행연도보다 문서의 날짜·표지·특허 우선일을 우선했다. HIR 파일 URL의 `2025/11`은 게시 경로이므로 문서의 2021/2023 발행연도로 대체하지 않았다.

### 2.2 두 가지 코드를 구분해서 읽는 법

CSV의 **Classification은 변화 유형**, **Evidence Level은 근거 수준**이다. “A. 공통 기술”의 A와 “근거 수준 A”는 서로 다른 개념이므로 변화 유형은 한글로 저장했다.

| 코드 | 이 조사에서의 적용 |
|---|---|
| 공통 | 두 제품에서 동일 기술 계열을 확인. 모든 공정조건이 같다는 의미는 아님 |
| 개선 | 기존 계열을 유지하면서 제품 간 변화가 직접 확인됨 |
| 신규 | 공식 자료가 12단 개발에서 도입했다고 설명하는 구현. 최초 발명 시점 주장은 아님 |
| 미확인 | 양쪽 제품 비교 또는 세부 구현을 확정할 자료가 부족함 |
| 근거 A | 해당 제품 적용 또는 개발 중 사용이 일차 자료에 직접 명시됨. 한쪽 제품만 확인될 수도 있음 |
| 근거 B | 학술문헌·특허에서 관련 기술을 확인하되 특정 제품 채택은 미확인. 학술 기술로드맵 HIR도 관련 기술 확인 자료로 취급 |
| 근거 C | 제품과의 연결이 가설적이거나 직접 자료가 부족함. 제조사 기술문서로 공법 자체를 확인했어도 HBM3 연관성을 직접 확정하지 못하면 보수적으로 C 부여 |

A는 독립 실험으로 성능 개선의 인과관계를 검증했다는 뜻이 아니다. 기업 자료는 **기업이 해당 적용·개발 경험을 밝혔다**는 근거이다. B/C 후보를 실제 미사용 기술로 읽어서는 안 된다.

### 2.3 시점·출처 추적

문헌 DB에 발행일, 기술 개발·적용 시점, 확인 상태와 범위 결정을 별도 열로 넣었다. 특허 우선일·출원일·공개일은 각각 다른 사건이며 상용 적용일을 뜻하지 않는다. 모든 후보는 Source ID, 모든 대응표 행은 Technology ID와 Source ID로 연결했다.

## 3. HBM3 8단과 12단의 제품 구조 및 기술적 차이

### 3.1 비교 가능한 사실

| 항목 | 8단 HBM3 | 12단 HBM3 | 근거와 해석 제한 |
|---|---|---|---|
| 적층 DRAM 수 | 8개 | 12개 | [S02]. 8/12는 DRAM 적층 수이며 base die까지 센 전체 실리콘 개수로 해석하지 않음 |
| 제품 용량 | 16GB | 24GB | [S02]. 적층 수와 용량 모두 1.5배 |
| 전체 적층 높이 | 비교 기준 | 같은 높이 수준 | [S02]. 절대 높이·공차·측정 기준면은 미확인 |
| 개별 DRAM 두께 | 비교 기준 | 기존 대비 40% 감소 | [S02]. 모든 위치의 다이가 같은 두께라는 근거는 없음 |
| 다이 간 간격 | 비교 기준 | 기존 대비 13% 축소 | [S03]. 수직 간극이지 범프의 수평 pitch 감소가 아님 |
| 패키징 계열 | MR-MUF | Advanced MR-MUF | [S05]. 기존 계열의 개선 |
| 내부 접속 | TSV와 범프 기반 | TSV와 범프 기반 | [S02] [S04] [S07]. 구체 치수·재료 변화 미확인 |

일반 HBM 구조는 base die 위 DRAM 적층체와 수직 접속으로 설명할 수 있다. 초기 SK하이닉스 학술자료도 이 구조를 설명하지만, 그 4단 실험체의 치수·재료를 HBM3에 옮겨 쓰지 않았다. [S27] HBM 내부의 수직 연결과 HBM–연산칩 사이의 시스템 패키지 연결도 별개이다. [S10]

### 3.2 발표 연혁의 주의점

| 시점 | 확인한 내용 | 해석 |
|---|---|---|
| 2021-10-20 | 16/24GB HBM3 개발 발표에 12개 다이·약 30 μm가 이미 등장 [S01] | 12단 개념이 2023년에 처음 등장했다고 쓰면 부정확 |
| 2022-01-27 | JESD238 공개 배포문에 8/12-high가 함께 포함 [S11] | 동일 규격 세대의 적층 옵션. 기업 제조공법 규정은 아님 |
| 2022-06 | 초기 HBM3 양산 [S02] [S07] | 이번 비교의 8단 기준. 24GB 양산까지 동시 확정한 것으로 확대하지 않음 |
| 2023-04-20 | 12단 24GB 샘플 평가·양산 준비 계획 발표 [S02] | 고객 평가/샘플 단계와 양산 완료를 구분 |
| 2024 회고 | 2023년 12단 HBM3 개발·양산 설명 [S06] | 사후 제품 적용 확인 자료 |

2021년 시제품 설명과 2023년 패키지 제품 발표의 정확한 개발 단계 차이는 추가 확인이 필요하다. **2021년의 30 μm와 2023년의 40% 감소를 조합해 8단 절대 두께를 역산하지 않았다.** 동일 revision이라는 근거가 없기 때문이다.

8단→12단의 용량 증가를 대역폭의 50% 증가로 바꾸어 해석하지 않았다. ECC·회로 설계·속도 등 제품특성의 변화도 모두 패키징 공정의 효과로 설명하지 않는다.

## 4. HBM 적층 패키징 공정 개요

### 4.1 공개자료로 구성한 일반 흐름

아래는 공정 이해를 위한 **일반 개요**이다. SK하이닉스의 공장 traveler, 실제 세부순서 또는 장비 목록은 아니다.

| 단계 | 입력 → 출력 | 후보/근거 |
|---|---|---|
| 선행 웨이퍼 제조·TSV 형성 | DRAM 회로/전극 형성 → TSV를 가진 웨이퍼 | 경계 T33; [S23] |
| 임시 지지·박막화·후면 가공 | 웨이퍼 → 목표 두께와 후면 접점을 가진 웨이퍼 | T01–T04, T07–T09, T25; 일반 MEOL [S12] |
| 접점 형성·검사·다이 분리 | 가공 웨이퍼 → 적층 가능한 다이 | T05–T06, T10, T21, T26; [S12] [S13] [S14] [S17] [S09] |
| 배치·정렬·접합 | 개별 다이/하부 웨이퍼 또는 다이 → 전기접속된 적층체 | T11–T14; [S04] [S22] |
| 칩 간 충전·봉지 | 적층체 → 보호재가 채워진 구조 | T15–T18; [S04] |
| 전기검사·신뢰성 평가·출하 준비 | 적층 패키지 → 규격 판정된 제품 | T19–T31; [S03] [S09] |

실제 순서는 기술 선택에 따라 달라진다. 특히 DBG/SDBG는 **절단 또는 개질을 먼저 하고 연삭으로 분리**하므로 “연삭 후 완전 절단”이라는 하나의 순서를 모든 후보에 강제할 수 없다. 범프의 앞/뒷면 가공 및 시험 삽입 위치도 미확인이다.

### 4.2 제품에서 확인한 부분 흐름

공식 기술 설명으로 확인되는 범위는 **다이 적층 중 순간 가열 고정 → 일괄 reflow 접합 → MUF 충전·봉지**라는 원리 수준이다. [S04] [S05] 가접합과 최종 접합은 같은 단계로 합치지 않는다. 열을 사용한다는 이유만으로 이 방식을 TC-NCF, laser-assisted bonding 또는 일반적인 TCB 전체와 동일시하지 않는다.

MR-MUF는 접합(MR)과 충전·봉지(MUF)의 통합 계열이다. 후보에서는 T13과 T15로 나누고, 12단 구현 변화 T14·T16·T17을 연결했다. 상위 계열 MR-MUF 자체를 또 하나의 독립 후보로 추가해 중복 집계하지 않았다.

## 5. 공정별 세부기술 후보

정의·기능·제품별 적용·변화·추가 검증 항목은 `technology_candidates.csv`에 있다. 아래는 탐색 영역별 인덱스이며 최종 기술트리가 아니다.

| 탐색 영역 | 기술 후보 |
|---|---|
| 박막화·지지·분리 | T01 후면연삭/두께 제어, T02 임시 캐리어, T03 debond/cleaning, T04 dry-polish stress relief, T05 DBG, T06 SDBG |
| TSV 후면 가공·접점 | T07 TSV reveal, T08 후면 절연/CMP, T09 backside metallization/RDL, T10 pillar/solder 형성, T11 TSV–범프 접속 |
| 적층·접합 | T12 픽업/정렬, T13 mass reflow, T14 순간가열 고정, T19 접합조건 탐색 |
| 충전·봉지·재료 | T15 MUF, T16 방열 EMC, T17 진공 가압 충전, T18 CTE/탄성률 제어 |
| 전기시험 | T20 12단 시험 기준, T21 KGD 선별, T22 적층 전후 시험 접근, T23 접속 검출회로, T24 daisy-chain/Kelvin |
| 계측·불량 분석 | T25 RST/TSV 깊이, T26 3D 광학검사, T27 초음파검사, T28 단면 SEM |
| 신뢰성·해석 | T29 열기계 FEA, T30 온도 사이클, T31 proxy 시험체 |
| 구현·범위 확인이 필요한 후보 | T32 stand-off/gap 관리, T33 TSV 형성, T34 thermal dummy bump, T35 박막 웨이퍼 휨 제어 |

서로 다른 수준의 항목을 모두 “완성된 독립 기술변수”로 취급하지 않는다.

- T19·T20은 공개된 개발 활동의 기능 단위이다. 사용된 장비·제어 알고리즘까지 확인된 세부기술이 아니다.
- T35는 공식 자료가 언급한 기능을 유실하지 않기 위한 임시 항목이다. T14 또는 T02와 중복인지 아직 모른다.
- T05/T06은 대안 공법이다. 제품에서 함께 쓰인 것으로 해석하지 않는다.
- T15/T16/T17은 각각 성형 방식/재료/충전 구현이다. 향후 평가에서 상하위 요소의 중복 영향을 점검한다.
- T10/T32는 범프 형성과 최종 간극 관리의 관계이다. T32는 변화된 형상에서 유도한 검증 전 후보이다.
- T24·T27·T28·T30은 평가 방법 후보이다. 양산 전수검사로 확인한 목록이 아니다.

## 6. HBM3 8단과 12단의 공정기술 적용 비교

| 유형 | 후보 | 판단 |
|---|---|---|
| 공통 3개 | T11, T13, T15 | 수직 접속·MR·MUF 계열이 두 제품에 이어짐 [S02] [S04] [S05] [S07] |
| 개선 2개 | T01, T16 | 박막화와 방열 보호재의 변화 확인 [S02] [S05] [S06] |
| 신규 적용 1개 | T14 | 공식 설명에서 12단 개발 시 도입한 칩 고정 구현으로 제시 [S04] [S05] |
| 미확인 29개 중 제품 직접 근거 4개 | T17, T19, T20, T35 | 12단 적용/개발 활동은 확인하되 양쪽 비교나 세부구현은 미확정 [S03] |
| 나머지 미확인 25개 | 나머지 ID | 기술 존재·일반 연관성은 있으나 특정 제품 채택 또는 변화 미확인 |

T14의 “신규”는 이번 두 제품 비교에서 공식적으로 소개된 도입을 뜻한다. 관련 아이디어의 세계 최초 발명, 특허와의 일대일 대응, 8단의 모든 revision에서 미사용이었다는 증명은 아니다. 더 엄격하게 양산 recipe 비교를 요구한다면 전문가 검토에서 “개선” 또는 “미확인”으로 재분류할 수 있도록 원래 근거를 보존했다.

**근거 A 10개가 모두 제품 간 개선을 뜻하지 않는다.** T17처럼 한쪽만 직접 확인되어 A이면서 변화유형은 미확인일 수 있다. 현재의 35개는 전문가 검증용 longlist이고, 교차영향행렬의 확정 차원 수가 아니다.

## 7. 적층 수 증가에 따른 기술적 문제와 대응기술

### 7.1 제품 개발에서 직접 설명된 연결

| 문제 | 확인된 대응/활동 | 근거 |
|---|---|---|
| 높이 제한 | 박막화 T01 | [S02] |
| 박막 칩 휨 | 순간가열 고정 T14, 구현 미공개 제어 T35 | [S04] [S05] [S03] |
| 협소 간극 충전 | 진공 가압 충전 T17 | [S03] |
| 접합·품질 확보 | 접합조건 탐색 T19, 시험 기준 T20 | [S03] |
| 방열 요구 | 보호재 개선 T16 | [S06] |

이는 기업이 밝힌 문제–대응 관계이다. 각 기술의 독립 효과나 영향 방향·크기를 통제 실험으로 분리한 결과는 아니다.

### 7.2 일반 문헌에서 추가한 연결

박막 취급/파손, TSV reveal 균일도, 절단면 손상, 정렬, 계면 피로, 검사 접근과 시험환경 대표성을 별도 문제로 정리했다. 예를 들어 underfill 물성과 접합 신뢰성의 관계는 4-chip WLUF 연구에서 확인되지만, 이 결과가 SK하이닉스 12단의 정량 최적 조건을 제공하지는 않는다. [S19]

`challenge_technology_map.csv`에는 **11개 문제와 44개 대응 관계**를 저장했다. 각 행의 Relation Status가 “제품 관계 확인”, “일반 기술 관계 확인; 제품 연결 가설”, “부분 문헌 확인” 등을 구분한다. 제품특성 열은 향후 검토할 연결 대상일 뿐 최종 제품특성 분류체계가 아니다.

### 7.3 정량 수치를 합치지 않은 이유

| 자료 | 공개 표현 | 이 조사에서의 처리 |
|---|---|---|
| S03 | 생산성 약 3배, 방열 약 2.5배 | 측정 대상·기준·공정 경계가 충분하지 않아 비교 지표 미채택 |
| S04 | 방열 36% 개선 | S03과 같은 실험·분모라는 근거 없음 |
| S05 | 신규 EMC 방열 특성 1.6배 | 재료 특성과 완성 패키지 방열을 구분 |
| S08 | MR-MUF와 TC-NCF의 실험 비교 | HBM3 8단→12단 비교가 아니며 원문도 부분 확인 |

서로 평균하거나 동일 성능지표로 환산하지 않았다. 제품 간격과 다이 두께 변화로 전체 높이를 재구성하는 계산도 base/top die·봉지층·측정 공차가 없어 수행하지 않았다.

## 8. 불확실한 기술 및 전문가 검증 필요사항

### 8.1 실제 적용 목록에서 분리한 사항

| 항목 | 처리 사유 |
|---|---|
| Hybrid bonding / bumpless Cu–Cu | 2023 설명은 향후 계획이다. HBM3 12단 적용으로 확인되지 않음 [S04] |
| TC-NCF가 SK하이닉스 HBM3 12단의 주 접합 방식이라는 주장 | 공식 MR-MUF 계보와 맞지 않음. 선행 특허·비교 실험은 채택 증명이 아님 [S05] [S08] [S22] |
| 삼성의 grouped TCB + reflow 특허 | 출원인과 시기가 다름. SK하이닉스 구현으로 전용하지 않음 [S26] |
| Offset stack package 특허 | TSV 정합 적층과 구조가 다름. 제목/출원인만으로 선정하지 않음 [S25] |
| HBM3E의 방열 개선율·다이 두께 | 다른 제품 세대 자료이므로 수치 전용 제외 [S05] |
| on-die ECC·DRAM 회로·셀 공정 | 제품/회로 특성이며 이번 후공정 기술 후보와 구분 [S07] [S11] |
| CoWoS·EMIB·인터포저 제조·냉각장치 | 시스템 패키징/냉각 영역. HBM 내부 적층의 후보 수에 포함하지 않음 [S10] |
| 단순한 “고수율·고방열·고용량” | 성과 또는 제품특성이지 세부 공정기술명이 아님 |

기술 중요도가 낮다고 판단해서 삭제한 항목은 없다. 위의 분리는 범위 또는 근거의 불일치에 따른 것이다.

### 8.2 검증 질문

1. **제품 식별:** 2021년 24GB 개발품과 2023년 12단 제품은 어떤 공정 revision 차이가 있는가? 비교할 8단/12단 part number를 확보할 수 있는가?
2. **박막화:** 최상층·중간층·base die 두께는 각각 무엇이며, 어떤 계측 위치와 공차를 적용했는가?
3. **휨 제어:** T35는 T14 가접합과 별개인가? carrier 지지, 표면 응력 조절 등 구체 구현은 무엇인가?
4. **접합:** 순간가열 가접합과 최종 mass reflow의 역할은 무엇이며, 기존 8단에 같은 단계가 있었는가?
5. **재료·충전:** 신규 EMC의 재료 특성과 유동/경화 조건 중 무엇이 바뀌었는가? 진공 가압 방식의 8단 사용 여부는?
6. **TSV·범프:** 재질, 높이, pitch, 후면 가공법에 실제 변경이 있었는가? 수직 간극 축소와 수평 pitch를 구분할 수 있는가?
7. **검사·시험:** 공개된 시험 기준 설정은 어떤 시험법/장비 개선을 뜻하는가? KGD/부분 적층/최종 시험은 어디에 삽입되는가?
8. **분석 단위:** T19·T20·T28·T29·T31을 공정기술로 평가할지, 공정 개발·검증 지원으로 분리할지? T35는 통합 가능한가?
9. **방법론 정합:** Follow Paper 지정 절을 확보한 뒤, 본 longlist의 기술 수준과 원논문의 전문가 도출 단위를 대조해야 한다.

근거 C나 원문 부분 확인 항목을 제외한 축소 목록부터 점수화하는 대신, 전문가에게 **채택 여부·구체 구현·중복 관계**를 먼저 물어 후보를 정제하는 것이 이번 단계의 다음 작업이다. 이는 중요도 평가가 아니다.

## 9. 공정기술 후보 도출 결과 요약

### RQ별 답변

- **RQ1:** 8단에서 직접 확인된 기술 계열은 TSV–범프 접속, MR, MUF이며, 12단 비교에서 기존 박막화·EMC 기준도 확인된다. 전체 제조 레시피는 공개 자료만으로 확정할 수 없다.
- **RQ2:** 12단은 동일 계열 위에 박막화·보호재 변경·칩 고정 구현을 더했다. 충전 및 시험 관련 직접 설명도 있으나 구현 상세는 제한적이다.
- **RQ3:** 높이 제약, 박막 칩 휨, 협소 간극 충전, 방열, 초기 수율/품질 확보가 제품 개발 설명과 연결된다. 나머지 문제는 일반 문헌 기반의 검증 가설이다.
- **RQ4:** 확인된 개선은 T01·T16, 도입 설명이 있는 구현은 T14이다. T17·T19·T20·T35는 12단에서 확인되지만 비교 유형을 확정하지 않았다.
- **RQ5:** 공통 3개를 포함한 35개 후보를 보존했다. 적층 증가가 각 기술의 중요도를 얼마나 바꾸는지는 평가하지 않았다.

총 **35개 후보 = 공통 3 + 개선 2 + 신규 1 + 미확인 29**이다. 근거 수준은 **A 10 + B 12 + C 13**이다. 후보 수는 성숙도·가치·핵심성 순위가 아니다.

이번 조사에서 답할 수 있는 핵심은 **기존 MR-MUF 기반 수직 적층을 유지하면서, 동일 높이에 더 많은 DRAM을 넣기 위한 박막화와 그에 수반되는 휨·충전·방열 문제에 대응하는 구현이 개선되었다**는 것이다. 특정 특허가 이 개선에 실제 사용되었는지, 공정변수의 변화량, 기술별 독립 효과는 아직 확인되지 않았다. [S02] [S04] [S05] [S06]

### 파일 사용 방법

| 파일 | 용도 |
|---|---|
| technology_literature_report.md | 범위·판단 기준·비교 결과·제한사항 |
| technology_candidates.csv | 후보별 정의/기능/제품 적용/검증 질문 |
| literature_database.csv | Source ID별 URL·위치·시점·확인 상태 |
| challenge_technology_map.csv | 문제–기술 관계와 확인/가설 상태 |
| search_log.csv | 실제 검색식과 접근 결과 |

CSV는 쉼표 구분, UTF-8 BOM 인코딩이다. Source ID의 여러 값은 세미콜론으로 구분했다. “미확인”을 미사용·0·결측치 제거 대상으로 자동 치환하지 않는다. Technology ID는 추후 통합·분할하더라도 이전 ID와의 관계를 기록해 추적성을 유지한다.

## 참고문헌 링크

아래는 열람 위치를 위한 링크 인덱스이다. 저자·시점·확인 상태와 근거 구간은 문헌 DB를 기준으로 한다.

- **S00**: 공진화 분석기반 기술 인텔리전스 : 반도체 패키지공정 사례. 2020. [원문/서지 링크](https://doi.org/10.14386/SIME.2020.28.4.63)
- **S01**: SK hynix Announces Development of HBM3 DRAM. 2021. [원문/서지 링크](https://news.skhynix.com/en/sk-hynix-announces-development-of-hbm3-dram/)
- **S02**: SK hynix Develops Industry’s First 12-Layer HBM3, Provides Samples to Customers. 2023. [원문/서지 링크](https://news.skhynix.com/en/sk-hynix-develops-industrys-first-12-layer-hbm3/)
- **S03**: Strengthening HBM Market Leadership: Meet the SK hynix Team Behind the World’s First 12-Layer HBM3. 2023. [원문/서지 링크](https://news.skhynix.com/en/meet-the-sk-hynix-team-behind-the-worlds-first-12-layer-hbm3/)
- **S04**: [Tech Pathfinder] Small Size, Big Impact: Unveiling the Latest Advances in Semiconductor Packaging and Miniaturization. 2023. [원문/서지 링크](https://news.skhynix.com/en/small-size-big-impact/)
- **S05**: [Rulebreakers’ Revolutions] How MR-MUF’s Heat Control Breakthrough Elevated HBM to New Heights. 2024. [원문/서지 링크](https://news.skhynix.com/en/rulebreaker-revolutions-mr-muf-unlocks-hbm-heat-control/)
- **S06**: SK hynix VP Gyujei Lee Targets Continued HBM Success With Next-Gen Packaging Technology. 2024. [원문/서지 링크](https://news.skhynix.com/en/gyujei-lee-next-gen-packaging-tech-key-to-hbm-success/)
- **S07**: “First Movers on a Path That No-one Has Taken Before” – Meet the Engineers Leading the World’s First Mass-production of HBM3. 2022. [원문/서지 링크](https://news.skhynix.com/en/meet-the-engineers-leading-the-worlds-first-mass-production-of-hbm3/)
- **S08**: A Study on the Advanced Chip to Wafer Stack for Better Thermal Dissipation of High Bandwidth Memory. 2023. [원문/서지 링크](https://doi.org/10.1109/ECTC51909.2023.00151)
- **S09**: Heterogeneous Integration Roadmap, 2023 Edition, Chapter 17: Test Technology. 2023. [원문/서지 링크](https://eps.ieee.org/wp-content/uploads/2025/11/ch17_test.pdf)
- **S10**: Heterogeneous Integration Roadmap, 2021 Edition, Chapter 22: Interconnects for 2D and 3D Architectures. 2021. [원문/서지 링크](https://eps.ieee.org/wp-content/uploads/2025/11/ch22_2D-3D.pdf)
- **S11**: JEDEC Publishes HBM3 Update to High Bandwidth Memory (HBM) Standard. 2022. [원문/서지 링크](https://markets.financialcontent.com/stocks/article/bizwire-2022-1-27-jedec-publishes-hbm3-update-to-high-bandwidth-memory-hbm-standard?CSSURL=36.htm)
- **S12**: 2.5D/3D TSV Packaging. 미표기. [원문/서지 링크](https://amkor.com/technology/25d-3d-tsv/)
- **S13**: DBG (Dicing Before Grinding) Process. 미표기. [원문/서지 링크](https://www-hq.disco.co.jp/eg/solution/library/dbg/dbg_process.html)
- **S14**: SDBG (Stealth Dicing Before Grinding) Process. 미표기. [원문/서지 링크](https://www.disco.co.jp/eg/solution/library/dbg/sdbg.html)
- **S15**: Stress Relief for the DBG Process. 미표기. [원문/서지 링크](https://www.disco.co.jp/eg/solution/library/dbg/dbg.html)
- **S16**: BGM Series. 미표기. [원문/서지 링크](https://www.lasertec.co.jp/en/products/semiconductor/bgm300.html)
- **S17**: Lasertec Launches New Bump Inspection and Measurement System BIM300. 2014. [원문/서지 링크](https://www.lasertec.co.jp/en/news/2014/20141113_2891.html)
- **S18**: Bump & Copper Pillar. 미표기. [원문/서지 링크](https://www.camtek.com/markets/bump-copper-pillar/)
- **S19**: Effect of Wafer Level Underfill on the Microbump Reliability of Ultrathin-Chip Stacking Type 3D-IC Assembly during Thermal Cycling Tests. 2017. [원문/서지 링크](https://doi.org/10.3390/ma10101220)
- **S20**: Temporary polymer bonding for the manufacturing of thin wafers: An innovative low temperature process. 2021. [원문/서지 링크](https://doi.org/10.1016/j.mssp.2020.105550)
- **S21**: Proposed package type for evaluating reliability of HBM Memory. 2024. [원문/서지 링크](https://doi.org/10.1016/j.sse.2024.108923)
- **S22**: US20190333910A1 — Methods of stacking semiconductor dies. 2019. [원문/서지 링크](https://patents.google.com/patent/US20190333910A1/en)
- **S23**: US9140743B2 — Semiconductor system that tests the connectivity between a metal and a bump that are formed in the upper portion of a penetrating electrode. 2015. [원문/서지 링크](https://patents.google.com/patent/US9140743B2/en)
- **S24**: US12002783B2 — Methods of manufacturing semiconductor device with bump interconnection. 2024. [원문/서지 링크](https://patents.google.com/patent/US12002783B2/ko)
- **S25**: US20220293564A1 — Stack packages and methods of manufacturing the same. 2022. [원문/서지 링크](https://patents.google.com/patent/US20220293564A1/en)
- **S26**: KR20250100153A — Semiconductor package. 2025. [원문/서지 링크](https://patents.google.com/patent/KR20250100153A/en)
- **S27**: A Study on the Effectiveness of Underfill in the High Bandwidth Memory with TSV. 2013. [원문/서지 링크](https://doi.org/10.4071/isom-2013-THP15)
- **S28**: Event Materials — IR Materials. 미표기. [원문/서지 링크](https://www.skhynix.com/ir/UI-FR-IR12_T7/)

[S00]: https://doi.org/10.14386/SIME.2020.28.4.63
[S01]: https://news.skhynix.com/en/sk-hynix-announces-development-of-hbm3-dram/
[S02]: https://news.skhynix.com/en/sk-hynix-develops-industrys-first-12-layer-hbm3/
[S03]: https://news.skhynix.com/en/meet-the-sk-hynix-team-behind-the-worlds-first-12-layer-hbm3/
[S04]: https://news.skhynix.com/en/small-size-big-impact/
[S05]: https://news.skhynix.com/en/rulebreaker-revolutions-mr-muf-unlocks-hbm-heat-control/
[S06]: https://news.skhynix.com/en/gyujei-lee-next-gen-packaging-tech-key-to-hbm-success/
[S07]: https://news.skhynix.com/en/meet-the-engineers-leading-the-worlds-first-mass-production-of-hbm3/
[S08]: https://doi.org/10.1109/ECTC51909.2023.00151
[S09]: https://eps.ieee.org/wp-content/uploads/2025/11/ch17_test.pdf
[S10]: https://eps.ieee.org/wp-content/uploads/2025/11/ch22_2D-3D.pdf
[S11]: https://markets.financialcontent.com/stocks/article/bizwire-2022-1-27-jedec-publishes-hbm3-update-to-high-bandwidth-memory-hbm-standard?CSSURL=36.htm
[S12]: https://amkor.com/technology/25d-3d-tsv/
[S13]: https://www-hq.disco.co.jp/eg/solution/library/dbg/dbg_process.html
[S14]: https://www.disco.co.jp/eg/solution/library/dbg/sdbg.html
[S15]: https://www.disco.co.jp/eg/solution/library/dbg/dbg.html
[S16]: https://www.lasertec.co.jp/en/products/semiconductor/bgm300.html
[S17]: https://www.lasertec.co.jp/en/news/2014/20141113_2891.html
[S18]: https://www.camtek.com/markets/bump-copper-pillar/
[S19]: https://doi.org/10.3390/ma10101220
[S20]: https://doi.org/10.1016/j.mssp.2020.105550
[S21]: https://doi.org/10.1016/j.sse.2024.108923
[S22]: https://patents.google.com/patent/US20190333910A1/en
[S23]: https://patents.google.com/patent/US9140743B2/en
[S24]: https://patents.google.com/patent/US12002783B2/ko
[S25]: https://patents.google.com/patent/US20220293564A1/en
[S26]: https://patents.google.com/patent/KR20250100153A/en
[S27]: https://doi.org/10.4071/isom-2013-THP15
[S28]: https://www.skhynix.com/ir/UI-FR-IR12_T7/

