---
id: PLAN-03
task_ref: TASK-03
date: 2026-05-04
status: draft
references: [SPEC-auth, UC-001, EC-001, ADR-002]
---

> 이 문서는 sdd-plan으로 자동 조립되었다. 직접 수정 금지.
> 사용자 검토는 frontmatter의 `status`를 `reviewed`로 변경하여 표시한다.

# PLAN-03 — Redis 세션 스토어 설정

## 1. 요약

TASK-03(Redis 세션 스토어 설정)의 구현 계획. Redis 클라이언트 추가, 연결 설정, 세션 저장·조회·만료 인터페이스 구현. SPEC-auth Contract §3(세션 관리)와 ADR-002(세션 저장소 Redis 채택)에 따른다.

## 2. TASK 인용

> Redis를 세션 스토어로 설정한다. 토큰 발급 시 세션 정보를 저장하고, 검증 시 조회, 만료 시 삭제할 수 있어야 한다. (TASK-03 본문에서)

## 3. 근거 추적

| ID | 종류 | 인용 사유 |
|---|---|---|
| SPEC-auth §3 | SPEC | 세션 관리 Contract — 저장·조회·만료 의무 정의 |
| UC-001 | USECASE | 정상 로그인 → 세션 저장 → 후속 요청 인증 흐름 |
| EC-001 | EDGECASE | 만료된 세션으로 요청 시 401 반환 |
| EC-002 | EDGECASE | Redis 연결 실패 시 fallback (메모리 저장) |
| ADR-002 | ADR | 세션 저장소로 Redis 채택 결정과 그 이유 |

## 4. 수정 대상 파일

| 경로 | 변경 종류 | 요약 |
|---|---|---|
| `src/auth/session/store.ts` | 신규 | `SessionStore` 인터페이스 정의 (set/get/delete) |
| `src/auth/session/redis-store.ts` | 신규 | Redis 구현체. ioredis 클라이언트 사용. TTL 옵션 포함. |
| `src/auth/session/memory-store.ts` | 신규 | 메모리 fallback 구현체 (EC-002 대응) |
| `src/auth/session/index.ts` | 신규 | 환경 설정에 따라 store 선택 export |
| `src/config/env.ts` | 수정 | REDIS_URL, SESSION_TTL 환경 변수 추가 |
| `tests/auth/session/redis-store.test.ts` | 신규 | UC-001, EC-001 시나리오 테스트 |
| `tests/auth/session/memory-store.test.ts` | 신규 | EC-002 시나리오 테스트 |

## 5. 부수 변경

### 의존성
- `ioredis@^5` 추가

### 환경 변수
- `REDIS_URL`: Redis 연결 문자열 (필수)
- `SESSION_TTL`: 세션 만료 시간(초). 기본 3600

### DB / 인프라
- Redis 인스턴스 필요. docker-compose.yml에 redis 서비스 추가.

## 6. 검증 방법

| 테스트 | 검증 대상 |
|---|---|
| `redis-store.test.ts: should set and get session` | UC-001 정상 흐름 |
| `redis-store.test.ts: should expire session after TTL` | EC-001 만료 처리 |
| `memory-store.test.ts: should fallback when Redis unavailable` | EC-002 fallback |
| 통합 테스트 | TASK-04(만료 처리), TASK-05(통합 테스트)의 입력 |

수동 검증: Redis docker 컨테이너 띄우고 로컬 환경에서 로그인→세션 조회→만료 흐름 1회 확인.

## 7. 추적 범위

**본 문서**:
- SPEC-auth (전체)
- ISSUE-0001 본문 + TASK-03 본문
- UC-001, EC-001, EC-002
- ADR-002

**안 본 것**:
- TASK-01, TASK-02, TASK-04, TASK-05 본문 (다른 TASK는 PLAN 범위 밖)
- SPEC-billing 등 다른 도메인
- ADR-001, ADR-003 (auth 도메인 무관)

## 8. 위험·열린 질문

### 위험
- Redis 연결 실패 시 fallback이 EC-002에 정의되어 있으나, 운영 환경에서도 fallback 허용할지 미정. 일단 환경 변수로 토글 가능하게 구현.

### 열린 질문
- 세션 키 prefix 규칙 (예: `session:user:{id}`)이 SPEC에 명시되지 않음. 관례적으로 `session:{token}` 사용. SPEC 갱신 또는 ADR 신규 필요할 수 있음.
