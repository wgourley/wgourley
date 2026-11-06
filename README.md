## William Gourley

I run a small self-hosted estate on Linux and do most of the work on it myself — the applications, the server, the mail, and the monitoring that tells me when any of it stops.

### What I run

- **An e-commerce shop** — Bagisto on Laravel, with a custom theme and a number of controller and template overrides kept outside the vendor tree.
- **A community forum** — Flarum, restructured from 19 categories down to 8 without losing a thread.
- **A helpdesk** — UVdesk on Symfony, with app-level template overrides.
- **An internet radio and TV station** — AzuraCast, AVideo and ffplayout, running in Docker.
- **A phone system** — FreePBX in Docker, behind a locked-down SIP allow-list.
- **The mail for five domains** — Mailu, relaying through a transactional provider after a deliverability block.

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

### Here

What I publish here is the generic half of that work — the parts that are useful to someone else and safe to share. Infrastructure configuration stays private, for obvious reasons.
