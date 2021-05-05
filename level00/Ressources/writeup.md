# LEVEL 00

**LOGIN: level00**

**PASSWORD: level00**

 ----


=> Quand on arrive, il n'y a rien dans le home, pas d'índice. 

Iniatilement les projetcs étaient liés à une vidéo de présentation du projet. 
Après avoir retrouver cette vidéo dans les archives, on y trouve un premier indice : 

*FIND this first file who can run only as flag00....*

Du coup : 

``` 
ls -l ` find / -user flag00 2>&-` 

----r--r-- 1 flag00 flag00 15 Mar  5  2016 /rofs/usr/sbin/john
----r--r-- 1 flag00 flag00 15 Mar  5  2016 /usr/sbin/john

cat /usr/sbin/john
cdiiddwpgswtgt

```

Le code ne marche pas pour passer au niveau suivant. 
Vu le nom du fichier je lance *John the Ripper* mais rien de concluant. 

Direction https://www.dcode.fr/ , premier niveau du CTF on commence par le code cesar :
Bingo !! 

**TOKEN = x24ti5gi3x0ol2eh4esiuxias**
