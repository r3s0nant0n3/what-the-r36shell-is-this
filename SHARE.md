# Share Note: ROCKNIX EE-Clone Shell Tools

These two scripts were built for RK3326 EE/EmuELEC clone handhelds where:

- live ROCKNIX boots from TF1 on `mmcblk1`
- internal vendor firmware lives on eMMC `mmcblk0`
- display and audio need to be debugged as separate DTB problems

## Files

- Desktop research shell:
  `/Users/malory/Downloads/Handheld-Clone-Research/tools/rocknix-shell`
- Handheld-side shell:
  `/Users/malory/Downloads/Handheld-Clone-Research/tools/rocknix-device-shell`

## What Each One Does

`rocknix-shell` runs on the Mac. It compares local DTBs, decompiles to DTS, ranks candidates against the extracted vendor DTB, and can SSH into the handheld for read-only inspection.

`rocknix-device-shell` runs on the handheld itself. It gives a simple prompt for storage, ROM paths, eMMC, DTB discovery, audio logs, and boot info.

## Fast Start

On the Mac:

```bash
cd /Users/malory/Downloads/Handheld-Clone-Research/tools
./rocknix-shell
```

Useful commands:

```text
top 10
summary vendor
summary eeclone
diff vendor eeclone
probe
quit
```

On the handheld over SSH:

```bash
ssh root@10.0.0.84
/storage/tools/rocknix-device-shell
```

Useful commands:

```text
info
roms
emmc
dtbs
audio
boot
quit
```

## Installed Paths On This Handheld

- `/storage/tools/rocknix-device-shell`
- `/storage/roms/tools/rocknix-device-shell`

## Why This Exists

The normal R36S assumptions do not fit this class of clone. The internal vendor DTB and the live ROCKNIX eeclone DTB diverge in important ways, especially the audio card model and GPIO wiring. These scripts are meant to make that comparison repeatable instead of relying on scattered one-off shell commands.
