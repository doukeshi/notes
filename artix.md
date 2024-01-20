# Artix -> Systemd-Free Arch Linux (with OpenRC)

## Bootstrap

```
# dd bs=512M if=img.iso of=/dev/sdX
# basestrap /mnt base base-devel linux-lts openrc elogind-openrc
```

## Configure the base system

```
# pacman -S linux-firmware {intel|amd}-ucode man-db

// Time
# ln -sf /usr/share/zoneinfo/UTC /etc/localtime
# hwclock --systohc

// User
# passwd root
# useradd -G wheel -m -s /bin/bash x
# passwd x
# visudo

// Localization
# vi /etc/locale.gen
# locale-gen

// 📄 > /etc/locale.conf
LANG=en_SG.UTF-8
LC_TIME=C.UTF-8
LC_COLLATE=C

// Host
# echo "archie" > /etc/hostname

// 📄 >> /etc/hosts
127.0.0.1   localhost
::1         localhost
127.0.1.1   archie
```

## EFI Boot Stub: EFISTUB

```
// 📄 > /boot/startup.nsh
vmlinuz-linux-lts rw root=PARTUUID=xxxx initrd=\{intel|amd}-ucode.img initrd=\initramfs-linux-lts.img
```

> - PARTUUID of the rootfs ?
>
> `$ blkid -s PARTUUID -o value /dev/sdX`
>
> - UEFI Shell is not avaliable
>
> Download [shell.efi](https://github.com/tianocore/edk2/blob/UDK2018/ShellBinPkg/UefiShell/X64/Shell.efi) to `/boot`

## Network

```
# pacman -S iwd
$ git -C /opt clone https://gitea.artixlinux.org/packages/iwd-openrc
# cp /opt/iwd-openrc/iwd.initd /etc/init.d/iwd
# chmod +x /etc/init.d/iwd

// 📄 > /etc/iwd/main.conf
[General]
EnableNetworkConfiguration=true
[Network]
EnableIPv6=true
NameResolvingService=none

// 📄 >> /etc/resolv.conf
nameserver ${dns-addr}
```

## Arch repos

```
# pacman -S artix-archlinux-support

// 📄 >> /etc/pacman.conf
# Arch
[extra]
Include = /etc/pacman.d/mirrorlist-arch

# pacman-key --populate archlinux
# pacman -Syyu
```

## fonts

```
# pacman -S noto-fonts noto-fonts-cjk noto-fonts-emoji
```
