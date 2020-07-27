<!-- TITLE: Live Troubleshooting -->
<!-- SUBTITLE: How to troubleshoot live -->

# Database Fixes
if you have to make hanges to the production databases, this is the section for you

there are two ways to query/fix the database in production: 1) the rails Active Records and 2) access directly to the postgresql database.

which of these methods you use depends on your use case. here is how to gain access to both:

## Active Records in Rails
you must have an authentiated heroku account to use the rails console. once you have heroku-cli configured and logged in, you can acess the rails console for any environment by doing the following:

```
heroku run --app=<heroku_app_name> rails c
```

this will log you into the rails console to be able to query the database through Active Records.

## Access to Postgreql (psql)
the connection string for the production postgresql can be found in LastPass in the "Prod DB Ops" document which is in the **Shared-DevOpsHigh** folder. 

once you get the connection string you can run the `psql` command from anywhere and have an SQL interface to the production database.
```
psql postgres://neighborOps:<secret_password>@prod-db.csygbnmyokub.us-east-1.rds.amazonaws.com:5432/neiybor_api_production
```
