# résumé en une page 


LINUX : BOOT vers l'init (premier process)


Bouton Marche (électrique ou assimilé cf VM)



CPU lance le BIOS (Basic Input or Output System)
* via le Bootsrap Processor (vs application processor)
* se rend au BIOS entrypoint (BIOS code POST)
* stocké dans la mémoire non volatile ROM (Read Only Memory)
* stocké sur la carte mère (mémoire flash sur OS moderne - upgrade)
* read only = non volatile (mémoire non perdue si arrêt électrique)
* configuration du BIOS stockées dans le CMOS de la carte mère
* mémoire volatile
* batterie du CMOS (Complementary metal-oxide-semiconductor)



LINUX : BOOT vers l'init (premier process)


BIOS - POST (Power On Self Test) : vérification du hardware




BIOS - Boot device : on lance quoi ?
* CD, network (PXE > DHCP > PXE > TFTP)...


BIOS - Master Boot Record (MBR 512B) = premier secteur d'amorçage
* table des partitions




LINUX : BOOT vers l'init (premier process)


BootLoader (GRUB - Grand Unified Boot loader)
* sélection du noyau


ls /boot/grub/
cat /boot/grub/grub.cfg
cat /etc/default/grub
ls /etc/grub.d/
#GRUB_BACKGROUND
sudo update-grub


Rq : GRUB_CMDLINE_LINUX_DEFAULT  | man bootparam


LINUX : BOOT vers l'init (premier process)


GRUB - Décompression (vmlinuz) et chargement en RAM du kernel + initramfs
* VM : prise en charge de la mémoire virtuelle
* Z : compresssion


ls /boot/
cat /usr/src/linux-headers-$(uname -r)/scripts/extract-vmlinux




LINUX : BOOT vers l'init (premier process)


Lancement du Kernel
* activation de la mémoire
* initialisation de page/table mémoire
* détection du CPU
* initialisation de la prise en compte des hardwares



initialisation des Filesystem



initramfs/initrd > montage du root FS > objectif l'init (systemd)
* PID 1 = init
* PID 0 = scheduler



LINUX : BOOT vers l'init (premier process)


Exécution de systemd /usr/bin/systemd
=> lancement de /usr/lib/systemd/system/*



Init historique (Premier Process) > systemd
* /lib/systemd/systemd
* nom du serveur
* timezone
* check disque (fsck)
* montage des filesystems
* suppression des vieux fichiers de /tmp
* configuration des interface réseau
* configuration de packet filter
* démarrage de démonds et éléments réseau



LINUX : BOOT vers l'init (premier process)


Run level
0 - arrêt
1 -	simple utilisateur (single)
2 - multi-utilisateurs sans réseau
3 - multi-utilisateurs avec réseau
5 - mode graphique
6 - redémarrage


runlevel




LINUX : Terminal vs Console vs Shell

TERMINAL


historiquement cela ressemblait à des machines à écrire



multiuser & échange input/output avec le système



c'est un device qui va utiliser un processus pour communiquer



connection avec identification (user/password, clef sécurisée...)



permet :
* afficher des lignes
* gestion des retour à la ligne
* CR : cariage return
* LF : line feed
* envoi d'instruction au process



LINUX : Terminal vs Console vs Shell


tty = terminal  > teletypewriter



exemple sur ubuntu ctrl + alt + 



avoir les caractéristiques de son terminal


who
stty -a
echo "toto" > /dev/tty1




reél terminal vs virtual terminal (émulateur)
* réel = premier terminal > console
* terminal virtuel = application (fait office de terminal)
* augmentation des possibilités (clones...)



input > 0  / output > 1

référence aux file descriptor (fd > stdin/stdout)





LINUX : Terminal vs Console vs Shell
CONSOLE


accès physique au terminal primaire



connexion avec des outils spécifiques en datacenter



pas besoin d'accès réseau
* dernier recours si perte de connexion réseau totale)
* connexion standard
* ou connexion via les outils construteurs (idrac Dell / ilo HP)
* intervention distante



LINUX : Terminal vs Console vs Shell
SHELL


shell vs kernel



interpréteur de commande via le terminal
* mode de communication



différents type de shell
* bourne shell (/bin/sh)
* bash (bourne again shell) (/bin/bash)
* z-shell (zsh)
* ...



permet des fonctions avancées
* pipe : communication inter-processus



prompt vs command


prompt : command (options) (arguments)


LINUX : Commandes & Hiérarchie du Système de Fichiers

Un standard


Système de Fichierss = Filesystem


Filesystem Hierarchy Standard (FHS) : standard Linux (version 3 datant 2015)


composé de fichiers et de répertoires


sur linux tout n'est que fichiers


repose sur le disque (prochaine vidéo) & un format (formater)




LINUX : Commandes & Hiérarchie du Système de Fichiers

Commandes pour débuter

lister les fichiers et les répertoires


ls



quelques options intéressantes


-a : liste tout y compris les fichiers cachés (commençant par .)
-l : format liste détaillée
-t : classer par date de modification
-r : inverser l'ordre de la date
-h : taille en format lisible pour un humain ;)
-1 : liste simple avec un élément par ligne


Note : et bien d'autres encore plus importantes (mais moins utilisées)


LINUX : Commandes & Hiérarchie du Système de Fichiers


changer de répertoire


cd



utilisation courante


/
~
..
.



afficher le répertoire courant


pwd



installer la commande tree (optionnel)


sudo apt update
sudo apt install tree




LINUX : Commandes & Hiérarchie du Système de Fichiers

LES REPERTOIRES


la racine ou le root directory


/




LINUX : Commandes & Hiérarchie du Système de Fichiers


le chargeur d'amorçage (vue dans la vidéo sur le boot)


/boot/




LINUX : Commandes & Hiérarchie du Système de Fichiers


les binaires de base & réservés aux administrateurs


/bin/
/sbin/




LINUX : Commandes & Hiérarchie du Système de Fichiers


les périphériques physiques ou virtuelles
* le stockage (hdd, ssd, cd, usb...)
* les terminaux (tty - cf vidéos précédentes)
* /dev/null, /dev/zero ou /dev/random
* ...


/dev/




LINUX : Commandes & Hiérarchie du Système de Fichiers


les fichiers de configuration


/etc/




LINUX : Commandes & Hiérarchie du Système de Fichiers


les home dédiées aux utilisateurs (vrais ou applicatifs)


/home/




LINUX : Commandes & Hiérarchie du Système de Fichiers


les librairies utilisées par les binaires ou applicatifs


/lib/




LINUX : Commandes & Hiérarchie du Système de Fichiers


les applis optionnelles (installées manuellement)


/opt/




LINUX : Commandes & Hiérarchie du Système de Fichiers


la home de l'utilisateur root


/root/




LINUX : Commandes & Hiérarchie du Système de Fichiers


autres répertoires de binaires non nécessaires au système
* Unix Système Resources


/usr/
/usr/bin/
/usr/lib/
/usr/share/
/usr/src/ > code source du noyau (non compilé)




LINUX : Commandes & Hiérarchie du Système de Fichiers


fichiers variables = données
* logs
* base de données
* journaux...


/var/
/var/log/
/var/lib/




LINUX : Commandes & Hiérarchie du Système de Fichiers


les fichiers temporaires (vidage)


/tmp/




LINUX : Commandes & Hiérarchie du Système de Fichiers


les pseudos filesystèmes & informations du noyau


/proc/
/sys/




LINUX : Commandes & Hiérarchie du Système de Fichiers


fichiers de récupérations pour le filesystem


lost+found




LINUX : Commandes & Hiérarchie du Système de Fichiers


les montage temporaires


/mnt/
/media/




LINUX : LE MAN & RTFM



la documentation formelle sur linux, ses commandes


disponible sur le terminal ou en ligne


différentes langues disponibles


utilisable via la commande



man
man man
h




LINUX : LE MAN & RTFM



Structure d'une page de man


nom : commande ou autre


copyright


résumé (synopsys)


description


options


Notes


Exemples


Auteurs de la commande


...





man man-pages




LINUX : LE MAN & RTFM

```
man -L fr man
```

découpé en section


    Programmes exécutables ou commandes de l'interpréteur de commandes (shell) 
    Appels système (Fonctions fournies par le noyau)
    Appels de bibliothèque (fonctions fournies par des bibliothèques)
    Fichiers spéciaux (situés généralement dans /dev)
    Formats des fichiers et conventions
    Jeux ;
    Divers (y compris les macropaquets et les conventions)
    Commandes de gestion du système (admin)
    Interface du noyau Linux.




LINUX : LE MAN & RTFM


chaque section dispose d'une intro


man 1 intro



comment chercher ?


man -k <recherche>
man -k swapoff
apropos <recherche>
man -K <recherche> 




LINUX : LE MAN & RTFM


recherche dans une page


\<mot>



n # next
N # previous
G # bas de page
g # haut de page


LINUX : Les commandes du débutant


un début pour les débutants... à compléter par la suite :)



ls : list directory/files
* -la
* -larth
* -R




tabulation ;)


ctrl + r : recherche




LINUX : Les commandes du débutant


pwd : print working directory



cd : change directory	(builtin commande - type > help)



cat : concatener et afficher le contenu de fichiers
* -n
* -A



LINUX : Les commandes du débutant


man : la documentation
* -k
* -L fr



LINUX : Les commandes du débutant


mkdir : make directory
* -p



rmdir : remove directory
* -p : a/b/c /!\



rm : remove fichiers, répertoires ou liens
* -r : récursive /!
* -f
* -i



LINUX : Les commandes du débutant



cp : copy
* -r
* -p
* -f


mv : move




touch : créer un fichier vide



date : date & heure du système



whoami : qui suis-je ?


