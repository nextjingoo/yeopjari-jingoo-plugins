# 지침플러그인

"옆자리 진구씨"가 배포하는 회사 업무용 AI 지침 Claude Code 플러그인 모음입니다.

## 설치

```
/plugin marketplace add <이 저장소 owner>/지침플러그인
/plugin install summary-report-writer@yeopjari-jingoo-plugins
```

(마켓플레이스 저장소 이름은 한글이어도 되지만, `marketplace.json`의 `name` 필드는 `claude plugin validate`가 비ASCII 문자를 "공식 마켓플레이스 사칭"으로 오탐하는 버그가 있어 영문(`yeopjari-jingoo-plugins`)으로 고정했습니다.)

설치 후 "Run /reload-plugins to activate."가 뜨면 `/reload-plugins`를 한 번 더 실행합니다.

## 포함된 플러그인

| 플러그인 | 설명 |
|---|---|
| `summary-report-writer` | 투자/사업 기획서 등 원본 자료를 임원 보고용 요약 보고서로 재구성하는 표준 프로세스. 원본 상세 파악 → 9개 항목 인터뷰 → 초안 작성 → 독립 자가검토 서브에이전트까지 포함 |

## 구조

```
지침플러그인/
├── .claude-plugin/marketplace.json   ← 마켓플레이스 카탈로그
└── plugins/
    └── summary-report-writer/        ← 플러그인 하나당 폴더 하나
```

새 지침을 추가할 땐 `plugins/` 아래에 폴더를 하나 만들고 `marketplace.json`의 `plugins` 배열에 항목을 추가합니다.
