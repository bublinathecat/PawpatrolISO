# Office Patrol

A gamified self-audit for the Duvo Prague office. Anyone in the office can run it without an auditor present: it explains every check in plain English (what to look at, why it matters, what could go wrong, what proof to collect) and produces a management review, a full per-control report and a spreadsheet to store.

## Run it

- **Online:** enable GitHub Pages on this repository (see below) and open the Pages URL.
- **Offline:** download the repository and open `index.html` in a browser. Spreadsheet export needs an internet connection (it loads SheetJS from cdnjs).

## Modes

| Mode | What it covers | Checks |
|---|---|---|
| ☠ Easy | Legal baseline and basic hygiene (GDPR, Czech labour, H&S and fire law) | 27 |
| ☠☠ Medium | ISO 27001 / SOC 2 ready. Includes Easy. | 65 |
| ☠☠☠ Hard | What a bank or critical-entity customer would audit (NIS2 supply chain, DORA contractual inspection rights). Includes everything. | 73 |
| 🤝 Client visit | Quick check within 24 h before a client or auditor visit | 25 |

## How scoring works (and why)

Points reward **findings and evidence, not passes**. Marking a control "In place" without naming the proof earns little; logging a gap with a description, risk and proof earns the most. Harder tiers multiply points. This counters the main weakness of self-assessment: people clicking "fine" to finish faster.

## Outputs

From the results screen:

- **Management review** (HTML, prints to PDF): bottom line, readiness per tier, top risks with required changes, status by area, decisions requested.
- **Full report** (HTML): management review plus every control with status, finding, proof, method, automation idea and framework mapping.
- **Spreadsheet** (.xlsx): Summary, Results and an Action plan sheet with Owner and Due date columns.
- **Patrol file** (.json): the raw run, which can be imported again later to reopen or compare.

Patrols are saved in the browser that ran them. To keep a record, export the spreadsheet and patrol file and store them in the team drive.

## Process

1. **Owner:** the Prague office security owner (and a deputy) runs the patrol.
2. **Cadence:** Medium quarterly, Hard yearly, Client visit within 24 h before every client or auditor visit, plus a full run after any office change (move, refit, new landlord service).
3. **Record:** export the spreadsheet and patrol file to the team drive. Do not commit results to this repository.
4. **Fix:** high-risk items get an owner and due date in the Action plan sheet and are reviewed at the next security sync.
5. **Improve:** where a control is marked "Automatable: Full", prefer automating it over re-checking it by hand.

## Editing the controls

All checks live in `controls.js`, one object per control:

```js
{ "id": "VI-02", "domain": "Visitors", "control": "...", "why": "...", "threat": "...",
  "tier": 1, "cv": true, "how": "...", "proof": "...",
  "gdpr": "...", "cz": "...", "iso": "...", "soc2": "...", "nis2": "...", "ai": "...",
  "auto": "Full", "idea": "..." }
```

`tier` is 1 (Easy), 2 (Medium) or 3 (Hard). `cv: true` puts the control in the client-visit check. Keep ids stable: saved patrols refer to controls by id. The full mapping with framework references is in `docs/control-mapping.xlsx`.

## Publish with GitHub Pages

1. Create a repository (ideally in the company's GitHub organisation) and upload `index.html`, `controls.js`, `README.md`, `.gitignore` and the `docs` folder.
2. Settings → Pages → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)` → Save.
3. After about a minute the Pages URL appears in the same screen.

## Data handling

- The app sends nothing anywhere. Answers stay in the browser until you export them.
- **Never commit patrol results or exported reports to a public repository.** They describe the office's security gaps. `.gitignore` excludes the export file names as a safety net.
- A public Pages site exposes the control catalogue, which is generic. If that is still too much, host it in a private repository with access-controlled Pages, or run it locally.

## Disclaimer

Legal references are mapping aids, not legal advice. Confirm Czech-law specifics (thresholds, decrees, inspection intervals) with the OZO or Czech counsel before relying on them in a customer response.
