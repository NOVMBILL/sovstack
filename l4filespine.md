Below is the **L4 “File Spine” Protocol** – only this layer, nothing else.
It **sits on top of L0–L3** (Secret Box → Device Shell → Network Cloak → Comms Veil).

Think **IKEA / LEGO manual**: boxes to tick, steps in order.

Two levels:

* **BASIC (MVS)** – minimum everyone does
* **ADVANCED** – extra armor (second backup, age, Syncthing, remote copy)

---

# 0. What You’re Building at L4

You are building **four simple things**:

1. **ONE WORK FOLDER**
   → Where all important documents live (on CLEAN LAPTOP)

2. **ONE LOCAL BACKUP**
   → External USB drive `BACKUP_A`
   → Automatically encrypted with `restic`

3. **ONE RESTORE TEST**
   → A folder you can restore into, to prove backups work

4. **(ADVANCED) SECOND BACKUP + OPTIONAL SYNC & age ARCHIVE**
   → Offsite `BACKUP_B` + optional encrypted tarball and multi-device sync

Everything else = copies and labels.

---

# 1. Prerequisites

You already have from earlier layers:

* ✅ **CLEAN LAPTOP** (Debian or similar, with full-disk encryption)
* ✅ **CLEAN PHONE** (but we mainly use the laptop at L4)
* ✅ **KeePass vault** (`my-secrets.kdbx`) on CLEAN LAPTOP
* ✅ **VPN** on CLEAN LAPTOP (L2)

For L4 you need *physical stuff*:

* 📝 Paper + ✍️ Pen
* 💾 **1 or 2 USB external drives** (ideally empty or ok to erase)

  * At least **64 GB** each if you have lots of files
* 🗂️ Labels or tape to name drives:

  * `BACKUP_A`
  * `BACKUP_B` (ADVANCED / optional)

---

# 2. Name Your Drives and Work Folder

## 2.1 Label the drives (physical + software)

1. Take your first external drive.

   * Stick a label on it: `BACKUP_A`
2. (Optional ADVANCED) Take second drive.

   * Label: `BACKUP_B`

On CLEAN LAPTOP:

1. Plug in `BACKUP_A`.
2. Open **Files** (file manager).
3. In the side bar, right-click the drive name → **Rename** to `BACKUP_A`.

If you have `BACKUP_B`, do the same (rename to `BACKUP_B`).

On paper, write:

> `L4 DRIVES`
> BACKUP_A: physical location = ______
> BACKUP_B: physical location = ______ (if you have it)

Tick:

* [ ] BACKUP_A labeled (physical + in Files)
* [ ] BACKUP_B labeled (if you have it)

---

## 2.2 Create your WORK FOLDER

On CLEAN LAPTOP:

1. Open **Files**.
2. Go to your **Home** folder.
3. Create a new folder:

   * Name: `SovStack-Work`

On paper:

> `L4 WORK FOLDER`
> Path: `/home/<yourname>/SovStack-Work`

Tick:

* [ ] `SovStack-Work` folder created

**RULE:**
All important documents you care about (plans, PDFs, notes, text files, export files from apps) should live **inside `SovStack-Work` or its subfolders**.

---

# 3. Install restic (Backup Engine) on CLEAN LAPTOP

We’ll use `restic` to encrypt and back up `SovStack-Work` to `BACKUP_A`.

## 3.1 Install restic

On CLEAN LAPTOP:

1. Open **Terminal**.
2. Type (or copy-paste) and press Enter:

```bash
sudo apt update
sudo apt install restic
```

Enter your **user password** when asked.

Tick:

* [ ] `restic` installed without errors

---

## 3.2 Create a restic password (and store it in KeePass)

This is the **backup encryption password**. It can be long and random; you will store it in KeePass and in a small text file.

1. Open **KeePassXC** on CLEAN LAPTOP.
2. Add a new entry:

   * Title: `RESTIC BACKUP PASSWORD`
   * Username: leave blank or `restic`
   * Password: click **Generate** and create a **32+ character** password.
3. Save the entry.

Now create a password file on disk:

1. Open **Text Editor**.

2. Copy the password from KeePass entry `RESTIC BACKUP PASSWORD`.

3. Paste into the empty text file.

4. Save as:

   * `restic-password.txt` in your `Secrets` folder:

   Path: `/home/<yourname>/Secrets/restic-password.txt`

5. Close the text editor.

On paper, write:

> `RESTIC`
> Password stored in KeePass entry: `RESTIC BACKUP PASSWORD`
> File copy location: `/home/<yourname>/Secrets/restic-password.txt`

Tick:

* [ ] KeePass entry created for RESTIC BACKUP PASSWORD
* [ ] `restic-password.txt` created in `Secrets` folder

*(This file lives on your encrypted disk; if someone steals only the external drive, they do **not** have this password.)*

---

# 4. Make a Backup Script for BACKUP_A (Basic)

We will make a simple script. When you run it, it will:

1. Check if repository exists on `BACKUP_A`
2. Create it if needed
3. Back up `SovStack-Work`
4. Keep a simple rotation of old backups

## 4.1 Find path to BACKUP_A

On CLEAN LAPTOP:

1. Plug in `BACKUP_A`.

2. Open **Files**.

3. Click on `BACKUP_A` in the side bar.

4. Press `Ctrl + L` (or look for a location/path bar).

   * You should see something like:

   `/media/<yourname>/BACKUP_A`
   or
   `/run/media/<yourname>/BACKUP_A`

5. **Write down the exact path** on paper:

> `BACKUP_A PATH: ____________________`

Tick:

* [ ] BACKUP_A path written on paper

---

## 4.2 Create folder for the restic repository on BACKUP_A

In **Files**, with `BACKUP_A` open:

1. Right-click in empty area → **New Folder**.
2. Name it: `restic-repo`

So the full path is something like:

* `/media/<yourname>/BACKUP_A/restic-repo`
  or
* `/run/media/<yourname>/BACKUP_A/restic-repo`

Write the full path on paper:

> `BACKUP_A RESTIC REPO:`
> `/media/<yourname>/BACKUP_A/restic-repo` (or whatever it is)

Tick:

* [ ] `restic-repo` folder created on BACKUP_A

---

## 4.3 Create the backup script

On CLEAN LAPTOP:

1. Open **Text Editor**.
2. Paste the following script (adjust two PATHS):

```bash
#!/bin/bash

# === L4 BACKUP TO BACKUP_A ===

# 1. Tell restic where to store the repository and find the password
export RESTIC_PASSWORD_FILE="$HOME/Secrets/restic-password.txt"
export RESTIC_REPOSITORY="/media/$USER/BACKUP_A/restic-repo"

# If your BACKUP_A path was /run/media/... change the line above to:
# export RESTIC_REPOSITORY="/run/media/$USER/BACKUP_A/restic-repo"

# 2. Initialize the repository if needed
restic snapshots >/dev/null 2>&1
if [ $? -ne 0 ]; then
  echo "Initializing restic repository on BACKUP_A..."
  restic init
fi

# 3. Run the backup of your WORK FOLDER
echo "Starting backup of SovStack-Work..."
restic backup "$HOME/SovStack-Work"

# 4. Apply simple retention policy (tune if you like)
echo "Applying retention (7 daily, 4 weekly, 6 monthly)..."
restic forget --keep-daily 7 --keep-weekly 4 --keep-monthly 6 --prune

echo "Backup to BACKUP_A completed."
```

3. Edit the `RESTIC_REPOSITORY` line so that it matches the path you wrote down (`/media/...` or `/run/media/...`).

4. Save the file as:

   * `backup_to_BACKUP_A.sh` in your **home** folder:

   `/home/<yourname>/backup_to_BACKUP_A.sh`

5. Make it executable:

   * Open **Terminal** and run:

```bash
chmod +x ~/backup_to_BACKUP_A.sh
```

Tick:

* [ ] Script `backup_to_BACKUP_A.sh` saved in home folder
* [ ] Script made executable with `chmod +x`

---

## 4.4 Run your FIRST backup (Basic)

On CLEAN LAPTOP:

1. Plug in `BACKUP_A`.
2. Wait for it to appear in **Files**.
3. Open **Terminal**.
4. Run:

```bash
~/backup_to_BACKUP_A.sh
```

The first time:

* It will say “Initializing restic repository…”
* It will take longer (first backup).

Watch for `Backup to BACKUP_A completed.` at the end.

Tick:

* [ ] First backup to BACKUP_A completed with no errors

---

# 5. Test a Restore (Prove It Works)

We now prove that backups are **real**, not magic.

## 5.1 Make a test file

On CLEAN LAPTOP:

1. Inside `SovStack-Work`, create a file:

   * Name: `TEST-L4.txt`
   * Put some text in it, e.g. `Hello L4 backup`

2. Save it.

Now run backup again:

```bash
~/backup_to_BACKUP_A.sh
```

Tick:

* [ ] `TEST-L4.txt` created
* [ ] Second backup run completed

---

## 5.2 Restore into a test folder

1. On CLEAN LAPTOP, create a new folder:

   * `SovStack-Restore-Test` in your home:

   `/home/<yourname>/SovStack-Restore-Test`

2. In **Terminal**, with `BACKUP_A` still plugged in, run:

```bash
export RESTIC_PASSWORD_FILE="$HOME/Secrets/restic-password.txt"
export RESTIC_REPOSITORY="/media/$USER/BACKUP_A/restic-repo"
# or /run/media/... if that's your path

restic snapshots
```

You should see a list of snapshots.

3. Now restore the latest snapshot to the test folder:

```bash
restic restore latest --target "$HOME/SovStack-Restore-Test"
```

4. When done, open **Files** → `SovStack-Restore-Test` → `home/<yourname>/SovStack-Work/` (restic recreates the path).

5. Confirm that `TEST-L4.txt` exists and has the correct text.

Tick:

* [ ] `restic snapshots` showed snapshots
* [ ] `restic restore` ran without errors
* [ ] `TEST-L4.txt` appeared in `SovStack-Restore-Test` with correct content

Now you **know** backups work.

You can delete `SovStack-Restore-Test` afterwards if you want.

---

# 6. Daily / Weekly L4 Rules (Basic)

On paper, write:

> `L4 DAILY / WEEKLY RULES`
>
> **DAILY (or whenever working):**
> – Save all important files into `SovStack-Work` (nowhere else).
>
> **WEEKLY:**
> – Plug in BACKUP_A.
> – Run: `~/backup_to_BACKUP_A.sh`
> – Wait for “Backup completed.”
>
> **MONTHLY:**
> – Do one test restore of a small file into `SovStack-Restore-Test` (like we did once).

Tick:

* [ ] L4 DAILY / WEEKLY RULES written and placed near CLEAN LAPTOP

---

# 7. L4 “NEVER DO” LIST (Basic)

New heading on paper:

> `L4 – NEVER DO THIS`
>
> 1. Never keep your only copy of an important file **outside** `SovStack-Work`.
> 2. Never edit or delete files **inside** the `restic-repo` folder directly.
> 3. Never keep only **one** backup (BACKUP_A only) for life-or-death data. (ADVANCED adds BACKUP_B.)
> 4. Never store `restic-password.txt` on any device that is not CLEAN or full-disk encrypted.
> 5. Never assume backups work if you haven’t tested a restore **in the last month**.

Tick:

* [ ] L4 NEVER DO list written and visible

At this point, **BASIC L4 is done**: you have one WORK FOLDER, one encrypted backup to BACKUP_A, and a tested restore path.

---

# 8. ADVANCED L4 – Second Backup + age + Sync

Only do this when BASIC is solid.

## 8.1 BACKUP_B – second, offsite backup

Concept:

* `BACKUP_A` stays at home.
* `BACKUP_B` lives somewhere else (trusted friend, office locker, safe box).

### 8.1.1 Prepare BACKUP_B

Repeat the same steps as BACKUP_A:

1. Label drive physically: `BACKUP_B`.
2. Plug into CLEAN LAPTOP.
3. Rename in **Files** to `BACKUP_B`.
4. Create folder `restic-repo` on it.
5. Note path (`/media/<yourname>/BACKUP_B` or `/run/media/...`).

On paper:

> `BACKUP_B PATH: ____________________`

Tick:

* [ ] BACKUP_B labeled, path noted
* [ ] `restic-repo` created on BACKUP_B

---

### 8.1.2 Create second backup script for BACKUP_B

On CLEAN LAPTOP:

1. Open **Text Editor**.
2. Paste and adjust the script:

```bash
#!/bin/bash

# === L4 BACKUP TO BACKUP_B ===

export RESTIC_PASSWORD_FILE="$HOME/Secrets/restic-password.txt"
export RESTIC_REPOSITORY="/media/$USER/BACKUP_B/restic-repo"
# or /run/media/... if needed

restic snapshots >/dev/null 2>&1
if [ $? -ne 0 ]; then
  echo "Initializing restic repository on BACKUP_B..."
  restic init
fi

echo "Starting backup of SovStack-Work to BACKUP_B..."
restic backup "$HOME/SovStack-Work"

echo "Backup to BACKUP_B completed."
```

3. Save as:

   * `backup_to_BACKUP_B.sh` in your home folder.

4. Make executable:

```bash
chmod +x ~/backup_to_BACKUP_B.sh
```

Tick:

* [ ] `backup_to_BACKUP_B.sh` created and made executable

---

### 8.1.3 Run first BACKUP_B backup

1. Plug in `BACKUP_B`.
2. In **Terminal**:

```bash
~/backup_to_BACKUP_B.sh
```

3. Wait for completion.

Then **unplug BACKUP_B** and move it to a **different physical location** than BACKUP_A.

On paper:

> `BACKUP_B STORAGE LOCATION: _____________`

Tick:

* [ ] First backup to BACKUP_B done
* [ ] BACKUP_B stored offsite / in different place

**ADVANCED RULE:**

* BACKUP_A = weekly, stays at home.
* BACKUP_B = monthly, kept elsewhere.

---

## 8.2 age – Super-Secret Archive

age is for encrypting **one big archive** (e.g. all seed phrases, codex exports, ultra-sensitive docs) into a single `.age` file you can store anywhere.

### 8.2.1 Install age

On CLEAN LAPTOP:

```bash
sudo apt install age
```

Tick:

* [ ] `age` installed

---

### 8.2.2 Create an age key

On CLEAN LAPTOP:

```bash
age-keygen -o $HOME/Secrets/age.key
```

This prints something like:

`# created: ...`
`# public key: age1something...`

Copy the public key line and store:

1. In KeePass:

   * New entry: `AGE KEY`
   * Put:

     * Username: `age`
     * Password: (optional passphrase if you protect the key file)
     * Notes: paste the `public key: age1...` there

2. On paper:

> `AGE KEY`
> File: `/home/<yourname>/Secrets/age.key`
> Public key: age1____________________

Tick:

* [ ] `age.key` created
* [ ] Public key stored in KeePass and on paper

---

### 8.2.3 Make a “Super Secret” archive

1. Decide what goes in it:

   * A folder like `SovStack-Work/Ultra-Secret/` containing:

     * Seed phrase PDFs
     * Codex exports
     * Most sensitive documents

2. On CLEAN LAPTOP, in **Terminal**:

```bash
cd "$HOME/SovStack-Work"
tar -cvf Ultra-Secret.tar Ultra-Secret
```

This creates `Ultra-Secret.tar` inside `SovStack-Work`.

3. Now encrypt it with age (replace `age1...` with your public key from KeePass):

```bash
cd "$HOME/SovStack-Work"
age -r "age1YOURPUBLICKEY..." -o Ultra-Secret.tar.age Ultra-Secret.tar
```

4. Verify file exists:

```bash
ls Ultra-Secret.tar.age
```

Tick:

* [ ] `Ultra-Secret.tar.age` created

Now you can:

* Delete `Ultra-Secret.tar` (the unencrypted tarball):

```bash
rm Ultra-Secret.tar
```

**DO NOT** delete the original `Ultra-Secret` folder yet until you are sure everything works.

---

### 8.2.4 Test decrypting the age archive

On CLEAN LAPTOP:

```bash
cd "$HOME/SovStack-Work"
age -d -i "$HOME/Secrets/age.key" Ultra-Secret.tar.age > Ultra-Secret-RESTORED.tar
```

Then:

```bash
tar -xvf Ultra-Secret-RESTORED.tar -C "$HOME/SovStack-Restore-Test"
```

Check inside `SovStack-Restore-Test/Ultra-Secret` that files look correct.

If all good, you know you can recover secrets from just:

* `Ultra-Secret.tar.age`
* `age.key`
* plus your **disk encryption** and device.

You may then **optionally**:

* Delete `Ultra-Secret` original folder (if you want only encrypted form).
* Or keep it but rely on restic backups.

Tick:

* [ ] age decryption tested and files verified

---

## 8.3 Syncthing – Multi-Device File Sync (Optional Advanced)

Use this only if you want `SovStack-Work` available on more than one CLEAN device.

### 8.3.1 Install Syncthing on CLEAN LAPTOP

```bash
sudo apt install syncthing
syncthing &
```

This starts Syncthing and opens a web UI (usually at `http://127.0.0.1:8384` in browser).

In Syncthing UI:

1. Set a **Device Name**, e.g. `CLEAN-LAPTOP`.
2. Add a **Folder**:

   * Folder path: `/home/<yourname>/SovStack-Work`
   * Folder label: `SovStack-Work`
   * Folder ID: accept default or simple name
   * Click **Save**.

Tick:

* [ ] Syncthing running on CLEAN LAPTOP
* [ ] `SovStack-Work` folder added

---

### 8.3.2 Install Syncthing on CLEAN PHONE (Android)

*(On iPhone, Syncthing support is messy; treat multi-device sync as laptop ↔ Android or laptop ↔ another laptop.)*

On CLEAN PHONE (Android):

1. Install **Syncthing** (from F-Droid or Play Store).

2. Open Syncthing:

   * Set device name, e.g. `CLEAN-PHONE`.

3. On Syncthing UI (either on laptop or phone):

   * Add device: scan the other device’s QR code.

4. Once devices are paired:

   * On laptop Syncthing UI, share `SovStack-Work` folder with `CLEAN-PHONE`.
   * On phone, accept the folder and choose a location (e.g. `/storage/emulated/0/SovStack-Work`).

Tick:

* [ ] Devices paired in Syncthing
* [ ] `SovStack-Work` syncing between laptop and phone

**RULE:**

* `SovStack-Work` is synced between CLEAN devices.
* `restic` backups still run only from CLEAN LAPTOP.

---

# 9. L4 Weekly & Monthly Checklists (Full)

## Weekly (10–15 minutes)

On CLEAN LAPTOP:

* [ ] Save any new important files into `SovStack-Work`
* [ ] Plug in BACKUP_A
* [ ] Run: `~/backup_to_BACKUP_A.sh`
* [ ] Confirm “Backup completed” message
* [ ] If using Syncthing: check that `SovStack-Work` is in sync (Syncthing UI shows “Up to Date”)

On CLEAN PHONE (if Syncthing):

* [ ] Open Syncthing app, confirm no errors

---

## Monthly (20–30 minutes)

* [ ] Plug in BACKUP_A and BACKUP_B (one after the other)

* [ ] Run `~/backup_to_BACKUP_A.sh`

* [ ] Run `~/backup_to_BACKUP_B.sh`

* [ ] Do a small **test restore**:

  ```bash
  export RESTIC_PASSWORD_FILE="$HOME/Secrets/restic-password.txt"
  export RESTIC_REPOSITORY="/media/$USER/BACKUP_A/restic-repo"   # or /run/media/...
  restic restore latest --target "$HOME/SovStack-Restore-Test"
  ```

* [ ] Check a file restored correctly

* [ ] If using age: try decrypting `Ultra-Secret.tar.age` into `SovStack-Restore-Test` again, just to confirm

* [ ] Check BACKUP_A and BACKUP_B are still stored in their intended places

---

# 10. Emergency Branches (L4)

### Case 1 – CLEAN LAPTOP dies / stolen

* Files inside `SovStack-Work` are **gone from that device**, but:

  1. Get a new CLEAN LAPTOP (run L1 again).

  2. Install `restic`.

  3. Plug in BACKUP_A (or BACKUP_B).

  4. In Terminal:

     ```bash
     sudo apt install restic
     nano ~/restic-password.txt      # or copy it from old Secrets backup, or use KeePass
     ```

     (If you still have `restic-password.txt` backed up elsewhere or recorded; if not, see below.)

  5. Set env vars and restore:

     ```bash
     export RESTIC_PASSWORD_FILE="$HOME/Secrets/restic-password.txt"
     export RESTIC_REPOSITORY="/media/$USER/BACKUP_A/restic-repo"
     restic restore latest --target "$HOME"
     ```

* If you **lost both** the restic password **and** all devices with `restic-password.txt` **and** all copies in KeePass: backup is unrecoverable. That’s by design.

---

### Case 2 – BACKUP_A fails, but BACKUP_B survives

* Replace BACKUP_A with a new drive.
* Re-do 8.1 steps for the new BACKUP_A.
* BACKUP_B still has your old snapshots; you can restore from it.

---

### Case 3 – You accidentally delete something from `SovStack-Work`

* Don’t panic.

* Plug BACKUP_A.

* Restore from an older snapshot:

  ```bash
  export RESTIC_PASSWORD_FILE="$HOME/Secrets/restic-password.txt"
  export RESTIC_REPOSITORY="/media/$USER/BACKUP_A/restic-repo"
  restic snapshots                       # pick a snapshot from before deletion
  restic restore <SNAPSHOT-ID> --target "$HOME/SovStack-Restore-Test"
  ```

* Copy the needed file from `SovStack-Restore-Test` back into `SovStack-Work`.

---

# 11. Final Micro-Checklist (Caveman Version)

To confirm **L4 File Spine** is in place:

1. [ ] All important files live in **one place**: `SovStack-Work` on CLEAN LAPTOP.
2. [ ] `restic` is installed and `backup_to_BACKUP_A.sh` works.
3. [ ] You have run **at least one successful restore test** from BACKUP_A.
4. [ ] BACKUP_A is plugged in weekly, script run, and then unplugged.
5. [ ] (ADVANCED) BACKUP_B exists, lives in a different location, and has a working backup.
6. [ ] (ADVANCED) `age.key` exists, `Ultra-Secret.tar.age` exists, and you have decrypted it once successfully.
7. [ ] (Optional ADVANCED) Syncthing syncs `SovStack-Work` between CLEAN LAPTOP and another CLEAN device.

If all 7 boxes are true (or at least 1–4 for BASIC), your **L4 Storage & Files layer** is live: files go in a single WORK FOLDER, get encrypted, get backed up, and can be restored on demand.
