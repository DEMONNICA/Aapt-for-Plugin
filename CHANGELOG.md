> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [4.5.0]
>
> - Added author verification to `verify_module_id` in `verify.sh`.
> - Added `me.yuki.aster:Aster` and `me.yuki.folksu:FolkSU` to APatch detection in `detect_root_all`.
> - Added `sudo` binary for all supported architectures, installed in module mode and Axeron plugin root mode only.
> - Added unsupported architecture check in `customize.sh` — installation now aborts instead of continuing without binaries.
> - Changed KSU spoofed fallback case in `customize.sh` — simplified to `KernelSU-Next Spoofed`, `Wild KSU Spoofed`, and generic `KernelSU Spoofed`. Removed VortexSU and ReSukiSU specific cases.
> - Changed `device_info` RAM label logic in `customize.sh` — replaced long `if/elif` chain with reusable `ram_label()` function.
> - Changed `device_info` SDK validation in `customize.sh` — added check for empty or non-numeric SDK value before minimum version check.
> - Changed ReSukiSU detection in `detect_root_all` to `BakaSU` — name is read from the APK (`ReSukiSU`/`BakaSU`), and `BakaSU` is added to the spoofed `aapt` check.
> - Changed `aapt` to `v0.2-android-16.0.0_r4` and `aapt2` to `2.20-android-16.0.0_r4`.
> - Fixed installation failure on Magisk Kitsune — `update-binary` now follows the official Magisk module template (sets `OUTFD` and `ZIPFILE` from installer arguments, handles empty `MAGISK_VER_CODE`).
> - Removed `com.vortexsu.vortexsu:VortexSU` from KernelSU detection and `moe.bemly.kokoro:Kokoro Mask` from Magisk detection in `detect_root_all`.
> - Removed fallback `AAPT_VER` and hardcoded `35.0.2` version in `service.sh`.
---

> [4.2.0]
>
> - Added extraction of `update-binary` in `verify.sh`.
> - Changed `module_remove_check` in `customize.sh` — plugin removal moved to a separate section.
> - Changed `PREFIX` separator in `service.sh` from `•` to `|` for both plugin and module mode.
> - Changed sed separator in `service.sh` from `|` to `@` to avoid conflict with description content.
> - Changed `set_donate_link` in `customize.sh` — removed `else` fallback since `banner=` is always present in `module.prop`.
> - Changed `axeronPlugin` update logic in `customize.sh` — checks if field exists before updating, appends if missing.
> - Changed hash priority in `verify.sh` — now checks `md5 sha512 sha384 sha256 sha224 sha1`.
> - Removed `.method` file deletion from `uninstall.sh` module mode.
> - Removed `axeronPlugin` from module mode `module.prop` in `service.sh` and `customize.sh`.
> - Removed `detect_plugin_combination` from `customize.sh` — KANG and SEKOIIRE detection removed.
---

> [4.0.0]
>
> - Added `${USER}` to Axeron detection output in `detect_root_all`.
> - Added back `axeronPlugin` update in `customize.sh` for plugin mode.
> - Changed detection order in `detect_root_all` to alphabetical — Axeron → APatch → KernelSU → Magisk.
> - Changed `for entry` lists in `detect_root_all` sorted alphabetically by label.
> - Changed root method reading order in `service.sh` to APatch → KSU → Magisk.
> - Changed APatch `.method` from 4 lines to 5 lines — added `APATCH_VER` (KernelPatch codename) as line 2.
> - Changed `curl` for `APATCH_KERNEL_VER_CODE` to use `--insecure` flag.
> - Changed `APATCH_KERNEL_VER_CODE` fallback from `?` to last known value from `.method` line 5.
> - Changed `service.sh` APatch block to always read from `.method` directly, removed `if [ -z ]` guard.
> - Changed `VER_KERNEL` to `APATCH_KERNEL_VER_CODE` in `service.sh` for consistency.
> - Changed `uninstall.sh` fstrim moved inside each mode block — module and plugin.
> - Changed `.method` deletion order in `uninstall.sh` to APatch → KSU → Magisk.
> - Fixed `io.github.huskydg.magisk` label incorrectly set to `Kitsune Mask`, corrected to `Magisk Kitsune`.
> - Fixed `VER_KERNEL` in `service.sh` APatch block placed outside `if` block.
> - Removed `USER_DETECT` variable from `service.sh` — unused.
---

> [3.5.0]
>
> - Added hybrid plugin/module mode support across `customize.sh`, `service.sh`, and `uninstall.sh`.
> - Added `module_remove_check()` in `customize.sh` — handles removal from `modules_update`, `modules`, and `plugins` at once.
> - Added `detect_root_all()` in `customize.sh` for KSU, Magisk, APatch, and Axeron detection via `pm list packages`, including spoofed KSU variant detection via `ksud` output.
> - Added strings-based detection for `frb.axeron.manager` in `detect_root_all` to distinguish AxManager from Folkpure.
> - Added `set_donate_link()` in `customize.sh` for module mode only.
> - Added `aapt_install()` in `customize.sh` to copy binaries to `$AXERONBIN` and rename by ABI.
> - Added `INSTALL_PATH` variable in `customize.sh` for hybrid path handling.
> - Added plugin combination detection in `customize.sh` for plugin mode only.
> - Added `dev.axora.manager` to Axeron package detection.
> - Added `MODDIR` and `MODPROP` definitions in `service.sh`.
> - Added root method reading from KSU, Magisk, and APatch `.method` files in `service.sh` for module mode.
> - Added ABI detection in `service.sh` for `name=Aapt for $ABI` update.
> - Added `name`, `description`, and `version` update for module mode via `MODPROP` in `service.sh`.
> - Added `MODDIR` definition in `uninstall.sh`.
> - Added hybrid if/else in `uninstall.sh` — module mode and plugin mode separated.
> - Added module mode uninstall — removes `.method` files from KSU, Magisk, and APatch directories.
> - Added module mode cache cleanup in `uninstall.sh`.
> - Added module mode fstrim per partition in `uninstall.sh`.
> - Changed `check_axeron_requirement` merged into `detect_root_all` in `customize.sh`.
> - Changed `set_permissions` from manual `chmod` loop to `set_perm_recursive` and `set_perm`.
> - Changed notification check from `IS_ROOTED` to `$USER` — plugin shows "Restart & close", module shows "Reboot your device".
> - Changed `service.sh` module.prop update to hybrid — plugin updates `AXMPROP`, module updates `MODPROP`.
> - Changed `uninstall.sh` to use `$AXERON` directly instead of `IS_AXERON`.
> - Changed uninstall order in `uninstall.sh` — module first, plugin second.
> - Changed `verify_module_id` verified message — plugin shows "Verified Plugin 悪魔", module shows "Verified Module 悪魔".
> - Changed `module.prop` description to be more concise.
> - Changed `verify_module_id` to add `tr -d '\r'` for CRLF compatibility.
> - Changed module mode binary extraction from `system/bin/$ARCH_FILE` to `system/bin/aapt-$ABI` and `system/bin/aapt2-$ABI`.
> - Removed `abort_verify` from `customize.sh` — moved to `verify.sh`.
> - Removed `get_app_label` from `customize.sh` — now inline in `detect_root_all`.
> - Removed `IS_ROOTED` variable.
> - Removed hash cleanup from `customize.sh` — handled by `verify.sh`.
> - Removed `axeronPlugin` and `description` update from `customize.sh` — moved to `service.sh`.
> - Removed banner addition from `customize.sh` — already defined directly in `module.prop`.
> - Removed `ARCH_FILE` mapping from `customize.sh` — artifact from ADH sqlite3 module.
> - Removed `$AXERONDIR/.method` from plugin uninstall targets — shared resource.
> - Removed `sync` from plugin mode in `uninstall.sh`.
---

> [2.2.0]
>
> - Changed `banner=` in `module.prop` from local asset path to remote GitHub URL.
> - Changed notification in `service.sh` to toast using `AxManager.TOAST`, displaying aapt version only.
> - Removed `assets/AAPT.jpg` from ZIP extraction in `customize.sh`.
---

> [2.0.0]
>
> - Changed plugin banner — replaced old banner with a new design.
> - Changed hardcoded `AAPT` reference in `customize.sh` and `uninstall.sh` to use `$ID` variable.
> - Changed `get_app_label` to use `strings` directly instead of `$AAPT_BIN` variable.
> - Changed `$AXERONBIN/fstrim` to `fstrim` directly in `uninstall.sh`.
> - Changed `customize.sh` with detailed sub-comments across all functions.
> - Changed `service.sh` comment style for consistency with other plugins.
> - Changed `uninstall.sh` with proper path definitions and consistent comment style.
---

> [1.5.0]
>
> - Changed `customize.sh` indentation and code structure.
> - Changed `device_info` with `device_capitalized` declared in local.
> - Changed `service.sh` with proper root/non-root detection and notification handling.
> - Changed `uninstall.sh` with proper storage trim via FSTRIM and sm.
> - Fixed `aapt` and `aapt2` permission not set correctly after copy to `$AXERONBIN`.
> - Fixed binary extraction path from `system/bin/$ABI/` to `system/bin/aapt-$ABI`.
> - Fixed removal of `$AXERONBIN/aapt` and `$AXERONBIN/aapt2` on uninstall.
> - Fixed `banner=` duplicate newline in `module.prop`.
> - Fixed `find` bracket bug for sha/md5 cleanup.
> - Fixed notification for `shell/non-root` users.
> - Removed cache directory cleanup from `uninstall.sh`.
---

> [1.0.0]
>
> - Initial release.
---