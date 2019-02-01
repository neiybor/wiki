<!-- TITLE: Mac Setup -->
<!-- SUBTITLE: Mac setup instructions -->

Download VirtualBox (https://www.virtualbox.org/wiki/Downloads)
Download Ubuntu image (Bionic Beaver - 18.04): https://www.osboxes.org/ubuntu
Create neighbor folder
```
mkdir neighbor
cd neighbor
```
Clone config-management repo
`git clone git@github.com:neiybor/config-management.git`
Run dev setup script
```
# this will clone the other repos and set up your
# environment. Type ‘Y’ when it asks. You will need AWS
# credentials (access key id, secret access key) for
# when it asks.

./config-management/setup-dev.sh
```
Start servers
```
cd rails-api
rails s -p 3001

cd ../react-frontend
yarn start
```
Edit Mac hosts file to access https://nbr.pizza.
Run ‘ifconfig’ in VM terminal to get inet address as shown below:
Add the following line to Mac hosts file (located at /etc/hosts): 
```
# replace the inet address below with the one obtained 
# when you ran ifconfig

192.168.0.115 nbr.pizza
```
Verify by visiting https://nbr.pizza in your browser.

Create Local Network Share
In your Files explorer, right click the neighbor folder and click Properties 
Click the Local Network Share tab and copy the settings below (the share name will default to whatever you named your folder, probably ‘neighbor.’ Click the Create Share button.
Click on the Permissions tab and copy the settings below (leave the Group name as the default, just change the Access setting for Owner, Group and Others to ‘Create and delete files.’

Access the shared folder from the host (Mac)
To access the folder from Finder, navigate to Network (under Locations) and click on your VM. From here you will see the shared folder you created. 
To access the folder from Terminal:
```
# replace YOUR_SHARED_FILE_NAME with... you guessed it.
# it should be neighbor

cd /Volumes/YOUR_SHARED_FILE_NAME/
```