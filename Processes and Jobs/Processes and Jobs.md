# Processes and Jobs 

## Listing Processes

I used ps-aux to show all running processes and found the challenge file, it was easy to invoke it from there with it's absolute path.

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

I used the ps -ef and grep dont from the running processing and /challenge/dont_run process id is 73 so I killed it and 
and ensured that command is not working again. Hence, I used the /challenge/run command to get the flag.

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

The challenge required me to interrupt the /challenge/run to get the flag so I used ctrl+c to get the flag.

```bash
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{QESbij3I--O9xTZZ8HJDiZS6TO7.dNDN4QDL5IjN0czW}
```
## Suspending Processes

The challenge required me to get another copy of the /challenge/run command running in the terminal, hence I suspended the process /challenge/run
and then ran the /challenege/run command again to get the flag.

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

This challenge required me to execute the /challenge/run command, then suspend it and had to resume it with the fg command to get the flag.

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

In this /challenge/run was supposed to be first suspended and then resumed in the background and then a new version of /challenge/run was supposed to be launched to get the flag.

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
# Foregrounding Process

In this challenge, I invoked the /challenge/run command and then suspended it with ctrl + z and then used the bg command to resume it in the background.
Now I used the fg command to run it in the foreground with re-suspending it to get the flag.

```bash
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the 
background, and *then* foreground it without re-suspending it! You can 
background me with Ctrl-Z (and resume me in the background with 'bg') or, if 
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out. After that, resume me into the foreground with 'fg'; 
I'll wait.
hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{oHFLoIqZuuEomAKm0S2ylQJvse1.dhDN4QDL5IjN0czW}
```
# Starting Background Processes

This challenge just required me to append & to the command /challenge/run to start it in the background.

```bash
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 85



Yay, you started me in the background! Because of that, this text will probably 
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
hacker@processes~starting-backgrounded-processes:~$ pwn.college{EBmfh3IAMgwPxKc7Mz24tZyHTvI.dlDN4QDL5IjN0czW}

[1]+  Done                    /challenge/run
```
## Process Exit Codes

$? allows us to read a special variable ? with the echo command, it stores the exit code of a recently terminated command. We just had to get that 
exit code in this challenge and run it as an argument to the given command to get the flag.

```bash
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
187
hacker@processes~process-exit-codes:~$ /challenge/submit-code 187
CORRECT! Here is your flag:
pwn.college{g7m8ddqnbtlkeNDUlojZ-qCcjbH.dljN4UDL5IjN0czW}
```
