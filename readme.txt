This project contains the static contents for the development documentation.

When deploying om IIS there needs to be a rewrite rule for this, for example:

name:               ARR_a9devdoc_8181_loadbalance
action:             Route to server farm
regex pattern:      ^A9devdoc(.+)
path:               /{R:0}


To check how it looks you can best run
> mkdocs serve

To deploy on the vaiz web application you have to execute the following steps

1.
-- build from th MarkDown files html files
> mkdocs build --clean

2.
-- build war from html file
> mvn clean install

3.
-- deploy the war (A9devdoc.war) on the vaizr webapplication machine

- host : 13.81.11.62
- name : EUJSF01  (Europe JS-Forms 01)

logon local

- username : EUJSF01/vaizradmin
- password : 123Schaats!

a. stop tomcat (location tomcat : C:\java\Tomcat 7.0), there is a shortcut on the desktop
b. remove webapps\vaizrA9devdoc.war
c. remove webapps\vaizrA9devdoc
d. copy   A9devdoc.war to webapps
e. rename A9devdoc.war to vaizrA9devdoc
f. start tomcat (location tomcat : C:\java\Tomcat 7.0), there is a shortcut on the desktop
g. check the outside url ( https://eu01.assainet.com/vaizrA9devdoc )

- you can go here from your remote desktop
- copy the A9devdoc.war to remote_machine/logs
-

You can run these scripts on windows and on unix to buld the whole devdocumentation

