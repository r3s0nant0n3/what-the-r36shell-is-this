# Install

## Desktop Tool

The desktop-side shell is meant to run on the Mac where the research artifacts live.

```bash
chmod +x rocknix-shell
./rocknix-shell
```

If your paths differ from the original research machine, override them with environment variables:

```bash
export ROCKNIX_HOST=10.0.0.84
export ROCKNIX_VENDOR_DTB=/path/to/vendor.dtb
export ROCKNIX_EECLONE_DTB=/path/to/eeclone.dtb
./rocknix-shell
```

## Handheld Tool

Copy `rocknix-device-shell` to the device:

```bash
scp rocknix-device-shell root@10.0.0.84:/storage/tools/rocknix-device-shell
ssh root@10.0.0.84 'chmod +x /storage/tools/rocknix-device-shell'
```

Optional second copy inside ROM storage:

```bash
ssh root@10.0.0.84 'mkdir -p /storage/roms/tools'
scp rocknix-device-shell root@10.0.0.84:/storage/roms/tools/rocknix-device-shell
ssh root@10.0.0.84 'chmod +x /storage/roms/tools/rocknix-device-shell'
```

Run it:

```bash
ssh root@10.0.0.84
/storage/tools/rocknix-device-shell
```

## Useful Handheld Commands

```text
doctor
bt-doctor
wifi
bluetooth
keyboard
screenshot-status
snapshot
bundle
```

## Notes

- `snapshot` writes reports under `/storage/tools/reports/`
- screenshots use ROCKNIX's native `/usr/bin/rocknix-screenshot` path when available
- on clone hardware, UI toggles alone are not proof that Wi-Fi or Bluetooth actually came up
