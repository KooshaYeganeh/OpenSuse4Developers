# OpenSuse4Developers
Everything you need as a developer on OpenSuse Leap 15.3


![OpenSuse](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fi.redd.it%2Fi9arhctym0y41.jpg&f=1&nofb=1&ipt=aa5b5bb4e4c31aed02e822d4a664e6bbe1c7490319d1ea1aa6d2be2bb04112fe&ipo=images)

## Install VsCode
*1- It is true that Vim is the best text editor, but if the number of lines of your code increases and you need to open and edit many files (especially in web applications), vscode will help you.*

1- `sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc`

2- `sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'`

3- `sudo zypper refresh`

4- `sudo zypper install code`



## Install Docker


1- `sudo zypper install -y docker`
2- `sudo systemctl start docker`
3- `sudo systemctl enable docker`


## vundle
*These are my personal settings for the Vim editor and are set for programming with Python. In order for you to have your own settings, you must first install vundle and then install your settings and plugins.*

`git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

{
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




}


## git


sudo zypper install git


## MariaDB

`sudo rpm --import https://yum.mariadb.org/RPM-GPG-KEY-MariaDB`
`sudo zypper --gpg-auto-import-keys refresh`
`sudo zypper addrepo --gpgcheck --refresh https://yum.mariadb.org/10.7/opensuse/15/x86_64 mariadb`

`sudo zypper refresh`
sudo zypper install MariaDB-server MariaDB-client


## Nginx

`sudo zypper install nginx`


## Multimedia Codec

*After installing OpenSuse, we often see an error (h256 codec) that does not allow us to play videos.
To solve this problem, we can either install VLC or follow the steps below:*

`sudo zypper addrepo -cfp 90 'https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Tumbleweed/' packman`

`sudo zypper addrepo -cfp 90 'https://ftp.gwdg.de/pub/linux/misc/packman/suse/openSUSE_Leap_$releasever/' packman`

`sudo zypper refresh`

`sudo zypper dist-upgrade --from packman --allow-vendor-change`
