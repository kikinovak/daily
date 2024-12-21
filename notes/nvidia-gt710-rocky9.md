# Carte NVidia GT 710 sous Rocky Linux 9

*Écrit le 21 décembre 2024*

Le pilote `akmod-nvidia-470xx` fourni par le dépôt RPM Fusion ne fonctionne
pas. En revanche on peut prendre celui de ELRepo Testing :

```
# dnf --disablerepo=rpmfusion* --enablerepo=elrepo-testing \
  info kmod-nvidia-470xx | head
...
Available Packages
Name         : kmod-nvidia-470xx
Version      : 470.256.02
Release      : 2.el9_5.elrepo
Architecture : x86_64
Size         : 41 M
Source       : kmod-nvidia-470xx-470.256.02-2.el9_5.elrepo.nosrc.rpm
Repository   : elrepo-testing
```

Installer le pilote :

```
# dnf --disablerepo=rpmfusion* --enablerepo=elrepo-testing \
  install -y kmod-nvidia-470xx
```

L'installation du paquet ajoute automatiquement une entrée dans
`/etc/default/grub` pour empêcher le chargement du module `nouveau`, mais les
paramètres sont inscrits en doublons. C'est donc une bonne idée de rectifier le
tir à la main :

```
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_CMDLINE_LINUX="rd.driver.blacklist=nouveau \
                    modprobe.blacklist=nouveau \
                    nouveau.modeset=0 \
                    nvidia-drm.modeset=1 \
                    quiet vga=791 mitigations=off \
                    loglevel=3"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```

Prendre en compte les modifications (Systèmes UEFI et BIOS Legacy) :

```
# grub2-mkconfig --update-bls-cmdline -o /boot/grub2/grub.cfg
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

