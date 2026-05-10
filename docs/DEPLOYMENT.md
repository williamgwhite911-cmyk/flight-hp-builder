# Deployment

## First-Time GitHub Pages Setup

Run this once. After it's set up, every `git push` redeploys automatically.

```bash
# 1. Initialize git in the repo folder
git init -b main
git add .
git commit -m "Initial commit"

# 2. Create the GitHub repo and push
gh repo create flight-hp-builder --public --source=. --push \
  --description "AI-generated, compliance-checked H&P paragraph for flight crew transports"

# 3. Enable GitHub Pages
gh api -X POST "repos/{owner}/flight-hp-builder/pages" \
  -f "source[branch]=main" -f "source[path]=/"

# 4. Confirm the URL (give it 30-60 seconds to build)
gh api "repos/{owner}/flight-hp-builder/pages" --jq .html_url
```

The URL will be `https://<your-username>.github.io/flight-hp-builder/`.

## Updating the App

Whenever the app changes:

```bash
git add .
git commit -m "Update <what changed>"
git push
```

GitHub Pages redeploys in about 60 seconds.

## Installing on iPhone / iPad

1. Open the GitHub Pages URL in **Safari** on your device.
2. Tap **Share**, then **Add to Home Screen**.
3. Confirm name and tap **Add**.

The app icon (a white "H" with purple AI accent on dark blue) lands on the home screen and opens fullscreen.

## Installing on Android

1. Open the URL in **Chrome**.
2. Tap the three-dot menu, then **Install app** or **Add to Home Screen**.

## Notes

- The app is fully client-side. GitHub Pages just serves static files.
- API keys are stored in each device's localStorage, not on GitHub.
- AI calls go directly from the browser to api.anthropic.com.
- Distance calls go directly from the browser to maps.googleapis.com.
- Updating the manifest or icons may require clearing the home-screen install and re-adding it for the new icon to take effect on iOS.
