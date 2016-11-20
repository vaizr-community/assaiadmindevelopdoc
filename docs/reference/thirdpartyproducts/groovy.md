# Groovy

## Usage of groovy

During the build with maven and all the groovy inside the AssaiDCMS project is taken care of maven and your IDE (NetBeans). All the groovy code inside the AssaiDCMS resides in the following directory ``<your workspace>\AssaiDCMS\src\main\groovy``However if you want to make use of the groovy generators. You have to run groovy from the command line. An example of using groovy from the command line is given in [Tutorial 2 : Create a master detail]( /tutorial/master_detail )

## Installation

You can download the groovy installation for windows [here](https://dl.bintray.com/groovy/Distributions/groovy-2.4.6-installer.exe). If this link does not work you should check [http://www.groovy-lang.org/download.html](http://www.groovy-lang.org/download.html)

After the installation you probably have to modify the GROOVY_HOME in your environment settings.

﻿Control Panel => System and Security => System => Advanded system settings => Environment Variables ...

Change the setting to the actual place where it is installed. for example

    GROOVY_HOME = C:\tools\Groovy\GROOVY~6 ==> ﻿C:\tools\Groovy\GROOVY-2.4.6

## Verify Groovy

    C:\workspaces>groovy -v
    Groovy Version: 2.4.6 JVM: 1.8.0_77 Vendor: Oracle Corporation OS: Windows 7

