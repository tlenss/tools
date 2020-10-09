# tools

broot (https://dystroy.org/broot/)

# ctop
https://github.com/bcicen/ctop
```
sudo wget https://github.com/bcicen/ctop/releases/download/v0.7.2/ctop-0.7.2-linux-amd64 -O /usr/local/bin/ctop
sudo chmod +x /usr/local/bin/ctop
```
# terminal
```
apt install terminator
```

# lazydocker
```
curl https://raw.githubusercontent.com/jesseduffield/lazydocker/master/scripts/install_update_linux.sh | bash
echo "alias lzd='lazydocker'" >> ~/.zshrc
```

# shortened manpages
```
apt install tldr
```

# commandline correcty tool
```
apt install fuck
```

# zsh shell
```
apt install zsh
```

# run parallel commands over multiple cpu cores
```
apt install parallel
```

# json processor
```
apt install jq
```

# pipe data monitor
```
apt install pv
```

# search
```
apt install silversearcher-ag
```

# ls but better
```
snap install lsd
```

# fuzzy finder
```
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

# better cat and with syntax higlighting
```
wget https://github.com/sharkdp/bat/releases/download/v0.10.0/bat_0.10.0_amd64.deb
dpkg -i bat_0.10.0_amd64.deb
```

# beter find
```
wget https://github.com/sharkdp/fd/releases/download/v7.3.0/fd_7.3.0_amd64.deb
dpkg -i fd_7.3.0_amd64.deb
```

# Disk Usage/Free Utility
```
git clone https://github.com/muesli/duf.git
cd duf
go buil
```

# ZSH stuff

# zsh theme
```
git clone https://github.com/denysdovhan/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt"
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
```

# manage zsh stuff
```
curl -sL --proto-redir -all,https https://raw.githubusercontent.com/zplug/installer/master/installer.zsh | zsh
```
```
vi ~/.zshrc
```

```
source "/home/tlenssel/.zplug/init.zsh"

# Locale
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8

# Exports
export PATH=$HOME/bin:/usr/local/bin:/home/[path]/.local/bin:$PATH
export PATH="/usr/local/opt/gnu-tar/libexec/gnubin:$PATH"
export PATH="$HOME/.symfony/bin:$PATH"
export PATH="/usr/local/sbin:$PATH"
export PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"

export EDITOR='vim'
export GPG_TTY=$(tty)
export GOPATH="/home/[path]/Dev/go-dev"

export DEFAULT_USER=username
export SPACESHIP_PROMPT_ADD_NEWLINE=false
export SPACESHIP_KUBECONTEXT_SHOW=false
export ZSH=/home/[path]/.oh-my-zsh
export SSH_KEY_PATH="$HOME/.ssh/id_rsa"

ssh-add -A &> /dev/null

alias c="clear"
alias mux="tmuxinator"

setopt BANG_HIST
setopt EXTENDED_HISTORY
setopt INC_APPEND_HISTORY
setopt SHARE_HISTORY
setopt HIST_EXPIRE_DUPS_FIRST
setopt HIST_IGNORE_DUPS
setopt HIST_IGNORE_ALL_DUPS
setopt HIST_FIND_NO_DUPS
setopt HIST_IGNORE_SPACE
setopt HIST_SAVE_NO_DUPS
setopt HIST_REDUCE_BLANKS
setopt HIST_VERIFY
setopt HIST_BEEP

# Default pager
export PAGER='less'

# less options
less_opts=(
  # Quit if entire file fits on first screen.
  --quit-if-one-screen
  # Ignore case in searches that do not contain uppercase.
  --ignore-case
  # Allow ANSI colour escapes, but no other escapes.
  --RAW-CONTROL-CHARS
  # Quiet the terminal bell. (when trying to scroll past the end of the buffer)
  --quiet
  # Do not complain when we are on a dumb terminal.
  --dumb
)
export LESS="${less_opts[*]}"

# Default editor for local and remote sessions
if [[ -n "$SSH_CONNECTION" ]]; then
  # on the server
  if [ command -v vim >/dev/null 2>&1 ]; then
    export EDITOR='vim'
  else
    export EDITOR='vi'
  fi
else
  export EDITOR='vim'
fi

# SSH
color-ssh() {
    trap "~/Bin/colorterm.sh" INT EXIT
    if [[ "$*" =~ "www-6" ]]; then
        ~/Bin/colorterm.sh prod
    elif [[ "$*" =~ "dev-1" ]]; then
        ~/Bin/colorterm.sh dev
    else
        ~/Bin/colorterm.sh other
    fi
    ssh $*
}
alias ssh=color-ssh

# Misc aliases
alias ls='ls -GFh --color=auto'
alias prettyjson='python -m json.tool'

# Docker aliases
alias docker-commands='docker inspect -f "{{.Name}} {{.Config.Cmd}}" $(docker ps -a -q)'
alias docker-cleanup="docker ps -a | grep Exited | awk {'print $1'} | xargs docker rm"

alias php7='docker run --rm \
-ti \
-e COMPOSER_HOME \
-v ${PWD}:/code \
-e COMPOSER_AUTH \
-v $COMPOSER_HOME:$COMPOSER_HOME \
-e COMPOSER_MEMORY_LIMIT=-1 \
-e SSH_AUTH_SOCK=/ssh-auth.sock \
-v $SSH_AUTH_SOCK:/ssh-auth.sock \
-v /etc/passwd:/etc/passwd:ro \
-v /etc/group:/etc/group:ro \
-v /home/$USERNAME/.ssh/known_hosts:/home/$USERNAME/.ssh/known_hosts \
-v /home/$USERNAME/.gitconfig:/home/$USERNAME/.gitconfig \
--user ${UID}:${GID} \
--workdir /code \
[IMAGE]:7.0-dev '

alias php73='docker run --rm \
-ti \
-e COMPOSER_HOME \
-v ${PWD}:/code \
-e COMPOSER_AUTH \
-v $COMPOSER_HOME:$COMPOSER_HOME \
-e COMPOSER_MEMORY_LIMIT=-1 \
-e SSH_AUTH_SOCK=/ssh-auth.sock \
-v $SSH_AUTH_SOCK:/ssh-auth.sock \
-v /etc/passwd:/etc/passwd:ro \
-v /etc/group:/etc/group:ro \
-v /home/$USERNAME/.ssh/known_hosts:/home/$USERNAME/.ssh/known_hosts \
-v /home/$USERNAME/.gitconfig:/home/$USERNAME/.gitconfig \
--user ${UID}:${GID} \
--workdir /code \
[IMAGE]:7.3-dev '

alias phpunit='docker run --rm \
-ti \
-v ${PWD}:/code \
--user ${UID}:${GID} \
--workdir /code \
[IMAGE]:7.0-dev /code/vendor/bin/phpunit '

export COMPOSER_HOME=$HOME/.composer
export COMPOSER_AUTH=$(cat ~/.composer/auth.json)

phps=("7.0" "7.1" "7.2" "7.3" "7.4")

function composer() {
  PHP_VERSION='7.0'
  PS3='select version: '

  select opt in $phps; do
    if [[ ! -v "phps[$REPLY]" ]] ; then
      echo "Invalid option"
      continue
    else
      PHP_VERSION=$opt
      break
    fi
  done

  docker run --rm --interactive --tty \
  --env COMPOSER_HOME \
  --env SSH_AUTH_SOCK=/ssh-auth.sock \
  --env COMPOSER_MEMORY_LIMIT=-1 \
  --env COMPOSER_AUTH=$(cat ~/.composer/auth.json) \
  --user ${UID}:${GID} \
  --volume $SSH_AUTH_SOCK:/ssh-auth.sock \
  --volume /etc/passwd:/etc/passwd:ro \
  --volume /etc/group:/etc/group:ro \
  --volume /home/$USERNAME/.ssh/known_hosts:/home/$USERNAME/.ssh/known_hosts \
  --volume $COMPOSER_HOME:$COMPOSER_HOME \
  --volume $PWD:/var/www/html \
  [IMAGE]:$PHP_VERSION-dev composer "$@"
}

# ------------------------------------------------------------------------------
# Dependencies
# ------------------------------------------------------------------------------

# Let zplug manage itself like other packages
zplug 'zplug/zplug', hook-build:'zplug --self-manage'

# Oh-My-Zsh core
zplug "lib/*", from:oh-my-zsh

# Oh-My-Zsh plugins
zplug "plugins/history-substring-search", from:oh-my-zsh
zplug "plugins/git", from:oh-my-zsh
zplug "plugins/git-extras", from:oh-my-zsh
zplug "plugins/git-completion", from:oh-my-zsh
zplug "plugins/git-flow", from:oh-my-zsh
zplug "plugins/brew", from:oh-my-zsh
zplug "plugins/composer", from:oh-my-zsh
zplug "plugins/docker-compose", from:oh-my-zsh
zplug "plugins/docker", from:oh-my-zsh
zplug "plugins/screen", from:oh-my-zsh
zplug "plugins/extract", from:oh-my-zsh
zplug "plugins/ssh-agent", from:oh-my-zsh
zplug "plugins/autojump", from:oh-my-zsh

# SSH
zstyle :omz:plugins:ssh-agent agent-forwarding on
zstyle -a :omz:plugins:ssh-agent identities id_rsa
zstyle -a :omz:plugins:ssh-agent identities tl_rsa
zstyle -a :omz:plugins:ssh-agent identities id_rsa_bitbucket
zstyle :omz:plugins:ssh-agent lifetime 4h

# Zsh improvements
zplug "zsh-users/zsh-autosuggestions"
zplug "zsh-users/zsh-syntax-highlighting"
zplug "hlissner/zsh-autopair", defer:2

# Spaceship ZSH
zplug "denysdovhan/spaceship-prompt", as:theme, use:"spaceship.zsh"

# Install plugins if there are plugins that have not been installed
if ! zplug check --verbose; then
  zplug install
fi

# Then, source plugins and add commands to $PATH
zplug load

eval $(thefuck --alias)


[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
alias lzd='lazydocker'
```
