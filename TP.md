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

LINUX : Permissions sur fichiers et répertoires


Comment lister les permissions (mode) sur des fichiers ou répertoires ?


ls -l
-rw-rw-r--  1 oki oki     0 avril  3 16:46 toto
drwxrwxr-x  2 oki oki  4096 mars   4 21:48 x-process

stat <fichier>
  File: toto
  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: fd01h/64769d	Inode: 8138908     Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/     oki)   Gid: ( 1000/     oki)

getfacl toto
# file: toto
# owner: oki
# group: oki
user::rw-
group::rw-
other::r--




LINUX : Permissions sur fichiers et répertoires

INTERPRETATION

-rw-rw-r--  1 oki oki     0 avril  3 16:46 toto
drwxrwxr-x  2 oki oki  4096 mars   4 21:48 x-process




1er caractère
d : directory
c : character device
l : symlink
p : named pipe
s : socket
b : block device
D : door

: file





LINUX : Permissions sur fichiers et répertoires

INTERPRETATION

-rw-rw-r--  1 oki oki     0 avril  3 16:46 toto
drwxrwxr-x  2 oki oki  4096 mars   4 21:48 x-process




par bloc de 3 : owner / group / other

  r : read
  w : write
  x : executable




notation en octal (cf stat):

  4 = read (r)
  2 = write (w)
  1 = executable (x)

  exemple : 765 ( rwx rw- r-x )






LINUX : Permissions sur fichiers et répertoires

COMMANDES DE MODIFICATION

changement de mode/permissions


chmod



	* options : -R et -c




changer le owner et le groupe


chgroup
chown




LINUX : L'édition avec Vi/Vim


ouverture d'un fichier


vi toto



mode ajout


a



mode insertion


i




LINUX : L'édition avec Vi/Vim


mode visuel


ctrl + v



mode normal


Esc



enregistrer


:w



enregistrer et quitter


:wq
:wq!




LINUX : L'édition avec Vi/Vim


première et dernière ligne (en mode normal)


gg
G



la recherche de caractères


/



la recherche d'une ligne


:<num_ligne>




LINUX : L'édition avec Vi/Vim


undo/redo


u
:undo
:redo



copier/coller une ligne


yy
p



copier coller plusieurs ligne


3yy
p




LINUX : L'édition avec Vi/Vim


copier/coller d'un numéro de ligne à un autre


:set number
11,35y
p



supprimer des lignes


dd
10dd



remplacer des caracères


:s///g
:%s///g

LINUX : Elevation de privilèges & su / sudo



sur notre VM on a créé deux utilisateurs :

  * xavki > user standard

  * root > administrateur (super)






LINUX : Elevation de privilèges & su / sudo

COMMANDE : SU (Switch User)

commande pour changer d'utilsateur ou jouer une commande


su



	* -c 

	* - : ouvre un shell dans l'environnement du user

	* -s : spécification d'un shell




su -c "whoami" root
su -c "ls /root/" - root
su -c "env" root




LINUX : Elevation de privilèges & su / sudo



su c'est bien mais :

  * tout ou rien : root sinon rien (ou droits peu facile et fins)

  * tout temps changer d'utilisateur

  * sécurité = éviter de disposer du user root






LINUX : Elevation de privilèges & su / sudo

COMMANDE : SUDO (Super User DO)

parfois nécessaire de l'installer (en tant que root)


apt update
apt install sudo
usermod -aG sudo xavki




permet :

  * lancer une commande en tan qu'un user (défaut root)

  * permet une gestion fine des droits (par commande, users, groupes...)




exemple :

sudo ls /root




LINUX : Elevation de privilèges & su / sudo


configuration


sudo cat /etc/sudoers
sudo visudo
sudo EDITOR=vim visudo
sudo -l
sudo -k
sudo -i



Defaults editor=/usr/bin/vim


 <sys_source> = (<qui_cible>) 
 <sys_source> = (<qui_cible>) , , 

xavki ALL = (ALL) ALL
xavki ALL = (ALL) NOPASSWD: /sbin/shutdown


Note : toujours garder une session de root ouverte à coté


LINUX : USERS & GROUPS


point important pour sysadmin/devops/sre
* indication sur la bonne gestion du parc



souvent automatisée par des outils (ansible, puppet...)



LINUX : USERS & GROUPS


UID/GID



* identifiants uniques




* UID : 
		* 0 pour root
		* 0 - 100 : mode statique pour le système
		* < 1000 : dynamique pour le système
		* > 1000 : autres
		* nobody : valeur max définie




LINUX : USERS & GROUPS


* GID :
		* pour les groupes
		* 0 pour le groupe root
		* 100 le groupe par défault (users)
		* groupe utilisateur à partir de 1000




LINUX : USERS & GROUPS

GROUPES



lister les groupes :


getent group


/etc/group






LINUX : USERS & GROUPS


ajouter un groupe :


groupadd



	* -g : forcer le GID

	* -r : groupe système



Note :

	* fichier de configuration de groupadd /etc/login.defs

	* changer des fichiers ou répertoires chgrp ou chown

	* si changement de GID pour un groupe : newgrp / groupmod




LINUX : USERS & GROUPS


supprimer un groupe :


groupdel




LINUX : USERS & GROUPS

USERS



différentes actions possibles :

  * useradd : ajout

  * userdel : suppression

  * usermod : modification






similaires à : adduser, deluser



LINUX : USERS & GROUPS



useradd :

  * /etc/default/useradd ou /etc/adduser.conf > configuration

  * -s : spécifier le shell

  * -c : commentaire

  * -d : localisation de la home

  * -g : le groupe de l'utilisateur

  * -G : les groupes additionnels

  * -k : localisation du squelette






LINUX : USERS & GROUPS


sudo useradd usertest
sudo useradd -c "Mon nom est personne"
-d /home/mydir -g usertest2 -G docker -m 
-s /usr/bin/sh


Note : account désactivé par défaut > définir le password

sudo passwd usertest
su - usertest




LINUX : USERS & GROUPS



comment lister les utilisateurs :

  * /etc/passwd

  * getent passwd

  * compgen -u






LINUX : USERS & GROUPS

Note :

	* si ajout/update de users en masse (bulk) : newusers					

	* autre option via adduser




LINUX : USERS & GROUPS



comment supprimer un utilisateur ?


userdel :

-r : suppression de la home



deluser :

  * --remove-home

  * --backup-to

  * --remove-all-files : attention








LINUX : USERS & GROUPS


générer un password


openssl rand -base64 12




LINUX : USERS & GROUPS



passwd la commande :

  	* changer le mot de passe d'un user (ou du sien)

  	* -e : force l'expiration (réinitialisation)

  	* -l : locker un user

  	* -n : minimum de jour entre les changements

  	* -u : unlock

  	* -x : maximum de validité

  	* -w : nombre de jour avant la demande de changement

  	* -S : statut (couplé à -a)



LINUX : ENVIRONNEMENT



tuto précédent : utilisateurs & permissions

  * /home/<user>

  * personnalisation par utilisateur (réel ou system)


=> Environnement & Scripts de démarrage
=> bien sûr tout cela s'enclenche à la connexion = login




LINUX : ENVIRONNEMENT



la commande login

  * man login (files...)

  * configuration /etc/login.defs (man !!)

  * deux types de interactive (remote ou su) / non interactive (script distant)

  * shell login vs non login (sh après auth)

  * ex : non login et non interactive = script lancé dans la CLI






LINUX : ENVIRONNEMENT



après lancement de login :

  * scripts (autocompletion etc)

  * source de certaines variables (variables d'environnement)







l'environnement :

  * commande env (man !!) : -i / ajout variable

  * commande export (help !!)






LINUX : ENVIRONNEMENT



cheminement des fichiers définissant l'environnement
* pour un interactive login ;)

  1- /etc/profile
  2- /etc/profile.d/*
  3- ~/profile ou ~/.bash_profile
  4- ~/.bashrc (exception)
  ...
  x- ~/.bash_logout


  LINUX : MOTD & ISSUE & LOGOUT



messages à l'utilisateur :

  * avant le login : issue

  * après login : motd
  		(Message Of The Day)

  * à la sortie : .bash_logout


=> "Man !!!"




LINUX : MOTD & ISSUE

ISSUE


prelogin message


attention aux informations affichées

  * sécurité

  * éviter les versions, noms de users, société...




fichier à éditer :



		/etc/issue




LINUX : MOTD & ISSUE

MOTD



postlogin message


fournir des infos à l'utilisateur (ex: environnement)




fichier à éditer


/etc/motd




LINUX : MOTD & ISSUE


script custom


/etc/profile.d/01-motd.sh
chmod +x /etc/profile.d/01-motd.sh



#!/usr/bin/bash
echo "Machine : "$(hostname)
echo "IP : "$(hostname -I)




supprimer pour un utilisateur


touch ~/.hushlogin



https://github.com/dylanaraps/neofetch


LINUX : MOTD & ISSUE


fichier à modifier


~/.bashrc_logout



exemple: compte à rebours


for i in {1..11};do
echo $((10-i))
sleep 1s
done


LINUX : UMASK & SKEL ??



suite des vidéos sur les permissions et l'environnement


d'où viennent :
* fichiers de la HOME
* ~/.profile
* ~/.bashrc




LINUX : UMASK & SKEL ??

SKELETON



répertoire modèle


définit dans la configuration de useradd /etc/default/useradd


/etc/skel par défaut


attention à bien maintenir les permissions/droits


uniquement pour les nouveaux utilisateurs




LINUX : UMASK & SKEL ??

UMASK



rappel : rwx rwx rwx

  * 4 : r

  * 2 : w

  * 1 : x

  ex: 

  	* 7 : rwx

  	* 6 : r-w

  	* 5 : r-x






LINUX : UMASK & SKEL ??



les permissions appliquées par défaut :

  * 666 : fichiers

  * 777 : répertoires




mais pourtant ? à la création les droits sont différents


définit dans l'environnement




LINUX : UMASK & SKEL ??



on reprend notre cheminement à partir du login > au bash.rc

  /etc/login.defs
  /etc/profile
  /etc/profile.d/*
  /etc/bash.bashrc
  ~/.profile
  ~/.bash_profile
  ~/.bashrc






umask 002
umask u=#,g=#,o=#



LINUX : DATE & TIME


date / heure : élément crucial
* logs
* systèmes distribués
* différents calculs
* gettimeoftheday
* tellement important
* NTP/PTP



LINUX : DATE & TIME


notion de format / localisation
* yyyy/mm/dd...
* CEST : Central European Summer Time
* UTC : Universal Time Coordinated
* RTC : Real Time Clock



LINUX : DATE & TIME



format epoch = nb secondes depuis 01/01/1970 00:00:00
* problématique du 32bits en 2038 ;)
* vive le 64bits



temps de la machine VS temps du système
* machine : horloge RTC / bios / pile...
* système : prise en compte des fuseaux horaires...



LINUX : DATE & TIME

DATE/HEURE

commande pour le système


date
timedatectl




spécification de format


date +%Y%m%d
date +%Y%m%d-%H:%M:%S
date +%T.%N




LINUX : DATE & TIME

MACHINE


commande : hwclock


réglage commande ou bios


afficher l'heure



sudo hwclock --show




LINUX : DATE & TIME



pour changer


sudo hwclock --set --date "13 Jan 2022 20:08" --utc




synchroniser matériel et système


sudo hwclock --systohc


et inversement

sudo hwclock --hctosys




LINUX : DATE & TIME

TIMEZONE

vérifier la timezone du système


cat /etc/timezone
timedatectl
date +%Z  #%z
ls -la /etc/localtime




changer de timezone (2 méthodes)


timedatectl list-timezones
timedatectl set-timezone 

sudo rm -rf /etc/localtime
sudo ln -s /usr/share/zoneinfo/America/New_York /etc/localtime




LINUX : DATE & TIME

DATE & HEURE

changer ou définir la date et l'heure


timedatectl set-time "2022-01-01 00:00:01"
timedateclt set-date "2022-02-01"
timedatectl set-time "00:30:01"




ou avec date


date -s HH:MM:SS
date -s MM/JJ/AAAA




LINUX : DATE & TIME

NTP SERVICE

timedatectl status
timedatectl timesync-status
timedatectl show-timesync


LINUX : LES LOCALES

Les spécificités des localisations :

	* format de la date et heures

	* premier jour de la semaine

	* la monnaie

	* le séparateur numérique (milliers)

	...

	=> Les Locales




LINUX : LES LOCALES

Comment trouver les locales ?

	* /etc/default/locale

	* commande : localectl

	* commande : locale

	* fr_FR.utf8 = langue.encodage


Les valeurs :

localectl list-locales
locale -a




LINUX : LES LOCALES

Liste des principales locales :

	* LANG : valeur si non défini dans "LC_*"

	* LANGUAGE : définition de valeurs utilisables par défaut
				* classé par ordre séparé de ":"

	* LC_TIME : format des heures et des dates

	* LC_COLLATE : classement lors de tris ou regexp

	* LC_ALL : surcharge toutes les autres locales

	* LC_NUMERIC : format numérique

	* LC_MESSAGES : langues des mots et réponses

	* LC_PAPER : format du papier

	* LC_MONETARY : format monétaire

	* LC_TELEPHONE / LC_ADDRESS / LC_MEASUREMENT / LC_NAME




LINUX : LES LOCALES

Détail sur une locale :

locale -k LC_TIME
locale -k LC_PAPER



Commandes à retenir :

man locale
man localectl
man update-locale




LINUX : LES LOCALES

Mise à jour :

sudo update-locale LC_PAPER=en_US.UTF-8
sudo localectl set-locale LC_PAPER=en_US.UTF-8



Spécifique pour un utilisateur :

~/.bashrc
export LC_ALL=en_US.UTF-8




LINUX : LES LOCALES

Et un peu plus...

pour la définition du clavier


# sur console
sudo loadkeys fr
ou
setxkbmap us
setxkbmap fr


LINUX : Type de Fichiers

Types :

	* Fichier standard  (-)

	* Directory/Répertoire (d)

	* Hard link (-)

	* Symbolic link (l)

	* Character/Block device (c) (b)

	* Local domain socket (s)

	* Named pipe (p)




LINUX : Type de Fichiers

FICHIER

	* assemblage cohérent de Bytes

	* tout est fichier sur linux

	* texte, vidéos, musiques, images, données...



déterminer le type de contenu :


touch <fichier>
vim <fichier>
...
file <fichier>
stat <fichier>




LINUX : Type de Fichiers

DIRECTORY

	* un fichier permettant de regrouper d'autres fichiers

	* "." / ".."



mkdir <répertoire>
rmdir <répertoire>
rm -r <répertoire>
...
stat <répertoire>




LINUX : Type de Fichiers

HARD LINK (link)

	* différents des symbolic links (symlink)

	* lien vers l'inode : adresse du contenu du fichier
			* hard links = même adresse

	* sur des fichiers ou des directory



ln <source> <dest>
rm <link>
ls -i 
stat <link>




LINUX : Type de Fichiers

SOFT LINK (symlink)

	* différents des hard links (links)

	* ne pointe pas vers le même inode (adresse)

	* sur des fichiers ou directory



ln <source> <dest>
rm <link>
ls -i 
stat <link>




LINUX : Type de Fichiers

CHARACTER/BLOCK DEVICES

	* devices (https://en.wikipedia.org/wiki/Device_file) 

	* device file = interface avec un driver (disks, mémoire...)

	* character = 
			* accessible directement sans tampon (buffer/cache)
			* caractère par caractère
			* ex : terminal, imprimantes...

	* block = 
			* accessible via un tampon (cache)
			* envoi/lecture par block (routine de cache)
			* ex : la mémoire, les disques...
			
	* device file = interface avec un driver (disks, mémoire...)


https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/admin-guide/devices.txt

mknod xavki_c_device c 100 1
mknod xavki_b_device b 100 1




LINUX : Type de Fichiers

LOCAL DOMAIN SOCKET

	* socket = connexion entre processus (process)

	* socket interne et socker réseau (connexion réseau)

	* créé via un syscall (fonction système) spécifique "socket()"



man 2 socket




LINUX : Type de Fichiers

NAMED PIPE (FIFO)

	* similaire à un pipe (communication entre process)

	* "pipe" = anonymous pipe "|"

	* "named" pipe = un fichier

	* sans stockage de la donnée



mknode xavki_named_pipe p
mkfifo xavki_fifo


LINUX : Copie / Déplacement / Compression de répertoires

3 commandes importantes pour agir sur les répertoires :

	* cp

	* mv

	* tar




LINUX : Copie / Déplacement / Compression de répertoires

CP

copie de fichiers


cp <source> <destination>
cp <source1> <source2> <destination>




copie de répertoires


cp -r <source> <destination>




avec confirmation


cp -ri <source> <destination>




LINUX : Copie / Déplacement / Compression de répertoires


avec backup si on écrase


cp -b toto.txt titi.txt




si pas les permissions d'écriture
sur le fichier de destination


cp -f toto.txt titi.txt




préserver les droits et owner/group


cp -p toto.txt titi.txt




LINUX : Copie / Déplacement / Compression de répertoires

MOVE



déplacer/renommer fichiers et répertoires


avec confirmation



mv -i rep1 rep2




ne pas écraser un fichier existant


mv -n file1.txt rep2/




LINUX : Copie / Déplacement / Compression de répertoires


écraser si plus récent


mv -u file1.txt rep2/




créer un backup de la destination si existante


mv -b file1.txt file2.txt




LINUX : Copie / Déplacement / Compression de répertoires

COMPRESSION/REGROUPEMENT



créer un tarball et souvent gzipper


avec tar (existe d'autres solution zip...)




créer une tarball


tar -cf mytarball.tar mydir/
tar -cvf mytarball.tar mydir/



extraction


tar xvf mytar.tar




avec compression/décompression


tar -czvf mytarball.tar.gz mydir/
tar -xzvf mytar.tar.gz




LINUX : Copie / Déplacement / Compression de répertoires


en format bz plus compressé


tar -cjvf mytarball.tar.bz2 mydir/
tar -xjvf mytar.tar.bz2




juste lister le contenu et sa structure


tar -tvf mytar.tar.gz




LINUX : Copie / Déplacement / Compression de répertoires


extraite juste un, des fichiers ou pattern


tar -xzvf mytar.tar.gz mydir/toto.txt
tar -xzvf mytar.tar.gz mydir/toto.txt --wildcards "\*.txt"




ajouter juste un fichier


tar -rvf mytar.tar.gz file1.txt


LINUX : Inodes & caractéristiques d'un fichier



vidéo précédente => différents types de fichiers


commande stat





options :

  -f : filesytème du fichier

  -L : suivre les liens symboliques (symlink)






stat sortie (output)


  File: toto.txt
  Size: 5         	Blocks: 8          IO Block: 4096   regular file
Device: fd01h/64769d	Inode: 8165659     Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/     oki)   Gid: ( 1000/     oki)
Access: 2022-04-15 07:42:40.323132281 +0200
Modify: 2022-04-15 07:42:40.323132281 +0200
Change: 2022-04-15 07:42:40.323132281 +0200
 Birth: -




LINUX : Inodes & caractéristiques d'un fichier

INFORMATIONS

	* File : le nom du fichier (où la représentation du symlink)
	* Size : taille en bytes
	* Block : nombre de blocks alloués
	* IO Block : taille de chaque block
	* type de fichier
	* Device : le numéro de device
	* Inode : numéro d'inode
	* Links : nombre de hard links
	* Access : permissions symbol et octal
	* UID / GID
	* Access : dernière date d'accès
	* Modify : date de la dernière modification du contenu
	* Change : date de changement du contenu et des attributs
	* Birth : non utilisé sous linux




LINUX : Inodes & caractéristiques d'un fichier

NOTION DE BLOCK


	* un filesystème est découpé en morceaux = blocks

	* chaque block device dispose d'une taille de blocks




lsblk




	* plusieurs niveaux de blocks
			* disk block size (disque) ~ 512
			* data block size (filesystème) ~ 4096 (4k)



	Block Disk > Block FileSystem > Fichiers... ou blocks applicatifs




	* si un block FS à une taille de 4096 bytes et un fichier 8 bytes
			* => utilisation de 4096 bytes




LINUX : Inodes & caractéristiques d'un fichier


nombre de blocks par device


cat /proc/partitions
cat /sys/block/nvme0n1/queue/physical_block_size 
cat /sys/block/nvme0n1/queue/logical_block_size 




LINUX : Inodes & caractéristiques d'un fichier

ou

sudo fdisk -l /dev/nvme0n1
Disk /dev/nvme0n1: 476,96 GiB, 512110190592 bytes, 1000215216 sectors
Disk model: LENSE30512GMSP34MEAT3TA                 
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes




LINUX : Inodes & caractéristiques d'un fichier



choix de la taille des blocks

  * petits fichiers = block size plus petits (mais perte lié aux méta-données)

  * gros fichiers = large block (mais si petits fichiers = perte)

  * trop de blocks = dépasser la limite gérable par le system




les inodes sont des pointeurs vers les data blocks
* inodes = noeuds d'index




LINUX : Inodes & caractéristiques d'un fichier

NOTION INODES

	* pointeurs vers les data blocks

	* diposent de metadatas :
			* device du fichier
			* le numéro d'inode (unique dur sur un filesystem)
			* type de fichier et mode
			* GID/UID
			* nombre de hard links

	* taille du fichier

	* nombre de blocks

	* atime : dernier accès

	* mtime : date de modification du contenu

	* ctime : date de changement du contenu et des attributs




LINUX : Inodes & caractéristiques d'un fichier

PROCESS DE LECTURE D'UN FICHIER


1 - lire l'inode




2 - trouver l'inode dans la table des inodes




3 - lire les informations de l'inode




4 - récupération de la localisation des blocks
			* block début/fin ou début/taille




5 - lecture des datas blocks



LINUX : Montage d'un disque sans partitionnement


généralement on utilise à minima du partitionnement



peut être pratique (migration de serveur...)




inconvénients :

  * pas d'isolation (si le disque est plein perte VM)

  * exemple : base de données, risque sécu sur /tmp, logs...

  * partition : cas d'utilisation pour les dual boot (windows/linux...)






LINUX : Montage d'un disque sans partitionnement

SUR VIRTUALBOX



création du disque


ajout du disque




lister les disques


sudo fdisk -l




formater le disque


sudo mkfs.ext4 /dev/sdb




LINUX : Montage d'un disque sans partitionnement


le monter temporairement


sudo mkdir /srv/xavki
sudo mount -t ext4 /dev/sdb /srv/xavki
df




LINUX : Montage d'un disque sans partitionnement

DF

* disk free

* information sur l'utilisation des filesystems

* la consommation des inodes

* les montages actifs sur le système

* page Wikipédia : https://fr.wikipedia.org/wiki/Df\_(Unix)




LINUX : Montage d'un disque sans partitionnement


* colonnes :

	* Filesystem : devices des filesystems

	* 1k-block : taille en block de 1Kb

	* Used : taille utilisée

	* Available : taille disponible

	* Use% : utilisation en pourcentage

	* Mounted on : où le device est monté sur FHS




LINUX : Montage d'un disque sans partitionnement


* options

	* -a : affiche tous les montages

	* -h : format de taille humain

	* -i : consommation en inodes

	* --total : dernière ligne (tail -1)

	* -T : type de filesystem

	* -t <ext4> : un type de filesystem

	* -x <tmpfs> : exclure un type de filesystem




LINUX : Montage d'un disque sans partitionnement


si persistence


cat /etc/fstab
/dev/sdb  /srv/xavki  ext4  defaults  0 0




LINUX : Montage d'un disque sans partitionnement


si démontage


sudo umount /dev/sdb
ou
sudo umount /srv/xavki




retirer le disque de la VM



l'ajouter à une autre VM



le monter sur l'autre VM


sudo mkdir /tmp/xavki
sudo mount -t ext4 /dev/sdb /tmp/xavki



informations sur le filesystem


sudo dumpe2fs -h /dev/sdb


LINUX : DD

COPIE :

	* devices

	* partitions ou volume logique

	* disque ou zones de disque

	* local ou distant (combinaison avec ssh)




LINUX : DD


copie de disk à disk


dd if=/dev/sdb of=/dev/sdc
dd if=/dev/sdb of=/dev/sdc status=progress




LINUX : DD


copie en format image (copie sur cd ou usb)


dd if=/dev/sdb of=myimage.img




LINUX : DD


restauration


dd if=myimage.img of=/dev/sdc




LINUX : DD


nettoyer


dd if=/dev/zero of=/dev/sdc
dd if=/dev/random of=/dev/sdc


LINUX : Mount & Le fichier FSTAB

Trouver les montages :

	* mount 

	* /etc/fstab

	* /etc/mtab : fstab + commande mount


Les options sont utilisables pour mount ou fstab


LINUX : Mount & Le fichier FSTAB


montage dans fstab


<filesystème> <montage> <typeFS> <options> <dump> <pass>
/dev/sdb   		 /srv/xavki   ext4  defaults  0  0
UUID=xxxxxx    /srv/xavki   ext4  defaults  0  0
#NAS
//192.168.7.12/rep_a_partager   /srv/xavki   ext4  defaults  0  0
#NFS
10.10.0.10:/backups /var/backups  nfs      defaults    0       0




LINUX : Mount & Le fichier FSTAB


liste des UUID


sudo blkid
sudo lsblk -fe7




LINUX : Mount & Le fichier FSTAB



quelques options courantes :

  * filesystème : disque, UUID, partition, volume logique, label

  * montage : localisation dans le FSH (Filesystem Hierarchie)

  * type de FS : ext2, ext3, ex4, xfs, btrfs, ntfs, swap...

  * dump : jamais utilisé

  * pass : 0 (rien) / 1 (avant 2) / 2 (ordre de priorité) par fsck






LINUX : Mount & Le fichier FSTAB


	* options : du montage 

			* defaults : rw,exec,auto,suid,dev,nouser,async
			* rw/ro : lecture écriture ou readonly
			* exec/noexec : permet l'exécution ou non de binaires
			* auto/noauto : monté au boot/reboot ou mount -a
			* nofail (important) : permet le boot même sans le device
			* discard : spécifique ssd (activation du trim ~ amélioration durée/perf)
			* sync/async : i/o réalisé en synchrone ou asynchrone
			* suid/nosuid : autorise les actions sur les bits suid/sgid
			* noatime/relatime : mettre à jour ou pas la date accès à l'inode
			* user/nouser : les user ou seul root peuvent monter le FS
			* _netdev : device accessible par réseau (besoin du réseau avant de monter)
			* uid= / gid= : spécification des users si hors linux (équivalence, default root)




LINUX : Mount & Le fichier FSTAB


je suis à la porte... suppression du volume


init=/bin/bash
mount -no remount,rw /
#nano ... ajout nofail
#passwd root
exec /sbin/init




LINUX : Mount & Le fichier FSTAB


le mount bind ou comment monter un rep/fichier dans un autre ?


/home/linux/bon-fichier   /mnt/read-only/mauvais-fichier     none       bind      0   0


ou

sudo mount --bind /srv/xavki test/


astuce :

findmnt



toutes les options sont utilisables via mount (test et validation avant le fstab)


LINUX : Première PARTITION

Partitions :

	* devices

	* découpage d'un disque en sous éléments

	* isolation et espace dédié (différents FS, OS, montages...)

	* peut être redimensionnée (attenion quand même)




LINUX : Première PARTITION

Procédure simplifiée :


1 - ajouter un disque




2 - rechercher le disk : fdisk -l




3 - Lancer fdisk sur /dev/<disk>




4 - n pour créer une partition




LINUX : Première PARTITION

4 primaire + étendues
primaire = partitions dans le MBR du disque (découverte au boot)
étendue = fractionnement d'une partition primaire (conteneur)


5 - p pour une partition primaire




6 - t pour définir le type (linux = 83)




7 - w enregistrer




8 - cat /proc/partition partx /dev/<partition>




9 - install xfsprogs

10 - mkfs.xfs /dev/<partition>

11 - création dir & montage


LINUX : EXT4 vs XFS vs BTRFS vs ZFS


Disque > block> système d'exploitation > filesystème




Journalisation : enregistrement des modifications (datas/metadatas)
				* utile en cas de crash	




Delayed allocation : les données sont stockées dans un buffer/tampon
				* avant d'être écrites sur les data blocks
				* permet de temporiser pour réduire la fragmentation...




LINUX : EXT4 vs XFS vs BTRFS vs ZFS

EXT4


* Exemple :

	Disque = Boot Block + Block Group + .... + Block Group




	Block Group = x blocks




	Block Group = 
			* Super Block (1) : infos du filesystème (nb blocks...)
			* Group Descriptor(x) : localisation des bitmap et table inodes
			* Data Block Bitmap (1) : carte de blocks dédiés aux blocks
			* Inode Bitmap (1) : carte des blocks dédiés aux inodes
			* Inode Table (n) : metadatas et données des fichiers
			* Data Block (n) : données




	Ex : Directory > Inode > X data blocks




LINUX : EXT4 vs XFS vs BTRFS vs ZFS


* https://ext4.wiki.kernel.org/index.php/Main_Page

* 4ème version des filesystem étendus

* à partir du kernel 2.6.19

* taille maximum d'un fichier 16TB

* taille maxi du filesystem 1EB

* nombre maximum de sous répertoire 64000

* compatibilité de ext3 avec ext4




LINUX : EXT4 vs XFS vs BTRFS vs ZFS


* défragmentation à chaud (sans démonter le disque) e4defrag

* multi-block allocation = amélioration lecture/écriture

* retarde allocation des blocks (avant de flusher sur disk)  
	* basée sur les extents
	* allocation plus rapide pour les fichiers
	* autres FS : allocation immédiate (même si la donnée va en cache)

* journal checksum : éviter la corruption de fichier
	(si activation réduction de la performance)

* vitesse de fsck améliorée

* timestamp en nanoseconde

* désactivation de la journalisation possible




LINUX : EXT4 vs XFS vs BTRFS vs ZFS

XFS


* adapté aux gros volumes de données et gros fichiers/répertoires

* default sur les os RedHat

* haute performance de lecture et d'écriture

* allocation groupe ~ block groupes : mais plus gros que BG

* allocation groupe fonctionnement similaire à un filesystème
		* permet la paraléllisation et la scalabilité

* journalisation des metadatas : amélioration de la consistence




LINUX : EXT4 vs XFS vs BTRFS vs ZFS


* défragmentation à chaud

* redimensionnement à chaud

* direct I/O : bypass le cache du kernel dédié aux fichiers 
		* moins de CPU

* delayed allocation amélioration des performances : 
	* quand la donnée est arrivée sur disque
	* réduction de la fragmentation

* quota et journalisation (en cas de crash)

* extension des attibuts par fichier

* taille maximum du filesystem 8EB




LINUX : EXT4 vs XFS vs BTRFS vs ZFS

BTRFS

* https://btrfs.readthedocs.io/en/latest/

* maximum filesystem 16EB

* maximum fichier 16EB

* adapté pour les nombreux petits fichiers

* allocation dynamique des inodes

* permet de réaliser du RAID strippé, mirroré ou les deux

* compression, lecture et écriture des snapshots (incrémental)




LINUX : EXT4 vs XFS vs BTRFS vs ZFS


* COW : copy on write 

* future de ext4

* disques > storage pool > volumes (partitions) > filesystems

* réalisation de snapshots

* compression (zlib)

* compatible SSD (trim...)

* défragmentation à chaud




LINUX : EXT4 vs XFS vs BTRFS vs ZFS

ZFS

* maximum filesystem 1ZB

* volume manager + filesystem

* maximum fichier 16 EM

* multiple disques = pool de stockage > filesystems

* ajout facile de disques poru être pris en compte par le pool

* cow : copy on write (on n'écrase jamais la donnée)

* snapshots du filesystem

* RAID-Z : amélioration de l'intégrité de la data



LINUX : LVM - Introduction

LVM : Logical Volume Manager

man 8 LVM



Intérêts LVM :

	* partitionnement limité sur la gestion des secteurs

	* partitionnement risqué

	* partiionnement difficile si plusieurs disques (cumul)

	* LVM apporte un moyen snapshot (hormis certains FS)

	* LVM apport un moyen de stripper ( parallélisation des écritures)

	* LVM ne résoud pas la haute dispo des disques (niveau Raid)




LINUX : LVM - Introduction

SANS

Disk > partitions > filesystem


 
AVEC

Disk > Physical Volumes > Volume Groups > Logical Volumes > FS


ou

Disk > partitions > PV > VG > LV > FS



ATTENTION :
Type de partition à passer de Linux (83) en Linux LVM (8e)


LINUX : LVM - Introduction

PHYSICAL VOLUME (PV)

* représentation d'un disque physique, d'une partition, d'un volume RAID, baie SAN

* une sort de déclaration des disk utilisable


Principales commandes :

* pvcreate: création d'un PV
* pvdisplay ou pvs : afficher la liste des PV
* pvremove : supprimer un PV
* pvresize : redimensionner un PV
* pvscan : lister les disques pour les PV




LINUX : LVM - Introduction

VOLUME GROUPE (VG)

* couche logique contenant à minima 1 PV

* permet d'agréger les PV 

* utilisable via les volumes logiques (découpage...)


Principales commandes :

* vgcreate : créer un volume groupe
* vgdisplay ou vgs : lister les VG
* vgremove : supprimer un VG
* vgreduce : pour réduire la taille des VG
* vgrename : pour changer le nom d'un VG
* vgconvert : changer les metadatas
* vgextend : ajouter un PV à un VG existant
* vgsplit : couper en 2 un VG
* vgmerge : regrouper 2 VG en un
* vgscan : lister les disques d'un LV




LINUX : LVM - Introduction

LOGICAL VOLUME (LV)

* un à plusieurs LV par VG

* un LV est utilisable pour un filesystem (volume)

* fonctionnalités avancées : stripping, taille de blocs, snapshots...


Principales commandes :

* lvcreate: créer un volume logique (snapshot, stripping...)
* lvdisplay ou lvs : afficher les information d'un ou des LV
* lvremove : supprimer un LV
* lvextend : agrandir un LV
* lvconvert : pour restaurer un snapshot ou convertir
* lvresize : redimensionner un LV
* lvreduce : pour réduire la taille d'un LV
* lvscan : scanner tous les disques d'un LV


LINUX : LVM - Premier Volume Logique


Disks/Partitions > PV > VG > LV > Volumes FS



Exemple :

* ajout de 2 disques 1G

* monter un /srv/xavki de 1,5G

* monter un /srv/demo de 200M




LINUX : LVM - Premier Volume Logique

1- création et ajout des disques sur virtualbox
2- partitionnement des disques
3- création des physical volumes (PV)

pvcreate /dev/sdb1 /dev/sdc1
pvdisplay




LINUX : LVM - Premier Volume Logique

4- création d'un volume unique vg_data

vgcreate vg_data /dev/sdb1 /dev/sdc1
vgdisplay


5- création des volumes logiques lv_xavki & lv_demo

lvcreate -n lv_xavki -L 1.5G vg_data
lvcreate -n lv_demo -L 200M vg_data




LINUX : LVM - Premier Volume Logique

6- formatons le FS

mkfs.ext4 /dev/vg_data/lv_xavki
mkfs.ext4 /dev/vg_data/lv_demo


7- montage des volumes

mkdir /srv/{xavki,demo}



/dev/vg_data/lv_xavki  /srv/xavki ext4 nofail 0 0
/dev/vg_data/lv_demo  /srv/demo ext4 nofail 0 0

mount -a
df -h


LINUX : LVM - Etendre un volume logique & ajout de disque


Disks/Partitions > PV > VG > LV > Volumes FS




Remplissons un volume


df -h
fallocate -l 1500M /srv/xavki
df -h




LINUX : LVM - Etendre un volume logique & ajout de disque


vérifions si il reste l'espace allouable au niveau du VG


vgs
vgdisplay vg_data
lvextend -L +300M /dev/vg_data/lv_xavki
df -h




redimensionnons le filesystem (ext4)


resize2fs /dev/vg_data/lv_xavki
df -h




LINUX : LVM - Etendre un volume logique & ajout de disque


et si on remplit de nouveau ??


fallocate -l 1500M /srv/xavki




ajoutons un nouveau disque


pvcreate /dev/sdd1
vgextend vg_data /dev/sdd1
vgs
vgdisplay vg_data
lvextend -l +50%FREE /dev/vg_data/lv_xavki
lvextend -l +100%FREE /dev/vg_data/lv_demo
resize2fs /dev/vg_data/lv_xavki
resize2fs /dev/vg_data/lv_demo



LINUX : LVM - Réduire un volume logique


Disks/Partitions > PV > VG > LV > Volumes FS




lvs
lvdisplay




démonter le volume en question


umount /srv/demo




LINUX : LVM - Réduire un volume logique


réaliser un fsck


e2fsck -f /dev/vg_data/lv_demo




réduire le filesystème à la taille souhaitée


resize2fs /dev/vg_data/lv_demo 100M




LINUX : LVM - Réduire un volume logique


réduire le LV et resize


lvreduce -L 100M /dev/vg_data/lv_demo
resize2fs /dev/vg_data/lv_demo
mount /srv/demo
vgs

LINUX : LVM - Créer et restaurer un Snapshot


Disk > Partitions > PV > VG > LV > Volume FS




créer un snapshot de LV


touch /srv/xavki/demo1.txt
lvcreate -L 1G -s -n snap_lv_data /dev/vg_data/lv_xavki
sudo lvdisplay
# lvs
touch /srv/xavki/demo2.txt


Note : attention au volume libre du VG


LINUX : LVM - Créer et restaurer un Snapshot


on peut vérifier


sudo mount /dev/vg_data/snap_lv_data /mnt/snap_check
ls /mnt/snap_check
sudo umount /mnt/snap_check




vérifier la taille utilisée


sudo lvs /dev/vg_data/snap_lv_data




LINUX : LVM - Créer et restaurer un Snapshot



attention ne pas atteindre les 100% sinon plus de snap


étendre un snapshot manuellement



lvextend -L +100M /dev/vg_data/snap_lv_data




LINUX : LVM - Créer et restaurer un Snapshot


activer l'extension automatique des snapshots


vim /etc/lvm/lvm.conf
snapshot_autoextend_threshold = 100
# Setting this to 100 disables automatic extension
snapshot_autoextend_percent = 20




LINUX : LVM - Créer et restaurer un Snapshot


restauration du snapshot


lvconvert --merge /dev/vg_data/snap_lv_data
ls /srv/xavki/
# parfois  lvchange -an et lvchange -ay



LINUX : LVM - LV strippé


Disk > Partitions > PV > VG > LV > Volume FS



Intérêts ?

	* RAID 0

	* agrégation de disque en répartissant l'écriture/lecture

	* performance (cumul iops)




LINUX : LVM - LV strippé


création des PV (physical volumes) - ex 2 partitions


pvcreate /dev/sd[b-c]1




LINUX : LVM - LV strippé


création du volume group


vgcreate -v vg_data /dev/sd[b-c]1




LINUX : LVM - LV strippé


création du LV strippé


lvcreate -L 1G -n lv_strip -i 2 -I 4k /dev/vg_data
lvdisplay -m /dev/vg_data/lv_strip
lvs -o +devices
dmsetup table




LINUX : LVM - LV strippé


puis montage


mkfs.ext4 /dev/vg_data/lv_strip
mount -t ext4 /dev/vg_data/lv_strip /srv/xavki




test


dd if=/dev/zero of=/srv/xavki/test.txt bs=1G count=1 oflag=direct



LINUX : LVM - Remplacer un disque



avant :
/dev/sdb1 > pv > vg > lv > volume fs





après
/dev/sdc1 > pv > vg > lv > volume fs


Exemple : remplacement d'un disque


LINUX : LVM - Remplacer un disque


Ajout d'un disque



création de la partition (optionnelle)



création du PV du nouveau disque



LINUX : LVM - Remplacer un disque


ajout du nouveau PV au VG existant


pvextend vg_data /dev/sdc1




démonter le volume


umount /srv/xavki
# si possible faire un backup




LINUX : LVM - Remplacer un disque


déplacement des extends de l'ancien PV vers les autres PV (nouveau)


pvmove /dev/sdb1
pvmove /dev/sdb1 /dev/sdc1




retirer l'ancien PV du VG


vgreduce vg_data /dev/sdb1




remonter


mount -t ext4 /dev/vg_data/lv_xavki /srv/xavki



LINUX : LVM - Comment mirrorer/copier un volume ?

Physical Extents = blocks LVM (taille > nombre)

* petits LV = petits extents

* gros LV = gros extents

* default 4M (2M > 128M)

* vgcreate -s (spécifier la taille des extents)




LINUX : LVM - Comment mirrorer/copier un volume ?


commençons à partir de 2 partitions


pvcreate /dev/sdb1 /dev/sdc1
vgcreate vg_data /dev/sdb1 /dev/sdc1




LINUX : LVM - Comment mirrorer/copier un volume ?


puis créons un LV mirroré


lvcreate -L 200M -n lv_xavki -m1 /dev/vg_data
lvs -o +devices -a


Rq : -m nombre de copie


LINUX : LVM - Comment mirrorer/copier un volume ?


n'oublions pas le formatage de notre FS


mkfs.ext4 /dev/vg_data/lv_xavki
mount -t ext4 /dev/vg_data/lv_xavki /srv/xavki
touch /srv/xavki/demo1.txt




LINUX : LVM - Comment mirrorer/copier un volume ?


test : remplacement d'un PV

attention : si uniquement des LV mirrorés

lvconvert --replace /dev/sdb1 /dev/vg_data/lv_xavki /dev/sdd1
lvdisplay
lvs




LINUX : LVM - Comment mirrorer/copier un volume ?


réparation du LV mirroré (sync extents)


lvconvert --repair /dev/vg_data/lv_xavki
lvs -a -o +devices




LINUX : LVM - Comment mirrorer/copier un volume ?


comment passer d'un LV mirroré à un LV simple ?


lvconvert -m 0 /dev/vg_data/lv_xavki /dev/sdd1
lvs -a -o +devices




LINUX : LVM - Comment mirrorer/copier un volume ?


inversement, comment mirroré un LV simple ?


lvconvert -m 1 /dev/vg_data/lv_xavki /dev/sdc1




LINUX : LVM - Comment mirrorer/copier un volume ?


comment ajouter un PV pour ajouter un mirroring ?


vgextend vg_data /dev/sdd1
lvconvert -m 2 /dev/vg_data/lv_xavki /dev/sdd1


LINUX : Les RAID

RAID : Redundant Array of Independent Disks
1978 : les origines du RAID 5 (IBM) et mention du RAID 1
1987 : technologie RAID (Berkeley)


LINUX : Les RAID

Intérêts ?

* suite à des coûts de stockage très bas

* problématique de performances

* redondance des données (si perte de disque ou erreurs)



Prérequis :

* avoir plusieurs disques

* le nombre dépend du choix de RAID




LINUX : Les RAID

Type de contrôles :

* logiciel

		* moins coûteuse

		* administration système

		* compatibilité

		* moins proche du matériel (erreurs...)

		* consommation de ressources systèmes




LINUX : Les RAID


* matériel semi-matériel : 
		routines en dehors de l'OS
		pas indépendant

		* éviter la dépendance au système d'exploitation

		* idéal pour des fichiers externes à celui-ci

		* consommaion de ressources (système non dédié)

		* difficultés de changement de carte-mère




LINUX : Les RAID


* matériel :
		processeur, mémoire, batterie dédiés

		* détection de problèmes matériels

		* préservation des ressources

		* opérations en arrière plan (check, diag...)

		* pas de compatibilité entre les controleurs

		* le coût

		* haute dispo nécessaire 




LINUX : Les RAID

RAID 0

A1	A2
B2	B1
C1	C2

* disques entrelacés 

* strippé (cf vidéo LVM strippé)

* 2 disques requis

* amélioration sensible des performances

* taille est égale au plus petit des disques (même capacité)

* risque de perte x2 (perte 1 disque = perte totale)




LINUX : Les RAID

RAID 1

A1	A1
B1	B1
C1	C1

* mirroré (duplication)

* 2 disques requis

* résistance à la panne (erreurs ou perte totale)

* pas de perte du service

* performances variables en lectue (amélioration si multithread)

* réduction de perf en écriture (légère)

* capacité = plsu petit des disques

* risque divisé par 2

* augmentation du coût




LINUX : Les RAID

RAID 10

A1	A1	|	A2	A2
B2	B2	|	B1	B1

* 4 disques requis

* cumul de 2 RAID 0 sous un RAID 1

* 2 mirrorés x 2 disques strippés

* cumul des atouts des RAID 0 & 1 (perf et redondance)




LINUX : Les RAID

RAID 5

A1	A2	P
B1	P		B2
P		C1	C2

* 3 disques (n blocs de données & 1 parité par disque)

* mirroré et strippé mais avec des informations de parités
		* algo de parité

* performance de lecture

* écriture réduite

* sur failure pas de perte de l'Array mais reconstruction

* perte de données si perte de 2 disques




LINUX : Les RAID

RAID 6

* idem RAID 5 mais 2 disques de parité


LINUX : RAID 1

Raid logiciel > commande mdadm


sudo apt install mdadm




sudo systemctl status mdmonitor
sudo systemctl start mdmonitor




LINUX : RAID 1


pour un RAID 1


sudo mdadm --create --verbose /dev/md0 --level 1 --raid-devices 2 /dev/sdb1 /dev/sdc1




cat /proc/mdstat
mdadm --detail /dev/md0




LINUX : RAID 1


vitesse de synchronisation


sysctl -a | grep raid


Note : KibiBytes > 1024 Bytes


changer la valeur


echo 50000 > /proc/sys/dev/raid/speed_limit_min


ou

sysctl -w dev.raid.speed_limit_min=50000




LINUX : RAID 1


de manière permanente


# /etc/sysctl.conf
dev.raid.speed_limit_min = 50000




LINUX : RAID 1


pour sauvegarder la configuration de la grappe RAID


mdadm --detail --scan --verbose >> /etc/mdadm/mdadm.conf
update-initramfs -u


Note : important pour garder le numéro du device


LINUX : RAID 1


utilisation


mkfs.ext4 /dev/md0
#/etc/fstab


LINUX : RAID 1 - Ajout, Suppression de disques, Manips


ajouter un disque pour jouer :)



sortir un disque de la grappe raid (array)


mdadm --manage /dev/md0 --fail /dev/sdc1
mdadm --manage /dev/md0 --remove /dev/sdc1




remettre


mdadm --manage /dev/md0 --re-add /dev/sdc1
mdadm --manage /dev/md0 --add /dev/sdc1




si nécessaire


mdadm --stop /dev/md0
mdadm --assemble /dev/md0 /dev/sdb1 /dev/sdc1




LINUX : RAID 1 - Ajout / Suppression de disques


ajouter le nouveau disque


mdadm --manage /dev/md0 --add /dev/sdd1
mdadm -D /dev/md0
cat /proc/mdstat




si remplacement direct


mdadm --manage /dev/md0 --add /dev/sde1
mdadm --manage /dev/md0 --replace /dev/sdc1 --with /dev/sde1




étendre


mdadm --grow /dev/md0 --raid-devices 4 --add /dev/sde1


LINUX : RAID 1 - Test recovery


ajouter un disque pour jouer :)



sortir un disque de la grappe raid (array)


mdadm --manage /dev/md0 --fail /dev/sdc1
mdadm --manage /dev/md0 --remove /dev/sdc1



remettre


mdadm --manage /dev/md0 --re-add /dev/sdc1
mdadm --manage /dev/md0 --add /dev/sdc1
mdadm --manage /dev/md0 --replace /dev/sdc1 --with /dev/sdd1
mdadm --grow /dev/md0 --raid-devices 3 --add /dev/sdc1




LINUX : RAID 1 - Test recovery


stopper un array Raid


mdadm --stop /dev/md0
mdadm --stop --scan




redémarrer un array


mdadm --assemble /dev/md0
mdadm --assemble --scan




LINUX : RAID 1 - Test recovery


ajouter un spare


mdadm --manage /dev/md0 --add /dev/sdd1
mdadm --add-spare /dev/md0 /dev/sde1
mdadm -D /dev/md0 --scan >> /etc/mdadm/mdadm.conf
update-initramfs -u




test suppression du disque


sfdisk -d /dev/sda | sfdisk /dev/sdb




recovery


mdadm --stop /dev/md0
mdadm --assemble /dev/md0




LINUX : RAID 1 - Test recovery


passer en read-only


umount /dev/md0
mdadm --manage /dev/md0 --readonly
mount /dev/md0




repasser en lecture/écriture


mdadm --manage /dev/md0 --readwrite




forcer un rebuild


mdadm --assemble --run --force --update=resync /dev/md0 /dev/sdb1 /dev/sdc1


LINUX : RAID 0 - 5 - 10

RAID 0

mdadm --create --verbose /dev/md0 --level=0 --raid-devices=2 /dev/sdb /dev/sdc
lsblk
mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
update-initramfs -u
mkfs.ext4 /dev/md0
mount /dev/md0 /srv/xavki
#echo '/dev/md0 /mnt/md0 ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
df -h




LINUX : RAID 0 - 5 - 10


clean


dd if=/dev/zero of=/dev/sda bs=1M count=1024
mdadm --zero-superblock /dev/sdb1
mdadm --remove /dev/md0
cp /etc/mdadm/mdadm.conf /etc/mdadm/mdadm.conf.bak




LINUX : RAID 0 - 5 - 10


raid 5


sudo mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sda /dev/sdb /dev/sdc




LINUX : RAID 0 - 5 - 10


raid 6


sudo mdadm --create --verbose /dev/md0 --level=6 --raid-devices=4 /dev/sda /dev/sdb /dev/sdc /dev/sdd




LINUX : RAID 0 - 5 - 10


raid 10


sudo mdadm --create --verbose /dev/md0 --level=10 --raid-devices=4 /dev/sda /dev/sdb /dev/sdc /dev/sdd


LINUX : FSCK - Réparer/Vérifier le Filesystem


vérifier un device


fsck /dev/<device>




forcer la vérification (même si pas nécessaire)


fsck -f /dev/<device>




LINUX : FSCK - Réparer/Vérifier le Filesystem


vérifier les secteurs défectueux


fsck -f -c /dev/<device>


Note : si correction vous aurez une demande de confirmation
-N : si juste check


LINUX : FSCK - Réparer/Vérifier le Filesystem


pour checker tous les devices du fstab (sauf la racine)


fsck -AR -y




LINUX : FSCK - Réparer/Vérifier le Filesystem


comment faire un fsck sur la racine sur ancienne machine


touch /forcefsck
reboot
ls /




sur une nouvelle machine via la cmdline (lancement kernel)


fsck.mode=force fsck.repair=yes
/etc/default/grub
update-grub




LINUX : FSCK - Réparer/Vérifier le Filesystem


fréquence de vérification

tune2fs -c 50 -i 2w /dev/hda1

LINUX : Recap RAID & LVM & DEVICE


Storage Device : disque SSD, HDD, RAID ARRAY
* accès à des block devices
* superblock : metadatas relatives au filesystem



Partition : sous ensemble d'un device de stockage
* primaire/étendue
* typée



LINUX : Recap RAID & LVM & DEVICE


RAID Array (Redundant Array of Independent Disks)
* redondance & aggrégation
* physique ou logiciel ou mixte
* différent type : 0,1,5,10 ...



LVM : PV + VG + LV



Filesystem : comment stocker fichiers, répertoires, journalisation...



LINUX : Recap RAID & LVM & DEVICE


┌──►   FILESYSTEM ◄──────┐◄──┐◄───┐
│                        │   │    │
│                        │   │ LV │
│                        │   │    │
│                        │   │    │
│                        │   │ VG │
├────────┬─►  RAID  ─────┼───┤    │
│        │               │   │    │
│        │               │   │ PV │
│        │               │   │    │
│                        │   │    │
├─────► PARTITIONS  ─────┴───┘    │
│                                 │
                                  │


DISKS ──────────────────────────────┘


LINUX : I/O



I/O = Input/Output


Disk IO (sous toute leur forme)


stockage = HDD / SSD / NAS (NET)


Input = écriture


Output = lecture




LINUX : I/O


data transfert

Les Mesures :


IOPS => lecture/écriture par seconde (en nombre)


KB/s (MB/s) => un débit (quantité par seconde)




point ultra important de performance :
* base de données
* traitement de tâches généralement



LINUX : I/O

Représentation :

USER > Kernel > Mémoire <-> Disks




Mémoire <-> Disks
	* Buffer = écriture
	* Cache  = lecture




LINUX : I/O

Impacts importants :

	* lenteurs applications

	* saturation des CPU 

	* saturation de la RAM



Indicateur principal :

	* iowait (mesure du temps d'attente CPU)

	* attente de lecture/écriture IO

	* wa (top...) , %iowait (iostat), wait...

	* processus status = D (tâche non interruptible)




LINUX : I/O



Facteurs :

  * noatime (fstab) : pas de timestamp (atime)
  	https://opensource.com/article/20/6/linux-noatime

  * développement applicatif (APM est ton ami)

  * garder tout à jour :) (système, applicatif, firmwares...)

  * type de disk (HDD / SSD)

  * type de connectique pour SSD (SAT/NVMe)

  * nombre de disque dans une grappe RAID

  * RAID Level ( 0 = strip, x2, x4... )

  * type random/sequential

  * IOPS

  * taux de lecture et d'écriture

  * taille des blocs (différents niveaux)






LINUX : I/O

FIO > benchmark

Quelques calcules :

* si j'ai un disk capable d'écrire 155 MB/s avec des blocs 4K

	> 155 * 1024 / 4k = 39680 IOPS

* inversement mon disque a pour capacité 40k IOPS et blocs 4k

	> 40000 * 4k / 1024 = 156,25 MB/s
 

LINUX : I/O - iostat



variation d'utilisation en fonction de l'OS


iowait :
* pourcentage (10%)
* x% du CPU est destiné à attendre
* io = lecture/écriture
* si multi processeurs/cores = moyenne


depuis le boot de la machine (tips en fin de vidéo)


ajout d'un nombre fréquence en secondes




LINUX : I/O - iostat


-c : seulement les stats CPU


iostat -c
avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           9,09    0,10    3,47    1,72    0,00   85,62


Note : idem top commande

%user : pourcentage d'utilisation CPU utilisé par le userland (programmes...)
%nice : pourcentage d'utilisation CPU avec une nice priorité (cf tutos process)
%system : pourcentage CPU utilisé par le CPU (noyau)
%iowait : pourcentage CPU en attente d'IO
%steal : pourcentage CPU en attente d'un autre CPU
%idle : pourcentage du CPU qui se tourne les pouces !!




LINUX : I/O - iostat



-h : human readable


-d : uniquement les statistiques des devices


-x : statistiques détaillées (xd)


-p : en spécifiant le device


-m : données en mega


-t : afficher l'heure




LINUX : I/O - iostat

interval


iostat 3 2


Note : par défaut depuis le démarrage de la machine


LINUX : I/O - iostat

rs : lectures réalisées par seconde
ws : écritures réalisées par seconde
	tps : transferts par seconde (requêtes d'IO par seconde > agrégation logique)
	%util : pourcentage de temps d'utilisation du disque (100% saturé)

tm_act : pourcentage du temps pendant lequel le disque est occupé
kbps : nombre de KB transférés à partir du disque / vers le disque
msps : moyenne du temps de recherche (si les disques supportent ce
compteur)
kB_read (/s) : volume/blocks lus en KB sur le device
kB_wrtn (/s) : volume/blocks écrits en KB sur le device
kB_dscd (/s) : volume/blocks rejetés par le device


LINUX : Udev - Manager les devices



dev : devices (périphériques) > /dev (répertoire dynamique)


Udev = Userspace /dev (devices)


track les évènements du kernel


avec le kernel > 2.6 : avant devfs


udevd = daemon




LINUX : Udev - Manager les devices

Multiples enjeux :

	* enjeu desktop (plug souris, etc)

	* nom des devices

	* abstraction du péripériques

	* droits sur les périphériques




LINUX : Udev - Manager les devices



rules :

  * /etc/udev/rules.conf : conf générale
  * /etc/udev/rules.d/ : règles perso
  * /lib/udev/rules.d/ : règles générales






ls /dev/disk
ls -l /dev/disk/by-id



LINUX : Udev - Manager les devices

man udev

udevadm :

* monitor : écoute des évènements au niveau du kernel

* control : modification d'un état

* trigger : lance un signal

* test : récupère le résultat de l'exécution




LINUX : Udev - Manager les devices


exemples :


udevadm monitor --udev
udevadm info /dev/nvme0n1
udevadm info -a /dev/nvme0n1
udevadm test /sys/block/sdb


LINUX : Udev - Démo - Créer un nouveau SymLink

udevadm :

* monitor : écoute des évènements au niveau du kernel

* control : modification d'un état

* trigger : lance un signal

* test : récupère le résultat de l'exécution




LINUX : Udev - Démo - Créer un nouveau SymLink

Les Keywords (cumulatif séprateur ","):

* ACTION : sur quel action du device agir 
	add / remove / change

* DEVPATH

* KERNEL : nom de l'évènement du device (généralement device)

* NAME : pour le nom des interfaces réseaux

* PROGRAM : sélectionner sur une commande

* RUN : lance de commande




LINUX : Udev - Démo - Créer un nouveau SymLink

Recherche dans le devpath (les éléments des parents)

* KERNELS : recherche dans le devpath

* SUBSYSTEMS : recherche dans le devpath le nom d'un sous système

* DRIVERS : recherche le driver du device dans le subpath




LINUX : Udev - Démo - Créer un nouveau SymLink

Utilisation des attributs

* ATTR{<attribut>} : recherche dans les attributs du device

* ATTRS{<attributs>} : idem dans les parents

* ENV{<propriété>) : utilisation de la propriété du device




LINUX : Udev - Démo - Créer un nouveau SymLink


udevadm monitor --udev
udevadm info -a /dev/nvme0n1
udevadm info -a /dev/nvme0n1 -q property
udevadm info -a /dev/nvme0n1 -q all
udevadm info -a /dev/nvme0n1 -q all --help




LINUX : Udev - Démo - Créer un nouveau SymLink

Les opérateurs:

* "==" : égal à

* "!=" : différent de

* "="  : affecte/définit des valeurs

* "+=" : ajoute des éléments à une variable déjà définie

* "-=" : retire la valeur de la variable

* ":=" : définit une valeur en dernière position et empêhce tout changement




LINUX : Udev - Démo - Créer un nouveau SymLink

Petit exemple : création d'un nouve device pointant vers /dev/sdb

notre règle


KERNEL=="sd*", ENV{ID_SERIAL}=="xxxxx", SYMLINK+="sdx", RUN+="/bin/sh -c '${date +%Y%m%d} - echo SDX created' > /tmp/xavki.log"



pour tester la règle


udevadm trigger --typ devices --action change


LINUX : Udev - Démo - Créer un device custom

SCSI = Small Computer System Interface
Protocole dédié aux interfaces de stockage (disques)
C'est une connexion : carte dédiée / bus (identification)

Les Keywords (cumulatif séprateur ","):

* ACTION : sur quel action du device agir 
	add / remove / change

* DEVPATH

* KERNEL : nom de l'évènement du device (généralement device)

* NAME : pour le nom des interfaces réseaux

* PROGRAM : sélectionner sur une commande

* RUN : lance de commande




LINUX : Udev - Démo - Créer un device custom

Recherche dans le devpath (les éléments des parents)

* KERNELS : recherche dans le devpath

* SUBSYSTEMS : recherche dans le devpath le nom d'un sous système

* DRIVERS : recherche le driver du device dans le subpath




LINUX : Udev - Démo - Créer un device custom

Utilisation des attributs

* ATTR{<attribut>} : recherche dans les attributs du device

* ATTRS{<attributs>} : idem dans les parents

* ENV{<propriété>) : utilisation de la propriété du device




LINUX : Udev - Démo - Créer un device custom


udevadm monitor --udev
udevadm info -a /dev/nvme0n1
udevadm info -a /dev/nvme0n1 -q property
udevadm info -a /dev/nvme0n1 -q all
udevadm info -a /dev/nvme0n1 -q all --help




LINUX : Udev - Démo - Créer un device custom

Les opérateurs:

* "==" : égal à

* "!=" : différent de

* "="  : affecte/définit des valeurs

* "+=" : ajoute des éléments à une variable déjà définie

* "-=" : retire la valeur de la variable

* ":=" : définit une valeur en dernière position et empêhce tout changement




LINUX : Udev - Démo - Créer un device custom

Petit exemple : récupérer l'identifiant scsi pour repérer un disque et lui affecter un device

récupération de l'id scsi


/usr/lib/udev/scsi_id -g -u /dev/sdb



notre règle


KERNEL=="sd*",
ENV{DEVTYPE}=="disk",
PROGRAM=="/usr/lib/udev/scsi_id -g -u -d $devnode",
RESULT=="xxx",
RUN+="/bin/sh -c 'mknod /dev/xavki b $major $minor; chown xavki:xavki/dev/xavki; chmod 660 /dev/xavki'"



pour tester la règle


udevadm trigger --typ devices --action change


LINUX : Device Mapper

https://en.wikipedia.org/wiki/Device_mapper
DM = Device Mapper

DM =

* framework fourni par le kernel linux

* mapper des blocks devices physique

* en blocks devices virtuels pour l'utilisateur

* possibilité de crtyper les disques

* les fondements de LVM2


Mapper = table de mappage

* un device dispoe d'un nom (sda) et par le couple major/minor (256:1)




LINUX : Device Mapper

DMSETUP


liste des devices


dmsetup ls
dmsetup ls --tree #lsblk




afficher la table de mappage


dmsetup table




résumé global de device mapper


dmsetup info #lvdisplay ou lvs
dmsetup info -c vgubuntu-root




LINUX : Device Mapper


affichage des dépendances (couple major/minor)


dmsetup deps




renommer des device


dmsetup rename deb1--vg-tmp deb1--vg-temp




LINUX : Device Mapper


suspendre les I/O


dmsetup suspend --nolockfs deb1--vg-tmp
dmsetup suspend --noflush deb1--vg-tmp
dmsetup info




réactiver


dmsetup resume deb1--vg-tmp




création


echo "0 1024 linear /dev/sdb1 0" | dmsetup create toto


https://docs.kernel.org/admin-guide/device-mapper/index.html



LINUX : Pseudos Devices



/dev/null


/dev/zero


/dev/full


/dev/random


/dev/loop


man null


LINUX : Pseudos Devices


/dev/null : pas d'output, pas de valeur


cat /dev/null
ls > /dev/null
ls nothing 2> /dev/null
dd if=/dev/null of=test.txt count=1 bs=1024
ls -a




LINUX : Pseudos Devices


/dev/zero : flux continu de valeur null (ASCII 0 = 0x00) c'est à dire de 0 en binaire


man ascii
cat /dev/zero
dd if=/dev/zero of=/opt/zero.txt bs=2048 count=2048
dd if=/dev/zero of=test.txt count=1 bs=1024
ls -a


Note : American Standard Code for Information Interchange
Codage de caractères


LINUX : Pseudos Devices


/dev/full : idem à /dev/zero mais avec un retour d'espace plein


echo "toto" > /dev/full




LINUX : Pseudos Devices


/dev/random : génère des chiffres aléatoire (souvent utilisé en cryptographie)


dd if=/dev/random of=test.txt count=1 bs=1024
head -c 500 /dev/random | tr -dc 'a-zA-Z0-9~!@#$%^&*_-'
head -c 500 /dev/random | base64




LINUX : Pseudos Devices


/dev/loop : mise à disposition de fichiers sous forme de block device (/dev)


losetup --list



LINUX : Device TTY & PTS


précédente vidéo : shell vs console vs terminal


TeleTYpewriter ou  Téléscripteurs

TTY = console terminal (primitif)
PTS = pseudo terminal (indirect)
Note : man !!!


LINUX : Device TTY & PTS


commandes


tty
who
w



changer de terminal


ctrl + alt + f[1-6]



debug : pas de tty/terminal (ssh,docker...)


-t 


LINUX : Multiplexer de terminaux - SCREEN



multiplexer de terminaux


permet :

  * partager un terminal

  * maintenir des commandes longues (sinon nohup &)

  * organiser le travail






LINUX : Multiplexer de terminaux - SCREEN


lister les screens


screen -ls




ouvrir un screen


screen
screen -ls




s'attacher à un screen


screen -r <id_screen>
exit




LINUX : Multiplexer de terminaux - SCREEN


donner un nom


screen -S <nom_session>
screen -r <nom_session>




multi-attachement


screen -S <nom_session>
sleep 10000
screen -x <nom_session> 




LINUX : Multiplexer de terminaux - SCREEN


raccourcis


    [CTRL]+[a] suivi de [n]: pour «next», aller au terminal suivant.
    [CTRL]+[a] suivi de [p]: pour «previous», aller au terminal précédent.
    [CTRL]+[a] suivi de [0]..[9]: aller au terminal n.
    [CTRL]+[a] suivi de [']: saisir dans le prompt le numéro du terminal.
    [CTRL]+[a] suivi de ["]: lister des différents terminaux, avec la possibilité d'en choisir un.
    [CTRL]+[a] suivi de [w]: lister les terminaux actuels avec leur nom.
    [CTRL]+[a] suivi de [a]: retourner au terminal d'où l'on vient.
    [CTRL]+[a] suivi de [A]: nommer les terminaux et s'y rendre par la suite plus aisément.




LINUX : STDIN & STDOUT & STDERR



pour chaque programme


3 streams (canaux de communications) :

  * entrées

  * sorties

  * erreurs






LINUX : STDIN & STDOUT & STDERR

stdin (0) : standard input
stdout (1) : standard output
stderr (2) : standard error

man stdout




disposent aussi d'un device


ls /dev/std*




LINUX : STDIN & STDOUT & STDERR

file descriptor (FD) : fichiers numérotés et réservés
* moyens d'échanges/communication
* chaque process dispose de ses files descriptors
* à retrouver dans /proc//fd/1...
* potentiellement communicable entre programmes
* ex : un fichier lu/sortie est représenté sous forme de FD à sa lecture
* par opposition à la socket descriptor (réseau)
* 0/1/2 et 3-9 (temporaires)

man open




LINUX : STDIN & STDOUT & STDERR


stdin & stdout


echo "stdin" > /dev/stdin
echo "stdout" > /dev/stdout
echo "nothing" | sudo tee /dev/stderr
read
echo $REPLY




LINUX : STDIN & STDOUT & STDERR


stderr


ls nothing
ls * toto  2>/dev/null
ls * toto 2>&1 >/dev/null




cat <<EOF 
toto
EOF




LINUX : STDIN & STDOUT & STDERR

echo $$
sudo cat /proc/16806/fd/0




LINUX : STDIN & STDOUT & STDERR


exec 7<<EOF
Salut Xavki
EOF
read -u 7
echo $REPLY



LINUX : Redirections & Pipe & tee



Rediriger les flux (cf vidéo précédente stdin/stderr/stdout)
* interaction avec le terminal


redirection simple de stdout vers un fichier



ls /tmp > output.txt


Note : on écrase le contenu du fichier à chaque fois


LINUX : Redirections & Pipe & tee


redirection


ls /tmp >> output.txt




rediriger stdout (file descriptor 1)


ls /tmp 1> output.txt




LINUX : Redirections & Pipe & tee


rediriger stderr


ls /tmp 2> output.txt




LINUX : Redirections & Pipe & tee


séparation dans 2 fichiers


ls . nothing 2> stderr.txt 1> stdout.xt




LINUX : Redirections & Pipe & tee


rediriger stderr vers stdout


ls /tmp 2>&1 > output.txt
cp toto titi &> /dev/null
ls nothing 2>/dev/null


Note : attention l'ordre compte


LINUX : Redirections & Pipe & tee


injecter un fichier avec stdin


ls < stdout.xt
ls . nothing 2> stderr.txt 1> stdout.new < stdout.xt 
ls * nothing 2>/dev/fd/1 1> /dev/null
sort < b.txt > c.txt



idem à :


echo "hello world" |& cat




LINUX : Redirections & Pipe & tee


combiner 2 commandes sans erreurs


ls nothing && echo toto




combiner avec erreur


ls nothing || echo toto




LINUX : Redirections & Pipe & tee


le pipe (communication inter-processus)


cat /etc/hosts | grep 127


Note : stdout de 1 écrit dans stdin de 2


LINUX : Redirections & Pipe & tee


avec tee (option-a) :


ls /tmp | tee output.txt
ls /tmp | tee -a output.txt



LINUX : DU & DF


DU = Disk Usage

Options courantes :

* -h : format humain (juste répertoires)



du -h /tmp



* -s : summarize (somme pour un répertoire)



du -sh /tmp




LINUX : DU & DF


* -a : fichiers et répertoires



du -sh /tmp



-c : ajoute le total


du -csh /tmp



* --time : ajout de la dernière date de modification



du -h --time *



* combinaison avec sort et head



du | sort -n -r | head
du * | sort -n -r | head




LINUX : DU & DF


DF

DF = Disk Filesystem

* -a : affiche tous les montages

* -h : format de taille humain

* -i : consommation en inodes

* --total : dernière ligne (tail -1)

* -T : type de filesystem

* -t <ext4> : un type de filesystem

* -x <tmpfs> : exclure un type de filesystem




LINUX : DU & DF



colonnes :


Filesystem : devices des filesystems


1k-block : taille en block de 1Kb


Used : taille utilisée


Available : taille disponible


Use% : utilisation en pourcentage


Mounted on : où le device est monté sur FHS


LINUX : CLI Devices


récupérer les ID des devices


blkid




lister les blockdevices


lsblk
lsblk -f
lsblk -r
lsblk -d -o name,rota




LINUX : CLI Devices


taille, secteurs des disques


fdisk -l | grep '^Disk /dev/'




LINUX : CLI Devices


caractéristiques des disques
* SMART : collecte d'informations sur les disques
* fonctionne avec un daemon


sudo apt-get install smartmontools
sudo smartctl --all  /dev/nvme0n1
sudo smartctl --smart=on  /dev/nvme0n1
sudo smartctl -l error  /dev/nvme0n1
sudo smartctl -l selftest  /dev/nvme0n1
cat /etc/default/smartmontools




LINUX : CLI Devices


informations fournies par udev


sudo udevadm info -a -n /dev/nvme0n1




autres infos


sudo lshw -class disk -class storage
sudo lshw -short -C disk
cat /sys/block/nvme0n1/queue/rotational
iostat
dumpe2fs




LINUX : CLI Devices


test


ioping -c 10 -s 1M /tmp



LINUX : La commande GREP


recherche de patterns dans des lignes de fichiers (et un peu plus...)
* fichiers de configuration
* fichiers de données "plates"
* recherches dans les logs (erreurs...)
* filtrer des informations
* ...



souvent imbriqué "pipé" avec d'autres commandes (cf vidéo précédente)



LINUX : La commande GREP


GREP = grep, egrep, fgrep, rgrep, agrep, zgrep...
* egrep = -E
* fgrep = -F
* pgrep = recherche processus
* zgrep = recherche dans des fichiers compressés
* agrep = recherche approximative



à l'aide !!!


man grep




LINUX : La commande GREP


ligne de commande


grep <options> <recherche> <fichier>
<commande> | grep ...




LINUX : La commande GREP


exemple (quotes...)


grep 127. /etc/hosts
grep "127." /etc/hosts




LINUX : La commande GREP


-i : insensible à la casse


grep "LOCAL" /etc/hosts
grep -i "LOCAL" /etc/hosts




LINUX : La commande GREP


-c : retourne le nombre d'occurences dans le fichier


grep -i -c "LOCAL" /etc/hosts




LINUX : La commande GREP


-n : ajoute le numéro de la ligne en plus


grep -i -n "LOCAL" /etc/hosts




LINUX : La commande GREP


-v : inverse la recherche


grep -i -v "LOCAL" /etc/hosts


Note : exemple les commentaires


LINUX : La commande GREP


-r : recherche récursive


grep -ri "LOCAL" 
grep -ri "LOCAL" /etc/
grep -ri "LOCAL" /etc/hosts /etc/resolv.conf




LINUX : La commande GREP


-E : pattern regexp


grep -E "(127|192).(0|168).[01].[176]" /etc/hosts
egrep "127.0.[01].1" /etc/hosts




LINUX : La commande GREP


-m : limiter aux x premiers lignes sélectionnées


grep -E -m 2 "(127|192).(0|168).[01].[176]" /etc/hosts




LINUX : La commande GREP


-l : juste afficher les fichiers contenant le pattern


grep -rl "127" /etc/hosts




LINUX : La commande GREP


-A/-B/-C : nombre de lignes après / nombre de lignes avant


grep -A2 -B1 "5" test.txt
grep -C1 "5" test.txt




LINUX : La commande GREP


-e : multiple pattern


grep -e "127" -e "192" /etc/hosts




LINUX : La commande GREP


et parfois


alias grep
 --color=always




LINUX : La commande GREP


-o : seulement le résultat du pattern (regexp)


grep -Eo "([0-9]{1,3}\.){3}[0-9]{1,3}" /etc/hosts



LINUX : Les ALIAS



alias = utilisation de commandes & options via des raccourcis


partie intégrante de votre environnement
* .bash_rc, .bash_profile... .bash_aliases




comment lister les alias ?


alias
alias ls




LINUX : Les ALIAS


créer ponctuellement un alias


alias xavki='ls -i'
alias c='clear'




supprimer un alias


unalias ls
unalias -a




LINUX : Les ALIAS


pour en bénéficier à toutes nouvelles sessions


vim ~/.bashrc
source ~/.bashrc




ne pas utiliser un alias


\grep -i "alias" *




LINUX : Les ALIAS

les alias c'est bien mais c'est du oneline ??!! = fonction


hello(){
echo "hello"
}




mkcd(){
mkdir $1 && cd $1
}




LINUX : Les ALIAS


exemple up


up() {
if [ "${1/[^0-9]/}" == "$1" ];then p=./;
for i in $(seq 1 $1);
do p=${p}../;
done;
cd $p;
else echo 'usage: up N';
fi
}


LINUX : La commande FIND

Permet :

* trouver des fichiers et des répertoires

* multicritères : noms, date de modification, taille...

* exécuter des commandes à partir des fichiers/réperoires




LINUX : La commande FIND


commande


find <point_recherche> <options> <expression>




tout lister (fichiers/répertoires et récurrence)


find .




LINUX : La commande FIND


à partir d'un nom exact


find . -name "slides.md"
find . -name "Slides.md"
find . -name "*.txt"




incensitive


find . -iname "slides.md"




LINUX : La commande FIND


avec un pattern & regex


find . -name "*.txt"
find . -regextype sed -regex ".*/[to]\{4\}\.txt"




inverse/reverse


find . ! -name "slides.md"




LINUX : La commande FIND


en précisant le type


find . -type d
find . -type d -iname "*iops*"
find . ! -type f -iname "*iops*"



f plain files
d directories
l symbolic links
b block devices
c character devices
p named pipes
s sockets




LINUX : La commande FIND


limiter le niveau de profondeur


find . -type d -iname "*iops*" -maxdepth 1




par la taille


find . -size +3k -type f
find . -size -3k -type f
find . -empty


Note : G,M,k,c


LINUX : La commande FIND


date/heure de modification


find . -cmin -60
find . -cmin +60
find . -mtime +100


Note: a = access ; m = modification ; c = creation


LINUX : La commande FIND


coupler avec l'exécution d'une commande


find . -mtime +100 -exec cat '{}' \;
find . -mtime +10 -mtime -20 -exec cat '{}' \;
find . -mtime +10 -mtime -20 -exec wc -l {} \;
find . -name "*.png" -exec cp {} /backups/images \;


Note : pour supprimer rm ou -delete


LINUX : La commande FIND


en fonction des permissions & user


find . -perm 775
find . -perm /u=x
find . -user xavki -group www-data




opérateur


find . -name "*.txt" -or -name "*.pdf"
find . -name "*.txt" -and -name "*.pdf"
find . -name "*.txt" -and ! -name "*test*"


LINUX : Un PROCESS c'est quoi ??


process = processus (tasks)



un process = c'est une instance d'un programme (plus ou moins gros/important



c'est un exécutable (permissions)



stocké sur la machine (sauf exceptions...)



lancer un programme = créer un nouveau processus



lancé par un utilisateur (système ou réel)



PID = identifiant unique du processus



Linux = multitask OS (multiple process en même temps)

https://tldp.org/LDP/tlk/kernel/processes.html


LINUX : Un PROCESS c'est quoi ??


process = processus (tasks)



lister les processus : commande ps


ps 
echo $$
ps aux
ps auxwww


Note : notre bash/shell est un process


LINUX : Un PROCESS c'est quoi ??


process / hardware = CPU & Memoire & stockage (lui-même)

Caractéristiques :


	* un identifiant le PID




	* adresse en mémoire




	* un statut : running, stopped, waiting, zombie




	* un propriétaire (owner qui a lancé le process) - UID




	* des ressources : cpu/ram




	* des fichiers utilisés

	* des sockets réseaux (fichiers dédiés à la communication) & des ports

	* des signaux

	* peut attendre :  cpu / io disque / réseau...




LINUX : Un PROCESS c'est quoi ??

PID :

	* identifiant unique dans le kernel

	* numéro incrémenté par ordre de création

	* isolation entre les processus (sécurité)




LINUX : Un PROCESS c'est quoi ??

PID 1 = Init

	* le père de tous les process (règle Unix)



ps aux | head -n2



	* émane de systemD (management des services, montages... sous forme d'unités)



man init




	* c'est donc la première et la dernière task du système (commande init 0 - arrêt / init 6 - reboot)

	* issue de la phase de boot (cf vidéo précédente)

	* création de processus par fork 



man 2 fork




	* reaping = s'occupe des processus orphelins (perte des parents)




LINUX : Un PROCESS c'est quoi ??

Un peu d'histoire : https://linuxfr.org/news/systemd-l-init-martyrise-l-init-bafoue-mais-l-init-libere


LINUX : Qu'est-ce qu'un fork ?


programme = un bout de code inerte
* du code
* des variables
* des données
* dispose d'un point d'entrée (explicite ou non)



process = un programme lancé/exécuté
* stockage en mémoire (adresses)
* réservation/utilisation de ressources (cpu/mémoire)
* isolation (ex : redéfinition du contexte)



LINUX : Qu'est-ce qu'un fork ?



fork :
1- lancement du programme principal




2- création du process parent (PID parent)
		* affectation ressources
		* owner
		* isolation...




LINUX : Qu'est-ce qu'un fork ?


3- appel fork() (syscall)
		* copie presque intégrale du process actuel (parent)
		* code retour < 0 : errreur
		* code retour = 0 : pour l'enfant
		* code retour = PID de l'enfant : pour le parent




LINUX : Qu'est-ce qu'un fork ?


4- identification :
		* de l'enfant vue du parent (PID)
		* parent (PPID)
		* parent lance wait() (attente de l'enfant)




5- l'enfant termine (exit)




6- le parent lève le wait (signal SIGCHLD) et continue




LINUX : Qu'est-ce qu'un fork ?

exemple :

echo $$
echo $PPID
ps aux | grep $PPID
ps faux



oki         3180  3.7  1.0 4304660 261788 ?      Ssl  21:07   1:12  \_ /usr/bin/gnome-shell
oki         3399  0.0  0.0 162700  7136 ?        Sl   21:07   0:00  |   |   \_ ...
oki         5614  0.9  0.3 841544 73416 ?        Sl   21:24   0:08  |   \_ /usr/bin/python3 /usr/bin/terminator
oki         7343  0.1  0.0  21316 15400 pts/1    Ss   21:38   0:00  |       \_ /bin/bash
oki         7504  0.0  0.0  11928  3852 pts/1    R+   21:39   0:00  |           \_ ps faux




LINUX : Qu'est-ce qu'un fork ?



Process suite :

  * cat /proc/1/status
  * 2 > 32767 (proportionnel aux coeurs)
  * pid 0 : swaper ou scheduler (responsable du paging)
  * pid_max





pid_max = min(pid_max_max, max_t(int, pid_max,
           PIDS_PER_CPU_DEFAULT * num_possible_cpus()));


https://elixir.bootlin.com/linux/v4.7.10/source/kernel/pid.c#L595


LINUX : Qu'est-ce qu'un fork ?


	* ses file descriptors



less slides.md
ps aux | grep slides
ls -la /proc/<pid>/fd


LINUX : Qu'est-ce qu'un fork ?


programme = un bout de code inerte
* du code
* des variables
* des données
* dispose d'un point d'entrée (explicite ou non)



process = un programme lancé/exécuté
* stockage en mémoire (adresses)
* réservation/utilisation de ressources (cpu/mémoire)
* isolation (ex : redéfinition du contexte)



LINUX : Qu'est-ce qu'un fork ?



fork :
1- lancement du programme principal




2- création du process parent (PID parent)
		* affectation ressources
		* owner
		* isolation...




LINUX : Qu'est-ce qu'un fork ?


3- appel fork() (syscall)
		* copie presque intégrale du process actuel (parent)
		* code retour < 0 : errreur
		* code retour = 0 : pour l'enfant
		* code retour = PID de l'enfant : pour le parent




LINUX : Qu'est-ce qu'un fork ?


4- identification :
		* de l'enfant vue du parent (PID)
		* parent (PPID)
		* parent lance wait() (attente de l'enfant)




5- l'enfant termine (exit)




6- le parent lève le wait (signal SIGCHLD) et continue




LINUX : Qu'est-ce qu'un fork ?

exemple :

echo $$
echo $PPID
ps aux | grep $PPID
ps faux



oki         3180  3.7  1.0 4304660 261788 ?      Ssl  21:07   1:12  \_ /usr/bin/gnome-shell
oki         3399  0.0  0.0 162700  7136 ?        Sl   21:07   0:00  |   |   \_ ...
oki         5614  0.9  0.3 841544 73416 ?        Sl   21:24   0:08  |   \_ /usr/bin/python3 /usr/bin/terminator
oki         7343  0.1  0.0  21316 15400 pts/1    Ss   21:38   0:00  |       \_ /bin/bash
oki         7504  0.0  0.0  11928  3852 pts/1    R+   21:39   0:00  |           \_ ps faux




LINUX : Qu'est-ce qu'un fork ?



Process suite :

  * cat /proc/1/status
  * 2 > 32767 (proportionnel aux coeurs)
  * pid 0 : swaper ou scheduler (responsable du paging)
  * pid_max





pid_max = min(pid_max_max, max_t(int, pid_max,
           PIDS_PER_CPU_DEFAULT * num_possible_cpus()));


https://elixir.bootlin.com/linux/v4.7.10/source/kernel/pid.c#L595


LINUX : Qu'est-ce qu'un fork ?


	* ses file descriptors



less slides.md
ps aux | grep slides
ls -la /proc/<pid>/fd



LINUX : Le statut des Process


status d'un process



* created




* ready (runnable R)




* running (running R)




* waiting (sleeping) > libère le core/cpu
	* interruptible (S)
	* ininterruptible (D - ex : iowait) 




* arrêté (stopped T)




* terminated 




* orphelins (zombie Z)




LINUX : Le statut des Process


                ┌─────────────┐
    NEW         │ Scheduler   │      TERMINATED
     │          └─────────────┘           ▲
     │                                    │
     └────► READY ────────► RUNNING ──────┘
             ▲                 │
             │                 │    ┌───────┐
             │                 │    │ EXIT  │
             └──── WAITING ◄───┘    └───────┘
            ┌───────────────────┐
            │  IO or Events     │
            └───────────────────┘



LINUX : Process vs Fork vs Thread

Linux : OS multitâches et préemptif
* démarrer
* stopper
* reprendre
Rôle du scheduler

1 core : pas de parallélisation
On parle de "simultanéité apparente"
Du coup, le scheduler intègre une priorisation

démarrer/stopper/reprendre = context switching (commutation de contexte)
* l'enjeu est de fixer l'état du process suspendu
* pour pouvoir le reprendre où il en était


LINUX : Process vs Fork vs Thread

Processus/Fork :

     ┌──────────────────┐
     │                  │
     │    Pile (Stack)  │ Variables locales & retours de Fonctions
     │                  │
     ├──────────────────┤
     │                  │
     │   Bibliothèques  │	Lib partagées
     │                  │
     ├──────────────────┤
     │                  │
     │   Tas (Heap)     │	Variables non ordonnées/vrac
     │                  │
     ├──────────────────┤
     │                  │
     │  Données (Datas) │	Variables globales
     │                  │
     ├──────────────────┤
     │                  │
     │   Code (Text)    │	Code à exécuter
     │                  │
     └──────────────────┘




LINUX : Process vs Fork vs Thread


	* fonction fork() et wait()




	* processus fils




	* PID différents entre père et fils




	* copie similaire au process parent (même variables et code par ex)




	* valeurs différenciées via l'utilisation du PID




	* par exemple au fork() COPIE des files descriptors




	* mais différenciation après




	* communication entre processus (plus coûteux)




LINUX : Process vs Fork vs Thread

Thread :

     ┌──────────────────┐
     │    Pile1         │
     │    Pile2         │ Variables locales & retours de Fonctions
     │    Pile3         │
     ├──────────────────┤
     │                  │
     │   Bibliothèques  │ Lib partagées
     │                  │
     ├──────────────────┤
     │                  │
     │   Tas (Heap)     │ Variables temporaires/vrac
     │                  │
     ├──────────────────┤
     │                  │
     │  Données (Datas) │ Variables globales
     │                  │
     ├──────────────────┤
     │                  │
     │   Code (Text)    │ Code à exécuter
     │                  │
     └──────────────────┘




LINUX : Process vs Fork vs Thread


	* en apparence similaire à un processus




	* même mémoire




	* identification : Thread Group ID (PID)  et Thread ID 




	* cependant les variables et FD sont partagées en mémoire




	* économie de commutation de contexte (la mémoire reste la même)




	* communication simplifiée car mémoire partagée




	* si perte du père perte des threads




	* le thread n'est pas tout le contenu du code du père
	* juste une fonction (plus léger qu'un fork)
	* délégation de certaines petites tâches au thread
	* optimisé par le multitâche et donc pseudo-paralélisation (de tâches diff)




	* certains problèmes : modification en parallèle des variables en mémoire
	* solutions existent (mutex = priorisation)


LINUX : Process & Priorités (niceness)



Linux : OS Multitâches & Preemptive


Management des tâches par le scheduler


outil : nice (ionice pour les io)




LINUX : Process & Priorités (niceness)

NICE :


	* nice : combien tu es "nice" avec les autres ??




	* nombre entre -20 et +19




	* plus la valeur est haute = moins prioritaire (become nice ;) )




	* plus la valeur est faible ou inf à 0 = plus prioritaire (less nice)




	* moins utilisé (capacités des CPU et scheduler)




	* valeur hérité du parent




	* sécurité : un owner du process ne peut que augmenter la valeur ;) (devenir root)




LINUX : Process & Priorités (niceness)


lançons un process


nice -n 5 /usr/bin/sleep infinity



si process déjà existant


renice 10 $(pgrep sleep)
ps -l $(pgrep sleep)
renice 11 $(pgrep sleep)
renice 5 $(pgrep sleep)
sudo renice 5 $(pgrep sleep)


LINUX : Commande PS


ps = process state


man ps




pid, uid, priorité, cpu, mémoire, statuts, cmdline...


le petit copain de la commande TOP




LINUX : Commande PS


attention : le tiret joue un rôle


ps a
ps -a


Note : a = tous les process


LINUX : Commande PS


exemples


ps a # tous les utilisateurs hors root
ps au # ajout d'information user
ps aux # tous les process sans exception
ps faux # sous forme d'arbre
ps fauxww # cmdline complète sans limite
ps raux # seulement les process running




LINUX : Commande PS



colonnes

  * USER : propriétaire du process (pas du programme ;) )
  * PID : Process id
  * %CPU : pourcentage d'utilisation du cpu par ce process (temps)
  * %MEM : pourcentage de la mémoire utilisé par ce process
  * VSZ : Virtual Memory Size (allouée mais pas forcément utilisée physique ou non)
  * RSS : Resident Set Size (utilisée et physique)
  * STAT : status du process (R / S / D / T / Z)
  * TIME : temps cumulé de CPU utilisé
  * CMD : la ligne de commande (programme)
  * TTY : terminal associé (si tel est le cas)






LINUX : Commande PS


trier par une colonne


ps aux --sort=+%mem




PPID, horodatage


ps -ef




pour les threads


ps -eLf


Note :
* LWP : ID du thread
* NLWP : Nb de thread


LINUX : Commande PS


TOP10 des process pour le CPU


ps -eo pcpu,args | sort -rn  | head




récupérer la commande d'un process


ps -q 11729 -o cmd | tail -n1
ps -p 1 11729




LINUX : Commande PS


complément


ps -C vim
pgrep vim
pidof vim
pstree


LINUX : Signaux & Kill


signal = moyen d'interagir avec un process en cours



capturé par les programmes > actions en conséquence




environ 30 signaux


connus par un numéro ou un nom




LINUX : Signaux & Kill



comportements différents :

  * certains signaux peuvent être capturés

  * certains peuvent être bloqués

  * certains peuvent entrainer un core dump
  	(génère un fichier avec la mémoire, registres, détails)






LINUX : Signaux & Kill


signal = moyen d'interagir avec un process en cours
envoyer des signaux :


kill -<signal> <pid>
kill -s <signal> <pid>




LINUX : Signaux & Kill

Les principaux SIG :

HUP (1) : Hangup - capturé / bloqué
		* soit utilisé par certains programme pour se "reloader" 
		* soit utilisé par les shell pour arrêter leurs process fils




LINUX : Signaux & Kill


INT (2) : Interrupt - capturé / bloqué
		* équivalent d'un Ctrl+C




LINUX : Signaux & Kill


QUIT (3) : Quit - capturé / bloqué / dumpé
		* identique à TERM mais avec core dump




LINUX : Signaux & Kill


KILL (9) : Kill - rien
		* coupure brutale et inarrêtable




LINUX : Signaux & Kill


TERM (15) : capturé / bloqué
		* arrêt propre du process




LINUX : Signaux & Kill


SEGV (11) : Segmentation Fault - capturé / bloqué / dumpé
		* arrêt suite à une erreur mémoire




LINUX : Signaux & Kill


STOP (17) : Stop - rien
		* mettre en pause un process




LINUX : Signaux & Kill


CONT (19) : Continue - capturé
		* reprendre un process en STOP



LINUX : Jobs & Nohup



jobs = comment faire tourner un process en backgroud ?


pour ne pas perdre le process :
* fermeture du terminal
* perte de connexion réseau
* ...




LINUX : Jobs & Nohup


créer un job


<command> &




lister les jobs


jobs
jobs -l
jobs -p
jobs -r




LINUX : Jobs & Nohup


reprendre un job


fg %<num>




LINUX : Jobs & Nohup


mettre en pause (stopped)

Ctrl+Z

jobs -s
bg %1 # running
fg %1
Ctrl+Z




LINUX : Jobs & Nohup



nohup = pas de signal up possible (attention ça limite pas tout)


combinaison avec le job



nohup sleep 3600 &


LINUX : PROC, le pseudo-fs


qu'est-ce que fait PS ??


strace -e openat ps




LINUX : PROC, le pseudo-fs



du coup regardons un peu /proc


quelques génériques



cat /proc/version
cat /proc/cmdline
cat /proc/uptime
cat /proc/loadavg
cat /proc/cpuinfo
cat /proc/meminfo
cat /proc/vmstat
cat /proc/diskstats
cat /proc/stat




LINUX : PROC, le pseudo-fs


pour chaque process


ls /proc/$(pgrep sleep)/
cat /proc/xx/cmdline
cat /proc/xx/cwd
cat /proc/xx/environ
cat /proc/xx/exe
cat /proc/xx/fdinfo/1
ls /proc/xx/fd/
cat /proc/xx/oom_score
cat /proc/xx/cgroup
cat /proc/xx/ns
cat /proc/xx/stat
cat /proc/xx/statm



LINUX : Crontab & les Crons

Objectif :

	* programmer des tâches régulières

	* lancer ces tâches avec un utilisateur spécifié



man cron




LINUX : Crontab & les Crons

Deux types de configuration :

	* crontab : à travers la commande crontab ou /var/spool/cron
			* gestion par utilisateur

	* /etc/cron.d/ ou /etc/cron.daily/ (hourly...) : avec des fichiers 
			* possiblité de définir l'utilisateur dans la ligne de cron




LINUX : Crontab & les Crons

Par la commande crontab :

éditer


crontab -e
* * * * * echo "$(date)" >> /tmp/xavki.txt



lister


crontab -l




LINUX : Crontab & les Crons


pour lister d'un autre utilisateur


crontab -u toto -l



supprimer tout le fichier (attention)


crontab -r



visualiser ou éditer via spool


sudo cat /var/spool/cron/crontabs/oki




LINUX : Crontab & les Crons

Une ligne de cron : job

	* <fréquence><user?><variable?><commande>

	* fréquence : <minute><heure><jour_mois><mois><jour_semaine>




LINUX : Crontab & les Crons

Les caractères spéciaux :

	* "*" : toutes les occurences (ex : toutes les minutes...)

	* "," : spécifier plusieurs valeurs de temps (ex : 1,2,3 (lun/mar/mer)

	* "-" : définir une plage de temps (ex : 10-20 entre 10min et 20min)

	* "/" : définir un interval de temps (ex : */5 toutes les 5 minutes)

	* "L" : définir le dernier élément de (ex : 5L dernier vendredi

	* "#" : pour indiquer le jour du mois avec sa position (ex : 2#3 troisième mardi)




LINUX : Crontab & les Crons


exemples :


* * * * * echo "Je suis là" > /tmp/xavki.txt
* * * * * root echo "Je suis là" > /tmp/xavki.txt
*/5 * * * * /opt/monscript.sh




Envoi de mail possible (sous réserv de configurer un serveur smtp


MAILTO="xavki@moi.fr"




LINUX : Crontab & les Crons


cas de /etc/cron.d/ ou autre


* * * * * root echo "$(date)" >> /tmp/xavki.txt




autorisation


/etc/cron.allow
/etc/cron.deny


LINUX : SYSTEMD - Introduction


SystemD = System Daemon



Grosse application avec plein de services




annecdote : remplacement de SystemV  > System D = System 500 (chiffre romain)


Pour l'histoire :


https://linuxfr.org/news/systemd-l-init-martyrise-l-init-bafoue-mais-l-init-libere


LINUX : SYSTEMD - Introduction



beaucoup de discussions :

  * accélérer le boot final (desktop)

  * anti principe KISS (Keep It Simple and Stupid

  * non respect de règles fondamentales linux (conf hors etc ...)

  * scripts shell tranformés en déclaration

  * projet mené d'une main de fer

  * résistance de certaines distributions

  * ...






LINUX : SYSTEMD - Introduction

Perso = peu importe il faut faire comme c'est :)
... mais il y a encore des reliquats : /etc/init.d/ ou commande service...

Informations :

man systemd
man systemd.service
...


https://www.freedesktop.org/wiki/Software/systemd/
https://lea-linux.org/documentations/Systemd


LINUX : SYSTEMD - Introduction


pid1 = init > systemd


ps aux
ls -la /sbin/init 
ps -q 1




LINUX : SYSTEMD - Introduction



Management de différents daemons :

  * logind
  * systemd
  * journald
  * networkd
  * resolvd
  * ...




Ordonne et Parallélise le démarrage (gain de temps)




LINUX : SYSTEMD - Introduction


Leur configuration se découpe par unités :


systemctl -t help
systemctl list-units




LINUX : SYSTEMD - Introduction


	* service : process
	* socket : socket réseau de communication & IPC
	* target : regroupement de plusieurs unités (association au runlevel & ordonnancement)
	* mount : les montages en complément de fstab
	* automount : comme autofs (montage à la demande)
	* timer : équivalent des crons
	* device : pour la gestion des devices
	* scope : gestion de groupes au sein de systemd
	* slice : gestion des cgroups
	* snapshot : sauvegarde de l'état des services (systemd)
	* swap : montage de la swap (cf vidéo mémoire plus tard)
	* session
	* path




LINUX : SYSTEMD - Introduction



Suite de d'utilitaires/programmes

  * systemctl
  * journalctl
  * sysctl
  * resolvectl
  * hostnamectl
  * ...






LINUX : SYSTEMD - Introduction


systemctl list-units -t service
man systemd.service




LINUX : SYSTEMD - Introduction


systemctl get-default
systemctl list-dependencies
systemd-analyze blame




LINUX : SYSTEMD - Introduction

Les principaux répertoires de configurations :
à éviter de modifier :
* /usr/lib/systemd/system/
* /lib/systemd/system/
à modifier et compléter :
* /etc/systemd/system/
* /run/systemd/system/
Format de nombreux fichiers en .ini



LINUX : SYSTEMD - Hostname & HostnameCTL


hostname : nom du serveur localement


echo $HOSTNAME
hostname
sysctl kernel.hostname


Note : si modif de sysctl non préservé au reboot


LINUX : SYSTEMD - Hostname & HostnameCTL


la commande hostname


hostname
hostname -i
hostname -I
hostname -d
hostname -f




LINUX : SYSTEMD - Hostname & HostnameCTL


un daemon hostnamed géré via un service (unité)


man systemd-hostnamed
sudo systemctl status systemd-hostnamed.service




LINUX : SYSTEMD - Hostname & HostnameCTL


redirige sur l'interface locale (vidéo network plus tard)


ping $HOSTNAME




LINUX : SYSTEMD - Hostname & HostnameCTL


gérez dans un fichier de configuration


cat /etc/hostname


Note : si changement /etc/hosts aussi


LINUX : SYSTEMD - Hostname & HostnameCTL


avec hostnamectl le nom standard


hostnamectl status
hostnamectl --static
hostnamectl set-hostname doki1
hostnamectl --static
cat /etc/hostname




LINUX : SYSTEMD - Hostname & HostnameCTL


définir un pretty hostname


hostnamectl --pretty set-hostname "Xavki Computer"
hostnamectl --pretty
cat /etc/machine-info




LINUX : SYSTEMD - Hostname & HostnameCTL


définir une localisation (Rack, DC, U, immeuble, bureau...)


hostnamectl set-location "XavCave"


LINUX : SYSTEMD - Premier Service

Qu'est-ce qu'un service systemd ?

* un type d'unité systemd

* un programme (processus... ou plusieurs)

* un daemon (tourne en tâche de fond)

* l'unité pour manager les daemons (start/stop/boot...)




LINUX : SYSTEMD - Premier Service

Localisation des fichiers de configuration des services

* /etc/systemd/system : configuration locale
* /run/systemd/system : configuration du runtime
* /lib/systemd/system : configuration "packagée"
* /usr/lib/systemd/system/




LINUX : SYSTEMD - Premier Service

Constitution d'une configuration de service

[Unit]
Description=My app
[Service]
Type=simple
ExecStart=/usr/bin/sleep infinity
[Install]
WantedBy=multi-user.target




LINUX : SYSTEMD - Premier Service

Description : quelques mots sur l'unité en question (multi unités)
Service : type d'unité (informe sur le type de comportement attendu)
ExecStart : le process lancé et ses options et arguments
Wanted-By : niveau de runlevel (utile pour démarrer le programme auto)
Rq: toute édition d'un fichier de conf systemd nécessite

systemctl daemon-reload




LINUX : SYSTEMD - Premier Service


les commandes systemctl de base : lister


systemctl
systemctl list-units
systemctl list-units --type service




LINUX : SYSTEMD - Premier Service


arrêter ou démarrer un service


systemctl start hello
systemctl status hello
systemctl stop hello
systemctl restart hello




LINUX : SYSTEMD - Premier Service

D'autres :

reload : demande aux daemons de recharger leur configuration (si possible)
try-restart : essaie de redémarrer une unité déjà démarré (pas si stopped)
reload-or-try-restart : essaie de reload sinon restart


ExecReload=/usr/bin/bash -c '/usr/bin/touch /tmp/xavki-$$(date +%%Y%%m%%d%%H%%M%%S)'




LINUX : SYSTEMD - Premier Service


activer le démarrage au boot de la machine


systemctl enable hello
systemctl disable hello




LINUX : SYSTEMD - Premier Service


vérifier le status (vérification via le code retour)


systemctl is-active hello
systemctl is-failed hello


LINUX : SYSTEMD - Statuts des Services

Lister les services

systemctl -t service
systemctl list-units -t service



* load : l'unité a été lancée

* active : englobe les états

* sub : état détaillé




LINUX : SYSTEMD - Statuts des Services

Lister les états

systemctl list-unit-files
sudo systemctl list-unit-files hello.service




LINUX : SYSTEMD - Statuts des Services

Liste des States

* bad : dans le cas de problème avec systemd

* disabled : non lancé au boot

* enabled : lancé au boot

* indirect : disabled mais enabled via une autre unité

* linked : l'unité disponible via un lien symbolique

* masked : non disponible à systemd (masqué)

* static : sans bloc INSTALL




LINUX : SYSTEMD - Statuts des Services


masked


sudo mv /etc/systemd/system/hello.service /lib/systemd/system/
sudo systemctl mask hello



linked


sudo systemctl link /etc/hello.service


LINUX : SYSTEMD - Edit & Override


lister les propriétés d'une unité


sudo systemctl status hello
systemctl show hello.service --all




Visualiser la valeur d'une propriété


systemctl show hello.service --property ExecStart,Description




LINUX : SYSTEMD - Edit & Override


Surcharger une propriété


systemctl edit hello.service
systemctl edit hello.service --full


Note : attention se base sur le fichier override.conf


LINUX : SYSTEMD - Edit & Override


surcharger des propriétés


/etc/systemd/system/hello.service.d/override.conf




Ajout d'une propriété (exemple: After)


Override properties (exemple : ExecStart)


/etc/systemd/system/hello.service.d/override.conf



LINUX : SYSTEMD - Types de Services


man systemd.service


Objectif : comment apprécier le caractère actif du service ?


LINUX : SYSTEMD - Types de Services

Types :

* oneshot : pour lancer une fois (exemple au démarrage), reste en attente

* exec : lancement d'un simple process vérifié sur le simple execve

* simple : daemon d'un simple process (classique) - attente de fork (1er)

* forking : l'ExecStart doit utiliser le syscall fork()

* dbus : reste actif tant que le bus est utilisé

* notify

* idle

* exec




LINUX : SYSTEMD - Types de Services


OneShot


[Unit]
Description=My Hello app
[Service]
Type=oneshot
ExecStart=/usr/bin/sleep 10
RemainAfterExit=true
[Install]
WantedBy=multi-user.target


Note : attention Remain After Exit (garde le caractère actif)


LINUX : SYSTEMD - Types de Services


Exec (attend le syscall execve)


[Service]
Type=exec
ExecStart=/usr/bin/sleep infinity




LINUX : SYSTEMD - Types de Services


Simple (attend le fork de systemd)


[Service]
Type=Simple
ExecStart=/usr/bin/sleep infinity




LINUX : SYSTEMD - Types de Services


Idle


[Service]
Type=Idle
ExecStart=/usr/bin/sleep infinity


Note : évite de lancer le service en même temps
* attend que d'autres process en cours d'activation
* lancement au bout de 5s quand même


LINUX : SYSTEMD - Types de Services


Forking (attend le syscall fork() )


[Service]
Type=forking
ExecStart=/bin/bash -c '/usr/bin/sleep 2s; /usr/bin/sleep 500s &'




LINUX : SYSTEMD - Types de Services


Notify


[Service]
Type=notify
ExecStart=bash -c '/usr/bin/sleep 20s; systemd-notify --ready; /usr/bin/sleep infinity'
NotifyAccess=all




LINUX : SYSTEMD - Types de Services


D-Bus


[Service]
Type=dbus
BusName=dev.jambor.Test
ExecStart=bash -c 'sleep 2; dbus-test-tool echo --system --name=dev.jambor.Test'



LINUX : SYSTEMD - Propriétés de Restarts & Fails


man systemd.service


Objectif : comment permettre de l'auto-guerisson de vos services ?


LINUX : SYSTEMD - Propriétés de restart & Fails

Deux endroits pour ajouter des propriétés :

* le [Unit]

* le [Service]



[Unit]
Description=My app Hello
[Service]
ExecStart=/usr/bin/sleep 10s
[Install]
WantedBy=multi-user.target




LINUX : SYSTEMD - Propriétés de restart & Fails
[Service]


le simple restart peu importe l'exit (exemple : sleep)


Restart=always (exit)



le simple restart sur un fail (exi diff de 0)


Restart=on-failure (exit != 0)


Note: mais nécessité de prise en compte du comportement du programmea
Restart=on-abnormal


LINUX : SYSTEMD - Propriétés de restart & Fails
[Service]


temps d'attente entre les restarts (valeur par défaut)


RestartSec=1




LINUX : SYSTEMD - Propriétés de restart & Fails
[Service]


limiter la durée d'un service (mais restart potentiel)


[Service]
RuntimeMaxSec=180s




LINUX : SYSTEMD - Propriétés de restart & Fails
[Unit]


défaut si Restart=always


[Unit]
StartLimitBurst=5 (nombre de fois en fail)
StartLimitIntervalSec=10 (5 fois dans l'interval de 10s)


Rq : et si RestartSec=3 > jamais les 5 fois :)
La solution simple qui fonctionne toujours est de définir StartLimitIntervalSec=0.
RestartSec à au moins 5 secondes, pour éviter de mettre trop de stress


LINUX : SYSTEMD - Propriétés de restart & Fails
[Unit]


pour limiter le nombre de restart (2)


[Unit]
Description=My app Hello
StartLimitBurst=2
StartLimitIntervalSec=300
[Service]
ExecStart=/usr/bin/sleep 10s
Restart=always
RestartSec=5s
[Install]
WantedBy=multi-user.target




LINUX : SYSTEMD - Propriétés de restart & Fails
[Unit]


pour cadencer les restart sans les limiter du tout


[Unit]
Description=My app Hello
StartLimitBurst=2
StartLimitIntervalSec=300
[Service]
ExecStart=/usr/bin/sleep 10s
Restart=always
RestartSec=5s
[Install]
WantedBy=multi-user.target




LINUX : SYSTEMD - Propriétés de restart & Fails
[Unit]


redémarrer le serveur en cas de fail :


[Unit]
Description=My App
StartLimitIntervalSec=30
StartLimitBurst=2
FailureAction=reboot


SuccessAction=
StartLimitAction=reboot > reboot si startlimitaction activé (burst/interval)
OnFailure=my-app-recovery.service


LINUX : SYSTEMD - Les Dépendances


man systemd.service


Objectif : comment permettre une dépendance entre vos services ?

gérées par le [Unit]



LINUX : SYSTEMD - Les Dépendances

Deux services hello1 et hello2

[Unit]
Description=Hello
[Service]
Type=simple
ExecStart=/usr/bin/sleep 50s
[Install]
WantedBy=multi-user.target




LINUX : SYSTEMD - Les Dépendances

Différentes propriétés de la section Unit :

* After

* Before

* Wants

* Requires

* Requisite

* BindsTo

* PartOf

* Conflicts



systemctl list-dependencies test.service --all --reverse




LINUX : SYSTEMD - Les Dépendances

After : lancé après peu importe l'état (ordre)

Before : idem mais après

Wants : devrait être activée avec d'autres unités (non obligatoire)

Requisite : n'inclus pas de notion d'ordre (même transaction > After)


LINUX : SYSTEMD - Les Dépendances

PartOf : dépendance au restart et stop

start de hello1 rien sur hello2


systemctl stop hello1 hello2
systemctl status hello1 hello2
systemctl start hello1



stop de hello1 entraine stop de hello2


systemctl start hello1 hello2
systemctl status hello1 hello2
systemctl stop hello1




LINUX : SYSTEMD - Les Dépendances

Requires :

* démarrage des services listés

* arrêt sur un des services listés



démarrage des services listés


systemctl stop hello1 hello2
systemctl status hello1 hello2
systemctl start hello1
systemctl status hello1 hello2 # pas de dépendance
systemctl stop hello1
systemctl start hello2 
systemctl status hello1 hello2 # dépendance



arrêt d'un des services listés


systemctl start hello1 hello2
systemctl status hello1 hello2
systemctl stop hello1




LINUX : SYSTEMD - Les Dépendances

BindTo :

* démarrage des services listés

* arrêt sur un des services listés

* mais sur failed du service listé stop



systemctl start hello1 hello2
systemctl status hello1 hello2
kill -9 <pid_service_listé>




LINUX : SYSTEMD - Les Dépendances

Conflicts :

* si hello1 est activé alors b est inactivé

* inversement


LINUX : SYSTEMD - Gestion de l'environnement


man systemd.service


Objectif : Comment changer le répertoire de travail, variables d'env ?

gérées par le [System]



LINUX : SYSTEMD - Gestion de l'environnement


WorkingDirectory


echo "Test WorkingDirectory" > /tmp/xavki.txt



[Service]
Type=simple
WorkingDirectory=/tmp/
ExecStart=/usr/bin/cat xavki.txt


Note : ne fonctionne pour le chemin (path) vers le script


LINUX : SYSTEMD - Gestion de l'environnement


les permissions sur les répertoires :


[Service]
Type=simple
ExecStart=/usr/bin/ls /home/oki
InaccessibleDirectories=/home


ReadWriteDirectories=
ReadOnlyDirectories=
Note : ajouter "-" pour éviter une erreur si non existant


LINUX : SYSTEMD - Gestion de l'environnement


protection de la home (true/false/read-only)

ProtectHome > /home/ ou /run/user/ non accesible

ProtectSystem (true/false/full) :

ProtectSystem > /usr/ en read-only
* si full, /etc/ aussi


LINUX : SYSTEMD - Gestion de l'environnement


le répertoire temporaire privé (True/False)


[Service]
Type=simple
ExecStart=/bin/bash -c "echo toto > /tmp/xavki.txt"
PrivateTmp=True


Note :
* pour la sécurité, suppression /tmp/ & /var/tmp/ du process
* idem pour les networks & pour les devices


LINUX : SYSTEMD - Gestion de l'environnement


répertoire dédié au process (clean au stop)


[Service]
Type=simple
ExecStart=/usr/bin/sleep infinity
RuntimeDirectory=xavki


RuntimeDirectoryMode : pour spécifier le mode (permissions sur le répertoire)


LINUX : SYSTEMD - Gestion de l'environnement


définir des variables d'environnement

Environment=NODE_ENV=production PORT=1494

[Service]
Environment=ENV=production APP=myapp
Type=simple
ExecStart=/bin/bash -c "/usr/bin/echo $ENV; /usr/bin/echo $APP"




LINUX : SYSTEMD - Gestion de l'environnement


par fichier

EnvironmentFile=/etc/myapp/environment

[Service]
EnvironmentFile=/etc/myapp/environment
Type=simple
ExecStart=/bin/bash -c "/usr/bin/echo $ENV; /usr/bin/echo $APP"


LINUX : SYSTEMD - les Exec & user/group


man systemd.service


Objectif :

gérées par le [System]



LINUX : SYSTEMD - les Exec

ExecStart

ExecStop

ExecReload


LINUX : SYSTEMD - les Exec

ExecStartPre

ExecStartPost

ExecStopPost


LINUX : SYSTEMD - les Exec


Exemple :


#/etc/systemd/system/test.service
[Unit]
Description=Test Systemd Service
[Service]
ExecStartPre=/usr/bin/echo -e "\033[0;33m Pre start \033[0m"
ExecStart=/usr/bin/sleep 20;/usr/bin/echo -e "\033[0;33m Pre start \033[0m"
ExecStartPost=/usr/bin/echo -e "\033[0;33m Post start \033[0m"
ExecStop=/usr/bin/pkill -f sleep
ExecStopPost=/usr/bin/echo -e "\033[0;33m Post stop \033[0m"
ExecReload=/usr/bin/echo -e "\033[0;33m Reload \033[0m"
[Install]
WantedBy=multi-user.target




LINUX : SYSTEMD - les Exec


si exit normal du programme


RemainAfterExit=true




LINUX : SYSTEMD - les Exec


préciser le user et le group


User=oki
Group=oki




LINUX : SYSTEMD - les Exec


action sur le MAINPID


ExecStop=/usr/bin/kill -TERM $MAINPID
ExecReload=/bin/kill -HUP $MAINPID


Note : si forking utilisation de PIDFile=


LINUX : Les LOGS

Objectif : Consulter les logs des applicatifs gérés par systemd ?


LINUX : Les LOGS

C'est quoi des logs ??


* enregistrement des actions réalisées par les applicatifs




* historique




* idem pour les programmes dédiés au système




* permet de débuguer (retrouver la cause et corriger)




* par défaut les logs sont centralisés dans /var/log/




LINUX : Les LOGS


* rotation de logs : cycle de compression des logs



syslog
syslog.1
syslog.2.gz
syslog.3.gz




LINUX : Les LOGS


* types : 
		* Application Logs
		* Event Logs
		* Service Logs
		* System Logs




* format : syslog



<timestamp> <user> <service/app[pid]> <message>




LINUX : Les LOGS


/var/log/boot.log : logs de démarrage



/var/log/cron.log : logs dédiés aux crons



/var/log/auth.log (secure) : les logs d'authentification/session et l'utilisation du sudo



/var/log/syslog : tous les messages sauf auth



LINUX : Les LOGS


/var/log/messages : tous les messages non critiques



/var/log/kern.log : les logs du kernel



/var/log/dmesg (dmesg) : les logs relatifs au device driver



/var/log/mail.log : logs relatifs au serveur de mail



/var/log/daemon.log : logs des services tournant en arrière plan

Note : https://fr.wikipedia.org/wiki/Syslog



LINUX : SYSTEMD - Logs & Journalctl


man systemd.service


Objectif : Consulter les logs des applicatifs gérés par systemd ?


LINUX : SYSTEMD - Logs & Journalctl


journalctl : consulter vos logs via une commande


journalctl




pour une unité


journalctl -u hello2




l'équivalent de tail


tail -f /var/log/syslog
journalctl -fu hello




LINUX : SYSTEMD - Logs & Journalctl


par applicatif


journalctl /usr/bin/sleep




par log level


journalctl -p err




cumuler


journalctl /usr/bin/sleep -u hello1




LINUX : SYSTEMD - Logs & Journalctl


par date


journalctl --since "2022-01-01 01:00:00" --until "2022-09-21 18:13:00"




mode courant


journalctl --since yesterday
journalctl --since "1 hour ago"




sortie json


journalctl -u hello2 -o json




LINUX : SYSTEMD - Logs & Journalctl


logs level

0 	Emergency 	emerg 		: système non utilisable
1 	Alert 	alert 				: correction à apporter immédiatement
2 	Critical 	crit 				: conditions critiques (hardware)
3 	Error 	err 					: erreur
4 	Warning 	warning 		: précvention
5 	Notice 	notice 				: pas de problème mais à noter
6 	Informational 	info 	: information
7 	Debug 	debug 				: maximum d'information


LINUX : SYSTEMD - Logs & Journalctl


utilisation de syslog (défaut)


StandardOutput=syslog
StandardError=syslog




spécifier une autre destination


StandardOutput=append:/var/log/xavki.log
StandardError=append:/var/log/xavki_err.log


inherit, null, tty, journal, kmsg
journal+console, kmsg+console
file:path, append:path, truncate:path, socket, fd:name


LINUX : SYSTEMD - Logs & Journalctl


définir un identifiant spécifique


SyslogIdentifier=xavki




ajouter des champs


LogExtraFields




limiter le nombre de messages par intervales


LogRateLimitIntervalSec
LogRateLimitBurst


LINUX : SYSTEMD - Les Templates

Objectif : Et si j'ai des services que je veux instancier ?
Avec une seule unité ?


LINUX : SYSTEMD - Les Templates


un service simple sans template


<service_name>.service




un service simple avec template


<service_name>@<argument>.service


Note : argument = instance = variable réutilisable dans la configuration
Attention : le nom du fichier doit aussi comporter le @


LINUX : SYSTEMD - Les Templates


deux formats de variables possibles:

%i : échappe les caractères spéciaux
%I : sans échappemement


LINUX : SYSTEMD - Les Templates


et d'autres variables


    %n: nom de l'unité
    %N: idem %n mais avec échappement
    %p: préfix de l'unité (ex: hello) avant le @
    %P: idem %p mais avec échappement
    %f: nom de l'instance de l'unité avec un / devant
    %c: indique le contrôle group (cgroup) d'appartenance
    %u: nom du user qui lance l'unité
    %U: UID du user qui lance l'unité
    %H: le nom du serveur où a été lancé l'unité (hostname)



LINUX : SYSTEMD - Les Templates

Objectif : Et si j'ai des services que je veux instancier ?
Avec une seule unité ?


un service simple sans template


<service_name>.service




un service simple avec template


<service_name>@<argument>.service


Note : argument = instance = variable réutilisable dans la configuration
Attention : le nom du fichier doit aussi comporter le @


deux formats de variables possibles:

%i : échappe les caractères spéciaux
%I : sans échappemement


et d'autres variables


    %n: nom de l'unité
    %N: idem %n mais avec échappement
    %p: préfix de l'unité (ex: hello) avant le @
    %P: idem %p mais avec échappement
    %f: nom de l'instance de l'unité avec un / devant
    %c: indique le contrôle group (cgroup) d'appartenance
    %u: nom du user qui lance l'unité
    %U: UID du user qui lance l'unité
    %H: le nom du serveur où a été lancé l'unité (hostname)


Alias=
Also=
WantedBy=
RequiredBy=
DefaultInstance=
AssertPath




















 








































   
