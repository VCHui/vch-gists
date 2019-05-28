# Using Python on Max OS X

## A typical system

* Yosemite (Mac OS X 10.0) and above

* Python is a framework
  - Lib location: `/System/Library/Frameworks/Python.framework/Versions/2.7`
  - `/usr/lib/python2.7` is symlinked to `...framework/Versions/2.7/lib`
  - Third party packages, e.g. Xcode, go to `...framework/Versions/2.7/Extras`

* User environment based on the Mac OS X host
  - Location: `${HOME}/Library/Python/2.7`
  - :warning: `${HOME}/Library/Python/2.7/bin` is __NOT__ on
    `${PATH}` by default
    - Require manual update to `~/.bash_profile`

## Aims

* The host based Python is the default

* Multiple user virtual environments based on the host
  - Override the default only when activated
  - Locations of the environments to go, e.g.
    - `${HOME}/opt/venv0`
    - `${HOME}/opt/venv1`
    - ...
  - `rm -rf ~/opt/venv0` to remove an installation

* A miniconda3 base setup
  - Location: `${HOME}/opt/miniconda3`

* Multiple conda environments based on the miniconda3
  - Locations of the environments to go, e.g.
    - `${HOME}/opt/miniconda3/env/2.7`
    - `${HOME}/opt/miniconda3/env/pytorch`
    - `${HOME}/opt/miniconda3/env/tensorflow`
    - ...
  - `conda remove --name 2.7 --all` to remove an environment

* `rm -rf ~/opt/miniconda3` to remove the miniconda3
  installation completely

* `rm -rf ~/opt` to remove all the installations


## Checkups

* How many Python installations on the system?
  ```shell
  find / -path "bin/python*" 2> /dev/null
  ```
* Check if the Python installations are accessible?
  ```shell
  echo $PATH
  ```
* Which python is default?
  ```shell
  which python
  ```

## Using the Python of the host installation

* `pip`

  - Installation
    ```shell
    easy_install --user pip
    ```

  - The installation places `pip` in `${HOME}/Library/Python/2.7/bin`

  - Make `pip` searchable on `${PATH}`
    ```shell
    which pip || ( echo "export PATH=${HOME}/Library/Python/2.7/bin:${PATH}" >> ~/.bash_profile )
    ```

  - Verify installation in a new shell
    ```shell
    which pip
    ```

  - List all locally installed packages
    ```shell
    pip list
    ```
    - :bulb: Some packages are installed by Xcode


* `virtualenv`

  - Installation
    ```shell
    pip install --user virtualenv
    ```

  - Verify installation
    ```shell
    which virtualenv
    ```

* Setup a separate python installation based on the host installation

  - Create a separate environment, in `~/opt/venv0`, for instance
    ```shell
    virtualenv ~/opt/venv0
    ```

  - Activate the environment
    ```shell
    source ~/opt/venv0/bin/activate
    ```
    - :bulb: `python` and `pip` are found on `~/opt/venv0/bin`
    - :bulb: `pip install` will put the package in
      `~/opt/venv0/lib/python2.7/site-packages`

  - Deactivate the environment
    ```shell
    deactivate
    ```
    - :bulb: `python` and `pip` are back to their defaults

  - Remove the environment completely
    ```shell
    rm -rf ~/opt/venv0
    ```

## Using Miniconda3

* Installation (Download: https://docs.conda.io/en/latest/miniconda.html)
  ```shell
  bash ~/Downloads/Miniconda3-latest-MacOSX-x86_64.sh -b -p ~/opt/miniconda3
  ```

* Activate the Conda environment to verify
  ```shell
  source ~/opt/miniconda3/bin/activate
  ```
  - :bulb: `python` and `pip` are found on `~/opt/miniconda3/bin`
  - :bulb: `pip install` will put the package in
    `~/opt/miniconda3/lib/python3.7/site-packages`

* :warning: TAB completion does not work!


### Setup a python2.7 environment based on miniconda3

- Create the environment
  ```shell
  conda create --name 2.7 python=2.7
  ```

- Activate the environment
  ```shell
  conda activate 2.7
  ```
  - :bulb: `python` and `pip` are found on `~/opt/miniconda3/envs/2.7/bin`
  - :bulb: `pip install` will put the package in
    `~/opt/miniconda3/envs/2.7/lib/python2.7/site-packages`

- Deactivate the environment
  ```shell
  conda deactivate
  ```

- Remove the environment
  ```shell
  conda remove --name 2.7 --all
  ```

* List all environments
  ```shell
  conda env list
  ```


## Using jupyter

* List kernels
  ```shell
  jupyter kernelspec list
  ```

* Install a kernel for any python environment
  ```shell
  pip install ipykernel
  python -m ipykernel install --user --name venv2.7 --display-name "venv2.7"
  ```
