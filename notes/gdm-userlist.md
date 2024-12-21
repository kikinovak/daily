# Désactiver l'affichage des utilisateurs dans GDM

*Écrit le 21 décembre 2024*

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

