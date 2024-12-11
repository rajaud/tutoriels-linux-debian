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

 



