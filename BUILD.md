# Build Notes

이 문서는 plugin을 GitHub repo에 푸시·배포하기 전 확인 사항이다.

## 0. 디렉터리 구조

이 repo는 **single-plugin marketplace** 패턴이다 — Claude Code가 인식하는 marketplace 자체이면서, 그 안에 plugin 하나(`sdd`)를 담는다.

```
.
├── .claude-plugin/
│   └── marketplace.json     # marketplace 카탈로그
├── plugins/
│   └── sdd/                 # plugin 실체
│       ├── .claude-plugin/
│       │   └── plugin.json
│       ├── skills/
│       ├── agents/
│       └── data/
│           ├── guides/
│           └── schemas/
├── README.md
└── BUILD.md
```

`marketplace.json`의 plugin source는 `"./plugins/sdd"` (상대 경로 문자열). github/url object source는 Claude Code 내부에서 SSH-protocol clone을 트리거해 사용자 환경에 따라 host key 검증 실패를 일으키므로 사용하지 않는다.

## 1. 새 repo로 publish 시 채울 placeholder

- `plugins/sdd/.claude-plugin/plugin.json`:
  - `author.name`, `author.email`
  - `repository`
- `.claude-plugin/marketplace.json`:
  - `owner.name`
- `README.md`:
  - 설치 섹션의 GitHub URL과 절대 경로 예시

## 2. SDD 방법론 패키지 동기화

이 plugin은 **SDD 방법론 패키지 v1.2** 기반.

`plugins/sdd/data/guides/`와 `plugins/sdd/data/schemas/`가 v1.2 패키지의 `guides/`와 `schemas/` 디렉터리와 1:1 동일해야 한다.

새 SDD 패키지 버전이 출시되면 동기화 절차:

```bash
# 예시
PKG_VERSION=1.3
wget https://github.com/<owner>/sdd-methodology/releases/download/v$PKG_VERSION/sdd-methodology-v$PKG_VERSION.zip
unzip sdd-methodology-v$PKG_VERSION.zip
rm -rf plugins/sdd/data/guides plugins/sdd/data/schemas
cp -r sdd-methodology/guides plugins/sdd/data/
cp -r sdd-methodology/schemas plugins/sdd/data/
# README 첫 줄 갱신: "이 plugin은 SDD 방법론 패키지 v$PKG_VERSION을 기반으로 합니다."
```

## 3. GitHub 푸시 전 검증

PLUGIN_SPEC.md §8(검증 방법) A·B·C·D를 참조.

### A. 빌드 검증 (정적)

```bash
# 디렉터리 구조 확인
test -f .claude-plugin/marketplace.json
test -f plugins/sdd/.claude-plugin/plugin.json
test -d plugins/sdd/skills && [ $(ls plugins/sdd/skills | wc -l) -eq 13 ]
test -d plugins/sdd/agents && [ $(ls plugins/sdd/agents | wc -l) -eq 4 ]
test -d plugins/sdd/data/guides && [ $(ls plugins/sdd/data/guides | wc -l) -eq 8 ]
test -d plugins/sdd/data/schemas && [ $(ls plugins/sdd/data/schemas | wc -l) -eq 16 ]

# JSON 유효성
python3 -m json.tool < .claude-plugin/marketplace.json > /dev/null
python3 -m json.tool < plugins/sdd/.claude-plugin/plugin.json > /dev/null

# SKILL.md frontmatter 존재
for f in plugins/sdd/skills/*/SKILL.md; do head -1 $f | grep -q '^---' || echo "FAIL: $f"; done
```

### B. Claude Code 설치 검증

```bash
# 사용자 환경에서 (HTTPS clone, 그 후 로컬 marketplace 등록)
git clone https://github.com/<owner>/sdd-claude-plugin.git
# Claude Code 안에서:
#   /plugin marketplace add /절대/경로/sdd-claude-plugin
#   /plugin install sdd@sdd-plugins
#   /reload-plugins   → "Loaded 1 plugins, 13 skills, ..." 라인 확인
```

### C. Smoke test

PLUGIN_SPEC.md §8 C 표 참조.

## 4. 버전 정책

- **patch** (0.1.x): plugin 자체 버그 수정, README·BUILD 갱신
- **minor** (0.x.0): skill 추가·변경·SKILL.md 수정
- **major** (x.0.0): 디렉터리 구조 변경, 비호환 API 변경

SDD 패키지 버전이 올라가도 plugin 자체에 큰 변화 없으면 minor.
