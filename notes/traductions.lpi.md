# Traductions LPI

*Écrit le 11 janvier 2025*

Détails : `LPI-Translation-Guide.pdf`

Se connecter à la plateforme GitLab du *Linux Professional Institute* :

* https://git.lpi.org/

Afficher le clé SSH publique :

$ cat ~/.ssh/id_rsa.pub

Importer la clé SSH sur la plateforme : **Preferences** > **SSH Keys**

Afficher la page du projet, par exemple :

* https://git.lpi.org/learningmaterials/lm-101-fr

Cliquer sur **Code** et copier le lien **Clone with SSH** dans le
presse-papier.

Cloner le répertoire en utilisant l'option `--recursive` :

```
$ git clone --recursive git@git.lpi.org:learningmaterials/lm-102-fr.git
$ cd lm-102-fr/
$ git submodule update --remote --merge
```

> Si c'est un nouveau projet, il faudra éventuellement créer quelques
> répertoires manquants.

Lancer OmegaT et ouvrir le projet : **Projet** > **Ouvrir**

> Dans la fenêtre subséquente (`OmegaT a détecté un projet en équipe de type
> 3.6`) il faut impérativement cliquer sur **Annuler**.

Depuis la version 6.0 il faut paramètrer OmegaT : **Options** > 
**Préférences** > **Éditeur** :

- [x] Insérer le texte source

- [ ] Insérer la meilleure correspondance

- [ ] Tenter de remplacer les nombres des correspondances

- [ ] Autoriser une traduction identique à la source

