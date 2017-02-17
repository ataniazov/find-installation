==============================================
FIND installation  & configuration steps:
==============================================
::

    # apt-get update && apt-get upgrade

Docker
----------
Install docker::

    # apt-get install docker.io

FIND Server
----------------
::

    # git clone https://github.com/schollz/find.git && cd find
    # docker build -t finddocker .
    # docker run --name find --restart=always -p 18003:8003 -p 11883:1883 -d -v /root/find/data:/data finddocker ./find -data /data
    # reboot
    
On your browser go to http://SERVER_IP:18003
Dashboard on http://SERVER_IP:18003/dashboard/YOUR_GROUP_NAME


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
