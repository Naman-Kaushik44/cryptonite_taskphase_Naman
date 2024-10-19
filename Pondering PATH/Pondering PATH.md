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
