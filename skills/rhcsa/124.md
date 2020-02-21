# 124

  
 2 FILE SYSTEM HIERARCHY hier\(7\) man page

 / root directory

/usr installed soft. ,shared lib. ,static read only data

/usr/bin user commands , binaries

 /usr/sbin system administrator commands , binaries

 /usr/local customized local software

 /usr/lib

 /usr/lib64

 /etc configuration files

 /var variable data persistent between boots, DDBB logs spooled doc printer

 /run data for processes running , recreated on reboot

 consolidates /var/run and /var/lock

/home home directory where regular users store their configuration and personal data files

/root home for root

/tmp temporary space erase at 10 days untouched . /var/tmp this is 30 days

/boot files needed for start boot

/dev devices and other hardware

movement across system file tree

 path begin with / is absolute path if not is a relative path

pwd shows curret directory

ls list content of current directory

 -latr long hidden time ...

cd goes to /home

 .. go back in the tree

 ../.. 2 steps back

 . go current

 /path go to abs path

 - go to the last path

 ~ go to the home directory

 cp file1 file2

 mv file1 file2

 rm file1

 -r recursive for directory, -f force

 mkdir create directory

 cp -r dir1 dir2 copy dir1 as dir2

 mv dir1 dir2 move

 rm -r dir1 delete the entire dir

 rmdir dir1 delete empty directory

 less view text screen by screen

 file globbing , regex for path example touch file{1..100}

\* wildcard

? any character

~ current home directory

 ~username user´s name current home directory

 ~+ current working directory

 ~. previus working directory

 \[abc...\] anyone in

 \[!abc...\] not someone in

 \[^abc...\] not someone in

 \[\[:alpha:\]\] any alphabetic

 \[\[:lower:\]\] any lower case

 \[\[:upper:\]\] any upper case

 \[\[:alnum:\]\] any alphabetic or digit

 \[\[:punct:\]\] any printable not space or alphanumeric

 \[\[:digit:\]\] any digit

 \[\[:space:\]\] any espace ,tab,newline...

 brace expansion {}

 scaping -protecting from brace expansion

 \ scape a single character

 ' ' scape all in

 " " scape all in but resolve variables

 5 MANAGING LOCAL LINUX USER AND GROUP\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

User config files

 users can run process and are owners of files

 /ets/shadow store de password

/etc/passwd flat file with information about local users

 diego:x:1000:1000:diego:/home/diego:/bin/bash as is

 1username 2password \(old\) 3UID 4GID 5GECOS 6home directory 7shell

 diego :x :1000 :1000 :diego :/home/diego :/bin/bash

groups config files

 /etc/groups definiton of groups

 every user has 1 primary group

 for local user, is defined by GID 4 th field of /etc/passwd

 the primary group owns new files created by the user

 created with the same name of the user

 suplementary groups

 created for ensure the user have access permision to files and resources

 of the system

 groupname password GID list of user menbers

 diego :x :1000 :diego

 diego:x:1000:diego as is

 users may be a menber of zero o more suplementary groups

 user of suplementary groups era listed in last field coma separated

gaining superuser access

 polkit threat with graphic part GNOME and its privileges

 su swicht user

 su - change for root

 su - user change for user

 without "-" it doesnt load the enviroment variables of the user

 you must know the password ,this is not recomemdable

 sudo allow use root commands but using the user´s password that executes sudo

 sudo -l shows user's executions capablities

 /var/log/secure is traceable

 /etc/sudoers list of the sudoers if first character is % indicates group

 last line inserted has the priority

cmd

 echo $PATH

 echo $HOME

managing users

 /etc/login.defs rules and ranges for UID GID and administrator UID and GID

cmd useradd username is default enough

 --help

 -u can assigin UID

 usermod --help

 -c add strig to the 5GECOS field

 -g specify a primary group for user account

 -G specify a list of suplementary groups for the user acount

 -a append used with -G to add suplementary gropus without erase

 the previus

 -d specify a new home directory

 -m move the home directory to a new location, mus be used with -d option

 -s specify a new login shell or nologin -s /sbin/nologin

 -L lock user account

 -U unlock user account

 userdel removes the user from /etc/passwd but nor remove the home directory

 -r remove the home directory

 find / -nouser -o -nogroup 2&gt;/dev/null to find unowed files

 cmd

 passwd username used to set new pass or change it

managing groups

 uses the next 4GID in range available

 groupadd -g GID specify a GID 1000+

 -r specify system group 999-

 groupmod -n &lt;oldname&gt; &lt;newname&gt;

 -g &lt;newGID&gt; &lt;group&gt;

 groupdel &lt;group&gt;

 managing user passwords

 stored in /etc/shadow as 2º field

 3 parts format $x$xxxxxxxx$xxxxxxxxxxxxxxxxxxxxxx

 &lt;- salt-&gt;

 $x x=1 md5 hash

 x=5 sha 256

 x=6 sha512

 /etc/shadow format

 1 name

 2 pass

 3 lastchange

 4 minage

 5 maxage

 6 warning

 7 inactive

 8 expired

 9 blank

 chage change aging of a password

 options -d 0 username force pass update at next login

 -m x username set min days before the pass may be changed

 -M x username set max days before the pass must be changed

 -W x username set warning days

 -I x username set days of inactivity

 -E x \(or yyyy-mm-dd\)username set days to expired or a particular day

6 CONTROLING ACCES TO FILES WITH LINUX FILE SYSTEM PERMISSIONS

 permision efect on files efect on directorys

 r read content can be read content may be listed

 w write can change files can create or delete any file subdirectory

 x execute can be executed as a command content of the directory can ba accessed

 the user have usually both permissions on directorys read-only read and exec

 if only read , can be listed but without statistics

 if only exec not list alowed but you can still execute a command

 if you specify explicity de file name

 cmd ls -ld directoryname shows expand file listing and prevent descending in the directory

 managing system command permission from the command line

 as root:

 cmd chmod change mode 2 notations

 symbolic chmod whowhatwhich

 who u,g,o,a user,group, others, all

 what +-= add remove set exactly

 which r w x

 example chmod -R og+rw dir1

 numeric

 example chmod -R 750 file1

 X option carefully ....

 changing file / directory ownership

 only root

 chown user file set user as owner of file

 chown -R user dir set user as owner of dir an its content

 file´s owner

 chown :admin file set group as owner of file

 chown -R :admin dir set group as owner of dir an its content

 may use exactly the same cmd chgrp to managing default premissions and file access

 example drwxrwxrwt 1777 ugo+rwx

 sticky bit

 cmd chmod u+s file suid the file executes as the user that owns the file

 cmd chmod g+s directory sgid the file executes as the group that owns the file

 and in directories create a shared group directory

 chmod o+t sticky, in directories user with write permision only

 can remove files of their own ,cannot remove or save

 files owned by others user

 or s4 s2 t1 so cmd chmod 2750 directory

 default file permissions

 umask example for user 002

 root 022

 permissions granted sub the umask value from 777 ,this is permisions directories

 then sub 111 for the files

 example umask 777 - 0022 = 755 for directories and 755 - 111 =644 for files

 umask cmd is defined in /etc/profile and /etc/bashrc

 user in ~/.bahsrc and ~/.bash\_profile

 8 CONTROLLING SERVICES AND DAEMONS\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

 cmd systemctl used to manage the the system objects, called units

 cmd systemctl -t help

 3 units

 -service represented as .services are frequently accessed daemon, such web serer

 -socket have a .socket , are inter process communication .control of socket will be passed to a daemon or new client connections. similar to the use of ixnetd for

 its services started of demand

 -path have a .path extension, delay the activation of a service until specific file

 change occurs, common for services that use spool directories, as the printing system /var/spool

 service states

 cmd sytemctl status sshd.service shows service status

 keyword descriptions

 loaded unit configuration file has been processed

 active running running 1 or more continuing processes

 active exited succesfully completed a one-time configuration

 active waiting running but waiting for a event

 inactive not running

 enabled will be started at boot time

 disable will not be started at boot

 static can not be enable but may be started for any other enabled unit automatically

 systemctl status replaces services NAME status of old versions

 systemctl used less to paginate

 controlling system services

 systemctl status service info about it

 systemctl stop service

systemctl start service

 systemctl restart service

 systemctl reload service

 systemctl enable service

 systemctl disable service

 systemctl is-enable service

 systemctl mask service

 systemctl umask service

 systemctl list-dependencies service

9 CONFIGURING AND SECURING OPENSSH SERVICE\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

 Connection mode

 cmd w –f to view user an from are connectc

 ~/.ssh/known\_host stored known host

 /etc/ssh/ssh\_host\_key\* stored public key

 ssh remotehost connect as curret user if exist

 ssh username@remotehost connect as indicate user

 ssh username@remotehost cmd connect as indicate user and executes a command

 \# configuring ssh key-based aunthentication

 ssh-keygen generates the public part of the key and private

 ~/.ssh/id\_rsa id\_rsa.pub is the default path

 ssh-copy-id copies the id\_rsa.pub to the destination host

 ssh-copy-id -i ~/.ssh/id\_rsa.pub root@server2 -i to specific path

 \# configuring ssh service configuration

 /etc/ssh/sshd\_config configuration file of openssh

 edit an change

 permitrootlogin root can not login

 permitrootlogin without-password so is

 passwordautentication if is set to no, only login with keystroke

 after changes sshd must be restarted or reloaded cmd systemctl reload sshd

10 analyzing and storing logs\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

 2 services managing the log of syste

 - systemd-journald log of system start send the syslog to rsyslog for managing ,is not persistent in /run/log

- rsyslog stores in /var/log/ directory filter the messages of syslog ,is persistent

log files: /var/log/

 messages - mostly of messages are logged here

 secure - massages about authentication and related error

 maillog - log of mail server related messages

 cron - log file related to periodically executed task-running

 boot.log - startup messages are logged here

 syslog files configuration

 each log message is categorized by a facility \(type of message\) and priority \(the severity of the message\) rsyslog.conf 5 man page

 severities

 0 emerg 4 warning

 1 alert 5 notice

 2 crit 6 info

 3 err 7 debug

configuration file in /etc/rsyslog.conf

customized configuration in /etc/rsyslog.d/\*.conf

 example of log creation

 echo "\*.debug /var/log/messages-debug" &gt;/etc/rsyslog.d/debug.conf

 example of rsyslog.conf

 \#dont log private aunthentication messages

 authpriv.none;\*.info; cron.none /var/log/messages

 \# everyboy has a emergency

 \*.emerg

 \# the /var/log/secure has restrictions

 authpriv.\* /var/log/secure

 \#save errors critical and higher in a especial file.

 uucp,news.crit

 \#boot massages

 local7.\* /var/log/boot.log

in order to avoid the ful of the file system tha contains /var/log the routine logrotate mananage the log files

 that it creates changing the name file for /var/log/messages-yyyymmdd and creates a new to use ,

every certain time, 4 weeks, old log are discarted

 logrotate executed by cron daily .

 analyze a log entry

 1 field timestamp when the log entry was recorded

 2 field the from which log message was sent

 3 field the program or process that sent the the log message

 4 field the actual message sent

 monitor a log file

 cmd tail -f /var/log/messages or other path

 send a syslog message with logger useful to check new logs

 logger -p local7.notice "checkin the log system"

 reviewing systemd journal entries

systemd journal are stores in a structured, indexed binary file

cmd journalctl shows the entrire log system

journalctl -p &lt;priority&gt; debug,info,notice,warning,err,crit,alert,emerg dinwecae

journalctl -n 5 shows only 5 lines ,default is 10

journalctl -f similar to tail -f for

journalctl -o verbose

journalctl --since "yyyy-mm-dd hh:mm:ss" --until "yyyy-mm-dd hh:mm:ss"

 --since today

 \_COMM name of the command

 \_EXE path to the executable for the process

 \_PID \_PID of the process

 \_UID \_UID of the user running process

 \_SYSTEMD\_UNIT the system unit the started the process

 journalctl \_SYSTEMD\_UNIT=sshd.service \_PID=1182

 preserving the systemd journal

 change the default /run/log/journal for /var/log/journal that is persistent

mkdir /var/log/journal

chown root:systemd /var/log/journal

chmod 2755 /var/log/journal

killall -USR1 systemd-journld reboot

journalctl -b show last log

 -b -1 -1 boot

 -b -2 -2 boot

 maintaining accurate time

 timedatectl list-timezones

 tzselet interactive time-zone selecction

 timedatectl set-timezone Americ/Phoenix

 set-time 9:00:00

 timedatectl set-ntp true enables automatic set time thru inet

 configuring the chronyd

 chronyd keep on track the local hardware clock

 2 ways to get it - thru ntp server that needs a inet conexion

 - calculating the time with the driftfile in /etc/chrony.conf

by default chronyd is a down disable service and uses ntp to synchronization , may be useful change the

 ntp servers in a isolated network

 stratum number of hops until reach the reference server \(stratum 0\)

 in /etc/chrony.conf can configure 2 sources of get the time - as server - 1 stratum above the ntp ser

 as peer - stands at the same level stratum

 /etc/chrony.conf example of configuration

 add or replace a line with - name or ip acepted

\# use public servers from pool.ntp.org project

server classroom.example.com iburst iburst option to more accurate clock synchronization

 after changes restart the service cmd systemctl restart chronyd

to verify the ntp server cmd chronyc sources -v

10 MANAGING RED HAT ENTERPRISE LINUX NETWORKING\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

validating a network configuration

 ip addr show eth0 shows device a add information

 - show the status of active interface

 -link lines is the MAC

 - inet line shows ip and prefix , broadcast ,scope ,

 - inet6 shows info about ipv6

 ip -s link show eth0 shows info

troubleshooting

 ip route show route info

 ping -c3 ip

 tracerout tracepath

 troubleshooting ports an services

 netstat ; ss

 -t TCP sockets

 -u UDP sockets

 -l only listening ports

 -p the process using the port

 -a all listening and established sockets -n numbers instead names for interfaces and ports

 configuring net with cmd nmcli

 networkmanager is a daemon that control and monitor network settings

 /etc/sysconfig/network-scripts/ config files after changes ,reload

 viewing network information

 nmcli con show &lt;interface&gt;

 nmcli dev status

 creating a network connection

 dhcp nmcli con add con-name "default" type ethernet ifname eth0

 static nmcli con add con-name "static" ifname eth0 autoconnect no type ethernet ip4 172.25.2.10 gw4 172.25.2.254

 nmcli con up "static"

if the static connection is lost , the default connection will atempt to autoconnect

to avoid this use, nmcli dev disconnect devicename

 help cmd nmcli con add help

 modifying network interfaces with nmcli

 nmcli con mod "static" connection.autoconnect no

 nmcli con mod "static" ipv4.dns 172.25.2.254 set DNS

 nmcli con mod "static" +ipv4.dns 8.8.8.8 set another DNS

nmcli con mod "static" ipv4.addresses "172.25.2.10/24 172.25.2.254" replaces ip an gatewway

nmcli con mod "static" +ipv4.addresses "10.10.10.10/16" add a ip without gateway

 more cmd

 nmcli dev disconnect devicename

 nmcli net off

 nmcli con del id-name

 editing files configuration

 interface configuration are in /etc/sysconfig/network-scripts/ifcfg-ifname

 example of change cmd echo "IPADDR1=10.0.2.2 &gt;&gt;/etc/sysconfig/network-scripts/ifcfg-eth0

 after changes must reload de conf and restart the interface

 nmcli con reload

 nmcli con down "system-eth0"

 nmcli con up "system-eth0"

 configuring host names and name resolution

 hostname stored in /etc/hostname

 getent host hostname can be used to check the resolution

 hostnamectl set-hostname "desktop.example.com"

 hostnamectl status

 in /etc/resolv.conf store are the info about dns server up to 3

 nmcli con mod "static" ipv4.ignore-auto-dns yes

12 ARCHIVING AND COPYING FILES ACROSS THE SYSTEM\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

tar creates a long file wit a set of others files then it can be compress

 tar c creates

 v verbose

 x extract with p preserve permmissions

 f file

 t list the content

 selinux and ACL permissions are saved if use --xattrs

 tar compress

 example tar czf /etc/...tar.gz /etc

 z tar.gz fast

 j tar.bz

 J tar.xz best

 extract a tar compres

 tar xJf /etc /example.tar.gz

copying files between systems securely with scp

 scp copies from remote to local or local to remote, uses ssh protocol \[user@\]remote:/path

examples scp server2:/etc/passwd /etc/host /home/student

 scp /etc/passwd /etc/host server2:/home/student

 fulldir recursively -r scp -r root@server2:/var/log/tmp

transfer files remotely with sftp

to initiate session

 sftp student@server2

 sftp server2 to login with current id

 sftp promt, sftp&gt;

 example

 sftp&gt; mkdir hostbackup

 sftp&gt; cd hostbackup

 sftp&gt; put /etc/host

 sftp&gt; get /etc/yum.conf

 sftp&gt; exit

 pwd

 ls

 cd

 mkdir

 rmdir

 put

 get

 synchronizing files between systems securely with rsync

 other way copy files across systems

first copy is full then incremental

 rsync options rsync -av /var/log/ /tmp log/ indicates that only the content of log will be copied

 options -v verbose

 -n dry run whised to run before to asure not delete important files

 -a all of next block

 -r synchronize recursively the whole directory tree

 -l synchronize symbolic links

 -p preserve permission

 -t preserve timestamps

 -g preserve group ownership

 -o preseve owner of the file

 -D synchronize devices files

 -A preserve ACL permisions

 -X preserve selinux permissions

works as scp between systems

 rsync -av server2:/etc/passwd /etc/host /home/student

rsync -av /etc/passwd /etc/host server2:/home/student

software package management, rpm and yum

 rpm is from local

 yum is from inet

 packages are named combined name-version-release.architecture

 each rpm package has 3 parts

 - files installed by the package

 - info metadata package requirements, changelog summary ,description licensing

 - scripts ,may run when updated removed or installed or triggered when other package is updated removed or installed

can be digitally signed with GPG as all red hat products to allow the system verify the integrity of a package before

 installing them.

 updates and patches

kernel packages are designed to support multiple versions installed,

 the yum package manager

 rpm does not resolve dependencies ,

yum is a front-end aplication for rpm ,

yum seach in the repositories for packages and their dependencies

 /etc/yum.conf is the configuration file

 /eyc/yum.repo.d is directory for repository configuration files , it has minimun a repo id in square brackets and url with the package location

software updates, managing with yum

 yum repolist shows a repository list

 yum list installed shows list of installed packages

 yum grouplist shows installed group

 finding software with yum

 yum --help

 yum list search in the packages installed, admit file globbling

 example yum list 'http\*' == rpm –qa 'http\*'

 yum search keyword list packages by keyword found in the name and summary only

 yum search all keyword list packages by keyword found in the name, summary and description

 yum info package gives detailed information about a package

 yum provides /PATH display packages that match with the path suplied

 yum install package obtain and install the package

 yum update package update a package

 yum update uptades all

 yum update kernel updates kernel is designed to support versions

 yum remove package remove package and any package that requies the package removed

groups of software, installing and removing with yum

 yum group list list installed and available

 yum group list hidden list hidden groups installed

 yum group list ids list groups with id use the id to install or remove

 yum group info shows a list of mandatory, default, and optinal package names or groups id´s.

 package may have a mark in front of them \(=,+,-, no mark\)

 = package installed , was installed as part of the group

 + package is not installed , will be if the group is installed or updated

 - package is not installed , will not be if the group is installed or updated

 no mark package is installed but was not installed through the group

 example yum group info "Identity Management server"

 yum group install in rehl7 a group is installed only if was installed through yum group install

 yum group mark install GROUPNAME marks a group as installed and any mmissing package and their dependecies will be installed on the next update

 yum history shows transaction history

 yum history undo nº undo the nº of transaction

Enabling yum software repositories

 enabling red hat software repositories

 yum repolist all shows all repositories

 yum-config-manager --enabled relh7-server-debug-rpms enabled repository

 --disabled relh7-server-debug-rpms

 yum --enabledrepo=pattern temporary

 --disablerepo=pattern

 this change the parameter 'enabled' of file /etc/yum.repos.d/redhat.repo

yum-config-manager --add-repo="http://...." creates a configuration file in /etc/yum.repos.d

 this file may be customized and added a GPG key

 rpm configuration package for the repository

some repositories provides this configuration file and GPG key as part of a rpm that can be

downloaded and installed usin yum localinstall

rpm --import http://....RPM-GPG-key recomended install gpg before the package

yum install http:///.... .rpm

examinig RPM package files

 rpm is low-level tool that can get info about the content of package files and installed packages

 it get the info fron local database or the package files themselves

 rpm -q or --query \[select-options\] \[select-options\]

 rpm -q -a shows all installed packages

 rpm -q package similar yum list

 rpm -q -p package.rpm shows the package named package.rpm from local

 rpm -q -f filename shows what package provides filename ,similar to yum provides

 rpm -q -i shows package in ,similar to yum info

 rpm -q -l shows installation paths of installed packages

 rpm -q -l -p shows where the package will be installed

 rpm -q -c list the configuration files

 rpm -q \_d shows only documentation files

 rpm -q –scripts list shell script that may run after or before the package is installed or removed

 rpm -q --changelog list change info por the package

 wget http://...package...rpm download a package

 local package files, install with yum

 yum localinstall package33

 rpm -q package33

extracting files from rpm packages

 rpm2cpio package.rpm \| cpio -id "\*txt" extract all \*txt from the rpm package ,recreated tree

 directory from the relative path

14 ACCESSING LINUX FILES\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

storage management concepts

a file system is a organized structure of data-holding files and directories residing in a storage devices

like physical disk or partition

mounting - process of adding a new file system to a tree directory

mount point the directory where the file system is mounted

storage devices are represented by a specialfile type called block, ls -l \(bwrx--x-rx\)

is stored in /dev first scsi tapa/sata or usb hard drive detected is called /dev/sda ../dev/sdb

in virtual machines is /dev/xvd or /dev/vdx

 LVM logical volume management

lvm can agregate one or more block devices into a storage group called volume group.

one or more physical volume can suport one or various VG volume groups with one or more logical volume.

 logical volume is like a partition

 /dev/myvg/mylv this is a symbolic link to dev/dm-number number is sequential begining in 0

 another symbolic link for every logical volume is in the /dev/mapper directory with the name of

 /dev/mapper/myvg/mylv

 examinig file system

 df -h in mib ^2 both shows file system and mount points

 df -H in mb ^10 S.I.

 du -h and -H shows the disk usage

 du /root

 du -sh dir shows the total usage for a dir

 mounting and unmounting file systems

 mount \[what\]\[where\]

 what - the device file holding the file system, residing in /dev or the uuid

 cmd blkid shows all existin partition with a file system on them and the uuid of the file system

 where must exist before the mount

 example mount /dev/vdb1 /mnt/mydata

 mount uuid="5465..5454" /mnt/mydata both are the same

 unmount /mnt/mydata you can not stand in /mydata in order to unmount works

 lost /mydata to know what process or users are in mydata to be able the unmount

 mount point for media is /run/media/&lt;user&gt;/&lt;label&gt;

 making links between files

 hard links - every file has one hard link by default

 - has the same permissions and stats that file referenced

 - if in the same dir. must have a diferent name

 - hard link pointing to the same file conten must be on the same file system

 - ls .-l shows the namner of hard link for a file after the permisions rwx--x-rw 1

 - all hard link of a file has the same inode

 ln file filelink

 ln newfile.txt /tmp/newfile-hl2.txt

 even the original file gets deleted the content is still avaliable as long as at least one hard link exist

 soft link is like a pointer may be use to directories, has distint inode number

 locating files on the system

 locate -search in the locate database \(may update with uptadedb by root, and every day with crontab\)

 for file name and path , shows results if the user have permission

 -i for case-insensitive

 -n to limit the result

 find \[where\]\[options\]\[what\]

 find / -name "\*.txt"

 find / -size +10M

 find / -perm /004 / wildcard

 find / -type l –name “free\*” –exec rm –f {} \;

