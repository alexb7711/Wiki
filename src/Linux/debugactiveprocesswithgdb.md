# Debugging an active process with GDB
At work, I often need to debug a running application via ssh. GDB can easily do this, but there are some hoops you have to jump through to get it going. The biggest being getting the PID (Proccess Identification). This can be automated pretty easily since `top` can pull that information up for you if you know the name of the proccess you are looking for. Using some newly learned techniques to manipulate strings that I found from watching [Luke Smith's](lukesmith.xyz) video, you can pass the username (if you have multiple people on the same server) and the process name. One little catch is that you may need to be in the same directory as the executable and source for it to hook and work correctly.

Another cool thing is that if you need to start gdb with specific parameters set, you can initialize those automatically. For example, I always get stopped by `SIGUSR1`. Every time I debug, I to write out `handle SIGUSR1 nostop`. Rather than doing that, you can put the flag `-ex "handle SIGUSR1 nostop"`, and it'll initialize gdb with that for you!

```
# debug.sh
# $1 == process name
#!/bin/sh
pid=`top -i -U $USER | grep $1`
pid=${pid#* }
pid=${pid%% ${USER}*}

echo PID found: $pid
echo Executing gdb...
echo gdb --pid=${pid} --ex "handle SIGUSR1 nostop" --tui

gdb $1 $pid --tui
```

Happy debugging!
