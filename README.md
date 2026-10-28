
De-identified event log for the anonymized article.

The log is derived from the mandatory procedural-history disclosures of Seoul's
owner-led redevelopment projects (정비사업 정보몽땅, `cleanup.seoul.go.kr`),
retrieved on 31 August 2026. It covers 796 projects and 28,473 dated events,
1996–2026.

## Columns

| Column | Values | Meaning |
|---|---|---|
| `case_id` | 8 random characters | one redevelopment project |
| `statute` | `urban_act`, `small_scale_act` | governing statute: Act on the Improvement of Urban Areas and Residential Environments, or Act on Special Cases Concerning Small-Scale Housing Improvement |
| `in_panel` | `0`, `1` | `1` for the 685 projects in the monthly state panel (see below) |
| `stage_rank` | `1`–`19` | position of the stage in the statutory sequence, matching $s(a)$ in the paper |
| `activity_type` | `apply`, `grant`, `notice`, `selection`, `contract`, `other` | application to the authority; its disposition; public notice of the disposition; selection of a firm; contract or contract amendment; anything else |
| `date` | `YYYY-MM` | month of the event |

`stage_rank` runs: 1 master plan · 2 safety diagnosis · 3 zone designation ·
4 promotion committee approval · 5 management firm selection ·
6 association establishment approval · 7 designer selection ·
8 implementation approval · 9 contractor selection ·
10 management and disposal approval · 11 demolition contractor selection ·
12 relocation · 13 demolition notification · 14 construction notification ·
15 general sale approval · 16 completion approval · 17 transfer announcement ·
18 association dissolution · 19 liquidation.

Dates are given at month resolution because that is the resolution the analysis
uses. Two events carry dates outside the observation window (1976 and 2033); the
latter is a recording error in the source. Analyses filter to `date <= 2026-08`.

## De-identification

Project identifiers bear no relation to the source portal's own identifiers.
Project names, districts, parcel numbers, firm names, consent rates and membership
counts are not included.

The log is **pseudonymous, not anonymous**. The source portal is public, and a
sufficiently determined party with an independent copy of it could match long
event sequences back to projects. Please do not attempt re-identification.

## Source and licence

Source data: Seoul Metropolitan Government, 정비사업 정보몽땅
(`cleanup.seoul.go.kr`), public disclosure under Article 124 of the Act on the
Improvement of Urban Areas and Residential Environments. Snapshot 2026-08-31.

Released under CC BY 4.0.

