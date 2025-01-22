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

Port number :

## DNS (Domain Name System)

DNS primarily uses port 53 for both TCP and UDP protocols

+ UDP port 53: Used for standard DNS queries and responses
+ TCP port 53: Used for larger DNS messages that exceed the UDP size limit (traditionally 512 bytes)



## NFS (Network File System)

NFS uses multiple ports, with the main ones being1:
TCP/UDP port 2049: Used by the NFS daemon (nfsd)
TCP/UDP port 111: Used by the portmapper service
Additional ports used by NFS-related services include:


## TCP/UDP port 635: Used by mountd (in ONTAP 9)

TCP/UDP port 4045: Used by nlockmgr
TCP/UDP port 4046: Used by status service
TCP/UDP port 4049: Used by rquotad
NTP (Network Time Protocol)
NTP uses port 123, typically with UDP protocol3.
UDP port 123: Used for NTP time synchronization
It's important to note that while these are the standard port numbers, they can sometimes be configured differently in specific environments. Always verify the actual port usage in your particular system setup





