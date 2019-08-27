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

## change command
To change command name, replace entry_point at setup.py.

```setup.py
if __name__ == "__main__":
    setuptools.setup(
        name='udf',
        version='0.0.1',
        packages=setuptools.find_packages(),
        entry_points={
            'console_scripts':[
                'udf = myapp.main:main',
            ],
        },
    )
```

And run command.
```
$ python setup.py sdist
$ pip install dist/udf-0.0.1.tar.gz
$ udf a b

['path to myapp module', 'a', 'b']
```

## change branch
add branch name in requirements.txt

```requirements.txt
-e git+https://github.com/TomHortons/py_command.git@master#egg=py_command
```