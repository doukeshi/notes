# Sway

```
# pacman -S noto-fonts sway foot fuzzel
```

## seatd

```
# usermod -aG seat x
$ git -C /opt clone https://gitea.artixlinux.org/packages/seatd-openrc
# cp /opt/seatd-openrc/seatd.initd /etc/init.d/seatd
# chmod +x /etc/init.d/seatd
# ln -sf /etc/init.d/seatd /etc/runlevels/boot/seatd
```

## Config

```
$ cp /etc/sway/config ~/.config/sway/config

// 📄 <> ~/.config/sway/config
set $mod Mod1
set $term foot
set $menu fuzzel
```
