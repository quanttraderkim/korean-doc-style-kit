# scoreboard.template

실제 누적 점수판은 git tracked 영역에 두지 않습니다.

이 파일은 로컬 전용 `evaluation/scoreboard.local.md`를 만들 때 참고하는 템플릿입니다.

## 권장 컬럼

| 날짜 | 케이스 ID | 문서 타입 | 실행 라운드 | 비교 기준 | 적용 모드 | 기준 총점 | 현재 총점 | 변화 | 핵심 실패 코드 | 변경점 요약 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| YYYY-MM-DD | `PRD-001` | PRD / Service Planning Doc | 1 | Skill Off / Skill On | Light report-style | 0 | 0 | 0 | `F1`, `F11` | 짧은 개선 메모 |

## 운영 원칙

- 실제 제목, URL, page id는 적지 않음
- 케이스 ID만 사용
- 실제 scorecard는 `evaluation/scoreboard.local.md`에만 기록
- rerun이면 `비교 기준`과 `변경점 요약`을 반드시 남김
- git에는 이 템플릿만 유지
