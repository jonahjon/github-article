## Tip 1 .git config file

vi ~/.bash_profile > i > paste():


```
function __git_dirty {
  git diff --quiet HEAD &>/dev/null
  [ $? == 1 ] && echo "!"
}

function __git_branch {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

bash_prompt() {
  local NONE="\[\033[0m\]"    # unsets color to term's fg color

  # regular colors
  local K="\[\033[0;30m\]"    # black
  local R="\[\033[0;31m\]"    # red
  local G="\[\033[0;32m\]"    # green
  local Y="\[\033[0;33m\]"    # yellow
  local B="\[\033[0;34m\]"    # blue
  local M="\[\033[0;35m\]"    # magenta
  local C="\[\033[0;36m\]"    # cyan
  local W="\[\033[0;37m\]"    # white

  local UC=$W                 # user's color
  [ $UID -eq "0" ] && UC=$R   # root's color

  export PS1="\A $W$Y\w $G\$(__git_branch)$R\$(__git_dirty)${NONE}$ "

}

bash_prompt
unset bash_prompt
```


touch ~/.gitignore
git config --global core.excludesfile ~/.gitignore
vi ~/.gitignore


Git Ignore

# Keys #
###########
*.pem#

# Logs and databases #
######################
*.sqlite

# OS generated files #
######################
.DS_Store
.Trashes