## 사용 데이터 및 조회 범위

### 분석 기간을 적용하는 테이블

**2023년 5월 4일~2024년 5월 5일**의 기록을 각 테이블의 `created_at` 기준으로 조회한다.

```sql
WHERE created_at >= '2023-05-04 00:00:00'
  AND created_at <  '2024-05-06 00:00:00'
```

| 테이블 | 내용 | 추가 조건 |
|---|---|---|
| `polls_questionreport` | 질문 신고 기록 | — |
| `polls_usercandidate` | 질문 카드에 제시된 후보 유저 | — |
| `polls_questionset` | 질문 세트 | `status = 'F'`, `opening_time >= created_at` |
| `polls_questionpiece` | 질문 조각 및 투표·스킵 상태 | — |
| `accounts_userquestionrecord` | 투표 기록 | `answer_status <> 'P'` |
| `accounts_timelinereport` | 타임라인 신고 기록 | — |
| `accounts_blockrecord` | 유저 차단 기록 | — |

### 기간 제한 없이 조회하는 테이블

| 테이블 | 내용 | 조회 조건 |
|---|---|---|
| `polls_question` | 질문 문구 및 생성 정보 | 전체 기간 |
| `accounts_user` | 유저 정보 | `is_superuser = 0`, `is_staff = 0` |
| `accounts_school` | 학교 정보 | 전체 조회 |
| `accounts_group` | 학급과 학교 연결 정보 | 전체 조회 |
| `accounts_attendance` | 유저별 출석 날짜 목록 | 전체 조회 |

`accounts_user`는 이전 가입자의 활동 기록에도 유저 정보를 연결할 수 있도록 가입일 제한 없이 조회한다.

`accounts_attendance`는 생성일 컬럼이 없어 전체 조회하며, 필요할 경우 출석 날짜 목록을 펼쳐 분석 기간을 적용한다.
