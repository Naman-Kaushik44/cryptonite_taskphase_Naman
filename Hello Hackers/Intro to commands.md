# Intro to Commands

First I generated an SSH key by running ``ssh-keygen -f key -N ''`` command in a terminal on Linux enviornment which generated key and key.pub files.
I copied the contents of the key.pub file by outputting it's content to the terminal with the ``cat key.pub`` command.
Then I linked my public SSH key to my pwn.college account and connected to the dojo with ``ssh -i ./key hacker@pwn.college`` command and started the challenge under Intro to commands in the Hello Hackers module of Linux Lumanarium.
The challenge taught me the initial information about commands, I basically understood that when I enter a command and hit enter, the command will be invoked.
An example given before the challenge is as follows:
```bash
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$
```
So here whoami is a simple command that returns the name of the user(hacker here).
I also learnt that commands are case sensitive.

The challenge asked me to invole the ``hello`` command and successfully obtained the flag.
```bash
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{0I9CtQQglRviLWk3UqGXJ-UXnnE.ddjNyUDL5IjN0czW}
```
