# Comprehending Commands

## cat : not the pet but the command!

cat is one of the most critical files in linux that is often used for reading files.

If it is given multiple arguments then it will concatenate(hence the name) multiple arguments.
One of the examples given in pwn.college is 

```bash
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```
If there is no argument then it will take from the terminal input and output it.
Challenge is to read the flag file from the home directory so we cat the flag file.

```bash
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{Y7bjo4E9uQbeiEhc0RaMOqECJ3G.dFzN1QDL5IjN0czW}
```

## catting absolute paths

cat arguments can be specified as root directories.

The challenge is to read the flag file from its absolute path /flag.

```bash
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{wUD9VGYlyj6bFtzOR7bJozUn7CY.dlTM5QDL5IjN0czW}
```
## more catting practice

All sorts of paths can be specified as arguments to the cat command, the challenge is to read the flag file by the absolute path and not with the cd command.
```bash
Connected!
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /opt/tcpdump/flag. Go cat it out **without** cding into that 
directory!
hacker@commands~more-catting-practice:~$ cat /opt/tcpdump/flag
pwn.college{M_MSIoDKi5vbPj-f8lJt_qO_pXs.dBjM5QDL5IjN0czW}
```
So I just put in the absolute path provided in the challenge as the argument for the cat command to get the flag.












