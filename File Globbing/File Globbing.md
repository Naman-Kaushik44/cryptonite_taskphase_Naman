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
## Matching paths with []

```bash
hacker@globbing~matching-paths-with-:~$ cd /challenge/files
hacker@globbing~matching-paths-with-:/challenge/files$ /challenge/run /file_[abhs]
Error: please run with a working directory of /home/hacker!
hacker@globbing~matching-paths-with-:/challenge/files$ cd ~
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[abhs]
You got it! Here is your flag!
pwn.college{syr6LKyiSVdTkE24NNyOAB11K3h.dRjM4QDL5IjN0czW}
```
##Mixing globs

```bash
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing      fantastic   kind        pwning     uplifting   zesty
beautiful    great       laughing    queenly    victorious
challenging  happy       magical     radiant    wonderful
delightful   incredible  nice        splendid   xenial
educational  jovial      optimistic  thrilling  youthful
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cang]
Your expansion did not expand to the requested files (challenging, educational, 
pwning). Instead, it expanded to:
[cang]
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cag]*
Your expansion did not expand to the requested files (challenging, educational, 
pwning). Instead, it expanded to:
amazing challenging great
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{oVj9YuVk266wrRSBVPNz325fyNC.dVjM4QDL5IjN0czW}
```
