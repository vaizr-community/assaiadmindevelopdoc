# Python

## Usage of python

For now python is only used to create and maintain the development documentation. The development documenation is created with MKDocs and MKDocs relies on python. We are currently using **python 2**.

Together with python you install **pip. pip** is a package management system used to install and manage software packages written in Python.

## Installation

You can download the python 2 installation for windows [here](https://www.python.org/ftp/python/2.7.11/python-2.7.11.amd64.msi). If this link does not work you should check [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)

After the installation you probably have to add the PYTHON_HOME in your environment settings.

﻿Control Panel => System and Security => System => Advanded system settings => Environment Varaibles ...

Add the system environment setting to the actual place where it is installed. for example

    PYTHON_HOME = ﻿C:\tools\Python27

And you have to add **two** extensions to the Path system environment setting ``%PYTHON_HOME%`` and ``%PYTHON_HOME%\Scripts ``

    Path = ...;%PYTHON_HOME%;%PYTHON_HOME%\Scripts

### Verify Python

    C:\workspaces>python --version
    Python 2.7.11

### Verify pip

    C:\workspaces>pip --version
    pip 8.1.1 from c:\tools\python27\lib\site-packages (python 2.7)

Probably you have to ugrade pip. This can be done by the following command

    C:\workspaces>pip install pip --upgrade

