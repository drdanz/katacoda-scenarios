In this step you will install YARP

`echo "deb http://www.icub.org/ubuntu xenial contrib/science" > /etc/apt/sources.list.d/icub.list`{{execute}}

`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 57A5ACB6110576A6`{{execute}}

`apt-get update`{{execute}}

`apt-get install -y yarp`{{execute}}

`yarp version`{{execute}}

---

For multiple terminals, execute the command on T1 `some-command`{{execute T1}}

For multiple terminals, execute the command on T2 `some-command`{{execute T2}}
