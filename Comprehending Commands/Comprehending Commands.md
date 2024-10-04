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
```
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```
Now the challenge wants us to find renamed run file in /challenge by listing the files and then invoke it.
```bash
hacker@commands~listing-files:~$ ls /challenge
5219-renamed-run-10698  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/5219-renamed-run-10698
Yahaha, you found me! Here is your flag:
pwn.college{gM7DYlrIzX2YFWyUhLx9FwCFh7g.dhjM4QDL5IjN0czW}
hacker@commands~listing-files:~$ 
```
## touching files

We can create a new, blank file by touching it with the touch command.
The challenge requires us to create two new files /tmp/pwn and /tmp/college, and run /challenge/run to get the flag.
```bash
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ ls
bin  hsperfdata_root  tmp.MiOQGWw5Zc
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.MiOQGWw5Zc
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{w2silAEzg1yfi24sGgXmtCnPzH7.dBzM4QDL5IjN0czW}
```
I entered the /tmp directory with cd command and then checked the already present files inside with ls command.
I then used touch command to create two new files with pwn and college names and then again ran the ls command to check if my new files had been added or not.

## removing files

An example in pwn.college that perfectly illustrates the process of removing files: 
```bash
In Linux, we remove files with the rm command, as so:

hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```
Now the challenge was to delete the delete_me file from the home directory and then run the command challenge/check to get the file.
```bash
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{gULQiHr4yI2E9mgipU99PqeEVw3.dZTOwUDL5IjN0czW}
```
## hidden files

ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts. To view them with ls, we need to invoke ls with the -a flag, as illustrated in the example on pwn.college:
```
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
```
The challenge is to find the flag, hidden as a dot-prepended file in /.
```bash
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.                      bin        etc    lib64   nix   run   tmp
..                     boot       home   libx32  opt   sbin  usr
.dockerenv             challenge  lib    media   proc  srv   var
.flag-145862451510170  dev        lib32  mnt     root  sys
hacker@commands~hidden-files:/$ cat .flag-145862451510170
pwn.college{keyqeuxUQmwL7ciDlZLxrHEqVtC.dBTN4QDL5IjN0czW}
```
I first entered the / by invoking the cd command and then ran the ls -a command to display the list of all files in / directory, including the hidden files. One file among them started with .flag which hints that it must contain the flag I am looking for so I simple displayed the contents of that file using the cat command to get the flag.

## An epic filesystem quest

I must say this was insanely fun to do. In the long run this might just be a practice of some simple commands but for the current me it was a bit challenging and took some thought at some junctions. 

I will add the entire thing from the command prompt here and explain my thought process in a summary at critical junctions:

```bash
acker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls 
TEASER  challenge  flag  lib32   media  opt   run   sys  var
bin     dev        home  lib64   mnt    proc  sbin  tmp
boot    etc        lib   libx32  nix    root  srv   usr
hacker@commands~an-epic-filesystem-quest:/$ ls -a
.           TEASER  challenge  flag  lib32   media  opt   run   sys  var
..          bin     dev        home  lib64   mnt    proc  sbin  tmp
.dockerenv  boot    etc        lib   libx32  nix    root  srv   usr
hacker@commands~an-epic-filesystem-quest:/$ cat TEASER
Great sleuthing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/networkx/__pycache__

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/local/lib/python3.8/dist-packages/networkx/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/__pycache__$ ls
GIST                     convert_matrix.cpython-38.pyc
__init__.cpython-38.pyc  exception.cpython-38.pyc
conftest.cpython-38.pyc  lazy_imports.cpython-38.pyc
convert.cpython-38.pyc   relabel.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/__pycache__$ cat GIST
Tubular find!
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/networkx/__pycache__$ cd /usr/lib/python3/dist-packages/matplotlib/testing/jpl_units
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/
ssh-entrypoint: hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/: No such file or directory
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/matplotlib/testing/jpl_units$ ls
Duration.py  EpochConverter.py  StrConverter.py  UnitDblConverter.py  __init__.py
Epoch.py     INSIGHT            UnitDbl.py       UnitDblFormatter.py  __pycache__
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/matplotlib/testing/jpl_units$ cat INSIGHT
Lucky listing!
The next clue is in: /opt/linux/linux-5.4/tools/arch/s390

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/matplotlib/testing/jpl_units$ cd /opt/linux/linux-5.4/tools/arch
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ ls
alpha  arc  arm  arm64  csky  h8300  hexagon  ia64  microblaze  mips  parisc  powerpc  riscv  s390  sh  sparc  x86  xtensa
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cat s390
cat: s390: Is a directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ grep trapped /s390
grep: /s390: No such file or directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ grep trapped /opt/linux/linux-5.4/tools/arch/s390
grep: /opt/linux/linux-5.4/tools/arch/s390: Is a directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ grep trapped /opt/linux/linux-5.4/tools/arch/s390
grep: /opt/linux/linux-5.4/tools/arch/s390: Is a directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ grep clue /opt/linux/linux-5.4/tools/arch/s390
grep: /opt/linux/linux-5.4/tools/arch/s390: Is a directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cat /opt/linux/linux-5.4/tools/arch/s390
cat: /opt/linux/linux-5.4/tools/arch/s390: Is a directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cat /s390
cat: /s390: No such file or directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ ls -a
.  ..  alpha  arc  arm  arm64  csky  h8300  hexagon  ia64  microblaze  mips  parisc  powerpc  riscv  s390  sh  sparc  x86  xtensa
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cat s390
cat: s390: Is a directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cat /s390/trapped
cat: /s390/trapped: No such file or directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cat /s390/clue
cat: /s390/clue: No such file or directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cat /s390/flag
cat: /s390/flag: No such file or directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ ls /s390
ls: cannot access '/s390': No such file or directory
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ ls s390
MEMO-TRAPPED  include
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cat s390/MEMO-TRAPPED
Lucky listing!
The next clue is in: /opt/linux/linux-5.4/arch/sh/kernel/vsyscall
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/arch$ cd /opt/linux/linux-5.4/arch/sh/kernel/vsyscall
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/sh/kernel/vsyscall$ ls 
Makefile  POINTER  vsyscall-note.S  vsyscall-sigreturn.S  vsyscall-syscall.S  vsyscall-trapa.S  vsyscall.c  vsyscall.lds.S
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/sh/kernel/vsyscall$ cat POINTER
Great sleuthing!
The next clue is in: /usr/share/locale/id/LC_MESSAGES

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/sh/kernel/vsyscall$ cd /usr/share/locale/id/LC_MESSAGES
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/id/LC_MESSAGES$ ls -a
.   .SPOILER  iso_15924.mo   iso_3166-2.mo  iso_3166.mo    iso_4217.mo   iso_639-3.mo  iso_639.mo    iso_639_5.mo
..  dpkg.mo   iso_3166-1.mo  iso_3166-3.mo  iso_3166_2.mo  iso_639-2.mo  iso_639-5.mo  iso_639_3.mo  sphinx.mo
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/id/LC_MESSAGES$ cat .SPOILER
Congratulations, you found the clue!
The next clue is in: /opt/radare2/shlr/sdb

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/share/locale/id/LC_MESSAGES$ cd /opt/radare2/shlr/sdb
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/sdb$ ls -a
.  ..  .WHISPER  Makefile  README.md  config.mk  include  memcache  meson.build  sdb  src  test  wasi.mk  wasi.sh
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/sdb$ cat .WHISPER
Tubular find!
The next clue is in: /opt/linux/linux-5.4/drivers/soc/bcm/brcmstb/pm

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/sdb$ ls /opt/linux/linux-5.4/drivers/soc/bcm/brcmstb/pm
Makefile  NUGGET-TRAPPED  aon_defs.h  pm-arm.c  pm-mips.c  pm.h  s2-arm.S  s2-mips.S  s3-mips.S
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/sdb$ cat /opt/linux/linux-5.4/drivers/soc/bcm/brcmstb/pm/NUGGET-TRAPPED
Great sleuthing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/sympy/solvers/ode/__pycache__

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/sdb$ ls /usr/local/lib/python3.8/dist-packages/sympy/solvers/ode/__pycache__
DISPATCH-TRAPPED               lie_group.cpython-38.pyc       riccati.cpython-38.pyc    systems.cpython-38.pyc
__init__.cpython-38.pyc        nonhomogeneous.cpython-38.pyc  single.cpython-38.pyc
hypergeometric.cpython-38.pyc  ode.cpython-38.pyc             subscheck.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/sdb$ cat /usr/local/lib/python3.8/dist-packages/sympy/solvers/ode/__pycache__/DISPATCH-TRAPPED
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{U183WkGSVuGlBug6ouQ4rYpA-ZW.dljM4QDL5IjN0czW}
```
So first I moved into the / directory with cd command and then listed all the files in it with ls. Then I used cat command to read the obviously suspicious files written in bold. Each of them gave me a new directory to move into to gather more clues.
The challenging part was when I was asked to read a file from the directory given without using the cd command. This took a while to figure out, I kept trying to read the s390 directory at the end of the path provided the previous clue. Then I thought again and noticed that I could try using these cat and ls commands just like cd by providing them with an entire path instead of just a directory or a file. Hence I used ls on the entire path which then listed all the file in the s390 directory which I was struggling with. Now I could again provide cat command with the entire path as the argument, of course after adding the clue file at the end of the path which I discovered with ls. After that the challenge was solved fairly quickly with my improved understanding of these commands.

## making directories

mkdir command is used to make directories.
This is illustrated by the following example:

```bash
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
```
Challenge is to make a /tmp/pwn directory and make a college file in it and then invoke the /challenge/run to get the flag

```bash
hacker@commands~making-directories:~$ cd /tmp
hacker@commands~making-directories:/tmp$ mkdir pwn
hacker@commands~making-directories:/tmp$ ls 
bin  hsperfdata_root  pwn  tmp.MiOQGWw5Zc
hacker@commands~making-directories:/tmp$ cd pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ ls
college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{g5v4b7x8dPl0bpIdLB_wduDbohX.dFzM4QDL5IjN0czW}
```
I cd'd into the tmp directory and then used the mkdir command to make pwn directory, checked if it worked with ls command and then again cd'd into the newly made pwn directory where I used the touch command to make a file with the name college which I again cross checked with ls. 

Finally ran the /challenge/run command to get the flag.

