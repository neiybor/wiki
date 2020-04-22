<!-- TITLE: Dev Setup -->
<!-- SUBTITLE: Setting up dev environments -->

See also [Mac Setup](/engineering/macsetup)
For debugging see [Setup Issues](/engineering/setup-issues)

-----
# Pre-dev Setup
1. Sign up with Zenefits to get your neighbor email.
1. Follow the Slack invite from Joseph and setup your account.
1. Follow the LastPass invite from Joseph and setup your account.
1. Login to Google Calendar from new neighbor email and admin have Joseph setup an onboarding meeting.

# Dev Setup
## Setup BIOS and OS
* Setup BIOS and OS
	1. Plug into Ethernet / connect wifi
	1. Install Windows and login
	1. Plugin the flash drive with Ubuntu
	1. Go to https://forums.lenovo.com/t5/ThinkPad-P-and-W-Series-Mobile/Thinkpad-P50-can-no-longer-get-into-BIOS-from-boot-screen-using/td-p/3498366 and follow the 9 steps to get into the right BIOS
	1. Update BIOS
		1. Security -> Secure Boot
			1. Set to Disabled
		1. Startup -> Boot
			1. Move USB HDD... to top of boot order
		1. Graphics (For P51)
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
		1. Install [Lastpass addon](https://chrome.google.com/webstore/detail/lastpass-free-password-ma/hdokiejnpimakedhajhdlcegeplioahd?hl=en)
	1. Get access to repos
		1. Neiybor Github account
	1. Setup your AWS account
		1. For the admin adding the new hire: make sure the new hire is added to the ‘engineers’ group
			1. Hint: Minimum password length is 16 chars
		1. New hire: login at https://console.aws.amazon.com/console/home?region=us-east-1 and change your password
		1. Admin: Make the user an access key
			1. Send them “You will need the following to setup the AWS CLI while the setup-dev script runs”
			1. Send them the key and secret
			1. Send them “default region: us-east-1”
			1. Send them “skip default output format”


## Get & run setup script
* Get & run setup script (recommended)
	1. Replace `<VALUES>` with your info
	```
	#install git
	sudo apt update
	sudo apt upgrade
	sudo apt install git
	# configure git
	git config --global color.ui true
	git config --global user.name "<FIRSTNAME LASTNAME>"
	git config --global user.email "<YOU>@neighbor.com"
	ssh-keygen -t rsa -b 4096 -C "<YOU>@neighbor.com" #use default file location on prompt
	```
	2. Upload ssh key that generated to your github account
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
	1. Try logging in to DB
	```
	psql -U dev neiybor_api_dev
	# password: dev
	```
	1. Try running backend server
		1. cd rails-api
		1. Start server on port 3001:
			1.` rails s -p 3001`
		1. Open browser to http://nbr.pizza:3001
		1. Verify you get a valid JSON response
		1. `Ctrl + c` in terminal to shut down backend server
	1. Populate the search index for your local enviornment:
		1. Run `PERCENT=100 rake api:index_listings`
		1. Run `rake:api test_users`
	1. Try running frontend server
		1. `cd react-frontend`
		1. Start the node server with HTTPS and the correct hostname by running:
			1. `npm run start`
		1. Browser should open to https://nbr.pizza/
		1. `Ctrl + c` in terminal to shut down backend server
	1. Try running entire dev environment
		1.  `start` 
		1. Verify that localstack spins up, backend starts, frontend starts.
		1. Visit https://nbr.pizza to verify that the environment works

## Install tools
* Install tools
	1. Install favorite editor
		1. VS Code
			1. sudo snap install code --classic
			1. Install Debugger for Chrome extension
				1. Follow setup instructions on extension page
	1. Install React Dev Tools for Chrome
	1. Chrome extension to block Google Analytics
		1. Add *.neighbor.com and neighbor.com to the list of blocked sites
		1. Another good alternative: Ghostery https://chrome.google.com/webstore/detail/ghostery/mlomiejdfkolichcflejclcbmpeaniij?hl=en
	1. Install Heroku CLI (google how to do it) and run heroku plugins:install heroku-config
	1. Setup default git editor to be VSCode, Emacs, VI, Gedit, …
		1. git config --global core.editor "code"
	1. Configure Chrome to launch listening on a debug port
		1. Save [Google Chrome](https://drive.google.com/open?id=1kRKIRivPSPq8XD2Lspx6ZMV37plkHu4-) to `~/.local/share/applications/google-chrome.desktop`
		1. Change Path variable to your home directory
	1. Tutorials
		1. [JavaScript/ES6](https://www.codecademy.com/learn/introduction-to-javascript)
		1. Typescript
			1. [5 Minute Intro](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)
		1. [Ruby/Rails](https://www.coursera.org/learn/ruby-on-rails-intro/home/welcome)
		1. [React](https://reactjs.org/tutorial/tutorial.html)
			1. [Quick start guide](https://reactjs.org/docs/hello-world.html)
		1. [Redux](https://redux.js.org/introduction/getting-started)
		1. [TypeScript React Starter](https://github.com/Microsoft/TypeScript-React-Starter#typescript-react-starter)


**NOTES**
Files/folders must be created in the VM or the server will complain when you try to start it (lack of permissions).
If when editing on your host, VSCode complains that you have insufficient permissions to save a file, edit it in your VM. If it complains in your VM, edit on your host. Basically, you have to keep VSCode open on both your host and VM.

## Editors
### react-frontend VSCode setup
Add `"javascript.preferences.importModuleSpecifier": "relative"` to settings.json
TS with create react app 2 doesn't allow absolute imports because of the Babel compiler

## Deprecated
* Optional setup
		1. Setup for Android transpiling development
			1. `sudo apt install default-jdk`
			1. Enable KVM in BIOS for hardware accelerated virtualization
				1. Security -> Virtualization
				1. Enable both Virtualization Technology and Vt-d Feature
			1. Install [Android Studio](https://developer.android.com/studio/install)
		1. Open SDK Manager
			1. Install Android SDK versions 25 and above
		1. [Walk through tutorial of creating your first Android app](https://developer.android.com/training/basics/firstapp/creating-project)
		1. After creating app, go to the “Run your app” -> “Run on an emulator” step of the tutorial
		1. If you get an error about syncing gradle files click “Try Again”
		1. Install Gradle
		1. https://gradle.org/next-steps/?version=4.9&format=bin
		```
		cd ~/Downloads/
		sudo mkdir /opt/gradle
		sudo unzip -d /opt/gradle gradle-4.9-bin.zip
		ls /opt/gradle/gradle-4.9
		```
		1. Add following to .bashrc (replacing `<USER>` with your username)
		```
		export JAVA_HOME="/usr/lib/jvm/default-java"
		export ANDROID_HOME="/home/<user>/Android/Sdk"
		export PATH="${PATH}:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin"
		export PATH=$PATH:/opt/gradle/gradle-4.9/bin
		```
		1. `source .bashrc`
		1. Remove old Android SDK debugger IF it exists
			1. `sudo rm /usr/bin/adb`
		1. Install Cordova
			1. `sudo npm install -g cordova`
			1. `cd ~/neiybor/transmogrifier`
			1. `npm install`
			1. `cordova platform add android`
		1. Build staging app
			1. `cordova build`
		1. Install apk on emlulator (i.e. after emulator started by Android Studio or command line)
			1. `adb -s emulator-5554 install -r ~/neiybor/transmogrifier/platforms/android/app/build/outputs/apk/debug/app-debug.apk`
		1. Build staging app for release to Play Store for testing
			1. `cordova build --release --prod`
