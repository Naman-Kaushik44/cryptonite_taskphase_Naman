# Pondering Paths

## 1) The Root
 What I learnt in this challenge :-

The linux filesystem is a tree and it has a root that is represented with /.  The root of the filesystem is a directory, and every directory can contain other directories and files.

We refer to files and directories by their path. A path from the root of the filesystem starts with / (that is, the root of the filesystem), and describes the set of directories that must be descended into to find the file. Every piece of the path is demarcated with another /.

The filesystem starts at / and a program can be invoked by providing it's path. The challenge required us to invoke the pwn program using the /pwn path. This style of path, one that starts with the root directory, is referred to as an "absolute path".

```bash
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{46KLaMFPUjo-E6yvkTn7NwVF66I.dhzN5QDL5IjN0czW}
```
## 2) Program and Absolute Paths
What I learnt in this challenge:-




```bash
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{MoxVNCth38jbdUgECBTT_BXovNv.dVDN1QDL5IjN0czW}
```

## 3) Position thyself
```bash
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /var/lib/apt/lists directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /var/lib/apt/lists
hacker@paths~position-thy-self:/var/lib/apt/lists$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{oJpDotKtlubpfh_eI03-1zzvp69.dZDN1QDL5IjN0czW}
```
## 4) Position elsewhere
```bash
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /proc/67/fd directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /proc/67/fd
hacker@paths~position-elsewhere:/proc/67/fd$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{0AW79cLTrNtlpLr7g_pgzHtOPr_.ddDN1QDL5IjN0czW}
hacker@paths~position-elsewhere:/proc/67/fd$ 
```
## 5) Position yet elsewhere 
```bash
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /var/lib/apt/lists directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /var/lib/apt/lists
hacker@paths~position-yet-elsewhere:/var/lib/apt/lists$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{QHo1Y1yLvIvxVP3cRgsGEmK6x3-.dhDN1QDL5IjN0czW}
```
## 6) impicitive relative paths, from /
```bash
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{o_IO3yJTNHA_JQA0fOW5VC1S4PV.dlDN1QDL5IjN0czW}
```
## 7) explicitive relative paths, from /
```bash
hacker@paths~explicit-relative-paths-from-:~$ .
ssh-entrypoint: .: filename argument required
.: usage: . filename [arguments]
hacker@paths~explicit-relative-paths-from-:~$ cd .
hacker@paths~explicit-relative-paths-from-:~$ challenge
ssh-entrypoint: challenge: command not found
hacker@paths~explicit-relative-paths-from-:~$ /challenge
ssh-entrypoint: /challenge: Is a directory
hacker@paths~explicit-relative-paths-from-:~$ ./challenge 
ssh-entrypoint: ./challenge: No such file or directory
hacker@paths~explicit-relative-paths-from-:~$ .challenge run
ssh-entrypoint: .challenge: command not found
hacker@paths~explicit-relative-paths-from-:~$ .
ssh-entrypoint: .: filename argument required
.: usage: . filename [arguments]
hacker@paths~explicit-relative-paths-from-:~$ cd .
hacker@paths~explicit-relative-paths-from-:~$ challenge./run
ssh-entrypoint: challenge./run: No such file or directory
hacker@paths~explicit-relative-paths-from-:~$ cd .
hacker@paths~explicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~explicit-relative-paths-from-:~$ cd ./
hacker@paths~explicit-relative-paths-from-:~$ challenge/run
ssh-entrypoint: challenge/run: No such file or directory
hacker@paths~explicit-relative-paths-from-:~$ cd ./
hacker@paths~explicit-relative-paths-from-:~$ echo hackers
hackers
hacker@paths~explicit-relative-paths-from-:~$ challenge
ssh-entrypoint: challenge: command not found
hacker@paths~explicit-relative-paths-from-:~$ /challenge
ssh-entrypoint: /challenge: Is a directory
hacker@paths~explicit-relative-paths-from-:~$ cd ./
hacker@paths~explicit-relative-paths-from-:~$ challenge/./.
ssh-entrypoint: challenge/./.: No such file or directory
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{UDuBPApIynvpFZJM67N8-0aVOnZ.dBTN1QDL5IjN0czW}
hacker@paths~explicit-relative-paths-from-:/$ 
```
## 8) implicit relative path
```bash
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{0VnsSqcQazcF6FGKQvuLAd2I8SC.dFTN1QDL5IjN0czW}
```

## 9) home sweet home 
```bash
hacker@paths~home-sweet-home:~$ cd ~
hacker@paths~home-sweet-home:~$ cd /
hacker@paths~home-sweet-home:/$ cd ~
hacker@paths~home-sweet-home:~$ /challenge/run
You must provide an argument to /challenge/run when you invoke it!
hacker@paths~home-sweet-home:~$ /challenge/run ~
Writing the file to /home/hacker!
/challenge/run: line 29: /home/hacker: Is a directory
... and reading it back to you:
cat: /home/hacker: Is a directory
hacker@paths~home-sweet-home:~$ cat ~
cat: /home/hacker: Is a directory
hacker@paths~home-sweet-home:~$ /challenge/run ~h
The argument you provided is not an absolute path!
hacker@paths~home-sweet-home:~$ /challenge/run ./~
The argument you provided is not an absolute path!
hacker@paths~home-sweet-home:~$ /challenge/run /.~
The argument you provided is not under your home directory!
hacker@paths~home-sweet-home:~$ /challenge/run
You must provide an argument to /challenge/run when you invoke it!
hacker@paths~home-sweet-home:~$ /challenge/run ~
Writing the file to /home/hacker!
/challenge/run: line 29: /home/hacker: Is a directory
... and reading it back to you:
cat: /home/hacker: Is a directory
hacker@paths~home-sweet-home:~$ cd ~
hacker@paths~home-sweet-home:~$ ls
Desktop
hacker@paths~home-sweet-home:~$ /challenge/run ~/~
Writing the file to /home/hacker/~!
... and reading it back to you:
pwn.college{k0EtJ0AiPIRkLkzzvrevuqRDR4n.dNzM4QDL5IjN0czW}
```
