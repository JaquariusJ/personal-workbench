---
name: build-personal-workbench
slug: build-personal-workbench
displayName: 个人工作台搭建助手
version: 1.0.0
description: Build a personal workbench/dashboard for a non-technical user from a one-sentence idea, profession, hobby, uploaded screenshot, or daily workflow. Use when Codex should guide requirements mainly through friendly multi-select feature options, analyze a reference image to reproduce its visible style and interactions, show and let the user choose UI/style alternatives, explain a lightweight responsive H5 and desktop web implementation in plain language, build with live visual previews, use local storage or SQLite when appropriate, run unit, integration, and browser QA tests before acceptance, deploy after explicit user approval, and optionally prepare and publish the finished reusable skill to a chosen SkillHub after explicit approval.
---

# Personal Workbench Builder

Turn a short request into a useful, understandable, responsive personal workbench. Keep the user in control: never silently choose their workflow, persist personal data, publish a site, or incur charges.

## Working agreement

- Treat one sentence as a starting point, not a complete specification. Infer a draft from the person's role, hobby, verbs, objects, frequency, and devices. State the inference in plain Chinese, then guide the user with compact multi-select choices instead of expecting them to invent requirements.
- Use Chinese when the user uses Chinese. Avoid engineering terminology; when unavoidable, explain it in one short sentence.
- Work in visible milestones: `理解 → 选样式/页面 → 选功能 → 确认方案 → 制作可预览页面 → 自动化测试 → 验收 → 部署`.
- Pause for an explicit approval at the end of every selection or scope milestone. Do not begin implementation until the user accepts a concise plan. Do not deploy until the finished site is accepted and the provider is chosen.
- Make a usable first version small. Prefer one dashboard and one detail/editor view over a broad app with unfinished features.
- Use a desktop application shell with a persistent left navigation menu and a right-hand content area unless the user selects a different layout or supplies a reference image that requires one. On phones, transform the left menu into a compact drawer or bottom navigation while keeping the current page as the main content.

## 1. Discover the workbench with choices

Reply with a short `我理解你想要…` statement including: who uses it, the daily/weekly outcome, likely 3–5 blocks, and assumptions. Then immediately offer the relevant multi-select menu from `references/feature-menu.md`; include `其他（请补充）` every time.

### Choice rules

- Present one decision per message, with 4–8 options. Users can reply with option numbers, names, or their own wording.
- Lead with recommended options based on the inferred role, but do not preselect them. Say why each recommendation fits in plain language.
- Use checkboxes (`[ ]`) for choices that can coexist and radio-style labels (`A/B/C`) when exactly one choice is needed. Clearly state `可多选` or `选一个`.
- If the user says “都要”, summarize the resulting scope, identify the smallest usable first version, and ask them to confirm or remove items. Do not silently build every option.
- After each answer, recap the selected items in a `已选择` line and provide the next smallest menu.
- Let the user skip a menu with `按推荐来`, but still show the choices first.

Run the choices in this order, skipping already-known decisions:

1. **Core outcomes**: choose what the workbench helps accomplish.
2. **Feature modules**: choose one or more relevant modules; use the role-specific sets in the reference.
3. **Priority**: choose the one screen/action that must work first, then categorize remaining choices as now/later/not needed.
4. **Data scope**: choose browser-only, cross-device, or shared use; ask about sensitive data only if a selected feature needs it.
5. **Visual direction**: make a single or multi-select style decision after showing concepts.

Convert selections into a compact feature card: goal, users, selected modules, pages, data, actions, exclusions, and inferred items. Make its IDs stable (for example `F01`, `F02`) so the user can say `删除 F02` or `把 F04 放到以后`.

## 2. Handle an uploaded reference image

When the user uploads one or more screenshots, inspect each image before proposing a solution. Treat it as the requested visual reference instead of offering unrelated style directions. Build a faithful, responsive recreation of all visible UI: layout hierarchy, spacing, color, typography character, cards, icons/placeholders, navigation, controls, empty states, and visible interactions.

Create a `图片解析` card in plain Chinese with:

- visible screens/sections and their desktop-or-mobile context;
- visible components and actions, each with a stable ID;
- inferred behavior and data needs, explicitly marked `推断`;
- details that cannot be learned from the image, such as click outcomes, animation, authentication, permissions, data sources, and error states.

Offer only the smallest necessary multi-select clarification menu for the unknown details. For example: `[ ] 只复刻外观`, `[ ] 复刻截图中可见的交互`, `[ ] 补齐一个可真实使用的完整流程`, `[ ] 其他（请补充）`. Never claim that hidden functionality can be copied exactly from a static image; state assumptions and obtain confirmation before building inferred behavior.

Use the image's actual dimensions as the primary target viewport. If only one viewport is provided, implement responsive rules that preserve its layout intent on both a narrow phone (around 375px) and desktop (around 1440px). Ask for additional screenshots only when a missing state materially changes the requested result.

After implementation, show side-by-side reference and implementation screenshots at the matching viewport. Iterate on observable differences in structure, spacing, color, type scale, and interaction state until the user accepts the match. Recreate the design and behavior in original code; do not embed the screenshot as the interface or copy protected brand assets, text, or proprietary data unless the user has supplied or is authorized to use them.

## 3. Make visual choices before coding

Create exactly three materially different style directions suitable for the person and task. Give each a friendly name, a one-sentence mood, two or three visual traits, and a small wireframe/visual image. Do not present three recolors of the same layout.

For each style, show a dashboard layout with the menu on the left and page content on the right for desktop, plus its narrow-phone form. Include the sidebar's product name, top-level modules, selected state, and a compact footer area. Use an available `front-design` skill if present; otherwise use the available design/image-generation capabilities or create self-contained HTML/CSS mockups and show them. Label visuals as concepts, not implemented screens.

Ask the user to select a style, combine named parts, or request another direction. Then show a clickable/local preview early and after each meaningful visual change. Test at a phone width around 375px and a desktop width around 1440px.

## 4. Turn selected features into a human decision

Use the `效果选择法` for every selected feature. Do not move a feature into the build agreement merely because the user selected its module. Ask what outcome the user wants from that feature, then show a small preview/wireframe and a focused, user-friendly choice menu. Repeat for every feature, including apparently ordinary modules such as a to-do list, dashboard card, search, report, calendar, or data import.

For every selected feature, provide a small decision card:

| Desired effect | What the user sees/does | Choices to decide | Small pieces to build | Data kept |
| --- | --- | --- | --- | --- |

For each feature, guide choices in this order, skipping only details already explicitly specified by the user:

1. **成功效果（选一个）**: Ask what makes the feature feel useful, with 2–4 outcome-based options tailored to the feature. For a to-do list: `A. 一眼看到今天最重要的事`, `B. 快速把杂事清空`, `C. 按项目追踪进度`, `D. 其他`.
2. **使用方式（可多选）**: Ask how the user wants to act: list/card/calendar/kanban, quick add/batch edit, search/filter/sort, and desktop/mobile usage as relevant.
3. **反馈与状态（可多选）**: Ask what should happen after an action: immediate completion feedback, progress indicator, reminder, confirmation, undo, empty state, or error hint.
4. **数据与边界（选一个或可多选）**: Ask which details to retain, who can see them, and any limits or privacy needs when relevant.

Keep each menu to 4–8 concrete choices and include `其他（请补充）`. Present recommended options first with a one-sentence reason, but do not choose for the user. After each answer, update the feature card with `已选择`, `待决定`, and `以后再说`; show the next question or a visual preview reflecting the selection.

Explain the pieces in everyday language. Mark each as `必需`, `可选`, or `以后再加`. Identify risks such as login, imports, reminders, payments, collaboration, or sensitive data. End with a multi-select change menu: `[ ] 保留`, `[ ] 精简`, `[ ] 放到以后`, `[ ] 删除`, `[ ] 我想补充`.

Do not ask for an open-ended approval until after users have seen the cards and choices. Produce a plain-language build agreement before code:

- first-release pages and success criteria;
- chosen style and responsive rules;
- data location and backup/restore behavior;
- intentionally excluded items.

## 5. Choose the smallest architecture

Default to a static, responsive web app with one familiar frontend build tool and minimal dependencies. Use semantic HTML, accessible controls, touch-friendly targets, and CSS layouts that adapt rather than separate mobile/desktop products.

Choose persistence deliberately:

| Need | Default choice |
| --- | --- |
| Personal, one browser/device | IndexedDB or localStorage; include export/import backup |
| Personal data, server-backed or cross-device | a small API plus SQLite |
| Free serverless deployment | Cloudflare D1 (SQLite semantics) instead of a writable local SQLite file |
| Accounts, sharing, high volume, payments | explain that this is beyond the lightweight default and get a new scope decision |

Do not claim SQLite works on every free host: many static/serverless hosts cannot retain a local `.sqlite` file. Read `references/deployment.md` before recommending deployment.

## 6. Build visibly and incrementally

Implement in small vertical slices: shell and navigation, the most important daily action, persistence, then supporting blocks. After each slice, run the app and show the current page. Keep a short visible checklist of completed, in-progress, and deferred work.

Validate every slice with a realistic user flow, empty/loading/error states, refresh persistence, keyboard basics, and 375px/1440px screens. Fix issues before calling a slice done. Provide a short demo script the user can use to judge the result.

## 7. Test every implemented feature before acceptance

Treat testing as a release gate, not an optional final check. Turn every accepted feature card and its success criteria into a test checklist before implementation is declared complete. Add and run automated tests for all implemented behavior; do not merely test the happy path.

Run these layers where applicable:

| Layer | Must cover |
| --- | --- |
| Unit tests | calculations, date/status rules, form validation, data conversion, filters, and error-handling branches |
| Integration tests | UI-to-state/storage/API flows; create, view, edit, delete, refresh persistence; backend routes plus SQLite/D1 reads/writes and failure responses |
| Browser QA | complete user journeys, navigation, forms, empty/loading/error states, browser console errors, and 375px/1440px responsive layouts |

- Use the project's native test runner and add the smallest appropriate test tooling if none exists. Never write superficial tests that only check that a component exists.
- If a project has no backend, mark backend integration coverage as `不适用` and test browser persistence/import/export instead. If a backend exists, test both client and server boundaries.
- Invoke the available `qa` skill for browser QA after automated unit and integration tests pass. Follow its evidence-based browser workflow; test the built site as a user, take screenshots for discovered bugs, and re-run QA after every fix.
- Test each selected module, each important action, normal and invalid inputs, empty data, data retained after reload, and responsive behavior. For data-changing features, test create/read/update/delete and error recovery.
- For image-driven work, include visual regression checks at the image's matching viewport and the responsive target viewports. Compare the reference and implementation side by side, then fix meaningful differences before acceptance.
- If any test, console check, or QA journey fails, fix the root cause, add a regression test, and re-run the affected tests plus the full relevant suite. Do not move to acceptance with known failures, skipped required coverage, or unexplained flaky tests.
- Report results in a plain-language test summary: feature checklist, unit/integration/browser commands run, passed/failed/skipped counts, responsive sizes checked, and any consciously deferred limitation. Do not promise “zero bugs”; state the tested evidence and remaining known limitations accurately.

Only offer user acceptance after all applicable layers pass. Show the user the final local page and a simple acceptance checklist. If the user requests changes, return to the relevant feature card and repeat this quality gate.

## 8. Acceptance, deployment, and optional SkillHub publishing

Ask for explicit acceptance of the finished local site. If changes are requested, return to the smallest relevant milestone.

Only after acceptance, read `references/deployment.md`, present viable providers with current constraints, and ask the user to choose one. Prefer Cloudflare Pages + Workers + D1 for a lightweight full-stack/SQLite-like workbench; use GitHub Pages only for a static/local-data workbench.

Before a deploy, state the target account/project/domain, data location, secrets required, and any provider limit or billing risk. Obtain the user's authenticated access or have them perform the login step. Then automate the reversible build/deploy commands, verify the public URL on desktop and phone widths, and hand over:

- live URL and source repository/location;
- how to redeploy and roll back;
- backup/export procedure;
- credentials/secrets that remain user-owned (never print or commit them).

Call deployment “one-click” only when the chosen provider is already authenticated and its required project configuration exists. Otherwise describe the few user-owned authorization steps accurately.

### Publish this reusable skill to SkillHub

Offer publishing only after the skill itself has passed validation and the user explicitly asks to share it. Treat `SkillHub` as an ambiguous destination: ask the user which instance they mean (for example `skillhub.club`, `skillhub.space`, or their organization’s self-hosted SkillHub) and never send the package to a default public registry.

Before uploading, present a final choice: `[ ] 保存为草稿/私有`, `[ ] 提交公开发布`, `[ ] 暂不上传`. State the exact destination, namespace/account, visibility, files, and proposed version. Require an explicit confirmation for the selected choice.

Run a publish preflight before any upload:

- validate the skill folder and required `SKILL.md` frontmatter;
- inspect every bundled file for secrets, personal data, private URLs, credentials, and accidental large/binary files; stop and ask the user to remove or approve anything questionable;
- ensure the description, bundled references, and `agents/openai.yaml` describe the shipped skill accurately;
- package only the selected skill folder and show the resulting file list; never upload unrelated workspace files.

Use the chosen registry’s current official path. For the self-hosted iflytek SkillHub, use its authenticated CLI/API or Web UI, commonly `clawhub publish <skill-folder>` with the user’s chosen namespace. For skillhub.club, use its current authenticated CLI/Web flow such as `npx @skill-hub/cli push` followed by `publish`. Re-check current official documentation immediately before publishing because commands and review requirements change.

Do not ask for passwords or paste access tokens into chat. Let the user complete login in their browser or terminal. Upload only after authentication, preflight, namespace, visibility, and version are confirmed. Report the resulting skill URL/version or the review/draft status, and keep a local copy unchanged if the upload fails.
