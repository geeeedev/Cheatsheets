# Purpose: Learning Bash Syntax 

[15 Useful Bash Shell Built-in Commands (With Examples)](https://www.thegeekstuff.com/2010/08/bash-shell-builtin-commands/)

cat == print or output [filepath] content in Terminal 
\~/ == \$Home == Users/gwennielau  
echo == print  
\> == print to [filepath], overwrite existing content  
\>> == print to [filepath], continue after existing content  
eval == execute [command]  
export == export [variable-or-function] to the environment of all the child processes running in the current shell  
env == lists all the environment variables  
...  
...  
...  

### Existing .bash_profile content example
```terminal
Gwennies-MacBook-Pro:~ gwennielau$ cat ~/.bash_profile -->
                                                        # an actual blank line in file
# Setting PATH for Python 3.8  
# The original version is saved in .bash_profile.pysave  
PATH="/Library/Frameworks/Python.framework/Versions/3.8/bin:${PATH}"  
export PATH  
export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"  
export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"      # rebuild to remove this line
export PYENV_ROOT="$HOME/.pyenv"  
export PATH="$PYENV_ROOT/bin:$PATH"  
eval "$(pyenv init --path)"  
```








