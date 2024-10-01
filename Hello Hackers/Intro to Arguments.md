# Intro to Arguments

From the info given in the challenge I learnt that when I type in a word of text as input, the shell parses that into a command and it's arguments. The first word is the command and the next words are it's arguments.
An example given in the challenge illustrates this as follows 
```bash
hacker@dojo:~$ echo Hello
Hello
hacker@dojo:~$
```
Here echo is the command and Hello is the argument, the echo command basically ''echoes'' all it's arguments back to the terminal.
In the challenge I had to just run the hello command with the argument hackers.
So that just means that I need to put hello as the first word for it to be a command and hackers as the second word for it to be considered an argument.
```bash
Connected!                                                                        
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{IMqdqkaCiHdjt-T9CtDAJOLaWOG.dhjNyUDL5IjN0czW}
```
Another thing I noticed is that once I have put in the command and put in the command to connect into the SSH, it automatically connects to the next challenge that I attempt.
