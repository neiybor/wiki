<!-- TITLE: Dev Setup -->
<!-- SUBTITLE: Setting up dev environments -->

# Dev Setup
1. Setup BIOS and OS
	1. Plug into Ethernet / connect wifi
	1. Install Windows and login
	1. Plugin the flash drive with Ubuntu
	1. Go to https://forums.lenovo.com/t5/ThinkPad-P-and-W-Series-Mobile/Thinkpad-P50-can-no-longer-get-into-BIOS-from-boot-screen-using/td-p/3498366 and follow the 9 steps to get into the right BIOS
	1. Update BIOS
		1. Security -> Secure Boot
			1. Set to Disabled
		1. Startup -> Boot
			1. Move USB HDD... to top of boot order
		1. Graphics
			1. Change Hybrid to Discrete graphics
		1. Save and exit
	1. Install Ubuntu
		1. Select “Download updates while installing” and “install 3rd party…” options and press continue
		1. Erase disk and install Ubuntu and select the “Encrypt” and “LVM” options. Press continue.
		1. Enter a security key -- note put it in lastpass -- you will be prompted to enter this key every time you login and there is NO RECOVERY
		1. On “Erase disk & install ubuntu” screen select the SSD drive
		1. On “Write changes to disk” prompt select Continue
		1. “Who are you?” page
			1. Computer name: email prefix (email part before @)
			1. Username: email prefix (email part before @)
			1. Require password on login
			1. Do NOT encrypt home folder (entire disk already encrypted)
		1. Remove the USB drive when installation is complete and press restart
		1. If it hangs saying “Assuming drive cache: write through” on reset, Hard reset computer
	1. Install chrome
		1. Download .deb file - select Save
		1. Open folder viewer and double click deb file to install
		1. Install lastpass addon
		1. Get access to repos
		1. Neiybor Github account
		1. Setup your AWS account
			1. For the admin adding the new hire: make sure the new hire is added to the ‘engineers’ group
			1. Hint: Minimum password length is 16 chars
			1. Make the user an access key
			1. Send them “You will need the following to setup the AWS CLI while the setup-dev script runs”
			1. Send them the key and secret
			1. Send them “default region: us-east-1”
			1. Send them “skip default output format”
1. Get & run setup script (recommended)
	1. Replace RED VALUES with your info
	```
	#install git
	sudo apt update
	sudo apt upgrade
	sudo apt install git
	# configure git
	git config --global color.ui true
	git config --global user.name "FIRSTNAME LASTNAME"
	git config --global user.email "YOUR@EMAIL.com"
	ssh-keygen -t rsa -b 4096 -C "YOUR@EMAIL.com" #use default file location on prompt
	```
	2. Upload ssh key just generated to your github account
		1. Go to https://github.com/settings/keys
		1. Run command: gedit ~/.ssh/id_rsa.pub
		1. Copy entire text and paste into new key form
	1. Download config-management repo
	```
	# download repo
	mkdir ~/neighbor
	cd ~/neighbor
	git clone git@github.com:neiybor/config-management.git
	
	# run setup script
	./config-management/setup-dev.sh
	```
	4. The script above changes the .profile file (needed for localstack) so
		1. log out of Ubuntu and
		1. log back in
	1. Optional steps for ops members (skip to next step)
		1. AWS Codecommit (instructions)
			1. Easiest to start w/ HTTPS access by generating a username/password
			1. Save the username/password in lastpass
			1. Use when prompted for “ops” repo in setup script
		1. Instructions on setting up a cert
			1. Create self-signed cert
	```
	cd ~
	mkdir .ssl
	cd .ssl
	
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout neiybor.local.key -out neiybor.local.crt
		<follow prompts
		Common Name (e.g. server FQDN or YOUR name) []:neiybor.local

	echo "127.0.0.1    neiybor.local" | sudo tee /etc/hosts
```
Follow instructions here:
https://www.digitalocean.com/community/tutorials/how-to-implement-ssl-termination-with-haproxy-on-ubuntu-14-04
Run app
Try logging in to DB


psql -U dev neiybor_api_dev
# password: dev


cd rails-api
Start server on port 3001:
rails s -p 3001


Open browser to http://nbr.pizza:3001
Verify you get a valid JSON response http://nbr.pizza:3001
cd react-frontend
Start the node server with HTTPS and the correct hostname by running:
yarn start
Browser should open to https://nbr.pizza/
Install tools
Install favorite editor
VS Code - sudo snap install vscode --classic


sudo snap install vscode --classic
Install Debugger for Chrome extension
Follow setup instructions on extension page
Install React Dev Tools for Chrome
Chrome extension to block Google Analytics
Add *.neighbor.com and neighbor.com to the list of blocked sites
Another good alternative: Ghostery https://chrome.google.com/webstore/detail/ghostery/mlomiejdfkolichcflejclcbmpeaniij?hl=en


More setup
Install Heroku CLI (google how to do it) and run heroku plugins:install heroku-config
Setup default git editor to be VSCode, Emacs, VI, Gedit, …
git config --global core.editor "code"
Tutorials
JavaScript/ES6
Typescript
5 Minute Intro
Ruby/Rails
React
Quick start guide
Redux
TypeScript React Starter
Optional setup
Lastpass extension
Always launch Chrome listening on a debug port


google-chrome --remote-debugging-port=9222
Google Tag Assistant Chrome extension
Setup for Android development
sudo apt install default-jdk
Enable KVM in BIOS for hardware accelerated virtualization
Security -> Virtualization
Enable both Virtualization Technology and Vt-d Feature
Install Android Studio
Open SDK Manager
Install Android SDK versions 25 and above
Walk through tutorial of creating your first Android app
After creating app go to the “Run your app” -> “Run on an emulator” step of the tutorial
If you get an error about syncing gradle files click “Try Again”
When creating a device
Install Gradle
https://gradle.org/next-steps/?version=4.9&format=bin


cd ~/Downloads/
sudo mkdir /opt/gradle
sudo unzip -d /opt/gradle gradle-4.9-bin.zip
ls /opt/gradle/gradle-4.9



Add following to .bashrc (replacing <user> with your username)
export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
export ANDROID_HOME="/home/<user>/Android/Sdk"
export PATH="${PATH}:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin"
export PATH=$PATH:/opt/gradle/gradle-4.9/bin

source .bashrc
Remove old Android SDK debugger IF it exists
sudo rm /usr/bin/adb
Install Cordova
sudo npm install -g cordova
cd ~/neiybor/transmogrifier
cordova platform add android
Build staging app
cordova build
Install apk on emlulator (i.e. after emulator started by Android Studio or command line)
adb -s emulator-5554 install -r ~/neiybor/transmogrifier/platforms/android/app/build/outputs/apk/debug/app-debug.apk
Build staging app for release to Play Store for testing
cordova build --release --buildConfig=build.json
V1 Android setup
sudo apt install default-jdk
Remove old SDK
sudo rm /usr/bin/adb
Enable CPU virtualization in BIOS
P51 - enable both virtualization settings
Install Android Studio
Install Android studio into standard ~/Android/Sdk
Install Gradle
https://gradle.org/next-steps/?version=4.9&format=bin


cd ~/Downloads/
Sudo mkdir /opt/gradle
Sudo unzip -d /opt/gradle gradle-4.9-bin.zip
ls /opt/gradle/gradle-4.9



Add following to .bashrc


export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
export ANDROID_HOME="~/Android/Sdk"
export PATH="${PATH}:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin"
export PATH=$PATH:/opt/gradle/gradle-4.9/bin


Mac

Download VirtualBox (https://www.virtualbox.org/wiki/Downloads)
Download Ubuntu image (Bionic Beaver - 18.04): https://www.osboxes.org/ubuntu
Create neighbor folder

mkdir neighbor
cd neighbor

Clone config-management repo

git clone git@github.com:neiybor/config-management.git

Run dev setup script

# this will clone the other repos and set up your
# environment. Type ‘Y’ when it asks. You will need AWS
# credentials (access key id, secret access key) for
# when it asks.

./config-management/setup-dev.sh

Start servers

cd rails-api
rails s -p 3001

cd ../react-frontend
yarn start


Edit Mac hosts file to access https://nbr.pizza.
Run ‘ifconfig’ in VM terminal to get inet address as shown below:


Add the following line to Mac hosts file (located at /etc/hosts): 

# replace the inet address below with the one obtained 
# when you ran ifconfig

192.168.0.115 nbr.pizza

Verify by visiting https://nbr.pizza in your browser.

Create Local Network Share
In your Files explorer, right click the neighbor folder and click Properties 
Click the Local Network Share tab and copy the settings below (the share name will default to whatever you named your folder, probably ‘neighbor.’ Click the Create Share button.
Click on the Permissions tab and copy the settings below (leave the Group name as the default, just change the Access setting for Owner, Group and Others to ‘Create and delete files.’

Access the shared folder from the host (Mac)
To access the folder from Finder, navigate to Network (under Locations) and click on your VM. From here you will see the shared folder you created. 
To access the folder from Terminal:

# replace YOUR_SHARED_FILE_NAME with... you guessed it.
# it should be neighbor

cd /Volumes/YOUR_SHARED_FILE_NAME/



**NOTES**
Files/folders must be created in the VM or the server will complain when you try to start it (lack of permissions).
If when editing on your host, VSCode complains that you have insufficient permissions to save a file, edit it in your VM. If it complains in your VM, edit on your host. Basically, you have to keep VSCode open on both your host and VM.

## Editors
### react-frontend VSCode setup
Add `"javascript.preferences.importModuleSpecifier": "relative"` to settings.json
TS with create react app 2 doesn't allow absolute imports because of the Babel compiler
