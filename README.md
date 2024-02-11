# Dotfiles for WSL
This repository hosts all my public configuration files for WSL. These dotfiles offer the following features:

* Modular configuration of *$SHELL* (*BASH* & *ZSH*): the *shellconfig* folder contains multiple files that can easily be customized
* Automated prompt customization: two custom prompts are possible (with or without *Starship* prompt). If using *TMUX*, all plugins are automatically installed. *VIM/Neovim* plugins are also automatically installed
* Remote session detection: certain things will not be enabled when a SSH session is detected (for servers). Also, the dotfiles will not be loaded at all when a non-interactive session is opened (ex.: SFTP connection)
* Quick discharge: an alias called either *bbash* or *zzsh* (depending on your $SHELL) is present to quickly open a session without any of the dotfiles loaded. This is useful for testing/troubleshooting using a vanilla shell environment. The same thing can be applied for some applications (ex.: *vvim* to load *VIM/Neovim* without any configuration)
* Easy to deploy as only generic paths/names are configured with the exception of certain variables explained below

<u>**Note**</u>: these dotfiles work on both macOS and Linux as well, but they are clearly designed for WSL specifically.

In its current state, my *$SHELL* loads quite quickly with the following statistics:


# Installation
It is possible to simply clone this repository and use the dotfiles (symlinks or copy the files):

```
git clone --depth 1 https://github.com/astsu777/dotfiles-wsl.git "$HOME"/.dotfiles-wsl
```

It is necessary to modify either the *.bashrc* or the *.zshrc* file and change the following variables according to your needs:
* **DOTFILES**: defines the default location of the dotfiles ($HOME/.dotfiles).
* **SCRIPTS**: defines the default location of the custom scripts ($HOME/.local/bin)
* **SOURCES**: defines the default location of source files ($HOME/.sources)
* **REPOS**: defines the default location of git repositories ($HOME/.sources/repos)

# Documentation - Root Folder
## Git
The file *gitconfig* contains the global *Git* configuration and several aliases to make life easier when using *Git* client.

## Links
*Links* is a text Web browser to run inside a terminal emulator. It can be very useful to read certain Web pages by only getting the text and not all the JavaScript, CSS, etc... It is very useful to be combined with a RSS reader such as *newsboat* for example. The custom config files stored in *links/* contains some customization but it stays very close to the defaults of the program.

## Shell/Prompt
The folder *shellconfig* contains all the config files used to customize my shell and my command prompt. It is modular: this means that both *BASH* and *ZSH* configurations are split between different files so it is common in both shells. I use *ZSH* on my workstations and *BASH* on all my servers and sometimes workstations: both are using the same dotfiles.

The logic of every file is the following:

* *bashrc*/*zshrc*: the configuration file of both *BASH* and *ZSH* respectively
* *inputrc*: customization for *BASH*
* *zshenv*: file necessary to load my *.zshrc* because it is not located in my *$HOME* folder
* *common*: settings that are common to both shells (environment variables, some settings, etc...)
* *functions*: all functions are defined here. I wanted them to be separated from aliases
* *apps_aliases*: contains all aliases for external applications (not built-in to the shell AND not drop-in replacements for important commands such as *ls* for example)
* *basecmds_aliases*: contains aliases that replace certain basic commands such as *cat* replaced by *highlight* for example
* *enhancements_aliases*: alias basic commands such as *ls* and automatically add some parameters such as auto-color

### Quick Discharge
Sometimes, it can be useful to drop all the customization and have a plain vanilla *BASH*/*ZSH* environment. In order to do this, it is pretty simple:

* *BASH*: type *bbash* and a new shell will be opened without any configuration whatsoever
* *ZSH*: type *zzsh* and a new shell will be opened without any configuration whatsoever

The same is available for other applications. For example, *VIM*/*Neovim* can be launched with the alias *vvim* and no configuration will be loaded.

## VIM/Neovim
![](https://i.postimg.cc/bvK0ZNTJ/screenshot-20210718-029.png)

In this repository, the *vim* folder contains all the necessary configuration files for *VIM*. However, I use *Neovim* as my text editor (mostly for new window stuff) but don't have a specific config file for it: the *~/.config/nvim/init.vim"* is actually a symlink to the *.vimrc*. When deploying my dotfiles, simply symlink the *vim* folder to *~/.config/nvim* and it will work.

Because the *VIM* configuration is quite light, it is fully compatible with *Neovim*. There is no *Neovim* specific setting present. The colorscheme used by default is called *[kuroi](https://github.com/aonemd/kuroi.vim)* and is made by *Aonemd*. I simply disabled the background to use the one set by the terminal emulator (usually a little bit transparent and dark). Other color schemes are installed and custom keybindings can be used to toggle between them.

A folder called *ftplugin* contain specific configuration for various file types.

The following keybindings are configured:

* **LEADER** has been configured to be **,** (=comma)

| Key Binding | Mode | Action |
| :--- | :--- | :--- |
| `LEADER + r` | NORMAL | reload VIM/Neovim configuration |
| `LEADER + +` | NORMAL | increase size of split |
| `LEADER + -` | NORMAL | decrease size of split |
| `LEADER + -` | NORMAL | reset size of split |
| `CTRL + h` | NORMAL | navigate to the window on the left |
| `CTRL + j` | NORMAL | navigate to the window on the bottom |
| `CTRL + k` | NORMAL | navigate to the window on the top |
| `CTRL + l` | NORMAL | navigate to the window on the right |
| `LEADER + y` | NORMAL | copy to the system clipboard |
| `LEADER + p` | NORMAL | paste from the system clipboard |
| `K` | NORMAL | navigate down 10 lines |
| `L` | NORMAL | navigate up 10 lines |
| `LEADER + o` | NORMAL | toggle spell check in English (US) |
| `LEADER + o + f` | NORMAL | toggle spell check in French (FR) |
| `LEADER + h` | NORMAL | type command to open a horizontal split |
| `LEADER + v` | NORMAL | type command to open a vertical split |
| `LEADER + F1` | NORMAL | toggle through the color schemes (all plugins except the custom default one) |
| `LEADER + F2` | NORMAL | toggle syntax highlighting (enabled by default) |
| `LEADER + n` | NORMAL | toggle Nerd Tree (plugin: nerdtree) |
| `LEADER + s` | NORMAL | check the file with Shellcheck |
| `LEADER + f` | NORMAL | enable Goyo (distraction-free typing) |
| `LEADER + f + f` | NORMAL | disable Goyo (distraction-free typing) |
| `LEADER + t + c` | NORMAL | toggle color code highlighting |
| `LEADER + SHIFT + f` | NORMAL | search files (plugin: fzf) |
| `LEADER + SHIFT + r` | NORMAL | search files' content (plugin: fzf) |
| `LEADER + SHIFT + o` | NORMAL | search available buffers (plugin: fzf) |
| `w + ! + !` | COMMAND | write the file using sudo |
| `LEADER + h` | NORMAL | toggle the status bar |
| `LEADER + SHIFT + c` | NORMAL | enable auto-commenting on new lines |
| `LEADER + SHIFT + c + d` | NORMAL | disable auto-commenting on new lines |
| `LEADER + Space` | NORMAL | jump to <++> marker and enter insert mode |
| `LEADER + Space` | VISUAL | jump to <++> marker and enter insert mode |
| `LEADER + LEADER + Space` | INSERT | jump to the next <++> marker |
| `; + l + o` | INSERT | insert *Lorem ipsum* paragraph |
| `; + b + l` | INSERT | insert comment block (may vary depending on file type) |
| `; + h + h` | INSERT | insert custom header (may vary depending on file type) |
| `LEADER + c` | NORMAL | process current file with a script called *compiler* (mainly for LaTeX) |
| `LEADER + SHIFT + p` | NORMAL | open preview of the compiled version of the current file |
| `g + c + <MOTION>` | VISUAL | (un)comment some text using a motion such as *gcap* to comment a whole paragraph (plugin: vim-commentary) |
| `c + s + <CURR_SURROUND> + <NEW_SURROUND>` | NORMAL | modify the surrounding quotes/parenthesies/etc... (plugin: vim-surround) |
| `d + s + <CURR_SURROUND>` | NORMAL | delete the surrounding quotes/parenthesies/etc... (plugin: vim-surround) |
| `y + s + <MOTION> + <NEW_SURROUND>` | NORMAL | surround text with quotes/parenthesies/etc... Use *yss* for the whole line, *ysiw* for a word, etc... (plugin: vim-surround) |
| `S + <NEW_SURROUNDINGS>` | VISUAL | surround paragraph with specified surroundings above and below the selected text (plugin: vim-surround) |
| `LEADER + r + r` | NORMAL | bulk rename files in the current directory (plugin: vim-renamer) |
| `LEADER + q` | NORMAL | toggle the quickfix window |

Additional keybindings are configured per filetype. All of them are described in the *ftplugin* folder. Most keybindings are for code snippets though and/or shortcuts while writing certain file types.

Finally, some keybindings are also provided by the installed plugins. All the useful ones are described in the above table.

# Documentation - Local Folder
### Scripts
Custom scripts are present in the folder *local/bin* for various things. This folder is present in the *$PATH* and all scripts can be called at any time. Some are meant to be called by other programs instead. For example, the folder *cron* contains scripts that can be used as cron jobs.

The following table provides a description of all the scripts:

| Script | Description |
| :--- | :--- |
| `android-webcam` | use an Android smartphone connected via USB as a webcam |
| `block-hosts` | implement various block-lists to the hosts file |
| `check-rep` | check a FQDN/IP/CVE/Hash against several search engines |
| `clear-dns-cache` | clear the local DNS cache if any is detected |
| `compiler` | compile a document to another format (mainly used for LaTeX) |
| `crontoggle` | enable/disable the cron jobs |
| `devour` | launch a new program and hide the current window (useful to hide terminal emulator) |
| `dhcp-server` | launch a local DHCP server |
| `displayselect` | quickly configure screen layout, mirroring, etc... |
| `dmenu-bookmarks` | display Web bookmarks in DMenu/FZF and open one in the default Web browser |
| `dmenu-mount` | mount connected USB devices using DMenu |
| `dmenu-nordvpn` | manage NordVPN using DMenu |
| `dmenu-pass` | use the *pass* password manager via DMenu |
| `dmenu-radio` | listen to Web radios via DMenu/FZF |
| `dmenu-record` | record the current screen, audio and/or the webcam via DMenu |
| `dmenu-run` | run prompt using DMenu with caching (remembers if TUI/GUI programs) |
| `dmenu-screenshot` | take a screenshot via DMenu |
| `dmenu-shutdown` | logout/suspend/hibernate/shutdown the computer via DMenu |
| `dmenu-stream` | check online streams and watch one via DMenu/FZF |
| `dmenu-system` | general menu with various options to manage the system via DMenu |
| `dmenu-theme` | change the overall WM/terminal emulator/VIM theme via DMenu |
| `dmenu-umount` | unmount connected USB devices using DMenu |
| `dmenu-unicode` | display all unicode and free font-awesome characters via DMenu and insert ehem anywhere |
| `dmenu-urimount` | mount a network share via DMenu |
| `dmenu-video` | watch/listen/download a local/online video via DMenu/FZF |
| `dmenu-websearch` | search online using various search engines via DMenu/FZF |
| `dmenu-wm` | list all opened windows and focus on one (like ALT-Tab on Windows) via DMenu |
| `docker-lab` | quickly spawn one or multiple CentOS/Debian containers for test purposes |
| `git_all_pull` | find all GIT repositories recursively and pull from them |
| `handler` | general file/URL mapper |
| `kbdbacklight` | adjust the keyboard backlight easily |
| `lsw` | list opened windows |
| `notification-log` | log all desktop notifications to console or to a file |
| `notifytoggle` | enable/disable a do-not-disturb mode (notifications are hidden) |
| `opout` | open a preview of certain file (most useful when called from Neovim/VIM) |
| `ssh-multi` | connect to one or multiple SSH servers in a *TMUX* window and sync input on all panes |
| `sxiview` | when opening a single image with *SXIV*, automatically expand to all other images in the same folder |
| `texclear` | clean all the build files generated by LaTeX |
| `tftp-server` | launch a local TFTP server |
| `tspool` | interact with task-spooler using either the *ts* or *tsp* command (or none if *task-spooler* is not installed) |
| `tui` | open a terminal emulator and execute a specific command (Ex.: 'tui htop' from DMenu) |
| `upcloud-manager` | easily interact with *Upcloud* API |
| `url_handler.sh` | file handler by file extensions of MIME types |
| `vttoggle` | toggle the ability to switch to other Virtual Terminals using CTRL-ALT-Fx |
| `websites-monitor` | quickly test many websites and test for error codes |
| `yt-archive` | easily download YouTube channels/playlists/videos with caching (backend: yt-dlp) |

<u>**Note**</u>: a symlink called *url_handler.sh* is referencing *handler* because this name is hardcoded in the program *Urlview*.

# Documentation - Config Folder
## Amfora - Gemini Client
![](https://i.postimg.cc/fTZK7yhS/screenshot-20210718-031.png)

The *Gemini* project is an alternative protocol to *HTTP* and can be used to serve text-only Websites over the Internet. It looks a lot like the *Gopher* protocol but is much newer and has some advantages. *Amfora* is a TUI client for *Gemini* capsules and its config file is located in the *config/amfora/config.toml* folder. The customization is mainly about the rendering, the keybindings and the colors used inside the application.

## HTOP
![](https://i.postimg.cc/jdtxmyf9/screenshot-20210925-050.jpg)

*Htop* is a TUI application to monitor the system in real-time. It can easily be customized through the *config/htop/htoprc* file. Most of the customization performed has everything to do with the layout:

* A customized two columns layout at the top
* Additional information such as system details (kernel,hostname,uptime), *systemd*/*SELinux* status, CPU temperatures and frequency, etc...
* All processes are sorted in a tree view, but it is collapsed by default (toggle with the asterisk and dash keys)
* Kernel and userland process threads are hidden
* The *basename* of a program is highlighted in bold in the process list
* New and old processes are highlighted for 5 seconds

## Newsboat
![](https://i.postimg.cc/qqH9xrkB/screenshot-20210718-038.png)

It is much more efficient to extract useful information from a lot of Websites using the RSS feeds rather than visiting the Website. It is also better for online privacy. My preferred RSS reader is *Newsboat*. Two files are used to configure this application:
* *config/newsboat/config*: this is the configuration file of the application itself. It is used for the customization, keybindings and also how to open certain links in the feeds
* *config/newsboat/urls*: this is the list of all the followed RSS feeds

Custom keybindings are defined on the *config* file. Here is the list:

* **MACRO** has been defined as ',' (=comma)

| Key Binding | Action |
| :--- | :--- |
| `j/k` | go down/up |
| `J/K` | go to previous/next feed |
| `g/G` | go to the top/bottom |
| `l` | open a feed/article |
| `h` | quit a feed/article |
| `a` | mark article as read |
| `e` | enqueue podcast for download |
| `n/N` | next/previous unread article |
| `U` | show URLs in an article |
| `MACRO + ,` OR `o` | open article in the default Web browser |
| `MACRO + t` | open article in the TUI Web browser |
| `MACRO + m` | download video from the article |
| `MACRO + v` | watch video from the article using *MPV* |

*Newsboat* comes with another program called *Podboat*. This is a companion application to download and listen to podcasts. When some podcasts are enqueued for download, *Podboat* can be used to download and listen to the podcasts. The keybindings for *Podboat* are all described in the program's status bar.

## Starship Prompt
The *[Starship](https://starship.rs/)* prompt is a cross-shell prompt compatible with *BASH*, *ZSH*, *FISH* and is written in *Rust*. I use this prompt on all my workstations so I can enjoy the same experience everywhere with some nice customization. When the *Starship* prompt is not installed, a more standard but yet customized prompt is also configured for *BASH* and *ZSH*. The following screenshot illustrates the *Starship* prompt vs. my customized *BASH* prompt:

![](https://i.postimg.cc/GmmxNftc/screenshot-20210718-036.png)

As shown by the screenshot, *Starship* shows some nice information about *Git* repositories and certain program versions when a folder contains certain file types. The customization of the prompt is handled by the *config/starship/starship.toml* file.

## Surfraw
I almost never use this application as I have my own script to perform Web search using various search engines. However, *surfraw* can still be useful and was an inspiration to create my own script. The file *config/surfraw/conf* only customizes what Web browser will be used when calling the program.

## TMUX
*TMUX* configuration has changed over the years and multiple config files are available. A single one is present for my workstations and two are aimed for remote SSH connections. The file called *tmux24-server.conf* is meant to be used on servers with *TMUX* v2.9 or higher (earlier versions should use the file called *tmuxpre29-server.conf* for compatibility purposes).

My dotfiles will open *TMUX* automatically unless the window manager is *DWM*, *BSPWM* or *i3*: I tend to open multiple terminal emulators when using a tiling window manager. This is configured in the file called *shellconfig/common*. On a remote server, *TMUX* is also automatically loaded upon login.
The look & feel differs between the workstation and the server configuration. The prefix keybinding too differs: CTRL+A for the workstation, CTRL+B for the server. Several themes are available as well.

<u>**Note**</u>: even though I also use a tiling window manager in macOS (called *Amethyst*), I still use *TMUX* automatically on my Mac as it is more convenient.

### Screen
A *screenrc* file is present in this repository in case I would not be able to use *TMUX*. It is very simple:

* Add keybinding to kill window with CTRL+k
* Set new windows as logged in automatically (avoid having to login manually)
* Enable SHIFT+PgUP/SHIFT+PgDOWN
* True colors and bold colors are enabled

## Weechat
![](https://i.postimg.cc/9MZdZ58B/screenshot-20210718-037.png)

*Weechat* has a lot of tweaks in its configuration provided in these dotfiles. Some plugins (called scripts) are also deployed but they also lead to potentially two issues:

* Plugins are mainly developed in *Perl*, *Ruby* and *Python*. An error message will appear of one these three dependencies is missing
* It is possible that plugins are outdated on first load: they need to be updated with the following commands:

```
/set script.scripts.download_enabled on
/script update
/script upgrade
```

The scripts download and deployment of the frameworks is never automated, not even by my [bootstrap script](https://github.com/astsu777/bootstrap.git) The reason for this is simply security.

# Contact
You can always reach out to me:

* [Twitter](https://twitter.com/astsu777)
* [Email](mailto:gaetan@ictpourtous.com)
