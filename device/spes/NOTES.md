<!-- SPDX-License-Identifier: MIT -->
# spes (Xiaomi Redmi Note 11, 2201117TL) — bring-up notes

Facts only, each read off the phone on 2026-11-24 from stock Android with
`adb`/`fastboot`. Captures stay outside the repository (device identifiers).

## Stock facts

- Model `2201117TL`, codename `spes`, product `spes_global`, SoC SM6225
  (Snapdragon 680, platform `bengal`).
- Stock: MIUI 14 `V14.0.3.0.TGCMIXM`, Android 13, kernel 4.19.157, ROM region
  AR, hardware variant SM5602.
- A/B: `slot-count: 2`, active slot `_b`. Storage is UFS (`sdX` LUNs).
- Bootloader locked: `fastboot getvar unlocked` → `no`; `secure boot` on.
- Unlock path: Xiaomi Mi Unlock through `miunlock` (offici5l); blocked until the
  Mi account has a verified phone number (server code 20041).

## Not yet done

- Unlock the bootloader (erases `userdata`).
- Full read-only backup of every partition but `userdata` and `super`,
  checked against checksums, stored outside the repository.
- Add the phone to the entry table in `CONTRIBUTING.md` (boot partition the
  installer may write, fastboot by buttons) before any flash.
- Kernel and device tree: mainline has `sm6225-xiaomi-spes-sm5602` through the
  postmarketOS tree; compare against what `linux-omamobile` needs.
