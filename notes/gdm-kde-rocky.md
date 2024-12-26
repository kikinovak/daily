# GDM et KDE sous Rocky Linux

*Écrit le 26 décembre 2024*

Le gestionnaire de connexion SDDM comporte quelques bugs prohibitifs, notamment
avec les pilotes NVidia. On peut très bien le remplacer par GDM.


## Définir la session par défaut

Le répertoire `/usr/share/accountsservice/user-templates/` comporte deux
fichiers `administrator` et `standard`. Copier ces deux *templates* vers
`/etc/accountsservice/user-templates/` en remplaçant la session `gnome` par
défaut par `plasmax11` :

```
[User]
Session=plasmax11
Icon=${HOME}/.face
```

> Le nom de la session se trouve dans `/usr/share/xsessions` pour X11 et
> `/usr/share/wayland-sessions` pour Wayland.


## Désactiver les autres sessions

Si l'on ne souhaite pas afficher les autres sessions dans le menu de sélection
de GDM, il suffit d'ajouter `NoDisplay=true` au fichier `.desktop`
correspondant.


## Personnaliser le logo

Pour personnaliser le logo de GDM, on peut remplacer le fichier
`/usr/share/pixmaps/fedora-gdm-logo.png`.


## Désactiver l'affichage des utilisateurs

Dans la configuration par défaut, GDM affiche la liste des utilisateurs dans un
ordre assez erratique, en fonction des dernières connexions.

Pour désactiver cet affichage, éditer un fichier
`/etc/dconf/db/gdm.d/00-login-screen` comme ceci :

```
# /etc/dconf/db/gdm.d/00-login-screen
[org/gnome/login-screen]
disable-user-list=true
```

Prendre en compte les modifications :

```
# dconf update
```

