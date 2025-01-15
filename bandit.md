# Bandit write-up

## Level 0

Username: bandit0 <br>
Password: bandit0

-  Simply connect via `ssh` and look into the readme file.

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit0@bandit.labs.overthewire.org -p 2220
  vi readme
  ```

  <details>
    <summary>Password</summary>

    ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
  </details>
</details>

## Level 1

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

  <details>
    <summary>Password</summary>

    263JGJPfgU6LtdEvgfWU1XP5yac29mFx
  </details>
</details>

## Level 2

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

  <details>
    <summary>Password</summary>

    MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
  </details>
</details>

## Level 3

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

  <details>
    <summary>Password</summary>

    2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
  </details>
</details>

## Level 4

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

  <details>
    <summary>Password</summary>

    4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
  </details>
</details>

## Level 5

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

  <details>
    <summary>Password</summary>

    HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
  </details>
</details>

## Level 6

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

  <details>
    <summary>Password</summary>

    morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
  </details>
</details>

## Level 7

Username: bandit7 <br>

- Connect via `ssh`
- Search for the flag with `cat` and pipe to `grep`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit7@bandit.labs.overthewire.org -p 2220
  cat data.txt | grep "millionth"
  ```

  <details>
    <summary>Password</summary>

    dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
  </details>
</details>

## Level 8

Username: bandit8 <br>

- Connect via `ssh`
- Search for the flag with `cat` and pipe to `grep` and `uniq -u` afterwards

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit8@bandit.labs.overthewire.org -p 2220
  cat data.txt | sort | uniq -u
  ```

  <details>
    <summary>Password</summary>

    4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
  </details>
</details>

## Level 9

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

  <details>
    <summary>Password</summary>

    FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
  </details>
</details>

## Level 10

Username: bandit10 <br>

- Connect via `ssh`
- Decode text with `base64 -d`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit10@bandit.labs.overthewire.org -p 2220
  base64 -d data.txt
  ```

  <details>
    <summary>Password</summary>

    dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
  </details>
</details>

## Level 11

Username: bandit11 <br>

- Connect via `ssh`
- Do the ROT13 with `tr`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit11@bandit.labs.overthewire.org -p 2220
  cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
  ```

  <details>
    <summary>Password</summary>

    7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
  </details>
</details>

## Level 12

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

  <details>
    <summary>Password</summary>

    FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
  </details>
</details>

## Level 13

Username: bandit13 <br>

- Connect via `ssh`
- Use `ssh -i` to login with ssh-key on localhost port 2220 as bandit14

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit13@bandit.labs.overthewire.org -p 2220
  ssh -i sshkey.private bandit14@localhost -p 2220
  ```

  <details>
    <summary>Password</summary>

    MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
  </details>
</details>

## Level 14

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

  <details>
    <summary>Password</summary>

    8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
  </details>
</details>

## Level 15

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

  <details>
    <summary>Password</summary>

    kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
  </details>
</details>

## Level 16

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

  <details>
    <summary>Password</summary>

    EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
  </details>
</details>


## Level 17

Username: bandit17 <br>

- Connect via `ssh`
- Compare the files with `diff`

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit17@bandit.labs.overthewire.org -p 2220
  diff password.old password.new
  ```

  <details>
    <summary>Password</summary>

    x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
  </details>
</details>

## Level 18

Username: bandit18 <br>

- Connect via `ssh` and specify shell
- `cat` the readme file
  

<details>
  <summary>The way</summary>

  ```shell
  ssh bandit18@bandit.labs.overthewire.org -p 2220 -t sh
  cat readme
  ```

  <details>
    <summary>Password</summary>

    cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
  </details>
</details>

## Level 19

Username: bandit19 <br>

- bandit20-do can run every command as user bandit 20 so use it to get bandit20 password

<details>
  <summary>The way</summary>
  
  ```shell
  ssh bandit19@bandit.labs.overthewire.org -p 2220
  ./bandit20-do cat /etc/bandit_pass/bandit20
  ```

  <details>
    <summary>Password</summary>

    0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
  </details>
</details>

## Level 20

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

  <details>
    <summary>Password</summary>

    EeoULMCra2q0dSkYj561DX7s1CpBuOBt
  </details>
</details>

## Level 21

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

  <details>
    <summary>Password</summary>

    tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
  </details>
</details>

## Level 22

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

  <details>
    <summary>Password</summary>

    0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
  </details>
</details>


## Level 23

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

  <details>
    <summary>Password</summary>

    gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
  </details>
</details>