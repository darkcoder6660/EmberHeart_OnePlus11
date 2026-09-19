# Loading Drivers for External Chipsets
---
### Starting from commit [091ed19](https://github.com/nullptr-t-oss/Dragonw1nd-Kernels/commit/091ed1948e7b8b74577f409560aaf5944cb014ef), CI can compile bootable dlkm and vendor_boot partitions where users can choose what modules to include or load automatically!

> [!IMPORTANT]
> - Need to use stock module dump for closed sourced modules
> - Need to disable avb in vendor_boot fstab to make the custom partitions bootable
> - Extract relevant props from stock partitions using avbtool and export relevant variables in build config

---

> [!IMPORTANT]
> ## Loading custom mac80211
>
> The mac80211 module provided by OnePlus lacks `__ieee80211_create_tpt_led_trigger` symbol, hence rtw88 , ath9k or any other mac80211 compliant drivers with led support won't load. To fix it, unload the default mac80211 and load the custom one.
>
> - Step 0: cd into the directory where all kernel modules are unzipped
> - Step 1: `rmmod mac80211`
> - Step 2: `insmod mac80211.ko`

> [!TIP]
> ## Loading rtw88 drivers
>
> If you have unzipped all the drivers in internal storage and want to load drivers for let's say rtl8821au chipset,
>
> - Step 0: cd into the directory where all kernel modules are unzipped
> - Step 1: `insmod rtw_core.ko`
> - Step 2: `insmod rtw_usb.ko`
> - Step 3: `insmod rtw_88xxa.ko`
> - Step 4: `insmod rtw_8821a.ko`
> - Step 5: `insmod rtw_8821au.ko`

> [!IMPORTANT]
> Make sure you've loaded the custom mac80211 module otherwise you'll get unknown symbol error `(__ieee80211_create_tpt_led_trigger)`

Tested wifi adaptors : [TP-Link Archer T2U Plus](https://amzn.in/d/76Ka5nB)

----

> [!TIP]
> ## Loading ath9k drivers
>
> If you have unzipped all the drivers in internal storage and want to load drivers for let's say Atheros AR9271 chipset,
>
> - Step 0: cd into the directory where all kernel modules are unzipped
> - Step 1: `insmod ath.ko`
> - Step 2: `insmod ath9k_hw.ko`
> - Step 3: `insmod ath9k_common.ko`
> - Step 4: `insmod ath9k.ko`
> - Step 5: `insmod ath9k_htc.ko`

> [!IMPORTANT]
> Make sure you've loaded the custom mac80211 module otherwise you'll get unknown symbol error `(__ieee80211_create_tpt_led_trigger)`
