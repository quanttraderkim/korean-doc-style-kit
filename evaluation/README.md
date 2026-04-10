# evaluation

이 폴더는 스킬을 실제 문서 결과로 점검하고 다시 개선하기 위한 운영 구조입니다. 목표는 감상평 수집이 아니라, `같은 문서`를 기준으로 `Skill Off / Skill On`을 비교하고, 반복 실패를 규칙으로 환원하는 것입니다.

단, git tracked 파일에는 실제 문서 식별자를 넣지 않습니다. 실제 평가 로그와 scorecard는 git에 두지 않고, 로컬 전용 `.local.md` 파일에만 기록합니다. git에는 평가 방법론과 템플릿만 남깁니다.

즉 이 레포는 `평가 프레임워크 공유용`입니다. 실제 benchmark 문서 세트와 실제 결과 로그는 각 사용자 환경에서 로컬 전용으로 운영하는 것을 기본으로 합니다.

## A. 기본 원칙

- 실제 문서로 평가
- 같은 문서를 `Skill Off`와 `Skill On`으로 모두 생성
- 문서 타입별로 고정된 regression case 유지
- 느낌 평가와 점수 평가를 같이 남김
- 반복 실패만 규칙으로 반영

## B. 권장 루프

1. [`cases/`](./cases/)에 있는 고정 문서 하나 선택
2. 스킬 없이 결과 생성
3. 스킬을 켠 결과 생성
4. [`rubric.md`](./rubric.md)로 점수 비교
5. [`review-checklist.md`](./review-checklist.md)로 질적 점검
6. [`failure-taxonomy.md`](./failure-taxonomy.md) 코드로 실패 유형 표기
7. 로컬 전용 `evaluation/results/*.local.md`에 결과 로그 남기기
8. 반복 실패만 스킬 / 프롬프트 / 예시에 반영

## C. 평가 산출물

- 점수표: [`rubric.md`](./rubric.md)
- 질적 체크리스트: [`review-checklist.md`](./review-checklist.md)
- 실패 코드: [`failure-taxonomy.md`](./failure-taxonomy.md)
- 리뷰 기록 템플릿: [`feedback-template.md`](./feedback-template.md)
- 고정 문서 세트 운영 방식: [`cases/README.md`](./cases/README.md)
- 누적 지표판 템플릿: [`scoreboard.template.md`](./scoreboard.template.md)
- 평가 결과 로그 운영 방식: [`results/README.md`](./results/README.md)

## D. 운영 기준

- 한 번의 평가로 규칙을 크게 바꾸지 않음
- 같은 실패가 2회 이상 반복될 때만 규칙 반영 검토
- 문체 문제와 구조 문제를 분리해서 기록
- 문서 타입 부적합은 별도 실패로 기록
- 회귀 세트는 문서 타입별로 최소 1개 이상 유지
- 새로운 규칙을 넣었으면 최소 2개 이상의 기존 케이스로 다시 확인
- rerun이면 이전 Skill On 대비 무엇을 바꿨는지 함께 기록

핵심은 `좋아 보임`이 아니라 `무엇이 좋아졌고, 무엇이 반복해서 실패하는가`를 계속 쌓는 것입니다.
