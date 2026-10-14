# Watch Together — configured starter

This folder is configured with the Supabase **project URL and publishable key supplied by the project owner**. A publishable key is intended for browser use; do not place a Supabase secret/service-role key in this file. The app still requires proper Supabase-side authorization before public use.

## Features in this prototype

- Create a room and copy an invite link
- Join from iPhone Safari or Android Chrome
- Host-led playback sync for the included public demo MP4
- Realtime text chat
- Experimental WebRTC voice chat using a public STUN server
- Responsive dark UI

## Important limits

- This is a prototype and has **not** been deployed or live-tested against your Supabase project or your two devices.
- The included clip is a public demo video, not a movie catalog.
- It does not scrape, embed, or bypass 7Reels or protected streams. Direct 7Reels integration has not been verified.
- Room channels are not authenticated private rooms in this starter. Room IDs are unlisted identifiers, not access control. Do not use for sensitive conversations or publicly promote the app before adding authentication, private Realtime channels and server-enforced membership/host authorization.
- Voice uses STUN only. Some network pairs require a TURN relay, which may not be free.
- Chat is not persisted; refreshing the page clears the chat history.

## Deploy with GitHub Pages

1. Sign in to GitHub and create a **new repository** (for example, `watch-together`).
2. Upload `index.html`, `README.md`, and `.nojekyll` from this folder to the repository root. Do not upload private keys or passwords. The configured Supabase publishable key is intentionally client-side.
3. In the repository, open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select branch `main` and folder `/ (root)`, then save.
6. Wait for GitHub Pages to publish the HTTPS URL. This URL has not been created or verified by this setup step.
7. Open the published URL on both devices. One person selects **Create a party**, then **Copy invite link** and sends it to the other person. The second person opens the link and taps **Join party**.
8. Test chat and playback first. For voice, both people tap **Enable microphone** and allow microphone access. If the guest requested voice before the host enabled the microphone, enable the host microphone and tap the guest's microphone button again.

## Local test

Serve the folder over localhost rather than opening `index.html` directly:

```bash
python -m http.server 8000
```

Open `http://localhost:8000`. Browsers treat localhost as a secure context for microphone permissions.

## Supabase checks if connection fails

- Verify the Project URL and publishable key are from the same Supabase project.
- Check the Supabase project is active and Realtime is available.
- Inspect the browser developer console and network panel for errors.
- Realtime access rules must be reviewed before production use. This prototype uses broadcast and presence channels without a robust membership/auth layer.

## 7Reels integration

First establish whether the site permits embedding and whether its player has a supported API. Do not try to bypass framing restrictions, DRM, or access controls. If the player cannot be controlled legitimately, use an authorized HTML5 video source in this app.
