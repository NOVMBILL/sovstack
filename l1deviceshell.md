Below is the **L1 “Device Shell” Protocol**
It **starts where L0 ended** (you already have `my-secrets.kdbx` + master password).

---

##### 0\. What You’re Building at L1

You are building **three things** around your L0 Secret Box:

1. **CLEAN LAPTOP**
   → Runs Linux (Debian or similar) with full-disk encryption.
   → Holds your main `my-secrets.kdbx` and SovStack work.
2. **CLEAN PHONE**
   → Best: GrapheneOS on a Pixel
   → If not possible: a hardened phone with clear warnings.
3. **ADVANCED OPERATOR GEAR**
   → Qubes OS laptop (compartments)
   → Tails USB (amnesic, Tor-only)
   → Burner phones

Everything else (Windows, macOS, iOS, stock Android) = **DIRTY DEVICES** = for the synthetic world only.

---

##### 1\. Prerequisites

You already have from **L0**:

* ✅ `my-secrets.kdbx` on at least one computer
* ✅ Master password written on 2 papers in 2 different safe places
* ✅ 2 USB sticks with `my-secrets.kdbx` (or you can create them now)

For **L1**, get:

* 📝 Paper + ✍️ Pen
* 🏷️ 4 small labels or tape (for naming devices)
* 💻 At least **one laptop/computer**
* 📱 At least **one smartphone**
* 💾 2 USB sticks (can reuse L0 ones)

---

##### 2\. Assign Roles to Your Devices

You **must decide roles**. Each physical device gets a sticker.

###### 2.1 Draw a simple table on paper

Write:

> `DEVICE ROLES`
>
> 1. Laptop A – role: \_\_\_\_\_\_
> 2. Laptop B – role: \_\_\_\_\_\_
> 3. Phone A – role: \_\_\_\_\_\_
> 4. Phone B – role: \_\_\_\_\_\_

Now assign:

* **One laptop** → `CLEAN LAPTOP`
* **One phone** → `CLEAN PHONE` (or “TEMP CLEAN PHONE” if you’re using stock OS for now)
* All other devices → `DIRTY`

###### 2.2 Put labels on devices

On the actual machines:

* On chosen SovStack laptop:
  → Stick a label: `CLEAN LAPTOP`
* On chosen SovStack phone:
  → Stick a label: `CLEAN PHONE` (or `TEMP CLEAN PHONE`)
* On every other device (PC/phone/tablet):
  → Stick a label: `DIRTY`

**Rule from now on:**

* **CLEAN** = SovStack, secrets, Bitcoin, private comms.
* **DIRTY** = Synthetic Stack junk you may still need to access.

---

##### 3\. Build the CLEAN LAPTOP (Linux + FDE)

###### 3.1 Back up anything you need

On the laptop you picked as `CLEAN LAPTOP`:

* If it has old files you care about:
  → Copy them to an external disk or other machine.
* You are about to **erase this disk**.

Tick when done:

* \[ ] Important files backed up or confirmed not needed.

---

###### 3.2 Download Debian (or similar Linux)

On **any** computer (can be DIRTY temporarily):

1. Open browser → search: `Debian download`
2. Go to official site (look for `debian.org`).
3. Download:

   * “64-bit PC (amd64)” ISO
   * For beginners: use the **stable** version.

4. Plug in a spare USB stick (not your L0 backup ones if you can avoid it).
5. Use a tool to write the ISO to USB (pick one):

   * Windows: **Rufus** or **balenaEtcher**
   * macOS/Linux: **balenaEtcher** or `dd` if you know how

You now have a **Debian installer USB**.

Tick:

* \[ ] Debian ISO downloaded from `debian.org`
* \[ ] Installer USB created

---

###### 3.3 Install Debian with full-disk encryption

On the **CLEAN LAPTOP**:

1. Plug in the Debian installer USB.
2. Reboot the laptop and choose to **boot from USB**
   (usually pressing `F12`, `Esc`, or similar when turning it on).
3. When Debian installer appears:

   * Choose language, keyboard, etc.
   * When asked about partitioning:

     * Choose:
       **Guided – use entire disk and set up encrypted LVM**

4. You will be asked to create:

   * **Disk encryption passphrase** (this is *not* your master password)
   * **User account** + **user password**

###### 3.3.1 Record your new secrets

On paper write:

> `CLEAN LAPTOP – DISK ENCRYPTION PASSWORD`
> \[exact passphrase you chose]
>
> `CLEAN LAPTOP – USER LOGIN`
> Username: \_\_\_\_\_\_
> Password: \_\_\_\_\_\_

Put this paper in the same kind of safe place as your L0 backups (or with them).

Tick:

* \[ ] Laptop disk encryption passphrase written on paper
* \[ ] Laptop user login and password written on paper

Finish the installer and reboot into Debian.

---

###### 3.4 First boot hardening

On the new Debian desktop:

1. **Update the system**

   * Open the “Software” or “Updates” tool and install all updates
   * Or run in terminal: `sudo apt update \&\& sudo apt upgrade`

2. **Enable a firewall**

   * Install `ufw`:
     `sudo apt install ufw`
   * Enable it:
     `sudo ufw enable`

3. **Create a “Secrets” folder**

   * In your home folder, make: `Secrets/`

Tick:

* \[ ] System updated
* \[ ] Firewall enabled (ufw active)
* \[ ] `Secrets/` folder created

---

###### 3.5 Move L0 vault onto CLEAN LAPTOP

Copy your `my-secrets.kdbx` onto this new machine:

1. Plug in one of your L0 USB backup sticks.
2. Open the USB drive.
3. Copy `my-secrets.kdbx` into `~/Secrets/` (your Secrets folder).

Now install KeePassXC again:

1. Open Software/Store → search `KeePassXC`
2. Install and open.

In KeePassXC:

1. Click **Open Database**
2. Choose `~/Secrets/my-secrets.kdbx`
3. Enter your **L0 master password** (your Secret Box sentence)
4. Verify you see your entries (including `TEST ACCOUNT`).

Tick:

* \[ ] `my-secrets.kdbx` copied to `CLEAN LAPTOP`
* \[ ] KeePassXC installed and vault opens correctly

---

##### 4\. Build the CLEAN PHONE

###### 4.1 Check what phone you have

Look at the phone labeled `CLEAN PHONE`:

* If it’s a **supported Google Pixel** (e.g. 5a, 6, 6a, 7, 7a, 8, etc.):
  → **Target = GrapheneOS** (best option)
* If it’s **not a Pixel**:
  → For now, it will be a **TEMP CLEAN PHONE** with hardened stock OS (or DivestOS/Calyx if available, in ADVANCED)

Write on your paper:

> `CLEAN PHONE MODEL: \_\_\_\_\_\_\_`
> `PLAN: GrapheneOS / TEMP STOCK OS`

Tick:

* \[ ] Phone model identified
* \[ ] Plan chosen

---

###### 4.2 If Pixel: Install GrapheneOS (Basic flow)

*(If not Pixel, skip to 4.3)*

Use the **CLEAN LAPTOP** for this.

1. On CLEAN LAPTOP, open browser → go to:
   `https://grapheneos.org/install/web`
2. Follow the **web installer** instructions on that page exactly:

   You will:

   * Turn on **Developer options** on the Pixel
   * Enable **OEM unlocking**
   * Connect phone to laptop via USB
   * Use the site’s built-in installer to flash GrapheneOS

3. When installer says finished:

   * Reboot the phone
   * Complete basic setup (language, time, Wi-Fi, etc.)

   ###### 4.2.1 Set phone lock

   On the new GrapheneOS:

1. Set a **strong 6+ digit PIN** (no easy patterns, no birthdays).
2. Disable fingerprint/face unlock

   Write on paper:

   > `CLEAN PHONE – LOCK PIN: \_\_\_\_\_\_`
   > (keep it somewhere safe, separate from the phone)

   ###### 4.2.2 Create basic app setup

   On GrapheneOS:

1. Do **not** log into a Google account (unless you explicitly need sandboxed Play later).
2. Install only:

   * Your browser of choice (privacy-friendly)
   * KeePass-compatible app for later (we handle this in a second)

   Tick:

* \[ ] GrapheneOS installed successfully
* \[ ] Strong PIN set and written down
* \[ ] No Google account added (or you accept it as a conscious tradeoff)

  ---

  ###### 4.3 If not Pixel: TEMP CLEAN PHONE hardening (stock OS)

  On this phone:

1. Set a **strong lock**:

   * 6+ digit PIN

2. Turn off obvious tracking where possible:

   * Disable “ad personalization” / “analytics” / “diagnostics”
   * Turn off “back up to cloud” for sensitive apps if possible

3. Remove or disable junk apps you don’t need (social media, games, etc.).
4. Plan: **this phone is still weaker** than GrapheneOS; treat it as **TEMP CLEAN** until you can upgrade hardware/OS.

   Write on paper:

   > `TEMP CLEAN PHONE LIMITS: no KYC accounts, no social media, light app list only`

   Tick:

* \[ ] Strong PIN set
* \[ ] Tracking toggles adjusted
* \[ ] Only essential apps left

  ---

  ###### 4.4 Put KeePass vault onto CLEAN PHONE

  On the **CLEAN LAPTOP**:

1. Make a copy of `my-secrets.kdbx` into a temporary folder (or use the same file).

   Then:

1. Connect CLEAN PHONE to CLEAN LAPTOP with USB.
2. On the phone, enable file transfer (if asked).
3. Copy `my-secrets.kdbx` onto the phone into a `Secrets` folder (create one if needed).

   On the phone:

* Install a KeePass-compatible app:

  * GrapheneOS / Android: **KeePassDX** (or similar FOSS KeePass app)
  * Stock Android: same
  * iPhone TEMP CLEAN phone (if that’s what you chose): **KeePassium**

  Open the app:

1. Tap **Open Database**.
2. Choose `my-secrets.kdbx`.
3. Enter your master password.
4. Check that `TEST ACCOUNT` appears.

   Tick:

* \[ ] `my-secrets.kdbx` copied to CLEAN PHONE
* \[ ] App opens vault successfully

  ---

  ##### 5\. “Never Do This on CLEAN Devices” Rules

  Write a big heading on paper:

  > `NEVER DO THIS ON CLEAN LAPTOP OR CLEAN PHONE`

  Under it, list:

1. No **Google / Apple / Microsoft account logins** (except sandboxed Play on Graphene if you *really* need it, and only for specific apps).
2. No **social media** (Facebook, Instagram, TikTok, etc.).
3. No **KYC exchanges or banking apps**.
4. No **random app installs** “just to try”.
5. No opening **unknown email attachments** or random USB sticks.

   Stick this paper somewhere near your CLEAN LAPTOP.

   Tick:

* \[ ] “NEVER DO THIS” list written and visible

  ---

  ##### 6\. Daily Use Workflow 

  ###### 6.1 CLEAN LAPTOP is for:

* KeePass vault (L0)
* Bitcoin wallets \& tools
* Private chat / privacy tools
* SovStack planning, documents, research

  ###### 6.2 CLEAN PHONE is for:

* 2FA / authenticators (if on this device)
* Private chat (Signal/Nostr/etc.), Bitcoin mobile wallets
* Checking SovStack-related info

  ###### 6.3 DIRTY devices are for:

* Any SynthStack junk that you absolutely need (you should work on leaving this all behind): Social media, Normal email, Banking / KYC exchanges, Entertainment, browsing, junk

  **Rule:**
  If you ever log into social media or KYC on a CLEAN device → it instantly becomes **DIRTY**. You must either:

* Wipe and rebuild it as CLEAN, or
* Reassign its role permanently to DIRTY.

  ---

  ##### 7\. Regular Checks (L1 Maintenance)

  ###### Weekly (5–10 minutes)

  On CLEAN LAPTOP:

* \[ ] Check that entering disk password at boot works (you didn’t forget).
* \[ ] Open KeePassXC, open `my-secrets.kdbx`.
* \[ ] Confirm you still remember your CLEAN LAPTOP user password.

  On CLEAN PHONE:

* \[ ] Unlock phone with PIN.
* \[ ] Open KeePass app and unlock vault.

  ###### Monthly (15–30 minutes)

* \[ ] Apply system updates on CLEAN LAPTOP.
* \[ ] Apply OS/app updates on CLEAN PHONE.
* \[ ] Confirm your two USB backups (from L0) still open `my-secrets.kdbx` on CLEAN LAPTOP.
* \[ ] Check your “NEVER DO THIS” list and confirm you didn’t break any rule.

  ---

  ##### 8\. ADVANCED L1: Operator Gear

  Do these **only** if BASIC is solid.

  ---

  ###### 8.1 Qubes OS Operator Laptop

  Goal: one extra laptop labeled **`OPERATOR LAPTOP`**

1. Choose a laptop compatible with Qubes OS (check `qubes-os.org/hcl`).
2. Back up any data (you will wipe it).
3. Download Qubes OS from official site.
4. Create Qubes installer USB (similar process as Debian).
5. Install Qubes, following their guide.

   After install:

* Create qubes like:

  * `vault` – no network, for secrets
  * `btc` – Bitcoin only
  * `work` – documents
  * `untrusted` – random browsing

  Stick a label on that laptop: `OPERATOR LAPTOP – QUBES`.

  Rule: `vault` qube never touches the network.

  ---

  ###### 8.2 Tails USB (Stealth Session Stick)

  Goal: one USB labeled **`TAILS`**

1. On CLEAN LAPTOP or OPERATOR LAPTOP:

   * Download **Tails** from official site.
   * Use their “installer” instructions to put it onto a USB.

2. To use:

   * Plug Tails USB into any computer.
   * Boot from USB.
   * Use it for specific high-risk sessions (Tor-only).

   Rule: When you shut down Tails, it forgets everything (unless you deliberately set up persistent storage).

   ---

   ###### 8.3 Burner Phones (DivestOS / CalyxOS)

   If you have spare phones:

1. Label them `BURNER 1`, `BURNER 2`.
2. If supported, flash:

   * **DivestOS** (preferred)
   * Or **CalyxOS**

3. These are for:

   * Travel
   * One-time ops
   * Situations where you don’t want to bring CLEAN PHONE

   Rule: Burners never hold your L0 vault; they are for temporary identities.

   ---

   ##### 9\. Final Micro-Checklist

   If you want the **shortest summary** to verify you’re done:

1. \[ ] **One laptop** is wiped and running Linux with full-disk encryption, labeled `CLEAN LAPTOP`.
2. \[ ] **One phone** is set aside and hardened as `CLEAN PHONE` (GrapheneOS if Pixel; TEMP CLEAN otherwise).
3. \[ ] `my-secrets.kdbx` is on CLEAN LAPTOP and CLEAN PHONE only (plus encrypted USB backups).
4. \[ ] You have **written rules** taped near CLEAN LAPTOP: what you are **never** allowed to do on it.
5. \[ ] All other devices are labeled `DIRTY` and used only for normal world / synthetic stuff.
6. \[ ] Once a week you unlock everything and check it still works.
7. \[ ] Once a month you update systems and test restoring your vault from USB on CLEAN LAPTOP.

   If all 7 are true, your **L1 Device Shell** is in place around your **L0 Secret Box** and you can safely start stacking higher layers on top.

