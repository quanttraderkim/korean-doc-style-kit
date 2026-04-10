Rewrite this Korean draft as a PRD or service planning document.

Requirements:

- Keep the actual decisions and scope intact
- Rewrite in concise report-style memo wording
- Reduce polite explanatory prose
- Make scope boundaries explicit
- Surface `핵심 판단 / 범위 / 범위 제외 또는 후속 / 오픈 이슈` near the top
- Use tables for requirements, scenarios, dependencies, or metrics when helpful
- If policy, exception, storage, upload, or lifecycle rules are mixed together, split them into labeled tables
- If the document is policy-heavy, prefer `활성화 조건 → 생성/저장 → 예외 다운로드 → 업로드/리마인드 → 미노출/파기/삭제 → 오픈 이슈` ordering
- If the source contains a large mapping matrix, add a smaller summary table first and keep the detailed table below
- Separate unresolved items into their own section
- Move revision history or operational metadata below the top summary unless they directly change the current decision

Recommended structure:

1. 목적
2. 배경
3. 문제 정의
4. 목표
5. 범위
6. 주요 사용자 흐름
7. 정책 / 예외
8. 리스크
9. 오픈 이슈
