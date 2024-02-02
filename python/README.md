# Rainbow All-Sky Imager Raw PGM Data Readfile (GO-Canada AGO/CGSM Rainbow)

[![Github Actions - Tests](https://github.com/ucalgary-aurora/rainbow-imager-readfile/workflows/tests/badge.svg)](https://github.com/ucalgary-aurora/rainbow-imager-readfile/actions?query=workflow%3Atests)
[![PyPI version](https://img.shields.io/pypi/v/rainbow-imager-readfile.svg)](https://pypi.python.org/pypi/rainbow-imager-readfile/)
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![PyPI Python versions](https://img.shields.io/pypi/pyversions/rainbow-imager-readfile.svg)](https://pypi.python.org/pypi/rainbow-imager-readfile/)

Python library for reading Rainbow All-Sky Imager (GO-Canada AGO/CGSM Rainbow) stream0 raw PGM-file data. The data can be found at https://data.phys.ucalgary.ca.

## Installation

The rainbow-imager-readfile library is available on PyPI:

```console
$ python3 -m pip install rainbow-imager-readfile
```

## Supported Python Versions

rainbow-imager-readfile officially supports Python 3.8+.

## Examples

Example Python notebooks can be found in the "examples" directory. Further, some examples can be found in the "Usage" section below.

## Usage

Import the library using `import rainbow_imager_readfile`

**Warning**: On Windows, be sure to put any `read` calls into a `main()` method. This is because we utilize the multiprocessing library and the method of forking processes in Windows requires it. Note that if you're using Jupyter or other IPython-based interfaces, this is not required.

### Read a single file

```python
>>> import rainbow_imager_readfile
>>> filename = "path/to/data/2015/01/01/fsmi_rainbow-11/ut06/20150101_0600_fsmi_rainbow-11_full.pgm.gz"
>>> img, meta, problematic_files = rainbow_imager_readfile.read(filename)
```

### Read multiple files

```python
>>> import rainbow_imager_readfile, glob
>>> file_list = glob.glob("path/to/files/2015/01/01/fsmi_rainbow-11/ut06/*full.pgm*")
>>> img, meta, problematic_files = rainbow_imager_readfile.read(file_list)
```

### Read using multiple worker processes

```python
>>> import rainbow_imager_readfile, glob
>>> file_list = glob.glob("path/to/files/2015/01/01/fsmi_rainbow-11/ut06/*full.pgm*")
>>> img, meta, problematic_files = rainbow_imager_readfile.read(file_list, workers=4)
```

### Read with no output

```python
>>> import rainbow_imager_readfile, glob
>>> file_list = glob.glob("path/to/files/2015/01/01/fsmi_rainbow-11/ut06/*full.pgm*")
>>> img, meta, problematic_files = rainbow_imager_readfile.read(file_list, workers=4, quiet=True)
```

### Read only the first frame of each file

```python
>>> import rainbow_imager_readfile, glob
>>> file_list = glob.glob("path/to/files/2015/01/01/fsmi_rainbow-11/ut06/*full.pgm*")
>>> img, meta, problematic_files = rainbow_imager_readfile.read(file_list, first_frame=True)
```

### Exclude reading the metadata

```python
>>> import rainbow_imager_readfile, glob
>>> file_list = glob.glob("path/to/files/2015/01/01/fsmi_rainbow-11/ut06/*full.pgm*")
>>> img, meta, problematic_files = rainbow_imager_readfile.read(file_list, no_metadata=True)
```

## Development

Clone the repository and install dependencies using Poetry.

```console
$ git clone https://github.com/ucalgary-aurora/rainbow-imager-readfile.git
$ cd rainbow-imager-readfile/python
$ make install
```

## Testing

```console
$ make test
[ or do each test separately ]
$ make test-flake8
$ make test-pylint
$ make test-pytest
```
