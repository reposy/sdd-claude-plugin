---
name: sdd-plan
description: PLAN을 자동 조립한다. TASK + 관련 SPEC/USECASE/EDGECASE/ADR을 자동 추적하여 구현 계획을 만든다. 사용자 발화 "PLAN 짜자", "구현 계획", "이 task 어떻게 구현" 또는 명시 호출 /sdd-plan {task_id}에 트리거.
---

# sdd-plan

조립 skill. 무거운 추적·조립은 서브에이전트에 위임.

## 동작

1. `sdd/` 디렉터리 + 인수 처리:
   - `{task_id}` (예: TASK-03) → 곧장 PLAN 조립
   - `{prompt}` (자유 문장) → 키워드 추출 → INDEX에서 관련 TASK 후보 제시 → 사용자 확인 → PLAN 조립
   - 없음 → INDEX 점검 → 진행 중 TASK 추천
2. **`agents/sdd-plan-agent.md` 서브에이전트 호출**. TASK ID와 사용자 컨텍스트 전달.
3. 서브에이전트가 TASK + 관련 모든 문서(SPEC/USECASE/EDGECASE/ADR) 자동 추적 → PLAN 조립.
4. 사용자 검토 요청. 승인 시 frontmatter `status: reviewed`로 변경.

## 변동 사항

- **참조 가이드**: `data/guides/PLAN_GUIDE.md`
- **참조 스키마**: `data/schemas/PLAN-XX.md`
- **산출 위치**: `sdd/issues/{issue_id}/PLAN-XX.md` (XX는 대응 TASK 번호와 일치)
- **갱신 INDEX**: `sdd/issues/{issue_id}/INDEX.md` (PLAN 표)

## 약속

- 한 PLAN = 한 TASK. 여러 묶음 금지.
- PLAN은 자동 조립. 사용자가 한 줄씩 깎지 않음. 사용자는 검토자.
- 수정 대신 재조립. 부분 수정 금지.
- `executed` 상태가 된 PLAN은 변경하지 않음 (이력 보존).
