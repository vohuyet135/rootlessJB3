# Description

Blah blah, read this: [How to make a jailbreak without a filesystem remount as r/w](https://github.com/jakeajames/rootlessJB/blob/master/writeup.pdf)

- Powered by jelbrekLib


## Support

- All A9-A11 devices
- All A7-A8 devices

## To be supported (sorted by priority)

- A12 devices

**DO NOT ASK FOR ETA**

## Usage notes

- voucher_swap is used for 16K devices, and v3ntex for 4K ones.
- Binaries are located in: /var/containers/Bundle/iosbinpack64
- Launch daemons are located in /var/containers/Bundle/iosbinpack64/LaunchDaemons
- /var/containers/Bundle/tweaksupport contains a filesystem simulation where tweaks and stuff get installed
- Symlinks include: /var/LIB, /var/ulb, /var/bin, /var/sbin, /var/Apps, /var/libexec

All executables must have at least these two entitlements:

    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
        <key>platform-application</key>
        <true/>
        <key>com.apple.private.security.container-required</key>
        <false/>
    </dict>
    </plist>


- Tweaks and stuff get installed in: /var/containers/Bundle/tweaksupport the same way you did with Electra betas.
- Tweaks must be patched using the patcher script provided. (Mac/Linux/iOS only) or manually with a hex editor
- Apps get installed in /var/Apps and later you need to run /var/containers/Bundle/iosbinpack64/usr/bin/uicache (other uicache binaries won't work)

# iOS 12
- No amfid patch, either run "inject /path/to/executable_or_dylib" after adding stuff, or reboot and rejailbreak
- Sandbox exceptions are broken. You can't tweak App Store apps + some system apps yet. However, on the app's second run the backup sandbox patches will have triggered and you'll be able to read from the tweak directories. Tweaking will still not work on the second run unless you run jailbreakd's fixupdylib() on the target dylibs manually.
- This is not dangerous and cannot screw you up but not likely to be unstable/buggy
- Tweaks pre-patched for rootlessJB 1.0 and 2.0 will not work. Use new patcher script. (ldid was replaced with ldid2!)

# iOS 12 - UPDATE
- Added a modified dpkg (https://github.com/limneos/dpkg/) that automatically handles patching, moving, entitling, trusting ,app-installation and daemon injection for debs
- Added recompiled dropbear v2018.76 customized for rootlessJB with fixed shell (still accepts --shell) , additional --path option to set ssh-exported path, correct scp paths and motd. 
- Added recompiled ldid2, plutil, bintools (nm,strings,diff)
- Added tweaks check on re-jailbreaking to re-enable apps and daemons

## Deb files
- Some packages are taken from CoolStar' Electra repo


patcher usage:
./patcher /path/to/deb /path/to/output_folder

Thanks to: Ian Beer, Brandon Azad, Jonathan Levin, Electra Team, IBSparkes, Sam Bingner, Sammy Guichelaar.


