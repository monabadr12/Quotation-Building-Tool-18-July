# User Guide — SI Rate Book

This guide walks through every tab in order. The tool has four tabs across the
top: **Coverage Map**, **Quotation Log**, **Generate Quote**, **Price Trends**,
and **Settings**.

---

## 1. First-time setup

1. Open the tool (either the live GitHub Pages link, or `index.html` directly).
2. Nothing needs installing — it's ready to use immediately.
3. Start with the **Quotation Log** tab to enter your first real quotation. The
   Coverage Map and Generate Quote tabs are empty until you've logged at least
   one quotation.

---

## 2. Quotation Log — entering your rate data

This is where you build up the database. Every quotation you've ever received
gets logged here.

**To add a quotation:**

1. Go to the **Quotation Log** tab.
2. In the left-hand form:
   - **Country** — type or pick from the list. If the country isn't there yet,
     just type its name; it will be added automatically as a basic entry (you can
     refine its region/coordinates later in Settings).
   - **Area / City** — where within the country the quotation applies (e.g.
     Doha, NEOM, Red Sea coast). Useful when the same country has different
     pricing by area; it's shown alongside the country in the log and in the
     benchmark panel.
   - **Date of quotation** — the date the subcontractor actually issued the rates
     (not today's date, unless that's when you received it).
   - **Currency** — the currency the rates are actually in.
   - **Exchange rate at quotation date** — how many units of that currency equal
     1 USD on the quotation's date (e.g. 3.75 for SAR). Click **"Fetch rate for
     date"** to fill it automatically from a public historical-rate dataset (GCC
     pegged currencies also have built-in fixed values); the fetched number is
     always editable, so verify it before saving. This matters because **all
     figures on the map, in benchmarks, and in generated quotes are in USD** —
     the tool converts your entered rates using this number. If a non-USD
     quotation is saved without a rate, it's flagged "no FX" in the log and its
     numbers are treated as USD until you edit and fix it.
   - **Subcontractor** — name, for your own reference.
   - **Site access type** — see the box below; this matters for Price Trends.
   - **Notes** — anything else worth remembering about this quote.
3. Scroll down to **"Rates by BOQ section."** Each of the 10 sections (General,
   Boring and Sampling, Exploratory Excavations, In-situ Testing, Groundwater
   Monitoring, Geophysical Investigations, Laboratory Soil/Rock/Chemical Testing,
   Reporting) is collapsible — click a section name to expand it.
4. Enter a rate **only for items you actually have a price for**. Leave everything
   else blank — the tool only uses what you give it.
5. Click **Save Quotation**.

> **Why "Site access type" matters:** tag each quotation as Standard, Restricted
> (airport/port/military/high-security), Urban/dense-utilities, Remote, or
> Offshore/marine. This is what lets the **Price Trends** tab later tell you
> whether a price increase was inflation or the site being harder to access. If
> you don't tag it, everything defaults to "Standard," which will blur that
> distinction later — so it's worth the extra five seconds per quote.

**To edit or delete a quotation:** find it in the table on the right and click
**Edit** or **Delete**. Editing loads it back into the form on the left.

**Bulk import from Excel:** instead of typing quotations one by one, you can
load many at once. Download the `quotations_import_template.xlsx` template
(provided with the tool package), fill one **column per quotation** — the 8
header fields (country, area, date, currency, exchange rate, subcontractor,
site access, notes) plus the item rates in the quotation's own currency — then
click **Import Excel** at the top of the page and select the file. The import
reports exactly what was loaded and flags anything it had to skip or default
(bad dates, unknown site-access values, missing exchange rates). Manual one-by-one
entry keeps working exactly as before; the two coexist. Don't modify columns A
and B of the template's Quotations sheet — the import matches rates by the item
codes in column A.

---

## 3. Coverage Map — visualizing prices worldwide

This tab shows every country on a grid-referenced world plan. Each marker is a
crosshair-and-circle symbol (styled like a borehole location symbol):

- **Solid ring** = you have a direct quotation on file for that country
- **Dashed ring** = the tool is estimating from other countries (no direct quote yet)
- **Grey hollow circle** = no data anywhere for that country yet
- **Color** (teal → amber → red) = relative cost, low to high
- **Size** = same, larger circle = higher estimated cost

**Zoom and pan:** use the **+ / − / Reset** buttons in the top-right corner of
the map, scroll the mouse wheel to zoom toward the cursor, and click-drag to pan
around when zoomed in. Country markers keep a constant on-screen size at any
zoom level.

**Benchmarking (one country at a time):** the map itself shows **only countries
where you have logged a real quotation**. To price a country, pick it from the
**"Benchmark a country…"** dropdown above the map. A benchmark panel opens below:

You can also type an **Area / City to benchmark** (e.g. Jeddah). The panel then
works through a strict priority order:

1. **Same city** — if a quotation exists for that exact city, it's used directly
   (inflation-adjusted to today). Highest priority.
2. **Another city in the same country** — e.g. you need Jeddah but only have
   Riyadh and Dammam quotations: the panel lists the cities that have data and
   lets you pick the nearest one yourself (cities are stored as text, so the tool
   can't measure distances between them — the default is simply the most recently
   quoted city). An optional % adjustment between the two cities (default 0%)
   lets you load for remote logistics, permits, or congestion; your % is saved
   for that city pair.
3. **No data in the country at all** — the panel prices it from the **nearest
   country with data** (switchable from a dropdown). The price difference
   defaults to the ratio of the two countries' **World Bank ICP price level
   indices** (shown openly in the panel), and you can type your own % instead —
   remembered for that country pair. A note reminds you the World Bank figure
   reflects the whole economy, not geotechnical works specifically.

**Download Excel (BOQ format):** every benchmark panel has a button that
generates a full Excel workbook in the exact layout of the original BOQ
template — one sheet per section (General, Boring, Exploratory, Insitu testing,
Groundwater, Geophysical, Lab Soil, Lab Rock, Chemical, Report) plus a "total"
summary sheet. The benchmark rates (USD) are filled into the Rate column;
quantities are left blank for you to enter per project, and all Amount, Sub-Total
and grand-total formulas are live, so the workbook recalculates as you type
quantities in Excel. Items without a benchmark rate stay blank. The basis of the
benchmark (source city/country, escalation, adjustment %) is written at the
bottom of the "total" sheet so the file is self-documenting.

**Two ways to view the map:**

- **Composite basket** (default) — colors the map using a fixed "sample job" — a
  small combination of common items (mobilization, drilling, sampling, a few lab
  tests). This gives one comparable number per country.
- **Single item** — pick any one of the 90 BOQ items from the dropdown (e.g. "CPT
  / PCPT" or "MASW") and the map recolors based on just that item's price,
  country by country. Use this when you want to compare one specific test across
  the world rather than a blended "typical job" price.

**Click any country marker** to open a detail panel below the map showing the
exact estimated rate for each item in the basket (or the single item, if in
single-item mode), along with the source of that estimate (direct / regional /
global — see the pricing logic explained in Generate Quote below).

**To change what's in the composite basket:** click **(edit basket)** next to
the map title, which jumps to Settings → Map Reference Basket (see Section 6).

---

## 4. Generate Quote — pricing a new bid

This is where you build an actual quotation for a project.

1. Go to **Generate Quote**.
2. **Country** — the project location.
3. **Target date** — defaults to today; change it if you're pricing for a future
   mobilization date, since inflation adjustment is calculated up to this date.
4. **Site access for this job** — if you pick something other than Standard, and
   you have enough tagged history for that access type in that country, an
   advisory box appears showing the historical premium seen for that access type
   (e.g. "+18% based on 4 item comparisons"). This is informational only — it is
   **not** automatically added to your totals, so you decide whether and how much
   to load onto specific items.
5. Click **Calculate**.
6. Expand each BOQ section and enter the **quantity** for every item your scope
   needs (this mirrors exactly how you'd fill out the original BOQ template).
7. As you type quantities, each row automatically fills in:
   - **Rate** — the estimated unit rate
   - **Source** — a colored badge:
     - **direct** — you have your own quotation for this country and item
     - **regional** — no data for this country, so it's averaged from other
       countries in the same region (adjusted by cost factor)
     - **global** — no regional data either, so it's a worldwide average
     - **none** — no data anywhere; you'll need to price this manually
   - **Amount** — quantity × rate
8. Section subtotals and the **Grand Total** update live at the bottom.
9. Click **Download CSV** to export the full priced BOQ as a spreadsheet-ready file.

> Hover over (or note) the source badge on any item — always double-check
> "regional" and "global" estimates against your own judgement before submitting
> a bid. They're a starting point, not a substitute for a real quote when one is
> obtainable.

---

## 5. Price Trends — separating inflation from site sensitivity

This tab only becomes useful once a country has **2 or more logged quotations**.

For each qualifying country, you'll see two tables:

1. **Time trend (same site-access tag)** — compares the same item quoted twice at
   different dates, *with the same access tag both times*, and works out the
   annualized % change. This is compared against the inflation % you've set for
   that country in Settings:
   - **Gap near zero** → your inflation assumption already explains the change.
   - **Large positive gap** → real-world escalation is running ahead of the CPI
     figure you're using — worth raising the inflation % for that country.
   - **Negative gap** → you may be over-escalating old quotes.

2. **Site-sensitivity premium** — compares "Standard" tagged quotes against
   Restricted/Urban/Remote/Offshore tagged quotes for the same items in the same
   country, independent of date. This gives you an average % premium for each
   access type, based purely on your own logged history.

Both tables depend entirely on the **Site access type** tag you set when logging
each quotation (Section 2). Untagged (default "Standard") quotations will not
show up correctly in the sensitivity comparison — go back and re-tag older
entries if you know they were for airports, ports, or other restricted sites.

---

## 6. Settings

**Country Rate Factors** (left panel):
- **Default inflation %** — used for any country without its own override.
- **Load reference data** — fills every country's inflation field with the
  latest available World Bank CPI figure (mostly 2024). This only fills the
  boxes on screen — nothing is saved until you click **Save Settings**, so
  review and edit any figure you don't trust first. A few countries with
  unreliable recent data (Syria, Yemen, Sudan, DR Congo, Myanmar) are left
  blank — set those manually if you have better insight.
- **Cost factor** — a relative multiplier (1.0 = normal) used only when the tool
  has to derive a price for a country with no direct quotation. Use this if you
  know, for example, that a particular country's logistics/labor costs run
  consistently higher or lower than its regional average.

**Add a Country / Location** (right panel): for any project location not already
in the built-in list. You'll need an approximate latitude/longitude (doesn't
need to be precise — it only places the dot on the map) and a **region**, which
determines which other countries it can borrow pricing from when data is
missing. You're free to type a new region name if the built-in groupings
(GCC, North Africa, etc.) don't match how your actual subcontractor pool is
organized — e.g. if one contractor covers a specific set of countries that
doesn't line up with pure geography.

**Map Reference Basket** (bottom panel): define what's in the "sample job" used
to color the Coverage Map in Composite basket mode. Set a quantity for any item
you want included (0 to exclude), then **Save Basket**. This has no effect on
Generate Quote — that always uses whatever quantities you actually type in there.

---

## Tips

- **Log real quotations as they come in**, even partial ones (rates for just a
  few items) — the pricing engine uses whatever you give it, and coverage builds
  up naturally over time.
- **Tag site access type from day one** — it costs nothing to do at entry time,
  but is very hard to reconstruct retroactively once you've forgotten which job
  was at an airport.
- **Revisit Settings periodically** — inflation rates and cost factors are your
  assumptions, not the tool's; keep them current for the countries you bid most often.

---

## 7. Moving your data between devices (Export / Import)

Your data lives in the browser of the device you entered it on. To carry it to
another device (or keep a safety backup):

**On the device that has your data:**
1. Click **Export data** (top-right of the header, next to Import data).
2. A file downloads, named like `si-rate-book-backup_2026-07-18.json`. This one
   file contains everything: all quotations, custom countries, and settings.
3. Get that file to the other device any way you like — email it to yourself,
   WhatsApp, Google Drive, USB stick.

**On the other device:**
1. Open the same tool link.
2. Click **Import data** and choose the backup file.
3. If the device already has data, you'll be asked whether to **Merge** (add the
   backup's quotations to what's already there, skipping duplicates) or
   **Replace** (wipe this device and use only the backup). If the device is
   empty, the backup just loads directly.

**Good habits:**
- Export a backup after any big data-entry session — it protects you against
  accidentally clearing browser data, not just device moves.
- The backup file is plain text (JSON) — you can store it anywhere you keep
  project files.
- This is manual sync: changes made on one device do NOT appear on another until
  you export from one and import on the other. For automatic live sync across
  devices, a cloud database backend is needed (a future upgrade).
