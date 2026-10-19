# Axzora Super App — landing page

The public front door for the Axzora Super App (Happy Paisa on BNB Smart Chain),
and a one-page directory of everything else in the ecosystem.

This repo is a **single static `index.html`**: no build step, no dependencies, no
fonts or scripts loaded from third parties. Open it directly, or serve the folder.

```bash
python3 -m http.server 8000     # http://localhost:8000
```

It also works from `file://` (all CSS and JS are inline), which is how it is used
inside the AxzoraOS WebView.

## What is on the page

| Section | Notes |
|---|---|
| Hero + token facts | HP address, USDT address, chain id 56, reference price |
| What the app does | Mint/burn/transfer, staking, pricing, voice, biometrics, wallet |
| Ecosystem | AxzoraOS, Axzora Server, Axzora Ludo, Axzora Docs |
| Token facts table | Copy-pasteable addresses; verify before signing |
| Quick start | Super app clone/run, plus APK sha256 + signing cert prefix |
| Live status | Fetches the OTA manifest and the Ludo `/health` **from your browser** |

## Live status behaviour

Two probes run on load, each with an 8 s `AbortController` timeout:

- `https://axzora-server-k39z.onrender.com/update/check` → expected `18.18 · code 210`
- `https://axzora-ludo.onrender.com/health` → expects `{"ok":true, …}`

States are honest rather than decorative: `online`, `not deployed` (404),
`http <code>`, `timed out`, or `unreachable` (network/CORS). A service with no
running instance is reported as **not deployed** — it is never faked.

## Design notes

- Dark by default, system font stack, no external requests except the two probes.
- Theme toggle persists in `localStorage` under `axzora.theme`; light theme is a
  full token set, not an inverted filter.
- Accessible: visible focus rings, `aria-live` on the status region, real
  `<table>` semantics, reduced-motion support.

## Replaced content

The repo previously contained a generic **"Aurora Studio"** agency template:
placeholder copy, an invented team, and a contact form that faked success with a
`setTimeout` ("Request sent!") without sending anything. That fake form is gone —
nothing on this page pretends to submit data.

## Related

- App: <https://github.com/axzoraharry/axzora-super-app>
- APK channel: <https://github.com/axzoraharry/axzora-ota/releases>
- Docs: <https://axzoraharry.github.io/axzora-docs/>

MIT.
