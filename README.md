# Flight Crew H&P Builder

A single-page web app that generates a compliance-checked History and Physical paragraph for flight crew transports. Designed for iPhone, iPad, and desktop browsers.

## Features

- **Two modes**: Interfacility (IFT) and Scene Call. The form fields adjust based on mode.
- **Indiana hospital dropdown** with 95+ facilities organized by system (IU Health, Franciscan, Ascension St. Vincent, Community, Parkview, Northwest Health, Memorial, Methodist Hospitals, Beacon, and many more), with auto-fill of street addresses.
- **Indiana county EMS dropdown** covering all 92 counties plus Indianapolis Fire EMS, Three Rivers Ambulance, Wishard/Eskenazi EMS, and others.
- **Twelve time-sensitive condition flags**: STEMI, MI/NSTEMI, LVO Stroke, Stroke (general), GSW, Trauma/hemorrhage, Status Epilepticus, Sepsis, Surgical emergency, Aortic dissection, Refractory respiratory failure, OB/neonatal emergency.
- **Transcript / Voice Memo extraction**: paste any sending facility report, dispatch transcript, or voice-memo transcription, and AI extracts structured data and pre-fills the form.
- **Distance and time calculation** via Google Maps Distance Matrix API for ground transport, with great-circle distance via haversine formula and air time estimate at 135 mph cruise.
- **Two AI-generated outputs**:
  - Page 1: Reason for Transport / H&P Narrative paragraph that meets all 12 Web Manual compliance criteria.
  - Page 2: Structured "StatFlight XXXXX was requested by..." template with full handoff details.
- **Compliance checklist** that runs against every generated narrative and flags met / missing / partial criteria.
- **Click-to-edit** outputs and copy-to-clipboard buttons.
- **Settings** stored locally on each device: API keys, model selection (Claude Haiku 4.5, Sonnet 4.6, Opus 4.6).

## Install on iPhone or iPad

1. Open the GitHub Pages URL in **Safari** on the device.
2. Tap the **Share** button.
3. Tap **Add to Home Screen**.
4. The app icon appears on your home screen and runs fullscreen.

On Android, use Chrome and the equivalent install option.

## Setup (One-Time Per Device)

The app needs an Anthropic API key for AI generation. The form, dropdowns, and manual entry all work without it.

1. Get a key at [console.anthropic.com](https://console.anthropic.com) -> Settings -> API Keys.
2. Optionally, get a Google Maps API key at [console.cloud.google.com](https://console.cloud.google.com) for automatic distance calculation. Enable Distance Matrix API and Geocoding API.
3. Open the installed app, tap the **gear icon** at top right.
4. Paste your key(s), pick a model, and Save.

Keys are stored only in your device's browser localStorage. They are sent only to api.anthropic.com (for AI) and maps.googleapis.com (for distance) when you press the corresponding buttons.

## HIPAA Notice

Sending Protected Health Information to a public AI API requires a signed Business Associate Agreement (BAA) with Anthropic. The Settings panel shows this warning every time it opens. Do not run AI extraction or generation on live patient data until your BAA is in place. For training, education, or de-identified content, no BAA is needed.

## Compliance Criteria

Every generated H&P narrative is checked against twelve criteria from the Web Manual requirements:

1. Who requested transport (name + title)
2. Requesting Agency / Facility
3. Requesting Provider (full name + credentials)
4. Clinical services NOT available at pickup location
5. Patient's summarized condition / diagnosis
6. Time-dependent illness flag
7. Mode of transport rationale
8. Air transport considerations (CCN-level care, ground ALS limits)
9. Ground time per Google Maps
10. Receiving destination + capabilities
11. Bypassed facility explanation (if applicable)
12. HPI: symptoms, history, events, interventions PTA

Each criterion shows met (green check), missing (red X), or N/A (grey dash) after generation.

## Privacy

- The form, dropdowns, copy buttons, and template generation all run in your browser. No data leaves the device unless you press an AI or distance button.
- AI generation sends only the form data + transcript text you've entered.
- Distance calculation sends only the addresses or coordinates you've entered.
- Your API keys are stored in localStorage on your device and never transmitted anywhere except to the respective API endpoints.
- Nothing is sent to GitHub, analytics services, or any third party.

## Disclaimer

The compliance checklist, hospital list, county EMS list, and clinical content in this app are reference values curated for typical flight nurse use. Verify against your service's protocols, your medical director's standing orders, and the actual patient before charting or transport. The hospital list is current as of typical Indiana facility roster but facilities open, close, and rename — verify before relying on a specific facility name.

## License

This is a personal tool. Use at your own risk. See LICENSE.

## Tech

- Vanilla HTML / CSS / JavaScript. No build step. Single file (plus icons + manifest).
- Anthropic Claude API for AI generation and transcript extraction (direct browser calls via `anthropic-dangerous-direct-browser-access` header).
- Google Maps Distance Matrix and Geocoding APIs for distance/time calculation.
- Designed mobile-first; tabbed layout on phones, two-pane layout on desktop and tablet.
