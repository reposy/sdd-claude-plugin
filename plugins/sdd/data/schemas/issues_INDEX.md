# ISSUE 목록

> 이 문서는 자동 생성된다. 수동 편집 금지.
> 마지막 갱신: YYYY-MM-DD HH:MM

## auth

| ISSUE | 의존 | 상태 |
|---|---|---|
| [ISSUE-0012](./ISSUE-0012/INDEX.md) — 로그인 API 구현 | — | closed |
| [ISSUE-0034](./ISSUE-0034/INDEX.md) — 토큰 갱신 구현 | ISSUE-0012 | open |
| [ISSUE-0048](./ISSUE-0048/INDEX.md) — 비밀번호 재설정 흐름 | ISSUE-0012 | open |

## billing

| ISSUE | 의존 | 상태 |
|---|---|---|
| [ISSUE-0051](./ISSUE-0051/INDEX.md) — 결제 위탁 연동 | ISSUE-0012 | open |

## notification

| ISSUE | 의존 | 상태 |
|---|---|---|
| [ISSUE-0055](./ISSUE-0055/INDEX.md) — 알림 발송 파이프라인 | — | open |

## 도메인 횡단

| ISSUE | 도메인 | 의존 | 상태 |
|---|---|---|---|
| [ISSUE-0070](./ISSUE-0070/INDEX.md) — 세션 만료 시 결제 흐름 처리 | auth, billing | ISSUE-0034, ISSUE-0051 | open |

---

## 생성 규칙

### 그룹 분류
- 한 도메인만 참조하는 ISSUE는 그 도메인 그룹에 배치 (`spec_refs`가 단일 도메인).
- 둘 이상 도메인을 참조하는 ISSUE는 `도메인 횡단` 그룹에 배치 (`spec_refs`가 2개 이상).
- `spec_refs`가 비고 `adr_refs`만 있는 ISSUE는 `도메인 무관` 그룹 (필요 시).

### 그룹 정렬
- 도메인 그룹: 알파벳 순.
- `도메인 횡단`은 항상 마지막.
- 빈 그룹(ISSUE 0개)은 출력하지 않음.

### 그룹 내 정렬
- ISSUE ID 오름차순.

### 표 칸 규칙
- **ISSUE 칸**: `[ISSUE-XXXX](./ISSUE-XXXX/INDEX.md) — {title}`. ISSUE frontmatter의 `id`와 `title` 사용.
- **도메인 칸** (도메인 횡단 그룹 전용): `spec_refs` 도메인 알파벳 순 쉼표 구분.
- **의존 칸**: `depends_on` 배열을 쉼표 구분. 없으면 `—`.
- **상태 칸**: `status` 값 그대로 (`open` / `closed` / `cancelled`).

### 미노출 정보
- TASK 진척(`3/5 done`)은 표시하지 않음. ISSUE 디렉터리 INDEX 책임.
- ISSUE 본문 요약·목적은 표시하지 않음. 카탈로그는 진입점만.

### 그래프 없음
- ISSUE 의존 그래프는 본 INDEX에 포함하지 않음. 표의 `의존` 칸으로 충분.
- 향후 ISSUE 수가 많아져 그래프가 필요하면 별도 `sdd/issues/GRAPH.md`로 분리.
