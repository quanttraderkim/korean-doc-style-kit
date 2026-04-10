# CLAUDE.md

이 레포를 Claude에서 사용할 때의 기본 원칙은 단순합니다.

정본은 `prompts/`가 아니라 [`skills/report-memo-doc-style/SKILL.md`](./skills/report-memo-doc-style/SKILL.md)입니다. Claude Code는 공식적으로 `~/.claude/skills/<skill-name>/SKILL.md` 또는 프로젝트 `.claude/skills/<skill-name>/SKILL.md` 위치의 스킬을 지원하므로, 가능하면 이 경로에 설치해서 실제 skill처럼 쓰는 방식을 권장합니다.

예시:

```bash
mkdir -p ~/.claude/skills
cp -R skills/report-memo-doc-style ~/.claude/skills/
```

설치 후에는 자동으로 관련 문서에서 로드되거나 `/report-memo-doc-style`로 직접 호출할 수 있습니다.

권장 순서:

1. `skills/report-memo-doc-style/SKILL.md`를 읽게 함
2. 문서 타입 지정
3. `source-preserving`, `light report-style`, `report-first` 중 mode 지정
4. 원문 초안을 함께 제공

예시:

> 이 레포의 `skills/report-memo-doc-style/SKILL.md`를 기준으로 이 문서를 upper planning 문서로 다시 써줘. mode는 light report-style. 방향, 우선순위, 1차 범위가 첫 화면에서 보이게 해줘.

`prompts/` 아래 파일은 스킬 파일을 직접 쓰기 어려운 환경에서만 참고용으로 사용합니다.
