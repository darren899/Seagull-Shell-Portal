# Seagull Maritime × Shell MS Team Portal

Confidential, gated portal prepared for the **Shell Maritime Security (MS) Team**.

Department confirmed from Shell audit pack — team heading visible in their audit slides. Audit authored by Dennis Kerlin, SDE-STS/RS (Kerlin's internal org chain, not the team identifier).

Built Session 38, 10 April 2026.

## Subdomain

`shell.seagullmaritimeltd.com`

## Repo

New, isolated from `seagull-portals`. Reasons:
1. Solves the storage ceiling — `seagull-portals` is getting heavy.
2. Clean deploy history — Shell never sees unrelated commits.
3. Isolated gate — a DD portal code leak cannot compromise this portal.

Suggested GitHub repo name: `seagull-shell-portal`.

## Deployment steps (for Darren — GitHub Desktop workflow)

1. In GitHub Desktop: **File → New Repository**
   - Name: `seagull-shell-portal`
   - Path: somewhere outside OneDrive (standard Repos folder)
   - Initialize with README: **NO** (we have one)
2. Copy everything from this staging folder into the new repo folder.
3. Publish repo to GitHub as **Public**.
4. On github.com, go to the new repo: **Settings → Pages**
   - Source: Deploy from branch `main`, folder `/ (root)`
   - Save
5. **Settings → Pages → Custom domain:** `shell.seagullmaritimeltd.com`
6. DNS (email to Eric): Add a CNAME record for `shell` pointing to `darren899.github.io` — same pattern as `portals` and `learn`.

The `CNAME` file is already in the root of this repo so GitHub Pages will pick it up automatically once the DNS is live.

## Access

**Code (v1):** `SHELL-SEA-2026`

Stored as a reversed base64 hash in `assets/js/gate.js`. This is not encryption — it's a speed bump. Real protection is:
- Private subdomain, not linked anywhere public
- Code shared with Shell through a secure channel only
- Session-only storage (user re-enters code in each new browser session)
- Zero overlap with the DD portal gate (separate storage key, separate code, separate mechanism)

**To change the code:** generate a new hash in the browser console and replace `ACCESS_HASH` in `gate.js`:

```js
btoa('YOUR-NEW-CODE').split('').reverse().join('')
```

## Structure

```
seagull-shell-portal/
├── index.html              Landing page (gated)
├── gate.html               Access code gate
├── CNAME                   shell.seagullmaritimeltd.com
├── README.md               This file
└── assets/
    ├── css/
    │   └── shell.css       Design system v0.1
    ├── js/
    │   └── gate.js         Gate enforcement + login logic
    └── img/
        ├── seagull-white.svg              Seagull logo (white)
        ├── seagull-white.png              Seagull logo (white PNG)
        ├── seagull-shell-tint.svg         Hero variant, red→yellow gradient
        └── shell-pecten-placeholder.svg   Placeholder scallop (swap for real Shell asset)
```

## Visual system

- **Base:** `#0A0A0A` near-black
- **Shell red:** `#DD1D21`
- **Shell yellow:** `#FBCE07`
- **Fonts:** Montserrat (display, uppercase) + Open Sans (body)
- **Radial glow accents** in hero and section backgrounds
- **Hover states:** red-to-yellow gradient top bar, subtle glow, upward translate

## Sections (planned — not yet built)

| # | Section | Target content |
|---|---------|---------------|
| 01 | Shell Audit | Original docs, finding closures, CWP, Libero matrix Shell-formatted |
| 02 | Our Tools | LMS + HSE App + Sanctions Screener + Risk Screening Tool, demo accounts |
| 03 | Our Campaign | Link out to campaign portal |
| 04 | Ongoing Updates | Live feed of doc releases and closeout progress |
| 05 | Intelligence | Vanguard Tech int reports |
| 06 | Human Rights | VPSHR/ICoCA mapping, training, doc cross-references |

## Notes for future sessions

- Shell department name confirmed: **Shell Maritime Security (MS) Team**. Hero tagline, page titles, footer and gate updated in Session 38.
- Shell pecten sourced from the real Shell audit doc (`Seagull Maritime Audit Comments.pdf`, page 1). Lives at `assets/img/shell-pecten.png` — 161×151, transparent background.
- Gate code should be rotated before the actual Shell submission — one version for build/dev, a fresh one for the live Shell handover.
- All document links will point to files hosted in this repo's own `docs/` folder (TBD), not the `seagull-portals` repo — fully isolated.
