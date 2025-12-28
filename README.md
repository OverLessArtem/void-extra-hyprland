# Void-Extra

> [!NOTE]
> This project is **not affiliated with or endorsed by the Void Linux project** or its maintainers.
>
>Use at your own discretion.

## Overview
A collection of template files for building packages on Void Linux with xbps-src.
If you don't wish to build the packages locally, this repository also provides prebuilt binaries.

> [!WARNING]
> The project has been renamed to void-extra to avoid confusion with Arch Linux’s AUR. Unlike the AUR, this repository is not intended as a way to add packages to Void Linux before they reach upstream. It is only a fallback for packages that have been rejected. See below for how to update your /etc/xbps.d/ entry.

<hr>

## Installation
Currently packages are tested on / crosscompiled for the following architectures:
- x86_64
- x86_64-musl
- aarch64
- aarch64-musl

<details>
<summary><b> 🛠️ Manually building </b></summary>
  
1. Clone both this repository as well as [void-packages](https://github.com/void-linux/void-packages):

    ```
    git clone https://github.com/Encoded14/void-extra.git
    git clone https://github.com/void-linux/void-packages.git
    ```
2. Copy the template files from this repository into void-packages:

    ```
    cp -r void-extra/srcpkgs/* void-packages/srcpkgs/
    ```
3. Edit shlibs by removing the lines found in shlibs_remove and appending the lines from shlibs_append.

    ```
    cd void-packages
    nvim common/shlibs
    ```
4. Bootstrap the build system:

    ```
    ./xbps-src binary-bootstrap
    ```
5. Build the packages you want:

    ```
    ./xbps-src pkg <package1> <package2> ...
    ```
6. Install the built packages:

    ```
    sudo xbps-install --repository /hostdir/binpkgs/ <package1> <package2> ...
    ```

</details>

<details>
<summary><b> 📦 Prebuilt binaries </b></summary>

1. Create an entry in /etc/xbps.d/ and add this repository. (Edit the end of the link with the architecture you require from the list above). This can be done with the following command:
    ```
    echo repository=https://raw.githubusercontent.com/Encoded14/void-extra/repository-x86_64 | sudo tee /etc/xbps.d/20-repository-extra.conf
    ```
2. Refresh your repositories and accept the fingerprint:

    ```
    sudo xbps-install -S
    ```
3. You are now able to search through all of the packages in this repository, and install them as usual:

    ```
    xbps-query -Rs hypr
    sudo xbps-install -S hyprland 
    ```

</details>

<hr>

### Running Hyprland

In order to run Hyprland you will need to install some additional packages which will depend on your setup, for example a [session and seat manager](https://docs.voidlinux.org/config/session-management.html) and [graphics drivers](https://docs.voidlinux.org/config/graphical-session/graphics-drivers/index.html). If you use an Nvidia GPU refer to the [Hyprland Wiki](https://wiki.hyprland.org/Nvidia), but keep in mind that Hyprland does not officially support Nvidia.

### Contributing
Contributions are greatly appreciated. Overall, this repository adheres to the same rules and guidelines as the [official void-packages repository](https://github.com/void-linux/void-packages/blob/master/CONTRIBUTING.md).

### Credits
[Makrennel: hyprland-void](https://github.com/Makrennel/hyprland-void): Hyprland template files
