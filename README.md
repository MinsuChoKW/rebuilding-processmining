# Idling, not stalling — event log

De-identified event log for *"Idling, not stalling: Event-log evidence on how urban
redevelopment projects spend their time."*

The log is derived from the mandatory procedural-history disclosures of Seoul's
owner-led redevelopment projects (정비사업 정보몽땅, `cleanup.seoul.go.kr`),
retrieved on 31 August 2026. It covers 796 projects and 28,473 dated events,
1996–2026.

```
event_log.csv    28,473 rows × 6 columns
sha256           b7f70d16ece286974926f039caddbdea632207fa7cc4081fb72b6b07010fe444
```

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

## Reference values

A reconstruction of the paper's panel from this file should return:

| Quantity | Value |
|---|---|
| projects / events | 796 / 28,473 |
| panel projects (`in_panel = 1`) | 685 |
| observed project-months | 90,790 |
| state distribution, *K* = 12 (advancing / idling / stalled) | 30.0 / 39.9 / 29.9 % |
| entries into idling | 2,428 |
| forward recovery within 12 months | 22.4 % |
| passed-stage / frontier idling, share of project-months | 36.5 / 3.4 % |

## How the panel is built

Enough detail to reproduce the table above.

**Panel.** The 685 projects are those at or beyond association establishment with
at least one event, excluding three whose first event predates the portal by more
than a decade. Each project is observed monthly from its first event until it
reaches completion approval (`stage_rank = 16`) or the snapshot (2026-08),
whichever is first. Completion approval is an absorbing state: post-completion
administration is not consensus procedure. This yields 90,790 project-months.

**States.** Let $r(t)$ be the highest `stage_rank` the project has reached by
month $t$, and let the window be the $K$ months $(t-K,\;t]$. The state at $t$ is

- **advancing** if $r(t) > r(t-K)$, that is a new highest stage was reached inside the window;
- **idling** if at least one event falls inside the window but $r(t) = r(t-K)$;
- **stalled** if no event falls inside the window.

$K = 12$ is the primary specification; the paper reports *K* = 8, 14 and 18
alongside. Idling months divide further: **passed-stage** if any event in the
window sits at a stage below $r(t)$, **frontier** if every event in the window
sits at $r(t)$.

**Fate of idling.** For each maximal run of consecutive idling months, the first
exit is classified as forward recovery, stalling, or censoring at the end of
observation. **An exit into completion approval counts as forward recovery**, since
reaching it is reaching a new stage.

**Cumulative incidence.** Spell lengths are whole months, so ties are real and are
kept. The cumulative incidence of cause $c$ is computed in discrete time,

$$F_c(t)=\sum_{s\le t} S(s^-)\,\frac{d_c(s)}{n(s)},\qquad
S(s)=\prod_{u\le s}\left(1-\frac{d(u)}{n(u)}\right),$$

with $n(s)$ the number of spells still at risk at month $s$, $d_c(s)$ the number
exiting to cause $c$ at $s$, and $d(s)$ the number exiting to any cause. This is
deterministic and needs no random seed.

> **A note on software.** Several survival packages break ties in duration by
> adding random jitter before estimating. On this log that lowers 12-month forward
> recovery from 22.4 % to about 21.8 %, and makes the estimate depend on the row
> order and the random seed (21.6–22.1 % across shuffles). The figure reported in
> the paper is the discrete-time estimate above, with ties retained.

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

## Citation

Citation details will be added on acceptance.
