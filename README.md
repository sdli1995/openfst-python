# OpenFst-Python

[![Python Version](https://img.shields.io/badge/python-2.7%2C%203.5%2C%203.6%2C%203.7%2C%203.8%2C%203.9%2C%203.10%2C%203.11-blue.svg)](https://www.python.org/)
[![Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/ambv/black)

OpenFst-Python exposes the official Python API to
[OpenFst](http://www.openfst.org/twiki/bin/view/FST/WebHome)
(officially called pywrapfst), but includes all the required OpenFst libraries
in the Python package, so you don't need to install it separately.

The version number of OpenFst-Python is the same as the OpenFst version
used. **The current version uses OpenFst 1.8.2.**

## Build Requirements

The build process will download and build OpenFst from the official
webpage, so you need an Internet connection and all OpenFst dependencies.
Essentially, you will need:

- A C++ compiler supporting C++17 (tested with GCC 12 on Debian 12 which python version >= 3.10).
- [Cython](https://cython.org/).
- [PatchELF](https://nixos.org/patchelf.html).
- [Zlib development](https://zlib.net/).
- [Python Requests](http://docs.python-requests.org).

## Installation

Most likely, you need to install deps. Then, simply install the
package from PyPI:

```bash
pip install absl-py requests cython==0.29.36
```

After that installing from sources, you can simply do:

```bash
python setup.py install
```

Notice that this downloads the appropriate version of OpenFst directly from
the Internet. If you don't have an Internet connection but are already in
possession of the appropriate tar.gz file, you can use the following command:

```bash
python setup.py build --download-dir=DIRECTORY_CONTAINING_OPENFST_TAR_GZ
python setup.py install
```
## Unit Test

```bash
python openfst_python/test.py
```

## Documentation

The Python API is the official one provided by OpenFst. Please, refer to its
[documentation](http://www.openfst.org/twiki/bin/view/FST/PythonExtension).

A toy example:

```python
import openfst_python as fst

f = fst.VectorFst()
s0 = f.add_state()
s1 = f.add_state()
s2 = f.add_state()
f.add_arc(s0, fst.Arc(1, 2, fst.Weight(f.weight_type(), 3.0), s1))
f.add_arc(s0, fst.Arc(1, 3, fst.Weight.one(f.weight_type()), s2))
f.add_arc(s1, fst.Arc(2, 1, fst.Weight(f.weight_type(), 1.0), s2))
f.set_start(s0)
f.set_final(s2, fst.Weight(f.weight_type(), 1.5))
```

## License

The OpenFst library is licensed under the Apache License, Version 2.0.
OpenFst-Python is just a wrapper of its official Python API, so
I am using the same license for most of the source code.
`ac_python_devel.m4` was not written by me and it is licensed under the
GPL license.
