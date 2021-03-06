<p align="left">
  <a href="#">
    <img 
      alt="dicom-populate-python-script-logo" 
      src="https://raw.githubusercontent.com/natanaelfneto/dicompopulate/master/assets/dp-logo.png" 
      width="240" />
  </a>
</p>

**DICOM Populate** is small code to send folders of dicom files to as many desired PACS server receivers as possible\
Version: **0.5**
***
# Table of Contents
* [Getting Started](#getting-started)
    * [Installation process](#installation-process)
    * [Dependencies](#dependencies)
    * [Usage](#usage)
    * [TODO](#TODO)
* [License](#license)
***
## Getting Started
### Via Bash
#### Installation Process
* Via pip\
_still not available in Pypi repository_
```Shell
pip install git+https://github.com/natanaelfneto/dicompopulate.git
```
* Via Git\
Clone or download the repository at:
```Shell
git clone https://github.com/natanaelfneto/dicompopulate.git
cd dicompopulate
python setup.py install
```
_enjoy_
***
### Dependencies
- pydicom
- pynetdicom
## TODO
* add _'localhost'_, _'pacs.example.com'_, names support insted or just pure IP Addresses
* fully migrate to python 3 standards
* make C-STORE better by stop closing conections and reopening for each dicom file sent [not yet sure how]
* check if file was save on destination conection (probably with C-FIND)
* check for valid TCP/IP:PORT listen before a C-ECHO attempt
* manage to save (proably with a simple sqlite database or other) wich files were already sent to avoid duplicate attempts on a re-run
* run script for a local and remote origin and local and remote destiny (only availabe so far from local origin to local and remote destiny)
* make available a test script for sending and receiving dicom files on python sender to python receiver, python sender and non-python receiver
## Usage
This messagem can also be found with **python populate.py -h** command
```ShellSession
usage: populate.py [-h] -p PATHS [PATHS ...] -c CONECTIONS [CONECTIONS ...]  [-d] [-v] [-w] [--verbose]

a script to populate a PACS with folder of DICOM files

optional arguments:

-h, --help                                  show this help message and exit

-p PATHS [PATHS ...], 
--paths PATHS [PATHS ...]                   array of dicom folders or files paths

-c CONECTIONS [CONECTIONS ...],
--conections CONECTIONS [CONECTIONS ...]    array of conection parameters for dicom 
                                            receivers (Application Entities)

-d, --debug                                 set debug flag (it only shows debug
                                            information and can be combined with the 
                                            verbose flag for a more robust output and log)

-v, --version                               output software version

-w, --max_workers                           set the maximum number of parallel
                                            processes allowed for C-STORE threads
                                            (default value is 10)

--verbose                                   set verbose flag to enhence output info
                                            (it only shows output information and can
                                            be combined with debug flag for a more
                                            robust output and log)
```
## Examples
### As terminal command
To run it as command:
```Shell
python populate.py --paths /PACS/1/ /PACS/2/ /PACS/3/dicom.dcm --conections DCM4CHEE@10.0.0.1:11112 OTHER@127.0.0.1:5555
```
### As python module
To use it as module follow the exemple, also available in populate/examples/exemple1.py
```Python
from populate import populate

# get all files and paths to send
path_1 = '/PACS/1/'
path_2 = '/PACS/2/'
path_3 = '/PACS/3/dicom.dcm'

# get all desired conections to receive
c_1 = 'DCM4CHEE@10.0.0.1:11112'
c_2 = 'OTHER@127.0.0.1:5555'

# populate
populate.run(
  # debug=True,
  # verbose=True,
  # max_workers=10,
  path=[ path_1, path_2, path_3 ],
  conections=[ c_1, c_2 ]
)

# debug, verbose and max_workers values are optional
```
## License
MIT License

Copyright (c) 2017 Natanael F. Neto (natanaelfneto)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.