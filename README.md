# SDD Plugin for Claude Code

> 이 plugin v0.1.0은 SDD 방법론 패키지 v1.2를 기반으로 합니다.

Spec-Driven Development(SDD) 방법론을 Claude Code에서 자동 적용하기 위한 plugin입니다. 사용자는 스펙을 깎고, LLM은 묻고 문서화하며, 코드는 스펙의 번역물이 됩니다.

## 핵심 원칙

- **사람은 스펙을 깎고, 구현은 LLM이 한다.**
- **코드는 스펙의 번역물이다.**
- **모든 작업·결정·코드는 스펙을 진실의 원천으로 삼아 진행된다.**

## 설치

```bash
# Claude Code에서
/plugin
# → marketplace 추가 → sdd 검색 → install
```

또는 GitHub에서 직접:

```bash
/plugin install github:reposy/sdd-claude-plugin
```

## 빠른 시작

```bash
# 1. SDD 디렉터리 부트스트랩
/sdd-init

# 또는 요구사항 파일과 함께
/sdd-init ./requirements.md

# 또는 자유 prompt로
/sdd-init "5~15인 팀 매니저용 회고 도구 만들고 싶어"

# 2. ROOT_SPEC 깎기
/sdd-root-spec

# 3. 진행 상태 확인
/sdd-status

# 4. 다음에 뭘 할지 추천 받기
/sdd-next

# 5. 도움말
/sdd-help ROOT_SPEC_GUIDE
```

## skill 목록 (13개)

### 깎기 skill (7개)

| 명령 | 용도 |
|---|---|
| `/sdd-root-spec` | 프로젝트 비전(ROOT_SPEC) 깎기 |
| `/sdd-spec {domain}` | 도메인 SPEC 깎기 |
| `/sdd-usecase {domain}` | 정상 흐름 시나리오(USECASE) 작성 |
| `/sdd-edgecase {domain}` | 실패 경로(EDGECASE) 작성 |
| `/sdd-issue {spec_id}` | SPEC 기반 이슈 도출 |
| `/sdd-task {issue_id}` | 이슈 기반 PR 단위 작업 분해 |
| `/sdd-adr` | 결정 기록(ADR) |

### 조립 skill (1개)

| 명령 | 용도 |
|---|---|
| `/sdd-plan {task_id}` | TASK + 관련 문서 자동 조립 → 구현 계획(PLAN) 생성 |

### 운영 skill (5개)

| 명령 | 용도 |
|---|---|
| `/sdd-init [filePath\|prompt]` | SDD 디렉터리 부트스트랩 |
| `/sdd-status` | 현재 진행 상태 보고 |
| `/sdd-next` | 다음 권장 작업 추천 |
| `/sdd-validate` | 산출물 검증 (가이드 체크리스트 일괄 적용) |
| `/sdd-help {문서명}` | 가이드/스키마 즉시 표시 |

## 디렉터리 구조 (사용자 프로젝트)

```
project/
├── src/
├── tests/
└── sdd/                    # plugin이 만들고 갱신
    ├── INDEX.md
    ├── ROOT_SPEC.md
    ├── specs/
    │   └── {domain}/
    │       ├── SPEC.md
    │       ├── usecases/
    │       └── edgecases/
    ├── issues/
    │   └── ISSUE-XXXX/
    │       ├── ISSUE.md
    │       ├── TASK-XX.md
    │       └── PLAN-XX.md
    └── adrs/
        └── ADR-XXX.md
```

## 동작 방식

1. **자동 트리거**: 사용자 자연어 발화에 적절한 skill이 자동 활성화
2. **상태 인식**: 모든 깎기 skill이 시작 시 INDEX 점검 → 어디까지 진행됐는지 파악
3. **능동 제안**: 단계 완료 시 LLM이 다음 단계를 제안 (사용자가 결정자)
4. **세션 안전성**: INDEX가 진실의 원천이라 LLM 메모리 초기화돼도 정확히 복원

## 본질이 더 궁금하다면

`data/guides/` 디렉터리에 SDD 방법론의 모든 가이드가 들어 있습니다. `/sdd-help all` 또는 `/sdd-help ROOT_SPEC_GUIDE` 등으로 직접 확인 가능합니다.

## 라이선스

MIT
