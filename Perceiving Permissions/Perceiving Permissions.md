# Perceiving Permissions

## Changing file ownership

```bash
hacker@permissions~changing-file-ownership:~$ ls -l
total 32
-rw-r--r-- 1 hacker hacker    4 Oct  9 04:55  COLLEGE
drwxr-xr-x 2 hacker hacker 4096 Sep 30 16:06  Desktop
-rw-r--r-- 1 hacker hacker    8 Oct  9 05:33  PWN
-rw-r--r-- 1 hacker hacker  829 Oct  9 05:30  instructions
-rw-r--r-- 1 hacker hacker   93 Oct  9 05:30  myflag
lrwxrwxrwx 1 hacker hacker    5 Oct  5 01:59  not-the-flag -> /flag
-rw-r--r-- 1 root   hacker   77 Oct  9 06:00  pwn_output
-rw-r--r-- 1 hacker hacker  435 Oct  9 05:24  the-flag
-rw-r--r-- 1 root   hacker   58 Oct  2 19:38 '~'
hacker@permissions~changing-file-ownership:~$ chown hacker pwn_output
hacker@permissions~changing-file-ownership:~$ cat pwn_output
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "oNs6OOwC"
hacker@permissions~changing-file-ownership:~$ cat PWN
COLLEGE
hacker@permissions~changing-file-ownership:~$ cat the-flag
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
hacker@permissions~changing-file-ownership:~$ chown hacker '~'
hacker@permissions~changing-file-ownership:~$ cat '`'
cat: '`': No such file or directory
hacker@permissions~changing-file-ownership:~$ cat '~'
pwn.college{k0EtJ0AiPIRkLkzzvrevuqRDR4n.dNzM4QDL5IjN0czW}
hacker@permissions~changing-file-ownership:~$ cat not-the-flag
cat: not-the-flag: Permission denied
hacker@permissions~changing-file-ownership:~$ chown hacker  not-the-flag
hacker@permissions~changing-file-ownership:~$ cat not-the-flag
pwn.college{EhC9EIXfTDQ4FgeU_6fNwaNekKH.dFTM2QDL5IjN0czW}
```
## Groups and Files
