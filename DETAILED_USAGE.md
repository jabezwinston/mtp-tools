## Device check : `mtp-detect`

- Probe for MTP devices
- Prints detailed information on each MTP device

```
$ mtp-detect

libmtp version: 1.1.19

Listing raw device(s)
Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
   Found 1 device(s):
   Motorola: Moto G (ID2) (22b8:2e82) @ bus 3, dev 30
Attempting to connect device(s)
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
USB low-level info:
   Interface has a kernel driver attached.
   bcdUSB: 512
   bDeviceClass: 0
   bDeviceSubClass: 0
   bDeviceProtocol: 0
   idVendor: 22b8
   idProduct: 2e82
.....
.....
.....

   MPEG-4 Part 14 Container Format (Audio+Video Emphasis)
   ISO MPEG-1 Audio Layer 2
   Abstract Playlist file
   XML file
   Free Lossless Audio Codec (FLAC)
OK.
```
---
## List files : `mtp-filetree`, `mtp-files`

- `mtp-filetree` - Lists files and folders with IDs (handles)
- `mtp-files`    - Lists  files and folders with detailed information

```
$ mtp-filetree
Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
Attempting to connect device(s)
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
Device: (NULL)
Storage: Internal shared storage
17 Makefile
18 calculator.h
19 add.c
20 div.c
21 get_number.c
22 main.c
23 mod.c
26 print_menu.c
28 sub.c
29 visa.pdf
OK.
```
---
## Copy file from device : `mtp-getfile`, `mtp-connect`,
- `mtp-getfile` expects **source file ID in device** (can be obtained using `mtp-filetree`) and **destination file path in host** as arguments
- `mtp-connect --getfile` expects **source file name in device** and **destination file path in host** as arguments

```
$ mtp-getfile 29 visa.pdf
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
Getting file/track 29 to local file visa.pdf
Progress: 606879 of 606879 (100%)

```
```
$ mtp-connect --getfile visa.pdf visa.pdf
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
Get file visa.pdf
Getting visa.pdf to visa.pdf
Unknown options: visa.pdf  (100%)
```
---
## Copy file into device : `mtp-sendfile`, `mtp-connect`
- `mtp-getfile` expects **source file path in host**  and **destination file path in device** as arguments
- `mtp-connect --getfile` expects **source file path in host** and **destination file path in device** as arguments

```
$ mtp-sendfile from_chennai.pdf from_chennai.pdf
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
Sending from_chennai.pdf to from_chennai.pdf
type: pdf, 44
Sending file...
Progress: 198494 of 198494 (100%)
New file ID: 30
```
```
$ mtp-connect --sendfile from_chennai.pdf from_chennai.pdf
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
Send file from_chennai.pdf
Sending from_chennai.pdf to from_chennai.pdf
type: pdf, 44
Sending file...
Progress: 198494 of 198494 (100%)
New file ID: 30
```
---
## Delete file in device : `mtp-delfile`, `mtp-connect`
```
mtp-delfile -f calculator.h
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
Deleting calculator.h
```
```
mtp-delfile -n 18
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
Deleting 18
```
```
$ mtp-connect --delete calculator.h
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
Delete calculator.h
```
---
### Create new folder : `mtp-newfolder`, `mtp-connect`
```
$ mtp-newfolder winston 0 0
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
New folder created with ID: 35
```
```
$ mtp-connect --newfolder winston
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
New folder winston
Creating new folder winston
New folder created with ID: 35
```
---
### Create sub-folder : `mtp-newfolder`
```
$ mtp-newfolder jabez 35 0
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
New folder created with ID: 36
```
---
### Format device : `mtp-format`
- Formats the device
- Generally Android devices don't support this operation !

```
$ mtp-format
libmtp version: 1.1.19

Device 0 (VID=22b8 and PID=2e82) is a Motorola Moto G (ID2).
libusb_detach_kernel_driver() failed, continuing anyway...: No error
Android device detected, assigning default bug flags
I will now format your device. This means that
all content (and licenses) will be lost forever.
you will not be able to undo this operation.
Continue? (y/n)
> y
Failed to format device.
Error 1: LIBMTP_Format_Storage(): device does not support formatting storage.

```
---