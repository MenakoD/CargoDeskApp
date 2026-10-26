# CargoDesk

A responsive, offline-capable workspace combining the ADR Exemption Auditor, CMR Waybill Issuer, and DGR Acceptance Hub.

## Features

- Matching navy sidebar and main canvas, with light document cards and teal accents.
- Sidebar navigation and mobile drawer, with keyboard focus and labelled controls.
- Device-local date and clock in the lower-left panel.
- Optional city-based weather with a timestamped cached reading.
- Existing ADR calculation, CMR form, and DGR checklist modules.
- Document print/PDF controls and a “How to use this app” guide, available in the sidebar and overview.
- No required packages, fonts, or external scripts for the core app.

## Open offline

Open `dist/index.html` in a browser. Keep every file inside `dist` together. No installation is required. Weather requires internet; its most recent successful reading is cached when browser storage is available. The clock uses the device time zone.

If a browser blocks the outer “Print / Save PDF” button when opening downloaded files, use the print button inside the tool itself. Dense document tables can scroll horizontally on phones; the CMR retains its paper-style structure.

## Share with your team

For a smartphone team, the recommended next step is a hosted HTTPS link, optionally shared as a QR code. Hosting has not yet been configured for team access. A home-screen web app (PWA) would make repeat access easier and can use the existing offline cache after a first connected visit; installation metadata and icons still need to be added and tested.

The ZIP remains an offline fallback for desktop users. Send `CargoDesk-Team.zip`; colleagues should extract it and open `index.html`. Each person has an independent workspace; this app does not synchronize forms between people. Print completed documents to PDF to share results. Entries remain while switching sections but may be lost when refreshing or closing the page.

## Hosted offline support

Serve `dist` from an HTTPS static host. A service worker caches the app after the first successful connected visit. Wait for all assets to finish loading before disconnecting. Directly opening the downloaded files works without this first visit.

## Local preview for development

From the project folder, with Python installed:

```powershell
python -m http.server 8765 --directory dist
```

Open `http://localhost:8765`. Stop the preview with Ctrl+C. For ordinary offline use you do not need Python or a server.

## Project structure

```text
cargo-desk/
  dist/
    index.html                   App shell, overview, and guide
    app.css                      Theme and responsive layout
    app.js                       Navigation, clock, weather, and printing
    sw.js                        Hosted offline cache
    adr_exemption_auditor.html    ADR module
    cmr_waybill_issuer.html       CMR module
    dgr_acceptance_hub.html       DGR module
  .agents/skills/cargodesk-development/SKILL.md
  .openai/hosting.json            Private Sites configuration
  README.md
```

## Reusable development skill

The project skill at `.agents/skills/cargodesk-development/SKILL.md` explains CargoDesk's architecture, offline constraints, responsive and print conventions, verification, and beginner-friendly guidance. Open the repository in Codex and invoke `$cargodesk-development` when maintaining it. If the skill is not discovered, reference its file directly.

## Validation and packaging

For JavaScript syntax checks, with Node.js installed:

```powershell
node --check dist/app.js
node --check dist/sw.js
```

Check each tool, switch sections with entered values, inspect mobile layout, and verify print preview. Test the extracted folder with internet disconnected. Weather failure should leave every document tool accessible.

Create a team package from the project folder:

```powershell
Compress-Archive -Path dist/* -DestinationPath CargoDesk-Team.zip -Force
```

Only app files belong in the team ZIP. Do not include real shipment data, secrets, or generated customer documents in the repository.

## Current limitations

The CMR tool offers Save Draft and Load Draft using this browser’s local storage; drafts do not sync to colleagues. Its draft stores form fields, not drawn signatures. There is no shared database, login, collaboration service, or general automatic recovery of document fields after closing or reloading. Weather defaults to Berlin until changed. The original modules contain example shipment values; replace them before producing operational documents. No team-accessible deployment is live. The reserved private Sites project is unpublished. GitHub repository access and website access are separate; a private repository alone does not make a GitHub Pages site private.

## Source tools

The three supplied HTML tools retain their existing logic. CargoDesk provides navigation and a responsive shell. Verify operational outputs against your team's current requirements. No regulatory correctness review is implied.

Weather: Open-Meteo geocoding and forecast APIs. Requests send the selected city to the geocoding service and coordinates to the forecast service. No cargo form data is sent by the shell.

## In-app onboarding

Choose **How to use this app** in the sidebar or the overview quick-start banner. The guide explains each module, phone navigation, PDF export, CMR draft limitations, offline use, and independent team workspaces. It also explains that the original DGR checklist starts with Pass selected and requires every checkpoint to be reviewed.

## Suggested next improvements

1. Host an HTTPS team link with the access level your team needs, then distribute the link or a QR code.
2. Add a web app manifest and local app icons for home-screen installation; verify offline startup on actual iPhone and Android devices.
3. Add recoverable drafts for ADR and DGR, plus an explicit clear-data action.
4. Make the DGR checklist start as unreviewed and require completion before an acceptance result, as a separately scoped workflow change.
5. Improve phone data entry with larger controls and a mobile form view for the paper CMR.
6. Add shipment reference, document version/date, and reviewer fields to support handovers.

These are suggestions, not implemented features. Shared records would require a separate storage and access design.

## Application disclaimer

The disclaimer is displayed below every app section and repeated in the user guide.

CargoDesk is an unofficial application provided for assistance and learning. It has not been independently validated or certified for operational use. Use it with care and at your own risk. Its calculations, checklists, and generated documents may contain errors, omissions, or outdated information. Verify all inputs and results against current regulations, carrier requirements, and your organization’s procedures before relying on them. The app does not replace qualified professional judgment, required inspections, or official operational approval. You remain responsible for how you use its results.
