# 플러그인배포

"옆자리 진구씨" 채널에서 다루는 회사 업무용과 일상에서 유용한 AI 지침을 Claude Code 플러그인으로 패키징해 배포하는 저장소다. GitHub public repo(`nextjingoo/yeopjari-jingoo-plugins`)로 push되어 있고, 메인 작업 폴더(`(0)ClaudeCode`)의 옵시디언 볼트와는 별개의 독립 git 저장소다.

사용자 설치 안내는 [UserGuide.md](UserGuide.md)에 있다 — 이 파일은 유지보수(구조·규칙·왜 이렇게 했는지) 전용이다.

# 구조

```
플러그인배포/
├── .claude-plugin/marketplace.json          ← 마켓플레이스 카탈로그
├── updatelog/
│   └── <plugin-name>_log.md                 ← 플러그인별 사용자 공지용 업데이트 로그 (버전별 누적)
└── plugins/
    └── <plugin-name>/
        ├── .claude-plugin/plugin.json       ← 플러그인 개별 메타데이터
        ├── skills/<plugin-name>/SKILL.md    ← 실행 절차 본문
        ├── agents/<agent-name>.md           ← 컴패니언 서브에이전트 (있는 경우)
        └── introduction/<plugin-name>_intro.md ← 사용자 대상 소개 문서 (목적·주요 기능·기능 흐름·결과물·이점)
```

`skills/`·`agents/`는 Claude Code 플러그인 스펙이 자동 스캔하는 예약 폴더고, `introduction/`은 스펙에 없는 임의 폴더라 무시된 채로 함께 배포된다(설치·검증에 영향 없음).

## 원본과의 관계

이 저장소의 플러그인은 손으로 새로 쓰지 않는다. 원본은 메인 작업 폴더(`(0)ClaudeCode`)의 `5-지침만들기/`에 있고, 그 프로젝트의 `guideline-plugin-deployer` 서브에이전트(`.claude/agents/지침만들기/`)가 원본을 분석해 이 저장소에 패키징한다. **원본 = 패키징 형태** 원칙에 따라 배포 과정에서 드러난 문제(환경 설명, 누락된 안내 등)는 이 저장소의 파일이 아니라 원본 표준지침에 먼저 반영되고, 그 결과가 여기로 그대로 옮겨진다.

새 지침을 플러그인으로 추가하거나 기존 지침을 갱신할 땐 위 서브에이전트를 통해 진행하는 것이 기본이다. 그 에이전트가 만드는 산출물은 다음과 같다:
1. `plugins/<plugin-name>/.claude-plugin/plugin.json` (name, displayName, version, description, author)
2. `plugins/<plugin-name>/skills/<plugin-name>/SKILL.md`, 필요시 `agents/<agent-name>.md`
3. `plugins/<plugin-name>/introduction/<plugin-name>_intro.md`
4. `marketplace.json`의 `plugins` 배열 항목 (name, source, version, description)
5. `updatelog/<plugin-name>_log.md` 사용자 공지 항목
6. `PluginList.md` 표 갱신

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
