# Python Help
---

## Compiling Python Code via Cython

### Install cython
`pip install cython`

### Transpile Python to C
For python 2:  
`cython --embed py.py -2 -I /usr/include/python2.7m/`

For python 3:  
`cython --embed py.py -3 -I /usr/include/python3.6m/`

### Compile C to Executable
For python 2:  
```
gcc `python2-config --cflags --ldflags` py.c -o py
```

For python 3?:  
```
gcc `python-config --cflags --ldflags` py.c -o py
```
