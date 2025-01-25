# Mettre à jour /e/OS manuellement

*Écrit le 16 janvier 2025*

Télécharger le fichier d'installation personnalisé :

```
$ wget -c https://www.microlinux.fr/download/e-2.3-r-20250122-UNOFFICIAL-a5y17lte.zip
```

Relier le téléphone au PC avec un câble USB.

Activer les Options Dévelopeur : Paramètres > À propos du téléphone > Appuyer
sept fois sur le numéro de version.

Paramètres > Système > Paramètres avancés > Options pour les développeurs :

- [x] Débogage USB

Autoriser l'appareil dans la fenêtre qui s'affiche.

Vérifer que la commande `adb devices` affiche bien le téléphone branché :

```
$ adb devices
List of devices attached
5200c271fe96351d        device
```

Redémarrer dans TWRP :

```
$ adb reboot recovery
```

Une fois que TWRP s'affiche : Advanced > ADB Sideload > Swipe to Start Sideload

```
adb sideload e-2.3-r-20250122-UNOFFICIAL-a5y17lte.zip
```

Dans l'application App Lounge > Paramètres > déconnecter la session anonyme et
définir un compte Google bidon pour installer les applications.

