> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [1.5.0]
>
> - Fixed `aapt` and `aapt2` permission not set correctly after copy to `$AXERONBIN`.
> - Fixed binary extraction path from `system/bin/$ABI/` to `system/bin/aapt-$ABI`.
> - Fixed removal of `$AXERONBIN/aapt` and `$AXERONBIN/aapt2` on uninstall.
> - Fixed `banner=` duplicate newline in `module.prop`.
> - Fixed `find` bracket bug for sha/md5 cleanup.
> - Fixed notification for `shell/non-root` users.
> - Improved `customize.sh` indentation and code structure.
> - Improved `device_info` with `device_capitalized` declared in local.
> - Improved `service.sh` with proper root/non-root detection and notification handling.
> - Improved `uninstall.sh` with proper storage trim via FSTRIM and sm.
> - Removed cache directory cleanup from `uninstall.sh`.
> - Misc improvements and fixes.
---

> [1.0.0]
>
> - Initial release.
---