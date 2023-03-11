## Command Shortcuts
I'm currently using zsh terminal and to add aliases I have to open a file with the following command in my terminal
```
% code ~/.zshrc
```

To write your own alias the syntax is
```
alias shortcut='actualcommand'
```

I currently have to type the following for git
```
% git add --all
% git commit -m ""
% git push origin main
% git status
```

It would be much easier if I could only type the following
```
% ga
% gc ""
% gp
% gs
```

To create the shortcut I'll use the syntax and put in my .zshrc file like so
```
alias ga='git add --all'
alias gc='git commit -m'
alias gp='git push origin main
alias gs='git status'
```

Once you've entered your aliases save and close the file.
In your terminal run the following command to reload file.
```
% source ~/.zshrc
```

Now you're all set. 

