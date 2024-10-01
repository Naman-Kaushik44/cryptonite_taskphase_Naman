# Intro to Commands

First I generated an SSH key by running ``ssh-keygen -f key -N ''`` command in a terminal on Linux enviornment which generated key and key.pub files.
I copied the contents of the key.pub file by outputting it's content to the terminal with the ``cat key.pub`` command.
Then I linked my public SSH key to my pwn.college account and connected to the dojo with ``ssh -i ./key hacker@pwn.college`` command and started the challenge under Intro to commands in the Hello Hackers module of Linux Lumanarium.
I followed the instructions written in the challenege that asked me to invole the ``hello`` command and successfully obtained the flag.
```bash
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{0I9CtQQglRviLWk3UqGXJ-UXnnE.ddjNyUDL5IjN0czW}
```
