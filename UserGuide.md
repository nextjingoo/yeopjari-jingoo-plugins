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

## 업데이트 방법

플러그인 내용이 개정되면 버전이 올라갑니다. 이미 설치한 플러그인은 아래 방법으로 최신 버전을 받을 수 있습니다.

### 터미널 (CLI)

```
claude plugin marketplace update yeopjari-jingoo-plugins
claude plugin install <플러그인 이름>@yeopjari-jingoo-plugins
```

### VSCode 확장

1. `Ctrl+Shift+P` → `Claude: Plugin marketplace add` 실행 → `nextjingoo/yeopjari-jingoo-plugins`를 다시 입력해 마켓플레이스 정보를 새로고침
2. `Ctrl+Shift+P` → `Claude: Apply plugin changes`로 적용

### 데스크톱 앱

1. 채팅창 프롬프트 박스 옆 **+** 버튼 → **플러그인** → **플러그인 탐색** 클릭
2. 뜬 창에서 **코드** 탭 선택 → `yeopjari-jingoo-plugins` 마켓플레이스 옆 **···** 클릭 → **업데이트 확인** 클릭
3. 업데이트가 있으면 플러그인 이름 오른쪽에 주황색 점(●)이 표시됩니다. 톱니바퀴(**관리**) 아이콘 클릭
4. 플러그인 상세 화면에서 파란색으로 활성화된 **업데이트** 버튼 클릭
5. 버전 번호가 올라가고 화면 아래에 "1.0.1에서 1.0.2로 업데이트되었습니다" 같은 알림이 뜨면 완료

**주황색 점이 뜨지 않거나 업데이트 버튼이 회색으로 비활성화돼 있으면** 최신 버전이 아직 반영되지 않은 것입니다. 이때는 삭제 후 재설치합니다.
1. 플러그인 상세 화면 우측 상단 **⋮** 메뉴에서 제거
2. 위 [설치 방법 · 데스크톱 앱](#데스크톱-앱) 절차를 그대로 다시 진행

## 구조

```
플러그인배포/
├── .claude-plugin/marketplace.json   ← 마켓플레이스 카탈로그
├── updatelog/                        ← 플러그인별 업데이트 로그 (버전별 변경 내용)
└── plugins/
    └── summary-report-writer/        ← 플러그인 하나당 폴더 하나
        └── introduction/             ← 플러그인 소개 문서 (설치 전 미리보기용)
```

각 플러그인이 무엇을 하는지 짧게 보고 싶다면 `plugins/<플러그인 이름>/introduction/` 안의 소개 문서를 먼저 읽어보세요. 무엇이 바뀌었는지는 `updatelog/<플러그인 이름>_log.md`에서 확인할 수 있습니다.

유지보수 시 지켜야 할 세부 규칙은 [CLAUDE.md](CLAUDE.md)를 참고합니다.
