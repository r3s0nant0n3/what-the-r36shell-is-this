# ROCKNIX Shell

`rocknix-shell` is a small terminal helper for the RK3326 EE/EmuELEC clone research files under this tree. It is aimed at DTB/DTS comparison and safe read-only SSH probing, not EmulationStation theming.

## Location

- Tool: `/Users/malory/Downloads/Handheld-Clone-Research/tools/rocknix-shell`
- Device tool: `/Users/malory/Downloads/Handheld-Clone-Research/tools/rocknix-device-shell`
- Cache: `/Users/malory/Downloads/Handheld-Clone-Research/.cache/rocknix-shell`

## What It Knows By Default

- Internal vendor DTB:
  `/Users/malory/Downloads/Handheld-Clone-Research/DTB-Working/rk3326-evb-lp3-v12-linux.dtb`
- ROCKNIX eeclone DTB:
  `/Users/malory/Desktop/purple ee clone?/rk3326-gameconsole-eeclone.dtb`
- Likely clone DTBs:
  `/Users/malory/Desktop/desktop/dtb/clone`
- Baseline R36S DTBs:
  `/Users/malory/Desktop/desktop/dtb/r36s`
- SSH target:
  `root@10.0.0.84`

Override those with environment variables if the layout changes:

```bash
export ROCKNIX_HOST=10.0.0.99
export ROCKNIX_VENDOR_DTB=/some/other/vendor.dtb
```

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
