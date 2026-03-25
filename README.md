# ⚡ El Priser — Swedish Electricity Price Dashboard

A lightweight, single-file web page for visualising real-time and historical electricity spot prices in Sweden. Built for households on dynamic (rörligt) contracts where the price changes every 15 minutes.

## What it does

- Shows electricity prices for today, tomorrow (when published after ~14:00), and any past date
- Displays the **full price you actually pay** — spot price plus variable surcharges and VAT — not just the raw spot
- Two charts:
  - **Hourly chart** — 15-minute price bars for the selected period, with the current slot highlighted and a NOW marker
  - **Daily chart** — 60-day history of min/average/max prices per day
- Min, max and current price shown at the top with spot price as a sub-label
- Tap any bar to see a full price breakdown (spot + surcharges + VAT)
- Swipe left/right on mobile to navigate between days
- Double-tap the hourly chart to zoom in on the price range
- Tap any day on the daily chart to jump to that date

## Price calculation

The total price is calculated as:

```
total = (spot + rörliga + påslag) × 1.25 (VAT)
```

Default surcharge values (Göteborg Energi, SE3):
- Rörliga kostnader: 3.85 öre/kWh // incl. elcertifikat
- Påslag: 6.90 öre/kWh // supplier margin
- Elöverföringsavgift: 6.50 öre/kWh // grid transmission
- Energiskatt:  45.00 öre/kWh  // state energy tax

These are defined at the top of `elprices.html` in the `CHARGES` object and can be updated to match your own contract.

## Data source

Prices are fetched directly from [elprisetjustnu.se](https://www.elprisetjustnu.se) — a free, open API providing 15-minute Nord Pool spot prices for all Swedish price zones (SE1–SE4). No backend or API key required.

## How to use

1. Download `elprices.html`
2. Open it in any modern browser — it works as a local file or hosted on any static web host
3. Select your electricity zone (SE1–SE4) using the dropdown — your choice is saved in the browser for next time
4. Navigate between dates using the arrow buttons or the day picker
5. Tap any slot on the chart for a detailed price breakdown

## Hosting

Since this is a single static HTML file with no backend, it can be hosted anywhere:
- **Netlify Drop** — drag and drop the file at [app.netlify.com/drop](https://app.netlify.com/drop)
- **GitHub Pages** — push to a repo and enable Pages in settings
- **Cloudflare Pages** — connect your GitHub repo

## Customising surcharges

Open `elprices.html` and find the `CHARGES` object near the top of the script:

```javascript
const CHARGES = {
  rorliga:      3.85,   // Rörliga kostnader (incl. elcertifikat)
  paslag:       6.90,   // Påslag (supplier margin)
  eloverforing: 6.50,   // Elöverföringsavgift (grid transmission)
  energiskatt:  45.00,  // Energiskatt (state energy tax)
};
```

Update the values to match your own contract. Note that `eloverforing` and `energiskatt` are shown in the tooltip breakdown but follow your supplier's billing — check whether your contract includes them in the per-kWh price or bills them separately.

## Built with

- [Chart.js](https://www.chartjs.org/) — charts
- [Moment.js](https://momentjs.com/) — date formatting
- [Bootstrap 5](https://getbootstrap.com/) — layout utilities
- [elprisetjustnu.se API](https://www.elprisetjustnu.se) — price data

## License

MIT — see [LICENSE](LICENSE)

---

*Created by Alex Svideniuk with [Claude](https://claude.ai)*
