Below is the **final, perfected L5 “Browser Veil” Protocol** – fully aligned with L0–L4, L6, and L7 (including the optional nos2x signer).

It **only** covers this layer.

Think **LEGO / IKEA manual**: follow blocks in order, tick boxes.

Two levels:

* **BASIC (MVS)** – minimum everyone does
* **ADVANCED** – local search, quarantined Chromium, optional Nostr signer (nos2x)

---

# L5 – “Browser Veil” Protocol

## 0. What You’re Building at L5

You are building **three faces of the web** on your **CLEAN LAPTOP**:

1. **SOV BROWSER (EVERYDAY)**

   * **Mullvad Browser**
   * With:

     * uBlock Origin
     * ClearURLs
     * Cookie AutoDelete
   * Default search: **Mojeek** or **local SearXNG (ADV)**

2. **COMPAT BROWSER (FALLBACK + OPTIONAL NOSTR SIGNER)**

   * **LibreWolf**
   * Same core extensions (uBlock, ClearURLs, Cookie AutoDelete)
   * Same search defaults
   * **Optionally**: one Nostr signer extension (**nos2x**, ADVANCED) in this browser *only*

3. **GHOST BROWSER (ANON)**

   * **Tor Browser**
   * **No extra extensions, no customization**

ADVANCED extras:

4. **LOCAL SEARCH NODE**

   * **SearXNG** on `http://127.0.0.1:8888`
   * Used as main search engine in Mullvad + LibreWolf

5. **QUARANTINED CHROMIUM**

   * **Ungoogled-Chromium**
   * For stubborn sites + Jitsi (as referenced in L3)
   * No logins, no stored passwords

Everything else (Chrome, Edge, Safari, Brave, etc.) = **DIRTY BROWSERS** for DIRTY devices only.

---

## 1. Prerequisites

You already have:

* ✅ L0: `my-secrets.kdbx` + master password on CLEAN LAPTOP
* ✅ L1: **CLEAN LAPTOP** (Linux, full-disk encryption) and **DIRTY devices** labeled
* ✅ L2: VPN on CLEAN LAPTOP with:

  * Auto-connect
  * Kill switch
  * DNS via VPN
* ✅ L4: `SovStack-Work` folder + backups
* ✅ L3: knows that **Ungoogled-Chromium** is the COMPAT browser for Jitsi calls
* ✅ L7: Nostr is **L7**; this layer just provides browsers + optional signer used there

You need:

* 📝 Paper + ✍️ Pen
* 💻 CLEAN LAPTOP (Debian or similar)

---

## 2. Name Your Browsing Roles (On Paper)

On paper, write:

> `L5 BROWSER VEIL MAP`
>
> **SOV BROWSER (EVERYDAY):** Mullvad Browser
> **COMPAT BROWSER (FALLBACK):** LibreWolf
> **GHOST BROWSER (ANON):** Tor Browser
> **(ADV) LOCAL SEARCH:** SearXNG at [http://127.0.0.1:8888](http://127.0.0.1:8888)
> **(ADV) COMPAT CHROMIUM:** Ungoogled-Chromium
> **(ADV L7) NOSTR SIGNER:** nos2x **only** inside LibreWolf (optional)

✅ Tick when written.

---

## 3. BASIC – Install SOV BROWSER (Mullvad Browser)

### 3.1 Download & Install

On **CLEAN LAPTOP** (VPN ON):

1. Open any existing browser.
2. Search: `Mullvad Browser download`.
3. Go to the official **mullvad.net** page.
4. Download the **Linux** Mullvad Browser.
5. Install it according to their instructions (extract + run, or `.deb`).

✅ Tick:

* [ ] Mullvad Browser downloaded from official site
* [ ] Mullvad Browser installed and starts

---

### 3.2 First-Run Settings (Minimal Changes)

Open **Mullvad Browser**:

1. Let it start normally.
2. Do **not** install extra themes, fonts, or random add-ons.
3. In settings:

   * Set language & time zone as you like, but don’t over-customize.
   * Turn off telemetry/crash reports if present.

✅ Tick:

* [ ] Mullvad Browser works
* [ ] No cosmetic/extreme customizations applied

---

## 4. BASIC – Install COMPAT BROWSER (LibreWolf)

### 4.1 Install LibreWolf

On **CLEAN LAPTOP** (VPN ON):

1. Search: `LibreWolf Linux install`.
2. Follow the official instructions (repo or `.deb` package).
3. Install LibreWolf.
4. Launch LibreWolf once to confirm.

✅ Tick:

* [ ] LibreWolf installed and opens

---

### 4.2 Quick Hardening Check

In **LibreWolf**:

1. Open **Settings → Privacy & Security**.
2. Confirm telemetry / data collection are disabled (should be by default).
3. Ensure HTTPS-only mode is on (if available).
4. Leave fingerprinting protections at default.

✅ Tick:

* [ ] LibreWolf privacy settings verified
* [ ] No random extensions or themes yet

---

## 5. BASIC – Install GHOST BROWSER (Tor Browser)

### 5.1 Download & Install

On **CLEAN LAPTOP** (VPN ON):

1. Search: `Tor Browser Linux download`.
2. Go to **torproject.org**.
3. Download Linux Tor Browser.
4. Install (usually: extract folder → run `start-tor-browser`).

✅ Tick:

* [ ] Tor Browser downloaded from official site
* [ ] Tor Browser starts and connects successfully

---

### 5.2 Write GHOST Rules

On paper, write:

> `GHOST BROWSER (Tor) RULES`
>
> 1. **VPN must be ON** before starting Tor Browser.
> 2. Never log into **real-name / KYC** accounts in Tor.
> 3. Never visit **banks**, **KYC exchanges**, or government portals in Tor.
> 4. Never install extra add-ons, themes, or fonts in Tor Browser.
> 5. Use Tor Browser only for **sensitive research, onion sites, and high-risk reading/posting**.

✅ Tick when written and taped near CLEAN LAPTOP.

---

## 6. BASIC – Core Extensions for Mullvad & LibreWolf

Install only on **Mullvad Browser** and **LibreWolf**.
**Do NOT** add anything to Tor Browser.

### 6.1 uBlock Origin

On **Mullvad Browser**:

1. Open add-ons store (Firefox-compatible).
2. Search **“uBlock Origin”**.
3. Install extension by **Raymond Hill (gorhill)**.
4. Accept default filter lists.

Repeat the same steps in **LibreWolf**.

✅ Tick:

* [ ] uBlock Origin installed in Mullvad Browser
* [ ] uBlock Origin installed in LibreWolf

---

### 6.2 ClearURLs

On **Mullvad Browser**:

1. Search add-ons for **“ClearURLs”**.
2. Install the extension.

Repeat in **LibreWolf**.

✅ Tick:

* [ ] ClearURLs installed in Mullvad
* [ ] ClearURLs installed in LibreWolf

---

### 6.3 Cookie AutoDelete

On **Mullvad Browser**:

1. Search add-ons for **“Cookie AutoDelete”**.
2. Install it.
3. On first run:

   * Enable **Auto-clean** on tab close.
   * Whitelist **only** the minimum sites that truly must stay logged in (e.g. your email or one or two key services).

Repeat in **LibreWolf**.

✅ Tick:

* [ ] Cookie AutoDelete installed in Mullvad
* [ ] Cookie AutoDelete installed in LibreWolf
* [ ] Auto-clean enabled, whitelist minimal

---

### 6.4 (Optional BASIC+) LocalCDN / Decentraleyes

If you want a bit more protection and can tolerate occasional breakage:

1. In Mullvad & LibreWolf, install **LocalCDN** or **Decentraleyes** from official add-ons.
2. Accept default settings.

If this causes weird site behavior and you hate tinkering, skip it.

✅ Tick (if used):

* [ ] LocalCDN / Decentraleyes installed (optional)

---

## 7. BASIC – Private Search Defaults (Mojeek)

### 7.1 Set Mojeek as Default

In **Mullvad Browser**:

1. Visit `https://www.mojeek.com/`.
2. Add Mojeek as a search engine.
3. Set **Mojeek** as default.

In **LibreWolf**:

1. Same: open Mojeek.
2. Add and set Mojeek as default search.

✅ Tick:

* [ ] Mojeek is default search in Mullvad
* [ ] Mojeek is default search in LibreWolf

---

### 7.2 Optional Backup Engine

You can add one fallback engine (a different privacy-friendly engine) and use it manually for difficult queries.

**Rule:**
Mojeek stays default; backup engine is used only when needed.

✅ Tick (optional):

* [ ] Secondary engine added as backup (not default)

---

## 8. BASIC – Daily Browsing Workflow

On paper, write:

> `L5 DAILY BROWSER RULES`
>
> 🟢 **EVERYDAY SOV MODE**
> – Use **Mullvad Browser**.
> – VPN ON (L2).
> – uBlock Origin + ClearURLs + Cookie AutoDelete enabled.
> – Default search = **Mojeek** (or local SearXNG once configured).
> – Use for: reading, research, SovStack docs, Bitcoin content, Nostr info (not KYC logins).
>
> 🟡 **COMPAT MODE**
> – Use **LibreWolf** only when a site misbehaves in Mullvad.
> – Same extensions, same search defaults.
> – No KYC logins, no legacy social media.
> – (ADV L7) Optionally, LibreWolf carries the **nos2x Nostr signer** for web Nostr usage.
>
> 🔴 **GHOST MODE**
> – VPN ON + **Tor Browser**.
> – For highly sensitive topics, onion services, controversial reading/posting.
> – Never for real-name accounts, KYC sites, or banking.

✅ Tick when written and posted near CLEAN LAPTOP.

---

## 9. BASIC – “NEVER DO THIS” (L5)

On paper, write:

> `L5 – NEVER DO THIS`
>
> 1. Never install or use **Chrome, Edge, Safari, Brave** on the CLEAN LAPTOP.
> 2. Never log into **Google / Apple / Microsoft accounts** in Mullvad, LibreWolf, or Tor on CLEAN LAPTOP.
> 3. Never log into **banks, KYC exchanges, or government portals** in Mullvad, LibreWolf, or Tor.
>    – Those live only on **DIRTY devices**.
> 4. Never install random extensions beyond:
>    – uBlock Origin
>    – ClearURLs
>    – Cookie AutoDelete
>    – (Optional) LocalCDN / Decentraleyes
>    – (ADV) **nos2x in LibreWolf only**, if you explicitly choose it
> 5. Never customize **Tor Browser** (no new extensions, themes, or fonts).
> 6. Never store passwords in browser managers.
>    – All secrets stay in **KeePass** (L0).
> 7. Never paste a Nostr `nsec` into any website or generic browser field.

✅ Tick when written and visible.

---

## 10. ADVANCED – Local SearXNG (Local Search Node)

This makes your CLEAN LAPTOP act as its own search proxy.

### 10.1 Install Docker

On CLEAN LAPTOP:

```bash
sudo apt update
sudo apt install docker.io docker-compose
sudo systemctl enable docker
sudo systemctl start docker
```

✅ Tick:

* [ ] Docker + docker-compose installed and running

---

### 10.2 Create SearXNG Folder & Config

In terminal:

```bash
mkdir -p $HOME/searxng
cd $HOME/searxng
nano docker-compose.yml
```

Paste:

```yaml
version: "3"

services:
  searxng:
    image: searxng/searxng:latest
    restart: unless-stopped
    ports:
      - "127.0.0.1:8888:8080"
    volumes:
      - ./searxng:/etc/searxng
    environment:
      - SEARXNG_BASE_URL=http://127.0.0.1:8888/
```

Save and exit.

✅ Tick:

* [ ] `docker-compose.yml` created under `~/searxng`

---

### 10.3 Start SearXNG

```bash
cd ~/searxng
docker-compose up -d
```

Then open **Mullvad Browser** and visit:

* `http://127.0.0.1:8888`

You should see SearXNG’s search interface.

✅ Tick:

* [ ] SearXNG reachable at `http://127.0.0.1:8888`

---

### 10.4 Set SearXNG as Default Search

In **Mullvad Browser**:

1. Go to `http://127.0.0.1:8888`.
2. Add this as a search engine.
3. Set **SearXNG (127.0.0.1)** as **default**.
4. Keep **Mojeek** as backup.

Repeat these steps in **LibreWolf**.

✅ Tick:

* [ ] SearXNG set as default in Mullvad
* [ ] SearXNG set as default in LibreWolf
* [ ] Mojeek kept as backup engine

---

### 10.5 Start/Stop Cheatsheet

Write down:

```bash
# Start SearXNG
cd ~/searxng
docker-compose up -d

# Stop SearXNG
cd ~/searxng
docker-compose down
```

✅ Tick:

* [ ] SearXNG start/stop commands written down

---

## 11. ADVANCED – Quarantined Ungoogled-Chromium (COMPAT-ONLY)

Ungoogled-Chromium is a **sandbox browser** for stubborn sites and Jitsi (as in L3).

### 11.1 Install Ungoogled-Chromium

On CLEAN LAPTOP (VPN ON):

1. Search: `Ungoogled Chromium Debian install` (or for your distro).
2. Use official or well-documented method (repo, Flatpak, or `.deb`).
3. Install and open once.

✅ Tick:

* [ ] Ungoogled-Chromium installed and starts

---

### 11.2 COMPAT-ONLY Rules

In **Ungoogled-Chromium**:

1. Do **not** log into a Google account.
2. Do **not** sync anything.
3. Optionally install **uBlock Origin** and nothing else.
4. No password storage.

On paper, write:

> `UNGOOGLED-CHROMIUM = COMPAT ONLY`
>
> – Use only when a site fails in Mullvad + LibreWolf.
> – Use for **Jitsi** group calls (as in L3).
> – No Google account, no KYC, no long-term logins.
> – No password saving.

✅ Tick when written.

---

## 12. ADVANCED – Nostr Signer (nos2x in LibreWolf Only)

**This is optional.**
If you don’t need Nostr web frontends, **skip this entire section**.

If you **do** want to log into Nostr web apps (e.g. aggregator sites) without ever pasting `nsec` into websites, you can use nos2x **only in LibreWolf** as a Nostr signer.

### 12.1 Precondition: Key Handling

From L0/L7:

* Your Nostr private key (`nsec…`) is a **secret**:

  * Stored in KeePass (`my-secrets.kdbx`)
  * Backed up with L4
  * **Never** pasted into websites, emails, or random fields

nos2x is allowed to hold:

* Either your **main `nsec`** (if you’re comfortable)
* Or preferably a **separate pseudonymous key** dedicated to web usage

---

### 12.2 Install nos2x in LibreWolf

In **LibreWolf**:

1. Open the official extension source for **nos2x** (Firefox-compatible).
2. Install nos2x.
3. Do **not** install it in Mullvad or any other browser.

✅ Tick:

* [ ] nos2x installed **only** in LibreWolf

---

### 12.3 Import Nostr Key Into nos2x (Once)

1. Open KeePass on CLEAN LAPTOP.
2. Find your Nostr key entry:

   * e.g. `Nostr – PUBLIC ID` + `Nostr – PRIVATE nsec`
3. In LibreWolf, open **nos2x** options.
4. When it asks for your secret key, **carefully copy** the `nsec…` from KeePass and paste it into nos2x.

Then:

* Confirm nos2x shows a public key that matches your intended Nostr identity.
* Delete the clipboard contents (KeePass auto-clears; you can also overwrite manually).

✅ Tick:

* [ ] Nostr `nsec` imported into nos2x only
* [ ] No direct `nsec` pastes into any website

**Rule:** From now on, **you never again paste `nsec` into any web form**.

---

### 12.4 Use nos2x With Nostr Web Apps

When you visit a Nostr web client in **LibreWolf**:

1. The site will ask to connect to nos2x.
2. nos2x will show a confirmation prompt:

   * Approve only if you trust that site for signing.
3. The web app can now request signatures for:

   * Logins
   * Posts / likes / zaps, etc.

You are granting:

* “This site can ask nos2x to sign messages with my Nostr key.”
* The site **never sees your `nsec`** directly; it sees only signatures.

**Hard Rules:**

* Only LibreWolf gets nos2x.
* Mullvad + Tor stay **nos2x-free**.
* Never approve nos2x for random or unknown web apps.

✅ Tick:

* [ ] Confirmed: only LibreWolf + trusted sites use nos2x
* [ ] No `nsec` pasted into websites

---

### 12.5 nos2x “NEVER DO” Addendum

On paper, append to L5 NEVER DO list:

> – Never install nos2x in Mullvad or Ungoogled-Chromium.
> – Never paste `nsec` directly into any Nostr web client.
> – If nos2x or LibreWolf are compromised, **rotate Nostr key**:
> – Generate new key
> – Update identity where needed
> – Revoke trust in old key

✅ Tick when added.

---

## 13. L5 Checklists (Weekly / Monthly)

### Weekly (10–15 minutes)

On **CLEAN LAPTOP**:

* [ ] Confirm VPN auto-connects before browsing.
* [ ] Open **Mullvad Browser** → do a quick search via SearXNG/Mojeek.
* [ ] Open **LibreWolf** → ensure it works and extensions are active.
* [ ] Open **Tor Browser** → confirm it still connects.
* [ ] If using SearXNG:

  * Run `docker ps` and check SearXNG container is present when needed.
* [ ] If using nos2x:

  * Open a Nostr web app in LibreWolf, confirm signer still works (optional quick test).

---

### Monthly (15–20 minutes)

* [ ] Update browsers:

  * Mullvad
  * LibreWolf
  * Tor Browser
  * Ungoogled-Chromium
* [ ] Check extensions:

  * uBlock, ClearURLs, Cookie AutoDelete (and LocalCDN/Decentraleyes if you use them) are still installed and enabled.
* [ ] Verify:

  * **No new extensions** appeared in Mullvad/LibreWolf.
* [ ] If using SearXNG:

  * Update image:

```bash
cd ~/searxng
docker-compose pull
docker-compose up -d
```

* [ ] Confirm there is still **no Chrome/Edge/Safari/Brave** on CLEAN LAPTOP.
* [ ] If nos2x is used:

  * Review connected Nostr sites; revoke any you no longer trust.

---

## 14. Emergency Branches (L5)

### Case 1 – KYC / Google / Legacy Social Login in Mullvad/LibreWolf

If you log into **Google / Facebook / Twitter / KYC exchange / bank** inside Mullvad or LibreWolf:

1. Treat that browser profile as **contaminated**.

2. Easiest repair:

   * Uninstall that browser completely.
   * Reinstall and reapply L5 hardening (extensions + settings).

3. Or reassign that browser as **DIRTY** and only use the other as CLEAN.

---

### Case 2 – Site Demands Chrome/Edge

If a site refuses to work except with Chrome/Edge:

1. Use a **DIRTY device** with its DIRTY browser.
2. Do **not** install Chrome/Edge on CLEAN LAPTOP.
3. As an absolute last resort for SovStack–necessary stuff:

   * Use Ungoogled-Chromium (COMPAT-ONLY rules) on CLEAN LAPTOP, with no accounts and no stored secrets.

---

### Case 3 – SearXNG Fails

If `http://127.0.0.1:8888` stops working:

1. Switch default search back to **Mojeek** in Mullvad & LibreWolf.
2. Fix or rebuild SearXNG later; browsing continues via Mojeek.

---

### Case 4 – nos2x or LibreWolf Compromise

If you suspect nos2x or LibreWolf is compromised:

1. Immediately remove the extension and/or uninstall LibreWolf.
2. Generate a **new Nostr keypair** (via a trusted client).
3. Update your Nostr identity where needed.
4. Mark the old key as revoked/abandoned (in bios where applicable).
5. Recreate nos2x setup only if you truly need web sign-in.

---

## 15. Final Micro-Checklist (Caveman Version)

L5 “Browser Veil” is live if:

1. [ ] **Mullvad Browser** is the main SOV browser on CLEAN LAPTOP with:

   * uBlock Origin
   * ClearURLs
   * Cookie AutoDelete
   * Default search = local **SearXNG** or **Mojeek**

2. [ ] **LibreWolf** is the COMPAT browser with the same three core extensions and same search defaults.

   * If you chose: **nos2x** is installed **only here** as Nostr signer.

3. [ ] **Tor Browser** is the GHOST browser, used only with VPN ON and never for KYC/real-name logins.

4. [ ] **Ungoogled-Chromium** exists only as **COMPAT-ONLY** (Jitsi, stubborn sites), with no accounts and no saved passwords.

5. [ ] No Chrome/Edge/Safari/Brave exist on CLEAN LAPTOP; those live only on DIRTY devices.

6. [ ] L5 DAILY RULES and L5 NEVER DO lists (including nos2x addendum if used) are written and taped near CLEAN LAPTOP.

7. [ ] Weekly & monthly checks are done; SearXNG (if used) is running; extensions remain minimal and known.

If all 7 boxes are true, **L5 Browser Veil** is wrapped around your **L2 Network Cloak**, **L1 Device Shell**, and **L0 Secret Box**, and is consistent with **L3**, **L4**, **L6**, and **L7**.
