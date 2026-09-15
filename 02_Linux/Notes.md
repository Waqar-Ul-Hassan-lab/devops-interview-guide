## 20 Basic Linux Commands

| # | Command | Stands For | Description | Common Flags / Usage |
|---|---------|------------|-------------|----------------------|
| 1 | `pwd` | Print Working Directory | Print current working directory | `pwd` |
| 2 | `ls` | List | List files and directories | `ls -la`, `ls -lh`, `ls -ltr` |
| 3 | `cd` | Change Directory | Change directory | `cd ~`, `cd ..`, `cd /path/to/dir` |
| 4 | `mkdir` | Make Directory | Make directory | `mkdir dirname`, `mkdir -p path/to/dir` |
| 5 | `rmdir` / `rm` | Remove Directory / Remove | Remove directory or files | `rmdir dirname`, `rm -rf dirname` |
| 6 | `touch` | Touch | Create an empty file or update timestamp | `touch filename.txt` |
| 7 | `cat` / `less` | Concatenate / Less | View and concatenate file content | `cat file.txt`, `less file.txt` |
| 8 | `head` | Head | Display first few lines of a file | `head -n 10 file.txt` |
| 9 | `tail` | Tail | Display last few lines of a file | `tail -n 10 file.txt`, `tail -f app.log` |
| 10 | `grep` | Global Regular Expression Print | Search for a pattern in files | `grep "pattern" file.txt`, `grep -rn "pattern" .` |
| 11 | `find` | Find | Search for files and directories | `find . -name "*.log"`, `find / -type f` |
| 12 | `systemctl` | System Control | Control and inspect systemd services | `systemctl status <service>`, `systemctl restart <service>` |
| 13 | `chmod` / `chown` | Change Mode / Change Owner | Change file permissions and ownership | `chmod 755 file.sh`, `chown user:group file.txt` |
| 14 | `ps` / `top` / `htop` | Process Status / Table of Processes / Hisham's Top | Process monitoring and management | `ps aux`, `top`, `htop` |
| 15 | `kill` | Kill | Terminate processes | `kill <PID>`, `kill -9 <PID>` |
| 16 | `df` | Disk Free | Report file system disk space usage | `df -h` |
| 17 | `du` | Disk Usage | Estimate file/directory space usage | `du -sh *` |
| 18 | `ssh` | Secure Shell | Secure shell for remote login | `ssh user@host` |
| 19 | `scp` | Secure Copy | Secure copy files between hosts | `scp file.txt user@host:/path` |
| 20 | `rsync` | Remote Sync | Remote fast file synchronization | `rsync -avz src/ dest/` |
| 21 | `wget` | Web Get | Download files from the internet | `wget https://example.com/file.zip` |
| 22 | `sudo du -sh *` | disk usage shell command | Execute command with superuser/root privileges | `sudo du -sh *`, `sudo systemctl ...` |

---

## 1. You lost .pem file, can you restore it ?
## 2. And how will you connect to ec2 instance ?

- PEM stands for Privacy Enhanced Mail
- It is asymetric key, so it is not possible to restore it.
- And it is very difficult to connect to ec2 instance if you lost .pem file.
- But you still can connect to ec2 instance if you have access to it via AWS Console.
- You can use the ec2 instance connect, Session Manager, SSH Client
- One can also generate the ssh-keygen rsa pair to use public private key for sshing. 

---

## What if your /var directory is 90% occupied ?

- slash var is the directory which is used to store the variable data of the system.
- It stores the logs files in /var/log of the services like web server, database, application etc.
- First you will check which directory is taking too much space.
- This directory has logs so lets suppose they are having a lot of space.
- You can delete, perform rotation or zip the logs to free the space.
- Also you can clean the cache files by running `sudo apt clean` and `sudo apt autoclean`
- One can also check the tmp directory and clean it

---

## Linux server is slow due to high CPU utilizatin ? Give solution

- Login to ec2 instance
- Run the command top/htop
- Find the list of resources which is eating more cpu
- Then get the PID of those resources and check the details.
- If the process is not important, kill it
- Else manage the process by nice/renice commands

---

## Ngnix deployed application return connection refused ?

- To fix, first find either the ngnix service is running or not
- By running the command, `sudo systemctl status ngnix`
- If the ngnix is in stop state, fix it by starting it
- Also check the Firewall rules if any exists
- If it is an ec2 instance then check the security groups and rules
- Check the inbound traffic rules
- Check for the additional layers like
- API Gateways, Load Balancers etc

---

## Why SSH into ec2 instance failed ? 

- First check if the instance is running by `sudo systemctl status sshd`
- Check if the id address ,pem file & path, SSH commands are correct
- Check the permissions of Pem file
- Check if there is any firewall blocking the ssh port
- Check for the inbound traffic rules like port 22

---

## How to List the log files older than 7 days ?

- `sudo find /var/log -type f -name *.log`
-  you can add the flag `-mtime +7` to see older than 7 days
- `sudo find /var/log -type f -name *.log -mtime +7 -exec ls -ltr {} \;`

---

## Find and remove the 7 days older log files in /var/log directory ?

-  `sudo find /var/log -type f -name "*.log" -mtime +7 -exec rm {} \;`

---

## Cron job & shell script ?
## Compress 7 days older logs and delete 30 days older in /var/log/myapp/.

- Cron is a time-based job scheduler in Unix-like operating system. It is used to schedule jobs (commands or shell scripts) to run automatically at specified times.
- First check if specific directory exist or not
- find and compress the 7 days older files
- find and delete the files older than 7 days
- Keep a record of the actions performed
- You are executing the script by a cron job not manually

---

## Bulk user creation by CSV file ?

# sample csv file
``` 
Username,Password,GroupName
waqar,123456,admin
John,123456,dev
Jane,123456,qa
``` 
- first check for the csv file exist or not
- Then start from the 2nd line to last one
- Then give the output of the 2nd step to while loop
- then write the bash script code to do this.

---

## Find and delete files over 1000MB

- `sudo find /var/ -type f -size +1000M -exec rm -i {} \;`

---

## Get list of users who logged in 

- ` last -F` gives the list of all the users who have logged in and out
- `last -F | grep "$(date '+%b %e')" ` give the only logged users of today 
- `last -F | grep "$(date '+%b %e')" | awk '{print $1}' | uniq ` awk gets first column

---

## Website doesn't load ?

- first check the ngnix status `sudo systemctl status ngnix`
- check the /var/log/nginx/error.log file
- check the path of html file correct or not

---

## Delete the first and last line of file

- ` 'sed 1d;$d' file.txt ` will print the output and doesn't change file content
- ` 'sed -i 1d;$d' file.txt` will print nothing but edit the file content