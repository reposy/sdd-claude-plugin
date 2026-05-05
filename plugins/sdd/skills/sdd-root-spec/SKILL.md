---
name: sdd-root-spec
description: ROOT_SPEC을 깎는다. 프로젝트의 "왜 만드는가, 누구를 위해, 무엇을"을 정의하는 최상위 문서. 사용자 발화 "프로젝트 비전", "ROOT_SPEC", "왜·누구·무엇 정리", "비전 정의" 또는 명시 호출 /sdd-root-spec에 트리거.
---

# sdd-root-spec

이 skill은 표준 동작 패턴(PLUGIN_SPEC §4)을 따른다.

## 변동 사항

- **읽을 INDEX**: `sdd/INDEX.md`
- **참조 가이드**: `data/guides/ROOT_SPEC_GUIDE.md`
- **참조 스키마**: `data/schemas/ROOT_SPEC.md`
- **산출 위치**: `sdd/ROOT_SPEC.md`
- **갱신 INDEX**: `sdd/INDEX.md`

## 추가 규칙

- ROOT_SPEC은 프로젝트당 1개. 이미 완료 상태면 새로 깎지 않고 수정 흐름 권유.
- 6단계 게이트(문제 정의 → 페르소나 → 가치 제안 → 제품 비전 → 범위 명확화 → 위험·열린 질문) 강제. 단계 건너뛰기 금지.
- 단계별 통과 기준은 ROOT_SPEC_GUIDE의 각 단계 통과 기준 그대로.
- `sdd/` 디렉터리가 없으면 즉시 stop + `sdd-init` 권유.

## 다음 단계 제안 (7단계)

ROOT_SPEC 완료 시:
- "검증 통과. 이어서 SPEC을 깎으시겠습니까? ROOT_SPEC에서 식별 가능한 도메인 후보: [INDEX 갱신 시 추출]. 어느 것부터?"
- 사용자 응답에 따라 `sdd-spec` 트리거.
