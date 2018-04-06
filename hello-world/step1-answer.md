You need to run the following commands:

`echo "deb http://www.icub.org/ubuntu xenial contrib/science" > /etc/apt/sources.list.d/icub.list`{{execute}}

`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 57A5ACB6110576A6`{{execute}}

`apt-get update`{{execute}}

`apt-get install -y yarp`{{execute}}
