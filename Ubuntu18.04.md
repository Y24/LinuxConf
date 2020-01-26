# The Configuration of Ubuntu 18.04 LTS

## APT source

sudo gedit /etc/apt/sources.list

> deb <https://mirrors.aliyun.com/ubuntu/> bionic main restricted universe multiverse</br>
deb <https://mirrors.aliyun.com/ubuntu/> bionic-security main restricted universe multiverse</br>
deb <https://mirrors.aliyun.com/ubuntu/> bionic-updates main restricted universe multiverse</br>
deb <https://mirrors.aliyun.com/ubuntu/> bionic-proposed main restricted universe multiverse</br>
deb <https://mirrors.aliyun.com/ubuntu/> bionic-backports main restricted universe multiverse</br>

## Appearance/Theme

### Applications

  [`Arc-Dark`](https://github.com/horst3180/arc-theme)

#### Required

    - autoconf
    - automake
    - pkg-config
    - libgtk-3-dev
    - git
    - gnome-themes-standard
    - gtk2-engines-murrine

#### Steps

    1. git clone https://github.com/horst3180/arc-theme --depth 1 && cd arc-theme
    2. ./autogen.sh --prefix=/usr
    3. sudo make install

### Cursor

  [`Capitaine-cursors`](https://github.com/keeferrourke/capitaine-cursors)

#### Steps

    1. git clone https://github.com/keeferrourke/capitaine-cursors
    2. cd capitaine-cursors
    3. sudo cp -pr dist/ /usr/share/icons/capitaine-cursors

### Icons

  [`Arc`](https://github.com/horst3180/arc-icon-theme)

#### Required

  `Tela-manjaro`

    1. git clone https://github.com/vinceliuice/Tela-icon-theme
    2. cd Tela-icon-theme/
    3. ./install.sh manjaro

#### Steps

    1. git clone https://github.com/horst3180/arc-icon-theme --depth 1 && cd arc-icon-theme
    2. ./autogen.sh --prefix=/usr
    3. sudo make install
    4. sudo gedit /usr/share/icons/Arc/index.theme
       Inherits=Tela-manjaro,Adwaita,gnome,hicolor

### Shell

  See **Applications**.

### Background

  diy</br>
  Tips: </br>wget <https://images.wallpapersden.com/image/download/abstract-4k_67950_1920x1080.jpg>

### plymouth

Boot and shutdown animation.

#### Steps

    1. sudo cp -r ubuntu-touch /usr/share/plymouth/themes
    2. sudo cp default.plymouth default.plymouth.bak
    3. sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/ubuntu-touch/ubuntu-touch.plymouth 100
    4. sudo update-alternatives --config default.plymouth
    5. sudo -s
    6. echo FRAMEBUFFER=y >>/etc/initramfs-tools/conf.d/splash
    7. update-initramfs -u
    8. reboot

#### Config

    sudo gedit /usr/share/plymouth/themes/ubuntu-touch/ubuntu-touch.script

### Note

`ubuntu-touch` can be found in the dir `assets`.

### GDM

login page.

#### Steps

    1. git clone <https://github.com/mfabijanic/gdm3theme-blur>
    2. cd gdm3theme-blur
    3. ./setup.sh -i

## zsh

### Steps

    1. sudo apt install zsh powerline fonts-powerline
    2. sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
    3. git clone <git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions>
    4. git clone <https://github.com/zsh-users/zsh-syntax-highlighting.git> ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    5. gedit ~/.zshrc 
      - use random theme
      - add to plugins:   
        colored-man-pages z zsh-autosuggestions extract web-search zsh-syntax-highlighting

## Gnome shell extension

### Required

- `sudo apt install chrome-gnome-shell gnome-tweaks`

### Content

- Activities configurator
- Battery percentage
- Caffeine
- Coverflow alt-tab
- Dash to dock
- Dash to panel
- Openweather
- Remove accessibility
- Status area horizontal spacing
- User themes

## Software

- vscode
- idea
- jdk
- android studio
- sogoupinyin
- Google Chrome
- WPS office
- blender
- vlc media player
- more

## Dev Kit

### Flutter

Add the following content to ~/.zshrc

> export PATH="$PATH:Path/to/flutter/bin"</br>
export PUB_HOSTED_URL="<https://mirrors.tuna.tsinghua.edu.cn/dart-pub/"></br>
export FLUTTER_STORAGE_BASE_URL="<https://mirrors.tuna.tsinghua.edu.cn/flutter">

### Dart SDK

Dart
> <https://storage.googleapis.com/dart-archive/channels/stable/release/2.5.2/sdk/dartsdk-linux-x64-release.zip>

## vscode extension

- Arc+ color theme
- Material Icon Theme
- Python
- markdownlint
- IntelliJ IDEA Keybindings
- C/C++
- Flutter
- Bracket Pair Colorizer 2

## SSH&GitHub

### SSH

    1. ssh-keygen -t rsa -b 4096
    2. ssh-copy-id $username@$hostname

### Github

    1. ssh-keygen -t rsa -b 4096 -C "email address"
    2. add to github.
    3. git remote set-url origin git@github.com:Username/Project.git

### Note

On most systems the default private keys (~/.ssh/id_rsa and ~/.ssh/identity) are automatically added to the SSH authentication agent. You shouldn't need to run ssh-add path/to/key unless you override the file name when you generate a key.

## Latex for vscode

package: latexmk texlive

### Chinese support

    1. package: latex-cjk-all texlive-xetex texlive-latex-extra
    2. tlmgr install ctex
    3. vscode settings.json

```
"latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "latexmk",
            "tools": [
                "latexmk"
            ]
        },
        {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        }
    ],
    "latex-workshop.latex.tools": [{
        "name": "latexmk",
        "command": "latexmk",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-pdf",
            "%DOC%"
        ]
    }, {
        "name": "xelatex",
        "command": "xelatex",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
        ]
    }, {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
        ]
    }, {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
            "%DOCFILE%"
        ]
    }],
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk"
    ],
    "latex-workshop.latex.autoBuild.run": "never"
```

## Aria2

1. create dir

    `sudo mkdir /etc/aria2`

2. create session file

    `sudo touch /etc/aria2/aria2.session`

    `sudo chmod 777 /etc/aria2/aria2.session`
3. create config file.

    `sudo gedit /etc/aria2/aria2.conf`

> dir=/home/y24/Downloads</br>
disable-ipv6=true</br>
enable-rpc=true</br>
rpc-allow-origin-all=true</br>
rpc-listen-all=true</br>
\#rpc-listen-port=6800</br>
continue=true</br>
input-file=/etc/aria2/aria2.session</br>
save-session=/etc/aria2/aria2.session</br>
max-concurrent-downloads=20</br>
save-session-interval=120</br>
connect-timeout=120</br>
\#lowest-speed-limit=10K</br>
max-connection-per-server=10</br>
\#max-file-not-found=2</br>
min-split-size=10M</br>
split=10</br>
check-certificate=false</br>
\#http-no-cache=true</br>

`sudo aria2c --conf-path=/etc/aria2/aria2.conf -D`

## etc

### vscode c/c++ format error

    miss shared lib: libncurses5
