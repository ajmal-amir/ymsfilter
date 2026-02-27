# Amazon YMS — Yard Management Tool

> **Developed by Amir** &nbsp;|&nbsp; Trailer Management &nbsp;|&nbsp; Operations

A single-file web application for Amazon yard operations teams. Load your yard CSV export, instantly filter dwelling trailers, and generate a formatted shift report — all running in the browser with no installation required.

---

## 🚀 Live Demo

Deploy to GitHub Pages and access from anywhere:

```
https://<your-username>.github.io/<your-repo>/
```

---

## 📋 Features

### Tab 1 — Dwelling Filter
- Drag & drop or browse to load any yard CSV file
- Filters trailers where **Load Identifier is empty** AND **Notes is blank / OBEMPTY / OB EMPTY**
- Results sorted by **Time in Yard — longest first**
- Live search across all columns
- Click any column header to sort
- Download the filtered results as a CSV file

### Tab 2 — Shift Report
- Automatically calculates all key yard metrics from the loaded CSV
- Generates a ready-to-paste shift report in the exact format used by operations
- Configurable yard capacity and equipment numbers
- One-click **Copy to Clipboard** for the report text

---

## 🛠 How to Deploy (GitHub Pages)

1. Create a new GitHub repository (e.g. `yard-tool`)
2. Upload `index.html` to the repository root
3. Go to **Settings → Pages**
4. Under **Source**, select `main` branch and `/ (root)`
5. Click **Save**
6. Your app will be live at `https://<your-username>.github.io/yard-tool`

> The app works entirely in your browser. **No server, no backend, no installation needed.** Your CSV data never leaves your machine.

---

## 📂 Required CSV Format

The CSV must be a direct export from the yard management system and contain these exact column names:

| Column | Used For |
|---|---|
| `Notes` | Filter condition + report tagging logic |
| `Load identifier(s)` | Filter condition — must be empty to pass |
| `Time in Yard` | Sorting results longest-first |
| `Owner (Operator)` | Report — AZNG, AZNU, KAMP counts |
| `Visit Reason` | Report — Inbound/Outbound loaded counts |
| `Location` | Report — Onsite vs Offsite, Door, Home Lane |
| `Type` | Report — excludes Tractors from trailer counts |

All other columns in the CSV are preserved in the filtered output without modification.

---

## 📊 Shift Report — Metric Definitions

The report generates output in this format:

```
YC- 80.1% In / 55.5% Off
Yellow Tagged Trailers - 7
Red Tagged Trailers - 4
Kamp empty in yard  3  -  ( 2 already on door)
Empty AZNG-  18 onsite,  7 are tagged out ,  0 in the HL
Empty AZNU-  2 onsite,  2 tagged ,   2 in HL ,  1 on the way to site
Totes-  10 onsite,  3 on door,  0 in the HL
UPP-  7 onsite,  2 on door,  0 in the HL ,  0 on the way to site
Inbound loaded -  58 onsite
Outbound loaded-  40 onsite
Hostlers 16/18 available.  19/22 Day cabs available
```

### How each metric is calculated

| Metric | Calculation |
|---|---|
| **YC % In** | Onsite trailers ÷ Total Yard Capacity setting |
| **YC % Off** | PS (parking spot) trailers ÷ Total Off-Dock Spots setting |
| **Yellow Tagged** | Trailers where Notes contains `YELLOW TAGGED` (onsite) |
| **Red Tagged** | Trailers where Notes contains `RED TAGGED` (onsite) |
| **KAMP empty** | Owner = `KAMP` + Notes starts with `NIEMPTY` (onsite only) |
| **AZNG onsite** | Owner = `AZNG` + Notes = `OBEMPTY` / `OB EMPTY`, in DD/PS/HL |
| **AZNG tagged out** | AZNG empty trailers that also contain `YELLOW TAGGED` or `RED TAGGED` |
| **AZNG in HL** | AZNG empty trailers located in HL (Home Lane) spots |
| **AZNU onsite** | Owner = `AZNU` + Notes = `OBEMPTY` / `OB EMPTY`, in DD/PS/HL |
| **AZNU on way to site** | AZNU empty trailers located in OSY (offsite yard) locations |
| **Totes onsite** | Notes starts with `NITOTES` or `NITOTE`, in DD/PS/HL |
| **Totes on door** | Totes trailers in DD (dock door) locations |
| **UPP onsite** | Notes starts with `NIUPP`, in DD/PS/HL |
| **UPP on way to site** | NIUPP trailers located in OSY (offsite yard) locations |
| **Inbound loaded** | Visit Reason = `INBOUND` + has a Load ID, onsite only |
| **Outbound loaded** | Visit Reason = `OUTBOUND` + has a Load ID, onsite only |
| **Hostlers / Day Cabs** | Manually entered in the Config section |

### Location prefixes explained

| Prefix | Meaning |
|---|---|
| `DD` | Dock Door — trailer is on a live door |
| `PS` | Parking Spot — trailer is parked in the yard |
| `HL` | Home Lane — trailer is in a dedicated home lane |
| `OSY` | Offsite Yard — trailer is at an external/offsite location ("on the way to site") |

---

## ⚙️ Configuration Settings

Before generating the report, adjust these values to match your yard:

| Setting | Default | Description |
|---|---|---|
| Total Yard Capacity | 910 | Total number of spots in your yard |
| Total Off-Dock Spots (PS) | 310 | Total number of PS parking spots |
| Hostlers Total | 18 | Total hostlers assigned to your site |
| Hostlers Available | 16 | Hostlers available this shift |
| Day Cabs Total | 22 | Total day cabs assigned to your site |
| Day Cabs Available | 19 | Day cabs available this shift |

---

## 🔒 Privacy

All processing happens entirely in your browser using JavaScript. No data is uploaded to any server. No internet connection is required after the page loads (except for the Google Fonts stylesheet on first load).

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Language | HTML5, CSS3, Vanilla JavaScript |
| Fonts | Google Fonts — Rajdhani, IBM Plex Mono, Barlow |
| Dependencies | None — zero external libraries |
| Hosting | GitHub Pages (static file hosting) |

---

## 📁 File Structure

```
your-repo/
├── index.html      ← The entire application (single file)
└── README.md       ← This file
```

---

## 🐛 Troubleshooting

**"Missing columns" error**
Make sure your CSV export includes all required columns with the exact names listed above. Column names are case-sensitive.

**Filter returns 0 rows**
This means no trailers in the CSV have both an empty Load Identifier AND a blank/OBEMPTY/OB EMPTY note simultaneously. Check that your export is from the correct time period.

**Report numbers look wrong**
Verify the Location column uses the expected prefixes (`DD`, `PS`, `HL`, `OSY`). If your site uses different location codes, the onsite/offsite logic may need adjustment.

**Antivirus warning on the HTML file**
Some corporate security tools may flag locally-opened HTML files. Deploying to GitHub Pages avoids this issue entirely.

---

*Amazon YMS Yard Management Tool — Internal Use Only*
