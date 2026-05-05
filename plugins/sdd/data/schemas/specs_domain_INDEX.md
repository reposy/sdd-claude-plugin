# {도메인명}

> 이 문서는 자동 생성된다. 수동 편집 금지.
> 마지막 갱신: YYYY-MM-DD HH:MM

[SPEC 본문](./SPEC.md)
{SPEC frontmatter의 summary}

## 카탈로그
- [USECASE 목록](./usecases/INDEX.md)
- [EDGECASE 목록](./edgecases/INDEX.md)

## 대응 ISSUE

| ISSUE | 다루는 |
|---|---|
| [ISSUE-0012](../../issues/ISSUE-0012/INDEX.md) | UC-001, EC-001 |
| [ISSUE-0034](../../issues/ISSUE-0034/INDEX.md) | UC-002 |
| [ISSUE-0048](../../issues/ISSUE-0048/INDEX.md) | (SPEC 전반) |

---

## 생성 규칙

- **헤더**: 디렉터리명을 도메인명으로 사용.
- **SPEC 링크 + 한 줄 설명**: SPEC.md frontmatter의 `summary` 추출.
- **카탈로그**: usecases/, edgecases/ 디렉터리의 INDEX.md 진입점. 디렉터리 없으면 행 생략.
- **대응 ISSUE 정렬**: ISSUE ID 오름차순.
- **다루는 칸 규칙**: ISSUE frontmatter에서 이 도메인 관련 항목만 추출.
  - `usecase_refs`에 이 도메인의 UC가 있으면 해당 UC ID 표시
  - `edgecase_refs`에 이 도메인의 EC가 있으면 해당 EC ID 표시
  - UC/EC 참조 없이 `spec_refs`에 이 도메인만 있으면 `(SPEC 전반)` 표기
  - 정렬: UC 먼저(ID 오름차순), 그 다음 EC(ID 오름차순)
- **이 도메인과 무관한 ISSUE**: 표에 등장하지 않음.
- **카운트·진척 없음**: UC/EC 개수와 ISSUE 상태(open/closed)는 각 INDEX 책임.
