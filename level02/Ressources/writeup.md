# LEVEL02

**LOGIN: level02**

**PASSWORD: f2av5il02puano7naaf6adaaf**

----

Ok cette fois quand on arrive, on a : 
```
level02@SnowCrash:~$ ls -l
total 12
----r--r-- 1 flag02 level02 8302 Aug 30  2015 level02.pcap
```

Un fichier [pcap](https://fr.wikipedia.org/wiki/Pcap), on sort Wireshark ! 

On a donc un extrait d'une connection TCP. 
On Follow le stream et on passe en mode hexa, voilà une partie qui nous intéresse : 

![](https://github.com/bhm-heddy/42project_snowcrash/blob/master/level02/Ressources/level02.png)


*7f* correspond a la touche *delete* du clavier.

`ft_wandr...NDRel.L0L`
devient donc 
`ft_waNDReL0L`

**TOKEN = ft_waNDReL0L**

```
level02@SnowCrash:~$ su flag02
Password: 
Don't forget to launch getflag !
flag02@SnowCrash:~$ getflag
Check flag.Here is your token : kooda2puivaav1idi4f57q8iq
```

Si pour la correction, on a pas acces a Wireshard : 
`tcpflow -C -r level02.pcap`
