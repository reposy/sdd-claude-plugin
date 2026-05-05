---
name: sdd-help
description: SDD 가이드 또는 스키마 문서를 즉시 표시한다. 사용자 발화 "도움말", "가이드 보기", "ROOT_SPEC_GUIDE 보여줘" 또는 명시 호출 /sdd-help {문서명}에 트리거.
---

# sdd-help

가이드·스키마 빠른 참조 skill.

## 동작

1. 인수 받음:
   - 가이드 이름 (예: `ROOT_SPEC_GUIDE`, `SPEC_GUIDE`, `PLAN_GUIDE` 등 8개)
   - 스키마 이름 (예: `ROOT_SPEC`, `SPEC`, `PLAN-XX` 등 16개)
   - `all` → 사용 가능한 모든 문서 목록 표시
   - 없음 → 사용법 안내 + 목록
2. 인수 매칭:
   - `data/guides/{이름}.md` 또는 `data/guides/{이름}_GUIDE.md` 시도
   - `data/schemas/{이름}.md` 시도
   - 매칭 실패 시 후보 제시
3. 매칭된 파일 내용을 메인 대화에 표시.

## 사용 가능한 문서

### 가이드 (8개)
ROOT_SPEC_GUIDE, SPEC_GUIDE, USECASE_GUIDE, EDGECASE_GUIDE, ISSUE_GUIDE, TASK_GUIDE, ADR_GUIDE, PLAN_GUIDE

### 스키마 (본문, 8개)
ROOT_SPEC, SPEC, UC-XXX, EC-XXX, ISSUE, TASK-XX, ADR-XXX, PLAN-XX

### 스키마 (INDEX, 8개)
INDEX, specs_INDEX, specs_domain_INDEX, usecases_INDEX, edgecases_INDEX, issues_INDEX, issues_ISSUE_INDEX, adrs_INDEX

## 약속

- 산출물 파일 변경 없음 (읽기 전용).
- 메인에서 직접 처리 (서브에이전트 불필요).
