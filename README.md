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

If you want to made your AppImage updateable using `zsync` and `appimageupdatetool`, you need to set "USER|REPO|TAG", like this:
```
portable2appimage "FILE" "APP" "VERSION" "USER|REPO|TAG"
```
or like this directly (not recommended)
```
portable2appimage "FILE" "APP" "USER|REPO|TAG"
```

NOTE: only github releases are supported for updates.

## EXAMPLE
In this video I will first create an AppImage of freedownloadmanager (binary name `fdm`) using the following command:
```
portable2appimage freedownloadmanager.deb fdm
```
Version is taken from the ELF binary and may be wrong, this is why it is necessary to set it.

On the contrary, an AppImage of portable2appimage has the correct version, since it is on top of the file. In this example I also add "USER|REPO|TAG" for this repository, using this command:
```
portable2appimage portable2appimage portable2appimage "ivan|portable2appimage|latest"
```
This would not work until I don't upload the AppImage and the .zsync files in the "releases" section of this repository.

https://github.com/user-attachments/assets/50c86d37-0c68-4854-b0bf-53be805aa53a

This is an AppImage of Tixati instead. The script will automatically fix .desktop file validation errors:

https://github.com/user-attachments/assets/7fce5906-0517-4186-b874-30af32c2dc34

Finally, this one is ntsc-rs, binary name are two, you can pic just one, in our case `ntsc-rs-standalone`. The files contained in this archive are not set to "executable", the script is able to detect the indicated binary by checking whether it is an ELF file or a script:

https://github.com/user-attachments/assets/69cbce05-a1f1-4963-9c66-2b4b0774787c

And I could go on forever.

As long as your program is already running on its own, exporting it as an AppImage is a breeze.

## Why do it?
An AppImage isn't just an archive format that can run the program without you having to extract it. AppImage can isolate a program's dotfiles using a .config or .home directory with the same name as the AppImage, so you don't clutter your system and can take your configurations anywhere, even on a USB stick. Furthermore, sandboxing via Bubblewrap using the right interfaces is a breeze. Not to mention integration via various tools, which simply extract the .desktop file and icon from the AppImage to integrate it into the menu.

I have many more reasons to suggest, but I'll leave it up to you to discover the advantages.

---------------------------------

## Tips

### Add a custom icon and launcher
Add a icon and a .desktop file near the script to use them in the root of the AppDir.

### Use custom AppRun
As for custom icon and .desktop file, it is possible to use custom AppRun scripts if placed near this tool.

In this example, linuxtoys:

https://github.com/user-attachments/assets/2145ac2b-3136-41c5-97ef-05f96c0aa0f7

### Create AppImages for more architectures
Regardless of your architecture, you can use `appimagetool` to create AppImage packages for multiple architectures (provided the executables are compatible with those architectures).

To do this with portable2appimage, you need to export the $arch variable, like this:
```
export arch=aarch64
```
for the arm64/aarch 64 architecture, or
```
export arch=i686
```
for the 32-bit/i386/i486/i586/i686 architecture.

By default, portable2appimage uses x86_64, also known as amd64.
