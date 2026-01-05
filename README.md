# refind-theme

This folder contains a rEFInd boot manager theme. The files here (for example `theme.conf`, `icons/`, and `wallpaper/`) should be copied into your rEFInd installation's `themes` directory and enabled from your `refind.conf`.

Installation (UEFI)

1. Mount your EFI System Partition (ESP). On many distributions the ESP is `/boot/efi`;
	if not mounted, identify it (usually a FAT32 partition with the `EFI` directory) and mount it. Example:

	```bash
	sudo mkdir -p /mnt/esp
	sudo mount /dev/sdXY /mnt/esp    # replace /dev/sdXY with your EFI partition
	```

2. Copy this theme folder into rEFInd's `themes` directory. Common rEFInd install locations:

	- `/boot/efi/EFI/refind/themes/`
	- `/EFI/refind/themes/` (on some systems)

	Example copy command (from this repository root):

	```bash
	sudo cp -r refind-theme /mnt/esp/EFI/refind/themes/
	sudo chown -R root:root /mnt/esp/EFI/refind/themes/refind-theme
	sudo chmod -R a+r /mnt/esp/EFI/refind/themes/refind-theme
	```

3. Enable the theme in `refind.conf`.

	- Open your `refind.conf` (usually `/boot/efi/EFI/refind/refind.conf` or the same directory where rEFInd is installed).
	- Add or edit a line to include the theme's `theme.conf`. For example:

	  ```text
	  include themes/refind-theme/theme.conf
	  ```

	- Alternatively, you can set theme-specific options directly in `refind.conf` or use a relative path to the theme file if your layout differs.

4. Unmount the ESP if you mounted it:

	```bash
	sudo umount /mnt/esp
	```

Notes and tips

- If rEFInd was installed in a different location (for example via your distro's package manager), adjust the paths above accordingly.
- If the theme doesn't appear, ensure `refind.conf` is being read by rEFInd (check the file location and permissions).
- If Secure Boot is enabled, rEFInd must be signed or shim must be used for rEFInd to load; copying themes does not affect signing.

Customization

- Change the wallpaper by replacing the image in the `wallpaper/` folder and updating `theme.conf` if the filename changed.
- Icons live in `icons/`; you can swap or add icons but keep names referenced in `theme.conf`.
- Fonts and sizes can be adjusted inside `theme.conf`.

Troubleshooting

- Permission issues: ensure the files on the ESP are world-readable by the firmware (use `chmod a+r`).
- Wrong path: verify the `include` line points to the correct relative path from the rEFInd directory.
- Not loading after reboot: double-check you copied into the active EFI partition and that the system boots the same rEFInd installation you modified.

Where to copy this folder (summary)

- Copy the entire `refind-theme` directory into `EFI/refind/themes/` on your EFI System Partition (ESP).

Example quick install (one-liner, adjust device and paths):

```bash
sudo mount /dev/sdXY /mnt/esp && sudo cp -r refind-theme /mnt/esp/EFI/refind/themes/ && sudo umount /mnt/esp
```

If you'd like, I can also:

- update this README with screenshots or a sample `refind.conf` snippet tailored to your distro,
- or create a small install script to automate the copy and permission steps.

