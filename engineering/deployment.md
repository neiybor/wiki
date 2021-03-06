<!-- TITLE: Deployment -->
<!-- SUBTITLE: how to deploy Neighbor code -->

# config vars
To get config vars pushed to the right environment, checkout the `config-management` project and cd into the directory related to the project you want to update the vars for. the `config-management` repo is the source of truth for the config vars.

in the application directory, do an `ls -al` to see the dotEnv files for each environment. they will be named something like `.env.development.frontend`. make the change to the var you wish to update/add in that file and save it. then deploy it to the proper environment by issuing the following command:

`heroku config:push -f <env_file> --app=<heroku_app_name>`

where `<env_file>` is the file name you updated above and `<heroku_app_name>` is the application name as stated in heroku.

here is a list for the current (2020-07-25) `<heroku_app_name>`s for frontend and api:

* react-frontend staging: **neiybor-frontend-staging**
* react-frontend production: **swn-frontend**
* rails-api staging: **neighbor-api-staging**
* rails-api producton: **neighbor-api**

example for staging on front end:
```
git clone git@github.com:neiybor/config-management.git
cd config-management/frontend
vi .env.staging.frontend # make changes to file and save
heroku config:push -f .env.staging.frontend --app=neiybor-frontend-staging
```

**NOTE**: if you get an error `config:push is not a heroku command`, you need to install the heroku-config addon: `heroku plugins:install heroku-config`

# Production deployment
Deployment for production environments happens when you push something into master. this is true for `react-frontend` and `rails-api`. 

