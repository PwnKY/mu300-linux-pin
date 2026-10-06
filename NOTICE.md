# NOTICE — mirror of `dikeckaan/mu300-linux`

This repository is a **verbatim mirror** of the tracked files of

    https://github.com/dikeckaan/mu300-linux
    commit 35a1c5503303bf47870ecc79c4bd0ae892495c84
    "fix(tf): harden installer, slot boot and dashboard settings" (2026-10-05)

It exists so that a build stays reproducible if that commit becomes unreachable:
upstream deleted the branch (`clean-tf-7.2`) that pointed at it, so the commit is
no longer reachable from any ref, and a host may eventually collect it.

Nothing here is authored by the mirror's owner, and no authorship is claimed.
All credit belongs to the upstream author. The upstream `LICENSE` is kept
unchanged.

## What is in here

The complete tracked tree at that commit, byte for byte, with two exceptions:

1. **`stock/` was removed.** It contained `trustos-F50_FLYMODEM_ZYV1.0.0B09.img`,
   the stock TEE image. The upstream README states that stock firmware, Android
   vendor components and bootloaders "belong to their owners and are not
   distributed here", with that image as the single exception and "all rights to
   it remain with ZTE/Unisoc". It is not an input to the build, so it is not
   mirrored.
2. **This `NOTICE.md` was added.**

No other file was modified.

## Licences (as stated in the upstream README)

| content | licence |
|---|---|
| Kernel source: ZTE's GPL release for the U30 Air (mirrored by Enceka) and the Unisoc drivers in it | GPL-2.0 |
| Wi-Fi, Bluetooth and GPU drivers: realme C51/C53 AndroidT kernel release; the patches in `kernel/patches` | GPL-2.0 |
| Scripts, tools and documentation | MIT (see `LICENSE`) |

Both licences permit copying and redistribution as long as the notices and
licences are kept — which this mirror does — and GPL-2.0 additionally requires
that the source is made available, which is what this repository is.

## How it is used

`PwnKY/f50-immortalwrt-ci` builds the firmware from this mirror, pinned to the
commit recorded in its `inputs/pins.json`. The build applies
`scripts/local-adaptations.patch` on top (three changes: a parallelism cap, the
customization mount and hook in the rootfs assembler, and a build-time IPv4
download wrapper); that patch is the build harness's own work, not upstream's.

To move to a newer upstream state: pick the commit, refresh this mirror, update
the pin, and check that the LED work
(`openwrt/overlay/www/luci-static/resources/view/system/leds.js`) is still
present — it exists only on the deleted branch, so any upstream state that lacks
it would drop the LED fix this firmware depends on.
