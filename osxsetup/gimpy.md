# Using the Python of [GIMP](https://www.gimp.org) on Mac OS X

## Version: Native build `gimp-2.8.22-x86_64.dmg`
- Download from https://www.gimp.org/
- Drop the `GIMP.app`![wilber](https://www.gimp.org/images/wilber16.png)
  to `~/Applications`:file_folder:
- 2.8.22 is version matched to ubuntu:18.04 and debian:9
- :warning: gimp uses Python 2.7

## `GIMP.app` installation
- `~/Applications/GIMP.app/Contents/MacOS`
  - `GIMP-bin`: the executable
  - `GIMP`: a script to run GIMP-bin in a prepared shell environment
  - `python`: the executable
- Default `PYTHONHOME`
  - `~/Applications/GIMP.app/Contents/Resources/lib/python2.7/`
- `plug-ins` locations:
  - `~/Applications/GIMPa.pp/Contents/Resources/lib/gimp/2.0/`
  - `~/Library/Application Support/GIMP/2.8/`

## Using the Python of GIMP
- `cp ~/Applications/GIMP/Contents/MacOS/GIMP gimpy`
- Edit [`gimpy`](osxsetup/gimpy) to run python instead of gimp

## Install pip for the Python of GIMP
- Need `get-pip.py` from https://www.python.org
- Run `gimpy get-pip.py` to install executables to
  `~/Applications/GIMP.app/Contents/Resources/bin`
  - pip, pip2, pip2.7
  - easy_install, easy_install-2.7
  - wheel

## pip install other packages - examples
- `gimpy -m pip install ipython`
- `gimpy -m pip install numpy matplotlib`

## :warning: Python library modules missing by gimp dmg
- unittest
