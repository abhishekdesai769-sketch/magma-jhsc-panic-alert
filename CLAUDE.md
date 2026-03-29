# JHSC Panic Alert PWA

## Project Overview
A Progressive Web App (PWA) that serves as a panic alert button for MAGMA's JHSC (Joint Health and Safety Committee). Staff tap the button, the app captures GPS, and opens Microsoft Outlook with a pre-filled email to `panicalerts@magma-amgm.org`. The existing Power Automate flow picks up the email and handles Teams notifications, email alerts, and escalation.

## Tech Stack
- **Frontend**: Single HTML file with inline CSS and JS (zero dependencies)
- **PWA**: manifest.json + service worker for offline caching and home screen install
- **GPS**: Browser Geolocation API
- **Email**: Outlook iOS URL scheme (`ms-outlook://compose?...`)
- **Backend**: Existing Power Automate flow (untouched)
- **Hosting**: GitHub Pages (private repo)

## Key Files
- `index.html` -- The entire app (HTML + CSS + JS)
- `manifest.json` -- PWA manifest for Add to Home Screen
- `sw.js` -- Service worker for caching
- `icons/` -- PWA icons (generated)

## Architecture
```
PWA (PANIC button) -> GPS capture -> ms-outlook://compose URL scheme ->
Outlook sends email from staff's real address -> panicalerts@magma-amgm.org ->
Existing Power Automate flow (unchanged)
```

## Critical Design Decisions
1. Email MUST come FROM the staff member's real address (the flow uses `body/from` for routing adaptive cards)
2. GPS must never block the alert -- send with "Location unavailable" if GPS fails
3. Outlook URL scheme as primary, `mailto:` as fallback
4. Zero external dependencies -- everything inline in one HTML file

## Workflow instructions
When I give a vague or one-line request, ask me 2-3 clarifying questions before starting, then follow this workflow:
1. **Explore** -- find the relevant files, data model, and existing patterns
2. **Plan** -- propose the approach and wait for my approval
3. **Implement** -- make the changes in small, reviewable steps
4. **Verify** -- confirm the change works and nothing is broken
