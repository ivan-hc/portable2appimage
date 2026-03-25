# portable2appimage
Convert standalone portable apps to AppImages.

An experimental helper based on https://github.com/ivan-hc/AppImage-tips that allows you to convert a standalone portable app to an AppImage.

NOTE, This tool is necessary for simple programs that already run independently and without the need for external libraries. To build more complex AppImage packages, see [Anylinux](https://github.com/pkgforge-dev/Anylinux-AppImages) or [Archimage](https://github.com/ivan-hc/ArchImage).

---------------------------------

## Usage
Is recommended to quote the argument if it contain spaces. This command must run against a file.

Where FILE is the file name (it may be an executable or a 7z/tar/zip/deb package), if the file is an executable, just run the following command:
```
portable2appimage "FILE"
```

Where APP is the name of the executable and FILE is a 7z/tar/zip/deb archive that contains it, run the following command:
```
portable2appimage "FILE" "APP"
```

Optionally you can set a VERSION manually. Run the following command:
```
portable2appimage "FILE" "APP" "VERSION"
```

## EXAMPLE

https://github.com/user-attachments/assets/a4006936-86b4-4aa5-ac1c-e3e10a5d8773

## Tips
Add a icon and a .desktop file near the script to use them in the root of the AppDir.

In case no .desktop file and no icon is found, the script will create dumb ones.
