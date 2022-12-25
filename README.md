# Why this Exists, What it is

Microsoft disables the NTFS functionality on purpose on [their WSL Kernel](https://github.com/microsoft/WSL2-Linux-Kernel) releases. This is my custom kernel where I only enable NTFS functionality and touch nothing else. Made for people who want to mount NTFS formatted devices in their WSL Container/Distro without the extra steps needed to compile their own kernels. Also solves issues like: [missing NTFS3 kernel modules](https://github.com/microsoft/WSL/issues/8564), [etc](https://github.com/microsoft/WSL/issues?q=ntfs)

# Installation (more like _Replacing the Microsoft Kernel with Yours_)
1. If you launched your WSL distro(s) or instance(s), shut them down (all at once) by entering `wsl --shutdown` in PowerShell. If you want to shut down a specific Distro do that by entering `wsl -t DISTRO-NAME`. Get the distro names with `wsl --list --verbose`.
2. Download my latest kernel from the [releases](), or [compile it yourself]().
3. Put the file wherever you want on your Windows Host (the file has to stay there as long as you use that kernel, without the file in place your WSL2 distros won't launch).
4. Create a file called `.wslconfig` in your user home directory (generally `C:\Users\<username>` or aka `%HOMEDRIVE%\%HOMEPATH%`, in a simpler form `%UserProfile%`) with the following contents, my kernel file name is **'vmlinux'** and I placed it in `C:\Users\<myuser>` (the default kernel filename is 'vmlinux' if you don't change it, also the double backslashes are for escaping characters, so they are needed):
```ini
[wsl2]
kernel=C:\\Users\\main\\vmlinux
```
5. Launch your (default) distro with the new kernel by typing `wsl` or a specific one with `wsl -d DISTRO-NAME`.

# Build Instructions
**NOTE:** You can use a barebone Linux Install or a Virtual Machine for the building process. You can do it on WSL too, but you have to make sure not to do it under your Windows Hosts filesystem (so don't clone the repo inside `/mnt/c` or a subfolder of that, the same when compiling too. Use a folder like `~/tmp` for the cloning and compilation). Else you'll get errors because of filesystem case-sensivity conflicts. The easiest workaround is this. You can also configure case-sensivity on a folder basis on Windows, which would be another way (which I never tested).
1. Install dependencies:
    - Ubuntu/Debian Based Distros: `apt install -y build-essential flex bison dwarves libssl-dev libelf-dev`
    - Arch Based Distros: `pacman -S base-devel bc python pahole`
    - Alpine: `apk add make gcc libc-dev flex bison linux-headers libressl-dev elfutils-dev python3 perl pahole`
    - Fedora: `dnf install make gcc flex bison openssl openssl-devel bc elfutils-devel diffutils dwarves`
2. ...
