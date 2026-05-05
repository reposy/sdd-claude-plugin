# {도메인} EDGECASE 목록

> 이 문서는 자동 생성된다. 수동 편집 금지.
> 마지막 갱신: YYYY-MM-DD HH:MM

## Contract별

### C1 로그인
- [EC-001](./EC-001.md) — 잘못된 비밀번호 `[input-validation]`
- [EC-002](./EC-002.md) — 잠긴 계정 `[auth-denied]`
- [EC-007](./EC-007.md) — 동시 로그인 시도 `[concurrency]`

### C2 토큰 갱신
- [EC-005](./EC-005.md) — 만료된 토큰 `[auth-denied]`
- [EC-008](./EC-008.md) — 위조된 서명 `[auth-denied]`

_비어 있는 Contract: C3_

## 카테고리별

### input-validation
- [EC-001](./EC-001.md) — 잘못된 비밀번호 `[C1]`

### auth-denied
- [EC-002](./EC-002.md) — 잠긴 계정 `[C1]`
- [EC-005](./EC-005.md) — 만료된 토큰 `[C2]`
- [EC-008](./EC-008.md) — 위조된 서명 `[C2]`

### concurrency
- [EC-007](./EC-007.md) — 동시 로그인 시도 `[C1]`

_비어 있는 카테고리: state-conflict, resource-limit, external-failure_

---

## 생성 규칙

### Contract별 섹션
- **그룹 정렬**: SPEC.md의 Contract 정의 순서대로 (C1 → C2 → C3...).
- **그룹 헤더 형식**: `{Contract ID} {Contract 이름}` — 이름은 SPEC.md에서 추출.
- **그룹 내 EC 정렬**: EC ID 오름차순.
- **참조 형식**: `[EC-XXX](./EC-XXX.md) — {title} \`[{category}]\``. category는 EC frontmatter에서 추출, 백틱 코드 표기.
- **여러 Contract를 다루는 EC**: 각 Contract 그룹에 중복 등장.
- **빈 Contract 그룹 처리**: 헤더 자체를 출력하지 않고, 섹션 말미에 `_비어 있는 Contract: C3, C5_`로 요약. 모두 채워졌으면 `_비어 있는 Contract: 없음_`.

### 카테고리별 섹션
- **그룹 정렬**: 표준 카테고리 6종 정의 순서대로.
  1. `input-validation`
  2. `state-conflict`
  3. `resource-limit`
  4. `auth-denied`
  5. `concurrency`
  6. `external-failure`
- **그룹 헤더 형식**: 카테고리 코드 그대로 (`### input-validation`).
- **그룹 내 EC 정렬**: EC ID 오름차순.
- **참조 형식**: `[EC-XXX](./EC-XXX.md) — {title} \`[{contracts}]\``. contracts는 EC frontmatter의 `contracts` 배열을 쉼표 구분.
- **빈 카테고리 그룹 처리**: 헤더 자체를 출력하지 않고, 섹션 말미에 `_비어 있는 카테고리: state-conflict, resource-limit_`로 요약. 모두 채워졌으면 `_비어 있는 카테고리: 없음_`.

### 공통
- **deprecated EC**: 카탈로그에 등장하지 않음.
- **EC 본문 중복**: 두 섹션에 같은 EC가 등장. 의도된 중복 (두 진입점).
