# ROCKNIX Clone Shell Toolkit
# what-the-r36shell-is-this edition

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
