# File Globbing

## Matching with *

When it encounters a * character in any argument, the shell will treat it as "wildcard" and try to replace that argument with any files that match the pattern.
This is well illustrated in an example given on pwn.college.

``
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
``

The * matches any part of the filename except for / or a leading . character. For example:

``
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
``

The challenge just required me to use the glob to pass an argument to cd with just 4 characters or less.

I was confused at first in how it worked like I assumed that a glob was used for each place we wanted to shorten which obviously makes no sense since the time spent would be the same.

I later realized that we just need one * and a couple of characters unique to the word we want to glob to instantly shorten it.

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

When it encounters a ? character in any argument, the shell will treat it as single-character wildcard. This works like *, but only matches one character. For example:

``
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
``

In this challenge we only needed to change the directory to /challenge by globbing with ? by replacing c and l in the argument.

```bash
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{MWKVI3gGsoev9GEyeOCJEiUqPOW.dJjM4QDL5IjN0czW}
```
## Matching with []

The square brackes are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:

```
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

In this challenge I just changed working directory to /change/files and then ran the /challenge/run command with the argument globbed with characters a h s b which will be corresponding to their respective files after the execution of the command.

```bash
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[ahsb]
You got it! Here is your flag!
pwn.college{EBPRt5r7l2MvjSYkI4cRqg11eZk.dNjM4QDL5IjN0czW}
```
## Matching paths with []

Globbing happens on a path basis, so you can expand entire paths with your globbed arguments. For example:

``
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
``

So I was a little confused at first but after rereading the challenge I got that we had to start from the home directory and then navigate into opening those files with their absolute paths while using globbing to do it all at the same time which I did with the /challenge/run command.

```bash
hacker@globbing~matching-paths-with-:~$ cd /challenge/files
hacker@globbing~matching-paths-with-:/challenge/files$ /challenge/run /file_[abhs]
Error: please run with a working directory of /home/hacker!
hacker@globbing~matching-paths-with-:/challenge/files$ cd ~
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[abhs]
You got it! Here is your flag!
pwn.college{syr6LKyiSVdTkE24NNyOAB11K3h.dRjM4QDL5IjN0czW}
```
## Mixing globs

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
## Exclusionary Globbing

```bash
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ ls
amazing      fantastic   kind        pwning     uplifting   zesty
beautiful    great       laughing    queenly    victorious
challenging  happy       magical     radiant    wonderful
delightful   incredible  nice        splendid   xenial
educational  jovial      optimistic  thrilling  youthful
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{AG74a_3uAXnqzwWjBLgFP5ZrnUK.dZjM4QDL5IjN0czW}
hacker@globbing~exclusionary-globbing:/challenge/files$ 
```
