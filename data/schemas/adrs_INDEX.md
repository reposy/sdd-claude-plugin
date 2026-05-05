# ADR 목록

> 이 문서는 자동 생성된다. 수동 편집 금지.
> 마지막 갱신: YYYY-MM-DD HH:MM

총 {n}개 결정 기록.

## 출처 문서별 (context_doc)

발생 맥락이 된 문서별 그룹화. 한 ADR은 하나의 context_doc에만 속한다.

### ROOT_SPEC
- [ADR-001](./ADR-001.md) — 모노리스로 시작
- [ADR-003](./ADR-003.md) — PostgreSQL 채택
- [ADR-006](./ADR-006.md) — 가독성 우선 가치관

### SPEC-auth-v1.0
- [ADR-002](./ADR-002.md) — JWT 인증 채택

### SPEC-auth-v1.2
- [ADR-005](./ADR-005.md) — OAuth2로 변경

### SPEC-billing-v0.4
- [ADR-004](./ADR-004.md) — 결제 외부 위탁

## 주제별 (tags)

frontmatter의 tags별 그룹화. 한 ADR은 여러 tag에 등장할 수 있다.

### architecture
- [ADR-001](./ADR-001.md) — 모노리스로 시작

### auth
- [ADR-002](./ADR-002.md) — JWT 인증 채택
- [ADR-005](./ADR-005.md) — OAuth2로 변경

### billing
- [ADR-004](./ADR-004.md) — 결제 외부 위탁

### code-quality
- [ADR-006](./ADR-006.md) — 가독성 우선 가치관

### data
- [ADR-003](./ADR-003.md) — PostgreSQL 채택

### infra
- [ADR-003](./ADR-003.md) — PostgreSQL 채택

### philosophy
- [ADR-001](./ADR-001.md) — 모노리스로 시작
- [ADR-006](./ADR-006.md) — 가독성 우선 가치관

### security
- [ADR-002](./ADR-002.md) — JWT 인증 채택
- [ADR-005](./ADR-005.md) — OAuth2로 변경

### vendor
- [ADR-004](./ADR-004.md) — 결제 외부 위탁

## 시간 순 전체 목록

| ID | 제목 | 날짜 |
|---|---|---|
| [ADR-006](./ADR-006.md) | 가독성 우선 가치관 | 2026-05-01 |
| [ADR-005](./ADR-005.md) | OAuth2로 변경 | 2026-04-30 |
| [ADR-004](./ADR-004.md) | 결제 외부 위탁 | 2026-04-15 |
| [ADR-003](./ADR-003.md) | PostgreSQL 채택 | 2026-04-02 |
| [ADR-002](./ADR-002.md) | JWT 인증 채택 | 2026-03-25 |
| [ADR-001](./ADR-001.md) | 모노리스로 시작 | 2026-03-10 |

---

## 생성 규칙

- **그룹 정렬 (출처 문서별)**: ROOT_SPEC → SPEC-{domain}-v{ver} (도메인 알파벳 순, 같은 도메인 내 버전 오름차순) → ISSUE-XXXX (숫자 오름차순) → TASK-XX 등 기타.
- **그룹 정렬 (주제별)**: tag 알파벳 순.
- **그룹 내 ADR 정렬**: ID 오름차순 (= 작성 시간 순).
- **시간 순 전체 목록**: 날짜 내림차순 (최신 먼저). 같은 날짜는 ID 내림차순.
- **빈 그룹 표시 안 함**: 항목이 0개인 context_doc 또는 tag는 섹션에 등장하지 않음.
- **참조 형식**: `[ADR-XXX](./ADR-XXX.md) — {title}`. 본문 frontmatter의 `id`와 `title`을 그대로 사용.
- **마지막 갱신**: 생성기 실행 시각.
