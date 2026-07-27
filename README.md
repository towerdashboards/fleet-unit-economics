# Fleet Unit Economics — shared dashboard

Live site: https://towerdashboards.github.io/fleet-unit-economics/

A single-page weekly unit-economics model for a vehicle fleet. Visitors enter the shared
password and their name, tune one site's levers (capacity, vehicles, utilization, miles/hour,
hourly rate, hour pools) and all 30+ P&L rates, then save the configuration as a named
**instance** shared with everyone. Any three instances can be compared side by side
(KPIs + sensitivity/breakeven charts).

## How it works

- Static page hosted on GitHub Pages (this repo, `index.html`).
- Shared instances are stored in a gist (`instances.json`) owned by @towerdashboards and
  read/written by the page via the GitHub API.
- Saving is capped at **25 instances**. The site offers no delete function.

## Admin (owner only)

- **Delete or edit instances:** open the data gist from your gists list
  (https://gist.github.com/towerdashboards) — the file `instances.json` holds an array; remove
  entries and save. The site picks it up on Refresh.
- **Change the shared password:** compute the SHA-256 hex of the new password and replace the
  `PW_HASH` constant near the top of the `<script>` in `index.html`.
- **Rotate the storage token:** generate a new classic PAT with only the `gist` scope
  (Settings → Developer settings), and re-embed it in `index.html` (`TP` constant — the token
  is stored in reversed chunks; ask your assistant to re-encode it).

## Security notes (accepted trade-offs)

- The password gate is client-side. It keeps casual visitors out; it is not real security.
- The gist write token is embedded (obfuscated) in the public page source. A technically
  skilled visitor could extract it and tamper with the data gist. If that happens, revoke the
  token in GitHub settings and rotate.
