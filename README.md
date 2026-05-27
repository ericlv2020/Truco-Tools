# truco-tools

Private repository for Truco International Limited — dashboards, scripts, and document templates.

## Structure

```
truco-tools/
├── .github/workflows/
│   └── deploy.yml         # Injects the Airtable token from GitHub Secrets, deploys to Pages
├── dashboard.html         # Commercial Engine overview
├── deal-dashboard.html    # Live deal & opportunity tracker
├── order-bank.html        # Order bank & FY financial summary
└── quote-tracker.html     # Quote management & follow-up tracker
```

## Dashboards

All four dashboards pull live data from Airtable via the API:

- **`dashboard.html`** — Commercial Engine overview across opportunities, quotes, and orders
- **`deal-dashboard.html`** — live deal & opportunity tracker with pipeline KPIs and stage filtering
- **`quote-tracker.html`** — quote management & follow-up tracker with overdue alerts and sortable columns
- **`order-bank.html`** — order bank with FY financial summary KPIs (Completed, Active, Total)

## Setup

### 1. Airtable token (GitHub Secret)

The Airtable Personal Access Token is **not** stored in the repo. It lives in the
`AIRTABLE_TRUCO_TOOLS` GitHub Actions secret and is injected at deploy time.

Each dashboard ships with a sentinel placeholder in its inline `AIRTABLE_CONFIG`:

```js
apiKey: "AIRTABLE_TOKEN_PLACEHOLDER"
```

On every push to `main`, `.github/workflows/deploy.yml` replaces that sentinel in each
HTML file with the secret's value, then publishes to GitHub Pages. (A verify step fails
the build if any placeholder survives injection.)

To set or rotate the token:
1. Create a Personal Access Token at https://airtable.com/create/tokens
   - Scope: `data.records:read`
   - Access: your TI Commercial Engine base
2. Update the `AIRTABLE_TRUCO_TOOLS` secret under repo Settings → Secrets and variables → Actions
3. Push to `main` (or re-run the deploy workflow) to redeploy with the new token

### 2. Fork or clone

The repo already exists at https://github.com/ericlv2020/Truco-Tools — this step is for
forking or cloning it, not initial setup.

```bash
git clone https://github.com/ericlv2020/Truco-Tools.git
```

### 3. Enable GitHub Pages

The `deploy.yml` workflow publishes the site to the `gh-pages` branch (via peaceiris),
which it **auto-creates on the first deploy** — you don't create it by hand. Point Pages
at that branch, not `main`:

1. Push to `main` once so the workflow runs and creates the `gh-pages` branch
2. Go to repo Settings → Pages
3. Source: Deploy from branch → `gh-pages` → `/ (root)`
4. Save

Your dashboards will be live at:
- `https://ericlv2020.github.io/Truco-Tools/dashboard.html`
- `https://ericlv2020.github.io/Truco-Tools/deal-dashboard.html`
- `https://ericlv2020.github.io/Truco-Tools/quote-tracker.html`
- `https://ericlv2020.github.io/Truco-Tools/order-bank.html`

### 4. Security note

The repo is **private** but GitHub Pages URLs are publicly accessible if someone has the link.
The injected Airtable token is embedded in the published HTML, so it is visible to anyone with the URL.

**Mitigation options:**
- Use a read-only Airtable Personal Access Token (scoped to `data.records:read` only)
- Share the URL only with people you trust
- Rotate the token periodically from airtable.com/create/tokens

## Field mapping

Dashboards map to these Airtable field names:

| Dashboard field | Airtable field |
|---|---|
| Opportunity Name | `Opportunity Name` |
| Stage | `Stage` |
| Total Quoted Value | `Total Quoted Value` |
| Probability | `Probability (%)` |
| Expected Closure | `Expected Closure Date` |
| Next Action | `Next Action` |
| Quote Number | `Quote Number` |
| RFQ Reference | `RFQ Reference` |
| Quote Status | `Quote Status` |
| Follow-Up Date | `Follow-Up Date` |
| Quote Age | `Quote Age` |
| Outcome | `Outcome` |
