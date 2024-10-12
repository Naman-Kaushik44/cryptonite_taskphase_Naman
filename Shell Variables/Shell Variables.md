# Shell Variables

## Printing Variables

```bash
Connected!
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{A8V-xaxfiGWub0PCJqn1IzWAqT6.ddTN1QDL5IjN0czW}
```
## Setting Variables

```bash
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{AH3mK2gN55Hbf6qk4rMGmlQBtAD.dlTN1QDL5IjN0czW}
```
## Multi Word Variables

```bash
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{IUJgooAEu1RopQz_Cn7ACYgZFlp.dBjN1QDL5IjN0czW}
```
## Exporting Examples 

```bash
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ sh
sh-5.2$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{4L0oe3UDblh6r8ICdFgfUi_2Z4M.dJjN1QDL5IjN0czW}
```
