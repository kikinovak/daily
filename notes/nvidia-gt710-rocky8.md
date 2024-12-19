# Carte NVidia GT 710 sous Rocky Linux 8

*Écrit le 19 décembre 2024*

Le pilote propriétaire 470.xx est fourni par RPM Fusion :

```
# dnf info akmod-nvidia-470xx | head
...
Available Packages
Name         : akmod-nvidia-470xx
Epoch        : 3
Version      : 470.223.02
Release      : 1.el8
Architecture : x86_64
Size         : 84 k
Source       : nvidia-470xx-kmod-470.223.02-1.el8.src.rpm
Repository   : rpmfusion-nonfree
```

Installer le pilote :

```
# dnf install -y akmod-nvidia-470xx
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
                    nvidia-drm.modeset=1 \
                    quiet vga=791 mitigations=off"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```

Prendre en compte les modifications :

```
# grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
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

