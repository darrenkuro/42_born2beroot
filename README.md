<h1 align="center">BORN2BEROOT</h1>

<p align="center">
    <img alt="score" src="https://img.shields.io/static/v1?label=status&message=ongoing&color=red&logo=42&logoColor=green">
    <img alt="date" src="https://img.shields.io/static/v1?label=date&message=May%2014th,%202023&color=ff6984&logo=Cachet&logoColor=green">
    <img alt="size" src="https://img.shields.io/github/languages/code-size/darrenkuro/42_born2beroot?label=size">
    <img alt="loc" src="https://img.shields.io/tokei/lines/github/darrenkuro/42_born2beroot?label=lines">
    <img alt="file" src="https://img.shields.io/github/directory-file-count/darrenkuro/42_born2beroot/submitted?label=files">
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


#### What are the differences between `aptitude` and `apt`?

They are both package managers for Debian-based Linux system, with minor differences, such that `aptitude` has text-based interface while `apt` has a command-line interface. Essentially, `aptitude` is a more complex version that is build on `apt` and is suitable for more advanced system administrators for more complex tasks. 

#### What is `SELinux`?

`SELinux` is `Security-Enhanced Linux`, a security framework for Linux system that provides a mandatory access control (MAC) mechanism to restrict and control access to system resources. 

#### What is `AppArmor`?


