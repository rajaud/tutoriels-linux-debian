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


