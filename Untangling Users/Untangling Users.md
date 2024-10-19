# Untangling Users

## Becoming root with su

```bash
hacker@users~becoming-root-with-su:~$ su
Password: 
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{QiJuyOOqvY_D60DCzMO2ERy4GvV.dVTN0UDL5IjN0czW}
```
## Other users with su

```bash
hacker@users~other-users-with-su:~$ su zardus
Password: 
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{wrn2mn0cU1ubBIMb1ZPi-Vv65rC.dZTN0UDL5IjN0czW}
```
## Cracking Passwords

```bash
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:22 100% 2/3 0.04496g/s 261.8p/s 261.8c/s 261.8C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus
Password: 
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{kGfvaIf5ixJIJmMDHn86GKzMz2Y.ddTN0UDL5IjN0czW}
```

## Using Sudo

```bash
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{8roP8e8r2Z0Osg1Xg0q7Ket9Y3f.dhTN0UDL5IjN0czW}
```
