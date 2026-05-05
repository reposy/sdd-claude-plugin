---
name: sdd-task
description: TASK를 작성한다. ISSUE를 PR 단위 작업으로 분해. 사용자 발화 "태스크", "PR 단위", "작업 분해" 또는 명시 호출 /sdd-task {issue_id}에 트리거.
---

# sdd-task

이 skill은 표준 동작 패턴(PLUGIN_SPEC §4)을 따른다.

## 변동 사항

- **인수**: `{issue_id}` (예: ISSUE-0001). 없으면 INDEX에서 진행 중 ISSUE 후보 제시.
- **읽을 INDEX**: `sdd/issues/INDEX.md`, `sdd/issues/{issue_id}/INDEX.md`
- **참조 가이드**: `data/guides/TASK_GUIDE.md`
- **참조 스키마**: `data/schemas/TASK-XX.md`
- **산출 위치**: `sdd/issues/{issue_id}/TASK-XX.md` (XX는 ISSUE 내 순번)
- **갱신 INDEX**: `sdd/issues/{issue_id}/INDEX.md` (TASK 표 + 의존 그래프)

## 추가 규칙

- 해당 ISSUE가 없으면 즉시 stop + `sdd-issue` 권유.
- TASK는 PR 1개 단위 (논리적). 너무 크면 분리 권유.
- `depends_on`은 같은 ISSUE 내 TASK ID만 (다른 ISSUE TASK 인용 금지).
- `primary_kind` 명시: implementation / refactor / infra / chore.
- INDEX 갱신 시 의존 그래프(mermaid) 자동 재생성.

## 다음 단계 제안

TASK 추가 후:
- "TASK-XX 추가. PLAN 조립하시겠습니까? (`sdd-plan TASK-XX`) 또는 다른 TASK 추가?"
