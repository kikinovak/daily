# Compiler /e/OS depuis les sources

*Écrit le 23 janvier 2025*

Prérequis :

- Docker

- 16 Go de RAM

- 400 Go de disque

Récupérer l'image Docker :

```
$ docker pull registry.gitlab.e.foundation:5000/e/os/docker-lineage-cicd:community
```

Brancher le téléphone :

```
$ adb devices
List of devices attached
5200c271fe96351d        device
```

Récupérer le code du modèle :

```
$ adb shell getprop ro.product.device
a5y17lte
```

Créer une série de répertoires :

```
$ sudo mkdir -pv /srv/e/{src,zip,logs,ccache}
mkdir: created directory '/srv/e'
mkdir: created directory '/srv/e/src'
mkdir: created directory '/srv/e/zip'
mkdir: created directory '/srv/e/logs'
mkdir: created directory '/srv/e/ccache'
```

> Certains smartphones nécessitent l'extraction d'un *firmware*, mais pas
> le Samsung SM-A520F.

Démarrer le *build* :

```
$ docker run --rm \
  -v "/srv/e/src:/srv/src" \
  -v "/srv/e/zips:/srv/zips" \
  -v "/srv/e/logs:/srv/logs" \
  -v "/srv/e/ccache:/srv/ccache" \
  -e "BRANCH_NAME=v2.3-r" \
  -e "DEVICE_LIST=a5y17lte" \
  -e "REPO=https://gitlab.e.foundation/e/os/releases.git" \
  registry.gitlab.e.foundation:5000/e/os/docker-lineage-cicd:community
```

Surveiller les *logs* pendant la compilation :

```
$ cd /srv/e/logs/a5y17lte/
$ tail -f eos-2.3-20250123-UNOFFICIAL-a5y17lte.log
```

Croiser les doigts :

```
>> [Thu Jan 23 09:03:28 UTC 2025] Finishing build for a5y17lte
>> [Thu Jan 23 09:03:28 UTC 2025] Cleaning source dir for device a5y17lte
09:03:53 Entire build directory removed.

#### build completed successfully (25 seconds) ####
```

Et voici le résultat final :

```
$ ls -lGh /srv/e/zips/a5y17lte/
total 950M
-rw-r--r--. 1 root 950M 23 janv. 10:03 e-2.3-r-20250123-UNOFFICIAL-a5y17lte.zip
-rw-r--r--. 1 root   75 23 janv. 10:03 e-2.3-r-20250123-UNOFFICIAL-a5y17lte.zip.md5sum
-rw-r--r--. 1 root  107 23 janv. 10:03 e-2.3-r-20250123-UNOFFICIAL-a5y17lte.zip.sha256sum
```

