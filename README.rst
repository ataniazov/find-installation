==============================================
FIND 
==============================================

The Framework for Internal Navigation and Discovery (FIND) allows you to use your (Android) smartphone or WiFi-enabled computer (laptop or Raspberry Pi or etc.) to determine your position within your home or office. You can easily use this system in place of motion sensors as its resolution will allow your phone to distinguish whether you are in the living room, the kitchen or the bedroom, etc. The position information can then be used in a variety of ways including home automation, way-finding, or tracking!

==============================================
FIND installation  & configuration steps:
==============================================
::

    # apt-get update && apt-get upgrade

Docker
------
Install docker::

    # apt-get install docker.io

FIND Server
-----------
::

    # git clone https://github.com/schollz/find.git && cd find
    # docker build -t finddocker .
    # docker run --name find --restart=always -p 18003:8003 -p 11883:1883 -d -v $HOME/find/data:/data finddocker ./find -data /data
    # reboot
    
On your browser go to http://SERVER_IP:18003
Dashboard on http://SERVER_IP:18003/dashboard/YOUR_GROUP_NAME


./find -help
------
::

    find (version  (devdevde), built )
    Example: 'findserver yourserver.com'
    Example: 'findserver -p :8080 localhost:8080'
    Example (mosquitto): 'findserver -mqtt 127.0.0.1:1883 -mqttadmin admin -mqttadminpass somepass -mosquitto `pgrep mosquitto`
    Options:
        -crt string
            location of ssl crt
        -data string
            path to data folder
        -dump string
            group to dump to folder
        -filter string
            JSON file for macs to filter
        -key string
            location of ssl key
        -message string
            message to display to all users
        -mosquitto pgrep mosquitto
            mosquitto PID (pgrep mosquitto)
        -mqtt string
            ADDRESS:PORT of mosquitto server
        -mqttadmin string
            admin to read all messages
        -mqttadminpass string
            admin to read all messages
        -p string
            port to bind (default ":8003")
        -rf string
            port for random forests calculations
        -s string
            unix socket
            
Example of usage:
-----------------
::

    TO-DO

FIND Client (Raspberry Pi 2 Model B)
------------------------------------
::

    $ sudo raspi-config
    $ sudo apt-get update && apt-get upgrade
    $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    $ mkdir find
    $ cd find/
    $ wget https://github.com/schollz/find/releases/download/v0.5/findclient_0.5_linux_arm.zip
    $ unzip findclient_0.5_linux_arm.zip
    $ sudo ./findclient -s "SERVER_IP" -g YOUR_GROUP -u USER_NAME -l LOCATION_NAME -e
    $ sudo ./findclient -s "SERVER_IP" -g YOUR_GROUP -u USER_NAME -l LOCATION_NAME -e -c PACKETS_COUNT
    $ sudo ./findclient -s "SERVER_IP" -g YOUR_GROUP -u USER_NAME
    
./findclient --help
-------------------
::

    NAME:
        findclient - client for sending WiFi fingerprints to a FIND server
    
    USAGE:
        findclient [global options] command [command options] [arguments...]
       
    VERSION:
        0.5 a3d23a9
       
    COMMANDS:
        help, h  Shows a list of commands or help for one command
    
    GLOBAL OPTIONS:
        --server value, -s value     server to connect (default: "https://ml.internalpositioning.com")
        --group value, -g value      group name (default: "group")
        --user value, -u value       user name (default: "user")
        --location value, -l value   location (needed for '--learn') (default: "location")
        --continue value, -c value   number of times to run (default: 3)
        --learn, -e                  need to set if you want to learn location
        --nodebug, -d                turns off debugging
        --iwlist, -w                 switch to iwlist if iw fails
        --interface value, -i value  WiFi interface to use for scaning (default: "wlan0")
        --help, -h                   show help
        --version, -v                print the version
       
        2017/02/17 10:21:40 You can see fewer messages by adding --nodebug
        2017/02/17 10:21:40 User: 
        2017/02/17 10:21:40 Group: 
        2017/02/17 10:21:40 Server: 
        2017/02/17 10:21:40 Running 0 times (you can run more using '-c SOMENUM'). Please wait...
