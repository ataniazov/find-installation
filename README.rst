# find-installation
find-installation
==============================================
SonarQube installation  & configuration steps:
==============================================
::

    # apt-get update && apt-get upgrade

PostgreSQL
----------
Install PostgreSQL & adding the JDBC driver::

    # apt-get install postgresql libpostgresql-jdbc-java

Add "sonar" database and "sonar" user with "sonar" password::

    $ sudo -u postgres psql
    postgres=# CREATE USER sonar WITH PASSWORD 'sonar';
    postgres=# \du
    postgres=# CREATE DATABASE sonar WITH OWNER sonar encoding 'UTF8';
    postgres=# GRANT ALL PRIVILEGES ON DATABASE sonar TO sonar;
    postgres=# \l
    postgres=# \q

Java (JRE & JVM)
----------------
::

    # apt-get install openjdk-8-jre-headless 

SonarQube Server
----------------
::

    $ wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-5.6.4.zip
    # apt-get install unzip
    $ unzip sonarqube-5.6.4.zip
    # mv sonarqube-5.6.4/ /opt/sonar/


Create the file /etc/init.d/sonar with this content::

    #!/bin/sh
    #
    # rc file for SonarQube
    #
    # chkconfig: 345 96 10
    # description: SonarQube system (www.sonarsource.org)
    #
    ### BEGIN INIT INFO
    # Provides: sonar
    # Required-Start: $network
    # Required-Stop: $network
    # Default-Start: 3 4 5
    # Default-Stop: 0 1 2 6
    # Short-Description: SonarQube system (www.sonarsource.org)
    # Description: SonarQube system (www.sonarsource.org)
    ### END INIT INFO
 
    /usr/bin/sonar $*

Register SonarQube at boot time (Ubuntu, 64 bit)::

    # ln -s /opt/sonar/bin/linux-x86-64/sonar.sh /usr/bin/sonar
    # chmod 755 /etc/init.d/sonar
    # update-rc.d sonar defaults
Setting the access to the Database::

    # vi /opt/sonar/conf/sonar.properties
    sonar.jdbc.username=sonar
    sonar.jdbc.password=sonar
    sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
Starting the Web Server::

    sonar.web.host=0.0.0.0
    sonar.web.port=80
    sonar.web.javaOpts=-server
::

    # reboot

On your browser go to http://<server-ip>:9000
Default login: 	admin
Default passwd: admin

AthenaPDF
---------
::

    # apt-get install docker.io
    # docker pull arachnysdocker/athenapdf-service
    # docker run --name athenapdf --restart=always -p 8080:8080 -d --env-file=athenapdf.env arachnysdocker/athenapdf-service

athenapdf
---------
::

    Usage: athenapdf [options] <URI> [output]
    convert HTML to PDF via stdin or a local / remote URI
    Options:

    -h, --help                   output usage information
    -V, --version                output the version number
    --debug                      show GUI
    -T, --timeout <seconds>      seconds before timing out (default: 120)
    -D, --delay <milliseconds>   milliseconds delay before saving (default: 200)
    -\P, --pagesize <size>        page size of the generated PDF (default: A4)
    -M, --margins <marginsType>  margins to use when generating the PDF (default: standard)
    -Z --zoom <factor>           zoom factor for higher scale rendering (default: 1 - represents 100%)
    -S, --stdout                 write conversion to stdout
    -A, --aggressive             aggressive mode / runs dom-distiller
    -B, --bypass                 bypasses paywalls on digital publications (experimental feature)
    --proxy <url>                use proxy to load remote HTML
    --no-portrait                render in landscape
    --no-background              omit CSS backgrounds
    --no-cache                   disables caching

Example of usage:
-----------------
::

    http://<docker-address>:8080/convert?auth=arachnys-weaver&url=http://blog.arachnys.com/
    $ curl http://dockerhost:8080/convert\?auth\=arachnys-weaver\&url\=http://blog.arachnys.com/ |> out.pdf


============================================
Analyzing with SonarQube Scanner for Jenkins
============================================
