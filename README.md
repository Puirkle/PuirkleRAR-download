<p align="center"><picture><source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Puirkle/PuirkleRAR-download/main/logo-dark.png"><img src="https://raw.githubusercontent.com/Puirkle/PuirkleRAR-download/main/logo.png" width="480" alt="PuirkleRAR"></picture></p>

# PuirkleRAR

PuirkleRAR is a free archiver for Windows, like WinRAR or 7-Zip. It packs files into small archives, opens almost any archive you come across, and can protect archives with a password.

**[Download PuirkleRAR](https://github.com/Puirkle/PuirkleRAR-download/releases)**: get `PuirkleRAR-setup.exe` from the newest release.

- **Small archives.** Its own `.prar` format finds repeated data across all your files and stores it once, then compresses the rest by file type. It is usually smaller than WinRAR's Best.
- **Shrinks files other archivers can't.** .jar, .zip, .docx/.xlsx/.pptx, .apk, PNG, PDF and Minecraft world (.mca) files are already compressed inside. PuirkleRAR unpacks their insides before packing and rebuilds each file exactly on extract. Folders full of these come out much smaller: 528 MB of Minecraft mod jars packed to 320 MB instead of 429 MB. At Ultra and Max, Ogg music and sounds are re-coded about 12% smaller, and also rebuilt exactly.
- **Opens almost everything:** .zip, .rar, .7z, .tar, .gz, .xz, .zst, .bz2, .iso, .cab and .prar.
- **Makes:** .prar, .zip, .7z, .tar.gz / .tar.xz / .tar.zst and self-extracting .exe. It makes .rar only if WinRAR is installed.
- **Passwords:** strong encryption, and file names are hidden too.
- **Repair:** add a recovery record, and a damaged archive can be fixed later.

## Install

1. Download `PuirkleRAR-setup.exe` from the [newest release](https://github.com/Puirkle/PuirkleRAR-download/releases).
2. Run it. No admin rights are needed, and it installs for your user only.
3. If Windows shows **"Windows protected your PC"**, click **More info**, then **Run anyway**. The program isn't code-signed (a signing certificate costs money), so Windows warns about it.

PuirkleRAR then appears in the Start menu, in the right-click menu of files and folders, and in **Settings > Apps > Default apps**.

**System requirements:** Windows 10 or 11, 64-bit. Ultra and Max levels on very large inputs need several GB of free memory.

**To update:** download the new setup and run it. It replaces the old version. Your archives aren't touched.

**To uninstall:** **Settings > Apps > Installed apps > PuirkleRAR > Uninstall**, or in PuirkleRAR's **Settings**. File types go back to the programs they had before. Your archives aren't touched.

## Pack files

- **Fastest way:** right-click files or folders, then **PuirkleRAR > Compress to .prar** (or .zip).
- **With options:** right-click, then **PuirkleRAR > Add to archive...**, or click **Add** in PuirkleRAR. You can choose:
  - **Format:** .prar (smallest), .zip (opens everywhere), .7z, .tar.gz, or a self-extracting .exe.
  - **Level:** see below.
  - **Password:** encrypts the archive. A forgotten password can't be recovered.
  - **Split into volumes:** for example 4095 MB parts for a FAT32 USB stick.
  - **Recovery record:** lets you repair the archive later. Use 5% or more for important backups.
  - **Comment:** a note shown when the archive is opened.

### Which level?

| Level | Speed | Size | Use it for |
|---|---|---|---|
| **Fast** | fastest, both ways | about WinRAR Best | videos, photos, music, and anything already compressed |
| **Normal** | faster than WinRAR's default | about 15-20% smaller than WinRAR Best on mixed folders | everyday use (the default) |
| **Best** | about the same as Normal | a little smaller than Normal | backups |
| **Ultra** | slow to pack, quick to extract | smaller still | when size matters more than packing time |
| **Max** | slowest, both ways; uses several GB of memory | smallest | when only size matters |

Measured on a 10.1 GB games folder (26,019 files):

| | Archive | Time to pack | Time to extract |
|---|---|---|---|
| WinRAR Best (solid) | 1,648 MB | 225 s | 38 s |
| PuirkleRAR Fast | 1,615 MB | 10 s | 42 s |
| PuirkleRAR Normal | 1,493 MB | 47 s | 52 s |
| PuirkleRAR Best | 1,483 MB | 54 s | 50 s |
| PuirkleRAR Ultra | 1,379 MB | 279 s | 84 s |
| PuirkleRAR Max | 1,201 MB | 790 s | about 10 min |

From Normal up, files that hold compressed data inside (jars, zips, Office documents, PNG images, PDFs, Minecraft region files) are unpacked before compressing and rebuilt exactly on extract. That is where most of the size comes from, and also why extracting at those levels takes a little longer than at Fast.

**What to expect:** documents, source code, programs and databases shrink a lot. Videos, photos, music, games' packed files and other archives are already compressed, so no program can make them much smaller. Pack those with **Fast**. Very large sets only shrink from GB to MB when they hold lots of repeated data, such as many copies of the same files or backups.

## Extract files

- Right-click an archive, then **PuirkleRAR > Extract here** or **Extract to a new folder**.
- Or double-click the archive to open it in PuirkleRAR, select files, and click **Extract To**. You can also drag files out of the window into Explorer.
- Every extracted file is checked against its checksum, so a damaged archive is reported, never silently extracted wrong.

## While it works

The progress window shows what PuirkleRAR is doing: which file it is reading, how much duplicate data it skipped, and for each kind of file how far compression is, the ratio, the speed and the time left.

- **Background:** lowers PuirkleRAR's priority so your PC stays responsive, and minimizes the window. The percentage shows in the taskbar.
- **Pause / Resume:** stops all work until you continue. Nothing is lost.
- **Mode...:** when everything is done, close PuirkleRAR, put the PC to sleep, or shut it down. Shut down warns you 60 seconds before; run `shutdown /a` to stop it.
- **Cancel:** stops and throws away the unfinished archive. Your files are not touched.

## More tools

- **Test:** checks an archive without extracting it.
- **Repair:** fixes a damaged .prar or .rar that has a recovery record, or rebuilds missing volumes from recovery volumes. The original is kept, and the repaired copy is written next to it.
- **Find:** searches file names, or text inside files, across archives.
- **Convert:** turns an archive into another format, for example .rar to .zip.
- **Lock:** stops further changes to an archive. This can't be undone.
- **Benchmark:** measures how fast your PC packs and unpacks.

## Command line

The installer adds `puirklerar` to your PATH, so it works in any newly opened terminal:

```
puirklerar a backup.prar "D:\Photos" "D:\Projects" -l best -p   # pack; -p asks for a password
puirklerar x backup.prar -o D:\restore                          # extract
puirklerar l backup.prar                                        # list contents
puirklerar a backup.prar "D:\Photos" -v 4095m -r 5              # 4 GB volumes, 5% recovery record
puirklerar --help                                               # everything else
```

## Questions

**Can other people open my .prar files?** Only with PuirkleRAR. To send files to someone without it, use **.zip**, or a **self-extracting .exe**, which unpacks itself with no program needed.

**Can I create .rar files?** Only if WinRAR is installed: PuirkleRAR then uses WinRAR's own `Rar.exe`. The RAR compression format is closed, so no free program can make .rar files on its own. Opening and extracting .rar always works.

**My antivirus or SmartScreen warns about the setup.** It's because the program isn't code-signed. Download it only from this page.

**Is my password stored anywhere?** No. Encrypted .prar archives use XChaCha20-Poly1305 with an Argon2id-derived key, and the password isn't saved. Without it, the data can't be recovered.

**Archives made by a newer version won't open.** Update PuirkleRAR to the latest version. Older versions can't read the newer, smaller archive format.
