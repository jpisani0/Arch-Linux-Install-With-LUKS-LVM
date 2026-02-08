I have had this issue on a keyboard that when connected in wired mode would only come up as an Apple style keyboard and the Function Keys would only work as multi-media keys (brightness, volume, etc.) and not work as their actual functions, whether or not the `fn` key was held down. First do:

```bash
cat /sys/module/hid_apple/parameters/fnmode
```

If this does not return `2`, then write 2 into it with `nvim` or your text editor of choice. This will only change it for the session. To change it permanently, create the file `/etc/modprobe.d/hid_apple.conf` and write this into it:

```bash
options hid_apple fnmode=2
```

Then, make sure you have the `modconf` HOOK in your `HOOKS-()` line OR that you have `/etc/modprobe.d/hid_apple.conf` in your `FILES=()` line and regenerate your initramfs with `mkinitcpio -P`.

More info at: https://wiki.archlinux.org/title/Apple_Keyboard