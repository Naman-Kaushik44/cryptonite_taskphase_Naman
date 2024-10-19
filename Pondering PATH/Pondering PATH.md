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
