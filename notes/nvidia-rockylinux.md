# Cartes NVidia sous Rocky Linux

WORK IN PROGRESS

*Écrit le 18 décembre 2024*

Une bonne page d'infos assez synthétique dans le forum de la distribution :

- [NVidia Drivers on Rocky
  Linux](https://forums.rockylinux.org/t/nvidia-drivers-on-rocky-linux/12366)

Et aussi cette page sur le site du projet RPM Fusion :

- [NVidia HOWTO](https://rpmfusion.org/Howto/NVIDIA)

## Carte GeForce GT 710 sous Rocky Linux 8

Vérifier le modèle de la carte :

```
# lspci | grep -i vga
01:00.0 VGA compatible controller: NVIDIA Corporation GK208B 
[GeForce GT 710] (rev a1)
```

Cette carte s'utilise avec le pilote 470.xx.

```
# dnf install -y akmod-nvidia-470xx
# reboot
```

> Le prochain démarrage peut durer quelques minutes, vu que le module est
> construit.

Vérifier si le pilote fonctionne correctement :

```
$ nvidia-settings
```

## Carte GeForce GT 710 sous Rocky Linux 9

Le pilote en provenance de RPM Fusion ne marche pas. En revanche celui de
ELRepo Testing fonctionne.

```
# dnf --disablerepo=rpmfusion* --enablerepo=elrepo-testing \
  install kmod-nvidia-470xx
# reboot
```


## Carte GTX 1650 sous Rocky Linux 9

Le pilote de RPM Fusion ne marche pas. On prend celui de ELRepo :

# dnf install nvidia-x11-drv
# reboot



###########################################

Pour installer le pilote le plus récent depuis le dépôt RPM Fusion :

```
# dnf install xorg-x11-drv-nvidia akmod-nvidia
```

Pour une version plus ancienne du pilote :

```
# dnf install xorg-x11-drv-nvidia-470xx akmod-nvidia-470xx
```

> Les paquets se chargent automatiquement de blacklister le module `nouveau`.
> Ce n'est donc pas la peine de le faire à la main.

Pour tester : 

# dnf install -y git
# git clone https://gitlab.com/kikinovak/rocky-8-desktop
# cd rocky-8-desktop
# ./setup --shell
# ./setup --repos
# ./setup --tools
# dnf group install -y base-x
# dnf install -y fluxbox xterm
# reboot

$ echo "exec fluxbox" > ~/.xinitrc
$ startx

