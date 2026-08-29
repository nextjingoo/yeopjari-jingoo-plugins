# 플러그인배포

"옆자리 진구씨"가 배포하는 회사 업무용과 일상에서 유용한 AI 지침 Claude Code 플러그인 모음입니다.

저장소: https://github.com/nextjingoo/yeopjari-jingoo-plugins

플러그인 목록은 [PluginList.md](PluginList.md)를 참고하세요.

## 플러그인이란?

Claude Code 플러그인은 명령어(슬래시 커맨드)·에이전트·스킬 같은 AI 지침을 하나로 묶어 배포하는 패키지입니다. 마켓플레이스에 등록된 플러그인을 설치하면 별도 설정 없이 바로 그 지침을 대화에서 불러 쓸 수 있습니다. 이 저장소는 "옆자리 진구씨" 채널에서 만든 지침들을 플러그인 형태로 모아 배포합니다.

이 가이드는 Claude Code를 쓰는 3가지 환경 — **터미널(CLI)**, **VSCode 확장**, **데스크톱 앱** — 각각에서 플러그인을 설치하는 방법을 안내합니다. 본인이 사용하는 환경에 해당하는 항목만 따라 하면 됩니다.

## 설치 방법

먼저 마켓플레이스를 한 번 등록하면, 이후로는 원하는 플러그인 이름만 바꿔가며 계속 설치할 수 있습니다.

### 터미널 (CLI)

```
claude plugin marketplace add nextjingoo/yeopjari-jingoo-plugins
claude plugin install <플러그인 이름>
```

### VSCode 확장

1. `Ctrl+Shift+P` → `Claude: Plugin marketplace add` 실행 → `nextjingoo/yeopjari-jingoo-plugins` 입력
2. `Ctrl+Shift+P` → `Claude: Plugin marketplace list`에서 원하는 플러그인 설치
   (설치 범위 User/Project는 실행 중 대화형으로 선택)
3. `Ctrl+Shift+P` → `Claude: Apply plugin changes`로 재시작 없이 적용

### 데스크톱 앱

1. 채팅창 프롬프트 박스 옆 **+** 버튼 → **Plugins**
2. **Manage plugins** → **Marketplaces** 탭 → 마켓플레이스 추가 → `nextjingoo/yeopjari-jingoo-plugins` 입력
3. **Add plugin**으로 돌아가 목록에서 원하는 플러그인 선택 → 설치
4. 설치 범위 선택: User(모든 프로젝트) / Project(팀 공유) / Local(이 폴더만)

설치 후 "Run /reload-plugins to activate."가 뜨면 `/reload-plugins`를 한 번 더 실행합니다.

## 구조

```
플러그인배포/
├── .claude-plugin/marketplace.json   ← 마켓플레이스 카탈로그
└── plugins/
    └── summary-report-writer/        ← 플러그인 하나당 폴더 하나
```

새 지침을 추가할 땐 `plugins/` 아래에 폴더를 하나 만들고 `marketplace.json`의 `plugins` 배열에 항목을 추가합니다. 유지보수 시 지켜야 할 세부 규칙은 [CLAUDE.md](CLAUDE.md)를 참고합니다.
