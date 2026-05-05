---
name: sdd-usecase
description: USECASE를 작성한다. SPEC의 정상 흐름 시나리오를 정의. 사용자 발화 "유스케이스", "성공 시나리오", "정상 흐름" 또는 명시 호출 /sdd-usecase {domain}에 트리거.
---

# sdd-usecase

이 skill은 표준 동작 패턴(PLUGIN_SPEC §4)을 따른다.

## 변동 사항

- **인수**: `{domain}` (예: auth). 없으면 INDEX에서 후보 제시.
- **읽을 INDEX**: `sdd/specs/{domain}/INDEX.md`, `sdd/specs/{domain}/usecases/INDEX.md` (있으면)
- **참조 가이드**: `data/guides/USECASE_GUIDE.md`
- **참조 스키마**: `data/schemas/UC-XXX.md`
- **산출 위치**: `sdd/specs/{domain}/usecases/UC-XXX.md` (XXX는 도메인 내 순번)
- **갱신 INDEX**: `sdd/specs/{domain}/INDEX.md`, `sdd/specs/{domain}/usecases/INDEX.md`

## 추가 규칙

- 해당 도메인 SPEC이 없으면 즉시 stop + `sdd-spec {domain}` 권유.
- usecases/ 디렉터리 없으면 생성 + `INDEX.md` 함께 생성 (`data/schemas/usecases_INDEX.md` 베이스).
- UC ID는 도메인 내 순번 (UC-001, UC-002 ...).
- 한 UC = 한 시나리오. 분기·예외는 EDGECASE로.
