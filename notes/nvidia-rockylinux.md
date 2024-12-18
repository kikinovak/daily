# Cartes NVidia sous Rocky Linux

*Écrit le 18 décembre 2024*

Une bonne page d'infos assez synthétique dans le forum de la distribution :

- [NVidia Drivers on Rocky
  Linux](https://forums.rockylinux.org/t/nvidia-drivers-on-rocky-linux/12366)

Et aussi cette page sur le site du projet RPM Fusion :

- [NVidia HOWTO](https://rpmfusion.org/Howto/NVIDIA)

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
