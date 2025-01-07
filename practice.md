# Suivi des vidéos et utilisation pratique avec exemeple en copie d'écran 

## Les différentes couches systèmes 

![image](https://github.com/user-attachments/assets/1a7af8a7-873a-4117-8f47-bf0167f0eccc)

## du bios à l'init, phase d'initialisation


![image](https://github.com/user-attachments/assets/433cdea9-8e3a-4269-9ef4-7733d5f273f9)

## Linux terminal versus console versus shell

>> Terminal : device qui va servir à communiquer avec la machine
il va prendre des input (clavier souris) et ressortir des outputs (ecran)
>> TTY > teletypewriter 

## commandes associées 

![image](https://github.com/user-attachments/assets/9b9c6551-8170-461a-8807-4ee47f4d04a9)

stty -a pour avoir les caractéristiques de son tty

On peut écrire sur un terminal si on a les droits 

```
echo "toto" > /dev/tty2
```
## Console 

>> accès physique au terminal primaire
>> pas besoin d'accès réseau, dernier ecours si perte de connexion totale

## Shell 

>> interpréteur de commande pour communiquer avec le kernel
>> langage pour commmuniquer avec le noyau

>> différents type : sh ; bash ; zsh

```
echo $SHELL
```

# Linux : commandes de bases et hiérarchie du filesystem

FHS pour Filesystm hierarchy standard (V3 en 2015). 
Repose sur le disque et le format

## Fonction couramment utilisées 

>> / pour le répertoire racine
>> ~ home du user courant = /home/bob pour moi
>> .. répertoire parent
>> . répertoire actuel

## Hiérarchie de systeme de fichier 

![468945985_4109731389307332_8570483096162121247_n](https://github.com/user-attachments/assets/90105381-39d1-48ae-a1c2-c5895ac53fa4)


# Le man ou RTFM read the fucking manuel

>> man man pour le manuel


>> Raccourci dans les options ; -a = -all etc

>> man -L fr man pour le français (pas toujours)

## Comment chercher dans le man

>> man -k <recherche>
>> apropos <recherche> : la même chose 

![image](https://github.com/user-attachments/assets/b5e2df53-3e21-40b1-b155-06a2182eb2b0)

>> recherche dans une page : /<terme>
>> puis n pour avancer ou N pour reculer
>> G pas de page et g haut de page

## Commandes usuelles

>> rmdir pour supprimer les directory
>> rm -i pour avoir confirmation
>> cp et mv ; on prend tous les premiers arguments et on les met dans le dernier
>>
>> touch ; créé ou met a jour la date du fichier
>> date 


## Permissions de fichiers 

![linuxfilespermission](https://github.com/user-attachments/assets/1e6c0fa6-16f1-4b8a-99f5-77da01a8b356)

3 cooamndes : 
>> LS ou stat ou getfacl pour voir les permissions

![image](https://github.com/user-attachments/assets/e442c133-1b2a-45aa-bf12-19ba2c955020)

>> Pour le filetype en premier il existe :
>> d : directory
>> c character device
>> l symlink
>> s socket
>> b block device
>> d door
>> p named pipe
>> - file

## commandes pour modifier les permissions 


>> chmod -R recurcive et -c mode verbeux et affiche uniquement les modif qui ont été faites
>> chmod 777 pour ajouter tous
>> chmod +r ou +x ou +w pour appliquer a tous les users
>> chmod o-w >> ici on enlève le mode writer pour le groupe other sinon u et g pour les 2 autres groupes



>> chown 

![image](https://github.com/user-attachments/assets/6f105d20-990c-4eae-a199-9ceea76521d9)

ICi on va changer le user en 1, puis le user et le group en les séparant avec : 

>> chgroup peu utilisé

 
# VI et VIM 

>> mode visuel ctr + v

>> G pour descendre en bas de page
>> gg pour le haut de page
>> / pour recherche et n pour l'occurence d'après m pour avant
>> : set number pour afficher les lignes
>> u undo
>> :undo et : redo pour avant après
>> supprimer des  lignes dd ou 10dd pour supprimer 10 lignes
>>
>>  copier coller
>> yy
>> p
>> ou pour copier coller 3 lignes
>> 3yy
>> p
>> rempalcer drs iterations
>> :%s/mat/mathieu/g % va supprimer toutes les occurences
>> mode visuel : ctr + v utile pour plusieurs bloc
>> ctr + v on selectionne les blos que l'on veut, pour "maj +i" pour revenir au début et faire ce que l'on veut, exemple rajouté un #, puis échap et ça rajoute dièse sur toutes les lignes
 

## Su sudo 

en fonction du user, on a pas le même environnement 


>> su pour switch user
>> su - pour switcher d'env aussi

![image](https://github.com/user-attachments/assets/c7c005a6-19d7-48ce-b03a-d23617a71e5a)

conf ici : /etc/sudoers

>> pour modif cela, on use VISUDO et on ouvre un second terminal pour éviter de perdre l'accès a la machine si on se trompe


![image](https://github.com/user-attachments/assets/754de823-aaa6-422f-bed5-aa7c942b5f75)


# Users et group 

UID et GID identifiant unique pour les groups et les users

UID : 
>> 0 root
>> 0 -100 : mode statique pour le systeme
>> <1000 dynamique mais reserrvé pour le systeme (user créé pour lancé un process et applicatif)
>> >1000 autres
>> nobody : valeur max définie (montage de filesystem ou docker)


GID : géré un ensemble de user
>> 0 pour le groupe root
>> 100 pour le groupe par défaut (users)
>> groupe utilisateur à partir de 1000

![image](https://github.com/user-attachments/assets/e6ebcd1e-5678-457e-9957-88fdbd5edc2c)

lister les groupes : 

>> cat /etc/group
>> getent group

créé un group : sudo groupadd ; 

fichier de conf pour groupadd ; /etc/login.defs mais ne jamais y toucher 

>> groupdel pour supprimer un group

>> Pour les users : On ne créé pas la home automatiquement ni le password,
>>
>> -m pour la home
>>
>> on créé le group g2 et on le rajoute au groupe docker

>> si utilisateur system, on peut mettre un /bin/nologin pour le bash par defaut donc aucun bash fourni pour une intéraction
>>
>> 
![image](https://github.com/user-attachments/assets/d35bf13e-7454-40f4-9488-b20303ae74a2)

>> adduser différent, fonctionne de manière interactive donc pas ouf en infra as code
>>
>> passwd pour modifier les mot de passe


# Enviroonement et variables 
```
login
```
login qui permet de débuter une session sur le systeme, il se base sur /etc/passwd pour afficher les infos de SHELL, USER ...

conf /etc/login.defs 

>> 2 types : interactif ou non
>>
>> shell login vs non login
>>
>> après lancement de login, scripts autocompletion etc, source de variables (variables d'env, etc) d'où source bashrc quand on modifie cela


```
env
```
variables environnement visible. On peut rajouter une variable avc -i 




```
export 
```
Pour ajouter à toute une session 

>> Cheminement de fichier définnissant l'environnement : pour tous les users
>> /etc/profile
>>
>> personnalisable dans /etc/profile.d/
>>
>> Pour chaques users : 

>> ~/.bash_profile
>> ~/.bashrc pour export ou alias tout le temps puis sourcé le fichier source ~/.bashrc ou . ~/.bashrc c'est pareil
>>
>> ~/.bash_logout quand on ferme la session


# MOTD & ISSUE & LOGOUT 

## avant le login >> ISSUE


>> prelogin message : attention sécurité ;

>> /etc/issue fichier de conf en sudo 



## après login >> MOTD (message of the day)
>> 

![image](https://github.com/user-attachments/assets/0d2dcacd-4ce0-43b3-8e1e-be539c25ad4e)

On peut créé des scripts dans /etc/profile.d/ qui vont être lu au démarrage

![image](https://github.com/user-attachments/assets/690689ed-6339-4627-a43b-c51bc3ce13f0)

>> PAr exemple ici, on le nom de la machine et l'ip



## LOGOUT 

```
~/.bash_logout
```

Ici pour modifier cela


# UMASK et SKEL 

D'ou viennent les fichiers qui sont dans ma home etc, 

La dans la conf de l'ajout de user : 

![image](https://github.com/user-attachments/assets/b854d64d-8fd2-4a60-bd52-686a6e6f0085)

On a un paragraphe sur le SKEL à /etc/skel

![image](https://github.com/user-attachments/assets/e7d66c46-f4bb-462f-8f8e-3570054ff12e)


>> aspect comportement par défaut : UMASK

>> dans /etc/login.defs

>> ![image](https://github.com/user-attachments/assets/57e367f5-f7b1-4841-805c-0eddae5debba)

![image](https://github.com/user-attachments/assets/aa3b3cde-6e1a-4e2d-8757-8f50c98cfff4)

Ici on affiche pour les fichiers et avec -S pour les dossiers

>> On peut définir avec la commande umask, ce qui va soustraire de 666 et 777 ce que l'on met 

# Date et time 

notion de format et localisation : 

CEST : central européen summer time 
UTC : universal tome coordinated
RTC : a disparaitre Rreal time cloack 

Format epoch : commence le 01 01 1970 en seconde (timestamp en monitoring) limité en 32bits en 2038. 

## temps de la machine vs temps du système 

machine : horlohge RTC, bios, pile 
systeme : prise en compte des fuseaux horaires, etc 

```
date
timedatectl
```

![image](https://github.com/user-attachments/assets/d24b0df5-9d79-44d8-822c-84192d3ebcdf)

>> format :

```
date +%Y%m%d
date +%Y.%m.%d/%H%M%s
```


![image](https://github.com/user-attachments/assets/3de3ab40-bace-49a9-b4ab-a329bb5f74ae)


>> hwclock pour gérer sur la machine, pour chznger 

```
sudo hwclock --set --date "2022-01-13 09:00:00" --utc

```

La on a modifier la hardware d'ou hwclock, on peut mettre a jour le hw ou le systeme l'un par rapport à l'autre 

![image](https://github.com/user-attachments/assets/31cb0911-8417-4a10-968e-b57f80d72b8c)


## Timezone 

définie à différent endroit

![image](https://github.com/user-attachments/assets/b39b683a-e015-4d20-b344-746f0151603c)


## changer de timezone : 2 méthodes

Pour lister 
```
sudo timedatectl list-timzone 
```

![image](https://github.com/user-attachments/assets/d6dae0af-0f5b-450f-a78c-b7c49d2286b4)

## Où par lien symbolique 

On va supprimer le lien symbolique pour en créer un nouveau 

```
sudo rm -rf /etc/localtime
sudo ln -s /usr/share/zoneinfo/America/New-York /etc/localtime
```

# Date et heure 

>> timedatectl encore mais on ne peut pas comme ça car on est en NTP actif

![image](https://github.com/user-attachments/assets/eadd45db-6d60-4233-88ec-ba3ff92b6b40)

Pour voir en détail : 

![image](https://github.com/user-attachments/assets/b5754985-f87d-4eb9-91b0-fd7fb9012eb1)


>> Autre protocole : TTP pls précis

# Les locales 

>> Les spécificités des localisations : format de date et heures, la monnaie, , etc

Pour les trouver : 

![image](https://github.com/user-attachments/assets/918f56fc-824d-431e-b45a-6160a2c1c3e3)


![image](https://github.com/user-attachments/assets/2e53bbfb-19a7-4659-88c6-74fb4b767d70)


Pour trouver les valeurs : 

![image](https://github.com/user-attachments/assets/4e9e96f4-47a4-4e79-8459-374bf946b654)

![image](https://github.com/user-attachments/assets/f5da766b-873e-4545-ab74-2bfbc592f99e)

```
man locale
man localctl
man update-locale
```
Modifier la disposition du clavier par exemple avec keyboard

MAJ du local

>> possible de le faire avec sudo localctl set-locale aussi


![image](https://github.com/user-attachments/assets/ea7e38d5-b1e6-4fab-853b-c159e09571f5)


>> spécifique pour un user : avc EXPORT dans le ~/.bashrc

>>> Modif clavier

```
setxkbmap fr ou us
```

# Les types de fichiers

![image](https://github.com/user-attachments/assets/69734a52-f6b4-46b8-b2d5-0e7f3ac840a8)


![linux file](https://github.com/user-attachments/assets/57eb3381-7fd4-4d93-a62e-2b6f0c0d5a20)


![image](https://github.com/user-attachments/assets/c08a1cba-0d3e-4d6e-8170-a542fc65e375)


![image](https://github.com/user-attachments/assets/67883655-7164-4e7d-a0d5-30980ff6e633)


Pour les répertoires : on voit les liens qui changent par rapport aux fichiers 

![image](https://github.com/user-attachments/assets/83164501-9341-47f6-87c4-66214f2a1034)


## Hard link  ln 

>> lien vers l'inode ils ont le même inode. 

![image](https://github.com/user-attachments/assets/f364622e-db6b-4025-a57a-d8fcc3ba44b7)


Si on supprime un fichier, le second est toujours là car on supprime juste l'accès à l'inode 'un fichier. 

> Lien sybolique avec ln -s 

![image](https://github.com/user-attachments/assets/f3ea09c0-2133-4cda-8c9b-25e5dab55d93)

Ici, si on supprime le lien donc ici, titi.txt, on ne peut plus y accéder 

![image](https://github.com/user-attachments/assets/0048ce5c-cc7f-408d-8f35-b1e45d17f2bd)


## Device char ou block

![image](https://github.com/user-attachments/assets/ce6424d5-60ce-4e5b-964f-6125c92f5a01)


![image](https://github.com/user-attachments/assets/b15f6af3-0b42-4744-85bf-d51ad7cf7c41)

# Locale domain socket

socket = connexion entre processus

socket interne ou socket réseau

créé par syscall

man 2 socket >> 2 car syscall

# Named PIPE 

>> différent du pipe, même fonctionnement mais attention

![image](https://github.com/user-attachments/assets/95d9cfb5-a753-4fde-8514-72a3ea802e63)


![image](https://github.com/user-attachments/assets/af04af63-9ef4-45b6-bc12-611bd840da26)

Protocole fifo pour first in first out 

# Déplacer copier et compresser 

>>> cp mv tar 

cp avec backup cp -b

cp -p pour preserver les permissions si on est root par exemple 

 # Stat block inodes et fichiers
 
![image](https://github.com/user-attachments/assets/c1294beb-812b-4b68-9634-89db90e33178)


>> notion de block : filesystem découpé en morceaux : block ; chaque block device dispoe d'une taille de block

>> lsblk pour voir les block


>> pluseiurs niveaux de block : disk block size : 512 ou data block 4096(4k)

>> inodes : pointeurs vers les data blocks 

>> Process de lecture d'un fichier :
>> 1 lire l'inode
>> 2 trouver l'inode dans la table des inodes
>> 3 lire les infos de l'inode
>> 4 récuération de la localisation des blocks
>> 5 lecture des data blocks

Le cache va ici permettre de recherche plus vite un fichier en sautant des étapes ici. 


# Montage d'un disque

>> sur virtualbox créé un disque virtuel et ajouter à la machine 

>> lister les disques

sudo fdisk -l | more 

![image](https://github.com/user-attachments/assets/48b5f757-4ba6-47bd-becc-bb7c8aa8ac26)


>> formater le disque 

mkfs.ext4 /dev/sdb

![image](https://github.com/user-attachments/assets/56fa2017-8e6c-44da-85f0-dbacd91e8ff8)

>> Monter le disque sur le filesystem
Si on ferme la machine, on perd le montage si on ne persiste pas


>> mount -t ext4 /dev/sdb /srv/mat/

![image](https://github.com/user-attachments/assets/7bf8a196-1b63-49c9-acc3-9501c404f3da)

On peut le voir avec la commande mount 

![image](https://github.com/user-attachments/assets/76aff31e-0550-4db1-935e-31b07ae81b08)

![image](https://github.com/user-attachments/assets/5c936632-b2ca-41d5-92d1-ad9b97a417eb)

#DF pour diszk free

![image](https://github.com/user-attachments/assets/0c6fcd14-5b3d-4fce-acdd-828352869700)

![image](https://github.com/user-attachments/assets/ee980c51-663c-4fd3-91f7-ff37ccae5fa4)

>> différente option de df

![image](https://github.com/user-attachments/assets/4f84f8e4-6ae5-4154-ad08-e93fa6c171f7)

umount pour démonter 

![image](https://github.com/user-attachments/assets/e2141290-e392-4c93-902b-94de253c628e)


# commande DD 

copie un disque de block a block 

>> exemple avec la commande status pour voir en cours : 

![image](https://github.com/user-attachments/assets/f1769968-385d-4399-b8fe-13608a487d7a)

on peut copié au formay image aussi : 

![image](https://github.com/user-attachments/assets/80f6a8aa-ab79-4be7-a358-aabab615880f)

![image](https://github.com/user-attachments/assets/05059aff-2215-4c91-bdd4-170d70cec59b)

cleané un disque : on peut le faire de block à block aussi

![image](https://github.com/user-attachments/assets/257e3299-78e8-43b0-b0b4-422dea1c231e)

et restoration : 

![image](https://github.com/user-attachments/assets/27ed64c1-23f9-4042-96f5-8df9354e894a)


# Mount et fstab : option bind fail sur reboot

>> cat /etc/fstab permet de rendre permanent les montage de mount 


![image](https://github.com/user-attachments/assets/3a2ea60d-b59c-48cf-9ea4-4e0446a2225d)

pour lister les uuid : sudo blkid ou sudo lsblk -fe7


![image](https://github.com/user-attachments/assets/b8add8ef-0a8f-46ad-9775-2233b2d67ef5)

![image](https://github.com/user-attachments/assets/90485d68-a6bb-44c7-ab64-257059a49775)

no fail !! TRES IMPORTANT évite le plantage du du PC au boot si le disque n'est pas OK

Exemple ici : si on monte un sdb dans /etc/fstab et qu'on supprime le disque dans virtual box ; 

![image](https://github.com/user-attachments/assets/c852ce19-2529-4181-aaee-da856fcab4a1)

on fait quoi ? idem que root mot de passe 

édite le grub : 

on ça : 

![image](https://github.com/user-attachments/assets/d562c5c1-1b1f-4b5e-896b-a20f500a5d3f)

On va modifié cela en rajoutant init=/bin/bash pour avoir un bask de dispo : puis ctrl + X pour fermer

Attention qwerty 

![image](https://github.com/user-attachments/assets/957d76d5-03d2-4083-91f6-e0f26ae6d7e8)

![image](https://github.com/user-attachments/assets/133f4f49-21dc-4fcb-bac5-5782a3c5b1a3)

![image](https://github.com/user-attachments/assets/dd27f75f-8f5e-4b3b-8dfb-6979d39e9437)

puis on relance l'init avec : 

![image](https://github.com/user-attachments/assets/1a96ebd0-76b0-4aef-9dcc-8dab6e772817)

montage de type bind monter un répertoire dans u nautre : 

![image](https://github.com/user-attachments/assets/3441d0cf-cd80-44b9-82ba-53045fc0465c)

>> findmnt permet de voir les montages avec arborescence

![image](https://github.com/user-attachments/assets/e45c86c2-bad1-4384-b8dc-34822d2b72b0)

# première partition et redimensionnement 

>> étendre partition / ou modifier

![image](https://github.com/user-attachments/assets/cd875cd7-07ad-430d-afdd-f0071056a452)

On fait les modif que l'on veut puis pour que le noyau linux le prenne en compte, 

>> partx /dev/sda4 puis pour vérifier


>> cat /proc/partitions

![image](https://github.com/user-attachments/assets/ef3725ef-d187-475f-b30f-e58680afe25d)

Enfin un resize : 

![image](https://github.com/user-attachments/assets/65b52901-4102-4d0c-b253-4c0aca45a928)

 #♥ Types de filesystem ext4, xfs, btrfs, zfs, ntfs... 

 
![image](https://github.com/user-attachments/assets/fa5dcb13-49c6-4252-8fa1-2813f7d4dc2c)

## EXT4 

![image](https://github.com/user-attachments/assets/2ee221ba-688d-4a0e-82d5-6c6ac6311a7e)

 ![image](https://github.com/user-attachments/assets/5a05ed34-d8fa-4ee9-b196-80670def5fa8)

![image](https://github.com/user-attachments/assets/66231357-a182-4228-bf52-5bc2fbb75cee)


## XFS 

![image](https://github.com/user-attachments/assets/8911feec-b2e6-4c8f-9c46-8464639c8155)

![image](https://github.com/user-attachments/assets/f92fff8c-615e-4886-92e2-0e51a4e16b62)

## BTRFS 

![image](https://github.com/user-attachments/assets/e5d8ab9f-ed3a-4d13-b9b2-613155a461ab)

![image](https://github.com/user-attachments/assets/c462f79a-cfb4-4cec-82a6-0cd93a0903d3)

## ZFS 

![image](https://github.com/user-attachments/assets/2ebd4bf3-e569-468f-8e50-2be96ea15cfb)


# LVM logical volume manager

principe en schéma 

![image](https://github.com/user-attachments/assets/b0eb0ade-b8f9-403d-9aed-d483e9463cd4)

Puis : 

![image](https://github.com/user-attachments/assets/cd96ae39-7635-4c33-a335-f39ac824d01d)

## Physical volume 

![image](https://github.com/user-attachments/assets/3a32fd37-9830-4915-b0ff-837c3c1cc992)



![image](https://github.com/user-attachments/assets/8fbb736d-261d-4e60-acf3-d8d303139f55)

## Volume groupe 
![image](https://github.com/user-attachments/assets/6d3f732e-331f-4fe6-b348-002a900c9dbc)

##☻ logical volume 

![image](https://github.com/user-attachments/assets/11f994b9-a596-469f-ac7c-80c59823f81c)


# LVM exemple 

exercice : rajouter 2 disque externe de 1 Go et mettre en place 2 disque virtuelles de 1.5Go et 200Mo. 

1 ) le faire sur virtual box 

2 ) sudo fdisk /dev/sdd par exemple et suivre les instructions + partitions en 8e pour lvm linux 

![image](https://github.com/user-attachments/assets/4594fdc5-bdcc-41f9-b663-f0a08e9ffa04)


![image](https://github.com/user-attachments/assets/837cc25e-fec5-4518-bd7e-acb921929957)


3 ) création des PV : 

![image](https://github.com/user-attachments/assets/9baca252-a11e-470b-9052-83d956751084)


4 ) création des volumes groupes 

![image](https://github.com/user-attachments/assets/7a572762-6b87-4fb3-96e5-9182cdf8bb88)

ou sudo vgs 

5 ) création des volumes logiques 

![image](https://github.com/user-attachments/assets/76244020-6489-4033-909e-e35821b1a35b)

6 ) on formate en ext4 

![image](https://github.com/user-attachments/assets/a640f64b-4724-4e72-a915-d0fa92a8816f)

7 ) on modifie le /etc/fstab avec sudo vim /etc/fstab

![image](https://github.com/user-attachments/assets/2e512060-b3e7-4319-939d-a896d5ff1290)



8 ) on vérifie 

![image](https://github.com/user-attachments/assets/979a5f85-fbf2-462f-9154-9718db3f2339)


# Etendre un volume logiquz et ajouter un disque 

1 on vérifie la dispo free dans les VG 

![image](https://github.com/user-attachments/assets/0daec942-ba32-4724-8523-38254ce1d62f)

2 ) on étend le VG puis on resize 

![image](https://github.com/user-attachments/assets/4e8a3675-c5c4-499a-9974-313b7f5ccc16)

# diminuer un volume logique 

1 ) check les LV et VG 

2 ) demonte le disque 

 3 ) vérifie le disque 

![image](https://github.com/user-attachments/assets/fafa21d2-c692-4647-b03a-7c78e9be4524)

4 ) on on resize le VG puis on reduce le LV, on resize et on remonte le tout 

![image](https://github.com/user-attachments/assets/edcddcc2-797f-4534-9554-73c650db3546)


# snapshot et restauration 

![image](https://github.com/user-attachments/assets/7c368e76-0ed4-4996-a614-4a9af3e1e138)

# LV strippé 

>> pas d'intérêt ici car on est sur du virtuel

![image](https://github.com/user-attachments/assets/9c4bfc13-6aec-42da-95ae-23dc363dc2c1)

# remplacer un disque 

![image](https://github.com/user-attachments/assets/812c6094-86c3-4ab1-9884-2b815d07d16c)


# Mirroring les physical volume 

avec 3 disques de même caractéristique sous virtual box, je ne le fais pas mais je suis la vidéo 
>> on fait un
```
fdsik /dev/sdc d e
partx sdc1 d1 e1
pv create /dev/sdc1 d1 e1
vgcreate vg_data /dev/sdc1 d1 
lvcreate -L 200M -n lv_mat -m 1 /dev/vg_data


```

![image](https://github.com/user-attachments/assets/9288e2ae-c589-4569-ba21-7d6aae017bf4)


# les RAID intro 

![image](https://github.com/user-attachments/assets/91dbe132-e737-4948-951f-f27ccfc5302b)

RAID phsique ou logiciel ou semi matériel

## RAID 0 ou strippé 

![image](https://github.com/user-attachments/assets/5d8c4f9b-1330-4981-8e3d-e274ed7fce21)

## RAID 1 

![image](https://github.com/user-attachments/assets/5a1de1f6-fb48-4d0a-8503-99bb339f45a3)

#" RAID 10 pour 1 et 0 

mini 4 disques 

![image](https://github.com/user-attachments/assets/b3b96206-2d74-4a82-ac13-4dbeb4732d97)

## RAID 5 

Mini 3 disques 

![image](https://github.com/user-attachments/assets/5477cbce-2a32-4b8f-aaa2-1b553af5411f)

## RAID 6 avec 2 disques de parité mais plus chère bien sur 

#####################

# RAID 1 

installer mdadm

création des partitions avec fdisk /dev/sdc et sdd et fd pour raid puis : 

![image](https://github.com/user-attachments/assets/354f8707-5de6-4562-b8b7-8ff7cf169562)


Option de vitesse de raid : 
visualisé : 

![image](https://github.com/user-attachments/assets/683cffd1-1587-4e83-b626-8d24c36fc5b4)

et modifié ce fichier sysctl.conf pour modifier de manière permanente 

DANGER ici : si on reste comme ça et rebbot; l'UID et le nom md0 peuvent changer et donc KO, pour éviter cela, on va fixer cela 

![image](https://github.com/user-attachments/assets/f9bd5eaa-495b-4f33-ae94-0b924b94fcee)


![image](https://github.com/user-attachments/assets/7486f065-63f7-4024-9558-51770f8de26c)

# ajouter ou supprimer des disques 

1 le passer en faulty : 

![image](https://github.com/user-attachments/assets/d933f917-b426-4aeb-ad32-0eaf9e18b00a)

2 le supprimer : 

![image](https://github.com/user-attachments/assets/63c6b880-929d-41de-bba1-0b7de6dfbf8b)

# add : 

![image](https://github.com/user-attachments/assets/18133ff3-357a-4bf7-a6b0-f778f2f6f9a3)

# récupération de raid : 

![image](https://github.com/user-attachments/assets/30708bc3-f724-474f-92ce-442b305df20a)

# Fsck pour tchecker les disques 

# Résumé des disques 

![image](https://github.com/user-attachments/assets/7aa39457-f0c5-4cfd-95e2-514be6ba0634)


# LES I/O 

![image](https://github.com/user-attachments/assets/43c2ce60-4b89-44e1-8697-d3f835a31a32)

# Pyramide du stockage 

![image](https://github.com/user-attachments/assets/e6a8369f-923c-4560-b7d9-7061d396c57d)



![image](https://github.com/user-attachments/assets/6263e420-2347-400f-a5f5-223bf03fa4c2)



![image](https://github.com/user-attachments/assets/6475f1b8-0733-4097-bb42-f11e26f0814c)


![image](https://github.com/user-attachments/assets/573cffd2-d1d7-47fd-a452-a8ffdb685288)


![image](https://github.com/user-attachments/assets/32b54a82-f8de-4a7b-88b5-b3af082bdebe)


# iostat pour visualiser les stats d'écritures et de lectures

!!! lu depuis le boot de la machine 

![image](https://github.com/user-attachments/assets/244f949b-f40a-49df-8a4b-1f5b746f61d8)

Pour installer : 

![image](https://github.com/user-attachments/assets/7dbb7177-95e8-466a-8921-e033a6e66bf6)

```
iostat 5 # rafraichisssement toutes les 5sec
iostat -c # pour cpu 

```

![image](https://github.com/user-attachments/assets/c52d965a-1478-421e-a938-2cc42240dd37)


![image](https://github.com/user-attachments/assets/9df75e00-d65e-4318-beaf-b132bad6c020)

## Delta possible avec intervalle  : 

```
iostat 3 5 
```
![image](https://github.com/user-attachments/assets/9ba528ec-a46c-4779-9514-3dfaeb6a69e1)

![image](https://github.com/user-attachments/assets/59e66857-84f2-437a-83cb-ba4e3a618d46)


# Udev manager les devices 

![image](https://github.com/user-attachments/assets/690b5de8-e127-4cde-a2c0-231e1f1b990c)


![image](https://github.com/user-attachments/assets/6d420286-eb32-4d16-b9f6-03b0092256b6)

![image](https://github.com/user-attachments/assets/5743207e-5740-4dee-abdc-040241ca0c9c)

## exemple pour la souris

![image](https://github.com/user-attachments/assets/5544e247-07d1-4821-81b4-7407cfd7dc5f)



![image](https://github.com/user-attachments/assets/0b55baeb-076c-4884-b312-8399489774cd)


![image](https://github.com/user-attachments/assets/0ba85ffd-7f18-4b5a-8163-794a9271171c)


# SCSI 

![image](https://github.com/user-attachments/assets/47956365-c380-4b10-b986-d0303267d415)

![image](https://github.com/user-attachments/assets/4b378b5f-625a-4e3b-b2c4-bdc87c04f736)


![image](https://github.com/user-attachments/assets/537e4941-c4dc-48d6-b34f-a6fa7bf8497e)


![image](https://github.com/user-attachments/assets/a6ad1844-5a73-47ed-8cbf-ed51010ffbf9)

avec un petit d pour passer le device 

![image](https://github.com/user-attachments/assets/905b9613-dfee-4544-9598-144fbee1e029)



# DEvice mapper 

Framework pour wrapper les devices et faire l'interface entre le kernel et les devices 


![image](https://github.com/user-attachments/assets/98f00d02-e4ab-4936-b213-5ae1caa14172)

![image](https://github.com/user-attachments/assets/2cd17e10-acb6-4648-a6bc-c1afe94d2b56)

# les pseudo devices 

![image](https://github.com/user-attachments/assets/d21cc645-d90e-4810-bbac-fe859bdd4f18)

![image](https://github.com/user-attachments/assets/483ad26f-e882-4dce-bef7-cc0fd892c229)

/dev/null
![image](https://github.com/user-attachments/assets/e450cabb-a31c-4d7c-81ff-eecc69c76e81)

/dev/zero 

![image](https://github.com/user-attachments/assets/065db816-e968-43ee-b5ee-bf658fcd0aa8)

/dev/random 

utilisé en cryptographie 
![image](https://github.com/user-attachments/assets/22123b27-5205-4bd9-b629-fe3c8cd947c1)

/dev/loop pour les devices et snap pour les applications.


