# Build Notes

이 문서는 plugin을 GitHub repo에 푸시·배포하기 전 확인 사항이다.

## 1. 사용자 채울 placeholder

- `.claude-plugin/plugin.json`:
  - `author.name`, `author.email`
  - `repository`
- `README.md`:
  - 설치 섹션의 `<owner>` placeholder

## 2. SDD 방법론 패키지 동기화

이 plugin은 **SDD 방법론 패키지 v1.2** 기반.

`data/guides/`와 `data/schemas/`가 v1.2 패키지의 `guides/`와 `schemas/` 디렉터리와 1:1 동일해야 한다.

새 SDD 패키지 버전이 출시되면 동기화 절차:

```bash
# 예시
PKG_VERSION=1.3
wget https://github.com/<owner>/sdd-methodology/releases/download/v$PKG_VERSION/sdd-methodology-v$PKG_VERSION.zip
unzip sdd-methodology-v$PKG_VERSION.zip
rm -rf data/guides data/schemas
cp -r sdd-methodology/guides data/
cp -r sdd-methodology/schemas data/
# README 첫 줄 갱신: "이 plugin은 SDD 방법론 패키지 v$PKG_VERSION을 기반으로 합니다."
```

## 3. GitHub 푸시 전 검증

PLUGIN_SPEC.md §8(검증 방법) A·B·C·D를 참조.

### A. 빌드 검증 (정적)

```bash
# 디렉터리 구조 확인
test -f .claude-plugin/plugin.json
test -d skills && [ $(ls skills | wc -l) -eq 13 ]
test -d agents && [ $(ls agents | wc -l) -eq 4 ]
test -d data/guides && [ $(ls data/guides | wc -l) -eq 8 ]
test -d data/schemas && [ $(ls data/schemas | wc -l) -eq 16 ]

# JSON 유효성
cat .claude-plugin/plugin.json | python3 -m json.tool > /dev/null

# SKILL.md frontmatter 존재
for f in skills/*/SKILL.md; do head -1 $f | grep -q '^---' || echo "FAIL: $f"; done
```

### B. Claude Code 설치 검증

```bash
# Claude Code에서
/plugin install github:<owner>/sdd-claude-plugin
/skills | grep sdd-     # 13개 sdd-* 표시 확인
```

### C. Smoke test

PLUGIN_SPEC.md §8 C 표 참조.

## 4. 버전 정책

- **patch** (0.1.x): plugin 자체 버그 수정, README·BUILD 갱신
- **minor** (0.x.0): skill 추가·변경·SKILL.md 수정
- **major** (x.0.0): 디렉터리 구조 변경, 비호환 API 변경

SDD 패키지 버전이 올라가도 plugin 자체에 큰 변화 없으면 minor.
