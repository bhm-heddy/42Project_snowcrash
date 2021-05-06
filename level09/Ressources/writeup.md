# LEVEL 09

**LOGIN: level09*

**PASSWORD: 25749xKZ8L7DkSCwJkT9dyv6f**

 ----



```
level09@SnowCrash:~$ ls -l ; echo ; file level09 
total 12
-rwsr-sr-x 1 flag09 level09 7640 Mar  5  2016 level09
----r--r-- 1 flag09 level09   26 Mar  5  2016 token

level09: setuid setgid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=0x0e1c5a0dfb537112250e1c78d5afec3104abb143, not stripped
```

```
./level09 
You need to provied only one arg.
level09@SnowCrash:~$ ./level09 token 
tpmhr
```
```
level09@SnowCrash:~$ echo toto > test.txt ; ./level09 test.txt
tfuw2y~{
level09@SnowCrash:~$ echo abcdef > test.txt ; ./level09 test.txt
tfuw2y~{
level09@SnowCrash:~$ cat token 
f4kmm6p|=�p�n��DB�Du{��
```

Ok! l'output du binaire ne dépend pas du contenu du fichier, d'autant plus qu'un `nm level09` nous apprend qu'il n'y a pas d'appel a `open`

Le binaire prend donc une chaine, la modifie puis la print. Le fichier token contient donc le token modifier par le binaire.

```
level09@SnowCrash:~$ ./level09 abcdefg
acegikm
level09@SnowCrash:~$ ./level09 111111
123456
level09@SnowCrash:~$ ./level09 aaaaaa
abcdef
```

Le binaire rajoute n+1 a chaque lettre de la string

On se fait un petit reverse 
```C
int             main(int ac, char **av)
{
        char *s = av[1];
        char *ret = (char*)malloc(sizeof(char) *strlen(s) + 1);
        int i =0;
        int j =0;
        while (s[i])
        {
                ret[i] = s[i] - j;
                j++;
                i++;
        }
        printf("[%s]\n", ret);
        return (0);

}
```
```
./a.out `cat token `
[f3iji1ju5yuevaus41q1afiuq]
```

**TOKEN: f3iji1ju5yuevaus41q1afiuq**

```
level09@SnowCrash:~$ su flag09
Password: 
Don't forget to launch getflag !
flag09@SnowCrash:~$ getflag
Check flag.Here is your token : s5cAJpM8ev6XHw998pRWG728z
```

