## LEVEL01

**LOGIN: level01**

**PASSWORD: x24ti5gi3x0ol2eh4esiuxias**


 ----

Pareil quand on arrive rien ne semble trainer. 
Vu précédemment :
```
cat /etc/passwd
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
```
le *42* n'est surement pas là par hasard... peut être l'id ou le sel ? 

###### *Avant le masquage du mot de passe (c'est-à-dire dans les premières implantations de Unix), ce champ contenait un hachage cryptographique du mot de passe de l'utilisateur (en combinaison avec un sel). Le sel et le mot de passe haché OU une valeur d'exception. Le sel et le mot de passe haché sont dans le format "$id$sel$motdepassehaché", c'est la forme imprimable d'un hachage de mot de passe tel que produit par crypt (C). "$id" est l'algorithme utilisé : sur GNU/Linux, "$1$" signifie MD5, "$2a$" signifie Blowfish, "$2y$" signifie Blowfish (manipulation correcte de caractères 8 bits), "$5$" signifie SHA-256 et "$6$ signifie SHA-5124, d'autres versions de Unix (comme NetBSD) peuvent avoir des codes de fonctions de hachage différents[réf. souhaitée]. L'étirement de clé est utilisé pour augmenter la difficulté de cassage de mot de passe, en utilisant par défaut 1000 itérations de MD5 modifié5, 64 itérations de Blowfish, 5000 itérations de SHA-256 ou SHA-5126. Le nombre d'itérations peut changer pour Blowfish, ou pour SHA-256 et SHA-512 en utilisant par exemple "$6$rounds=50000 $".) https://fr.wikipedia.org/wiki/Passwd#Le_fichier_/etc/passwd*

On ressort John pour voir :

```
echo -n '42hDRfypTqqnw' >flag01
john -show flag01
?:abcdefg
```

**TOKEN = abcdefg**
```
level01@SnowCrash:~$ su flag01
Password: 
Don't forget to launch getflag !
flag01@SnowCrash:~$ getflag
Check flag.Here is your token : f2av5il02puano7naaf6adaaf
```
