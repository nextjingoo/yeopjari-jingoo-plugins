# 플러그인배포

"옆자리 진구씨" 채널에서 다루는 회사 업무용과 일상에서 유용한 AI 지침을 Claude Code 플러그인으로 패키징해 배포하는 저장소다. GitHub public repo(`nextjingoo/yeopjari-jingoo-plugins`)로 push되어 있고, 메인 작업 폴더(`(0)ClaudeCode`)의 옵시디언 볼트와는 별개의 독립 git 저장소다.

사용자 설치 안내는 [UserGuide.md](UserGuide.md)에 있다 — 이 파일은 유지보수(구조·규칙·왜 이렇게 했는지) 전용이다.

# 구조

```
플러그인배포/
├── .claude-plugin/marketplace.json   ← 마켓플레이스 카탈로그
└── plugins/
    └── <plugin-name>/
        └── .claude-plugin/plugin.json ← 플러그인 개별 메타데이터
```

새 지침을 플러그인으로 추가할 때:
1. `plugins/` 아래 새 폴더 생성, 그 안에 `.claude-plugin/plugin.json` 작성 (name, displayName, version, description, author 필수)
2. `marketplace.json`의 `plugins` 배열에 항목 추가 (name, source, version, description)

# 버전 관리

`marketplace.json`의 plugins 항목에 `version` 필드가 있어서 **자동 실시간 반영이 아니다.** 내용을 수정하면 `plugin.json`과 `marketplace.json` 양쪽의 `version`을 같이 올리고 push해야 이미 설치한 사용자가 업데이트 대상으로 인식한다. (버전 필드를 아예 생략하면 git commit SHA로 자동 추적되어 실시간 반영되지만, 이 저장소는 의도적으로 버전 고정 방식을 택했다.)

# 알려진 버그: marketplace.json name 필드 한글 오탐

`claude plugin validate`가 `marketplace.json`의 최상위 `name` 필드에 비ASCII(한글) 문자가 있으면 실제 내용과 무관하게 "공식 Anthropic 마켓플레이스 사칭"으로 오탐한다. 그래서 `name`만 영문(`yeopjari-jingoo-plugins`)으로 고정했다. `owner.name`, `description`, 개별 플러그인 이름·설명은 한글이어도 문제없이 통과한다.

# 배포 절차

로컬에서 수정 후:
```
git add <파일>
git commit -m "..."
git push
```
커밋·push는 사용자가 명시적으로 요청할 때만 실행한다 (메인 프로젝트 CLAUDE.md와 동일한 원칙).
