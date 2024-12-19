# Carte NVidia GTX 1650 sous Rocky Linux 8

*Écrit le 19 décembre 2024*

Le pilote propriétaire 550.xx est fourni par RPM Fusion :

```
# dnf info akmod-nvidia | head
...
Available Packages
Name         : akmod-nvidia
Epoch        : 3
Version      : 550.127.05
Release      : 1.el8
Architecture : x86_64
Size         : 88 k
Source       : nvidia-kmod-550.127.05-1.el8.src.rpm
Repository   : rpmfusion-nonfree
```

Installer le pilote :

```
# dnf install -y akmod-nvidia
```

L'installation du paquet ajoute automatiquement une entrée dans
`/etc/default/grub` pour empêcher le chargement du module `nouveau`, mais les
paramètres sont inscrits en doublons. C'est donc une bonne idée de rectifier le
tir à la main :

```
# /etc/default/grub
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_CMDLINE_LINUX="rd.driver.blacklist=nouveau \
                    modprobe.blacklist=nouveau \
                    quiet vga=791 mitigations=off \
                    loglevel=3"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```

Prendre en compte les modifications sur un système BIOS Legacy :

```
# grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
done
```

Sur un système UEFI :

```
# grub2-mkconfig -o /boot/efi/EFI/rocky/grub.cfg
Generating grub configuration file ...
Adding boot menu entry for EFI firmware configuration
done
```

Redémarrer :

```
# reboot
```

Lancer l'outil de paramétrage NVidia en mode graphique pour vérifier la bonne
prise en charge du pilote :

```
$ nvidia-settings
```

