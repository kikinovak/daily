# Vagrant et KVM sous Rocky Linux 9

*Écrit le 16 février 2025*

Vagrant a besoin du *plugin* `vagrant-libvirt` pour pouvoir être utilisé avec
l'hyperviseur KVM. Dans ce cas il faut bien choisir la dernière version de
Vagrant avec laquelle ce *plugin* veut bien s'installer.

Une fois que le dépôt Hashicorp est activé, afficher les versions disponibles
de Vagrant:

```
# dnf --showduplicates list vagrant
Available Packages
vagrant.x86_64       2.2.9-1        hashicorp
vagrant.x86_64       2.2.10-1       hashicorp
vagrant.x86_64       2.2.10-2       hashicorp
vagrant.x86_64       2.2.10-3       hashicorp
vagrant.x86_64       2.2.10-4       hashicorp
vagrant.x86_64       2.2.11-1       hashicorp
vagrant.x86_64       2.2.12-1       hashicorp
vagrant.x86_64       2.2.13-1       hashicorp
vagrant.x86_64       2.2.14-1       hashicorp
vagrant.x86_64       2.2.15-1       hashicorp
vagrant.x86_64       2.2.16-1       hashicorp
vagrant.x86_64       2.2.17-1       hashicorp
vagrant.x86_64       2.2.18-1       hashicorp
vagrant.x86_64       2.2.19-1       hashicorp
vagrant.x86_64       2.3.0-1        hashicorp
vagrant.x86_64       2.3.1-1        hashicorp
vagrant.x86_64       2.3.2-1        hashicorp
vagrant.x86_64       2.3.3-1        hashicorp
vagrant.x86_64       2.3.4-1        hashicorp
vagrant.x86_64       2.3.6-1        hashicorp
vagrant.x86_64       2.3.7-1        hashicorp
vagrant.x86_64       2.4.0-1        hashicorp
vagrant.x86_64       2.4.1-1        hashicorp
vagrant.x86_64       2.4.2-1        hashicorp
vagrant.x86_64       2.4.3-1        hashicorp
```

> Le contenu du dépôt Hashicorp ne s'affiche pas dans un navigateur web. Il
> faut donc utiliser `dnf list`.

Installer la version qui va bien :

```
# dnf install vagrant-2.4.1-1
```

Construire les *plugins* dont on a besoin :

```
$ vagrant  plugin install vagrant-libvirt
Installing the 'vagrant-libvirt' plugin. This can take a few minutes...
Fetching xml-simple-1.1.9.gem
Fetching nokogiri-1.18.2-x86_64-linux-gnu.gem
Fetching ruby-libvirt-0.8.4.gem
Building native extensions. This could take a while...
Fetching formatador-1.1.0.gem
Fetching fog-core-2.5.0.gem
Fetching fog-xml-0.1.5.gem
Fetching fog-json-1.2.0.gem
Fetching fog-libvirt-0.13.2.gem
Fetching diffy-3.4.3.gem
Fetching vagrant-libvirt-0.12.2.gem
Installed the plugin 'vagrant-libvirt (0.12.2)'!

$ vagrant  plugin install vagrant-sshfs
Installing the 'vagrant-sshfs' plugin. This can take a few minutes...
Building native extensions. This could take a while...
Fetching win32-process-0.10.0.gem
Fetching vagrant-sshfs-1.3.7.gem
Installed the plugin 'vagrant-sshfs (1.3.7)'!

$ vagrant plugin list
vagrant-libvirt (0.12.2, global)
vagrant-sshfs (1.3.7, global
```

> Attention : la construction des *plugins* se fait en tant qu'utilisateur
> normal.

Pour éviter la mise à jour de `vagrant` il faudra ajouter la ligne suivante à
`/etc/yum.conf` :

```
exclude=vagrant
```

