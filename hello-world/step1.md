In this step you will install YARP

Add robotology repository:
`echo "deb http://www.icub.org/ubuntu xenial contrib/science" > /etc/apt/sources.list.d/icub.list`{{execute}}

Add robotology GPG key:
`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 57A5ACB6110576A6`{{execute}}

Update apt repository list:
`apt update`{{execute}}

Install yarp:
`apt install -y yarp`{{execute}}

Check yarp installed version:
`yarp version`{{execute}}

---

For multiple terminals, execute the command on T1 `some-command`{{execute T1}}

For multiple terminals, execute the command on T2 `some-command`{{execute T2}}
