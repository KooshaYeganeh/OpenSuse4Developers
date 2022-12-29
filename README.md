# OpenSuse4Developers
*Everything you need as a developer on OpenSuse Leap 15.3*


![OpenSuse](./images/opensuse.jpg)



## Zsh and oh-my-zsh 


```
sudo zypper -n install zsh
```

```
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

For the image to have zsh from the moment you start, add a line to the settings of the bashrc file

```
sudo vi ~/.bashrc
```

add **exec zsh** to end of Line and write and quit.


## Install VsCode
*1- It is true that Vim is the best text editor, but if the number of lines of your code increases and you need to open and edit many files (especially in web applications), vscode will help you.*




``` 
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
```



```
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
```


```
sudo zypper refresh
```


```
sudo zypper install code
```




## Install Docker

[Docker](./images/docker.png)

```
sudo zypper install -y docker
```
```
sudo systemctl start docker
```
```
sudo systemctl enable docker
```


## vundle
*These are my personal settings for the Vim editor and are set for programming with Python. In order for you to have your own settings, you must first install vundle and then install your settings and plugins.*

```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

```
    set nocompatible              " required
    filetype off                  " required

    " set the runtime path to include Vundle and initialize
    set rtp+=~/.vim/bundle/Vundle.vim
    call vundle#begin()
    "
    " alternatively, pass a path where Vundle should install plugins
    " call vundle#begin('~/some/path/here')
    "
    " let Vundle manage Vundle, required
    Plugin 'gmarik/Vundle.vim'
    Plugin 'vim-syntastic/syntastic'
    Plugin 'nvie/vim-flake8'
    Plugin 'vim-scripts/indentpython.vim'
    Plugin 'scrooloose/nerdtree'
    Plugin 'jistr/vim-nerdtree-tabs'
    Plugin 'Lokaltog/powerline', {'rtp': 'powerline/bindings/vim/'}
    Plugin 'chriskempson/base16-vim'
    Plugin 'wuelnerdotexe/vim-enfocado'
    " add all your plugins here (note older versions of Vundle
    " used Bundle instead of Plugin)
    "
    " ...
    "
    " All of your Plugins must be added before the following line
    call vundle#end()            " required
    filetype plugin indent on    " required

    set encoding=utf-8

    au BufNewFile,BufRead *.py
        \set tabstop=4
        \set softtabstop=4
        \set shiftwidth=4
        \set textwidth=79
        \set expandtab
        \set autoindent
        \set fileformat=unix


    au BufRead,BufNewFile *.py,*.pyw,*.c,*.h match BadWhitespace /\s\+$/
    highlight BadWhitespace ctermbg=red guibg=darkred

    let NERDTreeIgnore=['\.pyc$', '\~$'] "ignore files in NERDTree
    let python_highlight_all=1
    syntax on


    colorscheme atom-dark

    set number
    set showmatch
    set history=1000
    set undolevels=1000
    set wildignore=*.swp,*.bak,*.pyc
    set visualbell
    set noerrorbells




```


## git


```
sudo zypper install git
```

## MariaDB

```sudo rpm --import https://yum.mariadb.org/RPM-GPG-KEY-MariaDB```
```
sudo zypper --gpg-auto-import-keys refresh
```  
```
sudo zypper addrepo --gpgcheck --refresh https://yum.mariadb.org/10.7/opensuse/15/x86_64 mariadb
```
```
sudo zypper refresh
```  
```
sudo zypper install MariaDB-server MariaDB-client
```

**Note : To add the user and password in MariaDB's config file 
(so that you don't have to enter the user and password every time in your system) you musy do This :**

```
sudo vi /etc/my.cnf
```

We add these lines to the config File:

```
[client]
user=koosha
password=10203
```

## Nginx

[Nginx](https://1000logos.net/wp-content/uploads/2020/08/Nginx-Logo.png)


```
sudo zypper -n install nginx
```

**Note : The default path of static files in the Nginix web server is a 
little different from other Linuxes. In most Linuxes, it is in the `/var/www/nginx`
but in OpenSuse it is in the  `/srv/www/htdocs` path.**


## Apache

[Apache](https://www.apache.org/foundation/press/kit/asf_logo.png)

```
sudo zypper -n install apache2
```


## Multimedia Codec

*After installing OpenSuse, we often see an error (h256 codec) that does not allow us to play videos.
To solve this problem, we can either install VLC or follow the steps below:*

```
sudo zypper addrepo -cfp 90 'https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Tumbleweed/' packman
```
```
sudo zypper addrepo -cfp 90 'https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Leap_$releasever/' packman
```
```
sudo zypper refresh
```

```
sudo zypper dist-upgrade --from packman --allow-vendor-change
```

## Install TLP for better power management

```
sudo zypper install tlp tlp-rdw
```
```
sudo systemctl enable tlp
```

## configure /tmp

*In OpenSuse, the contents of the /tmp directory are not deleted by default every boot,
if you want this directory to be deleted, we create a tmp.conf file in the /etc/tmpfiles.d path.*

```
vi /etc/tmpfiles.d/tmp.conf
```
*add this Line*
```
D /tmp 1777 root root -
```
or

*Or in GUI you can chnage setting from the path system_setttng -> privacy -> purge Trash and Temporary Files -> purge After *


## Security

If you are a programmer and you have a suse virtual server for your work
and you want to install Package tcp wrappers on your server, 
in this case Sousse works like Ubuntu and the name of Package tcp wrappers is different from other RPMs.


### ClamAV

[clamAV](https://logodix.com/logo/1583401.png)

```
sudo zypper install pcre-devel clamav clamav-database clamav-nodb clamz
```

**Updating virus database signatures**

```
sudo freshclam
```

> ٔImportant Note : If an error occurs while updating the signatures, you can download the database separately and place it in your specified path.

```
wget  https://database.clamav.net/daily.cvd
```

```
sudo mkdir /var/lib/clamav
```

```
mv daily.cvd /var/lib/clamav/daily.cvd
```

```
sudo systemctl start clamav-freshclam
```


### RootkitHunter

```
sudo zypper -n install rkhunter
```

### Malware Detect (Maldet)

```
sudo zypper install -n wget
```

```
cd /tmp/
```
```
wget http://www.rfxn.com/downloads/maldetect-current.tar.gz
```
```
tar xfz maldetect-current.tar.gz
```
```
cd maldetect-1.6.4
```
```
./install.sh
```

```
cd
```

**Configuring Maldet**

```
sudo vi /usr/local/maldetect/conf.maldet
```

**find the following lines and edit them to as below**

```
# To enable the email notification.
email_alert="1"

# Specify the email address on which you want to receive an email notification.
email_addr="user@domain.com"

# Enable the LMD signature autoupdate.
autoupdate_signatures="1"

# Enable the automatic updates of the LMD installation.
autoupdate_version="1"

# Enable the daily automatic scanning.
cron_daily_scan="1"

# Allows non-root users to perform scans.
scan_user_access="1"
 
# Move hits to quarantine & alert
quarantine_hits="1"

# Clean string based malware injections.
quarantine_clean="0"

# Suspend user if malware found. 
quarantine_suspend_user="1"

# Minimum userid value that be suspended
quarantine_suspend_user_minuid="500"

# Enable Email Alerting
email_alert="1"

# Email Address in which you want to receive scan reports
email_addr="you@domain.com"

# Use with ClamAV
scan_clamscan="1"

# Enable scanning for root-owned files. Set 1 to disable.
scan_ignore_root="0"
```

**Updating Maldet**
*First run the following command to create the correct paths for the logged-in user; you may have issues updating without doing this.*

``` 
sudo /usr/local/sbin/maldet --mkpubpaths
```

**To update the Maldet virus definitions database, execute the following command:**

```
maldet -u
```





### lynis

> Lynis is a battle-tested security tool for systems running Linux, macOS, or Unix-based operating system. It performs an extensive health scan of your systems to support system hardening and compliance testing

```
sudo zypper -n install lynis
```


### fail2ban

> Fail2ban is an intrusion prevention software framework. Written in the Python programming language, it is designed to prevent against brute-force attacks. It is able to run on POSIX systems that have an interface to a packet-control system or firewall installed locally, such as iptables or TCP Wrapper

```
sudo zypper -n install fail2ban
```


### Vim 

> Vim is a free and open-source, screen-based text editor program

```
sudo zypper -n install vim
```
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

### Git

> Git is free and open source software for distributed version control: tracking changes in any set of files, usually used for coordinating work among programmers collaboratively developing source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows

```
sudo zypper -n install git
```



### TCP wrappers

> TCP Wrapper is a host-based networking ACL system, used to filter network access to Internet Protocol servers on operating systems such as Linux or BSD. It allows host or subnetwork IP addresses, names and/or ident query replies, to be used as tokens on which to filter for access control purposes

```
sudo zypper -n install tcpd
```

### Ecryptfs-utils

> ecryptfs cryptographic filesystem (utilities)
eCryptfs is a POSIX-compliant enterprise-class stacked cryptographic filesystem for Linux. 


```
sudo zypper -n install ecryptfs-utils
```





### aide

> AIDE (Advanced Intrusion Detection Environment) is a small yet powerful, free open source intrusion detection tool, that uses predefined rules to check file and directory integrity in Unix-like operating systems such as Linux. It is an independent static binary for simplified client/server monitoring configurations.


```
sudo zypper -n install aide
```


### psad


> psad is a collection of three lightweight system daemons (two main daemons and one helper daemon) that run on Linux machines and analyze iptables log messages to detect port scans and other suspicious traffic. A typical deployment is to run psad on the iptables firewall where it has the fastest access to log data.

```
mkdir /tmp/psad
```

```
cd /tmp/psad
```

```
wget http://www.cipherdyne.org/psad/download/psad-2.2-1.x86_64.rpm
```

```
rpm -ivh psad-2.2-1.x86_64.rpm 
```

```
cd ..
```

```
rm -rf psad
```

**Edit the PSAD configuration file.**

```
sudo vi /etc/psad/psad.conf
```

**EMAIL_ADDRESSES** - change this to your email address.
**HOSTNAME** - this is set during install - but double check and change to a FQDN if needed.
**ENABLE_AUTO_IDS_EMAILS** - set this to Y if you would like to receive email notifications of intrusions that are detected.

**Add iptables LOG rules for both IPv4 and IPv6.**

```
iptables -A INPUT -j LOG
```
```
iptables -A FORWARD -j LOG
```
```
ip6tables -A INPUT -j LOG
```
```
ip6tables -A FORWARD -j LOG
```

**Reload and update PSAD.**

```
psad -R
```
```
psad --sig-update
```
```
psad -H
```

Note : To check the status of PSAD, open a Terminal Window and enter :

```
psad --Status
```

### sshfs

> SSHFS itself is a file system in user space (FUSE) that uses the SSH File Transfer Protocol (SFTP) to mount a remote file system. The sshfs command is a client tool for using SSHFS to mount a remote file system from another server locally on your machine.


```
sudo zypper -n install sshfs
```

### MySQL Tuner

> If you have a MariaDB database on your server, I suggest you use this script to diagnose configuration problems and increase stability.


MainLink : https://github.com/major/MySQLTuner-perl
Download Link : https://github.com/major/MySQLTuner-perl/archive/refs/heads/master.zip



### DDOS Deflate

> DoS Deflate is a lightweight bash shell script designed to assist in the process of blocking a denial of service attack. It utilizes the command below to create a list of IP addresses connected to the server, along with their total number of connections.


```
wget http://www.inetbase.com/scripts/ddos/install.sh
```

```
chmod 0700 install.sh
```

```
./install.sh
```



### Monitoring

[munin](https://munin-monitoring.org/assets/img/screenshot.png)

> Munin is a networked resource monitoring tool that can help analyze resource trends and "what just happened to kill our performance?" problems. It is designed to be very plug and play. A default installation provides a lot of graphs with almost no work

**Munin**

```
sudo zypper install munin
```



















