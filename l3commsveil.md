Below is the **L3 “Comms Veil” Protocol** – **perfected** to match L0–L2 and L5 (especially the COMPAT browser rule).

It **sits on top of L0, L1, L2** (Secret Box → Device Shell → Network Cloak).
Think **IKEA / LEGO manual**: boxes to tick, steps in order.

Two levels:

* **BASIC (MVS)** – minimum everyone does
* **ADVANCED** – extra armor (Cwtch, mesh, SimpleX sunset)

---

# 0. What You’re Building at L3

You are building **four lines** of communication, all on CLEAN devices:

1. **EVERYDAY LINE**
   → **Keychat** on CLEAN PHONE (+ optional on CLEAN LAPTOP)
   → Text + 1:1 voice/video

2. **OFFLINE / CRISIS LINE**
   → **Briar** (Android) or **Bitchat Mesh** (iOS / Android)
   → Works when internet is censored or dead (local mesh / Tor)

3. **HIGH-RISK LINE (ADVANCED)**
   → **Cwtch** on CLEAN LAPTOP
   → Tor-based, metadata-resistant DMs/groups

4. **VOICE / VIDEO LINE**
   → 1:1 calls inside **Keychat**
   → Group calls via **Jitsi Meet** on CLEAN LAPTOP, in the **COMPAT browser (Ungoogled-Chromium)** from L5, with E2EE enabled

(OPTIONAL ADVANCED: **SimpleX** transitional use, with a hard sunset.)

---

# 1. Prerequisites

You already have:

* ✅ L0: `my-secrets.kdbx` working on CLEAN LAPTOP + CLEAN PHONE
* ✅ L1: One **CLEAN LAPTOP** and one **CLEAN PHONE** labeled
* ✅ L2: VPN on CLEAN LAPTOP + CLEAN PHONE, always-on with kill switch
* ✅ L5: Browsers set up on CLEAN LAPTOP:

  * SOV: Mullvad Browser
  * COMPAT: LibreWolf
  * GHOST: Tor Browser
  * ADV COMPAT: **Ungoogled-Chromium** (quarantined COMPAT-only browser)

For L3 you need:

* 📝 Paper + ✍️ Pen
* 💻 CLEAN LAPTOP
* 📱 CLEAN PHONE (GrapheneOS / Android / iOS)
* 📶 VPN ON (L2 rules active)

---

# 2. Name Your L3 Tools on Paper

On paper, write:

> `L3 COMMS VEIL MAP`
>
> **EVERYDAY LINE:** Keychat
> **OFFLINE / CRISIS LINE:**
> – Android: Briar
> – iPhone: Bitchat Mesh
> **HIGH-RISK LINE (ADV):** Cwtch (CLEAN LAPTOP)
> **VOICE / VIDEO LINE:**
> – 1:1 = Keychat calls
> – Groups = Jitsi via COMPAT browser (Ungoogled-Chromium) on CLEAN LAPTOP

Tick:

* [ ] L3 COMMS VEIL MAP written

---

# 3. BASIC – Set Up the EVERYDAY LINE (Keychat)

Keychat = Bitcoin-native secure chat app (ecash/Nostr/modern crypto).

## 3.1 Install Keychat on CLEAN PHONE

### 3.1.A Android (GrapheneOS / stock)

On CLEAN PHONE:

1. Open browser.
2. Go to **keychat.io** (or search “Keychat app Bitcoin” and pick official site).
3. Tap **Download App**:

   * Download Android APK and install it
   * Or use Play Store if you already have sandboxed Play on GrapheneOS
4. Open **Keychat**.

Tick:

* [ ] Keychat installed on CLEAN PHONE (Android)

### 3.1.B iPhone (iOS)

On CLEAN PHONE (iPhone):

1. Open **App Store**.
2. Search **“keychat.io”**.
3. Install the official **Keychat io** app.
4. Open **Keychat**.

Tick:

* [ ] Keychat installed on CLEAN PHONE (iOS)

---

## 3.2 Create Your Keychat Identity

In Keychat (on CLEAN PHONE):

1. Tap **Get Started** / **Create Account**.
2. Choose a **display name** (pseudonym is fine).
3. Let Keychat generate its keys/recovery info.

On paper, write:

> `KEYCHAT`
> Device: CLEAN PHONE
> Display name: ______
> Recovery phrase / info (if shown): ______

Tick:

* [ ] Keychat identity created
* [ ] Recovery info (if any) written on paper

---

## 3.3 Add ONE Test Contact and Send a Message

1. Make sure someone you trust has Keychat (any device).
2. Ask for their **Keychat ID / profile link / QR**.
3. In Keychat → **Add Contact** → scan or paste.
4. Send message: `TEST: hello from CLEAN PHONE`.
5. Ask them to reply.

Tick:

* [ ] At least one contact added
* [ ] Test message sent and received

---

## 3.4 Test a 1:1 Voice Call in Keychat

With that same contact:

1. Open chat with them in Keychat.
2. Tap the **call** icon.
3. Let it connect for a few seconds, speak, then hang up.

Tick:

* [ ] 1:1 voice call works between CLEAN PHONE and contact

From now on:
**EVERYDAY LINE = Keychat on CLEAN PHONE (text + 1:1 calls).**

---

# 4. BASIC – Set Up OFFLINE / CRISIS LINE

You will use:

* **Android:** **Briar** – P2P messenger over Bluetooth/Wi-Fi/Tor
* **iPhone (and/or Android):** **Bitchat Mesh** – Bluetooth mesh chat, no account

These are for:

* Internet censorship
* Blackouts
* Local protests / crises

---

## 4.1 ANDROID – Install Briar on CLEAN PHONE

On CLEAN PHONE (Android):

1. With VPN ON, open F-Droid / Play Store / browser.
2. Search **“Briar secure messaging”**.
3. Install **Briar** from official sources.
4. Open **Briar**.

First run:

1. Choose a **nickname** (pseudonym).
2. Choose a **Briar unlock password / code**.

On paper:

> `BRIAR`
> Device: CLEAN PHONE (Android)
> Nickname: ______
> Unlock password / code: ______

Tick:

* [ ] Briar installed
* [ ] Nickname + unlock code written down

---

### 4.1.1 Add a Briar Contact (In Person)

You need a friend physically present, with Briar installed.

1. Both open Briar.
2. Both tap **Add Contact → Nearby**.
3. Follow prompts to scan each other’s QR or use NFC.
4. Wait until it confirms you’re connected.

Tick:

* [ ] At least one Briar contact added

---

### 4.1.2 Test Offline Messaging with Briar

Both phones:

1. Turn **Airplane Mode ON**.
2. Turn **Wi-Fi ON** and **Bluetooth ON** (Airplane Mode allows toggling).
3. Open Briar.
4. You send them: `TEST: offline Briar`.
5. Confirm they receive it.

Tick:

* [ ] Offline Briar message works in Airplane + Wi-Fi/Bluetooth mode

This is your **OFFLINE / CRISIS LINE (Android)**.

---

## 4.2 iPHONE (or Extra Android) – Install Bitchat Mesh

Bitchat Mesh = Bluetooth mesh chat, no SIM, no account.

### 4.2.A iOS

On CLEAN PHONE (iPhone):

1. Open **App Store**.
2. Search **“Bitchat Mesh”**.
3. Install the app.
4. Open it and pick a **display name**.

On paper:

> `BITCHAT MESH`
> Device: CLEAN PHONE (iPhone)
> Display name: ______

Tick:

* [ ] Bitchat Mesh installed on iOS
* [ ] Display name written

### 4.2.B (Optional) Android Bitchat

On CLEAN PHONE (Android):

1. From Play Store or official site, install **Bitchat Mesh** if available.
2. Pick a display name.

---

### 4.2.1 Test a Bitchat Mesh Conversation

You need someone physically nearby with Bitchat Mesh.

1. Both open Bitchat Mesh.
2. Join the same nearby channel / room, or see each other in the app’s peer list.
3. Send: `TEST: mesh`.
4. Confirm they receive it.

Tick:

* [ ] Bitchat Mesh message sent and received over Bluetooth mesh

**Note:**
Bitchat Mesh is local-only (Bluetooth mesh range, maybe with device hops). It’s for **local emergency / crowd comms**, not long-distance chat.

---

# 5. ADVANCED – HIGH-RISK LINE (Cwtch on CLEAN LAPTOP)

Cwtch = Tor-based, metadata-resistant messenger for high-risk contexts.

## 5.1 Install Cwtch on CLEAN LAPTOP

On CLEAN LAPTOP (VPN ON):

1. Search `Cwtch secure messenger download`.
2. Go to the official site (Open Privacy Research Society).
3. Download the Linux desktop app.
4. Install and run it.

Tick:

* [ ] Cwtch installed on CLEAN LAPTOP

---

## 5.2 Create Cwtch Profile

In Cwtch:

1. Click **New Profile**.
2. Pick a **profile name** (pseudonym).
3. Let Cwtch create your identity (onion address/profile).

On paper:

> `CWTCH PROFILE`
> Device: CLEAN LAPTOP
> Profile name: ______
> Backup info / onion address (if shown): ______

Tick:

* [ ] Cwtch profile created and recorded

---

## 5.3 Add ONE Cwtch Contact

You need a trusted contact also using Cwtch.

1. Ask for their **Cwtch contact string / QR**.
2. In Cwtch → **Add Contact** → paste or scan.
3. Send them: `TEST: cwtch`.
4. Confirm they reply.

Tick:

* [ ] At least one Cwtch contact added
* [ ] Test message exchange successful

This is your **HIGH-RISK LINE**.

---

# 6. BASIC – VOICE / VIDEO LINE

You already tested:

* **1:1 calls** → Keychat on CLEAN PHONE

Now add:

* **Group calls with video** → **Jitsi** on CLEAN LAPTOP in the **COMPAT browser (Ungoogled-Chromium)** from L5.

## 6.1 Join a Jitsi Call (Safe Pattern)

When someone sends you a **Jitsi link** (e.g. in Keychat/Briar/Cwtch):

### On CLEAN LAPTOP:

1. Ensure **VPN is ON** (L2).

2. Open the **COMPAT browser**:

   * This is **Ungoogled-Chromium** set up at L5 as the quarantined “compat-only” browser.
   * Do **not** use Chrome / Edge / Brave / Safari.

3. Paste or click the Jitsi link (from Keychat/Briar/Cwtch).

4. When Jitsi opens:

   * Allow microphone/camera if you want to speak/appear.
   * Open the **Security / Shield** icon.
   * Turn **E2EE ON** (End-to-End Encryption).
   * Enter the **room passphrase** that was shared with you **inside Keychat/Briar/Cwtch**, not via email/SMS.

Tick:

* [ ] Jitsi call joined from CLEAN LAPTOP using COMPAT browser
* [ ] E2EE turned ON and passphrase entered

**1:1 calls** stay in **Keychat** on CLEAN PHONE.
**Group calls** go to **Jitsi** via COMPAT browser on CLEAN LAPTOP.

---

## 6.2 (Optional ADVANCED) Self-Hosted Jitsi

If you or an ally runs your own Jitsi server:

1. Prefer that server domain (e.g. `https://meet.yourdomain.org/...`) over public `meet.jit.si`.
2. Still join via **Ungoogled-Chromium COMPAT browser** with VPN ON.
3. Still enable E2EE + passphrase.

Server admin can see **metadata** (who connects, when, IPs), so:

* Always use VPN
* Use pseudonyms in display name

---

# 7. ADVANCED – Optional SimpleX Transitional Use

SimpleX is allowed **only as a temporary tool** with a built-in *sunset*, since tokenization is expected.

If you choose to use SimpleX:

1. Install **SimpleX Chat** on CLEAN PHONE and (optional) CLEAN LAPTOP from official sources.
2. Use it like Keychat for text chats during the “clean” window.

On paper, write:

> `SIMPLEX SUNSET RULE`
> “When SimpleX adds tokens or token features, I stop using it for new chats.
> I move live conversations to Keychat or Cwtch.
> SimpleX becomes read-only history for 3 months, then I uninstall.”

When token features appear:

1. Open each important chat in SimpleX and tell contact:
   → “We are moving to Keychat/Cwtch.”
2. Create a new chat with them in Keychat/Cwtch.
3. Stop sending new messages in SimpleX.
4. After ~3 months, export anything you need manually (if possible) and uninstall SimpleX.

Tick (if using SimpleX):

* [ ] SIMPLEX SUNSET RULE written
* [ ] Migration plan clear

If you never use SimpleX, ignore this block.

---

# 8. L3 DAILY RULES

On paper, write:

> `L3 DAILY RULES`
>
> **EVERYDAY LINE**
> – Use **Keychat** on CLEAN PHONE for normal private chat and 1:1 voice calls.
>
> **OFFLINE / CRISIS LINE**
> – If internet/cell is censored or down:
> – Android: use **Briar** with pre-added contacts (Bluetooth/Wi-Fi mesh + Tor when available).
> – iPhone (or extra Android): use **Bitchat Mesh** for local Bluetooth mesh chat.
>
> **HIGH-RISK LINE (ADV)**
> – Use **Cwtch** on CLEAN LAPTOP for sensitive groups / operations.
>
> **VOICE / VIDEO LINE**
> – 1:1 calls: **Keychat** on CLEAN PHONE.
> – Group calls: **Jitsi** on CLEAN LAPTOP via **Ungoogled-Chromium COMPAT browser**, E2EE ON.

Tick:

* [ ] L3 DAILY RULES written and posted near CLEAN LAPTOP

---

# 9. L3 “NEVER DO THIS” LIST

New heading on paper:

> `L3 – NEVER DO THIS`
>
> 1. Never add your **real phone number or email** inside any L3 app on CLEAN devices (Keychat, Briar, Bitchat, Cwtch, SimpleX).
> 2. Never log into **Facebook / Instagram / TikTok / X / KYC exchanges / banks** inside:
>    – Keychat, Briar, Bitchat, Cwtch, SimpleX
>    – Jitsi meetings
> 3. Never install **Signal, Telegram, WhatsApp, Session, Messenger, etc.** on CLEAN devices.
>    – Those live only on DIRTY devices.
> 4. Never share Jitsi room links or meeting passphrases over **plain email or SMS**; share them only via Keychat/Briar/Cwtch.
> 5. Never use Briar or Bitchat Mesh for truly criminal / catastrophic topics unless you consciously accept **physical environment risk** (others near you, devices that can be seized).
> 6. **Browser constraint (aligned with L5):**
>    – Never install or use **Chrome, Edge, Safari, or Brave** on CLEAN LAPTOP.
>    – For Jitsi group calls on CLEAN LAPTOP, use only the **Ungoogled-Chromium COMPAT browser** from L5.

Tick:

* [ ] L3 NEVER DO list written and visible

---

# 10. Weekly & Monthly L3 Checklists

## Weekly (10–15 minutes)

On **CLEAN PHONE**:

* [ ] Open **Keychat** – send `WEEKLY TEST` to a trusted contact and get a reply.
* [ ] (Android) Open **Briar** – unlock and send `WEEKLY TEST` to a Briar contact.
* [ ] (iOS / Android) Open **Bitchat Mesh** – if a friend is nearby, exchange `WEEKLY TEST`.

On **CLEAN LAPTOP**:

* [ ] Open **Cwtch** – verify profile loads and send `WEEKLY TEST` to a contact.
* [ ] Join a short **Jitsi** test call via **Ungoogled-Chromium COMPAT browser**, toggle E2EE, verify you can see/hear someone or at least connect.

---

## Monthly (20–30 minutes)

* [ ] Review **L3 NEVER DO** list; confirm you didn’t violate any rule.
* [ ] Check for app updates (Keychat, Briar, Bitchat, Cwtch, SimpleX if used).
* [ ] Do one **full-group Jitsi rehearsal** if you rely on group calls:

  * Everyone joins via COMPAT browser, VPN ON, E2EE ON, passphrase shared via Keychat/Briar/Cwtch.
* [ ] Verify that CLEAN LAPTOP still has **no Chrome/Edge/Safari/Brave** installed.
* [ ] Confirm Ungoogled-Chromium is still used **only** for Jitsi and rare compat tasks.

---

# 11. Emergency Branches (L3)

### Case 1 – Internet / Cell Completely Down

* **Android CLEAN PHONE:**

  * Open **Briar** → talk to pre-added contacts (Bluetooth/Wi-Fi mesh).
* **iPhone / extra Android:**

  * Open **Bitchat Mesh** → talk to people within Bluetooth mesh range.

### Case 2 – You Installed a Banned Messenger on CLEAN PHONE (e.g., WhatsApp)

* That phone is now **contaminated**:

  * Option A: Re-label it **DIRTY PHONE** permanently; get a new device for CLEAN PHONE.
  * Option B: Factory reset, reinstall GrapheneOS/stock, and re-run L1–L3 setup.

### Case 3 – Jitsi Link Comes From an Unknown Person

* Treat as **untrusted**:

  * Join only from CLEAN LAPTOP **if necessary** using COMPAT browser, with:

    * Camera OFF
    * Mic muted
    * Pseudonymous display name
  * Or refuse to join entirely if stakes are high.
  * Never show real face or voice in unknown Jitsi rooms.

---

# 12. Final Micro-Checklist (Caveman Version)

To confirm **L3 Comms Veil** is fully in place and aligned with L5:

1. [ ] **Keychat** is on CLEAN PHONE, with at least one contact; you can send messages and make 1:1 calls.
2. [ ] (Android) **Briar** is on CLEAN PHONE, with at least one contact tested offline (Airplane + Wi-Fi/Bluetooth).
3. [ ] (iOS / Android) **Bitchat Mesh** is on a CLEAN PHONE, tested for local Bluetooth mesh chat.
4. [ ] **Cwtch** is on CLEAN LAPTOP with at least one contact and a successful test message (HIGH-RISK LINE).
5. [ ] You can join a **Jitsi group call** from CLEAN LAPTOP using **Ungoogled-Chromium COMPAT browser**, VPN ON, E2EE ON, passphrase shared in Keychat/Briar/Cwtch.
6. [ ] **L3 DAILY RULES** and **L3 NEVER DO** lists are written and visible near CLEAN LAPTOP.
7. [ ] Weekly tests (Keychat/Briar/Bitchat/Cwtch/Jitsi) and monthly reviews are happening.

If all 7 are true, your **L3 Comms Veil** is live, consistent with **L0–L2** and **L5**, and your communications now move through a clear, repeatable, compartmentalized pipeline.
