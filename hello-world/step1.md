In this step you will install YARP

Add robotology repository:
`echo "deb http://www.icub.org/ubuntu xenial contrib/science" > /etc/apt/sources.list.d/icub.list`{{execute T1}}

Add robotology GPG key:
`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 57A5ACB6110576A6`{{execute T1}}

Update apt repository list:
`apt-get update`{{execute T1}}

Install yarp:
`apt-get install -y yarp`{{execute T1}}

Check yarp installed version:
`yarp version`{{execute T1}}

Check yarp installed version:
`yarp check`{{execute T1}}
