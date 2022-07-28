# Virtual Environment and Multiple Python versions on Mac
Quick notes on setting up virtual env and multiple Python versions on Mac


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

Set the version of python to work with:
```
pyenv local 3.7.9
```


## Specify the version of Python to use with a virtual environment

Activate the version of Python you want to use (i.e. `pyenv local 3.7.9`).   

Create a virtual env that uses that version.

```
mkvirtualenv --python=`pyenv which python` myproject
```


Activate it with `workon`

