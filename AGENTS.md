# AGENTS.md

이 레포는 `프롬프트 모음`이 아니라 `문서 작성 스킬` 레포입니다. 에이전트가 이 레포를 읽을 때는 아래 원칙만 먼저 따르면 됩니다.

## 1. SKILL 중심

정본은 [`skills/report-memo-doc-style/SKILL.md`](./skills/report-memo-doc-style/SKILL.md)입니다. 프롬프트 템플릿은 shortcut 또는 fallback으로만 봅니다.

## 2. 사용자 README 우선

공개 사용자는 [`README.md`](./README.md)를 먼저 읽습니다. README에는 사용자 기준 설치와 사용만 두고, 내부 운영 메모는 여기나 maintainer 문서로 내립니다.

## 3. tracked 영역 익명화

git tracked 파일에는 실제 문서 제목, 제품명, 프로젝트명, URL, page id를 남기지 않습니다. 관련 기준은 [`PRIVACY.md`](./PRIVACY.md)를 따릅니다.

## 4. 운영 세부는 maintainer 문서 참조

회귀 운영, failure code 사용, 프리셋 추가 기준, 배포 메모 같은 세부 운영 규칙은 [`MAINTAINERS.md`](./MAINTAINERS.md)를 따릅니다.
