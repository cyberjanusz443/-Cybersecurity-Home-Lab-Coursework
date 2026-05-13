# 12 — Backups with rsync (Cross-OS via WSL)

Practical implementation of cross-platform backup strategy using `rsync`,
with **WSL2** (Windows Subsystem for Linux) as the bridge between
Windows source data and Linux backup logic.

## What I did

### Junior tier — WSL setup and cross-OS connectivity
- Installed WSL2 with Ubuntu distribution on Windows host
- Verified that WSL mounts Windows drives under `/mnt/c/`, allowing
  Linux tools to read/write Windows filesystem natively
- Tested bidirectional file transfer between Windows and Linux contexts
- Created the destination folder structure for backups in the Linux side

### Medium tier — rsync mirroring with --delete
- Implemented mirror sync from `/mnt/c/Kopia_Zapasowa/` (Windows source)
  to `~/backupy/windows_data/` (Linux destination):
  ```bash
  rsync -avz --delete /mnt/c/Kopia_Zapasowa/ ~/backupy/windows_data/
  ```
- The `--delete` flag ensures the destination is a **true mirror** — files
  removed from source are also removed from backup (no orphaned old files)
- Tested incremental sync: created `plik4.txt`, ran rsync (only the new file
  transferred), then deleted `plik.txt.txt` on source and re-ran rsync
  (sync deleted the file from backup)
- Used `-a` (archive mode: preserves permissions, timestamps, ownership)
  + `-v` (verbose) + `-z` (compression in transit, useful for slow links)

## Key screenshots
- `junior_Pobranie_WSL.jpg` — WSL installation and Ubuntu setup
- `junior_Sprawdzenie_Lacznosci_Z_Linux.jpg` — Connectivity test between
  Windows and WSL Linux environment
- `junior_Utworzenie_Kopi_Zapasowaej_Dysk_C.jpg` — Initial backup of Windows
  drive contents to WSL
- `medium_Mirroring.jpg` — `rsync -avz --delete` in action with
  incremental transfer stats and deletion notification

## Takeaway
**The 3-2-1 backup rule** is industry standard:
- **3 copies** of important data
- **2 different media types** (e.g., internal SSD + external drive)
- **1 offsite copy** (cloud, remote location)

`rsync --delete` gives you the local mirror part of this strategy.
For offsite, the same tool can sync over SSH to a remote server:
```bash
rsync -avz -e ssh /source/ user@remote:/backup/
```

**Anti-pattern to avoid:** "Backup" that synchronizes ransomware-encrypted
files to the backup destination. Always pair `rsync` with **immutable
snapshots** (ZFS, Btrfs, S3 Object Lock) so that yesterday's clean version
is preserved even if today's source data is compromised.

This is how I'd architect a production backup strategy for a small business.
