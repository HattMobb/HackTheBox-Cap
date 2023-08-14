# HackTheBox-Cap
A walkthrough/ write-up of the "Cap" box following the CREST pentesting pathway


## Enumeration
few basic ports open
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/39a6fbfa-b4f7-443e-890b-9912831361ec)


web page:

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/ab6c2d0f-2e5e-464d-a717-0525fe88444d)

manipulating the URL gives different data via IDOR - potentially other user accounts:
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/7820b130-040d-4daa-a97b-b326dc928c3a)

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/279c4a21-edb9-4122-bbdf-ce6b6428e49e)


downloading / combing through plainetxt pcap files - useful info:

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/6f7f5573-d83b-43b6-a55f-72ee3e9f7904)


ftp login with creds (ftp includes sensetive file):

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/f4e792d0-034a-4a0d-b5b0-946b1b956e3a)


creds also work with ssh:

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/ef70b8f6-a1e0-42ef-bf7d-ab6e834d50c9)


## Privesc

linpeas added:

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/88b4cb63-6975-4da6-9697-d4a8b3c56d02)

Exploit:

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/1f31957b-4bf4-4d37-ad9e-54ab88873496)

Looks like its a cpability exploit.

`cap_setuid` Allows a process to set its effective user ID, which can be used to gain the privileges of another user, including the root user.

From GTFObins:
If the binary has the Linux CAP_SETUID capability set or it is executed by another binary with the capability set, it can be used as a backdoor to maintain privileged access by manipulating its own process UID.

privesc:
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/253b1f2c-3e1f-409c-8d7e-2faad6de2ea1)



