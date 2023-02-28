# [Fedora](https://fedoraproject.org/wiki/Fedora_Project_Wiki) [<img src="https://github.com/SfikasTeo/Fedora/blob/main/Fedora_Logo.png" width="350" align="right" alt="Fedora">](https://docs.fedoraproject.org/en-US/docs/)
Fedora is an open sourced project suppported and maintained mainly by the [Red Hat Enterprise](https://www.redhat.com/en). The aim is a **leading edge** distribution with tested transitions between newer kernel versions and packages, following a **point release** methodology.  
The package management system of fedora is based on **[RPMs](https://en.wikipedia.org/wiki/RPM_Package_Manager)** with [DNF](https://dnf.readthedocs.io/en/latest/index.html) as the management tool. The fedora project offers a plethora of spins for different use cases, most commonly recommended are the **[Workstation](https://getfedora.org/en/workstation/)** for *plug and play use* or the **[Server](https://getfedora.org/en/server/)** spin for a more advanced and customized experience.  
Finally fedora by default uses **[systemd](https://docs.fedoraproject.org/en-US/quick-docs/understanding-and-administering-systemd/)** as the initialization system, and has migrated to the use of **[Wayland](https://wayland.freedesktop.org/)** instead of X11. Automatically implemented are also the firewalld and zram utilities.

## Starting up: Most commonly referred resources

* [Fedora Quick Docs](https://docs.fedoraproject.org/en-US/quick-docs/)
* [Fedora Project Wiki](https://fedoraproject.org/wiki/Fedora_Project_Wiki)
* [DNF Package Manager](https://dnf.readthedocs.io/en/latest/index.html)
* [Fedora Packages](https://packages.fedoraproject.org/)

## Fedora Package management and [DNF](https://docs.fedoraproject.org/en-US/quick-docs/dnf/)
DNF is generally considered one of the **slowest** package management systems. The first time DNF is used, a relatively **big size of metadata** from every repository must be updated, giving the first truth to the statement above. After the first use and after determining the fastest mirrors, although the package management is quite faster, **compared** to other package managers like **apt** or **pacman**, dnf lacks behind in speed. Configuring DNF with the following arguments is always recommended.
* **Add** the following options to DNF configuration file `sudo nano /etc/dnf/dnf.conf`
```
fastestmirror=True
max_parallel_downloads=5
defaultyes=True
```
* Reevaluating repositories metadata for faster mirrors may be advised: `dnf clean metadata`
* Most commonly used commands : 
    * `dnf info <package>` Display information about installed packages
    * `dnf search <package>` Search repositories for specific package
    * `dnf install <package>` Install specific package from a repository
    * `dnf remove <package>` Remove a specific package and its dependencies
    * `dnf upgrade` Upgrade system or specific package
 * **[Enable RPM Fusion](https://docs.fedoraproject.org/en-US/quick-docs/setup_rpmfusion/)**
 ```
 sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
 sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
 ```
 * Enable **[flathub](https://flathub.org/home)** repositories: 
 ```
 flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
 ```
 
 ## Install additional [media Codecs](https://docs.fedoraproject.org/en-US/quick-docs/assembly_installing-plugins-for-playing-movies-and-music/) From RPM Fusion
Several offline media players *like vlc or mpv* bundle all the relevant codecs by themselves.
```
sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel
sudo dnf install lame\* --exclude=lame-devel
sudo dnf group upgrade --with-optional Multimedia
 ```

