# GSOC Security Operations Dashboard

A browser-based Physical Security eTicketing System. Runs entirely on the
client (HTML/CSS/JS) with no backend or database required.

## Features
- Create security tickets
- **Import tickets in bulk from any local `.xlsx`, `.xls`, or `.csv` file**
  (loops through every row of the sheet and adds it as a ticket)
- Priority and category classification
- Ticket status tracking
- Search/filter tickets
- Dashboard counters
- Delete tickets
- CSV export
- Responsive mobile/desktop UI
- Local browser storage using `localStorage`

## Importing an Excel sheet
1. Click **Import Excel** in the header.
2. Choose any `.xlsx`, `.xls`, or `.csv` file from your device.
3. The app reads the file locally in your browser (via the [SheetJS](https://sheetjs.com/)
   library loaded from a public CDN — nothing is uploaded to any server) and
   loops through every row, adding each as a ticket.
4. Column headers are matched flexibly (case-insensitive), so sheets like
   `Ticket ID`, `Site`, `Zone/Location`, `Priority`, `Status`, `Assigned Team`,
   `Category`/`Issue Type`, and `Description`/`Closure/Notes` will map
   automatically. Unrecognized columns are ignored; missing fields fall back
   to sensible defaults (e.g. `Status` → `Open`).

## Run locally
Open `index.html` directly in a modern browser, or run a local server:

```bash
python -m http.server 8000
```

Then open http://localhost:8000

## Deploy with GitHub Pages (public URL, works on any device)

1. Create a new GitHub repository, e.g. `gsoc-ticketing-system`.
2. Upload `index.html` and `README.md`.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select the `main` branch and `/ (root)`.
6. Save.
7. GitHub publishes the site at:
   `https://<your-username>.github.io/gsoc-ticketing-system/`
8. Anyone with that link, on any device, can open the dashboard and import
   their own local Excel sheet — no installation needed.

## Important limitation

Tickets are stored only in each visitor's own browser (`localStorage`).
Excel import adds rows to that same local store — it is not synced between
devices or users. For a real multi-user GSOC system, add a backend database,
authentication, role-based access control, audit logs, server-side
validation, and secure APIs.
