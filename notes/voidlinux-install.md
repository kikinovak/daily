# Void Linux - Installation du système de base

*Écrit le 16 décembre 2024*

Téléchargement : **base** >  **Live image** (`glibc`)

- `void-live-x86_64-20240314-base.iso`

Clé USB :

```
# dd status=progress bs=4M if=void-live-x86_64-20240314-base.iso of=/dev/sdX
# sync
```

Démarrage : **[Tab]** à l'invite de GRUB pour afficher les options

- Disposition clavier : `vconsole.keymap=fr_CH-latin1`

- Résolution de la console : `video=800x600` (`1024x768`)

Clavier QWERTY à l'invite de GRUB :

- **[Y]** = **[Z]**

- **[_]** = **[Maj]** + **[)]**

- **[-]** = **[)]**

Void Live login :

  - `root` : `voidlinux`

  - `anon` : `voidlinux`

Lancer l'installateur :

```
# void-installer
```

- Clavier système : `fr_CH-latin1`

- Réseau : `DHCP`

- Source d'installation : `ISO`

- Nom d'hôte : `voidbox`

- Localisation : `fr_FR.UTF-8`

- Fuseau horaire : `Europe/Paris`

- Utilisateur initial : `microlinux` (`Microlinux`)

- Groupes par défaut pour l'utilisateur initial :

  * `wheel`

  * `floppy`

  * `audio`

  * `video`

  * `cdrom`

  * `optical`

  * `kvm`

  * `xbuilder`

- Utiliser un terminal graphique pour le chargeur de démarrage : oui

- Partitionnement : `cfdisk`

BIOS/MBR :

```
  Device     Boot    Start       End   Sectors  Size Id Type
  /dev/sda1  *        2048   2099199   2097152    1G 83 Linux
  /dev/sda2        2099200  10487807   8388608    4G 82 Linux swap
  /dev/sda3       10487808 117231407 106743600 50.9G 83 Linux
```

BIOS/GPT :

```
  Device        Start       End   Sectors  Size Type
  /dev/sda1      2048      4095      2048    1M BIOS boot
  /dev/sda2      4096   2101247   2097152    1G Linux filesystem
  /dev/sda3   2101248  10489855   8388608    4G Linux swap
  /dev/sda4  10489856 117229567 106739712 50.9G Linux filesystem
```

UEFI/GPT :

```
  Device        Start       End   Sectors  Size Type
  /dev/sda1      2048    206847    204800  100M EFI System
  /dev/sda2    206848   2303999   2097152    1G Linux filesystem
  /dev/sda3   2304000  10692607   8388608    4G Linux swap
  /dev/sda4  10692608 117229567 106536960 50.8G Linux filesystem
```

