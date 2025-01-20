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
# cd /etc/xdg/autostart
# ln -s /usr/share/applications/conky.desktop .
```

Éventuellement il faudra éditer `conky.desktop` et augmenter la durée d'attente
(option `--pause`) de `1` à `5` :

```
[Desktop Entry]
Type=Application
Exec=conky --daemonize --pause=5
StartupNotify=false
Terminal=false
Icon=conky-logomark-violet
NoDisplay=true
```

