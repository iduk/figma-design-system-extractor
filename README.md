# figma-design-system-extractor

Figma Dev Mode URL 하나를 던지면 **디자인 시스템 전체를 `.md` 문서로 자동 추출**하는 Claude Code 스킬.

## 🎯 두 가지 산출물

| 산출물 | 설명 |
|---|---|
| `DESIGN-SYSTEM-SNAPSHOT.md` | 색상/타이포/spacing/컴포넌트 현황 덤프 |
| `DESIGN-SYSTEM-CODE-RULES.md` | CSS변수/JS토큰/Tailwind 매핑 포함 개발 규칙 |

## ⚡ 5분 설치 가이드

### 1단계: Figma Token 발급
```bash
# 1. https://www.figma.com/settings 접속
# 2. Personal access tokens → Generate new token
# 3. 터미널에서:
export FIGMA_TOKEN=figd_xxxxxxxxxxxxxxxx
echo 'export FIGMA_TOKEN=figd_xxxx' >> ~/.zshrc  # 영구 설정
```

### 2단계: 스킬 설치
```bash
mkdir -p .claude/skills/figma-design-system/{scripts,templates,prompts}
# 위 파일들을 각 경로에 저장
chmod +x .claude/skills/figma-design-system/scripts/*.sh
cd .claude/skills/figma-design-system && npm install
```

### 3단계: 실행
**Claude Code에서 (권장):**
```
https://www.figma.com/design/AbCdEfGhIj/MyProject?m=dev
```

**터미널에서:**
```bash
bash .claude/skills/figma-design-system/scripts/extract-figma.sh \
  "https://www.figma.com/design/FILE_KEY/PROJECT?m=dev" \
  "design-system/raw"
```

## 📂 디렉터리 구조

```
.claude/skills/figma-design-system/
├── CLAUDE.md                   ← Claude 스킬 진입점
├── README.md
├── package.json
├── scripts/
│   ├── extract-figma.sh        ← Figma API → JSON
│   ├── parse-tokens.js         ← JSON → 토큰 정규화
│   ├── map-to-code.js          ← 토큰 → CSS/JS/Tailwind
│   └── generate-md.js          ← 최종 MD 생성
├── templates/
│   └── design-system.md.hbs
└── prompts/
    ├── analyze-figma.md
    └── code-mapping.md
```

## ⚠️ 주의사항

- Figma Variables API는 **Professional 플랜 이상** 필요
- Dev Resources는 Dev Mode 활성화된 파일만 조회 가능
- Node.js 18+ 필요 (`brew install node`)

## 📝 라이선스

MIT — 자유롭게 수정/배포하세요.

---

**전체 파일 내용은 [Releases](https://github.com/iduk/figma-design-system-extractor/releases) 에서 다운로드하세요.**
