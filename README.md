Flatpak-builder manifest for Cisco Packet Tracer
================================================
Based on Freedesktop runtime.

The Software License Agreement of Cisco Packet Tracer forbids third party
distribution. This means that public flatpak repositories
cannot provide this app for you. But don't worry, this repo helps you to
build the flatpak package by yourself from scratch.
Flatpak-building is a simple, distro-independent process, just follow the
steps below.

Let's do it!

## Clone this repo
`$ git clone https://github.com/rpallai/flatpak-pt.git`

## Install flatpak-builder and build dependencies
```
$ sudo dnf install flatpak-builder
$ flatpak install flathub org.freedesktop.Platform/x86_64/18.08 org.freedesktop.Sdk/x86_64/18.08
```
DNF is for Fedora, you might want to use 'apt' here.
If the "flathub" repository is not installed yet, see [this guide](https://flatpak.org/setup/).

## Download Packet Tracer
Supported releases:

- Packet Tracer 7.1.1 for Linux 64 bit.tar.gz
- Packet Tracer 7.2.1 for Linux 64 bit.tar.gz

You can download these from [netacad.com](https://netacad.com) after login. Put that file into the
"flatpak-pt" folder, next to the .json manifest. Do not unpack the archive.

Replace "com.cisco.PacketTracer-71" below with "com.cisco.PacketTracer-72" if you've chosen version 7.2.

## Build and install with flatpak
```
$ cd flatpak-pt && flatpak-builder --delete-build-dirs --force-clean --user --install build-dir com.cisco.PacketTracer-71.json
```

Now you can run the app if the build succeeded. Use your application launcher as usual.

Do not move the newly created "./.flatpak-builder" directory while the package is installed.

## Set the "PT7HOME" environment variable
This step is required for ptaplayer which is a javaws applet used by web assessments.
This applet works pretty well with different versions/spins of Java.

`$ echo "export PT7HOME=~/.local/share/flatpak/app/com.cisco.PacketTracer-71/current/active/files" >>~/.bashrc`

Log off, log in and that's all!

You can test your installation [here](https://assessment.netacad.net/check/check.html).

## Notes
- NetacadExamPlayer is not supported in 7.2
