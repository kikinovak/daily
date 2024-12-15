# VirtualBox sous Void Linux

*Écrit le 15 décembre 2024*


## Installation

Installer VirtualBox :

```
# xbps-install virtualbox-ose
```


## Configuration

Ajouter l'utilisateur au groupe système :

```
# usermod -aG vboxusers kikinovak
```


## VirtualBox Extension Pack

Vérifier la version de VirtualBox :

```
$ xbps-query virtualbox-ose | grep pkgver
pkgver: virtualbox-ose-7.0.20_1
```

Télécharger le *VirtualBox Extension Pack* pour cette version : **Download** >
**VirtualBox older builds** (en bas à droite sur la page) > **VirtualBox 7.0**
> **VirtualBox 7.0.20** > **Extension Pack**.

Installer le *VirtualBox Extension Pack* :

```
# VBoxManage extpack install Oracle_VM_VirtualBox_*-extpack
...
Do you agree to these license terms and conditions (y/n)? y

License accepted. For batch installation add
--accept-license=33d7284dc4a0ece381196fda3cfe2ed0e1e8e7ed7f27b9a9ebc4ee22e24bd23c
to the VBoxManage command line.

0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
Successfully installed "Oracle VM VirtualBox Extension Pack".
```

Redémarrer :

```
# reboot
```

