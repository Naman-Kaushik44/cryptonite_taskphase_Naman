# File Globbing

## Matching with *

```bash
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /c****enge
You specified the path to 'cd' to in more than 4 characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:/run$ cd /*ge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{0OMa33nfSO9bIqDhNkGLZweKg5J.dFjM4QDL5IjN0czW}
```

## Matching with ?

```bash
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{MWKVI3gGsoev9GEyeOCJEiUqPOW.dJjM4QDL5IjN0czW}
```
## Matching with []

```bash
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[ahsb]
You got it! Here is your flag!
pwn.college{EBPRt5r7l2MvjSYkI4cRqg11eZk.dNjM4QDL5IjN0czW}
```
