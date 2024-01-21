# QEMU

```
# pacman -S qemu-desktop
# usermod -aG kvm x

// Creat a hard disk image in the qcow2 format
$ qemu-img create -f qcow2 xx.img 32G

// Boot in UEFI mode: Copy OVMF_VARS
$ cp /usr/share/edk2/x64/OVMF_VARS.4m.fd .

// 📄 > COMMAND
$ qemu-system-x86_64 -daemonize -enable-kvm -cpu host -m 8G \
-drive virtio-vga-gl -display gtk,gl=on \
-drive if=pflash,format=raw,readonly=on,file=/usr/share/edk2/x64/OVMF_CODE.4m.fd \
-drive if=pflash,format=raw,file=/copy/of/OVMF_VARS.4m.fd \
-drive file=xx.img,if=virtio,aio=native,cache.direct=on \
-cdrom xx.iso
```

> For more about OVMF, ref: https://github.com/tianocore/edk2/blob/master/OvmfPkg/README

## User-mode network

```
# ip link set eth0 up
# ip addr add 10.0.2.15/24 dev eth0
$ ip route add default via 10.0.2.2 dev eth0

// 📄 >> /etc/resolv.conf
nameserver 10.0.2.3
```
