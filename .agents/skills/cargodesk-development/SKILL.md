---
name: cargodesk-development
description: Extend, maintain, or package the CargoDesk offline export-document workspace and its ADR auditor, CMR waybill, and DGR acceptance tools. Use for this project, not unrelated cargo advice or regulatory certification.
---

# CargoDesk development

Read the repository README before changing the application. The distributable app is `dist/`; the three HTML document tools are independent documents embedded by `app.js`. They remain mounted when navigating so entered data survives section changes. Avoid rebuilding frames on every navigation.

## Preserve the working modules

Preserve existing calculations, checklist logic, document fields, and print layouts unless the user requests changes to them. Keep screen-specific responsive styles inside `@media screen` so paper documents retain their structure. When a dense document cannot fit a narrow screen, retain usable horizontal scrolling rather than squeezing fields beyond readability.

The source tools contain sample entries. Do not present sample data as actual shipment records. Do not represent this project as regulatory validation. If asked to change compliance rules, establish the applicable regulation and edition from authoritative sources before implementing the requested rule.

## Offline and visual conventions

Keep the core UI, fonts, styles, and document logic local to `dist/`. Do not introduce a required CDN, external script, login, or backend into the offline flow without the user's request. Weather is optional: it may refresh online and show a timestamped saved reading offline. Never fabricate live weather or online status. Browser storage can fail; the document tools should remain usable.

Support both extracted-folder use through `index.html` and static HTTP/HTTPS hosting. Direct-file browser isolation can block the shell print action; each tool's native print button must remain available. A hosted service worker helps after a first connected visit; it does not replace the downloadable app. Update cache naming when changing cached assets and verify stale versions are retired.

Use the established matching navy sidebar and main canvas, light document surfaces, teal accents, and mint, blue, and amber tool identities. Keep date, time, and weather near the bottom left. At narrow widths, use the existing drawer. Include keyboard focus, clear labels, and readable form fields.

## Verify and deliver

Check navigation among all three tools, preservation of entered values across navigation, meaningful module behavior for changed code, browser-local opening, mobile layout, printing, and unavailable-weather handling as applicable. Run JavaScript syntax checks. Report checks that could not be performed honestly.

Update the README for behavior, structure, usage, sharing, or storage changes. Rebuild the team ZIP from the final `dist/` contents. Include the project skill and documentation in source control, but exclude shipment documents, credentials, and local server output. Publishing or a GitHub push requires task authorization; this skill grants none by itself.

## Learning support

The project owner is learning software development through air-cargo projects. For teaching requests, explain one manageable change and its important code, then let the user test it. For implementation requests, complete the authorized work and explain the main changes plainly. When fixing an error, explain what it means, where it happened, and why the correction works.
