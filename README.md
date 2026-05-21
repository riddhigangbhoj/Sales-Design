# Sales Design — Kinetic Age Leads Mock

A single-file HTML mock of the Kinetic Age admin panel's **Leads** flow:

- Lead Profile card with paired fields and AI-assisted (blue) info
- **Connect & Add Info** form (customer situation/needs, customer info, online/offline + trial type, notes)
- On connect, the lead hands off to the **FSE Panel**, routed to the matching section
  (Online · Online Trial · Offline Trial)
- Collapsible FSE card with a highlighted FSE call schedule, per-card **Start Assessment** link,
  and an AI summary block

## Run locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Everything lives in `index.html`.
