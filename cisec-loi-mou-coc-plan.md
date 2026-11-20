# CISEC Dashboard — LOI / MOU & COC Tab Plan

## Overview

Add a new sidebar tab **"LOI / MOU & COC"** to the existing CISEC dashboard (`CISEC/cisec-dashboard.html`).  
The tab shows a single unified table of all collaboration agreements and certificates, derived from the 16 PDF files in `CISEC/LOI & MOU/`. Since the PDFs are scanned images, data is seeded with placeholder dates (TBD) and all statuses set to **Aktif** for the user to update later.

---

## Sub-Task 1 — Add navigation item to sidebar

**Intent:** Register the new tab in the sidebar so the user can click it to navigate to the new module.

**Expected Outcomes:**
- A new nav item labelled "LOI / MOU & COC" with an appropriate icon appears in the sidebar below "Laporan & Statistik".
- Clicking it activates the new module and deactivates the current one (same behaviour as existing nav items).

**Todo List:**
- Add a `<div class="nav-item">` entry in `<aside>` with `onclick="showModule('loicoc', this)"` and icon `fas fa-handshake`.

**Relevant Context:**
- Sidebar nav pattern: `cisec-dashboard.html` lines 254–268
- `showModule()` function handles tab switching: line 586–595

**Status:** [ ] pending

---

## Sub-Task 2 — Add the module section (HTML)

**Intent:** Create the `<section id="mod-loicoc">` module with a header and a table listing all 16 organisations.

**Expected Outcomes:**
- Module shows a header "LOI / MOU & COC" with subtitle and red divider (consistent with other modules).
- A summary stat row shows total count, how many are Aktif, how many Tamat.
- A filterable table with columns: **#, Organisasi, Jenis, Tarikh Mula, Status**.
- All 16 rows are pre-filled from the file names with Jenis auto-detected (MOU for IBM/MOUIBM, COC for COC.pdf, LOI for the rest), Tarikh Mula = "TBD", Status = "Aktif".

**Todo List:**
- Add `<section id="mod-loicoc" class="module">` after the existing `mod-laporan` section.
- Include module header, stat summary (total / aktif / tamat counts computed from data).
- Include a filter dropdown for Jenis (Semua / LOI / MOU / COC) and Status (Semua / Aktif / Tamat).
- Render table rows via JavaScript data array (same pattern as `dataAhli` / `renderAhli`).

**Relevant Context:**
- Module HTML pattern: `cisec-dashboard.html` lines 275–374 (mod-ringkasan), 377–428 (mod-pelajar)
- Table + filter pattern: lines 411–427
- Badge colours: `badge-green` = Aktif, `badge-red` = Tamat

**Status:** [ ] pending

---

## Sub-Task 3 — Add JavaScript data and render logic

**Intent:** Define the data array for all 16 documents and wire up filtering + rendering functions.

**Expected Outcomes:**
- `dataLOI` array with 16 entries: `{ organisasi, jenis, tarikh, status }`.
- `renderLOI(data)` builds the table rows (same pattern as `renderAhli`).
- `filterLOI()` filters by Jenis and/or Status dropdowns.
- Summary counts (total, aktif, tamat) are dynamically computed and displayed.

**Data to seed (from file names):**

| Organisasi | Jenis |
|---|---|
| GIG | LOI |
| KITAB | LOI |
| MRM | LOI |
| Muhammadiyah | LOI |
| P. Lokh | LOI |
| PEKA | LOI |
| PEREKA | LOI |
| Politeknik USK | LOI |
| SKT | LOI |
| SOTA | LOI |
| IBM | LOI |
| IBM | MOU |
| Masjid Daerah | LOI |
| Micron | LOI |
| PKT Logistik | LOI |
| — | COC |

All Tarikh = "TBD", all Status = "Aktif".

**Relevant Context:**
- JS data/render pattern: lines 597–634 (dataAhli / renderAhli / filterAhli)

**Status:** [ ] pending
