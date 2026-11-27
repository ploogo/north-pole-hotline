# north-pole-hotline

A one-page "call Santa" app for little kids. Tap the big red phone and Santa answers by voice, powered by an ElevenLabs voice agent.

## How it works

- **Kids** tap the red button. The browser asks for the microphone, then Santa picks up right on the page. Tap the green button to hang up.
- **Grown-ups** tap "Grown-ups only", solve a quick math question, and fill in Santa's report: the child's first name, a nice-list check, what they've done well, what to work on, and secret gift notes. Santa says his elves told him, never that the parents did.
- The report is saved in the browser on that device (localStorage). Nothing is stored on a server. It is sent to ElevenLabs only as dynamic variables when a call starts.
- **Calls left today** shows something like 15/20 under the dial. The page has no server to ask ElevenLabs, so it counts calls connected on that phone since local midnight. Calls from the other phone don't show up in it.
- **Sharing between phones:** "Share report link" in the report form makes a link with the report packed into the URL hash (`#r=...`). Open it on the other phone and tap "Use this report". The hash never reaches GitHub's servers, but the link stays in whatever app you send it through. Secret gift notes are never put in the link, and importing keeps any gift notes already on the receiving phone.

## Pieces

- `index.html`: the whole app, no build step. The hand-drawn illustrations (Santa on the phone, elf, snowman, reindeer, walking telephone) were generated with Higgsfield and are embedded as WebP data URIs, so the page is still a single file.
- ElevenLabs agent: `agent_2401m8ck8rcfe6gtr22wvtc4ms4c` ("Santa Hotline (North Pole)"). Its prompt uses the variables `child_name`, `nice_status`, `parent_report`, `encourage`, and `gift_notes`.
- Browser SDK: `@elevenlabs/client@1.35.0` from jsDelivr.
- The agent only accepts calls from `ploogo.github.io` (allowlist) and is capped at 20 calls a day. There is no fallback link to ElevenLabs' hosted talk-to page, since the allowlist blocks it.

## Hosting

Served with GitHub Pages from the `main` branch root.
