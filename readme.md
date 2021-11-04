## Steps to Cross-compile for RPi (including older, Armv6 architectures)
1. Get the cross compiler as described in [this repo](https://github.com/Pro/raspi-toolchain).
2. Extract into `/opt/cross-pi-gcc`
3. Get the toolchain.make file from the current repo.
4. Sync (using rsync) the following folders into a "rootfs" folder. Folders to be synced from RPi:
   * /lib
   * /usr
   * /opt/vc/lib

    Use The following command for the rsync:
    ```
    rsync -vR --progress -rl --delete-after --safe-links pi@raspberrypi.local:/{lib,usr,opt/vc/lib} $HOME/rpi/rootfs
    ```

5. Set the environment variable `$RASPBIAN_ROOTFS` to point to the rootfs folder.
6. In VSCode install `cmake-tools` extension 
7. Press `Ctrl-Shift-P` to open context menu and select `CMake: Edit User-Local CMake Kits`
8. Add the following configuration in CMake Kits (at the end of the file is ok):
   ```
    {
        "name": "RaspberryPi Zero cross compile using toolchain.cmake",
        "toolchainFile": "<path to toolchain.cmake>"
    }
   ```
9. Then use VSCode to configure and run the build (from cmake-tools)