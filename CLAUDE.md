# CLAUDE.md

이 레포를 Claude에서 사용할 때의 기본 원칙은 단순합니다.

정본은 `prompts/`가 아니라 [`skills/report-memo-doc-style/SKILL.md`](./skills/report-memo-doc-style/SKILL.md)입니다. Claude에게 문서를 다시 쓰게 할 때는 먼저 이 파일을 읽게 하고, 그 다음 문서 타입과 rewrite mode를 지정하는 방식을 권장합니다.

권장 순서:

1. `skills/report-memo-doc-style/SKILL.md`를 읽게 함
2. 문서 타입 지정
3. `source-preserving`, `light report-style`, `report-first` 중 mode 지정
4. 원문 초안을 함께 제공

예시:

> 이 레포의 `skills/report-memo-doc-style/SKILL.md`를 기준으로 이 문서를 upper planning 문서로 다시 써줘. mode는 light report-style. 방향, 우선순위, 1차 범위가 첫 화면에서 보이게 해줘.

`prompts/` 아래 파일은 스킬 파일을 직접 쓰기 어려운 환경에서만 참고용으로 사용합니다.
