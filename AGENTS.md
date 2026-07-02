# Code Kenya pre-course — AI assistant rules (learner)

This file lives in your **course project folder** (for example a folder you named `code-kenya-precourse`) that you open in your editor with **File → Open Folder…**. It tells the in-editor AI how to run this course with the **Learn with Agents** tutor.

**Course manifest line (do not delete — used by an early lesson's automatic folder check):**
`COURSE_SLUG: code-kenya-pre-course`

**Editor you are using (change if needed — used so the AI calls your editor by the right name):**
`IDE: cursor`

> If you are using VS Code set this to `IDE: vscode`.
> If you are using Antigravity set this to `IDE: vscode`.
> If you are using another editor set this to `IDE: your-editor-name`.

---

## When the user wants to do this course

If they say any of the following (or close variations), they mean this program:

- "Start the Code Kenya pre-course"
- "Continue the Code Kenya pre-course"
- "Resume the Code Kenya course"
- "Next lesson" / "Check my work" in the context of this pre-course

**Use the Learn with Agents MCP** (the DevTutor / learnwithagents server), not generic web search, for **which lesson** to do and **how to verify** files in this folder.

1. **Load or continue:** `**start_or_resume_course**` or `**fetch_next_lesson**` with `**course_slug: "code-kenya-pre-course"**`.
2. **Tutor policy** — Each `fetch_next_lesson` response is assembled on the server: a **Tutor policy** (orchestration) block may come first, then the lesson title and body. The policy is the default for verify timing, teaching style, and tools; the **lesson** body is what the website shows. If anything disagrees, follow the **loaded lesson** for that step. You do not need to repeat the full policy in chat—it is already in the tool output.
3. **Teach** from the full tool text: policy (if any) + lesson, using **In this lesson** through **When you're done** in order. For modules still on the older format, use **Teach** / **Do** as written.
4. **After the student is ready** (per **When you're done**), run the check in the lesson **Verify** section: usually `**verify_step**`; the welcome lesson may use `**set_tutor_address**` then `**verify_tutor_address_recorded**` instead. Then `**mark_lesson_complete**` when advancing, not right after a fetch.
5. `**request_hint**` if stuck. `**list_courses**` if you need the slug. Do not show raw lesson IDs to the student.

---

## workspace_root (this folder)

Before every `verify_step`, pass **`workspace_root`** as the **absolute path to the directory that contains this `AGENTS.md` file** (the folder the student opened in the editor). If you omit it, checks run against the wrong directory and file checks fail.

### verify_step error prefixes (short)

- **`SYSTEM_ERROR:`** — path/process issue. Do not treat as the student’s fault; re-check the file or path yourself before alarming them.
- **`STUDENT_ERROR:`** — content does not match yet; explain in plain language and point to **Your task**.

---

## Naming the editor

Read the `IDE:` line above and use that app name (e.g. "open a terminal in **Cursor**"). If the line is missing, say **"your editor"** — never assume Cursor.

---

## MCP setup (the student's machine)

The **Learn with Agents** server must be installed in the student’s editor, with the Convex site URL and token from the program. If the MCP is missing or errors, help fix configuration; do not fake progress. See the package docs (`@learnwithagents/mcp-server` / your program’s README).

---

## Notes

- This folder may **not** be a monorepo; the course only checks **this** opened folder.
- Do **not** quote the **total** catalog count (e.g. "1 of 119"). Use **module** position only (e.g. "lesson 1 of 6 in Welcome and your editor").

---

## MCP Quick Reference

- **Start / continue a lesson:** call `start_or_resume_course` or `fetch_next_lesson` with `course_slug: "code-kenya-pre-course"`.
- **Run checks:** after the student signals ready, use `verify_step` (or `verify_tutor_address_recorded` for the welcome lesson) as the lesson's Verify section specifies.
- **Always pass `workspace_root`:** use the absolute path to the folder containing this `AGENTS.md` file (for example `C:\Users\<you>\code-kenya-precourse`). Passing `workspace_root` prevents path-related `SYSTEM_ERROR:` failures.
- **Verify kinds:** `verify_step` can run shell commands or file checks (`kind: shell | file_contains | file_regex`) — follow the lesson's Verify instruction for which kind to use.
- **Error prefixes:** handle `SYSTEM_ERROR:` as a path/process issue (not the student’s fault) and `STUDENT_ERROR:` as an indication the student hasn't completed the task yet.

Keep this file minimal — link to course docs when you need longer explanations.
