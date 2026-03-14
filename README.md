# what-the-r36shell-is-this
RK3326 EE/EmuELEC clone debugging shell tools for ROCKNIX handhelds. Provides DTB/DTS comparison, candidate ranking, and safe SSH inspection from desktop, plus a device-side shell for storage, ROM paths, audio logs, eMMC visibility, and boot diagnostics on stubborn R36S-style clones. 
-------------
# ROCKNIX Clone Shell Toolkit

Terminal tooling for RK3326 EE/EmuELEC clone handhelds running ROCKNIX.

This toolkit exists for clone devices where normal R36S assumptions break down:

- live ROCKNIX boots from TF1 on `mmcblk1`
- internal vendor firmware lives on eMMC `mmcblk0`
- display and audio are separate DTB problems
- UI toggles can be misleading without shell-level verification

## Included

- `rocknix-shell`
  Desktop-side research shell for DTB/DTS ranking, diffing, summaries, and SSH-assisted inspection.
- `rocknix-device-shell`
  Handheld-side shell for storage, ROM paths, eMMC, DTBs, audio, Wi-Fi, Bluetooth, keyboard, screenshot, report, snapshot, and bundle workflows.
- `LICENSE`
  MIT license.
- `README.md`
  This overview.
- `INSTALL.md`
  Install and usage steps.
- `CREDITS.md`
  Attribution.

## Fast Start

On the Mac:

```bash
cd ROCKNIX-Clone-Shell-Toolkit
chmod +x rocknix-shell
./rocknix-shell
```

On the handheld:

```bash
ssh root@10.0.0.84
/storage/tools/rocknix-device-shell
```

## Best Commands

Mac:

```text
top 10
summary vendor
summary eeclone
diff vendor eeclone
probe
```

Handheld:

```text
doctor
bt-doctor
snapshot
bundle
```

## Why It Matters

This toolkit answers the question the UI often cannot:

- did the toggle really do anything?
- did the radio actually enumerate?
- did the system really boot from the expected media?
- did the screenshot/report get captured?
- which DTBs are closest to the vendor internal firmware?

That makes it useful both for local debugging and for helping other owners of similar clones.
## Commands

```bash
./rocknix-shell
./rocknix-shell shell
./rocknix-shell inventory
./rocknix-shell summary "/path/to/file.dtb"
./rocknix-shell diff "/path/left.dtb" "/path/right.dtb"
./rocknix-shell rank | head
./rocknix-shell probe
./rocknix-shell ssh
./rocknix-shell next
```

## Workflow

Use `rank` first. It scores candidate DTBs against the internal vendor DTB using the audio card model, headphone detection line, speaker control line, panel hint, and rough DTS similarity. That gives a short list for manual review.

Use `summary` and `diff` on the top-ranked candidates. For this handheld, display and audio need to be treated as separate axes. A Panel 8 candidate can be visually promising while still missing vendor-style audio wiring.

Use `probe` only for read-only checks on the live ROCKNIX boot. It gathers `lsblk`, `blkid`, mounts, and visible DTB paths over SSH.

## Device-Side Tool

`rocknix-device-shell` is meant to be copied onto the handheld itself. It is a small `sh` script for the live ROCKNIX environment and focuses on:

- storage and ROM path inspection
- eMMC partition visibility
- DTB path discovery
- audio and boot log checks

Example once copied to the device:

```sh
/storage/tools/rocknix-device-shell
/storage/tools/rocknix-device-shell emmc
/storage/tools/rocknix-device-shell audio
```

## Interactive Mode

Run `./rocknix-shell` with no arguments to enter the prompt. Inside it you can use:

```text
inventory
top 10
summary vendor
summary eeclone
diff vendor eeclone
probe
ssh
quit
```

`vendor` and `eeclone` are built-in references, so you do not have to keep typing full paths during DTB work.
