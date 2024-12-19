# Paramétrage de GRUB sous Rocky Linux 9

*Écrit le 19 décembre 2024*

Depuis RHEL 9.3 la modification des paramètres de *kernel* dans GRUB ne se
passe plus tout à fait pareil.

À présent toute modification dans `/etc/default/grub` sera prise en compte par
la commande suivante :

```
# grub2-mkconfig --update-bls-cmdline -o /boot/grub2/grub.cfg
```

L'option `--update-bls-cmdline` se charge de mettre à jour toutes les entrées
qui figurent dans `/boot/loader/entries/` (une par *kernel* installé) :

```
# ls /boot/loader/entries/
1df74135e5b449d8ad2835d6a64a22d7-0-rescue.conf
1df74135e5b449d8ad2835d6a64a22d7-5.14.0-503.14.1.el9_5.x86_64.conf
1df74135e5b449d8ad2835d6a64a22d7-5.14.0-503.16.1.el9_5.x86_64.conf
# grep options /boot/loader/entries/*.conf
```

> Notons également que la commande pour mettre à jour la configuration sur un
> système UEFI est la même que sur un système avec un BIOS Legacy.

Et pour afficher les paramètres qu'on a effectivement utilisés pour démarrer :

```
# cat /proc/cmdline
```

