Below is the **L6 “Sats Circuit” Protocol – FINAL v2** – only this layer, nothing else.
It **sits on top of L0–L5** (Secret Box → Device Shell → Network Cloak → Comms Veil → File Spine → Browser Veil).

Think **IKEA / LEGO manual**: steps in order, boxes to tick.

Two levels:

* **BASIC (MVS)** – minimum everyone does
* **ADVANCED** – extra armor (SeedSigner VAULT, metal plates, JoinMarket, LN node, NWC zap jar, Cashu/Fedimint)

---

# 0\. What You’re Building at L6

You are building a **closed, labeled money circuit** on CLEAN devices.

**Six components:**

1. **VAULT WALLET (coldest hot)**
   → Long-term savings
   → Watch-only in Sparrow
   → Signing on **air-gapped SeedSigner** (ADVANCED) or local Sparrow (BASIC)
2. **SPEND WALLET**
   → Everyday on-chain spending \& receiving
   → Refilled from VAULT
3. **ENTRY WALLET**
   → All *new* sats from outside world land here first
   → P2P buys, gifts, payments, etc.
4. **LIGHTNING CIRCUIT**
   a. **PRIVATE LN WALLET / NODE** – your personal hot payment rail
   b. **PUBLIC ZAP JAR (LN + NWC)** – tiny, exposed hot wallet for Nostr zaps (L7)
5. **ECASH POUCH (ADVANCED)**
   → Tiny “cash in pocket” level balances (Cashu / Fedimint)
   → Extremely bounded
6. **SEED BACKUP LAYER**
   → Paper + **metal plates**
   → Restore-tested for VAULT (and optionally others)

Everything hangs off **your own Bitcoin node** on the CLEAN LAPTOP.

---

# 1\. Prerequisites

You already have:

* ✅ **L0:** KeePass (`my-secrets.kdbx`) + strong master password
* ✅ **L1:** CLEAN LAPTOP (Linux + FDE) and CLEAN PHONE; DIRTY devices labeled
* ✅ **L2:** VPN ON with kill switch on CLEAN devices
* ✅ **L3:** Private comms (Keychat, Briar/Bitchat, Cwtch, etc.)
* ✅ **L4:** `SovStack-Work` folder + restic backups + restore tested
* ✅ **L5:** Browser Veil (Mullvad / LibreWolf / Tor / optional Ungoogled-Chromium)

For L6 you need:

* 📝 Paper + ✍️ Pen
* 💻 CLEAN LAPTOP (Debian-like)
* 📱 CLEAN PHONE
* 💾 Optional extra USB for installers / bootstrap
* 🧱 For ADVANCED VAULT: **SeedSigner parts** + a **metal seed backup kit** (plate or washer system, stainless or titanium)

---

# 2\. Name Your Money Roles (On Paper)

On paper, write:

> `L6 MONEY MAP`
>
> \*\*VAULT WALLET\*\* – long-term BTC savings (coldest hot, SeedSigner-signing in ADVANCED)
> \*\*SPEND WALLET\*\* – everyday on-chain use
> \*\*ENTRY WALLET\*\* – all new sats land here first
> \*\*PRIVATE LN\*\* – personal LN payments (coffee, small stuff)
> \*\*PUBLIC ZAP JAR\*\* – tiny LN hot wallet exposed to Nostr via zap/LUD16 + NWC
> \*\*ECASH POUCH (ADV)\*\* – tiny ecash hot balance
> \*\*SEED BACKUPS\*\* – paper + metal, restore-tested

Tick:

* \[ ] L6 MONEY MAP written and stored with your other SovStack notes

---

# 3\. BASIC – Install \& Run Your Bitcoin Node (CLEAN LAPTOP)

## 3.1 Install Bitcoin Core

On CLEAN LAPTOP:

```bash
sudo apt update
sudo apt install bitcoin-qt
```

Tick:

* \[ ] `bitcoin-qt` installed

---

## 3.2 Initial Setup (Pruned, With Server)

1. Start **Bitcoin Core** from Applications.
2. When asked for data directory, choose:

   * Default or something like: `/home/<yourname>/Bitcoin`

3. Enable pruning:

   * Check “Prune block storage”
   * Set to **10 GB** (or larger if you have space)

Click OK and let it start.

Tick:

* \[ ] Data directory chosen
* \[ ] Pruning enabled

---

## 3.3 Configure Core for RPC (server mode)

1. Close Bitcoin Core (File → Exit).
2. In terminal:

```bash
mkdir -p ~/.bitcoin
nano ~/.bitcoin/bitcoin.conf
```

3. Paste:

```ini
server=1
prune=10000
txindex=0
rpcallowip=127.0.0.1
rpcbind=127.0.0.1
```

(Adjust `prune` if you chose a different size.)

4. Save and exit.
5. Restart Bitcoin Core.

Tick:

* \[ ] `bitcoin.conf` created
* \[ ] Core restarted with `server=1`

---

## 3.4 Let the Node Sync Fully

Leave Bitcoin Core running until:

* Progress bar hits **100%**
* Status says “Up to date” (no big backlog)

Tick:

* \[ ] Node synced and up to date

---

## 3.5 Autostart Node

In Bitcoin Core:

* Settings → Options (or Preferences)
* Enable “Start Bitcoin Core on system login”

Tick:

* \[ ] Core set to autostart

Your node is now the **spine** of the Sats Circuit.

---

# 4\. ADVANCED – Build the VAULT Signer (SeedSigner)

*(If you skip ADVANCED, VAULT will temporarily be a normal Sparrow software wallet. Still follow the later seed backup rules.)*

## 4.1 Assemble SeedSigner Hardware

High-level:

1. Get the standard SeedSigner parts (Pi Zero, screen, buttons, camera, case, microSD).
2. On **CLEAN LAPTOP**, download the SeedSigner image from its official site.
3. Flash image to the microSD using a tool like `balenaEtcher`.
4. Boot the Pi with that SD card in; verify SeedSigner UI appears.
5. Optionally remove/disable Wi-Fi hardware (use non-W model or hardware mod) if you want strict air-gap.

Tick:

* \[ ] SeedSigner assembled
* \[ ] Official image flashed from CLEAN LAPTOP
* \[ ] Device boots into SeedSigner UI

---

## 4.2 Decide VAULT Passphrase Policy

On paper, write:

> `VAULT PASSPHRASE POLICY`
>
> \[ ] \*\*Mode A – No BIP39 passphrase\*\* (simpler, less to forget)
> \[ ] \*\*Mode B – With BIP39 passphrase\*\* (extra security, extra risk)

Choose **one**:

* If **Mode A**: VAULT = seed only.
* If **Mode B**: create a passphrase (sentence) that:

  * Is independent from your L0 master password
  * Lives in **KeePass** (`VAULT – BIP39 passphrase`)
  * Is **not** written on the same plate/paper as the seed words

Tick:

* \[ ] VAULT passphrase mode chosen and written
* \[ ] (If Mode B) Passphrase stored in KeePass

---

## 4.3 Generate VAULT Seed on SeedSigner

On SeedSigner:

1. Choose **“New Seed”** (or equivalent).
2. Let it generate 12/24 words.
3. If using passphrase mode, configure BIP39 passphrase according to its workflow (or remember that you must always enter it before use).

On paper (temporary scratch):

> `VAULT SEED PHRASE (TEMP)`
> \[Write all words in order, clearly]

Tick:

* \[ ] VAULT seed generated on SeedSigner
* \[ ] Words copied to temporary paper sheet

*(This sheet will be used to create metal backups and then either stored carefully or destroyed, depending on your policy.)*

---

## 4.4 Export VAULT Xpub / Descriptor to Sparrow (Watch-Only Vault)

On SeedSigner:

1. Choose **“Export wallet / xpub / descriptor”** for the generated seed (single-sig).
2. Display **QR** of descriptor or xpub.

On CLEAN LAPTOP:

1. Open **Sparrow**.
2. File → New Wallet → Name: `VAULT` → Create Wallet.
3. Choose **Airgapped Hardware Wallet** / **Import xpub/descriptor** (whichever matches).
4. Use laptop webcam to scan the SeedSigner QR, or manually paste descriptor text if available.
5. Save wallet as **watch-only** (no private keys in Sparrow).

Tick:

* \[ ] VAULT wallet created in Sparrow as watch-only
* \[ ] Connected to local Core, showing derivation paths/addresses

---

## 4.5 VAULT Seed Metal Backup (Mandatory for Serious Funds)

### 4.5.1 Prepare the Metal Kit

1. Take your metal backup system (plate or washers).
2. Label on paper:

> `VAULT METAL BACKUP`
   >
   > Plate A – location: \_\_\_\_\_\_
   > Plate B – location: \_\_\_\_\_\_ (optional second copy)

Tick:

* \[ ] Metal kit ready
* \[ ] Planned storage locations written

---

### 4.5.2 Transfer Seed to Metal

Using your `VAULT SEED PHRASE (TEMP)` sheet:

1. For word-based plate:

   * Stamp the **first 4 letters** of each BIP39 word **deeply** into the plate (or full words if design allows).
   * Keep word order exact.

2. For washer system:

   * One washer per word.
   * Stamp a **number** and a **4-letter prefix** for each.

3. If using a **QR metal plate** (for SeedSigner):

   * Follow kit instructions to encode the seed/descriptor as metal QR.
   * Ensure you understand exactly **what the QR holds** (seed vs xprv vs descriptor).

Tick:

* \[ ] All VAULT words encoded on metal plate(s) in correct order / pattern

---

### 4.5.3 Test the VAULT Metal Backup (Restore Ritual)

You must prove the metal backup works, just like L4 file restore.

1. Using the metal plate only (ignore temporary paper):

   * Carefully read words (or scan QR into SeedSigner).

2. On SeedSigner:

   * Choose **“Restore seed”** (or equivalent).
   * Enter words (or scan QR) from the metal.
   * If using BIP39 passphrase (Mode B), enter the same passphrase you stored in KeePass.

3. Export the descriptor/xpub from this restored profile.
4. In Sparrow, create a **temporary test wallet**:

   * File → New Wallet → `VAULT-RESTORE-TEST` → import descriptor from SeedSigner.
   * Check that its receive addresses **match** the original VAULT watch-only wallet (at least the first few).

If addresses match, metal backup is proven.

Tick:

* \[ ] VAULT seed restored from metal into SeedSigner
* \[ ] Test wallet in Sparrow matches original VAULT addresses
* \[ ] Metal plate(s) confirmed good

---

### 4.5.4 Finalize Seed Storage

1. Decide what to do with the temporary paper:

   * Either store it as a **secondary backup** in a sealed envelope in a different place, **or**
   * Destroy it carefully if you trust only the metal + passphrase.

2. Place metal plate(s) in their designated locations:

   * Plate A – e.g., home safe
   * Plate B – e.g., different building, trusted family, safety deposit, etc.

Tick:

* \[ ] Temporary VAULT seed paper handled according to policy
* \[ ] Metal plate(s) stored in distinct physical locations

From now on, **SeedSigner is the only device that signs VAULT spends**. Sparrow just coordinates.

---

# 5\. BASIC – SPEND \& ENTRY Wallets in Sparrow

For BASIC, SPEND \& ENTRY are normal software wallets in Sparrow on CLEAN LAPTOP (with paper backup; metal optional).

## 5.1 SPEND Wallet (Everyday On-Chain)

In Sparrow:

1. File → New Wallet → Name: `SPEND` → Create Wallet.
2. Choose **New or Imported Software Wallet → New Seed**.
3. Generate seed words.

On paper:

> `SPEND SEED PHRASE`
> \[words]

In KeePass:

* New entry: `Sparrow – SPEND wallet password` (if you set a wallet password).

Tick:

* \[ ] SPEND wallet created
* \[ ] SPEND seed on paper
* \[ ] SPEND password (if any) in KeePass

*(ADVANCED: optionally create a metal plate for SPEND too, repeating the VAULT metal ritual.)*

---

## 5.2 ENTRY Wallet (New Sats In)

Repeat:

1. File → New Wallet → Name: `ENTRY`.
2. New seed; paper backup:

> `ENTRY SEED PHRASE`
   > \[words]

3. KeePass entry: `Sparrow – ENTRY wallet password`.

Tick:

* \[ ] ENTRY wallet created
* \[ ] ENTRY seed on paper
* \[ ] ENTRY password (if any) in KeePass

*(ADVANCED: metal backup if ENTRY holds large amounts; otherwise paper might be enough if ENTRY is “transit only.”)*

---

## 5.3 Export SPEND \& ENTRY Descriptors into L4 (File Spine)

For **each** wallet (SPEND, ENTRY):

1. Open wallet in Sparrow.
2. Go to **Settings → Export**.
3. Export **descriptors / backup** as a text file.
4. Save to:

   * `~/SovStack-Work/L6-Wallet-Backups/`

Name files:

* `SPEND-descriptors.txt`
* `ENTRY-descriptors.txt`

Tick:

* \[ ] Descriptors exported for SPEND \& ENTRY into L6 folder

These files now ride on your L4 restic backups.

---

# 6\. Label Rules (Buckets \& Flow)

In Sparrow, set **descriptions** for clarity:

* **VAULT** description:

> `Long-term savings. Signed via SeedSigner. Minimal movement. No direct KYC. Cleanest coins.`

* **SPEND** description:

> `On-chain daily spending. Refilled from VAULT.`

* **ENTRY** description:

> `All new sats from outside. P2P buys, gifts, income.`

On paper, write:

> `L6 FLOW RULES`
>
> 1. \*\*ENTRY\*\* = where all fresh sats land.
> 2. \*\*VAULT\*\* = long-term, conditioned, minimal movement, signed via SeedSigner (ADVANCED).
> 3. \*\*SPEND\*\* = only funded from VAULT, used for outflows.
> 4. Never mix VAULT + ENTRY UTXOs in a single transaction.
> 5. Use coin control and labels for every meaningful UTXO.

Tick:

* \[ ] L6 FLOW RULES written and stored

---

# 7\. BASIC – New Sats In: ENTRY Flow

All incoming sats from **non-KYC** sources (P2P trades, gifts, payments) land in ENTRY first.

## 7.1 Generate ENTRY Receive Address

In Sparrow:

1. Select `ENTRY`.
2. Click **Receive**.
3. Copy address #1.

On paper:

> `ENTRY ADDRESS #1 = \[address]`

Optionally store in KeePass entry: `ENTRY – recv #1`.

Tick:

* \[ ] ENTRY receiving address created and stored

---

## 7.2 Use ENTRY for P2P / Incoming

When:

* You buy BTC P2P (e.g., Bisq, RoboSats)
* You receive salary/invoice in BTC
* You get a gift

→ You give a **fresh ENTRY address**, never VAULT or SPEND.

After coins arrive:

1. In `ENTRY` wallet → Transactions / UTXOs.
2. Wait for confirmation.
3. Right-click TX/UTXO → **Add Label**:

   * `Bisq buy 2025-11-19`
   * `RoboSats #XYZ, 120k sats`
   * `Client ABC, 500k sats`

Tick:

* \[ ] At least one real incoming TX to ENTRY
* \[ ] UTXO labeled with source + date

---

# 8\. BASIC – ENTRY → VAULT (Simple Reconditioning)

Goal: keep provenance separated and move coins towards long-term VAULT in structured chunks.

## 8.1 Per-Source Sweep to VAULT

1. In `ENTRY` → **UTXOs** tab.
2. Select UTXOs **from a single source** (same trade, same client, etc.).
3. Right-click → **Send Selected**.

Recipient:

1. In `VAULT` (watch-only) → **Receive** → copy a fresh VAULT address.
2. Paste into ENTRY’s send screen.

Amount:

* Send almost the full amount from those UTXOs to the VAULT address.
* Structure amount so that change is either:

  * Avoided, or
  * Left clearly labeled in ENTRY.

Fee:

* Choose a reasonable on-chain fee.

Broadcast.

In `VAULT`:

1. After confirmation, label the new UTXO in Sparrow (watch-only):

   * `From ENTRY / Bisq 2025-11-19`
   * `From ENTRY / Client ABC`

Tick:

* \[ ] ENTRY → VAULT TX done
* \[ ] Incoming VAULT UTXO labeled with provenance

*(ADVANCED privacy: see JoinMarket later for mixing before or after ENTRY → VAULT.)*

---

# 9\. BASIC – Fund and Use SPEND Wallet

## 9.1 Fund SPEND from VAULT

When you want “daily spending ammo”:

1. In Sparrow, `VAULT` (watch-only) → **Receive**, copy a **SPEND**-target address instead?
   – Correct pattern:

   * `SPEND` → Receive → copy SPEND address.
   * In VAULT, you’ll create a PSBT to send to that address.

2. In Sparrow, with VAULT selected:

   * **New Transaction** → use coin control to pick specific VAULT UTXOs.
   * Set recipient to the SPEND address.

3. Click **Create Transaction** (do **not** sign yet).
4. Click **Finalize to PSBT** and **Export as QR**.

On SeedSigner (ADV VAULT):

1. Scan the PSBT QR.
2. Verify outputs/amounts (you are funding SPEND, not some random address).
3. Sign the PSBT.
4. SeedSigner shows **signed PSBT QR**.

Back in Sparrow:

1. Click **Scan PSBT** (QR), capture the signed QR from SeedSigner.
2. Sparrow now has a **signed transaction**.
3. Click **Broadcast**.

In `SPEND`:

* After it confirms, label UTXO:

> `Funded from VAULT for spends YYYY-MM-DD`

Tick:

* \[ ] SPEND funded from VAULT via SeedSigner-signed TX
* \[ ] Incoming SPEND UTXO labeled

*(BASIC with no SeedSigner: you create \& sign inside Sparrow directly; still label and treat carefully until you upgrade.)*

---

## 9.2 Spend from SPEND with Coin Control

When paying someone on-chain:

1. In `SPEND` → **UTXOs** tab.
2. Select the specific UTXO(s) you want to spend (avoid mixing weird histories).
3. Right-click → **Send Selected**.
4. Paste the recipient’s address.
5. Set amount + fee.
6. Label outgoing TX:

   * `Groceries merchant`
   * `Rent`
   * `Donation X`

Tick:

* \[ ] You use coin control for each SPEND TX
* \[ ] Outgoing TXs labeled with destination context

---

# 10\. ADVANCED – JoinMarket Reconditioning

JoinMarket = P2P CoinJoin using your node. Use if you want **stronger on-chain unlinking** between ENTRY sources and VAULT.

## 10.1 Install JoinMarket

On CLEAN LAPTOP:

```bash
sudo apt update
sudo apt install git python3-venv python3-pip
cd ~
git clone https://github.com/JoinMarket-Org/joinmarket-clientserver.git
cd joinmarket-clientserver
./install.sh --without-qt
```

Tick:

* \[ ] JoinMarket installed successfully

---

## 10.2 Configure JoinMarket to Use Local Core

```bash
cd ~/joinmarket-clientserver
cp joinmarket.cfg.sample joinmarket.cfg
nano joinmarket.cfg
```

Set essentials:

```ini
network = mainnet
rpc\_host = 127.0.0.1
rpc\_port = 8332
rpc\_user =
rpc\_password =
rpc\_wallet\_file = ""
```

Save and exit.

Tick:

* \[ ] joinmarket.cfg points to local Core

---

## 10.3 Create JoinMarket Wallet

```bash
cd ~/joinmarket-clientserver/scripts
python3 wallet-tool.py jm-wallet.json generate
```

During prompts:

* Write seed phrase on paper: `JOINMARKET WALLET SEED`.
* Store wallet password/passphrase in KeePass: `JoinMarket wallet password`.

Tick:

* \[ ] JoinMarket wallet created and backed up

---

## 10.4 Move Coins INTO JoinMarket

From `ENTRY` or `SPEND`:

1. Get a receiving address:

```bash
cd ~/joinmarket-clientserver/scripts
python3 wallet-tool.py jm-wallet.json display
```

2. In Sparrow (ENTRY/SPEND):

   * Use coin control → select UTXOs
   * Send to that JoinMarket address.

Wait for confirmations.

Tick:

* \[ ] Source coins moved into JoinMarket wallet

---

## 10.5 Do a CoinJoin + Send to Destination

Example direct-send mix:

```bash
cd ~/joinmarket-clientserver/scripts
python3 sendpayment.py -N 5 0.5 jm-wallet.json <amount\_sats> <destination\_address>
```

Where `<destination\_address>` is a **fresh VAULT** or **SPEND** address.

Tick:

* \[ ] At least one JoinMarket mix completed
* \[ ] Mixed coins landed in VAULT/SPEND and labeled (`JM mixed from ENTRY …`)

---

# 11\. BASIC – Lightning (PRIVATE Hot Wallet)

For MVS, Lightning = **small, self-custodial hot wallet** on CLEAN PHONE.

## 11.1 Install Self-Custodial LN Wallet

On CLEAN PHONE:

1. Install a reputable self-custodial LN wallet (e.g. Mutiny) from official source.
2. Let it generate a seed.

On paper:

> `PRIVATE LN SEED`
> \[words or backup phrase]

In KeePass:

* Entry: `PRIVATE LN Wallet` – add seed/recovery info \& PIN.

Tick:

* \[ ] Private LN wallet installed
* \[ ] LN seed backed up (paper + KeePass)

---

## 11.2 Top Up PRIVATE LN from SPEND

Flow:

1. In LN wallet: find **On-chain deposit** (or swap/bridge).
2. In `SPEND` wallet: send a small top-up amount (coffee/lunch sized).
3. Wait until LN wallet shows sats available.

Tick:

* \[ ] Small amount sent from SPEND → LN hot wallet

Rules:

* PRIVATE LN = **tiny** relative to on-chain savings.
* Top up from SPEND only.
* Never put meaningful savings on LN.

---

# 12\. ADVANCED – Full LN Node + ZEUS (PRIVATE LN Upgrade)

Instead of a simple mobile LN wallet, you can run your own LN node.

## 12.1 Run LN Node (LND or Core Lightning)

High-level:

1. Install **LND** or **Core Lightning** on CLEAN LAPTOP or home server.
2. Configure it to use your local Bitcoin Core.
3. Fund it from **SPEND** using on-chain channels.
4. Run it behind VPN (and ideally Tor).

Store:

* Node seed
* Static channel backup
* Admin macaroon / credentials

in KeePass + L4 (`SovStack-Work`).

Tick:

* \[ ] LN node installed and connected to local Core
* \[ ] Channels funded from SPEND only
* \[ ] Node secrets backed up

---

## 12.2 ZEUS on CLEAN PHONE

1. Install **ZEUS** from official source.
2. In LN node UI: generate connection string (QR / lndconnect / CLN JSON).
3. In ZEUS → add node → scan/paste details.
4. Confirm ZEUS shows LN balances/channels and can pay a tiny invoice.

Tick:

* \[ ] ZEUS connected to your LN node, test payment works

Rule:

* LN channels = small–moderate; never VAULT-level funds.
* All LN liquidity funded from SPEND.

---

# 13\. ADVANCED – PUBLIC ZAP JAR (LN + NWC for Nostr)

This is the **public-facing** LN wallet for Nostr zaps (L7).
It must be tiny and **completely separate** from PRIVATE LN and VAULT.

## 13.1 Create a Tiny “Zap Jar” Wallet

Options:

1. **Separate LN Wallet app** on CLEAN PHONE.
2. **Separate account/profile** on your LN node dedicated to NWC.

Label:

> `PUBLIC ZAP JAR – LN`

Tick:

* \[ ] Public zap jar LN wallet created and clearly labeled

---

## 13.2 Fund the Zap Jar from SPEND

1. From `SPEND`, send a **tiny amount** (e.g., 10k–100k sats) to zap jar’s on-chain deposit or inbound LN.
2. Wait until zap jar shows funds.

Tick:

* \[ ] Zap jar funded with small amount from SPEND

Rule:

* When it drains, top up from SPEND.
* When it overfills, sweep excess back to SPEND → VAULT, using coin control / mixing.

---

## 13.3 NWC Tokens – Handling \& Safety

Nostr Wallet Connect tokens let Nostr apps spend from zap jar.

Rules:

1. **NWC tokens are secrets**:

   * Store each in KeePass: `NWC – Zap Jar Token for <app>`.
   * Optionally in `SovStack-Work/L6-NWC/`, protected by L4.

2. NWC is allowed **only** on the Zap Jar wallet.
3. Set **spending limits** where supported (per payment / per period).
4. If misbehavior or leak is suspected:

   * Revoke affected NWC token(s).
   * Optionally rotate to a new zap jar wallet and abandon the old one.

Tick:

* \[ ] NWC tokens stored safely
* \[ ] NWC connected only to zap jar
* \[ ] Limits set

---

# 14\. ADVANCED – Ecash (Cashu / Fedimint) as Pouch

Ecash is for **tiny hot balances** only.

## 14.1 Cashu Wallet

1. Install a **Cashu**-compatible wallet on CLEAN PHONE.
2. Add a mint (preferably yours / trusted community).
3. Fund via LN or on-chain from **SPEND**.

Rules:

* Max in Cashu = what you’re OK losing if mint disappears (lunch money).
* Never use Cashu for savings or VAULT-level funds.

Tick:

* \[ ] Cashu wallet installed \& funded with tiny amount from SPEND

---

## 14.2 Fedimint (Federation Wallet)

If your community has a Fedimint:

1. Join the federation via its app.
2. Treat it as **community checking**, not personal cold storage.
3. Keep balances modest.

Tick:

* \[ ] Fedimint used only for small/medium operational balances

---

# 15\. SEED \& BACKUP MAINTENANCE (L6 Layer)

On paper, write:

> `L6 SEED \& BACKUP RULES`
>
> 1. VAULT seed = SeedSigner + metal plate(s), restore-tested.
> 2. SPEND \& ENTRY = at least paper backups; metal if balances justify.
> 3. BIP39 passphrase (if used) is \*\*never\*\* stored on same plate/paper as seed.
> 4. No photos / digital text of seeds.
> 5. At least 2 distinct physical locations for critical seed backups.

Tick:

* \[ ] L6 SEED \& BACKUP RULES written and stored

---

# 16\. Weekly / Monthly L6 Checklists

## Weekly (10–20 minutes)

On CLEAN LAPTOP:

* \[ ] Bitcoin Core running \& synced.
* \[ ] Sparrow opens VAULT (watch-only), SPEND, ENTRY.
* \[ ] All new UTXOs labeled with provenance.
* \[ ] No accidental mixing of VAULT + ENTRY in same TX.

On CLEAN PHONE:

* \[ ] PRIVATE LN wallet opens and works; balance ≈ “cash in pocket”.
* \[ ] (If used) Zap Jar still within tiny limit.
* \[ ] (If used) Cashu / Fedimint balances are small and intentional.

---

## Monthly (20–40 minutes)

* \[ ] Confirm descriptors in `SovStack-Work/L6-Wallet-Backups` (for any new wallets).
* \[ ] L4 restic backups run so L6 descriptors + notes are backed up.
* \[ ] Review labels in ENTRY / SPEND / VAULT watch-only – you still understand provenance.
* \[ ] Confirm no KYC exchange logins happened on CLEAN devices (KYC only on DIRTY).
* \[ ] SeedSigner still boots and can show VAULT descriptor.
* \[ ] (**Seed restore test lite**) – pick one backup (e.g., VAULT metal or paper) and partially re-derive addresses on a test wallet to confirm readability.

---

# 17\. L6 “NEVER DO THIS” LIST

Write:

> `L6 – NEVER DO THIS`
>
> 1. Never use \*\*KYC exchanges\*\* on CLEAN devices. (If you must use them, do it on DIRTY machines only.)
> 2. Never send sats directly from KYC exchange → VAULT.
> 3. Never mix VAULT and ENTRY coins in one transaction.
> 4. Never store seeds only on disk; always have paper (and metal for VAULT).
> 5. Never put long-term savings on \*\*Lightning\*\*, \*\*Cashu\*\*, or \*\*Fedimint\*\*.
> 6. Never install multicoin / shitcoin wallets on CLEAN devices.
> 7. Never use stablecoins as a SovStack savings asset.
> 8. Never connect NWC tokens to any wallet that holds serious funds; NWC = zap jar only.
> 9. Never engrave BIP39 passphrase on the same plate/paper as the seed.
> 10. Never assume backups work if you haven’t performed a restore-test in the last 12 months.

Tick:

* \[ ] L6 NEVER DO list written and visible near CLEAN LAPTOP

---

# 18\. Emergency Branches (L6)

### Case 1 – CLEAN LAPTOP Destroyed

* Node, Sparrow, JoinMarket, local LN node gone from that machine only.

Recovery:

1. New CLEAN LAPTOP (re-run L1).
2. Reinstall Bitcoin Core, sync.
3. Restore KeePass (`my-secrets.kdbx`) via L0/L4.
4. Reinstall Sparrow, reconnect to node.
5. Recreate VAULT watch-only from SeedSigner descriptor / metal backup.
6. Restore SPEND / ENTRY from their seeds (paper/metal), reimport descriptors if needed.

Funds intact if seeds + L4 backups exist.

---

### Case 2 – SeedSigner Lost / Destroyed

* VAULT funds are safe if metal backup (and passphrase, if used) exist.

Recovery:

1. Build a new SeedSigner from fresh hardware \& image.
2. Restore VAULT seed from metal plate (and passphrase) into new SeedSigner.
3. Re-export descriptor/xpub and verify Sparrow watch-only addresses match.

---

### Case 3 – VAULT Metal Plate Stolen / Exposed

* Attacker has seed (and maybe not passphrase).

If **no BIP39 passphrase**:

1. Immediately construct a **sweep transaction** from VAULT to a brand new VAULT2 wallet (new SeedSigner + new metal).
2. Sign via SeedSigner and broadcast.
3. After confirmations, retire old VAULT entirely.

If **with BIP39 passphrase**:

* If you believe passphrase is unknown and strong, you still have time.
* Still strongly recommended to migrate to new VAULT setup.

---

### Case 4 – You Accidentally Mixed VAULT + ENTRY UTXOs

* Label that resulting UTXO clearly: `MERGED VAULT+ENTRY (error)`.
* Treat it as “ENTRY-grade” forever.
* Option: push it through JoinMarket and only reuse in SPEND, never as pristine VAULT.

---

### Case 5 – LN Node or PRIVATE LN Wallet Lost

* Use stored seed + backup instructions to recover (wallet-specific).
* If no backup exists, LN funds may be lost.
* This is why LN is never used for core savings.

---

### Case 6 – Ecash Mint Disappears or Misbehaves

* Funds in that mint are gone.
* This is why ecash is only “cash in pocket.”

---

### Case 7 – NWC/Zap Jar Compromise

* If NWC token leaked or zap jar app compromised:

  1. Revoke token(s) immediately.
  2. Sweep remaining zap jar funds → SPEND (or direct to VAULT via structured flow).
  3. Optionally discard that zap jar wallet entirely and create a new one with new NWC tokens.

---

# 19\. Final Micro-Checklist (Caveman Version)

To confirm **L6 Sats Circuit – FINAL v2** is live and aligned with L0–L5 and future L7:

1. \[ ] Bitcoin Core is running on CLEAN LAPTOP as a pruned node with `server=1`.
2. \[ ] Sparrow is connected to Core and has **VAULT (watch-only)**, **SPEND**, and **ENTRY** wallets.
3. \[ ] VAULT is signed by **SeedSigner** (ADV) and has at least one **metal backup**, restore-tested.
4. \[ ] All wallet seeds are backed up (paper; metal for VAULT), with BIP39 passphrase policy written and enforced.
5. \[ ] Descriptors for SPEND/ENTRY (and any others) live in `SovStack-Work/L6-Wallet-Backups` and are included in L4 backups.
6. \[ ] All new sats land in ENTRY, then move (with coin control) → VAULT and → SPEND; you label every meaningful UTXO.
7. \[ ] You have at least one non-KYC ingress path (P2P or income) landing in ENTRY.
8. \[ ] (ADV) JoinMarket is installed and you’ve run at least one CoinJoin to VAULT or SPEND.
9. \[ ] PRIVATE LN wallet or node exists with only small hot funds, funded from SPEND.
10. \[ ] PUBLIC ZAP JAR wallet exists, is tiny, and any NWC tokens connect **only** to that jar.
11. \[ ] (ADV) Cashu / Fedimint used only as tiny “cash in pocket,” never for savings.
12. \[ ] L6 NEVER DO list and SEED \& BACKUP RULES are written and unbroken.

If these are true, **L6 “Sats Circuit”** is fully online: sats enter in a controlled way, get conditioned, stored, and spent through clearly separated, labeled channels, with SeedSigner + metal guarding the VAULT and tightly bounded hot exposure at every edge.

