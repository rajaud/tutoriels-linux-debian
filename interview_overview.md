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


# **?23 IP gateway diff **

![image](https://github.com/user-attachments/assets/1bb94608-48b7-4bc7-8c81-e140ba2afd6f)


# **?25 IP change to static **

![image](https://github.com/user-attachments/assets/6423ecdc-9e13-4a21-b67e-3206939ad678)

![image](https://github.com/user-attachments/assets/a058c7c0-3bdb-46fd-b0a2-8bc17fd64e7e)

![image](https://github.com/user-attachments/assets/d0c31f7c-39a0-4607-a294-f1c192f1621c)



# **?26 ping hostname with error unknown hosts **

![image](https://github.com/user-attachments/assets/e50a4e97-38b2-496e-bb80-ca9bafc71c7a)

![image](https://github.com/user-attachments/assets/5b622097-990b-4a42-92a1-effa0ac4e298)

![image](https://github.com/user-attachments/assets/c53f0cf6-9460-4af0-bc5a-d099ddc6e5b7)


# **?29 type of filesystem **

![image](https://github.com/user-attachments/assets/70507b0a-4fc2-410e-b351-b44c84ae721d)



# **?32 different types of DNS server **

![image](https://github.com/user-attachments/assets/d07f4d3d-add4-4bcd-90b8-5f134fd735e8)

![image](https://github.com/user-attachments/assets/30cdc697-0a21-41bb-a06e-f3923061e14d)



# **?33 locate DNS service zone file **

![image](https://github.com/user-attachments/assets/cace38cb-cf2c-43d9-a481-2ca1d69fd405)



# **?36 first column of a file  **

![image](https://github.com/user-attachments/assets/c1b2efef-ac68-46d6-989b-95fac5a3cfec)



# **?38 nslookup and dig diff **

![image](https://github.com/user-attachments/assets/9f89f873-bec6-4d65-9d56-3cb63385e17a)


![image](https://github.com/user-attachments/assets/ff2042f0-13ed-4982-93f7-a3f66c85852d)




# **?41 subnet **

![image](https://github.com/user-attachments/assets/9cc1b631-cf57-4f3c-8590-08110d44fb83)




# **?42 send /etc **

![image](https://github.com/user-attachments/assets/8c1561b3-c4bb-4f11-8227-a6712ceb0c47)

![image](https://github.com/user-attachments/assets/c9591290-c4ca-490f-b708-de006ffa1dfb)

![image](https://github.com/user-attachments/assets/8af5af9d-13cf-44a7-a326-0e9a74b30226)


# **?44 rsyslog **

![image](https://github.com/user-attachments/assets/fa47b029-598a-4e22-9deb-54886b56ab97)

# **?46 untar  **

![image](https://github.com/user-attachments/assets/ae8b9d29-ce50-42f4-b9be-03343013e5f5)





# **?48 nsswitch.conf file **

![image](https://github.com/user-attachments/assets/b1895e8e-3f06-46d7-ab8f-affd80731a89)




# **?56 mv command rename **

![image](https://github.com/user-attachments/assets/735727c0-5b8e-4d52-b8d6-33055dcb1246)


# **?59 trier a l'envers **

![image](https://github.com/user-attachments/assets/2116d4fe-7eff-44e0-bdbf-b6de4b916e55)

# **?63 bonding NIC **

![image](https://github.com/user-attachments/assets/2269c8af-b6ca-4538-a941-b1de3213e838)

![image](https://github.com/user-attachments/assets/efb2e08d-f044-467b-9c4d-5798617c4b38)


# **?64 awk et cut **

![image](https://github.com/user-attachments/assets/108d452b-70a0-47c3-a272-ef6f84eaaf49)


# **?66 df cooamnd  **

![image](https://github.com/user-attachments/assets/c03bb099-fa2b-4a24-9886-eb230ba529b1)


# **?74 display file'zs content **

![image](https://github.com/user-attachments/assets/f49442f1-4f33-4585-8838-e1f05b90943a)


# **?77 swap space **

![image](https://github.com/user-attachments/assets/6456b4cb-2581-4971-a4b6-703836618480)

![image](https://github.com/user-attachments/assets/55cb8ae6-79a9-4a4e-872b-3764ed90fb07)




# **?78 inode **

![image](https://github.com/user-attachments/assets/95476c4e-acbf-4c69-b2de-8f40fce74d04)

![image](https://github.com/user-attachments/assets/f6def095-5632-4773-a8a2-48fe187a833d)



# **?79 kernel tuning **

![image](https://github.com/user-attachments/assets/024e3e69-1cf5-478c-9803-62a0885ff515)

![image](https://github.com/user-attachments/assets/f5e61fec-f77f-428d-878d-72297ea36fdb)


# **?83 hardware inforamtion **

![image](https://github.com/user-attachments/assets/af041075-6964-4c0a-bce9-e5ef0e565872)

![image](https://github.com/user-attachments/assets/adf11403-8fa6-41d7-853e-a5e602331f88)

![image](https://github.com/user-attachments/assets/5e4ac8cc-608c-4055-9e5d-2a171d6dfbc8)




# **?84 mac adresse  **

![image](https://github.com/user-attachments/assets/6853ba4b-90bf-4bf9-9811-926fd84ab094)


# **?86 uniq and sed command **

![image](https://github.com/user-attachments/assets/0de819dc-3db5-44c2-99d7-131e2642e1b6)


# **?88 tar gzip unzip **

![image](https://github.com/user-attachments/assets/b6ffa5fe-7b90-4ff8-b274-05f4d5e8a7e1)


# **?105 mail server record in DNS **

![image](https://github.com/user-attachments/assets/6fcfa9da-f102-44d9-9de9-2a777553a5b8)





# **?117 init 6 for rebbot **

![image](https://github.com/user-attachments/assets/782da688-036c-4221-ab70-3b47cd01f5bc)



# **?122 how to remove package **

![image](https://github.com/user-attachments/assets/e428e612-5b86-405a-90b7-a41355cf8b2d)





# **?137 SAN NAS diff **

![image](https://github.com/user-attachments/assets/b2e4a432-1e3a-46bd-a25f-50682ada026f)


# **?140 netstat **

![image](https://github.com/user-attachments/assets/426f8817-0a3b-47e7-9a7c-75cf831bb5f4)



# **?141 raccourci clavier **

![image](https://github.com/user-attachments/assets/045ab4ad-9236-4f4e-9f14-13c988f3260c)


# **?143 type of bash **

![image](https://github.com/user-attachments/assets/dc873f54-a9d0-4bb5-8918-d2d20a8ecca6)



# **?167 soft link  **

![image](https://github.com/user-attachments/assets/d7d21e51-8ed4-417f-8781-325ef505276e)



# **?168 delete message in log file  **

![image](https://github.com/user-attachments/assets/c6a1ccb8-16e0-40cd-b548-b531c6413b6f)



# **?174 all package in system  **

![image](https://github.com/user-attachments/assets/54237ea4-ff1b-4926-8418-2e1f16003c39)



# **?183  **




# **?56 mv command rename **




# **?56 mv command rename **




# **?56 mv command rename **




# **?56 mv command rename **




# **?56 mv command rename **




# **?56 mv command rename **





# **?56 mv command rename **





# **?56 mv command rename **





# **?56 mv command rename **





# **?56 mv command rename **




# **?56 mv command rename **












