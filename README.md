<h1 align="center">BORN2BEROOT</h1>

<p align="center">
    <img alt="score" src="https://img.shields.io/static/v1?label=score&message=125/100&color=brightgreen&logo=42&logoColor=green">
    <img alt="date" src="https://img.shields.io/static/v1?label=date&message=May%2017th,%202023&color=ff6984&logo=Cachet&logoColor=green">
    <img alt="commit" src="https://img.shields.io/github/last-commit/darrenkuro/42_born2beroot">
</p>

#### sudo

- `sudo visudo` to edit /etc/sudoers (sudo config) to ensure correct syntax and no multiple users editting at once. 
- `/etc/sudoers.d` for addtional config files, these are read in alphabetical order, and can be editted with text editor directly.
- Add `Defaults	passwd_tries=3` to limit to 3 password attempts.
- Add `Defaults	log_input log_out` to record.
- ~~In `/etc/rsyslog.d`, add a file `sudo.conf` with `auth,authpriv.* /var/log/sudo/sudo.log`.~~
- Add `Defaults	logfile="/var/log/sudo/sudo.log"`
- To restart, `sudo systemctl restart rsyslog`.
- `Defaults requiretty` to force tty mode.

#### Password

- `vim /etc/login.defs`

- `PASS_MAX_DAYS	30` -> force user to change password every 30 days
- `PASS_MIN_DAYS	2`
- `PASS_WARN_AGE	7`
- These won't apply to existing users; do it manually for them: `sudo chage -M 30 <user>` `sudo chage -m 2 <user>` `sudo chage -W 7 <user>`
- Verify with `sudo chage -l <user>`
- `/etc/security/pwquality.conf`

#### Users

- `sudo addgroup <group>` to add user group.
- `getent group <group>` to check the group.
- `groups <user>` to check which groups a user belong to.
- `sudo adduser <user>` to add a user. `sudo userdel -r <user>` to delete a user and all associated files (-r).
- `sudo usermod -aG <group> <user>` add user to a group. Same as `sudo adduser <user> <group>`.

#### SSH

- get ip `ip a`.
- Network, use bridged adapter/eno2, on host machine `sh -p4242 dlu@10.15.248.42 (guest ip)`.

#### monitering.sh

- #Architecture: `uname -a`.
- #CPU physical: `lscpu | grep "Socket(s)" | awk -F': *' '{print $2}'`.
- #vCPU: `nproc --all`
- #Memory Usage: `$(free -m | awk '/^Mem:/ {print $3}')/$(free -m | awk '/^Mem:/ {print $2}')MB`. `free | awk '$1 == "Mem:" {printf("%.2f%%\n"), $3/$2 * 100}'`
- #Disk Usage: 

#### What are the differences between `aptitude` and `apt`?

They are both package managers for Debian-based Linux system, with minor differences, such that `aptitude` has text-based interface while `apt` has a command-line interface. Essentially, `aptitude` is a more complex version that is build on `apt` and is suitable for more advanced system administrators for more complex tasks. 

#### What is `SELinux`?

`SELinux` is `Security-Enhanced Linux`, a security framework for Linux system that provides a mandatory access control (MAC) mechanism to restrict and control access to system resources. 

#### What is `AppArmor`?

`AppArmor` is a security framework for Linux; it is a mandatory access control system that works alongside traditional discretionary access control mechanisms like file permissions. It allows admin to enfore detailed security policies for individual programs, it can specifiy what system resources (files, directories, sockets, etc.) a process can access and what operations it can perform.

#### What is `cron`?

`Cron` is a time-based job scheduler. It allows users to schedule and automate the execution of recurring tasks or commands at specified intervals. 

#### LVM

- `sudo vgrename <oldname> LVMGroup`.
- `sudo swappoff /dev/LVMGroup-swap_1` to deactivate it, `sudo lvrename LVMGroup swap_1 swap` to rename. Update `/etc/fstab` with new name; then `sudo swapon /dev/LVMGroup/swap`.

#### Commands
- `dpkg -l | grep <name>` to check a program is installed.
- `sudo ufw status numbered` to get rules with numbers. `sudo ufw allow <port>` to add rules to allow that port connection. `sudo ufw delete <number>` to delete rules.
- `sudo crontab -e` to edit the cron tabs. `sudo systemctl disable cron` will stop cron from running at startup.
- `lsblk` to view partitions.
- `http://10.15.248.42:80` for lighttpd webserver.
- `mysql -u admin -p`, `dlu42`; `show databases` for mariaDB. For wordpress, `dlu` or `dlu@student.42berlin.de`.
- Additional service: `fail2ban`, as a security measure for SSH against brute force attacks. `sudo fail2ban-client status`.
