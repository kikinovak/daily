# Docker sous Void Linux

*Écrit le 15 décembre 2024*


## Installation

Installer Docker avec tous ses composants :

```
#xbps-install docker docker-compose docker-buildx
```

## Configuration

Activer le service :

```
# ln -s /etc/sv/docker /var/service/
```

Ajouter l'utilisateur au groupe système :

```
# usermod -aG docker kikinovak
```

Tester Docker :

```
$ docker version
Client:
 Version:           27.4.0
 API version:       1.47
 Go version:        go1.23.3
 Git commit:        tag v27.4.0
 Built:             Wed Dec 11 03:49:43 2024
 OS/Arch:           linux/amd64
 Context:           default

Server:
 Engine:
  Version:          27.4.0
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.23.3
  Git commit:       tag v27.4.0
  Built:            Fri Dec 13 06:38:32 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.7.17
  GitCommit:        UNSET
 runc:
  Version:          1.1.13
  GitCommit:
 docker-init:
  Version:          0.19.0
  GitCommit:
```

> Notons ici que contrairement à d'autres distributions, Docker sous Void Linux
> ne crée **pas** de conflits avec le bridge de KVM.
