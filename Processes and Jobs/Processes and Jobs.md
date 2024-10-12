# Processes and Jobs 

## Listing Processes

```bash
hacker@processes~listing-processes:~$ ps -aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0   1056   640 ?        Ss   10:12   0:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init 
root           7  0.0  0.0   5052  2240 ?        S    10:12   0:00 /run/dojo/bin/sleep 6h
root          68  0.0  0.0   4132  2560 ?        S    10:12   0:00 /challenge/1001-run-21633
root          72  0.0  0.0   2744  1600 ?        S    10:12   0:00 sleep 6h
hacker        73  0.1  0.0   5240  4160 pts/0    Ss   10:12   0:00 /run/dojo/bin/ssh-entrypoint
hacker        90  0.0  0.0   7868  3200 pts/0    R+   10:13   0:00 ps -aux
hacker@processes~listing-processes:~$ /challenge/1001-run-21633
Yahaha, you found me! Here is your flag:
pwn.college{4Q_NlnuaQf3XFmbpBGJGqTquxCc.dhzM4QDL5IjN0czW}
```
# Killing Processes

```bash
Connected!                                                                        
hacker@processes~killing-processes:~$ ps -ef | grep dont
hacker        73      71  0 10:19 ?        00:00:00 /challenge/dont_run
hacker        93      75  0 10:20 pts/0    00:00:00 grep --color=auto dont
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ ps -ef | grep dont
hacker        95      75  0 10:21 pts/0    00:00:00 grep --color=auto dont
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{Ue776w4hjdkGs5hpROlCX5jwXQM.dJDN4QDL5IjN0czW}
```
## Interrupting Processes

```bash
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{QESbij3I--O9xTZZ8HJDiZS6TO7.dNDN4QDL5IjN0czW}
```
## Suspending Processes

```bash
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 11:00 pts/0    00:00:00 bash /challenge/run
root          84      82  0 11:00 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can 
background me with Ctrl-Z or, if you're not ready to do that for whatever 
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 11:00 pts/0    00:00:00 bash /challenge/run
root          89      65  0 11:00 pts/0    00:00:00 bash /challenge/run
root          91      89  0 11:00 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{QKA9bPrsRKf4sHRUhj8sFMl_j6h.dVDN4QDL5IjN0czW}
```
## Resuming Processes 

```bash
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with 
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{sO5-5yW_ljSWZyJWz1EZ-n6auiG.dZDN4QDL5IjN0czW}
```
## Backgrounding Process

```bash
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S+   bash /challenge/run
root          84 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S    bash /challenge/run
root          92 S    sleep 6h
root          93 S+   bash /challenge/run
root          95 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{sw7LwaFy7eYQ6_nGPOFx_x-fgFo.ddDN4QDL5IjN0czW}
```
