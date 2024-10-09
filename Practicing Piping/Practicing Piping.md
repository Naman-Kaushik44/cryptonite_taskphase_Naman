# Practicing Piping

This module is about input and output redirection. Simply put, every process in Linux has three initial, standard channels of communication:

Standard Input is the channel through which the process takes input. For example, the shell uses Standard Input to read the commands that we input.
Standard Output is the channel through which processes output normal data, such as the flag when it is printed to us in previous challenges or the output of utilities such as ls.
Standard Error is the channel through which processes output error details. For example, if we mistype a command, the shell will output, over standard error, that this command does not exist.

These three channels are used so frequently in Linux, they are known by shorter names: stdin, stdout, stderr.

## Redirecting Output

``>`` is used to redirect the stdout to files.

In this challenge we were required to redirect PWN to the filename COLLEGE. 

I just used the echo command which helps us print the argument to the terminal and then redirected it to the COLLEGE file to get the flag.

```bash
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{cHlQ5oNL24SXd4KcprW8QtJPvaW.dRjN1QDL5IjN0czW}
```
## Redirecting more Output

``>`` can be used to redirect the output from any command.
In this challenge we were required to redirect the stdout of /challenge/run to myflag file to get the flag.

/challenge/run still prints to thw terminal even after redirecting it's stdout because of it communicates its instructions and commands over the stderror and only prints the flag over stdout.

```bash
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{USwoYe-xIDs_N3b_y2HlJ3io378.dVjN1QDL5IjN0czW}
```
## Appending Output 

```bash
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{YgI_qYUtQyanTnTHIqnlgzXw4Pp.ddDM5QDL5IjN0czW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
```

## Redirecting Errors

```bash
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{YqyzVunMVHKsfjyVCs9jtmsapO0.ddjN1QDL5IjN0czW}

hacker@piping~redirecting-errors:~$ cat instructions
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will check that error output is redirected to a specific file path : instructions
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
```

## Redirecting Input 

```bash
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{0z3D8SvPf8d-ggmzi9eF3HO5lfZ.dBzN1QDL5IjN0czW}
```
## Grepping stored results

```bash
hacker@piping~grepping-stored-results:~$ /challenge/run >  /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
pwn.college{kmixtArgzxxaoWqoC3vrbNtu91_.dhTM4QDL5IjN0czW}
```
## Grepping Live Output

```bash
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{kIr5m7gJszq0O-l0rBF-TGFD2Oz.dlTM4QDL5IjN0czW}
hacker@piping~grepping-live-output:~$ 
```
## Grepping Errors

```bash
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{8HOxbJcT7KAZmuzQO-doJsB3eiT.dVDM5QDL5IjN0czW}
```
## Duplicating piped data with tee

```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee pwn_output | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat pwn_output
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "oNs6OOwC"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret oNs6OOwC | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{oNs6OOwCCF8_daCXkhOfkEmQQ2t.dFjM5QDL5IjN0czW}
```
## Writing to Multiple Programs

```bash
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
This secret data must directly and simultaneously make it to /challenge/the and 
/challenge/planet. Don't try to copy-paste it; it changes too fast.
2872031037138545782
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{Ugdw5_SySdwRgoU7BRA1oUqzf75.dBDO0UDL5IjN0czW}
```
## Split-Piping stderr and stdout

```bash
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack | 2>(/challeneg/the) >(/challenge/planet)
ssh-entrypoint: /challeneg/the: No such file or directory
ssh-entrypoint: 2/dev/fd/63: No such file or directory
Are you sure you're properly redirecting /challenge/hack's standard output into 
'/challenge/planet'?
You must redirect my standard error into '/challenge/the'!
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack | tee 2>(/challeneg/the) >(/challenge/planet)
ssh-entrypoint: /challeneg/the: No such file or directory
tee: 2/dev/fd/63: No such file or directory
This secret data must directly make it to /challenge/planet over my stdout. 
Don't try to copy-paste it; it changes too fast.
1521128053136516794
You must redirect my standard error into '/challenge/the'!
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2>&1 | >(/challeneg/the) >(/challenge/planet)
ssh-entrypoint: /challeneg/the: No such file or directory
ssh-entrypoint: /dev/fd/63: Permission denied
Are you sure you're properly redirecting /challenge/hack's standard output into 
'/challenge/planet'?
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack | >(/challenge/planet) 2>& 1 | >(/challenge/the)
ssh-entrypoint: /dev/fd/63: Permission denied
Are you sure you're properly redirecting /challenge/hack's standard output into 
Are you sure you're properly redirecting /challenge/hack's standard error into 
'/challenge/planet'?
'/challenge/the'?
You must redirect my standard error into '/challenge/the'!
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack | >(/challenge/planet) 2> >(/challenge/the)
Are you sure you're properly redirecting /challenge/hack's standard error into 
'/challenge/the'?
You must redirect my standard error into '/challenge/the'!
Are you sure you're properly redirecting /challenge/hack's standard output into 
'/challenge/planet'?
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack | /challenge/planet 2>&1 | /challenge/the
You must redirect my standard error into '/challenge/the'!
You are redirecting standard error *of /challenge/planet*! Instead, you must 
redirect standard error of 'hack'. This must be done *before* any |. The right 
side of the pipe is a different command, with its own redirection, than the 
left side!
Are you sure you're properly redirecting /challenge/hack's standard error into 
'/challenge/the'?
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack | /challenge/planet >(/challenge/the)
You must redirect my standard error into '/challenge/the'!
Are you sure you're properly redirecting /challenge/hack's standard error into 
'/challenge/the'?
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack | /challenge/planet >(/challenge/the)
You must redirect my standard error into '/challenge/the'!
Are you sure you're properly redirecting /challenge/hack's standard error into 
'/challenge/the'?
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >(/challenge/planet) 2> >(/challenge/the)
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{MrleifJEzZVCOQ9evIN7erD-5ul.dFDNwYDL5IjN0czW}
```
