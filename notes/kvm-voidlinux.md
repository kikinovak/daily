# Virtualisation KVM sous Void Linux

*Écrit le 14 décembre 2024*


## Installation

Installer QEMU :

```
# xbps-install qemu
```

Installer Libvirt :

```
# xbps-install libvirt
```

Installer Virtual Machine Manager :

```
# xbps-install virt-manager
```


## Configuration

Activer les services :

```
# ln -s /etc/sv/libvirtd /var/service/
# ln -s /etc/sv/virtlockd /var/service/
# ln -s /etc/sv/virtlogd /var/service/
```

> Le paquet `dbus` doit être installé et le service correspondant activé.

Ajouter l'utilisateur au groupe système :

```
# usermod -aG libvirt kikinovak
```


## Mise en place d'un bridge

Le fichier `/etc/rc.local` peut être utilisé pour mettre en place un bridge
comme ceci par exemple :

```
ip link add name br0 type bridge
ip link set eno1 master br0
ip link set eno1 up
```

Dans la configuration par défaut, le client `dhcpcd` fonctionne sur toutes les
interfaces réseau. On va donc l'arrêter dans un premier temps :

```
# rm -f /var/service/dhcpcd
```

Ensuite on va se servir du *template* `/etc/sv/dhcpcd-eth0` pour définir un
service spécifique à l'interface `br0` :

```
# cd /etc/sv/
# cp -R dhcpcd-eth0/ dhcpcd-br0
# sed -i 's/eth0/br0/' /etc/sv/dhcpcd-br0/run
# ln -s /etc/sv/dhcpcd-br0 /var/service
```

Redémarrer :

```
# reboot
```

Si tout s'est bien passé, on dispose d'une interface `br0` avec une adresse IP.

