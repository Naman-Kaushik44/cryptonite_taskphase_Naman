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
What I learnt in this challenge and my approach:-

If the run program is in the challenge directory and the challenge directory is in the /(root directory) then the path to the 'run' challenge program is /challenge/run. Hence to invoke the run challenge program, the run file is exectuted which was in the challenge directory which was in turn inside the / directory.


```bash
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{MoxVNCth38jbdUgECBTT_BXovNv.dVDN1QDL5IjN0czW}
```

## 3) Position thyself

What I learnt in this challenge and my approach:-

The cd (Change Directory) command is used to navigate through directories by passing a path to it as an argument. Basically for any process, the shell is hanging out in some or the other directory and the cd command helps us change it.

For the challenge, it specifically said that the challenge will tell me where I need to cd to before running the /challenge/run program hence I tried running the program straight up without cd to get an error or a prompt telling me about the correct path and the challenge indeed gave it to me after the attempt just like it said it would. Hence I got the flag by using cd command for the right path and then invoking the program.
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

What I learnt in this challenge, my approach and an observation :-

Again the challenge told me to change to a specific directory which I got by trying to invoke the /challenge/run program without it.
Then I changed the directory to it and got the flag by invoking the program /challenge/run.

One observation to be made here is that no matter what directory we are in, if we put in absolute paths everywhere, it won't matter.

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

This challenge was the same as the 3rd challenge, most likely to get us comfortable with cd and absolute paths and to show us the irrelevance of directory location as long as absolute path is being used.

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

For relative paths, the current working directory matters.
What is a relative path?
Ans: A relative path is any path that does not start at root (i.e., it does not start with /) and is interpreted relative to our current working directory (cwd) where our cwd is the directory that our prompt is currently located at.
This means that how we specify a particular file depends on where the terminal prompt is located.

An example given on the pwn.college website illustrates this as follows:

Imagine we want to access some file located at /tmp/a/b/my_file.

    If my cwd is /, then a relative path to the file is tmp/a/b/my_file.
    If my cwd is /tmp, then a relative path to the file is a/b/my_file.
    If my cwd is /tmp/a/b/c, then a relative path to the file is ../my_file. The .. refers to the parent directory.

Now the challenge was to run the /challenge/run program with a relative path while having the current working directory as /.
So we simply change the directory to / and then the current working directory is changed to / and then the relative path will be challenge/run.

```bash
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{o_IO3yJTNHA_JQA0fOW5VC1S4PV.dlDN1QDL5IjN0czW}
```

## 7) explicitive relative paths, from /

We just needed to cd to the / directory and then invoke a relative path.

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

So we just need to cd into the challenge direcory and to use /run we have to explicitly tell Linux that we want to execute the program in the current directory using .

```bash
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{0VnsSqcQazcF6FGKQvuLAd2I8SC.dFTN1QDL5IjN0czW}
```

## 9) home sweet home 

In this challenge we needed to cd into the home directory and run the /challenge/run command with an argument with certain constraints which are as follows :- 

Your argument must be an absolute path.

The path must be inside your home directory.

Before expansion, your argument must be three characters or less.

Hence I put in the argument as ~/~ which satisfies all three of these conditions.


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
