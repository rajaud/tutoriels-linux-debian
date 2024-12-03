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







































