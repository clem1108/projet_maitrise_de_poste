# Maitrise de poste day 2
## Sujet 4 

[graphe](./graphe.svg)

Les appareils USB
```bash
sudo dmesg | grep -i input
[sudo] Mot de passe de user : 
[    0.676046] input: Power Button as /devices/LNXSYSTM:00/LNXPWRBN:00/input/input0
[    0.676115] input: Sleep Button as /devices/LNXSYSTM:00/LNXSLPBN:00/input/input1
[    0.773465] input: AT Translated Set 2 keyboard as /devices/platform/i8042/serio0/input/input2
[    0.916761] input: Video Bus as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0A03:00/LNXVIDEO:00/input/input4
[    1.128376] input: ImExPS/2 Generic Explorer Mouse as /devices/platform/i8042/serio1/input/input5
[    1.971625] input: Unspecified device as /devices/pci0000:00/0000:00:04.0/input/input6
[    2.749642] input: VirtualBox USB Tablet as /devices/pci0000:00/0000:00:06.0/usb2/2-1/2-1:1.0/0003:80EE:0021.0001/input/input7
[    2.807586] hid-generic 0003:80EE:0021.0001: input,hidraw0: USB HID v1.10 Mouse [VirtualBox USB Tablet] on usb-0000:00:06.0-1/input0
[   10.101449] rfkill: input handler disabled
[   12.992290] rfkill: input handler enabled
[   14.940235] rfkill: input handler disabled
```

La version de Linuw
```bash
sudo dmesg | grep -i linux
[    0.000000] Linux version 5.4.0-38-generic (buildd@lgw01-amd64-011) (gcc version 9.3.0 (Ubuntu 9.3.0-10ubuntu2)) #42-Ubuntu SMP Mon Jun 8 14:14:24 UTC 2020 (Ubuntu 5.4.0-38.42-generic 5.4.44)
[    0.238814] ACPI: Added _OSI(Linux-Dell-Video)
[    0.238814] ACPI: Added _OSI(Linux-Lenovo-NV-HDMI-Audio)
[    0.238815] ACPI: Added _OSI(Linux-HPI-Hybrid-Graphics)
[    0.332878] pps_core: LinuxPPS API ver. 1 registered
[    0.332878] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.440362] Linux agpgart interface v0.103
[    0.459551] usb usb1: Manufacturer: Linux 5.4.0-38-generic ehci_hcd
[    0.531159] usb usb2: Manufacturer: Linux 5.4.0-38-generic ohci_hcd
[    0.551635] evm: security.selinux
[    2.057157] systemd[1]: systemd 245.4-4ubuntu3.1 running in system mode. (+PAM +AUDIT +SELINUX +IMA +APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +SECCOMP +BLKID +ELFUTILS +KMOD +IDN2 -IDN +PCRE2 default-hierarchy=hybrid)
[    7.896201] 12:27:28.844212 main     VBoxService 6.1.2 r135662 (verbosity: 0) linux.amd64 (Jan 13 2020 12:20:51) release log
[    7.896266] 12:27:28.844343 main     OS Product: Linux
               12:27:28.844468 main     Package type: LINUX_64BITS_GENERIC
```
les 5 lignes : 
* `BOOT_IMAGE=/boot/vmlinuz-5.4.0-38-generic root=UUID=9566a53d-2296-49c3-a10d-ccbf6b916324 ro quiet splash`  :arrow_right: montre le noyau de Linux sur lequel démarrer.
* `systemd[1]: Finished Load Kernel Modules.` :arrow_right: indique que tous les modules sont chargés.
* `systemd[1]: Mounted Kernel Configuration File System.` :arrow_right: indique que les fichiers de configuration système sont chargés.
* `systemd[1]: Started udev Kernel Device Manager` :arrow_right: indique que gestionnaire de périphériques de Linux est chargé.
* `IPv6: ADDRCONF(NETDEV_CHANGE): enp0s3: link becomes ready` :arrow_right: indique que la carte réseau est opérationnelle.

Le kernel ne génère plus de logs une fois le système démarré.

## sujet 3 
```shell
PS C:\Users\cleme> vboxmanage debugvm "windows 10" dumpvmcore --filename test.elf
```
```bash
user@MSI:/mnt/c/Users/cleme$ objdump -h test.elf|egrep -w "(Idx|load1)"
Idx Name          Size      VMA               LMA               File off  Algn
  1 load1         20000000  0000000000000000  0000000000000000  00006c00  2**0
user@MSI:/mnt/c/Users/cleme$ size=0x20000000;off=0x6c00;head -c $(($size+$off)) test.elf|tail -c +$(($off+1)) > test.raw

user@MSI:/mnt/c/Users/cleme$ volatility -f test.raw imageinfo
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : No suggestion (Instantiated with no profile)
                     AS Layer1 : FileAddressSpace (/mnt/c/Users/cleme/test.raw)
                      PAE type : No PAE
```
L'analyse ne fonctionne pas :cry: 