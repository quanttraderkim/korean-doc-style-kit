# PRIVACY

이 레포는 git에 올라가는 모든 문서와 로그를 기본적으로 일반화·익명화합니다.

## 기본 원칙

- 실제 문서 제목, 제품명, 프로젝트명, 조직명, 서비스명은 git tracked 파일에 넣지 않음
- Confluence / Jira URL, page id, issue key, source URL은 git tracked 파일에 넣지 않음
- 회귀 케이스는 항상 `STRAT-001`, `PRD-001`, `USECASE-001` 같은 익명 ID로만 기록
- 결과 로그, scoreboard, 예시, README, 프롬프트, 스킬 예시 모두 동일 기준 적용
- 실제 매핑 정보는 로컬 전용 파일에만 보관

## 로컬 전용 파일

실제 문서명, 익명 ID 매핑, 실제 scorecard, 실제 평가 로그, 실제 privacy audit 도구는 아래 로컬 전용 파일에만 보관합니다.

- `evaluation/private/case-map.local.md`
- `evaluation/scoreboard.local.md`
- `evaluation/results/*.local.md`
- `scripts/privacy_audit.local.py`

이 경로는 `.gitignore`에 포함되어 있으므로 원격에 올라가지 않습니다.

## 새 케이스 추가 절차

1. 새 케이스에 익명 ID 부여
2. git tracked 파일에는 익명 ID와 일반화된 설명만 기록
3. 실제 제목, URL, page id는 로컬 매핑 파일에만 기록
4. 결과 로그와 scoreboard는 로컬 전용 `.local.md` 파일에만 누적
5. 커밋 전 로컬 privacy check 실행

## 금지 항목

- 실제 제품명
- 실제 프로젝트명
- 실제 문서 제목
- 실제 page id / issue id / URL
- 내부 조직명이나 스페이스 키
- 스크린샷, 예시 문장, before/after 안에 남아 있는 실제 서비스 맥락

## 예외

예외는 두지 않음. private 저장소라도 git tracked 기준은 동일하게 유지합니다.

## 권장 운영

- 케이스 매핑은 로컬 전용 `evaluation/private/case-map.local.md`에만 기록
- 실제 scoreboard는 `evaluation/scoreboard.local.md`에만 기록
- 실제 평가 로그는 `evaluation/results/*.local.md`에만 기록
- 새 평가 로그 작성 전 로컬 privacy check 실행
- 커밋 직전 로컬 privacy check 재실행
- git tracked 영역에는 scoreboard와 실제 results를 두지 않음
- privacy audit 도구 자체도 git tracked 영역에 두지 않음
