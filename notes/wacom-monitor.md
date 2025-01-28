# Mapper une tablette Wacom pour un seul moniteur

*Écrit le 28 janvier 2025*

Dans la configuration par défaut, une tablette Wacom utilise les deux moniteurs
lorsqu'on utilise un double écran. En règle générale, on voudra plutôt en
utiliser un seul sur les deux.

Identifier la tablette :

```
$ xinput | grep stylus
    ↳ Wacom Intuos S Pen stylus   id=12  [slave  pointer  (2)]
```

Ici, on note l'identifiant `12`.

Identifier les écrans :

```
$ xrandr | grep ' connected'
DVI-D-0 connected primary 1680x1050+0+0 ...
HDMI-0 connected 1680x1050+1680+0 ...
```

Mapper la tablette sur l'écran de droite :

```
$ xinput map-to-output 12 HDMI-0
```

Mapper la tablette sur l'écran de gauche :

```
$ xinput map-to-output 12 DVI-D-0
```

> Il existe une méthode alternative avec `xsetwacom` mais elle ne détecte pas
> correctement les écrans suite à un bug avec le pilote NVidia.

