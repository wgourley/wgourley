# William Gourley

I run a small self-hosted estate on Linux and do most of the work on it myself — the applications, the server, the mail, and the monitoring that tells me when any of it stops.

### What I run

- **An e-commerce shop** — Bagisto on Laravel, with a custom theme and a number of controller and template overrides kept outside the vendor tree.
- **A community forum** — Flarum, restructured from 19 categories down to 8 without losing a thread.
- **A helpdesk** — UVdesk on Symfony, with app-level template overrides.
- **An internet radio and TV station** — AzuraCast, AVideo and ffplayout in Docker, with a 24/7 playout channel feeding the live player.
- **An IVR phone system** — FreePBX in Docker, behind a locked-down SIP allow-list.
- **The mail for five domains** — Mailu, relaying through a transactional provider after a deliverability block.
-  **A personal payments portal - FossBilling, customised layout and content for my needs.

All of it sits behind nginx and Cloudflare on a single VPS, with PHP-FPM, MySQL and a nightly encrypted backup to off-site storage.

### What I work on

Most of my time goes on the unglamorous half: deliverability, caching, backups, access control, and making failures visible.

- Laravel and Bagisto customisation without touching `packages/`
- SPF, DKIM, DMARC, SRS, and relay configuration
- nginx virtual hosts, real-IP handling, and maintenance gating
- Cron, scheduled tasks, and health monitoring
- Content-based file validation rather than trusting extensions or declared MIME types

### One thing I have learned the hard way

**A check that runs, fails, and tells nobody is worse than no check at all**, because it buys you confidence you have not earned.

I have found this on the same estate more times than I would like: a reload reporting success while cycling no workers; a log level quietly discarding the instrumentation meant to debug a fault; backups producing a 3 KB archive for three days after a site moved; a scheduler that had never run at all. Every one of them looked fine from the inside.

So anything that matters now pings an external monitor on success, and goes red when it stops. The monitor is outside the thing it watches, on purpose.

### Upstream

- **AVideo** — traced a bug where opening the Encoder silently logged users out of the main site (a stylesheet endpoint was replacing the session cookie). Reported with the root cause; fixed in v29.7.0.

### Here

What I publish here is the generic half of that work — the parts that are useful to someone else and safe to share. Infrastructure configuration stays private, for obvious reasons.
- [avideo-tweaks](https://github.com/wgourley/avideo-tweaks) — drop-in browser fixes for AVideo
- [vps-scripts](https://github.com/wgourley/vps-scripts) — Docker firewall, verified encrypted backups, monitoring, update-safe patches
- [ffplayout-avideo-live](https://github.com/wgourley/ffplayout-avideo-live) — run a 24/7 TV channel with ffplayout and AVideo Live
- [brand-kit-generator](https://github.com/wgourley/brand-kit-generator) — a complete logo package from one badge image

### Contact

Website design and builds, VPS setup and hardening, and AzuraCast, AVideo and FreePBX installs — [williamgourley.com](https://williamgourley.com)
