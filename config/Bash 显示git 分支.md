## Bash 显示git 分支

### 通用版本

function git_branch {
​    ref=$(git symbolic-ref HEAD 2> /dev/null) || return;
​    echo "("${ref#refs/heads/}") ";
}

PS1="[\[\e[1;35m\]\u\[\e[1;32m\]\w\[\e[0m\]] \[\e[0m\]\[\e[1;36m\]\$(git_branch)\[\e[0;33m\]\$"

