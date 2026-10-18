# MX4200 v1 · OpenWrt + ath11k RX ring fix

Builds official OpenWrt (same release config as downloads.openwrt.org) for the
**Linksys MX4200 v1** with one change: a patch that halves five ath11k RX/monitor
ring sizes so the Wi-Fi driver stops exhausting the ~372 MB of RAM and hanging
the router ([openwrt/openwrt#24154](https://github.com/openwrt/openwrt/issues/24154)).

Patch credit: [enspect/ath11k-ipq807x-rx-buffer-oom-fix](https://github.com/enspect/ath11k-ipq807x-rx-buffer-oom-fix),
with the correction from the issue thread (refill buffer size kept at 2048), as in
[HuyNQBGG/openwrt-mx4200-ath11k-test](https://github.com/HuyNQBGG/openwrt-mx4200-ath11k-test). GPL-2.0.

## Build
Actions → **Build MX4200 v1** → Run workflow → enter the OpenWrt version the routers run.
The sysupgrade image and ath11k packages appear under **Releases** (~1.5–3 h).

## Flash
From the router: System → Backup / Flash Firmware → Flash image → choose
`*linksys_mx4200v1-squashfs-sysupgrade.bin` → **keep settings** checked.
Then watch `grep MemAvailable /proc/meminfo` — it should stay well above 100 MB under load.

Not an official OpenWrt build.
