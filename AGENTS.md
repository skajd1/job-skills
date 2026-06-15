# Project Instructions

## Purpose

This workspace manages Korean cover-letter drafts as Markdown files. When the user provides a company name, JD or role description, and cover-letter prompts, create a tailored self-introduction draft using the existing profile and prior application materials.

## Required Drafting Flow

1. Read `개인_경험_역량_분석.md` first when it exists.
2. Read `README.md`, `자소서_작업_워크플로우.md`, `자소서_작성_규격.md`, `자소서_작성_요령.md`, `자소서_템플릿.md`, and `humanizer_사용법.md` before creating or updating a cover-letter file.
3. Follow `자소서_작업_워크플로우.md` exactly for every cover-letter task.
4. When there are 2 or more prompts, assign each prompt draft to a focused subagent. The main Codex must coordinate context, integrate drafts, and perform final review.
5. When there is only 1 prompt, the main Codex may draft it directly, but must still follow the same JD analysis, experience matching, humanizer review, and final overwrite rules.
6. Draft the cover letter in the project format:
   - `result/기업명/직무명YYMM.md`
   - one `## 문항 N. ...` section per prompt
   - one `### 답변 제목` and one `### 답변` per prompt
7. Apply the writing principles from `자소서_작성_요령.md`:
   - analyze the JD before drafting
   - answer the company's need, not only the applicant's desire
   - use one or two grounded experiences per prompt
   - use STAR for experience prompts
   - include numbers, concrete nouns, technologies, and role-specific outcomes whenever truthful
   - avoid generic template language and unsupported claims
8. After the first complete integrated draft is written, the main Codex must apply the `humanize-korean` skill as a mandatory review step before treating the file as final.
9. The humanized result must overwrite the draft content in the same `.md` file. Do not leave a separate draft file, copy file, or `_workspace` final artifact as the project deliverable.
10. Preserve all facts, company names, role names, project names, technologies, dates, numbers, and character-limit intent during humanizer review.
11. Re-check character limits, target company fit, and stale company names after humanizer review.

## Final Output Rule

The final deliverable for each application is a single Markdown file under `result/기업명/`. The file should contain the humanizer-reviewed answer text directly in each `### 답변` section. The entire `result/` directory is ignored by Git because it contains real company application drafts.

## Subagent Rule

Subagents are drafting assistants only. They should not perform final integration, humanizer review, or final approval. The main Codex owns the final answer quality and must verify the completed `.md` file before reporting completion.
