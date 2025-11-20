Below is the **L7 “Signal Rail” Protocol** – **only this layer**, nothing else.
It **sits on top of L0–L6** (Secret Box → Device Shell → Network Cloak → Comms Veil → File Spine → Browser Veil → Sats Circuit).

Think **IKEA / LEGO manual**: boxes to tick, simple steps, no guesswork.
Only **Nostr** (no SSB, Manyverse, Mastodon, Bluesky, AT, etc.).

Two levels:

* **BASIC (MVS)** – everyone does this
* **ADVANCED** – extra armor (signers, self-hosted relays, NIP-05, NWC, Yakihonne)

---

# 0. What You’re Building at L7

You are building **three things**:

1. **Two Nostr Identities (Personas)**

   * **PUBLIC** = “main Sov persona” (visible, posts, zaps, brand)
   * **GHOST** = “quiet, low-profile” persona (minimal metadata, high-privacy)

2. **Two Devices Using Nostr**

   * **CLEAN LAPTOP** → desktop client (**Gossip**)
   * **CLEAN PHONE** → mobile client (**Amethyst** on Android, **Damus** on iOS)

3. **One Relay Set**

   * A small set of **relays** that both personas talk to (BASIC)
   * (ADVANCED) + your **own relay** and per-persona relay filters

Everything else = decoration.

---

# 1. Prerequisites

You already have:

* ✅ L0: `my-secrets.kdbx` KeePass vault working on CLEAN LAPTOP + CLEAN PHONE
* ✅ L1: **CLEAN LAPTOP** (Linux, full-disk encryption) + **CLEAN PHONE** labeled
* ✅ L2: VPN on CLEAN LAPTOP + CLEAN PHONE (always-on, kill switch)
* ✅ L3: Private comms in place (Keychat, Briar/Bitchat, etc.)
* ✅ L4: `SovStack-Work` folder + restic backups
* ✅ L5: Browsers (Mullvad / LibreWolf / Tor / Ungoogled-Chromium) on CLEAN LAPTOP
* ✅ L6: Bitcoin node + Sparrow wallets (VAULT / SPEND / ENTRY) + small LN wallet

For L7 you need:

* 📝 Paper + ✍️ Pen
* 💻 CLEAN LAPTOP
* 📱 CLEAN PHONE (Graphene/Android or iOS)
* 🌐 VPN ON (L2 rules active)

---

# 2. Name Your Personas (On Paper)

On paper, write:

> `L7 NOSTR PERSONAS`
>
> **PUBLIC PERSONA (P)**
> – Name: __________
> – Purpose: Long-form posts, public face, zaps, linking to your work.
>
> **GHOST PERSONA (G)**
> – Name: __________
> – Purpose: Quiet reading, occasional high-signal posts, minimal identity.
>
> (Optional later: OPERATOR PERSONA – for relay admin/scripts only.)

Tick:

* [ ] PUBLIC persona defined
* [ ] GHOST persona defined

---

# 3. Install Desktop Client on CLEAN LAPTOP (Gossip)

## 3.1 Install Gossip

On **CLEAN LAPTOP** (VPN ON):

1. Open your **SOV browser (Mullvad Browser)**.
2. Search: `Gossip Nostr desktop` and go to the official site/repo.
3. Download the **Linux** build (AppImage / `.deb` / tar, depending on what they provide).
4. Install/run it (double-click AppImage / install `.deb` / follow instructions).

Tick:

* [ ] Gossip installed and opens on CLEAN LAPTOP

---

# 4. Create Keys in Gossip (PUBLIC + GHOST)

You will create **two keys** inside Gossip:

* One for **PUBLIC**
* One for **GHOST**

You will then **back them up into KeePass (L0)** and paper.

> You don’t need to understand Nostr cryptography.
> Just know:
>
> * `npub1…` = public key (share)
> * `nsec1…` = secret key (never share)

## 4.1 Create PUBLIC key in Gossip

In **Gossip**:

1. Find the menu for profiles / accounts (often in Settings or top-right).
2. Choose **Create New Profile** (or equivalent).
3. Name: your PUBLIC persona name (from paper).
4. Let Gossip generate the key.

Now **find the keys**:

1. Look for **“Show keys”, “Backup”, or “Export keys”** in profile/settings.

2. When you see:

   * Public key (starts with `npub1...`)
   * Secret key (starts with `nsec1...`)

3. On paper, write:

   > `PUBLIC NOSTR KEY`
   > `npub: ___________________________`
   > `nsec: ___________________________`

4. In KeePass (L0):

   * Create entry: `Nostr – PUBLIC Persona`
   * Username: `npub1…`
   * Password: `nsec1…`
   * Notes: “PUBLIC persona key, used in Gossip + phone client.”

Tick:

* [ ] PUBLIC key created in Gossip
* [ ] PUBLIC npub/nsec written on paper
* [ ] PUBLIC npub/nsec saved into KeePass

*(Gossip will also keep the key internally. That’s fine. CLEAN LAPTOP is L1-hardened.)*

---

## 4.2 Create GHOST key in Gossip

Repeat for GHOST:

1. In Gossip, **Create New Profile** again.
2. Name: your GHOST persona name (from paper).
3. Let it generate key.

Find keys and record:

1. View/export keys as before.

2. On paper, write:

   > `GHOST NOSTR KEY`
   > `npub: ___________________________`
   > `nsec: ___________________________`

3. In KeePass:

   * Entry: `Nostr – GHOST Persona`
   * Username: `npub1…`
   * Password: `nsec1…`
   * Notes: “GHOST persona, *laptop-only*, minimal profile.”

Tick:

* [ ] GHOST key created in Gossip
* [ ] GHOST npub/nsec written on paper
* [ ] GHOST npub/nsec stored in KeePass

---

# 5. Basic Relay Setup (Same for Both Personas)

For **BASIC MVS**, both personas will use the same small set of relays.
Advanced per-persona relay tuning comes later.

In **Gossip**, open **Relays** or similar menu.

### 5.1 Make a simple relay list

1. Keep the **default relays** that Gossip ships with **if they’re not obviously broken**.
2. Add **2–3 more well-known public relays** if Gossip suggests any (there’s usually a curated list).
3. Delete any relay entries that look clearly dead/404 in the UI.

On paper, write:

> `L7 RELAY SET – BASIC`
> – Relay 1: wss://__________________
> – Relay 2: wss://__________________
> – Relay 3: wss://__________________

Tick:

* [ ] 3–5 working relays configured in Gossip
* [ ] Same relay list used by both PUBLIC and GHOST profiles (for BASIC)

*(Later, for ADVANCED, GHOST will get a stricter set.)*

---

# 6. Set Basic Profiles (PUBLIC vs GHOST)

## 6.1 PUBLIC profile

In Gossip, choose the **PUBLIC** profile:

1. Go to **Profile / Settings → Edit profile**.
2. Set:

   * Name: PUBLIC persona name
   * Picture: optional (can use your project logo/pseudonym image)
   * About/Bio: concise statement of who/what this persona is
   * Website: if you have one for your Sov work

**Rule for PUBLIC**:

* It can be discoverable and link back to your other Sov assets (website, email alias, LN address, etc.).
* It **must not** leak real legal identity unless you consciously want that.

Tick:

* [ ] PUBLIC profile text and picture set

---

## 6.2 GHOST profile

In Gossip, choose **GHOST** profile:

1. Go to **Edit profile**.
2. Set:

   * Name: simple pseudonym (not linked to your brand)
   * Picture: optional, but keep it generic (no real photos, no logos reused from PUBLIC)
   * About/Bio: either empty or generic (e.g., “reading notes”, “research alt”).
   * No website, no email, no LN address for BASIC.

Tick:

* [ ] GHOST profile created with minimal info
* [ ] No real identity links in GHOST

---

# 7. Install Mobile Client on CLEAN PHONE (Android/iOS)

You will import **PUBLIC persona only** to the phone.
GHOST stays **laptop-only**.

---

## 7.1 Android CLEAN PHONE → Amethyst

On CLEAN PHONE (Android, VPN ON):

1. Open trusted store (GrapheneOS “Apps”, F-Droid, or Play Store as per your L1 rules).
2. Search **“Amethyst Nostr”**.
3. Install **Amethyst**.
4. Open Amethyst.

### 7.1.1 Import PUBLIC nsec into Amethyst

On CLEAN LAPTOP (Gossip):

1. Open KeePass or Gossip and get your **PUBLIC `nsec1…`**.
2. You can:

   * Either show it as text and type it into Amethyst, **or**
   * Paste into a temporary KeePass note and display a QR on laptop if Amethyst supports scanning it (depending on versions/UI).

On CLEAN PHONE:

1. In Amethyst, choose **“Import existing key” / “I already have a key”**.
2. Paste or scan your **PUBLIC `nsec1…`**.
3. Confirm.

Tick:

* [ ] Amethyst installed on CLEAN PHONE
* [ ] PUBLIC persona key imported (same `npub1…` as in Gossip)

---

## 7.2 iOS CLEAN PHONE → Damus

On CLEAN PHONE (iPhone, VPN ON):

1. Open **App Store**.
2. Search **“Damus Nostr”**.
3. Install **Damus**.
4. Open Damus.

### 7.2.1 Import PUBLIC nsec into Damus

Same as with Amethyst:

1. On CLEAN LAPTOP, retrieve PUBLIC `nsec1…`.
2. In Damus, choose **“Use existing key”** (not “new account”).
3. Paste or scan `nsec1…`.
4. Confirm.

Tick:

* [ ] Damus installed on CLEAN PHONE
* [ ] PUBLIC persona key imported (same `npub1…` as Gossip)

---

## 7.3 Relay sync on phone

On the mobile client (Amethyst or Damus):

1. Open **Relays** settings.
2. Add the same 3–5 relays you wrote in `L7 RELAY SET – BASIC`.
3. Remove random extras the app might add (if they look dead/weird).

Tick:

* [ ] PUBLIC persona on phone uses same BASIC relay set

From now on:

* PUBLIC persona = **Gossip on laptop + Amethyst/Damus on phone**
* GHOST persona = **Gossip on laptop only**

---

# 8. Optional: Read-Only on DIRTY Devices (npub Only)

If you want to **read** PUBLIC posts on a DIRTY device:

1. Take PUBLIC `npub1…` from KeePass/paper.
2. On the DIRTY device (KYC phone/computer), install a Nostr client or use a web client.
3. Choose **“view/read-only” / “import public key”** if app supports.
4. Paste `npub1…`.

**Rule:**
DIRTY devices **never** see `nsec1…`.
They are **read-only** windows into your PUBLIC feed.

Tick:

* [ ] If used: PUBLIC npub-only read access set on DIRTY devices

---

# 9. Nostr + Money (Zaps) – BASIC Rules

For BASIC MVS, treat Nostr as **talk + discovery**, and money as handled by **L6 wallets**, not by fancy connectors.

## 9.1 Add LN address to PUBLIC profile (optional but common)

If you want to receive zaps on PUBLIC persona:

1. Choose a **small, public Lightning address** from your L6 setup, e.g.:

   * A Lightning address from your **LN hot wallet** (Mutiny or node+ZEUS), **not** from cold storage / VAULT.

2. In Gossip & Amethyst/Damus, edit PUBLIC profile:

   * Add your LN address in the dedicated “Lightning” or “Wallet” field.

Rule:

* This LN address is **public-tip jar** level.
* It should be tied to a **low-balance LN wallet**, not your main reserves.

Tick:

* [ ] (Optional) PUBLIC profile has LN address from a small, hot wallet

---

## 9.2 How to zap others (BASIC)

When you see a post you want to zap:

1. Tap zap button in client (if available).
2. **If client opens your LN wallet directly**, confirm only **small amounts**.
3. If client does something weird or asks to connect to a strange service (NWC, custodial overlay you don’t understand):

   * Cancel the flow.
   * Instead, manually copy their LN address and pay from your LN wallet app directly.

Tick:

* [ ] Rule understood: if zap flow feels weird → bail, pay manually from LN wallet

---

# 10. L7 DAILY WORKFLOW (BASIC)

On paper, write:

> `L7 DAILY WORKFLOW`
>
> **On CLEAN LAPTOP (Gossip)**
> – PUBLIC: write long-form posts, threads, research notes.
> – GHOST: quietly read; sometimes post minimal, high-signal notes (no identity leaks).
>
> **On CLEAN PHONE (Amethyst/Damus)**
> – PUBLIC: reply, like, repost, short notes, zaps, check timeline.
>
> **When sending sats:**
> – Use LN wallet from L6 (Mutiny/ZEUS/etc.).
> – Treat Nostr as address book, not as custody layer.

Tick:

* [ ] L7 DAILY WORKFLOW written and visible near CLEAN LAPTOP

---

# 11. L7 “NEVER DO THIS” LIST (BASIC)

New heading on paper:

> `L7 – NEVER DO THIS`
>
> 1. Never paste any `nsec1…` key into a browser window or a random web Nostr client.
>    – Keys only live in: Gossip, Amethyst/Damus on CLEAN devices, and KeePass.
> 2. Never import `nsec1…` on **DIRTY** devices.
>    – DIRTY sees only `npub1…` (read-only).
> 3. Never use your **GHOST** persona on the phone.
>    – Ghost is laptop-only, with fewer relays and minimal profile.
> 4. Never link your **real name, KYC email, or KYC phone number** in any Nostr profile on CLEAN devices.
> 5. Never use NWC (Nostr Wallet Connect) by default.
>    – If you don’t fully understand it, don’t click “Connect wallet”.
> 6. Never reuse the same LN wallet for:
>    – PUBLIC zap jar
>    – Big L6 savings
>    – KYC exchange withdrawals

Tick:

* [ ] L7 NEVER DO list written and visible

---

# 12. Weekly & Monthly L7 Checklists

## Weekly (10–15 minutes)

On **CLEAN LAPTOP**:

* [ ] Open Gossip; confirm you can switch between PUBLIC and GHOST.
* [ ] Scroll PUBLIC feed; confirm posts load from your relay set.
* [ ] Switch to GHOST; confirm it still connects and can read/post.

On **CLEAN PHONE**:

* [ ] Open Amethyst/Damus; confirm PUBLIC persona still logs in and loads feed.
* [ ] If you use zaps: send a **tiny** test zap to someone you control or a known test account.

---

## Monthly (20–30 minutes)

* [ ] Re-check your **relay list** in Gossip + phone client; remove obviously dead/slow ones.
* [ ] Confirm PUBLIC and GHOST keys are still present in KeePass and on paper.
* [ ] Export any updated client backups (if Gossip/Amethyst offers export files) into `SovStack-Work/L7-Backups/`.
* [ ] Run L4 backup scripts so L7 backups get encrypted and stored.
* [ ] Re-read L7 NEVER DO list, confirm you didn’t violate anything.

---

# 13. ADVANCED L7 – Signers, Relays, NIP-05, Yakihonne, NWC

Only do this once BASIC feels automatic.

---

## 13.1 Signer Model (Amber / Gossip-as-signer / nos2x)

**Goal:** keep `nsec1…` mostly in **signer apps**, not sprinkled across every client.

Options:

1. **Android**: install **Amber** as signer, and have Amethyst use Amber to sign.
2. **Desktop**: let Gossip act as a Nostr Connect signer for other desktop/web clients.
3. **Web**: use **nos2x** browser extension to hold the key for web clients (Coracle, etc.).

Pattern:

* The **signer** app holds `nsec1…`.
* The **client** only sends “please sign this” requests.
* You can revoke at any time.

If you do this:

* Move PUBLIC `nsec1…` into a signer only.
* Remove it from plain-text storage in clients where possible (or at least don’t add it to new ones).

---

## 13.2 Per-Persona Relay Sets

Upgrade from “both share basic relay set” to:

* **PUBLIC RELAYS**: 4–8 general-purpose relays (including at least one paid/curated).
* **GHOST RELAYS**: 1 self-hosted + 1–2 small, privacy-focused relays.

In Gossip:

1. For PUBLIC: keep broader set.
2. For GHOST: **turn off** all but 2–3 relays.

This narrows metadata spread for GHOST.

---

## 13.3 Self-Hosted Relay (strfry or nostr-rs-relay)

If you’re comfortable with Docker:

1. On a small VPS or home server, run a Nostr relay (e.g., strfry).
2. Require auth (NIP-42) or at least rate limits.
3. Add this relay as:

   * Primary relay for GHOST.
   * One of several for PUBLIC.

Keep:

* Domain + configs backed up under L4.
* Relay logs minimal or pruned.

---

## 13.4 NIP-05 (“name@domain”) – PUBLIC Only

If you own a domain and want `name@yourdomain` on PUBLIC:

1. On your website host, create `/.well-known/nostr.json`.

2. Map:

   ```json
   {
     "names": {
       "name": "npub1..."
     }
   }
   ```

3. In PUBLIC profile, set NIP-05 to `name@yourdomain`.

Rules:

* Only for PUBLIC persona.
* Never for GHOST.
* Domain = under your control, not a random service.

---

## 13.5 Yakihonne (Rich PUBLIC client)

Use **Yakihonne** as an extra PUBLIC client:

* Long-form posts, curated feeds, social payments UI, MiniApps, etc.
* Always with PUBLIC persona only.
* Keys via signer if possible, or imported carefully once and backed up.

Never use it for GHOST.
Treat it as “front-of-house” only.

---

## 13.6 NWC (Nostr Wallet Connect) – Strict Rules

Use NWC only if you fully understand the trade-offs.

Minimal safe pattern:

1. Create a **dedicated tiny LN wallet** for NWC (separate from main).

2. In your LN wallet or provider:

   * Create one NWC connection with small monthly budget (e.g., 50k–200k sats).

3. Connect this NWC to **PUBLIC persona client** only (for auto-zaps).

Rules:

* One tiny wallet per NWC connection.
* Low budget.
* Never connect NWC to big balance node or cold savings.
* If any app misbehaves, revoke the NWC token immediately.

---

# 14. Emergency Branches (L7)

### Case 1 – You Lose `nsec1…` but Have `npub1…`

If you **only** have `npub1…` and no secret key:

* That identity is now **read-only**.
* You cannot post as it.
* You can either:

  1. Accept that it’s now an archive identity; create a new persona and announce the move, or
  2. If keys are still in some client (Gossip/Amethyst) but not in KeePass/paper, immediately:

     * Export keys again
     * Store back into KeePass and new paper backups

---

### Case 2 – Secret Key Leaked / Compromised

If PUBLIC `nsec1…` is exposed:

1. Immediately change PUBLIC profile bio to: “Compromised, moving to new key”.
2. Create a new PUBLIC persona with fresh key.
3. Post from old account pointing to new npub.
4. Stop using the old key.

If GHOST key leaks:

* Stop using that persona entirely.
* Create a new GHOST key, more strict relays, and never connect it to old patterns again.

---

### Case 3 – You Logged into Nostr with `nsec1…` on a DIRTY Device

Treat that persona as **compromised**:

* Either:

  1. Move to new key (like above), or
  2. Wipe that DIRTY device and never repeat.

---

# 15. Final Micro-Checklist (Caveman Version)

To confirm **L7 Signal Rail** is live:

1. [ ] You have **two Nostr personas** on paper + KeePass:

   * PUBLIC (`npub1…` / `nsec1…`)
   * GHOST (`npub1…` / `nsec1…`)

2. [ ] **Gossip** on CLEAN LAPTOP holds both personas and connects to a small set of working relays.

3. [ ] CLEAN PHONE runs **Amethyst (Android)** or **Damus (iOS)** with **PUBLIC persona** only, using the same relay set.

4. [ ] **GHOST persona** is **laptop-only**, minimal profile, no identity links.

5. [ ] PUBLIC persona optionally has an LN address pointing to a **tiny hot wallet**, not your savings.

6. [ ] No `nsec1…` has ever been put into a browser window or a DIRTY device; DIRTY devices see **npub only**.

7. [ ] L7 DAILY WORKFLOW and L7 NEVER DO lists are written and visible near CLEAN LAPTOP.

If all 7 are true, **L7 Nostr Signal Rail** is active: identity, publishing, and discovery now flow through a controlled, compartmentalized Nostr layer on top of your L0–L6 Sovereign Stack.
