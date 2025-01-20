# HPLIP sous Rocky Linux 9

*Écrit le 20 janvier 2025*

Installer HPLIP :

```
# dnf install -y hplip
```

> Le paquet `hplip` ne fournit plus d'interface graphique sous Rocky Linux 9.

Installer le plugin :

```
$ hp-plugin
```

Pour configurer une imprimante réseau, il suffit de fournir son adresse IP en
argument à `hp-setup` :

```
# hp-setup 192.168.2.252

HP Linux Imaging and Printing System (ver. 3.21.2)
Printer/Fax Setup Utility ver. 9.0

---------------------
| PRINT QUEUE SETUP |
---------------------

Please enter a name for this print queue 
(m=use model name:'OfficeJet_Pro_6970'*, q=quit) ?m
Using queue name: OfficeJet_Pro_6970
Locating PPD file... Please wait.

Found PPD file: drv:///hp/hpcups.drv/hp-officejet_pro_6970.ppd
Description: 

Does this PPD file appear to be the correct one (y=yes*, n=no, q=quit) ? y
Enter a location description for this printer (q=quit) ?Bureau
Enter additonal information or notes for this printer (q=quit) ?

Adding print queue to CUPS:
Device URI: hp:/net/OfficeJet_Pro_6970?ip=192.168.2.252
Queue name: OfficeJet_Pro_6970
PPD file: drv:///hp/hpcups.drv/hp-officejet_pro_6970.ppd
Location: Bureau
Information:

-------------------
| FAX QUEUE SETUP |
-------------------

Please enter a name for this fax queue 
(m=use model name:'OfficeJet_Pro_6970_fax'*, q=quit) ?q
OK, done.
```

À partir de là, on peut se connecter à l'interface de CUPS
(http://localhost:631) pour peaufiner la configuration et imprimer une page de
test.

