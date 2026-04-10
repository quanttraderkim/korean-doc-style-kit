# korean-doc-style-kit

한국어 비즈니스 문서를 AI 에이전트가 더 짧고, 더 구조적으로, 더 보고용 메모답게 쓰도록 돕는 스타일 킷입니다.

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

### Codex에서 쓸 때

[`skills/report-memo-doc-style`](./skills/report-memo-doc-style) 폴더를 로컬 Codex skills 디렉터리에 두고, 문서 요청 시 `$report-memo-doc-style`을 같이 호출하면 됩니다.

### 다른 에이전트에서 쓸 때

[`prompts/`](./prompts/) 아래 템플릿 중 하나를 그대로 복붙해서 쓰면 됩니다. 보통 아래 세 가지를 같이 주면 충분합니다.

1. 원본 초안
2. 문서 타입
3. 원문 유지형인지, 가벼운 보고형인지, 보고서형인지

처음 시작할 때는 `문서 타입`과 `rewrite mode`를 먼저 고르고, 그 다음 해당 프롬프트를 붙이는 방식 권장입니다.

## 어떤 문서에 어떤 프롬프트를 쓰나

| 문서 타입 | 언제 쓰나 | 추천 프롬프트 |
| --- | --- | --- |
| 전략 메모 | 왜 중요한지, 어떤 판단이 필요한지 먼저 보여줘야 할 때 | [`prompts/strategy-memo.md`](./prompts/strategy-memo.md) |
| PRD / 서비스기획 | 문제 정의, 범위, 흐름, 정책, 오픈 이슈를 분리해야 할 때 | [`prompts/prd-service-planning.md`](./prompts/prd-service-planning.md) |
| Skill / Capability Spec | 입력, 출력, 예외, 평가 기준을 명확히 써야 할 때 | [`prompts/skill-spec.md`](./prompts/skill-spec.md) |
| 유즈케이스 / 버티컬 워크플로 | `상황 / 동작 / 가치 / 제한` 구조로 정리해야 할 때 | [`prompts/use-case.md`](./prompts/use-case.md) |
| 허브 / 인덱스 페이지 | 어디부터 읽을지, 어떤 문서가 중요한지 먼저 보여줘야 할 때 | [`prompts/hub-page.md`](./prompts/hub-page.md) |
| 주간 업데이트 | 진행 / 이슈 / 다음 액션을 짧게 공유해야 할 때 | [`prompts/weekly-update.md`](./prompts/weekly-update.md) |
| 의사결정 원페이저 | 선택지 비교와 요청 결정사항을 한 장으로 정리할 때 | [`prompts/decision-one-pager.md`](./prompts/decision-one-pager.md) |

## 무엇이 들어 있나

- Codex에서 바로 쓸 수 있는 스킬
- 다른 에이전트에도 복붙해서 쓸 수 있는 문서 타입별 프롬프트
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

## 포함된 프롬프트 템플릿

- [`prompts/strategy-memo.md`](./prompts/strategy-memo.md)
- [`prompts/prd-service-planning.md`](./prompts/prd-service-planning.md)
- [`prompts/skill-spec.md`](./prompts/skill-spec.md)
- [`prompts/use-case.md`](./prompts/use-case.md)
- [`prompts/hub-page.md`](./prompts/hub-page.md)
- [`prompts/weekly-update.md`](./prompts/weekly-update.md)
- [`prompts/decision-one-pager.md`](./prompts/decision-one-pager.md)

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
- [`evaluation/scoreboard.template.md`](./evaluation/scoreboard.template.md)
- [`evaluation/results/README.md`](./evaluation/results/README.md)
- [`PRIVACY.md`](./PRIVACY.md)

목표는 문장을 예쁘게 만드는 것이 아닙니다. 더 빨리 읽히고, 더 빨리 판단되고, 더 일관되게 개선되는 문서를 만드는 것입니다.

## 익명화 원칙

이 레포의 git tracked 파일은 항상 일반화·익명화 상태를 유지합니다. 실제 문서 제목, 제품명, 프로젝트명, URL, page id는 넣지 않습니다. 실제 회귀 결과, scorecard, 날짜별 평가 로그도 git에 두지 않고 로컬 전용 `.local.md` 파일로만 관리합니다. 관련 기준은 [`PRIVACY.md`](./PRIVACY.md)를 따릅니다.
