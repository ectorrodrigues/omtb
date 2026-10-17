# raquelprada.com hosted player

Destination: `https://raquelprada.com/resources/omtb/player/`

1. Run `npm run build:hosted` and upload **the contents** of `dist/hosted/` into a new `resources/omtb/player/` directory under the website document root. Existing website files need not be replaced. This is a static build; no database, PHP, or private credentials are included.
2. Verify the page over HTTPS with `#queue=M7lc1UVf-VE&v=M7lc1UVf-VE` appended. YouTube must be allowed by the hosting server's CSP. Its iframe and script load from `https://www.youtube.com`; retain `strict-origin-when-cross-origin` referrer policy. Do not use a no-referrer policy, which can cause YouTube error 153.
3. Only after the page works, upload the Reddit app with `VITE_EXTERNAL_PLAYER_URL=https://raquelprada.com/resources/omtb/player/ npx devvit upload`, then install the resulting version in `omtbangs_dev`.

The Reddit app passes up to 100 public YouTube IDs and the selected title in the URL fragment. No session token is transferred. The chosen video is first, with remaining videos wrapping in order. Other queue items show discovery labels because their titles are not transferred. Reddit-native videos continue playing within Reddit.

A direct website visit or Refresh attempts the requested public Reddit JSON feed. Reddit may block that browser request; an error offers the Reddit app route, and a handoff queue remains playable without another feed fetch. The external build has no Devvit runtime dependency.

The embedded iframe remains visible if the YouTube JavaScript API fails; built-in YouTube controls can still be used. Next/previous request autoplay, but iOS may require a tap in the video. Video owners can also disallow embedding. Physical iPhone playback and the production host must be verified after upload.
