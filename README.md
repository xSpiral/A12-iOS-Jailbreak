# Description

Blah blah, read this: [How to make a jailbreak without a filesystem remount as r/w](https://github.com/jakeajames/rootlessJB/blob/master/writeup.pdf)

- Powered by jelbrekLib64e

## Supported 

- A12 devices

## Future Support

- All A7-A11 devices


## Usage notes

Currently, it will get root, unsandbox, and inject binaries in the trustcache.
However, jailrbeakd is not working, and running binaries(i.e. dropbear and uicache) and not working


- voucher_swap is used for 16K devices
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
- amfid is patched, however it'll require you to resign everything with a cert. Use `codesign -s 'IDENTITY' --entitlements /path/to/entitlements.xml --force /path/to/binary` **or** inject everything as usual. However note that soon I won't be injecting stuff automatically on jailbreak anymore!
- You **can** tweak App Store apps, but you'll either have to call jailbreakd's fixMmap() yourself **or** resign things with a real cert and amfid will handle that for you. Second option is preferred. See previous point on how to.
- This is not dangerous and cannot screw you up.
- Tweaks pre-patched for rootlessJB 1.0 and 2.0 will not work. Use new patcher script. (ldid was replaced with ldid2!)

patcher usage:
./patcher /path/to/deb /path/to/output_folder

# TODO (iOS 12-12.1.2, A12 Devices)
- create pmap bypass to enable executable mappings for binaries
- fix patchfinder with trustcache 
- testing testing testing

Thanks to: Ian Beer, Brandon Azad, Jonathan Levin, Electra Team, IBSparkes, Sammy Guichelaar, unc0ver by pwn20wnd & sbingner

