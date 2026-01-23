# learning_software_dev

## Git branch names and colours on Ubuntu and Conda show: add to .bashrc
```
# Show git branch name
force_color_prompt=yes
color_prompt=yes

parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

conda_env_prompt() {
  if [[ -n "$CONDA_DEFAULT_ENV" ]]; then
    echo "($CONDA_DEFAULT_ENV)"
  fi
}

if [ "$color_prompt" = yes ]; then
  PS1='$(conda_env_prompt)${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
else
  PS1='$(conda_env_prompt)${debian_chroot:+($debian_chroot)}\u@\h:\w$(parse_git_branch)\$ '
fi

unset color_prompt force_color_prompt
```

## Pretty terminal
```
unset __conda_setup
# <<< conda initialize <<<

export PATH=/usr/local/cuda-12.1/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-12.1/lib64/stubs${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export PATH="$CONDA_PREFIX/bin:$PATH"

# Show git branch name
force_color_prompt=yes
color_prompt=yes

parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

if [ "$color_prompt" = yes ]; then
  PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
else
  PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w$(parse_git_branch)\$ '
fi

unset color_prompt force_color_prompt
```

## Not breaking conda pip environments, add to .bashrc
`export PATH="$CONDA_PREFIX/bin:$PATH"`
