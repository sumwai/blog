---
title: vim fzf script
date: 2022-04-29T14:57:50+08:00
draft: true
---

### Install nvim and fzf

```shell
sudo pacman -Syy vim neovim fzf
```

### use script

```bash
#!/bin/bash

# if $1 not set, set path to `pwd`
if [ "$1" == '' ]; then
  path=`pwd | sed 's/\/*$//g'`
else
  # if not a dir
  if test ! -d $1; then
    exit;
  fi
  # trim '/' end the string
  path=`echo $1 | sed 's/\/*$//g'`
fi

# select file
file=$(cd $path && sudo fzf)

# if fzf return empty
if [ "$file" == '' ]; then
  exit
fi

# if file not found
if test ! -e "${path}/${file}"; then
  exit;
fi

# start nvim
cd $path && sudo -E nvim $file

# if quit, back to last workspace
cd - > /dev/null
```

### Move script to PATH

```shell
sudo mv vf /usr/local/bin/vf
```

### vf Usage

```shell
# open vim `fzf` on pwd
vf 
# open vim `fzf` on other directory
vf /etc
```

