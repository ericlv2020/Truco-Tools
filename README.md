# truco-tools

Private repository for Truco International Limited — dashboards, scripts, and document templates.

## Structure

```
truco-tools/
├── config.js              # Airtable credentials (update API key here)
├── deal-dashboard.html    # Live deal & opportunity tracker
├── quote-tracker.html     # Quote management & follow-up tracker
├── scripts/               # Utility scripts (coming)
└── templates/             # Document templates (coming)
```

## Dashboards

Both dashboards pull live data from Airtable via the API.

### Deal Dashboard (`deal-dashboard.html`)
- Pipeline KPIs: active deals, total value, weighted value, overdue follow-ups
- Full Opportunities table with stage filtering
- Quotes table with status filtering
- Color-coded by urgency

### Quote Tracker (`quote-tracker.html`)
- All quotes with sort, filter, and search
- Overdue follow-up alerts
- Summary cards by status
- Sortable by any column

## Setup

### 1. Add your Airtable API key

Open `config.js` and replace the placeholder:

```js
apiKey: "YOUR_AIRTABLE_API_KEY_HERE"
```

Get your key from: https://airtable.com/create/tokens
Create a Personal Access Token with:
- Scope: `data.records:read`
- Access: your TI Commercial Engine base

### 2. Set up the GitHub repo

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/truco-tools.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to repo Settings → Pages
2. Source: Deploy from branch → `main` → `/ (root)`
3. Save

Your dashboards will be live at:
- `https://YOUR_USERNAME.github.io/truco-tools/deal-dashboard.html`
- `https://YOUR_USERNAME.github.io/truco-tools/quote-tracker.html`

### 4. Security note

The repo is **private** but GitHub Pages URLs are publicly accessible if someone has the link.
The API key in `config.js` will be visible to anyone with the URL.

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
