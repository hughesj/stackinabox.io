# Welcome to **stackinabox.io**

## Introduction

This vagrant project will stand up a single Ubuntu 14.04 running OpenStack Liberty and Docker using Virtualbox. It will pull Docker images for [UrbanCode Deploy](https://hub.docker.com/r/stackinabox/urbancode-deploy/), [UrbanCode Deploy Agent](https://hub.docker.com/r/stackinabox/urbancode-deploy-agent/), [UrbanCode Patterns Blueprint Designer](https://hub.docker.com/r/stackinabox/urbancode-patterns-designer/), and [UrbanCode Patterns Engine](https://hub.docker.com/r/stackinabox/urbancode-patterns-engine/).  Using this vagrant image, once running using vagrant up, you'll be able to design and develop OpenStack HEAT based cloud automation that you can use to deploy applications to the embedded [OpenStack](https://www.blueboxcloud.com/) or to any other cloud provider supported by [UrbanCode Deploy's Blueprint Designer](https://developer.ibm.com/urbancode/products/urbancode-deploy/features/blueprint-designer/) ([Amazon Web Services](https://aws.amazon.com/), [Softlayer](http://www.softlayer.com/), [Azure](https://azure.microsoft.com/), or even your on-prem [VMware vCenter](https://www.vmware.com/products/vcenter-server)).

Using this vagrant environment, it is hoped that you will share the automation that you develop to deploy applications to the cloud with the larger community.  For an example check out  [JKE Banking Application](https://github.com/stackinabox/jke)

## Future Integrations

It's planned to add further Docker images to this vagrant setup to support many other deployment automation tools such as:  

  - [Chef Server](https://www.chef.io/chef/) (not yet implemented)
  - [Salt Stack](https://saltstack.com/) (not yet implemented)
  - [Puppet](https://puppet.com/) (not yet implemented)

### Set Up Instructions

#### Prerequisites  

  ##### Download and Install locally:  

  - [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)  
  - [Vagrant](https://www.vagrantup.com/downloads.html)  
  - [Git](https://git-scm.com/) 

  ##### Install required Vagrant plugins:  

````
    # install a few required vagrant plugins
    vagrant plugin install vagrant-docker-compose
    vagrant plugin install vagrant-multi-hostsupdater
````

  ##### Launch the OPDK ( pronounced o-pee-doo-kee ) i.e. Open Patterns Development Kit   

````
    # stand up the OpenStack and UrbanCode environment
	$: git clone https://github.com/stackinabox/stackinabox.io.git 
	$: cd stackinabox.io
	$: vagrant up
	....
	==> opdk: Creating ucddb
	==> opdk: Creating heatengine
	==> opdk: Creating blueprintdb
	==> opdk: Creating ucd
	==> opdk: Creating blueprintdesigner
	==> opdk: Creating agent
	==> opdk: Creating agent-relay
	....

	# the "vagrant up" command will take a while to complete.  It will download the opdk.box Virtual Box vm image. Once downloaded it will launch the vm in Virtual Box in "Headless" mode (no gui).  To learn how to halt the vm or destroy and recreate the vm see below.
````

After executing the above you can open your local web browser to the [Blueprint Designer](http://designer.stackinabox.io:9080/) landscaper and login with demo/labstack.  The demo user is intended to be the user primarily used for building your automation.  The demo user belongs to a 'demo' team in the Blueprint Designer and has it's own tenant in the embedded [BlueBox](http://bluebox.stackinabox.io) that will be used to run any automation provisioned through the Blueprint Designer on the BlueBox server when logged in as the demo user.  Additional user login information is provided below, under the **Access Information** section, to gain access to the administration views for both the Blueprint Designer as well as for the BlueBox OpenStack Mitaka server.

#### Install the example automated deployment application and assets   

   -- Open your browser to the include ["web terminal"](http://192.168.27.100:4200/)

````
    $openstack login: vagrant
    $password: vagrant

	# import the example JKE Banking Application automation
	$: git clone https://github.com/stackinabox/jke.git /vagrant/patterns/jke
	$: cd jke
	$: ./init.sh
    ....
    $: open your browser to the [JKE Tutorial](http://designer.stackinabox.io:9080/landscaper/view/tutorial)
````

If you have never used UrbanCode Deploy or the UrbanCode Blueprint Designer before you can open your browser to the url that is displated at the end of the JKE Banking Application's init.sh script you ran above [JKE Tutorial](http://192.168.27.100:9080/landscaper/view/tutorial) and login as demo/labstack user.  You will see a "guided tour" frame on the right side of your browser window.  Just follow the instructions and it will guide you through how to deploy the JKE Banking Application using UrbanCode Deploy and UrbanCode Blueprint Designer onto the embedded [BlueBox](http://openstack.stackinabox.io).

#### Halt the running environment without loosing any data/work  

     -- from your host machine open a terminal and run the following:

````
    # navigate to where you cloned the stackinabox.io repo
	$: cd /path/to/stackinabox.io/repo

	# halt the running vagrant environment without loosing any data
	$: vagrant halt
````

#### Resume the running environment with all previous data/work restored  

````
    # navigate to where you cloned the stackinabox.io repo
	$: cd /path/to/stackinabox.io/repo

	# resume the running vagrant environment with all previous data/work restored
	# relies on having previously run 'vagrant halt'
	$: vagrant up
````

#### Destroy vagrant environment and restart from begining (will loose all existing data/work)  

````
    # navigate to where you cloned the stackinabox.io repo
	$: cd /path/to/stackinabox.io/repo
	
	# destroy existing enviornment and restart from scratch (will loose any existing data/work)
	$: vagrant destroy
	$: vagrant up
````

#### Connect UrbanCode Blueprint Designer to Amazon's AWS

   -- Open your browser to the include ["web terminal"](http://192.168.27.100:4200/)

````
    $openstack login: vagrant
    $password: vagrant

    # once logged in run the aws setup script
	$: ~/aws-setup.sh

	# follow the instructions printed at the end of the script execution
````

#### Access Information

 - OpenStack i.e. [BlueBox](http://openstack.stackinabox.io)
	 - available at http://openstack.stackinabox.io 
		 - username: demo
		 - password: labstack  
		 _____________________  
		 - username: admin
		 - password: labstack
	 
 - [UrbanCode Deploy Server](http://ucd.stackinabox.io:8080)
	 - available at http://ucd.stackinabox.io:8080
		 - username: admin
		 - password: admin
		 
 - UrbanCode Deploy Agent
	 - importagent (default worker for importing deployment artifacts into UrbanCode Deploy)
	 
 - UrbanCode Deploy heat Engine
	 - running at http://heat.stackinabox.io:8004
	 
 - [UrbanCode Deploy Blueprint Designer](http://designer.stackinabox.io:9080/landscaper) (HEAT Designer)
	 - available at http://designer.stackinabox.io:9080/landscaper
	     - username: demo
	     - password: labstack  
	     _____________________  
		 - username: ucdpadmin
		 - password: ucdpadmin

		 
