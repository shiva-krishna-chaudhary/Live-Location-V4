# Live Location Server — Quick Run & Test

Short guide to run the project locally and test live location sharing from mobile and desktop.

## Prerequisites
- Node.js (v14+)
- Optional: `ngrok` (for exposing a local HTTPS URL)

## Notes
- I changed the socket client to use the same origin (`const socket = io();`) in `public/index.html`. This lets the client connect back to whichever origin serves the page (local or the ngrok HTTPS URL).

## Run locally
1. Start the app:

```bash
node server.js
```

2. Open the app on your laptop at:

```
http://localhost:3000
```

3. If you open the page via `file://` or plain HTTP on some mobile browsers, the Geolocation API may be blocked. Use an HTTPS origin for mobile testing.

## Expose with ngrok (recommended for mobile testing)
1. Install/run ngrok (if not installed you can use `npx`):

```bash
npx ngrok http 3000
```

2. ngrok will print an HTTPS URL like `https://abcd-1234.ngrok.io`. Open that HTTPS URL on both your laptop and mobile.

3. On the mobile page, enter a name in the `userName` field and tap **Start Sharing**. On the laptop, open the same HTTPS URL and you should see the mobile marker appear.

## What to check if it doesn't work
- Make sure you tapped **Start Sharing** on the mobile client. The app only emits location while `sharing` is true.
- Allow the browser's location permission prompt.
- If you see `Geolocation API only allowed in secure contexts` in the console, use an HTTPS origin (ngrok or a proper TLS server).
- Check the server terminal for socket connection logs. `server.js` logs connection events.

## Troubleshooting commands

Start server (logs printed to terminal):

```bash
node server.js
```

Stop with Ctrl+C.

Expose with ngrok:

```bash
npx ngrok http 3000
```

Open the HTTPS URL printed by ngrok on both devices.

---
If you want, I can also:
- add these instructions into a short `Makefile` or npm `scripts`,
- run the server locally and start an ngrok tunnel for you now.
