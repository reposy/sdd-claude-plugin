---
name: sdd-issue
description: ISSUE를 작성한다. SPEC을 바탕으로 작업 단위를 도출. 사용자 발화 "이슈 작성", "이슈 도출", "작업 단위", "ISSUE 만들자" 또는 명시 호출 /sdd-issue {spec_id}에 트리거.
---

# sdd-issue

이 skill은 표준 동작 패턴(PLUGIN_SPEC §4)을 따른다.

## 변동 사항

- **인수**: `{spec_id}` (예: SPEC-auth). 없으면 INDEX에서 후보 제시.
- **읽을 INDEX**: `sdd/INDEX.md`, `sdd/issues/INDEX.md`, 인용 SPEC들
- **참조 가이드**: `data/guides/ISSUE_GUIDE.md`
- **참조 스키마**: `data/schemas/ISSUE.md`
- **산출 위치**: `sdd/issues/ISSUE-XXXX/ISSUE.md` (XXXX는 전역 4자리 순번)
- **갱신 INDEX**: `sdd/INDEX.md`, `sdd/issues/INDEX.md`, `sdd/issues/ISSUE-XXXX/INDEX.md`

## 추가 규칙

- 해당 SPEC이 없으면 즉시 stop + `sdd-spec` 권유.
- 이슈 디렉터리 생성 시 `INDEX.md`도 함께 (`data/schemas/issues_ISSUE_INDEX.md` 베이스, TASK·PLAN 표 빈 상태).
- ISSUE는 SPEC을 인용해야 함. 추론으로 만들지 않음.
- 완료 조건은 검증 가능한 형태로 (테스트 케이스 ID 또는 명시적 기준).

## 다음 단계 제안

ISSUE 완료 시:
- "ISSUE-{XXXX} 완료. TASK로 분해하시겠습니까? (`sdd-task ISSUE-{XXXX}`)"
