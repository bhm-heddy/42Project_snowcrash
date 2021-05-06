# LEVEL 00

**LOGIN: level00**

**PASSWORD: g1qKMiRpXf53AWhDaU7FEkczr**

 ----

```
level13@SnowCrash:~$ strings level13
...
0123456
UID %d started us but we we expect %d
boe]!ai0FB@.:|L6l@A?>qJ}I
your token is %s
...
```
Ce strings nous donne ces info qui devraient nous etre utiles par la suite.

```
ltrace ./level13 
__libc_start_main(0x804858c, 1, 0xbffff7f4, 0x80485f0, 0x8048660 <unfinished ...>
getuid()                                                 = 2013
getuid()                                                 = 2013
printf("UID %d started us but we we expe"..., 2013UID 2013 started us but we we expect 4242
)      = 42
exit(1 <unfinished ...>
```
Il faudrait que `getuid()`retourne 4242.

On va faire un Hijacking syscalls, nous permettant d´include notre `getuid()`dans le binaire `level13`

```
int getuid(void)
{
	return (4242);
}
```

On compile la lib dynamique
`gcc -shared -fPIC -o fake.so getuid.c`

on run : 
`LD_PRELOAD=$PWD/fake.so ./level13`

ooooh ca n'a pas marché : 
`UID 2013 started us but we we expect 4242` 

On va passer par gdb :
`gdb ./level13 `

On set LD_PRELOAD:
`set environment LD_PRELOAD /home/user/level13/fake.so`

On run : 
`run`

Ok! là ca marche :
```
Starting program: /home/user/level13/level13 
your token is 2A31L79asukciNyi8uppkEuSx
```

**TOKEN : 2A31L79asukciNyi8uppkEuSx**

