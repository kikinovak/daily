# Conky avec KDE sous Rocky Linux

*Écrit le 1er janvier 2025*

Installer Conky :

```
# dnf install -y conky
```

Lancer Conky manuellement pour un premier test :

```
$ conky &
```

Peaufiner la configuration dans `/etc/conky/conky.conf`.

Définir le lancement automatique de Conky :

```
# cp /usr/share/applications/conky.conf /etc/xdg/autostart/
```

