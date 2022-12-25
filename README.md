# Why this Exists, What it is

Microsoft disables the NTFS functionality on purpose on [their WSL Kernel](https://github.com/microsoft/WSL2-Linux-Kernel) releases. This is my custom kernel where I only enable NTFS functionality and touch nothing else. Made for people who want to mount NTFS formatted devices in their WSL Container/Distro without the extra steps needed to compile their own kernels. Also solves issues like: [missing NTFS3 kernel modules](https://github.com/microsoft/WSL/issues/8564), [etc](https://github.com/microsoft/WSL/issues?q=ntfs)

# Installation (more like _Replacing the Microsoft Kernel with Yours_)
1. If you launched your WSL distro(s) or instance(s), shut them down (all at once) by entering `wsl --shutdown` in PowerShell. If you want to shut down a specific Distro do that by entering `wsl -t DISTRO-NAME`. Get the distro names with `wsl --list --verbose`.
2. Download my latest kernel from the [releases](), or [compile it yourself]().
3. Put the file wherever you want on your Windows Host (the file has to stay there as long as you use that kernel, without the file in place your WSL2 distros won't launch).
4. Create a file called `.wslconfig` in your user home directory (generally `C:\Users\<username>` or aka `%HOMEDRIVE%\%HOMEPATH%`, in a simpler form `%UserProfile%`) with the following contents, my kernel file name is **'vmlinux'** and I placed it in `C:\Users\<myuser>` (the default kernel filename is 'vmlinux' if you don't change it, also the double backslashes are for escaping characters, so they are needed):
```
[wsl2]
kernel=C:\\Users\\main\\vmlinux
```
5. Launch your (default) distro with the new kernel by typing `wsl` or a specific one with `wsl -d DISTRO-NAME`.

# How to Compile
