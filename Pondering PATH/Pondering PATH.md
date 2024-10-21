# Pondering PATH

## The PATH variable

I blanked out the PATH variable and then ran the /challenge/run command which when tried to delete the flag with rm command, it couldn't find the rm command and hence gave me the flag.
```bash
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{48kljwpcOmAr9LDAWG5JS1nwZ02.dZzNwUDL5IjN0czW}
```
## Setting PATH

I added the directory to the win command to the PATH variable and then ran the challenge/run command which gave me the flag because the win command could be now found in the PATH variable.
```bash
`hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{ERFL6wYGQfF1kmrs4rtpv0dia9l.dVzNyUDL5IjN0czW}
```
## Adding Commands

I created a the win file and found the absolute path to the cat command, then I created a new shell script in a directory and put in cat /flag as the stdout of echo command in the script. Then I enabled the win command to be executable and changed the path variable to add win command into it. After running the /challenge/run command, win was invoked and I got the flag. 

I had to reference from chatgpt for commands like which that allowed me to directly find cat's location but I know that I could have also done if by reading the path variable and checking the directories inside it for the location of the cat command. I also couldn't figure out how to append the cat command into the win file so I had to reference that as well.

```bash
hacker@path~adding-commands:~$ touch win
hacker@path~adding-commands:~$ which cat
/run/workspace/bin/cat
hacker@path~adding-commands:~$ echo '#!/bin/bash' > /home/hacker/win
hacker@path~adding-commands:~$ echo '/bin/cat /flag' >> /home/hacker/win
hacker@path~adding-commands:~$ chmod +x /home/hacker/win
hacker@path~adding-commands:~$ export PATH=/home/hacker:$PATH
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{88kcYYDEkwV5-qMM-tKn1bDzoDR.dZzNyUDL5IjN0czW}
```

## Hijacking Commands

This question was very similar to the last one in the sense that instead of win file in the previous challenge, I created a new rm file since we can't really make changes to the /challenge/run command. We can just make it find out version of the rm command instead of the system's inbuilt command.
I appended cat /flag into the rm file I created and then changed the path variable such that my version of rm is found by /challenge/run and the flag is not deleted.

```bash
hacker@path~hijacking-commands:~$ touch rm
hacker@path~hijacking-commands:~$ which cat
/run/workspace/bin/cat
hacker@path~hijacking-commands:~$ echo '#!/bin/bash' > /home/hacker/rm
hacker@path~hijacking-commands:~$ echo '/bin/cat /flag' >> /home/hacker/rm
hacker@path~hijacking-commands:~$ chmod +x /home/hacker/rm
hacker@path~hijacking-commands:~$ export PATH=/home/hacker:$PATH
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
pwn.college{EnweeLNGjKCFD1z-AUAZOUnRV_R.ddzNyUDL5IjN0czW}
```
