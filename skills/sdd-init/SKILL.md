---
name: sdd-init
description: SDD 디렉터리를 부트스트랩한다. sdd/ 폴더 + 5개 빈 INDEX + frontmatter 채워진 빈 ROOT_SPEC을 생성한다. 사용자 발화 "SDD 시작", "프로젝트 부트스트랩", "sdd 셋업" 또는 명시 호출 /sdd-init에 트리거. 인수로 파일 경로(./requirements.md) 또는 자유 prompt를 받을 수 있다.
---

# sdd-init

SDD 디렉터리 부트스트랩. 본격 깎기는 `sdd-root-spec`에 위임.

## 동작

1. **현재 위치 확인**. `sdd/` 디렉터리가 이미 존재하면 사용자에게 보고: "sdd/ 이미 존재. 덮어쓰지 않습니다. `sdd-status`로 현재 상태 확인하시거나, `sdd-root-spec`으로 이어가세요." → 종료.

2. **사용자 확인**. "SDD 디렉터리를 만들겠습니다. 위치: `<현재 프로젝트 루트>/sdd/`. 진행할까요?"

3. **인수 분기**:
   - 인수 없음 → 부트스트랩만 진행
   - 인수가 파일 경로(확장자 포함, `./` 또는 `/` 시작) → 파일 읽음 → ROOT_SPEC 1단계 입력 자료로 활용
   - 인수가 자유 prompt → 그대로 1단계 입력 자료로 활용

4. **디렉터리·파일 생성** (모두 frontmatter 채움, 본문은 빈 표 또는 빈 섹션 헤더):
   - `sdd/`
   - `sdd/INDEX.md` ← `data/schemas/INDEX.md` 베이스
   - `sdd/ROOT_SPEC.md` ← `data/schemas/ROOT_SPEC.md` 베이스 (빈 섹션 헤더)
   - `sdd/specs/`
   - `sdd/specs/INDEX.md` ← `data/schemas/specs_INDEX.md` 베이스
   - `sdd/issues/`
   - `sdd/issues/INDEX.md` ← `data/schemas/issues_INDEX.md` 베이스
   - `sdd/adrs/`
   - `sdd/adrs/INDEX.md` ← `data/schemas/adrs_INDEX.md` 베이스

   도메인별 디렉터리(`sdd/specs/{domain}/`)와 이슈별 디렉터리는 만들지 않음. 해당 깎기 skill이 첫 호출될 때 생성.

5. **frontmatter 값**:
   - 모든 INDEX: `id`, `version: 0.1`, `last_updated: <오늘>`
   - ROOT_SPEC: `id: ROOT_SPEC`, `version: 0.1`, `status: draft`, `date: <오늘>`

6. **완료 보고 + 다음 단계 제안**:
   - 인수 없음 → "디렉터리 + 빈 INDEX 5개 + 빈 ROOT_SPEC 생성 완료. ROOT_SPEC을 깎으시겠습니까? (`sdd-root-spec`)"
   - 인수 있음 → "생성 완료. ROOT_SPEC 1단계(문제 정의)를 입력 자료와 함께 시작합니다." → `sdd-root-spec` 트리거 (또는 권유)

## 참조 자원

- `data/schemas/INDEX.md`
- `data/schemas/ROOT_SPEC.md`
- `data/schemas/specs_INDEX.md`
- `data/schemas/issues_INDEX.md`
- `data/schemas/adrs_INDEX.md`

## 빈틈 패턴

- 사용자 프로젝트가 git repo인지 확인하지 않음 (사용자 책임)
- `sdd/` 외 디렉터리에 영향 주지 않음
- 기존 `sdd/`가 있으면 절대 덮어쓰지 않음 (안전 우선)
