---
name: korean-doc-skill
description: Use this skill when Korean business documents feel too long, too polite, too abstract, or too hard to scan. Apply it to strategy memos, upper-planning docs, PRDs, service planning docs, capability specs, execution guides, runbooks, script usage guides, weekly updates, one-pagers, and hub pages so they read like concise report-style memos with strong structure, selective tables, explicit numbering for long docs, and minimal filler.
homepage: https://github.com/quanttraderkim/korean-doc-skill
user-invocable: true
metadata: {"openclaw":{"homepage":"https://github.com/quanttraderkim/korean-doc-skill"}}
---

# Korean Doc Skill

## Overview

Use this skill when the target tone is a Korean business working document rather than an essay. The goal is fast comprehension, clear judgments, and scan-friendly structure.

This file is the canonical skill definition for Codex, Claude, OpenClaw, and other agents that can load a `SKILL.md` file directly.

Typical trigger signals:

- the draft is too long
- the writing is too polite or too explanatory
- the document has long prose but weak structure
- the reader should be able to skim it quickly
- the reader needs to execute, verify, or judge something quickly
- the output will be uploaded to a wiki or shared as an internal review document
- the user says things like `전략 문서로 정리`, `상위기획처럼`, `PRD처럼`, `위키 허브처럼`, `위클리처럼`, `이슈 대응 문서처럼`, `실행 가이드처럼`, `점검 절차처럼`, `런북처럼`

You do not need exact preset names from the user. If the user's natural-language intent is clear enough, infer the closest preset and proceed. If the user does not explicitly name the document type but the source itself clearly looks like a strategy memo, PRD, weekly, issue response memo, or hub page, infer from the source and continue.

## Core Rules

Write in short report-style memo Korean. Reduce repetitive `~입니다`, `~합니다`, `~됩니다`. Do not force every sentence into rigid `~함`. Also avoid drifting into long declarative prose such as repeated `~한다`, `~이다`, or `~다` sentence endings. Prefer noun phrases and short judgment-oriented wording such as `~필요`, `~전제`, `~검토`, `~제안`, `~가능`, `~우선`.

Lead with the conclusion. The first visible screen should answer why the document exists, what the key judgment is, and what needs to happen next.

If the first visible screen cannot answer those three questions quickly, compress it first. Use a summary table or short labeled blocks before adding more prose.

Keep paragraphs short. Most paragraphs should be 2 to 4 lines. If a paragraph grows longer, split it with a stronger heading, a table, or a short list.

Use headings to carry meaning. `###` headings should state the message or judgment, not a vague topic label.

For longer strategy, planning, or report documents, prefer explicit outline numbering. Use top-level labels such as `A.`, `B.`, `C.` and second-level labels such as `A-1.`, `A-2.` when they materially improve scanability. Avoid going deeper than two levels unless the user explicitly wants a more formal tree.

Use bullets only for parallel items. Do not break a single sentence into fake bullets just to make the page look shorter.

Do not force sentence-final periods onto every short line. In headings, labels, table cells, bullets, one-line judgments, and memo-style fragments, omit the final period by default. Use a period only when writing a full prose sentence with multiple clauses, when two or more sentences appear in one paragraph, or when punctuation materially reduces ambiguity.

If a section starts reading like explanatory narration with many consecutive `~다.` endings, compress it. Convert narrative explanation into a summary table, a short judgment block, or 2 to 3 memo-style bullets before expanding again.

If the output is intended to be pasted into a Confluence page body, do not repeat the page title as a top-level `#` heading. Confluence already renders the page title above the body, so start with a short lead sentence or the first real section such as `## A. 먼저 볼 항목`.

In top-summary sections such as `개요`, keep only the largest changes, purpose, target, or scope. Move edge cases, exception branches, empty-state handling, and implementation detail into lower sections such as `주요 변경 포인트`, `예외`, or `운영 포인트`.

When the document is mainly about a UI, layout, or visible behavior change, prefer an `AS-IS / TO-BE` visual comparison near the top before detailed prose. For Confluence delivery, favor native-looking links and simple table emphasis when they materially improve scanability.

For short summary tables, definition tables, and policy tables in Confluence, first-column emphasis often improves scanability. If the tool can write Confluence-native table styling or post-edit the rendered page, prefer subtle first-column background shading on label columns such as `항목`, `구분`, `용어`, `화면군`. If the pipeline is markdown-only, treat this as optional post-processing rather than a required output rule.

Use tables when the reader needs comparison, categorization, ownership, tradeoffs, options, targets, state transitions, or summary at a glance.

If three or more items need to be compared, categorized, or scanned quickly, default to a table rather than a paragraph. Do not leave comparison logic buried in prose.

Preserve the source logic unless the user explicitly asks for a report-first rewrite. Add structure first. Rewrite substance only when it materially improves clarity.

When documenting writing rules or guidance, avoid dense narrative explanation. Prefer short labeled blocks such as `A. 기본 방향`, `B. 문체`, `C. 구조`, `D. 표/불릿/제목`.

For long planning or policy documents, do not place document history, revision logs, ticket references, or guide metadata above the real summary. Show purpose and key judgment first, then place metadata below if needed.

## Rewrite Modes

Choose one mode first.

| Mode | Meaning | When to use |
| --- | --- | --- |
| Source-preserving rewrite | Keep the original logic and section order as much as possible. Improve wording and structure only. | The draft already has the right substance but reads poorly. |
| Light report-style rewrite | Keep the original logic, but add top summary, clearer headings, tables, or numbering where helpful. | The draft needs to be more readable for sharing or review. |
| Report-first rewrite | Reorder the document for decision support. Add stronger top summary and re-sequence sections around judgment. | The audience wants quick decision support, not source-faithful reading. |

If the user does not specify a mode, default to source-preserving rewrite plus structure improvement.

In practice, most users will not name the mode explicitly. If the user says `정리해줘`, `다듬어줘`, `위키용으로 다시 써줘`, or similar, default to `light report-style` unless source fidelity is clearly more important.

Natural-language shortcuts:

- `전략 문서`, `방향성 검토`, `논의 안` -> `Strategy Memo`
- `상위기획`, `연간 계획`, `컨셉 기획` -> `Upper Planning / Concept Planning`
- `상세기획`, `PRD`, `기획서` -> `PRD / Service Planning Doc`
- `유즈케이스`, `직군별 시나리오` -> `Use Case / Vertical Workflow Doc`
- `허브 문서`, `인덱스 페이지`, `문서 모음 소개` -> `Hub / Index Page`
- `위클리`, `주간 업데이트` -> 기본은 `Weekly Update`
- `상태판이 큰 위클리`, `보드형 위클리`, `큰 상태판 위클리`, `분기 보드` -> `Team Weekly Board` 변형
- `이슈 대응 문서`, `Q&A 대응`, `답변 정리` -> `Response Memo`
- `이슈 히스토리`, `장애 이력`, `대응 이력` -> `Issue History / Incident Log`
- `실행 가이드`, `점검 절차`, `런북`, `운영 가이드`, `스크립트 사용법`, `체크리스트` -> `Execution Guide / Runbook / Script Usage Guide`

## Default Tone

Prefer concrete nouns and verbs over abstract modifiers. Aim for report-style memo wording that sounds like an internal decision document, not an essay, not a telegraphic note dump, and not a textbook-style `~한다` narrative.

Prefer:

- `초기 도입은 A안 우선`
- `후속 연락 누락이 거래 누락으로 이어짐`
- `무료 유저 수익화는 필요하나 총매출 임팩트는 제한적`
- `핵심 타깃은 반복 고객 관리가 중요한 업종`

Avoid:

- `고객 경험을 보다 전략적으로 고도화할 수 있음`
- `본질적으로 중요한 의미를 갖는다고 판단됨`
- `결과적으로 여러 측면에서 유의미한 효과 기대 가능`
- `이 기능은 고객관리에 중요한 역할을 한다`

## Structural Defaults

Unless the user asks otherwise, use this order:

1. `목적`
2. `핵심 요약`
3. `핵심 판단` or main analysis sections
4. `리스크 / 전제 / 고려사항`
5. `시사점 / 다음 액션 / R&R`

For long documents, add an executive-summary table near the top when it genuinely helps the reader.

For strategy memos, use-case docs, and hub pages, assume a top summary table is needed unless the source is already extremely compact.

For long documents, numbered section labels are often worth adding directly in headings. Example: `## A. 핵심 요약`, `### A-1. 왜 지금 중요한가`.

When the document is a hub or index page, optimize for navigation first. The reader should understand what this document set is, where to start, and which child documents matter without reading long prose.

## Document-Type Presets

### Strategy Memo

Recommended structure:

- `목적`
- `핵심 요약`
- `왜 중요한가`
- `핵심 판단`
- `근거`
- `리스크/전제`
- `시사점`

Rules:

- Put the judgment in headings
- Put one comparison or summary table near the top by default
- Use lists for reasons, risks, or evidence only
- Avoid essay-style narration
- If the first screen does not show `왜 중요한가 / 핵심 판단 / 시사점`, compress before expanding
- If the source is option-heavy, show `권고안`, `비교 기준`, and `요청사항` on the first screen before detailed evidence
- For option-comparison memos, default to one compact comparison table first and push detailed financial or operational backup below

### Upper Planning / Concept Planning

Recommended structure:

- `목적`
- `핵심 요약`
- `왜 지금`
- `방향`
- `우선순위`
- `1차 범위`
- `후속 상세기획 연결`
- `리스크 / 전제`

Rules:

- Treat this as a direction-setting document, not a full execution plan
- The first screen should show `핵심 판단 / 방향 / 우선순위 / 1차 범위`
- Use summary tables aggressively near the top
- Compress execution detail, long history tables, and metadata unless they change the current judgment
- If execution detail must remain, push it below the direction-setting sections
- Distinguish clearly between `방향`, `우선순위`, and `후속 상세기획에서 풀 내용`

### PRD / Service Planning Doc

Recommended structure:

- `목적`
- `배경`
- `문제 정의`
- `목표`
- `범위`
- `주요 사용자 흐름`
- `정책/예외`
- `리스크`
- `오픈 이슈`

Rules:

- Prefer explicit scope boundaries
- Use tables for requirements, scenarios, dependencies, or metrics
- Put unresolved items in a separate section instead of burying them in prose
- For long planning docs, show `핵심 판단 / 범위 / 범위 제외 또는 후속 / 오픈 이슈` near the top
- If policy, exception, storage, upload, or lifecycle rules are mixed together, split them into labeled tables before adding prose
- When a source contains large mapping tables, keep the original detail but add a smaller summary table first so the reader can understand the logic before reading the full matrix
- If the document is policy-heavy, prefer `활성화 조건 → 생성/저장 → 예외 다운로드 → 업로드/리마인드 → 미노출/파기/삭제 → 오픈 이슈` ordering
- For policy-heavy planning docs, separate data principles, exception rules, and deletion/retention rules into tables before narrative explanation
- Move revision history or operational metadata below the top summary unless the history itself is the subject

### Skill Spec / Capability Spec

Recommended structure:

- `한 줄 정의`
- `언제 쓰는가`
- `입력`
- `출력`
- `핵심 동작`
- `예외/금지`
- `평가 기준`

Rules:

- Keep definitions literal
- Prefer small examples over long explanation
- Avoid marketing language

### Report / Decision Material

Recommended structure:

- `목적`
- `핵심 요약`
- `주요 판단`
- `옵션 비교`
- `리스크`
- `일정/R&R`

Rules:

- Put summary first
- Use tables aggressively for options, impact, and ownership
- Use collapsed detail only for backup material, not for the main argument

### Execution Guide / Runbook / Script Usage Guide

Recommended structure:

- `먼저 볼 항목`
- `바로 실행하는 순서`
- `판정 기준`
- `결과 확인`
- `권한 제한 시 수동 확인`
- `주의사항`

Rules:

- Treat this as an execution-support document, not a narrative explanation
- Put the final artifact, final file, final column, or final judgment point on the first screen
- If the reader only needs one file, one command, or one result field, state that explicitly near the top
- Show the shortest successful execution path before detailed explanation
- Prefer compact tables for `입력값`, `생성 파일`, `판정 기준`, `수동 확인 경로`
- When permission issues or environment limits are likely, add a separate fallback section instead of mixing it into the main flow
- This is not a live tracking board unless the document is continuously updated for status monitoring
- For CloudShell, console, script, or operational check docs, prefer `A. 먼저 볼 항목 -> B. 바로 실행하는 순서 -> C. 판정 기준 -> D. 결과 확인 -> E. 권한 제한 시 수동 확인` ordering

### Weekly Update

Recommended structure:

- `이번 주 핵심 변화`
- `진행 현황`
- `이슈 / 리스크`
- `다음 주 계획`
- `지원 필요사항`

Rules:

- Keep it short enough to skim in one screen per section
- Prefer status tables over long progress prose
- Separate done, blocked, next clearly
- Treat this as the default weekly preset
- Use this preset for short weekly summaries and dashboard-style updates
- Put `이번 주 핵심 변화 / 핵심 To-Do / 리스크` on the first screen before detailed tables
- If the source already has a stable project table, keep it below a compact executive summary instead of flattening it into prose
- Remove empty template rows, duplicated section blocks, and obvious system noise before polishing

### Team Weekly Board (Experimental)

Recommended structure:

- `이번 주 핵심 신호`
- `주요 공유 / 결정 필요`
- `핵심 To-Do`
- `포트폴리오 보드`
- `리스크 / 지원 요청`
- `참고 링크 / 부록`

Rules:

- Use this when the source is still a weekly-family document but the main body is a large board-heavy status page
- Keep one compact executive summary above the main board
- Preserve the board shape; do not rewrite the whole page into narrative summary
- Remove template noise, duplicated sections, and system metadata leaking into titles or cells
- If `전주 진행 / 금주 계획 / 장기 목표` are mixed in one cell, split them before polishing
- Keep the first screen meeting-friendly: top signals, decisions needed, and next actions first

### Decision One-Pager

Recommended structure:

- `목적`
- `핵심 판단`
- `선택지 비교`
- `추천안`
- `리스크 / 전제`
- `요청 결정사항`

Rules:

- Put the recommended option near the top
- Keep the document tight
- Use one main comparison table
- Avoid background history unless it changes the decision

### Use Case / Vertical Workflow Doc

Recommended structure:

- `한 줄 정의`
- `왜 이 직군 / 상황이 중요한가`
- `대표 장면 / 상황`
- `AI가 해야 하는 동작`
- `사용자 가치`
- `기본 기능`
- `사용자 설정값`
- `제한 / 금지`

Rules:

- Explain the situation as `상황 -> 동작 -> 가치` rather than loose description
- Use short scene-oriented headings
- Prefer one summary table near the top for `핵심 가치 / 대표 장면 / 피해야 할 포지션`
- Avoid turning the whole document into narrative explanation
- If multiple use cases exist, separate them as parallel blocks with the same shape
- If representative scenes are more than two, present them as a table or repeated fixed blocks, not free prose

### Hub / Index Page

Recommended structure:

- `한 줄 정의`
- `왜 이 문서 묶음을 보는가`
- `현재 우선 확인 대상`
- `문서 구조 / 카테고리`
- `권장 읽기 순서`
- `기본 원칙`

Rules:

- Optimize for navigation, not persuasion
- Keep the top area short and high-signal
- Use tables or grouped bullets to show category purpose and representative documents
- Avoid repeating the same document list in multiple formats unless each list serves a different reading path
- First screen should show `문서 묶음 정의 / 지금 먼저 볼 것 / 읽기 순서` before longer explanation

### Tracking / Ops Board (Experimental)

Recommended structure:

- `현재 상태`
- `이번 주 핵심 변화`
- `주요 이슈 / 리스크`
- `트래킹 항목`
- `다음 액션`
- `지원 필요사항`

Rules:

- Optimize for live tracking, not persuasive narrative
- Put status, owner, next action, and timing in tables by default
- Keep dated updates compact; do not let them drift into diary-style prose
- Separate `현재 상태`, `결정 필요`, and `참고 메모` clearly
- Use stable status labels such as `진행 중`, `대기`, `완료`, `리스크`
- If the page mixes agenda, tracking, and memo content, split them into separate labeled sections before polishing
- Use this preset for open issue boards, check-needed pages, and active coordination pages
- Keep unresolved items and resolved history in separate sections or tables
- If the source is mainly a chronological closed-issue log, do not force this shape; treat it as an issue history / incident log candidate instead

### Issue History / Incident Log (Experimental)

Recommended structure:

- `문서 범위`
- `최근 핵심 이슈`
- `이슈 / 사건 인덱스`
- `사건별 기록`
- `공통 패턴 / 재발 방지`
- `참고 링크`

Rules:

- Use this for accumulated issue history, known-issue memory, incident chronology, and response-history pages
- Optimize for reference and recall, not for live tracking
- Keep chronology and incident boundaries explicit
- For each incident, prefer a repeated fixed shape such as `이슈 내용 / 원인 / 영향 / 조치 / 후속`
- Put one compact index or summary block near the top before long historical detail
- Separate active unresolved tracking from closed historical record
- If the source is mainly a live open-issue board, use `Tracking / Ops Board` instead

### Response Memo (Experimental)

Recommended structure:

- `목적`
- `핵심 입장`
- `주요 질문 / 이슈`
- `권고 답변 / 모범 답변`
- `리스크 / 확인 필요사항`
- `요청사항 / 다음 액션`

Rules:

- Use this for PR response prep, executive Q&A prep, external inquiry 대응, and sensitive issue explanation memos
- Put the official stance or recommended answer on the first screen
- Separate `공식 답변`, `내부 판단`, `미확정 사항`, and `추가 확인 필요` clearly
- Prefer tables for `질문 / 답변 / 리스크 / 상태 / 담당`
- If the source is mainly a day-by-day 대응 연표, treat it as `Issue History / Incident Log` instead of forcing a response-memo shape

## Hard Don’ts

Do not write long introductory filler before the real point.

Do not use bullet points to simulate paragraph breaks.

Do not hide comparisons, category roles, or reading order inside prose when a small table would show them faster.

Do not repeat the same judgment in slightly different wording.

Do not add summary language unless it actually summarizes something.

Do not replace a concrete claim with an abstract phrase.

Do not put document history, revision logs, or metadata tables above the key summary in long planning or concept documents.

Do not hide the main body behind collapsed sections unless the user explicitly wants a report-first summary page.

Do not turn every sentence into rigid `~함` style. The target tone is concise internal memo/report wording, not forced shorthand.

Do not let the document slide into long `~한다` explanation mode. Declarative sentences are allowed when needed, but they should not dominate the page.

Do not write style guidance as dense narrative paragraphs when a short labeled checklist would communicate faster.

## Micro Examples

### Headings

Prefer:

- `### 무료 유저 수익화는 필요하나 총매출 임팩트는 제한적`
- `### 초기 도입 타깃은 반복 고객 관리 업종이 적절`

Avoid:

- `### 사업성`
- `### 타깃`

### Bullets

Good:

- `후속 연락 누락`
- `재방문 고객 관리 부재`
- `매출 회수 근거 약함`

Bad:

- `고객 관리가 중요함`
- `그래서 이 기능이 필요함`

The bad example is not parallel information. It should be a short paragraph or heading-level judgment instead.

### Tone

Prefer:

- `초기 타깃은 반복 고객 관리 업종`
- `추천 자동화보다 기억 복원과 후속 관리가 핵심`
- `규제 리스크로 자동 권유 포지션은 비적합`

Avoid:

- `이 기능은 특정 직군에게 중요한 가치를 제공한다`
- `이 서비스는 고객관리에 매우 유용한 역할을 한다`

### Tables

Use tables for:

- option comparison
- target segment comparison
- ownership / R&R
- summary at a glance

Do not use tables for:

- one short claim
- one example sentence
- a paragraph that reads naturally without comparison

## Rewrite Workflow

When using this skill:

1. Identify the document type first.
2. Decide whether the task is source-preserving rewrite, light report-style rewrite, or report-first rewrite.
3. Restructure the outline before rewriting sentences.
4. Convert long narrative blocks into one of:
   - a stronger heading plus short paragraph
   - a summary table
   - a true parallel bullet list
5. If the output is guidance, checklist, or a hub page, prefer grouped rule blocks over essay-style explanation.
6. Cut filler and abstract phrases last.

If unsure, prefer source-preserving rewrite plus structure improvement over aggressive summarization.

## Self-check Before Finalizing

Before returning the final draft, check:

1. Does the first visible screen show the purpose and key judgment?
2. Are `~입니다 / ~합니다 / ~됩니다` still overused?
3. Has the draft drifted into long `~한다` narrative explanation?
4. Are bullets used only for real parallel items?
5. Are tables used where comparison or summary matters?
6. Would explicit `A. / A-1.` numbering improve scanability?
7. Are the headings carrying actual messages?
8. Is any paragraph still too long and better split?
