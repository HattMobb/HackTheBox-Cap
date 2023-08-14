# HackTheBox-Cap
A walkthrough/ write-up of the "Cap" box following the CREST pentesting pathway on HackTheBox.


## Enumeration
Scans show a few commonly open ports:
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/39a6fbfa-b4f7-443e-890b-9912831361ec)


Navigating to the web page, I was greeted by some sort of security dashboard:
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/ab6c2d0f-2e5e-464d-a717-0525fe88444d)

Manipulating the URL parameters gives access to different data via IDOR - potentially other user accounts:
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/7820b130-040d-4daa-a97b-b326dc928c3a)

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/279c4a21-edb9-4122-bbdf-ce6b6428e49e)


## Foothold

Combing through plainetxt pcap files - reveals useful info:

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/6f7f5573-d83b-43b6-a55f-72ee3e9f7904)


The discovered credentials reveals credentials for ftp login (ftp includes sensetive file):

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/f4e792d0-034a-4a0d-b5b0-946b1b956e3a)


Credential reuse meant that the same information worked for ssh access.
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/ef70b8f6-a1e0-42ef-bf7d-ab6e834d50c9)


## Privesc

I added linPEAS to the machine to automate internal enumeration and highlight pivesc pathways:
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/88b4cb63-6975-4da6-9697-d4a8b3c56d02)

LinPEAS discovered a capability based privesc vector:

![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/1f31957b-4bf4-4d37-ad9e-54ab88873496)

When capabilities are set for a binary,  the binary will be able to perform specific actions that it would not be able to perform without the set capabilities (as we will soon see).
Some capabilities, such as cap_sys_admin, which allows an executable to perform actions with administrative privileges, can be dangerous if they are not used properly.

The `cap_setuid` on the Python binary allows the process to set its effective user ID, which can be used to gain the privileges of another user, including the root user.

From GTFObins:
If the binary has the Linux CAP_SETUID capability set or it is executed by another binary with the capability set, it can be used as a backdoor to maintain privileged access by manipulating its own process UID.

privesc:
![image](https://github.com/HattMobb/HackTheBox-Cap/assets/134090089/253b1f2c-3e1f-409c-8d7e-2faad6de2ea1)



