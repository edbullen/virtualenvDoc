# Virtual Environment and Multiple Python versions on Mac
Quick personal notes on setting up virtual env and multiple Python versions on Mac


## Virtual Environments with virtualenv wrapper

```
brew install virtualenvwrapper
```

Make a new v-env

```
mkvirtualenv my-project
```

Use the new v-env

```
workon my-project
```

deactivate
```
deactivate my-project
```

list
```
lsvirtualenv
```


remove

```
rmvirtualenv my-project
```



## Multiple Python Versions with pyenv

```
brew install pyenv
```

install a versin of Python
```
pyenv install 3.7.9
```

list versions 
```
pyenv versions
```

current version
```
pyenv version
```

Set the version of python to work with *in a particular folder*:
```
pyenv local 3.7.9
```
(sets the python version when working in the folder where this version was initialised)

## Specify the version of Python to use with a virtual environment

Activate the version of Python you want to use (i.e. `pyenv local 3.7.9`).   

Create a virtual env that uses that version.

```
mkvirtualenv --python=`pyenv which python` myproject
```


Activate it with `workon`

## Example `.zprofile`

```
# Configuration for virtualenv
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/opt/homebrew/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=/opt/homebrew/bin/virtualenv
source /opt/homebrew/bin/virtualenvwrapper.sh
 
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
 
# use the same directory for virtualenvs as virtualenvwrapper
export PIP_VIRTUALENV_BASE=$WORKON_HOME
# makes pip detect an active virtualenv and install to it
export PIP_RESPECT_VIRTUALENV=true
if [[ -r /usr/local/bin/virtualenvwrapper.sh ]]; then
source /usr/local/bin/virtualenvwrapper.sh
else
     echo "WARNING: Can't find virtualenvwrapper.sh"
fi
                
```
