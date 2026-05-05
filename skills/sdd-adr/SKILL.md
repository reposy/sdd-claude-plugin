---
name: sdd-adr
description: ADR을 작성한다. 결정과 검토된 대안·기각 사유를 기록. 사용자 발화 "결정 기록", "ADR 작성", "왜 이렇게 결정했는지 남기자" 또는 명시 호출 /sdd-adr에 트리거.
---

# sdd-adr

이 skill은 표준 동작 패턴(PLUGIN_SPEC §4)을 따른다.

## 변동 사항

- **읽을 INDEX**: `sdd/INDEX.md`, `sdd/adrs/INDEX.md`
- **참조 가이드**: `data/guides/ADR_GUIDE.md`
- **참조 스키마**: `data/schemas/ADR-XXX.md`
- **산출 위치**: `sdd/adrs/ADR-XXX.md` (XXX는 전역 3자리 순번)
- **갱신 INDEX**: `sdd/INDEX.md`, `sdd/adrs/INDEX.md`

## 추가 규칙

- ADR은 다른 문서 작성·수정 중 사용자가 결정을 내린 경우에만 작성. 결정 없는 ADR 만들지 않음.
- 검토된 대안 + 기각 사유 필수. 둘 중 하나라도 없으면 ADR 트리거 미달 → 사용자에게 짚어줌.
- `context_doc` 필드: 결정이 발생한 맥락 문서 (예: SPEC-auth-v1.2).
- 이전 ADR 갱신이라면 "이전 ADR 갱신" 섹션 명시. 이전 ADR 자체는 보존.
- 추론 금지. 사용자가 발화하지 않은 결정은 만들지 않음.
