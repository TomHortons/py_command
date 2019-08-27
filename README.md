py_command

---
This package demonstrates follows:
1. how to create a python package using setup.py
2. how to install private package from github

# Tutorial

### prep env
```
$ python -m venv .env
$ source .env/bin/activate
```

## install from github
```
$ myapp a b
command not found: myapp

$ pip install -r requirements.txt
$ myapp a b

['path to myapp module', 'a', 'b']

$ pip uninstall myapp
```

## create zip locally
```
$ myapp a b
command not found: myapp

$ python setup.py sdist
$ pip install dist/myapp-0.0.1.tar.gz
$ myapp a b

['path to myapp module', 'a', 'b']

$ pip uninstall myapp
```

## build on docker
Note that this dockerfile separates compiling and building image in order to avoid slow 'pip install' which is sometimes happen when compiling image on Docker.

```
$ docker build ./ -t example
$ docker run example

['/app/env/bin/myapp', 'a', 'b']
```
