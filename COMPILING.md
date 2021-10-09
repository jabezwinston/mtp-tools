## Compiling MTP tools from source code (Windows)
- Install [Cygwin](https://www.cygwin.com/)
- Install additional Cygwin packages by re-running Cygwin downloader (`setup-x86`/`setup-x86_64`) using the below command
```
$ setup-x86 -q -P libtool,m4,automake,libiconv-devel,gettext-devel,libusb1.0-devel,wget,gcc-g++,make,git
```
- Launch Cygwin terminal
- Get [libmtp](https://github.com/libmtp/libmtp)
```
$ git clone https://github.com/libmtp/libmtp
```
- Checkout to a tag
```
$ cd libmtp
$ git tag
...
...
...
$ git checkout libmtp-1-1-19
```
- Start compilation and install binaries
```
$ ./autogen.sh
...
...
...
$ make
$ make install
```
- The compiled binaries can be found at `/usr/local/bin`
```
$ cd /usr/local/bin
$ ls mtp-*.exe
mtp-albumart.exe      mtp-files.exe        mtp-newfolder.exe    mtp-thumb.exe
mtp-albums.exe        mtp-filetree.exe     mtp-newplaylist.exe  mtp-tracks.exe
mtp-connect.exe       mtp-folders.exe      mtp-playlists.exe    mtp-trexist.exe
mtp-delfile.exe       mtp-format.exe       mtp-reset.exe
mtp-detect.exe        mtp-getfile.exe      mtp-sendfile.exe
mtp-emptyfolders.exe  mtp-getplaylist.exe  mtp-sendtr.exe

```
- Cygwin symlinks don't work natively in Windows and hence to need removed 
  (`mtp-delfile.exe`, `mtp-getfile.exe`, `mtp-newfolder.exe`, `mtp-sendfile.exe`,`mtp-sendtr.exe` are symlinks to `mtp-connect.exe` )
```
$ for f in $(find -type l);do cp --remove-destination $(readlink $f) $f;done;
```
- For using `mtp-tools` in a standalone way (without Cywin installation), check DLL depedencies of MTP binaries

```
$ ldd mtp-detect.exe

        ntdll.dll => /cygdrive/c/Windows/SYSTEM32/ntdll.dll (0x77160000)
        KERNEL32.DLL => /cygdrive/c/Windows/System32/KERNEL32.DLL (0x76240000)
        KERNELBASE.dll => /cygdrive/c/Windows/System32/KERNELBASE.dll (0x76650000)
        cygmtp-9.dll => /usr/local/bin/cygmtp-9.dll (0x655c0000)
        cygwin1.dll => /usr/bin/cygwin1.dll (0x61000000)
        cyggcc_s-1.dll => /usr/bin/cyggcc_s-1.dll (0x6fc70000)
        cygiconv-2.dll => /usr/bin/cygiconv-2.dll (0x6e670000)
        cygusb-1.0.dll => /usr/bin/cygusb-1.0.dll (0x6d8c0000)
```

Manually copy `cygmtp-9.dll`, `cygwin1.dll`, `cyggcc_s-1.dll`, `cygiconv-2.dll`, `cygusb-1.0.dll` along with `mtp-*.exe` binaries

- The size of `mtp-*.exe` binaries can be reduced by `strip` command

```
$ strip mtp-*.exe
```