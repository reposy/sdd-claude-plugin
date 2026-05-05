# {프로젝트명}

> 이 문서는 자동 생성된다. 수동 편집 금지.
> 마지막 갱신: YYYY-MM-DD HH:MM

## 개요
{ROOT_SPEC.md의 "1. 한 문장 요약"을 그대로 가져옴}

## 핵심 문서
- [ROOT_SPEC](./ROOT_SPEC.md) — 왜, 누구를 위해, 무엇을
- [DECISION_GUIDE](./DECISION_GUIDE.md) — 사람 판단이 필요한 지점의 규칙
- [BACKLOG](./BACKLOG.md) — 다음 작업 후보

## 카탈로그
- [SPEC 목록](./specs/INDEX.md)
- [ISSUE 목록](./issues/INDEX.md)
- [ADR 목록](./adrs/INDEX.md)

---

## 생성 규칙

- **개요**: ROOT_SPEC.md의 "1. 한 문장 요약" 섹션 본문을 그대로 복사.
- **핵심 문서**: ROOT_SPEC.md, DECISION_GUIDE.md, BACKLOG.md 존재 여부 확인 후 링크. 없으면 행 생략.
- **카탈로그**: 하위 디렉터리(specs/, issues/, adrs/)의 INDEX.md 진입점. 디렉터리 없으면 행 생략.
- **그래프 없음**: SPEC 의존 그래프는 specs/INDEX.md 책임.
- **카운트·진척 없음**: 각 카탈로그의 양적 정보와 진행 상태는 해당 INDEX 책임. ROOT는 진입점만.
- **마지막 갱신**: 생성기 실행 시각.
