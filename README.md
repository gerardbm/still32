# Still32: dotfiles for Devuan 5 in 32 bits

**Modern dotfiles for those machines that refuse to die. Still 32 bits. Still SysVinit. With Devuan 5.**

This repository uses **stow** hierarchy: clone it into `$HOME` and use `stow --no-folding <package>` to create the symlinks automatically for each package. For more information about stow read its documentation: `stow(8)`.

The content of this repository is a mix between my regular [dotfiles](https://github.com/gerardbm/dotfiles.git) and my vim setup ([vimrc](https://github.com/gerardbm/vimrc.git)), adapted to be used under 32 bits systems and refined to remain fast, stable and minimalist.

Configuration files:

```
- Distro      : Devuan
- WM          : i3
- Menu        : rofi
- Shell       : zsh
- Terminal    : urxvt, xterm
- Multiplexer : tmux
- Font        : Terminess Powerline
- CVS         : git
- Editor      : vim, neovim
- Files       : vifm, ranger
- Finder      : fzf
- Youtube     : ytfzf
- IRC         : irssi
- Email       : mutt
- Music       : cmus
- Video       : mpv
- Images      : feh
- Reader      : mupdf, apvlv, zathura
- Browser     : w3m
- Interface   : surfraw
- Bittorrent  : transmission-cli
```

## Setup

### Devuan

**Add the user to the sudoers file**

1. Enter to the root mode: `su -` (then, root password)

2. Edit the file `/etc/sudoers`:

`sudo visudo -f /etc/sudoers`

3. Add this line after `ROOT ALL (ALL:ALL) ALL`:

`<user> ALL (ALL:ALL) ALL`

**Disable autologin on LXDE**:

1. Edit the following file:

`sudo nano /etc/lightdm/lightdm.conf`

2. Find the line `#autologin-user=`.

3. Uncomment the line and add the user:

`autologin-user=<user>`

### i3

Install the version 4.22 from the repositories:

`sudo apt-get install i3`

Make sure you have installed the following libraries, which are a requirement to run my setup properly:

- compton: compositor based on xcompmgr with some improvements.
- dunst: a customizable and lightweight notification-daemon.
- libnotify-bin: a program to send desktop notifications.
- lxappearance: customize look and feel (lxde-native).
- lxpolkit: authorization manager for the desktop.
- lxqt-openssh-askpass: handle password access.
- pulseaudio-utils: to run pulse audio controls from the keyboard.
- rofi: a window switcher, run dialog and dmenu replacement.
- rxvt-unicde-256color: VT102 emulator for the X window system.
- udiskie: automounter for removable media (flash drives).
- volumeicon-alsa: volume icon for the system tray.
- wicd: Wired and wireless network connection manager.
- xbacklight: adjust backlight brightness using RandR extension.
- xsel: command-line tool to manipulate the X selection.
- xsct: set screen color temperature.
- xcalib: tiny monitor calibration loader.

Optional:
- arandr: can be useful to generate xrandr \*.sh scripts.
- libfm-pref-apps and exo-preferred-applications: the name is self-descriptive.
- redshift: adjusts the color temperature of your screen according to your surroundings. This may help your eyes hurt less or reduce the risk for delayed sleep phase syndrome if you are working in front of the screen at night.

Useful tools: uuid, fbreader, simplescreenrecorder, translate-shell, trash-cli

### Zsh

Install the version 5.9 from the repositories:

`sudo apt-get install zsh`

Install [Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh) following the instructions from its page.

Via curl:

`sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

Via wget:

`sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`

Atomic theme must be downloaded from [Atomic repository](https://github.com/gerardbm/atomic).

Enable zsh-syntax-highlighting:

`git clone https://github.com/zsh-users/zsh-syntax-highlighting $HOME/.syntax`

<!-- Enable zsh-autosuggestions: -->

<!-- `git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions` -->

Symlink the zsh settings:

`cd $HOME/dotfiles && stow --no-folding zsh`

Change the current shell:

`$ chsh -s /usr/bin/zsh`

Log out and log in to see the new shell as default.

### URxvt

Install the version 9.30 from the repositories:

`sudo apt-get install rxvt-unicode`

Symlink the rxvt-unicode settings:

`cd $HOME/dotfiles && stow --no-folding X`

Cosmic color scheme is already included.

Install the scripts:

`cd $HOME/dotfiles && stow --no-folding urxvt`

To check for newer versions on Github:

- The script `resize-font`: https://github.com/simmel/urxvt-resize-font
- The script `url-select`: https://github.com/johntyree/urxvt-perls
- The script `clipboard`: https://github.com/pkkolos/urxvt-scripts
- The script `unichr`: https://emergent.unpythonic.net/

### Tmux

Install the version 3.3a from the repositories:

`sudo apt-get install tmux`

Then, install the package `urlview`:

`sudo apt-get install urlview`

Symlink the tmux settings:

`cd $HOME/dotfiles && stow --no-folding tmux`

### Git

Install the version 2.39.5 from the repositories:

`sudo apt-get install git`

Symlink the git settings:

`cd $HOME/dotfiles && stow --no-folding git`

### Powerline

Clone the [Powerline fonts repository](https://github.com/powerline/fonts):

`git clone https://github.com/powerline/fonts`

And install it:

`cd fonts && ./install.sh`.

**Fontconfig**

«In some distributions (e.g. Debian), Terminess Powerline is ignored by default and must be explicitly allowed. A fontconfig file is provided which enables it. Copy this file from the fontconfig directory to your home folder under ~/.config/fontconfig/conf.d (create it if it doesn't exist) and re-run `fc-cache -vf`». Paragraph extracted from [Powerline](https://github.com/powerline/fonts).

### FontAwesome

Install it from the repositories:

`sudo apt-get install fonts-font-awesome`

(Not using anymore, though).

### Vim

Install the version 9.0 from the repositories (the stable version is enough):

`sudo apt-get install vim vim-gtk3`

The package `vim-gtk3` adds the 'huge version' with a lot of features (+python3, +clipboard...), and the GTK3 GUI.

Install the plugins manager [vim-plug](https://github.com/junegunn/vim-plug); follow the instructions from its repository:

```sh
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
 ```

Install the plugins with the command:

`:PlugInstall`.

To make it compatible with the plugin `Shougo/deoplete.nvim`, it requires two plugins (`roxma/vim-hug-neovim-rpc` and `roxma/nvim-yarp`) that require neovim installed from pip3, so first install python3-pip and then install neovim from there:

`sudo apt-get install neovim`

This will install `pynvim`. If not, try:

`pip3 install pynvim`

Then from the Vim command line, execute:

`:pythonx import pynvim`

### Clang

Install clang from the repositories:

`sudo apt-get install clang libclang-dev`

The package `libclang-dev` is required on Devuan.

### Golang

Inistall golang from the repositories:

`sudo apt-get install golang`

Open Vim and run the following command:

`:GoInstallBinaries`

### Pylint

Note: check pyenv to install other Python versions.

Install pylint from pip3:

`pip3 install pylint`

### Vint

Install vint from pip3:

`pip3 install vim-vint`

### Shellcheck

Install shellcheck from the repositories:

`sudo apt-get install shellcheck`

### Chktex

Install chktex from the repositories:

`sudo apt-get install chktex`

### Nodejs, tern, jshint, csslint

Install node from the repositoies:

`sudo apt-get install nodejs npm`

Test the installation using:

```sh
node -v
npm version
```

Make a directory to install global npm modules:

`mkdir ~/.npm-global`

Configure npm to use the new directory path:

`npm config set prefix '~/.npm-global'`

Add the path to `~/.zshrc` file:

`export PATH=~/.npm-global/bin:$PATH`

Update the system variables:

`source ~/.zshrc`

Finally install the packages using npm:

```sh
npm install -g tern
npm install -g jshint
npm install -g csslint
```

### Pyenv

Install pyenv:

```sh
curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
```

Add pyenv to the path:

```sh
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zprofile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zprofile
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init --path)"' >> ~/.profile

echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

Install a Python version. For example:

```sh
pyenv install 3.8.0
```

Activate the Python version:

```sh
pyenv local 3.8.0
```

Then use `pip3.8` to install some Python tools: `youtube-dl`, `skyfield`, `pylint`, etc.

How to use again the system version:

```sh
pyenv local system
```

How to list all the available versions:

```sh
pyenv versions
```

### Ruby and Jekyll

Install the dependencies:

`sudo apt install git curl libssl-dev libreadline-dev zlib1g-dev autoconf bison build-essential libyaml-dev libreadline-dev libncurses5-dev libffi-dev libgdbm-dev`

Then install Rbenv:

`curl -sL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash -`

Add Rbenv to the PATH in `~/.zshrc`:

```sh
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(~/.rbenv/bin/rbenv init - zsh)"
```

Install the wanted Ruby version:

`rbenv install 2.6.4`

And make it global:

`rbenv global 2.6.4`

Finally install the last Jekyll version:

`gem install jekyll`

#### Update Ruby with

If the Ruby version is missing, upgrade ruby-build:

`cd /home/gerard/.rbenv/plugins/ruby-build && git pull && cd -`

Then install the newer version:

`rbenv install 3.2.0`

Then update Jekyll:

`gem install jekyll -v 4.3.3`

Some updates:

```
gem update --system
bundle update --bundler
```

### W3m

Install it from the repositories:

`sudo apt-get install w3m`

Symlink the w3m settings:

`cd $HOME/dotfiles && stow --no-folding w3m`

### Ranger

Install it from the repositories:

`sudo apt-get install ranger`

Symlink the ranger settings:

`cd $HOME/dotfiles && stow --no-folding ranger`

### Vifm

Install it from the repositories:

`sudo apt-get install vifm`

Symlink the vifm settings:

`cd $HOME/dotfiles && stow --no-folding vifm`

Install the atomic theme for vifm:

```sh
mkdir $HOME/.mutt
git clone https://github.com/gerardbm/atomic
cp atomic/vifm/atomic.vifm $HOME/.config/vifm/colors/
```

### FZF

Install it from the repositories:

`sudo apt-get install fzf`

Clone the Github repository to the `~/.fzf`.

`git clone https://github.com/junegunn/fzf.git ~/.fzf`

Change the branch:

`git checkout 0.47.0`

### Ytfzf

Install it from the repositories:

`sudo apt-get install ytfzf`

### Mutt

Install it from the repositories:

`sudo apt-get install mutt`

Copy the mutt settings (no symlink):

`cp $HOME/dotfiles/mutt/.muttrc $HOME/`

Install the atomic theme for mutt:

```sh
mkdir $HOME/.mutt
git clone https://github.com/gerardbm/atomic
cp atomic/mutt/atomic.muttrc $HOME/.mutt
```

### Cmus

Install it from the repositories:

`sudo apt-get install cmus`

Symlink the cmus settings:

`cd $HOME/dotfiles && stow --no-folding cmus`

Install the atomic theme for cmus:

```sh
git clone https://github.com/gerardbm/atomic
cp atomic/cmus/atomic.theme $HOME/.config/cmus
```

From cmus command line:

- Set the colorscheme: `:colorscheme atomic`
- Add the playlist: `:add $HOME/.config/cmus/playlist.pl`

### Irssi

Install it from the repositories:

`sudo apt-get install irssi`

Create the folder first and then copy (no symlink) the irssi settings:

`mkdir $HOME/.irssi && cp $HOME/dotfiles/irssi/.irssi/config $HOME/.irssi/`

Copy the script to install the plugins for the first time:

`cp $HOME/dotfiles/irssi/.irssi/config $HOME/.irssi/`

Run it:

`. ./iip.sh`

### Less

Less config is into a binarry file called `$HOME/.less`.

Compile the file `$HOME/.lesskey` with `lesskey` command to generate it.

Sources: https://www.systutorials.com/docs/linux/man/1-lesskey/#lbAE

### Youtube-dl

Download it from the repositories:

`sudo apt-get install youtube-dl`

Update it to the last version:

`sudo -H pip install --upgrade youtube-dl`

## Navigation

All shortcuts are vim-style (H, J, K, L + U, D) and they are configured to work without conflicts coherently between i3wm, tmux, (neo)vim et al. Explanation:

Horizontal navigation between WM workspaces, tmux windows and vim buffers only has two directions: left and right. In this case, a modifier in combination with H and L is coherent with vim-style.

Four directions navigation (e.g. i3wm windows, tmux panes, vim windows) needs four keys: for left, right, top and bottom. In this case, a modifier in combination with H, J, K, L is coherent with vim-style.

Vertical navigation to scroll up/down tmux windows, vim buffers or man pages has two directions but as well two speeds. In this case, a modifier in combination with J, K, U and D is coherent with vim-style.

These are the guidelines:
- Vim-like navigation.
- Make it intuitive.
- Reduce the keystrokes.
- Improve the workflow.

That said, it is very logical to have different modifier keys for every application:
- <kbd>Super</kbd> to control the windows manager (i3wm in my case).
- <kbd>Alt</kbd> to control the terminal multiplexer (tmux in my case).
- <kbd>Control</kbd> to control a specific program (vim, w3m, irssi).

Tmux and vim share <kbd>Alt</kbd>+{hjkl} to navigate between tmux panes and vim windows; thanks to the plugin [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator).

Tmux uses a prefix key to separate all the shortcuts from the system. This idea is very convenient to avoid conflicts between shortcuts, however it implies too much keystrokes. This prefix also has some disadvantages, because it uses the default <kbd>Control</kbd>+<kbd>b</kbd>: you lose a useful readline command (backward character). Some people remap it to <kbd>Control</kbd>+<kbd>a</kbd> because it's easier to press, so they lose a useful readline command (go to the start of the line). Also, it is used into vim to increase a numeric value.

My recommendation is to use the <kbd>Alt</kbd> key to remap some tmux bind-keys (using the `-n` flag), skipping the prefix for the most used actions.

The following table shows the main workflow:

```
| ACTION        | I3WM          | TMUX         | VIM          |
| $mod key      | Super         | Alt          | Control      |
| ------------- | ------------- | ------------ | ------------ |
|               | (workspaces)  | (windows)    | (buffers)    |
| Next          | Ctrl+Super+l  | Ctrl+Alt+l   | Ctrl+l       |
| Previous      | Ctrl+Super+h  | Ctrl+Alt+h   | Ctrl+h       |
| Last          | Ctrl+Super+p  | Ctrl+Alt+p   | Ctrl+p Enter |
| ------------- | ------------- | ------------ | ------------ |
|               |               | (windows)    | (buffers)    |
| Up: 1 line    |               | Alt+space k  | Ctrl+k       |
| Down: 1 line  |               | Alt+space j  | Ctrl+j       |
| Up: ½ page    |               | Alt+space u  | Ctrl+u       |
| Down: ½ page  |               | Alt+space d  | Ctrl+d       |
| ------------- | ------------- | ------------ | ------------ |
|               | (windows)     | (panes)      | (windows)    |
| Focus ←       | Super+h       | Alt+h        | Alt+h        |
| Focus →       | Super+l       | Alt+l        | Alt+l        |
| Focus ↑       | Super+k       | Alt+k        | Alt+k        |
| Focus ↓       | Super+j       | Alt+j        | Alt+j        |
| Focus last    |               |              | Ctrl+w p     |
| Focus next    |               |              | Ctrl+w l     |
| Focus prev    |               |              | Ctrl+w h     |
| Focus #1      | Super+1       | Alt+1        |              |
| Focus #2      | Super+2       | Alt+2        |              |
| Focus #3      | Super+3       | Alt+3        |              |
| Focus #4      | Super+4       | Alt+4        |              |
| Focus #5      | Super+5       | Alt+5        |              |
| Focus #6      | Super+6       | Alt+6        |              |
| Focus #7      | Super+7       | Alt+7        |              |
| Focus #8      | Super+8       | Alt+8        |              |
| Focus #9      | Super+9       | Alt+9        |              |
| New terminal  | Super+n       | Alt+n        | Ctrl+t       |
| Kill active   | Super+x       | Alt+x        | Ctrl+w j     |
| New terminal  | Ctrl+Super+n  | Ctrl+Alt+n   | Ctrl+t       |
| Kill active   | Ctrl+Super+j  | Ctrl+Alt+j   | Ctrl+w j     |
| Only active   |               |              | Ctrl+w o     |
| ------------- | ------------- | ------------ | ------------ |
|               | (windows)     | (panes)      | (windows)    |
| Fullscreen    | Super+f       | Alt+f        | Ctrl+f       |
| Resize ←      | Super+r h     | Alt+H        | >            |
| Resize →      | Super+r l     | Alt+L        | <            |
| Resize ↑      | Super+r k     | Alt+K        | -            |
| Resize ↓      | Super+r j     | Alt+J        | +            |
| Split v       | Super+.       | Alt+.        | Ctrl+w .     |
| Split h       | Super+-       | Alt+-        | Ctrl+w -     |
| ------------- | ------------- | ------------ | ------------ |
|               | (windows)     | (panes)      | (windows)    |
| Move to ←     | Super+H       |              | Ctrl+w H     |
| Move to →     | Super+L       |              | Ctrl+w L     |
| Move to ↑     | Super+K       | Alt+K        | Ctrl+w K     |
| Move to ↓     | Super+J       | Alt+J        | Ctrl+w J     |
| Move to last  | Super+Shift+p |              |              |
| Move to # WS  | Super+Shift+# |              |              |
```

Command line tools:

```
| ACTION        | man (less)    | w3m          | irssi        |
| ------------- | ------------- | ------------ | ------------ |
|               | (pages)       | (tabs)       | (windows)    |
| Next          |               | Ctrl+l       | Ctrl+j       |
| Previous      |               | Ctrl+h       | Ctrl+k (1)   |
| ------------- | ------------- | ------------ | ------------ |
|               | (buffers)     | (websites)   | (buffers)    |
| Up: 1 line    | k             | k            |              |
| Down: 1 line  | j             | j            |              |
| Up: ½ page    | u             | u            | Alt+u, Alt+p |
| Down: ½ page  | d             | d            | Alt+d, Alt+n |
|               |               |              |        (2)   |

---

| ACTION        | vifm          | ranger        | cmus         | mutt         |
| ------------- | ------------- | ------------- | ------------ | ------------ |
|               | (files, dirs) | (files, dirs) | (playlists)  | (emails)     |
| Up: 1 line    | k             | k             | k            | k            |
| Down: 1 line  | j             | j             | j            | j            |
| Custom ←      | h, fold       | h, fold       | h, seek -5   |              |
| Custom →      | l, unfold     | l, unfold     | l, seek +5   |              |

---

1. Irssi windows are displayed in a column (vertical) according to my setup.
2. Alt+p and Alt+n are configured by default into irssi.
```

PDF and images:

```
| ACTION        | mupdf         | apvlv         | feh          |
| ------------- | ------------- | ------------- | ------------ |
|               | (pdfs)        | (pdfs)        | (images)     |
| ←             | h             | h             | h            |
| →             | l             | l             | l            |
| ↑             | k             | k             | k            |
| ↓             | j             | j             | j            |
| Zoom in       | +             | z             | z            |
| Zoom out      | -             | Z             | Z            |
| Up: ½ page    | b             | u             |              |
| Down: ½ page  | space         | d             |              |
| Rotate        | R, L          | r             | <, >         |
| Quit          | q             | q             | q            |
```

Audio:

```
| ACTION        | cmus          |
| ------------- | ------------- |
| ← (-seek)     | h             |
| → (+seek)     | l             |
| ↑             | k             |
| ↓             | j             |
| Pause         | c             |
| Stop          | v             |
| Volume up     | +             |
| Volume down   | -             |
| Quit          | q             |
```

Video:

```
| ACTION        | mpv           |
| ------------- | ------------- |
| ← (-seek)     | h             |
| → (+seek)     | l             |
| ←             | Ctrl+h        |
| →             | Ctrl+l        |
| ↑             | Ctrl+k        |
| ↓             | Ctrl+j        |
| Reset         | Ctrl+p        |
| Zoom in       | z             |
| Zoom out      | Z             |
| Reset zoom    | Ctrl+z        |
| Rotate        | r             |
| Reset rotate  | Ctrl+r        |
| Volume up     | +             |
| Volume down   | -             |
| Quit          | q             |
```

Yes, a mouse would make the life easier. And slower ;-)

This setup works in Devuan 5.
