# MX4200 v1 · OpenWrt + ath11k RX ring fix (+ mesh packages)

Builds official OpenWrt (same release config as downloads.openwrt.org) for the
**Linksys MX4200 v1** with one code change: a patch that halves five ath11k RX/monitor
ring sizes so the Wi-Fi driver stops exhausting the ~372 MB of RAM and hanging
the router ([openwrt/openwrt#24154](https://github.com/openwrt/openwrt/issues/24154)).

Included packages: LuCI, zram-swap, luci-app-watchcat, full `wpad-mbedtls`
(802.11s mesh + 802.11r fast roaming), batman-adv + batctl, usteer (+ LuCI apps).

Patch credit: [enspect/ath11k-ipq807x-rx-buffer-oom-fix](https://github.com/enspect/ath11k-ipq807x-rx-buffer-oom-fix),
with the correction from the issue thread (refill buffer size kept at 2048), as in
[HuyNQBGG/openwrt-mx4200-ath11k-test](https://github.com/HuyNQBGG/openwrt-mx4200-ath11k-test). GPL-2.0.

## Build
Actions → **Build MX4200 v1** → Run workflow → enter the OpenWrt version.
The images and ath11k packages appear under **Releases** (~3 h on GitHub's free runners).

## Flash
- **From OpenWrt:** System → Backup / Flash Firmware → Flash image → `*-sysupgrade.bin` → keep settings.
- **From Linksys stock firmware:** `https://<router-ip>/fwupdate.html` → upload `*-factory.bin`.

Watch `grep MemAvailable /proc/meminfo` — it should level off well above 100 MB under load.

Not an official OpenWrt build.
