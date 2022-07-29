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
lsvirtualenv -b
```


remove

```
rmvirtualenv my-project
```



## Multiple Python Versions with pyenv

```
brew install pyenv
```

install a version of Python
```
pyenv install 3.7.9
```

NOTE: various compatibility issues on Mac M1 chips with Python earlier than 3.8: https://bugs.python.org/msg382939

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
eval "$(/opt/homebrew/bin/brew shellenv)"

# Configuration for virtualenv
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/opt/homebrew/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=/opt/homebrew/bin/virtualenv
source /opt/homebrew/bin/virtualenvwrapper.sh

export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

# Fix path issue in Pycharm for virtualenvwrapper.sh 
export PATH=$PATH:/opt/homebrew/bin
# use the same directory for virtualenvs as virtualenvwrapper
export PIP_VIRTUALENV_BASE=$WORKON_HOME

# makes pip detect an active virtualenv and install to it
export PIP_RESPECT_VIRTUALENV=true
                
```


## Getting Pycharm Projects to pick up the virtual env

This was painful, but it can be done.

Useful Stack Overflow forum: https://stackoverflow.com/questions/34520291/pycharm-cannot-find-the-packages-in-virtualenv

**Step 1** Select Setup for the Python Interpreter for this Project

![Alt text](Pycharm_screenshot_Step1.png?raw=true "Step1")

**Step 2** Add an new Interpreter for this Project

![Alt text](pycharm_screenshot_Step2.png?raw=true "Step2")

**Step 3** Select the Python executable in the correct Virtualenv path
![Alt text](pycharm_screenshot_Step3.png?raw=true "Step3")

**NOTE** Sometime the V-env doesn't show up in the list - you have to navigate using the elipsis (`...`) by the Interpreter dialog box and find the path to the linked Python interpreter for the virtual env required.

![Alt text](pycharm_screenshot_Step3_b.png?raw=true "Step3_b")
