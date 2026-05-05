---
name: sdd-edgecase
description: EDGECASE를 작성한다. SPEC의 계약이 정상 흐름을 벗어나는 상황과 기대 동작을 기록. 사용자 발화 "엣지케이스", "실패 경로", "예외 처리" 또는 명시 호출 /sdd-edgecase {domain}에 트리거.
---

# sdd-edgecase

이 skill은 표준 동작 패턴(PLUGIN_SPEC §4)을 따른다.

## 변동 사항

- **인수**: `{domain}` (예: auth). 없으면 INDEX에서 후보 제시.
- **읽을 INDEX**: `sdd/specs/{domain}/INDEX.md`, `sdd/specs/{domain}/edgecases/INDEX.md` (있으면)
- **참조 가이드**: `data/guides/EDGECASE_GUIDE.md`
- **참조 스키마**: `data/schemas/EC-XXX.md`
- **산출 위치**: `sdd/specs/{domain}/edgecases/EC-XXX.md`
- **갱신 INDEX**: `sdd/specs/{domain}/INDEX.md`, `sdd/specs/{domain}/edgecases/INDEX.md`

## 추가 규칙

- 해당 도메인 SPEC이 없으면 즉시 stop + `sdd-spec {domain}` 권유.
- edgecases/ 디렉터리 없으면 생성 + `INDEX.md` 함께 생성 (`data/schemas/edgecases_INDEX.md` 베이스).
- EC 두께 = 본질 결정론성. 부족하다 싶으면 적극 추가 권유.
- 한 EC = 한 실패 경로. 여러 실패를 묶지 않음.
