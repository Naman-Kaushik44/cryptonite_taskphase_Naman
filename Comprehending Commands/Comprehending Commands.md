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

## grepping for a needle in a haystack

Sometimes when the file is too big, its not possible to cd and read it so we only search for the relevant lines from the text with the help of the grep command.

hacker@dojo:~$ grep SEARCH_STRING /path/to/file

Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

Now the challege wants us to find the flag from a 100k line text.
So we grep the file out of it by providing the argument pwn.college along with the file path /challenge/data.txt to it since every flag on pwn.college start with that.
```bash
Connected!
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{Y5W1OXnWuLoZojijFj93nM_xtPZ.ddTM4QDL5IjN0czW}
```

## listing files
Directories can have a lot of file and other directories inside of them and they can be listed using the ls command.
ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided.

An example of this given on pwn.college is: 

hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$

Now the challenge wants us to find renamed run file in /challenge by listing the files and then invoke it.
```bash
hacker@commands~listing-files:~$ ls /challenge
5219-renamed-run-10698  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/5219-renamed-run-10698
Yahaha, you found me! Here is your flag:
pwn.college{gM7DYlrIzX2YFWyUhLx9FwCFh7g.dhjM4QDL5IjN0czW}
hacker@commands~listing-files:~$ 
```
## 










