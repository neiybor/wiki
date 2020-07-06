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
	* configure AWS API keys in environment

## local system setup
1. Clone repos
	* NOTE: the docker config uses relative paths so make sure these three repos are on the same level of the diretory structure as each other
	* `git clone git@github.com:neiybor/react-frontend.git`
	* `git clone git@github.com:neiybor/rails-api.git`
	* `git clone git@github.com:neiybor/config-management.git`
2. build with docker-compose
	* `cd config-management/docker`
	* `docker-compose build`
	* this will take a while to build espescially the `react-frontend` repo
2. startup with docker-compose
	* `docker-compose up`
  * in a separate window, verify all containers are up and running:
		* `docker ps`
		* you should see the following containers running:
			* docker_haproxy_1
			* docker_frontend_1
			* docker_api_1
			* docker_db_1
			* docker_localstack_1
2. browse to website by opening [https://nbr.pizza]