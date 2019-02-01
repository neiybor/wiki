<!-- TITLE: Mac Setup -->
<!-- SUBTITLE: Mac setup instructions -->

1. Download VirtualBox (https://www.virtualbox.org/wiki/Downloads)
1. Download Ubuntu image (Bionic Beaver - 18.04): https://www.osboxes.org/ubuntu
1. Create neighbor folder
	```
	mkdir neighbor
	cd neighbor
	```
1. Clone config-management repo
1. `git clone git@github.com:neiybor/config-management.git`
	Run dev setup script
	```
	# this will clone the other repos and set up your
	# environment. Type ‘Y’ when it asks. You will need AWS
	# credentials (access key id, secret access key) for
	# when it asks.
	
	./config-management/setup-dev.sh
	```
1. Start servers
	```
	cd rails-api
	rails s -p 3001
	
	cd ../react-frontend
	yarn start
	```
1. Edit Mac hosts file to access https://nbr.pizza.
1. Run ‘ifconfig’ in VM terminal to get inet address as shown below:
1. Add the following line to Mac hosts file (located at /etc/hosts): 
	```
	# replace the inet address below with the one obtained 
	# when you ran ifconfig
	
	192.168.0.115 nbr.pizza
	```
1. Verify by visiting https://nbr.pizza in your browser.

1. Create Local Network Share
1. In your Files explorer, right click the neighbor folder and click Properties 
1. Click the Local Network Share tab and copy the settings below (the share name will default to whatever you named your folder, probably ‘neighbor.’ Click the Create Share button.
1. Click on the Permissions tab and copy the settings below (leave the Group name as the default, just change the Access setting for Owner, Group and Others to ‘Create and delete files.’

1. Access the shared folder from the host (Mac)
1. To access the folder from Finder, navigate to Network (under Locations) and click on your VM. From here you will see the shared folder you created. 
1. To access the folder from Terminal:
	```
	# replace YOUR_SHARED_FILE_NAME with... you guessed it.
	# it should be neighbor
	
	cd /Volumes/YOUR_SHARED_FILE_NAME/
	```