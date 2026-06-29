# beneco-outage-monitor

BENECO power interruption monitor for the Philippine Science High School CAR Campus (Irisan, Baguio City). A lightweight, standalone HTML widget that fetches weekly scheduled outage notices and flags announcements affecting the campus area. No dependencies. Embeddable.

---

## Purpose

[BENECO](https://www.beneco.com.ph) (Benguet Electric Cooperative) serves Baguio City and Benguet province and publishes weekly scheduled power interruption notices. These notices list affected areas by barangay, purok, and landmark — but monitoring them manually requires checking the BENECO website or Facebook page regularly.

This tool automates that monitoring for a specific area of interest. It is designed for the Philippine Science High School CAR Campus in Irisan, Baguio City, but can be adapted for any location within BENECO's service area.

---

## How it works

```
BENECO (beneco.com.ph)
    └── publishes weekly schedules as PDF advisories
            └── Baguio City Guide (baguiocityguide.com)
                    └── republishes as structured HTML articles
                            └── exposes articles via WordPress REST API (public, no auth)
                                    └── beneco_monitor.html
                                            └── fetches articles every 3 hours
                                            └── parses interruption table (date, areas, purpose)
                                            └── filters to current week and next week
                                            └── scans for monitored keywords
                                            └── displays alert if match found, clear status if not
```

The widget runs entirely in the browser. There is no backend, no server, and no installation required.

**Limitation:** Baguio City Guide typically publishes the weekly BENECO schedule a few days in advance. Same-day unscheduled outages are not captured by this tool — for those, monitor the [BENECO website](https://www.beneco.com.ph/) directly.

---

## Usage

### Download and open

1. Download `beneco_monitor.html` from this repository.
2. Open it in any modern web browser. No internet server needed — it runs as a local file.

### Embed in a webpage

To embed the widget inside an existing webpage or portal:

```html
<iframe
  src="beneco_monitor.html"
  width="100%"
  height="400"
  frameborder="0"
  scrolling="auto">
</iframe>
```

If hosted on a web server, replace `beneco_monitor.html` with the full URL to the file.

---

## Modifying monitored keywords

Open `beneco_monitor.html` in any text editor and find this line near the top of the `<script>` section:

```js
const KEYWORDS = ['irisan', 'purok 12', 'philippine science', 'pshs'];
```

Edit the list to match your area. Each entry is a keyword that will be searched for (case-insensitive) in the full text of each interruption notice. Add, remove, or replace entries as needed. For example, for a different location:

```js
const KEYWORDS = ['bakakeng', 'purok 5', 'my school name'];
```

Save the file. The change takes effect the next time the page loads.

---

## Other settings

| Line | Setting | Default |
|---|---|---|
| `const REFRESH_MS = 3 * 60 * 60 * 1000;` | Auto-refresh interval | Every 3 hours |

To change the refresh interval, edit the numbers. For example, every 30 minutes:

```js
const REFRESH_MS = 30 * 60 * 1000;
```

---

## License

Open source · [MIT License](https://opensource.org/licenses/MIT) · Copyright © 2026 Ricarido Saturay, Jr.  
Developed with AI assistance (Claude by Anthropic).
