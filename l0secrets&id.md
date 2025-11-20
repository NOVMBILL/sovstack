# 0\. Secrets \& Identity



##### What you're building

You are building:

1. **One Secret Box**
   → A KeePass vault file (`my-secrets.kdbx`)
2. **One Master Key**
   → A strong sentence you can say but others can’t guess
3. **Two Helper Tools (optional but recommended)**
   → A TOTP app (like Aegis)
   → A file-encryption tool (age) and/or identity tool (GPG) \[ADVANCED]

Everything else = copies and safety nets.

---

##### 1\. Decide Your Devices

Pick which devices you have:

* **Computer**

  * Windows / macOS / **Linux (PREFERRED!!)**

* **Phone**

  * **Android (DEGOOGLED PHONE PREFERRED!!)** → use **KeePassDX** + **Aegis**
  * **iPhone** → use **KeePassium** (no Aegis; we’ll keep TOTPs in KeePass for now)

You only need **one computer** and **one phone** to complete BASIC.

---

##### 2\. Prepare Physical Stuff

Get:

* 📝 **Paper** (2–4 sheets)✍️ **Pen**
* 💾 **2 USB sticks** (or external drives)
* 📁 **One envelope** (or small folder)

You’ll use these for:

* Writing down your master password
* Writing down a simple map of where things are
* Copying your vault to multiple places

---

##### 3\. Create Your Master Password (The One Ring)

This password protects *everything*. Do this slowly.

###### 3.1 Build the sentence

1. Think of:

   * 1 private memory (that no one else knows in detail)
   * 1 random object
   * 1 random number

2. Combine them into a weird sentence, e.g.:

> `Yellow\_tractor!fence 47 ghosts sing slowly`

Rules:

* At least **5 words**
* Mix of **lowercase, UPPERCASE, numbers, symbols**
* **Not** a quote, song lyric, or famous phrase

###### 3.2 Write it down

On paper, write exactly:

> `MASTER PASSWORD #1`
> `Yellow\_tractor!fence 47 ghosts sing slowly`

Do this **twice on two separate sheets**.

* Put each sheet into its own envelope:

  * `MASTER PASSWORD COPY A`
  * `MASTER PASSWORD COPY B`

You will store them in **two different safe places** later.

✅ When done:
You have **one strong sentence** written on **two different papers**.

---

##### 4\. Install KeePass on the Computer (Root Secret Box)

On your computer:

1. Open browser → search **“KeePassXC download”**
2. Download from the official site (or your distro’s package manager).
3. Install and open **KeePassXC**.

###### 4.1 Create the vault

1. In KeePassXC:

   * Click **“Database → New Database…”**

2. Name it:

   * `my-secrets.kdbx`

3. When asked for **Master Password**, type your sentence **exactly**.
4. Save the file in a new folder:

   * `Documents\\Secrets\\my-secrets.kdbx`
     (or similar, but remember it)

✅ When done:

* You have a file called `my-secrets.kdbx`
* It opens **only** with your master password

---

###### 5\. Create Your First Entry (Test Entry)

Inside KeePassXC:

1. Click **“Add New Entry”** (usually a + icon)
2. Fill:

   * Title: `TEST ACCOUNT`
   * Username: `test@example.com`
   * Password: click **generate** (random, long, e.g. 20–30 chars)

3. Click **Save**.

###### 5.1 Test copy-paste

1. Double-click the `TEST ACCOUNT` entry.
2. Click the little icon to copy the password.
3. Paste it into a blank text editor just to see it works, then delete it.

✅ When done:

* You know how to **add** and **use** an entry.

---

##### 6\. Make Your First Copies (Backups of Vault)

Now copy `my-secrets.kdbx` to two USB sticks.

1. Plug in **USB #1**:

   * Make a folder: `SecretsBackup`
   * Copy `my-secrets.kdbx` into it

2. Eject USB #1
3. Repeat on **USB #2**

Now you have:

* Original: computer (e.g. `Documents\\Secrets\\my-secrets.kdbx`)
* Backup 1: USB #1
* Backup 2: USB #2

###### 6.1 Store them in different places

* USB #1 → hide at home (not obvious)
* USB #2 → hide in a **different** place (trusted family, safe, office locker)

✅ When done:

* 1 vault file in **3 places**
* Master password written on **2 papers** in **2 locations**

That’s already a robust BASIC-level L0.

---

##### 7\. Put KeePass on the Phone

###### 7A. Android (KeePassDX + optional Aegis)

On your Android phone:

1. Open app store (Play or F-Droid).
2. Install **KeePassDX**.
3. Move your vault file (`my-secrets.kdbx`) to the phone:

   * Simplest for BASIC:

     * Plug phone into computer
     * Copy `my-secrets.kdbx` to `Downloads/` or a `Secrets/` folder

   * Or use a cable or local network method

4. Open **KeePassDX**:

   * Tap **Open** or **Import**
   * Find `my-secrets.kdbx`
   * Enter your master password

You should now see `TEST ACCOUNT` on the phone too.

###### 7A.1 TOTP app (Aegis) – BASIC

1. Install **Aegis Authenticator** on Android.
2. For every account where a website offers “Authenticator app / TOTP”:

   * Turn it on
   * Scan the QR code using **Aegis**

3. Aegis will now show a 6-digit code rotating every 30 seconds.

We’ll tie this to KeePass usage in Section 9.

---

###### 7B. iPhone (KeePassium)

On your iPhone:

1. Open **App Store**.
2. Install **KeePassium** (free or paid; both open-source core).
3. Move `my-secrets.kdbx` to the phone:

   * Easiest: plug phone into computer and use Finder (macOS) or iTunes (Windows) “Files” section
   * Copy into KeePassium’s app folder

4. Open KeePassium, pick `my-secrets.kdbx`, enter your master password.

You now see `TEST ACCOUNT` on iPhone.

**No Aegis on iPhone.** For BASIC iPhone-only setups we keep TOTPs inside KeePass entries or accept SMS TOTP where forced (with warnings later).

---

##### 8\. Daily Use: Simple Rules

From now on, follow these rules:

###### RULE 1 – No more “remembering” passwords

When a website asks for a password:

1. In KeePass:

   * Click **“Add New Entry”**
   * Let KeePass **generate** a long random password (20+ chars)

2. Save the entry with:

   * Title: site name (e.g. `ProtonMail`)
   * Username: your login or email

You never manually invent passwords again.

---

###### RULE 2 – Login flow (everyday use)

To log in to a site:

1. Open KeePass (computer or phone).
2. Unlock with master password.
3. Find the entry (e.g. `ProtonMail`).
4. Copy username → paste into site.
5. Copy password → paste into site.

That’s it.

---

###### RULE 3 – TOTPs (2FA codes)

For sites with 2FA:

* **If you have Android and Aegis** (recommended):

  * Use **Aegis** for TOTPs.
  * Flow:

    1. Log in with username + password from KeePass
    2. Open Aegis → copy the 6-digit code → paste

* **If you’re on iPhone only (no Aegis)**:

  * Store the TOTP secret inside KeePass entry (KeePassXC \& KeePassium support TOTP):

    * When adding 2FA, choose “manual setup”, enter the secret key in KeePass’s TOTP field.

  * Then KeePass generates the 6-digit code when you open the entry.

**Important:**
Do **not** store TOTPs in SMS if you can avoid it. SMS is fallback only, not main layer.

---

##### 9\. Maintenance: Simple Checklists

###### 9.1 Weekly

Once per week:

* ✅ Open KeePass on computer
* ✅ Open KeePass on phone
* ✅ Confirm they both still open with the same master password
* ✅ Add any new accounts created that week (if you forgot, add them now)

###### 9.2 Monthly

Once per month:

* ✅ Plug in USB #1, copy new `my-secrets.kdbx` (overwrite old one)
* ✅ Plugin USB #2, same copy
* ✅ Check `TEST ACCOUNT` entry exists in all 3 copies (PC + 2 USBs)
* ✅ Check paper master-password envelopes still exist

---

##### 10\. “Oh No!” Scenarios (Foolproof Branches)

###### Scenario A – You forget the master password

* If **both paper copi**es are gone → vault is lost forever. That’s by design.
* ⦁	If at least **one paper exists**:

  * Go read it.
  * Use it to open the vault.
  * Optionally, change master password and update both papers.

###### Scenario B – Computer dies / stolen

* Vault is safe if the master password is strong.
* Use your **phone** or **one USB backup** on a new computer:

  1. Install KeePassXC again.
  2. Copy `my-secrets.kdbx` from USB or phone to new computer.
  3. Open with master password.

###### Scenario C – Phone dies / stolen

* Install KeePass again on new phone.
* Move `my-secrets.kdbx` from computer or USB to the new phone.
* Use the master password.

###### Scenario D – One USB lost

* Other USB still has backup.
* Make a **new third copy** from computer and store it somewhere new if needed.

---

##### 11\. Simple “Heir / Trusted Person” Instructions (One Page)

Write **one more paper**:

Title: `HOW TO OPEN MY SECRET BOX`

1. “There is a file called **my-secrets.kdbx**”

   * It is on:

     * \[ ] My computer (location: `\_\_\_\_\_\_\_\_\_\_`)
     * \[ ] USB #1 (location: `\_\_\_\_\_\_\_\_\_\_`)
     * \[ ] USB #2 (location: `\_\_\_\_\_\_\_\_\_\_`)

2. “There is a **Master Password** for this file”

   * It is written on:

     * \[ ] Envelope `MASTER PASSWORD COPY A` (location: `\_\_\_\_\_\_\_\_\_\_`)
     * \[ ] Envelope `MASTER PASSWORD COPY B` (location: `\_\_\_\_\_\_\_\_\_\_`)

3. “To open the file, you must:”

   * Install KeePassXC (computer) or KeePassDX/KeePassium (phone)
   * Open `my-secrets.kdbx`
   * Type the master password from the envelope

Put this paper somewhere obvious: with your will, in a safe, etc.

---

##### 12\. ADVANCED – age \& GPG

When you're ready for stronger armor **and** you can handle 1–2 extra steps, add this:

###### 12.1 Install GPG (identity \& signatures)

On your main computer:

1. Install GPG:

   * Windows: **Gpg4win**
   * macOS: **GPG Suite** or `gpg` via Homebrew
   * Linux: `gpg` usually preinstalled or via package manager

2. Create one primary key:

   * Real name or pseudonym, simple email
   * Strong passphrase (can be different from vault master password)

3. Write in KeePass:

   * Entry: `GPG MASTER KEY`
   * Put:

     * Key fingerprint
     * Where key is stored (path)
     * Passphrase

**Use case** (minimal): sign a text file `KEY-OWNERSHIP.txt` saying “This key belongs to me” so you tie identity to an actual key in a verifiable way.

###### 12.2 Install age (simple file encryption)

On your main computer:

1. Install `age` (via package, brew, or binary).
2. Run once to create a key:

   * `age-keygen -o age.key`

3. Store `age.key` path \& passphrase (if any) inside KeePass in entry `AGE KEY`.

###### 12.2.1 Encrypt your vault backups

Instead of copying `my-secrets.kdbx` directly to USB, do:

1. On computer:

   * `age -r YOUR\_AGE\_PUBLIC\_KEY -o my-secrets.kdbx.age my-secrets.kdbx`

2. Copy `my-secrets.kdbx.age` to USBs instead of raw file.

Now, if someone steals the USB, they see only encrypted garbage; they need:

* age key
* plus KeePass master password
  to read anything.

**NOTE:** test decryption at least once:

* Copy `my-secrets.kdbx.age` to a test folder
* Decrypt with `age` to `my-secrets-restored.kdbx`
* Open that file in KeePass with master password

If this works once, you’re good.

---

##### 13\. Final Checklist

If someone only wants the shortest “DO THESE THINGS” list:

1. 🧠 Make **one strong sentence** (master password) and write it on **two papers**.
2. 💻 Install **KeePassXC** on your computer; make `my-secrets.kdbx`.
3. 📱 Install **KeePassDX** (Android) or **KeePassium** (iPhone); open `my-secrets.kdbx` on phone.
4. 🔑 For every website:

   * Let KeePass generate passwords.
   * Store username + password in KeePass.

5. 🧱 Install **Aegis** (Android) and use it for 2FA codes (or KeePass TOTPs if on iPhone).
6. 💾 Copy `my-secrets.kdbx` onto **2 USBs** and hide them in **two different places**.
7. 🔄 Once a month, update both USBs with the latest `my-secrets.kdbx`.
8. 🧪 Once a month, **test a restore** from a USB onto KeePass on your computer.

If all 8 are true, your L0 layer is **up** and **foolproof for normal failures** (device loss, theft, forgetfulness), and you can start building higher layers on top.

