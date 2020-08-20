* <!-- TITLE: Macdocker -->
<!-- SUBTITLE: A quick summary of Macdocker -->

# Mac / Docker setup

## Prereqs

1. Install Docker
	* get Docker for Mac from docker website
2. Install Homebrew
2. Xcode  commandline tools (might have come with Homebrew)
2. Install and configure AWS CLI
	* brew install awscli
	* Configure AWS API keys in environment. These keys can be found in (aws)[https://console.aws.amazon.com/iam/home?region=us-east-1#/security_credentials]. Easiest way is to add them to your bash/zsh profile so they get loaded into your shell. If you want to be advanced you can look at https://github.com/miquella/vaulted.
	  ```sh
export AWS_ACCESS_KEY_ID="redacted"
export AWS_SECRET_ACCESS_KEY="redacted"
		```
2. Create an ssh key and configure Github
		1. `ssh -keygen -t rsa` (you can skip this step if you already have an SSH key you would like to use)
		2. `cat ~/.ssh/id_rsa.pub | pbcopy` # this will copy the public key to the keyboard buffer
		3. go to `https://github.com/settings/keys` and click on "New SSH key"
		4. paste what's in your keyboard buffer into the "Key" areas, give it a name and click "Add SSH key"
		5. in a terminal, enter `ssh-add -K` to add the ssh key to the ssh-agent (so you don't have to enter the password every time)

## local system setup
1. Clone repos
	* NOTE: the docker config uses relative paths so make sure these three repos are on the same level of the diretory structure as each other
	* `git clone git@github.com:neiybor/react-frontend.git`
	* `git clone git@github.com:neiybor/rails-api.git`
	* `git clone git@github.com:neiybor/config-management.git`
2. config `rails-api` for the docker dev environment
	* `cp config-management/docker/.env.docker.backend rails-api/.env`
2. config `react-frontend` for the docker dev environment
	* `cp config-management/docker/.env.docker.frontend react-frontend/.env`
2. update `/etc/hosts` file
	* add `nbr.pizza` to the localhost entry of `/etc/hosts` file
	* add `api.nbr.pizza` to localhost entry of `/etc/hosts` file
		```
		127.0.0.1 nbr.pizza
		127.0.0.1 api.nbr.pizza
		```
		
2. run `cd config-management/docker && ./setup.sh` to do the following:
	* build docker containers
	* create needed SNS topics
	* setup and migrate api db
2. this will startup the docker containers in the background (daemon mode with -d). verify all containers are up and running by entering `docker ps`
		* you should see the following containers running:
			* docker_haproxy_1
			* docker_frontend_1
			* docker_api_1
			* docker_db_1
			* docker_localstack_1
2. browse to website by opening <a href="https://nbr.pizza" target="_blank">https://nbr.pizza</a>. Ensure the browser is using https when visitng nbr.pizza otherwise it won't work.

## common activities
the `setup.sh` script above created several listings and users into the database. this section contains info about these users and listings for manual testing purposes.

### users
* host
	* email: `bothost@neighbor.com`
	* password: password
* renter
	* email: `botrenter@neighbor.com`
	* password: password
* admin
	* email: `sean@neiybor.com`
	* password: password


## heroku setup
`brew tap heroku/brew && brew install heroku` # to install the heroku-cli
`heroku plugins:install heroku-config` # to install config plugins for push and pull

## troubleshooting

### Inspect logs
`docker-compose logs [-f] [service_name]`

`docker-compose logs -f` - shows all logs (with tag on each line to indicate source service)
`docker-compose logs -f api` - shows just the api logs

### PSQL 
`psql -h localhost -U dev -d neiybor_api_dev`

will prompt for password which is `dev`

### Rails Console

`docker-compose run api rails c`

* update a user to be an admin
	* `User.find_by(email: 'kirkby@neighbor.com').update(admin: true)`

* count of listings for a given user
```
user_id = User.where(email: 'kirkby@neighbor.com').pluck(:id)[0]
Listing.where(user_id: user_id).count
```
