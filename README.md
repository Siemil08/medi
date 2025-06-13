### 복약정보 시스템

# 데이터베이스

## 사용자

| 1 | 사용자ID | USER_ID | nvarchar | 8 | * | Y |  |  |  |  |
| :---: | :---- | :---- | :---: | :---: | :---: | :---: | :---: | :---- | :---- | :---- |
| 2 | 이름 | USER_NM | nvarchar | 50 | * |  |  |  |  |  |
| 3 | 생년월일 | USER_BOD | nvarchar | 10 | * |  |  |  |  | yyyy-mm-dd |
| 4 | 휴대폰 번호 | USER_PH | nvarchar | 12 | * |  |  |  |  | - 없이 저장 |
| 5 | 이메일주소 | EMAIL | nvarchar | 20 |  |  |  |  |  |  |
| 6 | 기본주소 | ADDR_MAIN | nvarchar | 100 | * |  |  |  |  |  |
| 7 | 기타주소 | ADDR_GITA | nvarchar | 100 |  |  |  |  |  |  |

## 약품기본정보

| 1 | 약품코드 | MED_CODE | nvarchar | 20 | * | Y |  |  |  |  |
| :---: | :---- | :---- | :---: | :---: | :---: | :---: | :---: | :---- | :---- | :---- |
| 2 | 약품명(국문) | MED_NAME_KOR | nvarchar | 100 | * |  |  |  |  |  |
| 3 | 약품명(영문) | MED_NAME_ENG | nvarchar | 100 | * |  |  |  |  |  |
| 4 | 재형명 | FORM_TYPE | nvarchar | 50 | * |  |  |  |  | 예: 정제, 캡슐 등 |
| 5 | 약효 분류 | EFFECT_TYPE | nvarchar | 50 | * |  |  |  |  |  |
| 6 | 함량 | INGREDIENT | nvarchar | 100 | * |  |  |  |  |  |
| 7 | 표준 보관법 | STORAGE_TYPE | nvarchar | 200 | * |  |  |  |  | 실온, 냉장 등 |
| 8 | 표준 유통기한 | STANDARD_EXP_MONTH | INT |  | * |  |  |  |  | 제조/구매일로부터 n개월 |

## 사용자 약품 정보

| 1 | 사용자약품ID | USER_MED_ID | INT |  | * | Y |  |  |  |  |
| :---: | :---- | :---- | :---: | :---: | :---: | :---: | :---: | :---- | :---- | :---- |
| 2 | 사용자ID | USER_ID | nvarchar | 8 | * | Y |  | USER | USER |  |
| 3 | 약품코드 | MED_CODE | nvarchar | 20 | * | Y |  | MedicineInfo | MED_CODE |  |
| 4 | 구매/처방일자 | PURCHASE_DATE | date |  | * |  |  |  |  |  |
| 5 | 실제유통기한 | ACTUAL_EXP_DATE | date |  | * |  |  |  |  | PURCHASE_DATE+STANDARD_EXP_MONTH |

## 처방정보

| 1 | 처방ID | PRESC_ID | INT |  | * | Y |  |  |  |  |
| :---: | :---- | :---- | :---: | :---: | :---: | :---: | :---: | :---- | :---- | :---- |
| 2 | 사용자약품ID | USER_MED_ID | INT |  | * | Y |  | USER_MEDICINE | USER_MED_ID |  |
| 3 | 1회 투약량 | DOSAGE | nvarchar | 50 | * |  |  |  |  |  |
| 4 | 1일 투여횟수 | FREQ_PER_DAY | INT |  | * |  |  |  |  |  |
| 5 | 총 투여일수 | TOTAL_DAYS | INT |  | * |  |  |  |  |  |
| 6 | 복용법 | INSTRUCTION | nvarchar | 500 | * |  |  |  |  |  |

## 알람

| 1 | 알림ID | ALERT_ID | INT |  | * | Y |  |  |  |  |
| :---: | :---- | :---- | :---: | :---: | :---: | :---: | :---: | :---- | :---- | :---- |
| 2 | 사용자ID | USER_ID | nvarchar | 8 | * | Y |  | USER | USER_ID |  |
| 3 | 사용자약품ID | USER_MED_ID | int |  | * | Y |  | USER_MEDICINE | USER_MED_ID |  |
| 4 | 알림유형 | ALERT_TYPE | nvarchar | 20 | * |  |  |  |  |  |
| 5 | 알림예정일 | ALERT_DATE | datetime |  |  |  |  |  |  |  |

## 폐기정보

| 1 | 수거함ID | BOX_ID | INT |  | * | Y |  |  |  | 폐의약품 수거함 고유번호 |
| :---: | :---- | :---- | :---: | :---: | :---: | :---: | :---: | :---- | :---- | :---- |
| 2 | 위치명 | LOCATION | nvarchar | 20 | * |  |  |  |  | 예: OO약국, OO보건소 |
| 3 | 주소 | ADDRESS | nvarchar | 100 | * |  |  |  |  | 주소 |
| 4 | 상세위치 | ADDRESS_D | nvarchar | 200 |  |  |  |  |  | 건물 내 위치 등 |
| 5 | 제형명 | FORM_TYPE | nvarchar | 50 | * |  |  |  |  |  |
| 6 | 배출법 | DISPOSAL_METHOD | nvarchar | 200 | * |  |  |  |  | 배출 방법 안내 |

# 로직

| 사용자 등록 관련 로직 |
| ----- |
| 사용자 등록      ← 이건 필수! 어떻게 회원 가입을 시키지? 일반 회원가입 (카카오로 로그인 api) [참고 링크](https://jinhos-devlog.tistory.com/entry/Spring-Rest-API-%EC%B9%B4%EC%B9%B4%EC%98%A4-Kakao-OAuth-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0) 회원 정보 입력  건강정보. 당뇨 같은 것…  피해야하는 약물 정보 알레르겐 임신 상태 등 거주지 입력 |
| **약품 등록 관련** |
| 사용자 약품 정보 약품 이름 1회 투약량 1일 투여량 총 투여일수 복용량 약품 사진 찍으면 그거 인식해서 자동으로 사용자 약품으로 등록 처방전, 약품 포장 정보 ocr 인식 사용자 약품으로 등록 건강 이음 투약이력 상세에서 추출 가능 유통기한 수동입력 / 자동입력  사용자가 피해야하는 약품 자동 인식(선택)  |
| **알림 서비스** |
| 유통기한 알람 폐기 알람 복약 알람 ocr이나 사진을 찍었을 때 성분 검색해서 먹어서는 안되는 약품 알람(선택) |
| **폐기 정보 관련 서비스** |
| 사용자의 위치정보 수집 위와 가장 가까운 약품 폐기 장소 검색 추천 사용자 약품에서 약품 ID를 가져와 배출법 자동 검색. 안내. |
| **API 관련** |
| 공공데이터 약품 정보 공공데이터 약품 폐기 장소 (카카오로 로그인 api) [참고 링크](https://jinhos-devlog.tistory.com/entry/Spring-Rest-API-%EC%B9%B4%EC%B9%B4%EC%98%A4-Kakao-OAuth-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0) |

# 사양

어플리케이션  
dart 안드로이드로 제작
