# {도메인} USECASE 목록

> 이 문서는 자동 생성된다. 수동 편집 금지.
> 마지막 갱신: YYYY-MM-DD HH:MM

## Contract별

### C1 로그인
- [UC-001](./UC-001.md) — 정상 로그인
- [UC-003](./UC-003.md) — 자동 재로그인

### C2 토큰 갱신
- [UC-002](./UC-002.md) — 토큰 갱신

### C3 로그아웃
- [UC-004](./UC-004.md) — 정상 로그아웃

_비어 있는 Contract: 없음_

---

## 생성 규칙

- **그룹 정렬**: SPEC.md의 Contract 정의 순서대로 (C1 → C2 → C3...).
- **그룹 헤더 형식**: `{Contract ID} {Contract 이름}` — 이름은 SPEC.md에서 추출.
- **그룹 내 UC 정렬**: UC ID 오름차순.
- **참조 형식**: `[UC-XXX](./UC-XXX.md) — {title}`. UC frontmatter의 `id`와 `title` 사용.
- **여러 Contract를 다루는 UC**: 각 Contract 그룹에 중복 등장.
- **빈 Contract 그룹 처리**: 헤더 자체를 출력하지 않고, 마지막에 한 줄 요약으로 모음 (`_비어 있는 Contract: C3, C5_`). 모두 채워졌으면 `_비어 있는 Contract: 없음_`.
- **deprecated UC**: 카탈로그에 등장하지 않음.
