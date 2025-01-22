# 200 Questions sur Linux avec réponse à passer en entretien technique de Linux 



![linuxtec1](https://github.com/user-attachments/assets/4ff858bb-4a5d-4718-a32a-b1815181a4ac)


![linuxtec2](https://github.com/user-attachments/assets/acb6ade1-85bf-450d-a57a-308d672f3a70)


![linuxtec3](https://github.com/user-attachments/assets/bec32036-87d6-4f3c-9ce8-bd4bfe99c1c1)



![linuxtec4](https://github.com/user-attachments/assets/44388be6-9324-42e0-b103-9f01290295f8)



![linuxtec5](https://github.com/user-attachments/assets/3c60936c-5543-4582-b2e2-ced1712745c4)


![linuxtec6](https://github.com/user-attachments/assets/88a6e7bd-306f-4f27-87a8-d23471f65625)


![linuxtec7](https://github.com/user-attachments/assets/2ae1d874-60ee-4f8f-86e5-f16220dc4d30)


![linuxtec8](https://github.com/user-attachments/assets/8145bc29-7b11-4766-b77e-485cc9750ed7)

![linuxtec9](https://github.com/user-attachments/assets/ad20cecc-7b74-40bf-a989-bc18f9bcd54c)



![linuxtec10](https://github.com/user-attachments/assets/6c84d3df-b234-4b51-a538-808b71d9c84a)


![linuxtec11](https://github.com/user-attachments/assets/a218844c-1bf9-42bb-aa10-d660fa0e2bec)


![linuxtec12](https://github.com/user-attachments/assets/7597c30a-16e9-4f23-ad47-3252c9e4acd5)



![linuxtec13](https://github.com/user-attachments/assets/cd620598-cd89-457e-a0e0-1c19314b9b3e)



![linuxtec14](https://github.com/user-attachments/assets/b3e4fb58-1de3-472e-826f-e964a10a589b)



![linuxtec15](https://github.com/user-attachments/assets/5266e633-b6f9-4b53-8415-5fd08d4bd5a5)


![linuxtec16](https://github.com/user-attachments/assets/b16f30e4-db2b-4618-9611-23f8bfe531f7)



![linuxtec17](https://github.com/user-attachments/assets/68d06619-d3ee-4a9e-b653-644de274d3e5)



![linuxtec18](https://github.com/user-attachments/assets/39d21991-30d2-4768-9cb8-9eca719e0d9b)


![linuxtec19](https://github.com/user-attachments/assets/6efe2462-b9ac-4c92-875a-7a27b9e9bdb0)



## Explication via perplexity


# **  ?2 check kernel version **

La commande "uname" est un utilitaire Unix/Linux qui sert à afficher des informations sur le système d'exploitation et le matériel de la machine sur laquelle elle est exécutée. Voici ses principales utilisations et options les plus courantes :
Fonction principale : 
Afficher des informations système de base comme le nom du noyau, la version, l'architecture matérielle, etc.

Options couramment utilisées : 

+ -a (--all) : Affiche toutes les informations disponibles34
+ -s (--kernel-name) : Affiche le nom du noyau (comportement par défaut si aucune option n'est spécifiée)4
+ -n (--nodename) : Affiche le nom d'hôte du système sur le réseau4
+ -r (--kernel-release) : Affiche la version du noyau4
+ -v (--kernel-version) : Affiche la version détaillée du noyau4
+ -m (--machine) : Affiche le nom de l'architecture matérielle de la machine4
+ -p (--processor) : Affiche le type de processeur4
+ -o (--operating-system) : Affiche le nom du système d'exploitation4

Exemples d'utilisation : 

Afficher toutes les informations :

`uname -a`

Afficher uniquement la version du noyau :

`uname -r`

Afficher le nom de la machine et la version du noyau :

`uname -nm`

La commande uname est particulièrement utile pour les administrateurs système et les développeurs qui ont besoin d'obtenir rapidement des informations sur l'environnement système, notamment lors de la configuration de logiciels ou du débogage de problèmes liés au système

![image](https://github.com/user-attachments/assets/d9c2dd85-7891-47ac-8b3e-50ba5e7d7831)


# **?7 how to check network interface **

![image](https://github.com/user-attachments/assets/bd445b41-4faf-41fa-8d93-bee3d85fdc03)

# **?8 3 way to adding a user **

![image](https://github.com/user-attachments/assets/f84170f8-053b-4698-8200-8d1a1888f83a)

useradd pour scripting et ansible 

![image](https://github.com/user-attachments/assets/6ed6eb4c-d05b-4ccd-8ffc-e3cc6215ef79)

# **?9 change user password **

![image](https://github.com/user-attachments/assets/6a7eefcb-13ca-465a-8424-621f66ea8bcd)


# **?11 déconnexion systeme   **

![image](https://github.com/user-attachments/assets/c5316bf6-c023-4bfc-89e1-154538d995fc)





# **  ?19 Port number :** 

![image](https://github.com/user-attachments/assets/3dabfdad-3f9c-41cf-982c-48b9412fd4cf)



## DNS (Domain Name System)

DNS primarily uses port 53 for both TCP and UDP protocols

+ UDP port 53: Used for standard DNS queries and responses
+ TCP port 53: Used for larger DNS messages that exceed the UDP size limit (traditionally 512 bytes)



## NFS (Network File System)

NFS uses multiple ports, with the main ones being : 

+ TCP/UDP port 2049: Used by the NFS daemon (nfsd)
+ TCP/UDP port 111: Used by the portmapper service


Additional ports used by NFS-related services include:

+ TCP/UDP port 635: Used by mountd (in ONTAP 9)
+ TCP/UDP port 4045: Used by nlockmgr
+ TCP/UDP port 4046: Used by status service
+ TCP/UDP port 4049: Used by rquotad

 ## NTP (Network Time Protocol)

+ NTP uses port 123, typically with UDP protocol3.
+ UDP port 123: Used for NTP time synchronization

**It's important to note that while these are the standard port numbers, they can sometimes be configured differently in specific environments. Always verify the actual port usage in your particular system setup**


# NFS and NTP 

## NFS (Network File System)

NFS is a distributed file system protocol that allows a user on a client computer to access files over a network in a manner similar to how local storage is accessed. 

Key points about NFS include:

+ It enables sharing of files and directories between computers on a network
+ Typically used in Unix-like operating systems, but also available for other platforms
+ Allows for centralized management of data and resources
+ Uses RPC (Remote Procedure Call) for communication between clients and servers
  
NFS uses multiple ports for its operation, with the main one being:

+ TCP/UDP port 2049: Used by the NFS daemon (nfsd)


## NTP (Network Time Protocol)

NTP is a networking protocol designed to synchronize the clocks of computers over a network. 

Important aspects of NTP include:
+ Developed by David L. Mills in the 1980s
+ Uses UDP port 123 for communication
+ Aims to synchronize computer clocks with high precision, potentially up to nanosecond accuracy
+ Based on the Coordinated Universal Time (UTC)
+ Uses a hierarchical system of time sources called "strata"

Key features of NTP:
+ Reference time: All clocks are aligned to a reference clock based on UTC.
+ Fault-tolerant: Automatically seeks the best time sources for synchronization and can combine multiple sources to reduce accumulated errors.
+ Hierarchical structure: Uses a system of strata to define the distance from the reference clock.
+ Security implications: Precise time synchronization is crucial for cybersecurity, particularly for:
  -  One-Time Password (OTP) authentication systems
  - Digital forensics and log analysis during investigations
  
NTP is widely used and is essential for maintaining accurate time across networks, which is critical for many cybersecurity applications and protocols.


# **?20 DNS file name et located ? **

![image](https://github.com/user-attachments/assets/0ce6ad7a-2009-4b6a-a886-1425205030d3)




