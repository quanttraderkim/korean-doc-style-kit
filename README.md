# korean-doc-skill

한국어 비즈니스 문서를 AI 에이전트가 더 짧고, 더 구조적으로, 더 보고용 메모답게 쓰도록 돕는 문서 작성 스킬 레포입니다.

문제의식은 단순합니다. AI가 한국어 업무 문서를 만들면 대체로 말이 많고, `~입니다 / ~합니다`가 반복되고, 추상 수식어가 많아지고, 줄글이 길어집니다. 이 킷은 그 반대로 밀어줍니다. 결론 우선, 짧은 판단형 문장, 의미가 있는 제목, 필요한 곳에만 표와 불릿, 긴 문서에서는 `A. / A-1.` 넘버링을 쓰는 방향입니다.

## 왜 쓰나

이 레포는 아래 같은 문제를 줄이기 위한 것입니다.

- 문서가 너무 길어서 첫 화면에서 핵심 판단이 안 보임
- `~입니다 / ~합니다` 설명문이 반복돼 보고용 문서 느낌이 약함
- 표로 정리해야 할 내용을 줄글로 길게 풂
- 제목이 메시지 역할을 못 하고 단순 라벨로 끝남
- 에이전트마다 결과 스타일이 달라 문서 품질이 들쭉날쭉함
- 첫 화면에 판단이 안 보이고, 비교 정보가 줄글에 묻힘

목표는 문장을 예쁘게 꾸미는 것이 아닙니다. 더 빨리 읽히고, 더 빨리 판단되고, 더 일관되게 수정되는 문서를 만드는 것입니다.

## 30초 이해

이 레포를 적용하면 문서가 대략 아래 방향으로 바뀝니다.

Before:

> 이 기능은 사용자에게 여러 가지 의미 있는 가치가 있을 것으로 보이며, 장기적으로 긍정적인 효과가 기대됩니다.

After:

> 핵심 문제는 실행 누락.
>
> 초기 포지션은 범용 AI가 아니라 업무 보조 도구.

즉 긴 설명문을 짧은 판단형 문장, 의미 있는 제목, 필요한 표와 불릿으로 바꾸는 킷입니다.

## 빠르게 써보기

이 레포의 중심은 프롬프트가 아니라 [`skills/report-memo-doc-style/SKILL.md`](./skills/report-memo-doc-style/SKILL.md)입니다. 문서를 다시 쓰게 할 때는 먼저 이 파일을 읽게 하고, 그 다음 문서 타입과 rewrite mode를 지정하는 방식 권장입니다.

### 권장 방식: 모든 에이전트에서 SKILL.md를 정본으로 사용

Codex, Claude, OpenClaw, 다른 셸 에이전트 모두 아래처럼 쓸 수 있습니다.

1. 에이전트에게 이 레포의 [`skills/report-memo-doc-style/SKILL.md`](./skills/report-memo-doc-style/SKILL.md)를 읽게 함
2. 문서 타입을 지정함
3. `source-preserving`, `light report-style`, `report-first` 중 mode를 지정함
4. 원문 초안을 함께 줌

예시 요청:

> 이 레포의 `skills/report-memo-doc-style/SKILL.md`를 기준으로 이 문서를 strategy memo로 다시 써줘. mode는 light report-style. 원문 논리는 유지하고, 첫 화면에 핵심 판단과 요청사항이 보이게 해줘.

### Codex에서 쓸 때

[`skills/report-memo-doc-style`](./skills/report-memo-doc-style) 폴더를 로컬 Codex skills 디렉터리에 두고, 문서 요청 시 `$report-memo-doc-style`을 같이 호출하면 됩니다.

### Claude나 다른 에이전트에서 쓸 때

Claude Code는 공식적으로 personal / project scope skill을 지원합니다. 이 레포의 스킬을 Claude에서 실제 skill처럼 쓰려면, Claude 공식 문서가 안내하는 위치인 `~/.claude/skills/<skill-name>/SKILL.md` 또는 프로젝트의 `.claude/skills/<skill-name>/SKILL.md`로 설치하면 됩니다. 설치 후에는 자동 로드되거나 `/report-memo-doc-style`로 직접 호출할 수 있습니다.

예시:

```bash
mkdir -p ~/.claude/skills
cp -R skills/report-memo-doc-style ~/.claude/skills/
```

프로젝트 전용으로 두고 싶다면:

```bash
mkdir -p .claude/skills
cp -R skills/report-memo-doc-style .claude/skills/
```

이 레포의 root [`CLAUDE.md`](./CLAUDE.md)에는 Claude 기준 사용 방식을 따로 짧게 정리해두었습니다.

프롬프트 템플릿은 정본이 아니라 `shortcut` 또는 `fallback`입니다. 스킬 파일을 직접 읽히기 어려운 환경에서만 참고용으로 쓰는 것을 권장합니다.

### OpenClaw / ClawHub에서 쓸 때

현재 [`SKILL.md`](./skills/report-memo-doc-style/SKILL.md)는 `name`, `description`, `homepage`, `metadata.openclaw`를 포함한 OpenClaw-friendly frontmatter로 정리돼 있어서, OpenClaw workspace skill이나 ClawHub 배포용 skill로 쓰기 좋은 상태입니다.

OpenClaw 로컬 workspace에서는 `skills/report-memo-doc-style/`를 `<workspace>/skills/report-memo-doc-style/` 아래에 두고 쓰면 됩니다. 설치와 sync 흐름 자체는 OpenClaw / ClawHub 공식 문서를 따르는 편이 가장 안전합니다.

## 어떤 문서에 어떤 스킬 모드를 쓰나

| 문서 타입 | 언제 쓰나 | 먼저 지정할 것 | 참고 템플릿 |
| --- | --- | --- | --- |
| 전략 메모 | 왜 중요한지, 어떤 판단이 필요한지 먼저 보여줘야 할 때 | `strategy memo` + `light report-style` | [`prompts/strategy-memo.md`](./prompts/strategy-memo.md) |
| 상위기획 / 컨셉 기획 | 방향, 우선순위, 1차 범위를 먼저 보여줘야 할 때 | `upper planning` + `light report-style` | [`prompts/upper-planning.md`](./prompts/upper-planning.md) |
| PRD / 서비스기획 | 문제 정의, 범위, 흐름, 정책, 오픈 이슈를 분리해야 할 때 | `PRD / service planning` + `light report-style` | [`prompts/prd-service-planning.md`](./prompts/prd-service-planning.md) |
| Skill / Capability Spec | 입력, 출력, 예외, 평가 기준을 명확히 써야 할 때 | `skill spec` + `source-preserving` | [`prompts/skill-spec.md`](./prompts/skill-spec.md) |
| 유즈케이스 / 버티컬 워크플로 | `상황 / 동작 / 가치 / 제한` 구조로 정리해야 할 때 | `use case` + `light report-style` | [`prompts/use-case.md`](./prompts/use-case.md) |
| 허브 / 인덱스 페이지 | 어디부터 읽을지, 어떤 문서가 중요한지 먼저 보여줘야 할 때 | `hub page` + `source-preserving` | [`prompts/hub-page.md`](./prompts/hub-page.md) |
| 주간 업데이트 | 짧은 weekly summary나 대시보드 업데이트를 빠르게 공유해야 할 때 | `weekly update` + `light report-style` | [`prompts/weekly-update.md`](./prompts/weekly-update.md) |
| 팀 위클리 보드 (실험) | 큰 상태판 중심의 weekly / biweekly / 분기 포트폴리오 보드를 회의용으로 정리할 때 | `team weekly board` + `light report-style` | [`prompts/team-weekly-board.md`](./prompts/team-weekly-board.md) |
| 의사결정 원페이저 | 선택지 비교와 요청 결정사항을 한 장으로 정리할 때 | `decision one-pager` + `light report-style` | [`prompts/decision-one-pager.md`](./prompts/decision-one-pager.md) |
| 트래킹 / 옵스 보드 (실험) | 살아 있는 이슈 보드, 확인 필요사항, 운영 현황, 상태 추적 문서를 빠르게 읽히게 정리할 때 | `tracking / ops board` + `source-preserving` 또는 `light report-style` | [`prompts/tracking-ops-board.md`](./prompts/tracking-ops-board.md) |
| 이슈 히스토리 / 인시던트 로그 (실험) | 닫힌 이슈, 장애, 대응 이력을 누적 참조용으로 남길 때 | `issue history / incident log` + `source-preserving` | [`prompts/issue-history-incident-log.md`](./prompts/issue-history-incident-log.md) |
| 대응 문서 / Q&A 메모 (실험) | 대외·대내 답변, 예상 질문, 모범 답변, 리스크, 추가 확인사항을 정리할 때 | `response memo` + `light report-style` | [`prompts/response-memo.md`](./prompts/response-memo.md) |

## 무엇이 들어 있나

- 정본 역할의 스킬 문서: [`skills/report-memo-doc-style/SKILL.md`](./skills/report-memo-doc-style/SKILL.md)
- Codex / Claude / 다른 에이전트에서 스킬을 적용하는 방법
- 참고용 프롬프트 템플릿
- 스타일 차이를 바로 볼 수 있는 before / after 예시
- 스킬을 실제 문서로 점검하고 개선할 수 있는 evaluation 루프

## 기본 방향

- 에세이형 설명보다 보고용 메모체 우선
- `~입니다 / ~합니다 / ~됩니다` 최소화
- 모든 문장을 기계적으로 `~함`으로 끝내지는 않음
- 긴 설명형 `~한다`체도 기본값으로 두지 않음
- 명사형, 짧은 판단형 끝맺음 우선
- 결론과 핵심 판단을 앞에 배치
- 제목은 주제 라벨이 아니라 메시지 역할로 사용
- 불릿은 병렬 항목에만 사용
- 표는 비교, 요약, 소유자, 리스크, 옵션 정리에만 사용
- 긴 문서는 `A.`, `A-1.` 넘버링 권장
- 비교, 카테고리, 읽기 순서, 요약은 문단보다 작은 표 우선

## 참고용 프롬프트 템플릿

- [`prompts/strategy-memo.md`](./prompts/strategy-memo.md)
- [`prompts/upper-planning.md`](./prompts/upper-planning.md)
- [`prompts/prd-service-planning.md`](./prompts/prd-service-planning.md)
- [`prompts/skill-spec.md`](./prompts/skill-spec.md)
- [`prompts/use-case.md`](./prompts/use-case.md)
- [`prompts/hub-page.md`](./prompts/hub-page.md)
- [`prompts/weekly-update.md`](./prompts/weekly-update.md)
- [`prompts/team-weekly-board.md`](./prompts/team-weekly-board.md)
- [`prompts/decision-one-pager.md`](./prompts/decision-one-pager.md)
- [`prompts/tracking-ops-board.md`](./prompts/tracking-ops-board.md)
- [`prompts/issue-history-incident-log.md`](./prompts/issue-history-incident-log.md)
- [`prompts/response-memo.md`](./prompts/response-memo.md)

## 예시

- [`examples/before-strategy-memo.md`](./examples/before-strategy-memo.md)
- [`examples/after-strategy-memo.md`](./examples/after-strategy-memo.md)

## 이 스킬을 어떻게 진화시키나

이 레포는 정답 고정형이 아니라 피드백 루프를 전제로 합니다. 핵심은 `느낌상 좋아졌다`가 아니라, 같은 문서를 기준으로 `Skill Off / Skill On`을 비교하고, 반복 실패를 코드화해서 다시 스킬 규칙으로 환원하는 것입니다.

권장 루프는 아래 순서입니다.

1. 고정된 regression case 하나 선택
2. 스킬 없이 한 번, 스킬을 켜고 한 번 결과 생성
3. 같은 문서를 [`evaluation/rubric.md`](./evaluation/rubric.md)와 [`evaluation/review-checklist.md`](./evaluation/review-checklist.md)로 비교
4. 반복 실패를 [`evaluation/failure-taxonomy.md`](./evaluation/failure-taxonomy.md) 코드로 기록
5. 결과를 로컬 전용 `evaluation/results/*.local.md` 로그로 남김
6. 반복되는 실패만 스킬 규칙, 프롬프트, 예시에 반영

관련 파일:

- [`evaluation/README.md`](./evaluation/README.md)
- [`evaluation/rubric.md`](./evaluation/rubric.md)
- [`evaluation/failure-taxonomy.md`](./evaluation/failure-taxonomy.md)
- [`evaluation/review-checklist.md`](./evaluation/review-checklist.md)
- [`evaluation/feedback-template.md`](./evaluation/feedback-template.md)
- [`evaluation/cases/README.md`](./evaluation/cases/README.md)
- [`evaluation/cases/case.template.md`](./evaluation/cases/case.template.md)
- [`evaluation/scoreboard.template.md`](./evaluation/scoreboard.template.md)
- [`evaluation/results/README.md`](./evaluation/results/README.md)
- [`PRIVACY.md`](./PRIVACY.md)

목표는 문장을 예쁘게 만드는 것이 아닙니다. 더 빨리 읽히고, 더 빨리 판단되고, 더 일관되게 개선되는 문서를 만드는 것입니다.

## 익명화 원칙

이 레포의 git tracked 파일은 항상 일반화·익명화 상태를 유지합니다. 실제 문서 제목, 제품명, 프로젝트명, URL, page id는 넣지 않습니다. 실제 회귀 결과, scorecard, 날짜별 평가 로그도 git에 두지 않고 로컬 전용 `.local.md` 파일로만 관리합니다. 관련 기준은 [`PRIVACY.md`](./PRIVACY.md)를 따릅니다.
