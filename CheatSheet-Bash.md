# Purpose: Learning Bash Syntax 

[15 Useful Bash Shell Built-in Commands (With Examples)](https://www.thegeekstuff.com/2010/08/bash-shell-builtin-commands/)

cat == print or output [filepath] content in Terminal 
\~/ == \$Home == Users/gwennielau  
echo == print  
\> [filepath] == print to [filepath], overwrite existing content  
\>> [filepath] == print to [filepath], continue after existing content  
source [filepath] == reads and executes commands from [filepath] specified as its argument in the current shell environment. It is useful to load functions, variables, and configuration files into shell scripts.
eval [command] == execute [command]  
export [var] == export [variable-or-function] to the environment of all the child processes running in the current shell  
env == lists all the environment variables  
...  
...  
...  
> Restart your login session for the changes to take effect.  
    - In MacOS, restarting terminal windows is enough (because MacOS runs shells in them as login shells by default).  
    - If you're in a GUI session, you need to fully log out and log back in.  

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

'export PATH="/Users/gwennielau/Library/Python/3.8/bin:$PATH"'
echo 'export PATH="/Users/gwennielau/Library/Python/3.8/bin:$PATH"' >> ~/.profile

### Rebuild .bash_profile (To Remove Duplicates)
- enter in Terminal:
```bash
echo '' > ~/.bash_profile
echo '# Setting PATH for Python 3.8' >> ~/.bash_profile
echo '# The original version is saved in .bash_profile.pysave' >> ~/.bash_profile
echo 'PATH="/Library/Frameworks/Python.framework/Versions/3.8/bin:${PATH}"' >> ~/.bash_profile
echo 'export PATH' >> ~/.bash_profile
echo 'export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"' >> ~/.bash_profile
echo 'export PATH="/Users/gwennielau/Library/Python/3.8/bin:$PATH"' >> ~/.bash_profile
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(pyenv init --path)"' >> ~/.bash_profile
```

### Listing Existing Environment Variables
```terminal
Gwennies-MacBook-Pro:~ gwennielau$ env

TERM_PROGRAM=Apple_Terminal             ## env from Terminal
PYENV_ROOT=/Users/gwennielau/.pyenv
SHELL=/bin/bash
TERM=xterm-256color
TMPDIR=/var/folders/x0/vv1dzrss0js28gslzd5rrcnm0000gn/T/
TERM_PROGRAM_VERSION=433
TERM_SESSION_ID=C0355DBE-3EFD-4EF2-8A21-2DD3B1791DF2
USER=gwennielau
SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.0YoXNBaRNr/Listeners
PATH=/Users/gwennielau/Library/Python/3.8/bin:/Users/gwennielau/.pyenv/shims:/Users/gwennielau/.pyenv/bin:/usr/local/opt/openssl@1.1/bin:/usr/local/opt/openssl@1.1/bin:/Library/Frameworks/Python.framework/Versions/3.8/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/share/dotnet:~/.dotnet/tools
PWD=/Users/gwennielau
LANG=en_US.UTF-8
XPC_FLAGS=0x0
XPC_SERVICE_NAME=0
SHLVL=1
HOME=/Users/gwennielau
LOGNAME=gwennielau
_=/usr/bin/env
```

```
Gwennies-MacBook-Pro:dwellinglybackend gwennielau$ env

TERM_PROGRAM=vscode                     ## env from VSCode
PYENV_ROOT=/Users/gwennielau/.pyenv
TERM=xterm-256color
SHELL=/bin/bash
TMPDIR=/var/folders/x0/vv1dzrss0js28gslzd5rrcnm0000gn/T/
TERM_PROGRAM_VERSION=1.58.2
ORIGINAL_XDG_CURRENT_DESKTOP=undefined
USER=gwennielau
SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.0YoXNBaRNr/Listeners
__CF_USER_TEXT_ENCODING=0x1F5:0x0:0x0
PATH=/Users/gwennielau/Library/Python/3.8/bin:/Users/gwennielau/.pyenv/shims:/Users/gwennielau/.pyenv/bin:/usr/local/opt/openssl@1.1/bin:/usr/local/opt/openssl@1.1/bin:/Library/Frameworks/Python.framework/Versions/3.8/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/share/dotnet:~/.dotnet/tools:/usr/local/opt/openssl@1.1/bin:/Library/Frameworks/Python.framework/Versions/3.8/bin
PWD=/Users/gwennielau/Documents/REVIEW/--WORK/17CodePDX/Dwellingly/dwellinglybackend
LANG=en_US.UTF-8
XPC_FLAGS=0x0
XPC_SERVICE_NAME=0
SHLVL=2
HOME=/Users/gwennielau
VSCODE_GIT_ASKPASS_MAIN=/Applications/Visual Studio Code.app/Contents/Resources/app/extensions/git/dist/askpass-main.js
LOGNAME=gwennielau
VSCODE_GIT_IPC_HANDLE=/var/folders/x0/vv1dzrss0js28gslzd5rrcnm0000gn/T/vscode-git-5280f58605.sock
VSCODE_GIT_ASKPASS_NODE=/Applications/Visual Studio Code.app/Contents/Frameworks/Code Helper (Renderer).app/Contents/MacOS/Code Helper (Renderer)
GIT_ASKPASS=/Applications/Visual Studio Code.app/Contents/Resources/app/extensions/git/dist/askpass.sh
COLORTERM=truecolor
_=/usr/bin/env
```




