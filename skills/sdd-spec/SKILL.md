---
name: sdd-spec
description: 도메인 SPEC을 깎는다. ROOT_SPEC 기반으로 한 도메인의 외부 계약·불변식·범위를 정의. 사용자 발화 "도메인 SPEC", "auth SPEC 깎자", "계약 정의", "불변식" 또는 명시 호출 /sdd-spec {domain}에 트리거.
---

# sdd-spec

이 skill은 표준 동작 패턴(PLUGIN_SPEC §4)을 따른다.

## 변동 사항

- **인수**: `{domain}` (예: auth, billing). 없으면 INDEX에서 후보 제시.
- **읽을 INDEX**: `sdd/INDEX.md`, `sdd/specs/INDEX.md`, `sdd/specs/{domain}/INDEX.md` (있으면)
- **참조 가이드**: `data/guides/SPEC_GUIDE.md`
- **참조 스키마**: `data/schemas/SPEC.md`
- **산출 위치**: `sdd/specs/{domain}/SPEC.md`
- **갱신 INDEX**: `sdd/INDEX.md`, `sdd/specs/INDEX.md`, `sdd/specs/{domain}/INDEX.md`

## 추가 규칙

- ROOT_SPEC이 없으면 즉시 stop + `sdd-root-spec` 권유.
- 한 SPEC = 한 도메인. 도메인을 넘는 내용은 SPEC을 분리하라고 짚음.
- 도메인 디렉터리가 없으면 생성 + `INDEX.md`도 함께 생성 (`data/schemas/specs_domain_INDEX.md` 베이스).
- SPEC frontmatter의 `summary` 필드 필수 (v1.1부터).
- 구현 디테일(라이브러리 이름, 코드 본문) 발견 시 즉시 짚어 외부 행동 차원으로 환원 요구.

## 다음 단계 제안

SPEC 완료 시:
- "SPEC-{domain} 완료. 다음 후보: ① USECASE 작성, ② EDGECASE 작성, ③ ISSUE 도출, ④ 다른 도메인 SPEC. 어느 쪽?"
