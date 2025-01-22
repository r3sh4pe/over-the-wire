# Bandit write-up

## Level 1

Username: bandit0 <br>
Password: bandit0

-  Simply connect via `ssh` and look into the readme file.

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit0@bandit.labs.overthewire.org -p 2220
  vi readme
  ```

</details>

## Level 2

Username: bandit1 <br>

- Connect via `ssh`
- Print flag to cli with `cat`
- Have to add `\` in front of `-` to open / use file 

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit1@bandit.labs.overthewire.org -p 2220
  cat .\/-
  ```

</details>

## Level 3

Username: bandit2 <br>

- Connect via `ssh`
- Print flag to cli with `cat`
- Have to wrap filename in quotation marks because of the spaces

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit2@bandit.labs.overthewire.org -p 2220
  cat "spaces in this filename"
  ```

</details>

## Level 4

Username: bandit3 <br>

- Connect via `ssh`
- Print flag to cli with `cat`
- Have to use `\` in front of the dots becaues of the special meaning in linux filenames / filesystem

<details>
  <summary>The way</summary>

  ```shell
  ssh bandit3@bandit.labs.overthewire.org -p 2220
  cat inhere/\.\.\.Hiding-From-You
  ```

</details>

## Level 5

Username: bandit4 <br>

- Connect via `ssh`
- Have to search for the human readable file
- Option 1: By your own or
- Option 2: `for`-loop
- Print flag to cli with `cat`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit4@bandit.labs.overthewire.org -p 2220
  for filename in ./inhere/*; do file "$filename"; done
  cat inhere/-file07
  ```

</details>

## Level 6

Username: bandit5 <br>

- Connect via `ssh`
- Search for the flag with `file`
- Print flag to cli with `cat`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit5@bandit.labs.overthewire.org -p 2220
  find inhere/** -readable -size 1033c ! -executable
  cat inhere/maybehere07/.file2
  ```

</details>

## Level 7

Username: bandit6 <br>

- Connect via `ssh`
- Search for the flag with `file`
- Use `2>/dev/null` to redirect errors
- Print flag to cli with `cat`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit6@bandit.labs.overthewire.org -p 2220
  find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
  cat /var/lib/dpkg/info/bandit7.password
  ```

</details>

## Level 8

Username: bandit7 <br>

- Connect via `ssh`
- Search for the flag with `cat` and pipe to `grep`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit7@bandit.labs.overthewire.org -p 2220
  cat data.txt | grep "millionth"
  ```

</details>

## Level 9

Username: bandit8 <br>

- Connect via `ssh`
- Search for the flag with `cat` and pipe to `grep` and `uniq -u` afterwards

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit8@bandit.labs.overthewire.org -p 2220
  cat data.txt | sort | uniq -u
  ```

</details>

## Level 10

Username: bandit9 <br>

- Connect via `ssh`
- Have to convert to string with `strings` and pipe it to `grep "=="`
- Recognize the flag in the output

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit9@bandit.labs.overthewire.org -p 2220
  strings data.txt | grep '=='
  ```

</details>

## Level 11

Username: bandit10 <br>

- Connect via `ssh`
- Decode text with `base64 -d`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit10@bandit.labs.overthewire.org -p 2220
  base64 -d data.txt
  ```

</details>

## Level 12

Username: bandit11 <br>

- Connect via `ssh`
- Do the ROT13 with `tr`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit11@bandit.labs.overthewire.org -p 2220
  cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
  ```

</details>

## Level 13

Username: bandit12 <br>

- Connect via `ssh`
- follow instruction and create temp dir with `mktemp -d` and copy data.txt
- create file from the hexdump with `xdd -r`h
- do the following until you get a text file:
  -   check compression with `file`
  -   if gzip extend name with .gz and decompress wit `gzip -d`
  -   if bzip2 decompress with `bzip2 -d`
  -   if tar extract with `tar -xf`
  -   if ASCII text `cat` it

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit12@bandit.labs.overthewire.org -p 2220
  mktemp -d
  cp data.txt /tmp/tmp.Hr8NCrTJ01
  cd /tmp/tmp.Hr8NCrTJ01
  xdd -r data.txt data
  ```

</details>

## Level 14

Username: bandit13 <br>

- Connect via `ssh`
- Use `ssh -i` to login with ssh-key on localhost port 2220 as bandit14

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit13@bandit.labs.overthewire.org -p 2220
  ssh -i sshkey.private bandit14@localhost -p 2220
  ```

</details>

## Level 15

Username: bandit14 <br>

- Still connected via `ssh`
- Search for files containing bandit 14 with `find`
- cat /etc/bandit_pass/bandit14 for current password
- open telnet session on port 30000 and paste the current password

<details>
  <summary>The way</summary>
  
  ```shell
  find / -iname "bandit14" 2>/dev/null
  cat /etc/bandit_pass/bandit14
  telnet localhost 30000
  ```

</details>

## Level 16

Username: bandit15 <br>

- Connect via `ssh`
- Connect to localhost port 30001 with `openssl`
- Parse the current password

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit15@bandit.labs.overthewire.org -p 2220
  openssl s_client -connect localhost:30001
  ```

</details>

## Level 17

Username: bandit16 <br>

- Connect via `ssh`
- Simple `nmap` scan to finde open ports
- `nmap` version detection to find the ssl ports
- Pipe the current password to `openssl`. This is necessary because the password starts with k (KEYUPDATE).
- Create a ssh.key file with the response (private key)
- If necessary change permissions to 700
- Connect as bandit17 and get the password

<details>
  <summary>The way</summary>

  ```shell
  ssh bandit16@bandit.labs.overthewire.org -p 2220
  nmap -p 31000-32000 localhost
  nmap -sV -p 31046,31518,31691,31790,31960 localhost
  echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31790
  mktemp -d
  cd # into temp folder
  vi ssh.key # paste private key
  chmod 700 ssh.key
  ssh -i ssh.key bandit17@localhost -p 2220
  cat /etc/bandit_pass/bandit17
  ```

</details>


## Level 18

Username: bandit17 <br>

- Connect via `ssh`
- Compare the files with `diff`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit17@bandit.labs.overthewire.org -p 2220
  diff password.old password.new
  ```

</details>

## Level 19

Username: bandit18 <br>

- Connect via `ssh` and specify shell
- `cat` the readme file
  

<details>
  <summary>The way</summary>

  ```shell
  ssh bandit18@bandit.labs.overthewire.org -p 2220 -t sh
  cat readme
  ```

</details>

## Level 20

Username: bandit19 <br>

- bandit20-do can run every command as user bandit 20 so use it to get bandit20 password

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit19@bandit.labs.overthewire.org -p 2220
  ./bandit20-do cat /etc/bandit_pass/bandit20
  ```

</details>

## Level 21

Username: bandit20 <br>

- Pipe current password into netcat
- Use suconnect

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit12@bandit.labs.overthewire.org -p 2220
  echo "PASSWORD" | nc -l -p 1337
  suconnect 1337
  ```

</details>

## Level 22

Username: bandit21 <br>

- Search in /etc/crontab/ for a possible job / script
- Look into cronjob_bandit22.sh
- Get the flag

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit21@bandit.labs.overthewire.org -p 2220
  cat /etc/cron.d/cronjob_bandit22
  cat /usr/bin/cronjob_bandit22.sh
  cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
  ```

</details>

## Level 23

Username: bandit22 <br>

- Look into the script
- Do the commands with `myname=bandit23`
- Get the flag

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit22@bandit.labs.overthewire.org -p 2220
  cat /usr/bin/cronjob_bandit23.sh
  # On local machine
  myname=bandit23
  mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
  echo $mytarget
  # Back on bandit
  cat /tmp/8ca319486bfbbc3663ea0fbe81326349
  ```

</details>


## Level 24

Username: bandit23 <br>

- Look into the cronjob script
- it will execute all scripts in specific folder if owner == bandit23
- Write script to copy the flag
- Set permissions and cp the script into the right folder

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit23@bandit.labs.overthewire.org -p 2220
  cat /usr/bin/cronjob_bandit24.sh
  # On local machine
  mktemp -d # creates /tmp/tmp.random
  cd /tmp/tmp.random
  nano get_pass.sh

  # Script begin                            
  #!/bin/bash
  
  cp /etc/bandit_pass/bandit24 /tmp/tmp.random/
  chmod 777 /tmp/tmp.random/bandit24
  # Script end

  cp get_pass.sh /var/spool/bandit24/foo
  chmod /var/spool/bandit24/foo/get_pass.sh # if this says file doesn't exist repeat the line before and this line

  # After a minute or two 
  cat /tmp/tmp.random/bandit24
  ```

</details>

## Level 25

Username: bandit24 <br>

- create file with pw + pin
- pipe the file into netcat
- get flag

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit24@bandit.labs.overthewire.org -p 2220
  cd # into temp folder
  for i in $(seq -f "%04g" 0 9999); do echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i" >> pins; done
  cat pins | nc localhost 30002
  ```

</details>

## Level 26

Username: bandit25 <br>

- look for the shell used by bandit 26
- recoginze the the ssh key in `/home/bandit25`
- login to see banner
- exploit the way `more` works

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit25@bandit.labs.overthewire.org -p 2220
  grep bandit26 /home/passwd
  # shows /usr/bin/showtext
  vi /usr/bin/showtext # recognize it opens /home/bandit26/text.txt with more and exit
  # to exploit more resize so the bandit26 ASCII banner shouldn't fit
  ssh -i /home/bandit25/bandit26.sshkey bandit26@localhost -p 2220 # if the scroll funtion of more wasn't trigered decrease the terminal size
  # press v for entering vim
  # In vim for edeting bandit26 password file and get the flag:
  :e /etc/bandit_pass/bandit26
  ```

</details>

## Level 27

Username: bandit26 <br>

- bandit26 will still use showtext as shell so resize the terminal to get `more` started
- open shell in vim
- use the tool located in `/home/bandit26` to get the flag

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit26@bandit.labs.overthewire.org -p 2220
  # press v for entering vim
  # In vim set end execute shell:
  :set shell=/bin/bash
  :shell
  #now in bash session get thw flag:
  ./bandit27-do cat /etc/bandit_pass/bandit27
  ```

</details>

## Level 28

Username: bandit27 <br>

- Clone the repo (with the right port)
- look into the file

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit27@bandit.labs.overthewire.org -p 2220
  mktemp -d 
  cd # into temp dir
  git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
  cat repo/README.md
  ```

</details>

## Level 29

Username: bandit28 <br>

- Clone the repo (with the right port)
- check git history and checkout the interesting commit
- look into the file

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit28@bandit.labs.overthewire.org -p 2220
  mktemp -d
  cd # into temp dir
  git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
  cd repo
  git log
  git checkout 3621de89d8eac9d3b64302bfb2dc67e9a566decd
  cat README.md
  ```

</details>

## Level 30

Username: bandit29 <br>

- Clone the repo (with the right port)
- readme implies der could be development branches
- list branches and serch for the flag
- look into the file

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit29@bandit.labs.overthewire.org -p 2220
  mktemp -d
  cd # into temp dir
  git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo
  cd repo
  git branch -a # dev and sploits-dev seems interessting
  git checkout origin/dev
  cat README.md
  ```

</details>

## Level 31

Username: bandit30 <br>

- Clone the repo (with the right port)
- readme, branch list and commit log gives no hint
- but we can find a tag
- show the ref
<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit30@bandit.labs.overthewire.org -p 2220
  mktemp -d
  cd # into temp dir
  git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo
  cd repo
  git tag
  git show secret
  ```

</details>

## Level 32

Username: bandit1 <br>

- Clone the repo (with the right port)
- we have to commit and push a file according to README.md
- get the flag when file is pushed

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit31@bandit.labs.overthewire.org -p 2220
  mktemp -d
  cd # into temp dir
  git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo
  cd repo
  cat README.md
  echo README.md > key.txt
  vim key.txt # Remove everything but the content
  rm .gitignore # or delete only line
  git add key.txt
  git commit * -m "A very short but and simple message which describes with few words what is happening / fixed or added by the commit so everybode can get the purpose of the commit"
  git push origin master
  ```

</details>