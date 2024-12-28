# `linux`

- [Conferming Sudo Privelege](#conferming-sudo-privelege-)
- [Username](#username-)
- [Sets a Password for Any User](#sets-a-password-for-any-user-)
- [Navigate Dirs (Returns to Home)](#navigate-dirsreturns-to-home-)
- [History Show Command History](#history-show-command-history-)
- [Man, Help & TLDR](#man-help--tldr-)
- [Linux Hierarchy](#linux-hierarchy-)
- [LS](#ls-)
- [Touch Create](#touch-create-)
- [CP Copy](#cp-copy-)
- [Mkdir Make Directory](#mkdir-make-directory-)
- [RM Remove](#rm-remove-)
- [LN Links](#ln-links-)
- [Show File Size](#show-file-size-)
- [Find](#find-)
- [Which/Locate](#whichlocate-)
- [Tar](#tar-)
- [Show Storage Devices List](#show-storage-devices-list-)
- [VIM](#vim-)
- [Show File Contents](#show-file-contents-)
- [Cut -d (Delimiter ":,|") -f (Field Column Number)](#cut--ddelimeter---ffield-column-number-)
- [Grep Keyword File (2>/dev/null : Ignore Errors)](#grep-keyword-file-2devnull--ignore-errors-)
- [Regex (Always Between SQ 'Regex') Grep](#regex-always-betwen-sq-regex-grep-)
- [TR Translate](#tr-translate-)
- [AWK](#awk)
- [SED](#sed)
- [Change User](#change-user-)
- [Sudo Visudo, Config Sudoers Privileges](#sudo-visudo-config-sudoers-priveliges-)
- [Nmap, Arp-Scan & Bettercap](#nmap-arp-scan--bettercap)
- [Linux Structure](#linux-structure-)
- [Redirection](#redirection-)
- [Pipe | Tee](#pipe--tee-)
- [Bash](#bash-)
- [Env Environment](#env-environment-)
- [Variables](#variables-)
- [Alias/Unalias](#aliasunalias-)
- [Ctrl+Key](#crtlkey-)
- [Bash Startup Files](#bash-startup-files-)
- [Users/Groups](#usersgroups-)
- [Session Management](#session-management-)
- [Permissions](#permissions-)
- [Diff](#diff-)
- [Partitions, Mount/Unmount, Fdisk (MBR), Gdisk (GPT)](#partitions-mountummount-fdiskmbr-gdiskgpt-gdisk-for-bigger-disks-)
- [Networking](#networking-)
- [Netstat](#netstat-)
- [Systemd](#systemd-)
- [RPM Apt-Cache](#rpm-apt-cache-)
- [UFW Firewall](#ufw-firewall-)
- [SSH](#ssh-)
- [Managing Time](#managing-time-)
- [Process Management](#process-management-)
- [Task/Job Scheduling](#taskjob-scheduling-)
- [Log Files](#log-files-)

## `conferming sudo privelege` :

        sudo ls /root

## `username` :

        whoami

## `sets a password for any user` :

        passwd user

## `navigate dirs(returns to Home)` :

        sudo ls /root

## `history show command history` :

        history -c clear
        history -d delete specific line
        history -w update history file
        (history) crtl-r search command (repress to g back)
        (history) !number repeat command based on number
        (history) ls -l .bash_history (history file in the sys)

## `man ,help & tldr` :

        man manuel for commands ("q" to quit, "/" to search, "n" next occurence)
        man "section number" "command"
        man pages are summerized in mandb
        man -k "keyword" to search the mandb
        man (1) for enduser commands
        man (8) for adminstrator commands
        man (5) for config files     
        command --help
        tldr simple help

## `linux hierarchy` :

        (linux hier) bin|usr/bin => binary executables progs (sbin|usr/sbin sudo)
        (linux hier) lib|lib64 => libraries
        (linux hier) boot => contains linux kernel, grub .. (boot necessitys)
        (linux hier) dev => devices
        (linux hier) etc => config txt files
        (linux hier) media|mnt => mount a specific device
        (linux hier) sys => manages haedware
        (linux hier) usr => put ur scripts in usr/local/bin to make availble in the sys

## `ls` :

        ls -d, ls -R (like tree)
        ls a* (any thing after a even none) 
        ls a?* (any charecter "?" after "a") 
        ls a[mn]* (m or n)
        ls a[a-e]* (anything btw a and e )
        ls -lrt (show files in order of last modification)

## `touch create` :

        touch file{1..100}

## `cp copy` :

        cp /path/file /path/newfilename

## `mkdir make directory` :

        mkdir -p /data/{sales,account}

## `rm remove` :

        (danger) rm -rf / --no-preserve-root #remove entire sys

## `ln links` :

        ln #hardlink
        ln -s #subolic link

## `show file size` :

        du -sh file|dir
        du -sh . (show current folder size)
        du -sh * (show each file size in the current folder)

## `find` :

        (find) -name, -user, -size (+2G,M,k), -type(d,f), -path
        find / -user "hamdi" -exec cp {} (all found files to) /path \; (closing)
        (find) command line parsing ;(separates commands), \;(end of exec)
        find /etc/ -type f | xargs grep "127.0.0.1" 2>/dev/null (find evry file that contains "127.0.0.1" inside)
        find /etc -exec grep -l hamdi {} \; (same but containing hamdi) -exec cp {} /path \; (possible to add commands)
        find /etc/ -name "*.conf" -printf "%s, %p\n" | sort -rn (s:siz, p:path)
        find path -name "file" -not -path "execludedpath/*" (ignore path "*": all dirs under this path )
        find path -perm /444(u,g "or" o may have perm) ,-444(u,g "and" o must have perm) ,444 (exactly)

## `which/locate` :

        sudo updatedb
        which "package/command" (show its location)

## `tar` :

        sudo tar cvf name.tar /path (compress)
        sudo tar xvf name.tar /path (extract -C to change output path)
        sudo tar tvf name.tar /path (list content)
        (tar) copression meth gzip -z, bzip2 -j, xzip -J => compression

## `show storage devices list` :

        lsblk (best) blockdevices
        mount mounts(usb)
        df -h mounts+diskspace 
        findmnt

## `vim` :

        (vim) i or o insert mode
        (vim) Esc return to command mode :
        (vim) :wq! write ,quit and dont complain
        (vim) u undo last change (crtl+r to reedo)
        (vim) dd delete current line
        (vim) :%s/old/newg ("g"global) replces all occurence of old with new
        (vim) v visual mode
        (vim) /sometxt search sometxt
        (vim) y copy current selection
        (vim) gg move to top
        (vim) G  move to end
        (vim) w next word
        (vim) b previous word
        (vim) ^ start of the line
        (vim) $ end of the line
        (vim) dw delete current word
        (vim) O|o open line above|after cursor pos
        (vim) :se number show line num
        (vim) r replace character

## `show file contents` :

        cat -b, -n(nuber lines not empty) tac (cat reversed)
        more/less (less > more) tail/head

## `cut -d(delimeter ":,|") -f(field column number)` :

        cut -d : -f3 /etc/passwd | sort -n (numeric sort)

## `grep keyword file: (2>/dev/null : ignore errors)` :

        grep -i ignore case
        grep -v all line that dont conatain the pattern
        grep -A5, B5, C5(A5+B5) : first line with occurence +/- 5 lines
        grep -R recurseve search

## `regex (always betwen sq 'regex') grep` :

        grep '^hamdi' begenning of the line
        grep 'hamdi$' end of the line
        grep '\bhamdi\b' word ('\b....\b' 4char word)
        grep 'bx*t' x zero or more times (bxxxt,bxt,bt)
        grep 'box\{n\}t' exactly n times of x
        grep -E 'bx+t' one or more
        grep -E 'bx?t' zero or one time
        grep -E '(svm|vmx)' /proc/cpuinfo serach either svm or vmx (check virtualisation on cpu)

## `tr translate` :

        tr [:lower:] [:upper:]
        tr [a-z] [A-Z]

## `awk`:

        awk -F : '{ print $1 }' /etc/passwd (like cut -d : -f1 /etc/passwd)
        awk 'length ($0) > 40 ' /etc/passwd lines len > 40
        awk -F : '/hamdi/ {print $3}' /etc/passwd user id

## `sed`:

        sed -n 5p /etc/passwd show 5th line
        sed -i s/anna/hamdi/g text (s:substitute anna with hamdi g:global)
        sed -i  -e '2d' text (-e: edit ,delete 2end line)
        for i in *txt ;do sed -i 's/hello/bye/g' $i ; done

## `change user` :

        su - "user name" (switch user)
        sudo -i (opens a sudo prevelidged shell)

## `sudo visudo ,config sudoers priveliges` : 

        (visudo) user ALL=/usr/bin/passwd 
        /usr/bin/passwd root (gives user passwd capabilities)
        (visudo) Defaults timestamp_type=global,timestamp_timeout=240 (change time needed to reenter password)
                                                                       
## `nmap ,arp-scan & bettercap`:

        - find devices on local net : nmap, arp-scan
                sudo nmap (all info) 192.168.1.0/24 (-sn ip/mac/up|down)
                sudo arp-scan --interface=wlo1  --localnet

        - sudo bettercap :
                (bettercap) net.probe on ,net.show (scan and show devices on local net)
                (bettercap) set arp.spoof.fullduplex true
                (bettercap) set arp.spoof.targets 192.168.1.20 ,arp.spoof on ,net.sniff on
                (bettercap) set dns.spoof.domains facebook.com ,dns.spoof on

## `linux structure` :

        software => kernel => hardware
        command => shell =>  glibe  => kernel                     
                              /\
                              ||                                         
                services => systemd (manger of evrything)               

## `redirection` :

        (redirection) <  input
        (redirection) >  output override
        (redirection) >> output append
        (redirection) 2>/dev/null redirect errors
        (redirection) &>/file put output+errors in

## `pipe | tee` :

        (pipe) ps aux | tee psfile.txt | grep ssh (tee will put the output of ps in psfile.txt)

## `bash` :

        bash creates a subshell under current shell

## `env environment` :

        env (shows environment vars)
        /etc/environment

## `variables` :

        (vars) system (default linux) ,environment (application use)
        (vars) varname = value (define var "only known to the current shell")
        (vars) command(echo) $varname (read var value)
        (vars) export varname=value (no $ sign ,define var "all shells")
        (vars) $PATH var (executable commands paths "add file.sh to one of $PATH paths to make it accessible in shell", "usr/local/bin all users can use it")

## `alias/unalias` :

        alias name="command" (clear="cls")
        unalias name

## `crtl+key` :

        crtl+l clear
        crtl+u clear line
        crtl+a line begenning
        crtl+e line end
        crtl+c stop
        crtl+d exit
        crtl+z temporarily stop a job

## `bash startup files` :

        (bash startfiles) /etc/environment
        (bash startfiles) /etc/profile.d (executed while user login "scripts will be executed when added in this dir")
        (bash startfiles) ~/.bash_profile|.bash_logout (user specific login|logout)
        (bash startfiles) /etc/bashrc (every time subshell is excuted "~/.bashrc user specific")
        (bash startfiles) sudo nano /etc/profile.d/history.sh (adding history.sh to change $HIST properties : "export HISTSIZE=2500 \n export HISTFILESIZE=5000")
        (bash startfiles) login/out or source /etc/profile.d/history.sh to save changes
        (bash startfiles) find a bashrc file under /etc add a script "alias ipc='ip a'" will be saved for all users

## `users/groups` :

        (users/groups) "/etc/passwd" | "/etc/group" are where "user" | "group" info is stored
        (users/groups) id show current user id "uid" ,current group owner "gid" and groups like sudo or wheel
        (users/groups) useradd ("-m" ensure creation of home dir, "-D" default user settings "/etc/login.defs")
        (users/groups) groupadd ("usermod -aG group user" add a user to a group)
        (users/groups) vipw edit /etc/shadow ("edit user info"), vigr edit /etc/group
        (users/groups) chage user ,echo "user:password" | sudo chpasswd (deb) ,echo password | sudo passwd (red)
        (users/groups) groupdel/userdel groupmod
        (users/groups) useradd "user" -G "group1","group2",... (creates a user and enroll him multiple groups if user exists use usermod -aG to append "not create new sec groups")

## `session management` :

        (session) who/w current logins
        (session) loginctl (list-sessions ,show-session "id" ,show-user "user")
        (session) loginctl terminate-session "session-id"

## `permissions` :

        (permissions)           |   file   |   dir
        (permissions) read (4)  |   read   |   list (ls)  (u need to have r per to read a file "dir r per dont intervene")
        (permissions) write(2)  |   modify |   add/delete (u need to have w per in a dir to delete a file)
        (permissions) exec (1)  |   run    |   cd
        (permissions) chmod change permessions of a file/dir
        (permissions) chown change usr ownership "chown user file/dir" ,"chown user:group file/dir (user & group are owners of file/dir)"
        (permissions) chgrp change group ownership
        (permissions) sudo chmod "u/g" + s file/dir (set user id/set group id "4000")
        (permissions) chmod +t (stiky bit "dir permession" only modify if u own the file/dir "3000")
        (permissions) /etc/skel/.bashrc (make default changes)

## `diff` :

        diff file.txt file.txt (show differences </> " '>' the differnce exist on the right file ")

## `partitions ,mount|ummount ,fdisk(MBR) ,gdisk(GPT) "gdisk for bigger disks"` :

        (partitions) create partition => create system file => mount
        (partitions) lsblk (monitor avaible disks)
        (partitions) fdisk|gdisk /dev/"disk or partition"
        (partitions) mkfs.ext4|xfs /dev/"disk or partition"(create file systems)
        (partitions mount) mount|umount /dev/"disk or partition" /"dir"
        (partitions mount) lsof (find wich processes are keeping the divice busy)
        (partitions per mount) /etc/fstab (add permenet mounts "mount -a chek for errors")

## `networking` :

        (net ipv6) ::1/128 localhost ,::/ default route ,2000::/3 global unicast @s ,fd00::/8 unique local @s "private like 192.168.. "
        (net ipv6) ff00::/8 ,fe80::/64 link-local @s "automaticly assined base on the mac@"
        (net ipv6) dhcpv6 : multicast is sent to ff02::1:2 (all dhcp multicast group) port 547/udp ,dhcp sends back a packet to 546/udp
        (net ipv6) slaac  : multicast is sent to ff02::2 (all routers multicast group) ,router sends back an ip@ "allows the host to learn the net prefix" (radvd)
        (net) ip a ,ifconfig (returns net config)
        (net) ip a(address) add/del dev(nic) "ens33|wlo1" ip@/mask"24"
        (net) ip l(link) set (nic)"ens33|wlo1" up|down
        (net) ip r(route) show (show routing table) ,ip r add default via ip@ "configure default gateway"
        (net) name resolution "ip@ => name" hostnamectl hostname "name" ,/etc/host (edit etc hosts) ,/etc/resolv.conf (edit dns hosts) ,/etc/nsswitch.conf (order of host name res)
        (net) ping -c(count) 4 ip@
        (net) ss -tunap(protocols t:tcp ,u:udp ,a:all)
        (net) dig "dns name(google.com)" (reveals its ip@)
        (net) nmtui (configure networks)

## `netstat` :

        (netstat) apt install net-tools
        (netstat) netstat -lntp (displays detailed information about listening network services)
        
## `systemd` :

        (systemd) "default"|"custom" units "/user/lib/systemd/system"|"/etc/systemd/system"
        (systemd systemctl) systemctl -t help "avaible utilitys"
        (systemd systemctl) systemctl list-unit-files ,list-units ,[status,start|stop,enable|desable(automatic on sys boot),restart] "service"
        (systemd systemctl) systemctl cat "service" "show current conf" ,systemctl show (show avaible conf) ,systemctl status "service"
        (systemd systemctl) systemctl edit "service" ,systemctl daemon-reload "update all conf"
        (systemd systemctl) killall "service" ,kill -9 "service process id"
        (systemd systemctl) restart=on-failure (restart the service on failure)
        (systemd systemctl) system targets ,systemctl list-dependencies "target" ,systemctl list-units -t target (emergency ,rescue ,multi-user ,graphical : main 4 targets)
        (systemd systemctl) systemctl get-default ,systemctl set-default "target(multi-usertarget)" ,systemctl isolate "target(emergency.target)" (change from graphical to emergency)
        (systemd systemctl) in grub press e ,under linux change rhgbquiet to systemd.unit=emergency.target (change from graphical to emergency)
        (systemd systemctl) systemctl start default.target
        (systemd service wsl) service start "service" ,service status "service"

## `rpm apt-cache` :

        rpm -qf "file" (which package a file is from)
        rpm -ql "package" queries database to list package contents
        rpm -qpc "package" list confid files in a package file "package.rpm"
        rpm -qp --scripts "package" show package scripts

## `ufw firewall` :

        (ufw) configure firewall settings
        (ufw) ufw allow|deny proto tcp from 192.168.0.4 to any(ip@ on current host) port 22
        (ufw) ufw deny|allow proto udp from any to any port 8412:8500 (port range 8412=>8500)

## `ssh` :

        (ssh) ssh user|ip@ , scp file user|ip@:path (copy files securly)
        (ssh) /etc/ssh/sshd_config :
                (ssh) Port (define a port),PermintRootLogin (disable root login for safety),AllowUsers (define allowed users) ,PasswordAthentication
        (ssh) firewall-cmd --add-service ssh --permenet ;firewall-cmd --reload ,firewall-cmd --add-port 2022/tcp --permenet ;firewall-cmd --reload (red hat)
        (ssh) ufw allow OpenSSH ,ufw allow 2022/tcp (debian)
        (ssh) ssh-keygen ,ssh-copy-id "user@ip" ,ssh-agent /bin/bash ,ssh-add
        

## `managing time` :

        (time) touch file-$(date +%d-%B-%Y).tar (put the date in the file name)
        (time) hwclock (hardware clock) ,timedatectl
        (time) timedatectl set-ntp ,timedatectl timesync-status ,chronyc sources ,chronyc tracking

## `process management` :

        (process) jobs (view current jobs) ,bg (run jobs in the background "same as job &") ,fg "job number" (move a job to the foreground)
        (process) top (1:show cpus ,f:edit shown info ,z:color ,w:saves config ,r:renice ,k:kill process)
        (process) ps aux (info about processes) ,ps fax (show parent-child process relation) ,ps -ef
        (process) ps -e -o pid,args --forest
        (process) ps aux --sort pmem
        (process) nice -n -10 "job/process" (nice value varies from -20(best) to 19(worst) "set the importance")
        (process) kill "pid" ,killall "name" ,kill SIGTERM "stop process" ,kill SIGKILL "force off a process" ,man 7 signal (15 ,9)
        (process) dd if=/dev/zero of=/dev/null

## `task/job scheduling` :

        (task/job scheduling) /etc/crontab ,crontab -e (edit cron jobs for current user)
        (task/job scheduling) Example of job definition: ("*" for evry min/h/d/m/y)
        (task/job scheduling) # .---------------- minute (0 - 59)
        (task/job scheduling) # |  .------------- hour (0 - 23)
        (task/job scheduling) # |  |  .---------- day of month (1 - 31)
        (task/job scheduling) # |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
        (task/job scheduling) # |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
        (task/job scheduling) # |  |  |  |  |
        (task/job scheduling) # *  *  *  *  * user-name command to be executed
        (task/job scheduling) journalctl (systemd journal)
        (task/job scheduling) systemctl list-units -t timer (show systemd timers) ,systemctl list-unit-files -t timer "fstrim*"
        (task/job scheduling) at "time" => command ,atq (show shceduled jobs) ,at rm (remove job) "at is used only in the current terminal session"

## `log files` :

        (log files) journalctl ,journalctl -f ,/etc/systemd/journald.conf
        (log files) logger (write to the log system)
        (log files) /etc/rsyslog.conf




























