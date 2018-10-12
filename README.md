Flatpak-builder manifest for Cisco Packet Tracer
================================================
Based on Freedesktop runtime.

The Software License Agreement of Cisco Packet Tracer forbids the third party
distribution of the software. Which means that public flatpak repositories
cannot provide this app for you. But don't worry, this repo helps you to
build the flatpak package for yourself from scratch.
Flatpak-building is a distro-independent and simple process, just follow the
steps below.

Let's do it!

## Clone this repo
`$ git clone https://github.com/rpallai/flatpak-pt.git`

## Install flatpak-builder and build dependencies
```
$ sudo dnf install flatpak-builder
$ flatpak install flathub org.freedesktop.Sdk/x86_64/18.08
```
DNF is for Fedora, you might want to use 'apt-get' here.
If the "flathub" repository is not installed yet, see [this guide](https://flatpak.org/setup/).

## Download Packet Tracer
Supported releases:

- Packet Tracer 7.1.1 for Linux 64 bit.tar.gz
- Packet Tracer 7.2 for Linux 64 bit.tar.gz

You can download these from [netacad.com](https://netacad.com) after login. Put the file into the
"flatpak-pt" folder, next to the .json manifest.

Replace "com.cisco.PacketTracer-71" below with "com.cisco.PacketTracer-72" if you've chosen version 7.2

## Build and install with flatpak
```
$ cd flatpak-pt
$ flatpak-builder --user --install build-dir com.cisco.PacketTracer-71.json
```

The build ends with the following lines if everything went well:
```
Installing for user: com.cisco.PacketTracer-71/x86_64/master from com.cisco.PacketTracer-71-origin
[####################] 2 metadata, 1 content objects imported
Now at e97c4c055a16.
Pruning cache
```

Now you can run the app from the Application Launcher, just search for "cisco".

## Set the "PT7HOME" environment variable
This step is required for ptaplayer which is a javaws applet used by web assessments.
The applet works pretty well with different versions/spins of Java.

`$ echo "export PT7HOME=~/.local/share/flatpak/app/com.cisco.PacketTracer-71/current/active/files" >>~/.bashrc`

Log off, log in and that's all!

## Notes
- NetacadExamPlayer is not supported in 7.2
