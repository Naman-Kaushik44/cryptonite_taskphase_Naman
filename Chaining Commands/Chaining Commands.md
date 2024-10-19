# Chaining Commands

## Chaining with Semicolons

The challenge required me to chain two commands using ; to get the flag.

```bash
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{8iaiPR3W38bK-SYu8Fx1oWVUrTG.dVTN4QDL5IjN0czW}
```

## Your first Shell Script

```bash
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ echo /challenge/pwn > x.sh
hacker@chaining~your-first-shell-script:~$ echo /challenge/college >> x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{ov-sYcPmjWvFrkllsROnegoYV2c.dFzN4QDL5IjN0czW}
```
First I created a x.sh file with the touch command and then redirected the stdout of echo command in the append mode to x.sh file.
Then I put the x,sh file in the bash's argument to get the flag.

## Redirecting Script Output

```bash
hacker@chaining~redirecting-script-output:~$ touch x.sh
hacker@chaining~redirecting-script-output:~$ echo /challenge/pwn > x.sh
hacker@chaining~redirecting-script-output:~$ echo /challenge/college >> x.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{oK7LpTdlp6VkbTDqCAdQ6CTljxo.dhTM5QDL5IjN0czW}
```
I made a file again(x.sh) then I redirected the outputs of the echo commands in append mode to the x.sh file and ran the bash command with x.sh file as it's argument which I then fed into a pipe and this output was redirected to the /challenge/solve command in the end.

## Executable Shell Scripts

I created a file called shell.sh and then redirected stdout of echo command to it, then I proceeded to check the permission of my newly created file. I then changed the permission for the user to execute the file and then just invoked the file via it's relative path in the home directory to get the flag.
```bash
hacker@chaining~executable-shell-scripts:~$ touch shell.sh
hacker@chaining~executable-shell-scripts:~$ echo /challenge/solve > shell.sh
hacker@chaining~executable-shell-scripts:~$ ls -l shell.sh
-rw-r--r-- 1 hacker hacker 17 Oct 19 17:42 shell.sh
hacker@chaining~executable-shell-scripts:~$ chmode u+x shell.sh
ssh-entrypoint: chmode: command not found
hacker@chaining~executable-shell-scripts:~$ chmod u+x shell.sh
hacker@chaining~executable-shell-scripts:~$ ./shell.sh
Congratulations on your shell script execution! Your flag:
pwn.college{gs4jH27E6aJkNn1SZ5y-vlfqdm2.dRzNyUDL5IjN0czW}
```
