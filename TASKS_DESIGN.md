# Design spec for Uklid Rozvrh

## Stack
- Single HTML file (no build)
- Tailwind CDN
- AlpineJS or vanilla JS (vanilla for simplicity, no deps)
- localStorage for offline + data persistence
- ntfy.sh for push notifications (topic: vHCoTzxTAoRtbDV-uVdbPA)
-GitHub Pages hosting

## Routes
- `/#login` — password screen
- `/#calendar` — month view with tasks per day
- `/#tasks` — list of all tasks with edit/delete
- `/#add` — add task form
- `/#stats` — who did most tasks this month

## Auth
- Simple password "Blanicka1" stored as SHA256 hash in code
- sessionStorage keeps auth for current tab; re-login on new tab
- Not real security, but enough for family

## Data model
- Task: { id, name, icon, assignee, frequency, dayOfWeek, interval, lastDone, history[] }
- People: ["Pavel","Mamka","Blanka"]
- Frequencies: "daily", "weekly", "biweekly", "monthly", "once"
- If frequency=daily, show every day
- If weekly, show on dayOfWeek
- If biweekly, show every other week on dayOfWeek
- If monthly, show on day of month (e.g., 1st)
- If once, show on date

## ntfy integration
- Web app can manually trigger "send test notification"
- Cron job on Hermes server sends daily 9:00 AM push: "Uklid dnes: ..."
- Endpoint: POST https://ntfy.sh/vHCoTzxTAoRtbDV-uVdbPA
- Body: message text
- Title header: "Uklid rozvrh 📋"
- Priority: default
- Tags: "broom"

## Design
- Pure black + white (#0A0A0A background, #FEFEFE canvas)
- Inter variable font
- Subtle gradient accents (white fade)
- Vector SVG icons (broom, laundry, etc.)
- Smooth micro-interactions, ~200ms transitions
- Minimal, Notion-like