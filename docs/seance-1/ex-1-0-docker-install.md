# 1.0 — Install n8n with Docker 🐳

**Goal**: n8n runs on your own laptop, in your browser, at `localhost:5678`.

**Time**: 15 minutes.

**Mode**: individual. Every student runs n8n **locally**, on their own machine. No shared
server, no login card. This is one reason the module uses n8n: it is open source and
self-hosted — your data stays on your computer, not on someone else's server.

!!! note "Why Docker?"
    n8n needs Node.js, a database, and some configuration to run. Docker packages all of
    that into one **container** — an isolated, ready-to-run box. You do not install Node.js
    or anything else by hand. One command, and n8n is running.

---

## CP0 — Docker is installed and running

1. Open a terminal.
2. Run:
   ```bash
   docker --version
   ```
3. You should see a version number, for example `Docker version 27.x.x`.

✅ **Done when**: the command prints a version, with no error. → CP0.

??? tip "Hint — command not found"
    Docker is not installed. Install **Docker Desktop**:

    - Mac: [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
    - Windows: same link. Docker Desktop needs **WSL2** — the installer will tell you if it
      is missing, and offer to set it up. Accept, then restart your laptop.
    - Linux: install **Docker Engine** from your distribution's package manager
      (`docker.io` on Debian/Ubuntu), then add yourself to the `docker` group so you don't
      need `sudo` for every command:
      ```bash
      sudo usermod -aG docker $USER
      ```
      Log out and back in for this to take effect.

    Do this **before** the session if you can — a laptop install is slow on shared wifi.

??? tip "Hint — Docker Desktop is installed but the command still fails"
    Docker Desktop must be **running** (the whale icon in your menu bar / system tray).
    Open the Docker Desktop app, wait for it to say "Docker Desktop is running", then
    try again.

## CP1 — Start n8n

Follow the **official n8n Docker Compose guide**:
[docs.n8n.io/hosting/installation/docker](https://docs.n8n.io/hosting/installation/docker/#docker-compose)
— it stays accurate as n8n changes, so we link to it instead of copying commands here. Use
the **Docker Compose** steps on that page (not plain `docker run`): Compose remembers your
data when you stop and restart n8n, and you'll be doing that all module.

Once you're through it:

1. Check the container is running:
   ```bash
   docker compose ps
   ```
   You should see one container, `STATUS` = `Up`.

✅ **Done when**: `docker compose ps` shows the container running. → CP1.

??? tip "Hint — port 5678 already in use"
    Something else on your laptop is already using that port. Either stop it, or change the
    port mapping in your `docker-compose.yml` (e.g. `"5679:5678"`), restart with
    `docker compose up -d`, then open `localhost:5679` instead in CP2.

??? tip "Hint — first start is slow"
    The first run downloads the n8n image (a few hundred MB). This can take a minute or two
    depending on the wifi. Every start after that is instant.

## CP2 — Open n8n and create your owner account

1. Open `http://localhost:5678` in your browser.
2. n8n asks you to create the **owner account** for this instance: email, name, password.
   This accounts stays local to your machine — you are not registering on a server
   somewhere.
3. Skip or complete the optional setup questions n8n asks on first launch — none of them
   matter for this module.
4. You should land on an empty canvas with **+ Add first step**.

✅ **Done when**: you see the empty n8n canvas. → CP2. Go to Ex 1.1.

??? tip "Hint — blank page / connection refused"
    n8n is still starting. Wait 10 seconds and reload. Still nothing? Check
    `docker compose logs -f n8n` for an error, or raise your hand.

---

## Keep in mind for the rest of the module

- **Stop n8n** at the end of a session: `docker compose stop` (keeps your workflows for next
  time). **Restart it**: `docker compose up -d`. Do **not** use `docker compose down -v` —
  the `-v` deletes your saved data.
- Your workflows, credentials, and executions all live in the `n8n_data` Docker volume on
  your laptop. Nobody else can see them. Back them up yourself if you care about them past
  the module (Settings → Download all workflows, or the n8n CLI's `export` commands).
- From Séance 3 you will connect n8n to real external services (Slack, Google, an LLM
  provider, GitHub, …) using **your own accounts**. Today you only need n8n itself running —
  no credential except n8n's own owner login.

!!! success "Finished early?"
    Click around. Double-click a node category in the search box, read what nodes exist. You
    cannot break anything — it is your own local instance, and nothing is connected yet.
