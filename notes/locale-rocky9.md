# Locale système sous Rocky Linux 9

*Écrit le 18 décembre 2024*

Lorsqu'on installe un système Rocky Linux 9 minimal en français (**Français** >
**France**), la locale système n'est pas correctement renseignée au redémarrage
initial :

```
# localectl status
System Locale: LANG=C.UTF-8
    VC Keymap: ch-fr
   X11 Layout: ch
  X11 Variant: fr
```

Installer un paquet manquant :

```
# dnf install -y glibc-langpack-fr
```

Redéfinir explicitement la locale système :

```
# localectl set-locale LANG=fr_FR.UTF-8
```

On pourra procéder de manière similaire avec d'autres langues :

```
# dnf install -y glibc-langpack-de
# localectl set-locale LANG=de_AT.UTF-8
```

