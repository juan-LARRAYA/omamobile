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
- Kernel and device tree (checked 2026-11-25): upstream mainline does NOT have
  SM6225 or `spes` (only `sm6115*` and `sm4250*`), and neither does
  `derekross/linux-omamobile` (`omamobile` branch, v7.3-rc6 base). The only
  mainline-based tree that boots this phone is the community
  `GuidixX/kernel_xiaomi_sm6225-mainline` (branch `master`, Linux 7.4-rc3,
  DTBs `qcom/sm6225-xiaomi-spes-sm5602` and `qcom/sm6225-xiaomi-spesn`),
  packaged in postmarketOS as `linux-postmarketos-qcom-sm6225` (device
  `xiaomi-spes`: fastboot, boot header v3, 4096 page size, dtbo partition,
  `super` partition, USB 05c6:9039, DTB picked by `qcom,board-id`).
  Next: diff that tree against mainline to list the SM6225 additions, then
  carry them onto the Omamobile kernel one commit per change.
