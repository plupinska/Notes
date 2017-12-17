
### Some useful stuff for logging git info in bashrc

`g() {
  if [[ $# > 0 ]]; then
    git $@
  else
    git status
  fi
}`

`parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}`
`export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] \$ "`
