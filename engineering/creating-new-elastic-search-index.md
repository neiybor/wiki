<!-- TITLE: Creating New Elastic Search Index and Migrating Listings -->

## CREATION AND MIGRATION PROCESS

1) Open 5-10 search pages and leave them untouched throughout the process. Document how many hits are returned in the console (`...Found x matching...`).

2) Pick the new version number: {number}. Run rake task to create and populate the new index. Document the start-time that the rake task began:

```text
    FOR LOCAL:      rake api:create_index_and_populate CUSTOM_INDEX_NAME='development-listings-{hostname}-v{number}'
	FOR STAGING:    heroku run CUSTOM_INDEX_NAME='staging-listings-v{number}' rake api:create_index_and_populate -a neighbor-api-staging
	FOR PROD:       heroku run CUSTOM_INDEX_NAME='production-listings-v{number}' rake api:create_index_and_populate -a neighbor-api
```

3) In config-management, set ELASTIC_SEARCH_INDEX_VERSION = {number}, to be version {number} of the index (this will cause all future listings to be added to the new index). Add this to all three .env files:

```text
.env.development.backend
.env.staging.backend
.env.production.backend
```

4) Create a PR for config-management and merge.

5) Run query to get the ids of the listings that were created during the rake task runtime of step 1. Use the documented start-time from step 1 and use UTC.

```sql
select id from listings where (created_at > '{start-time}' or updated_at > '{start-time}') and status = 'Published';
```


6) Run rake task to add the listings found in step 4 to the new index. Pass in a comma separated list of listing ids:


```text
	FOR LOCAL:      rake api:index_listings_by_id IDS='{id},{id},{id}'
	FOR STAGING:    heroku run IDS='{id},{id},{id}' rake api:index_listings_by_id -a neighbor-api-staging
	FOR PROD:       heroku run IDS='{id},{id},{id}' rake api:index_listings_by_id -a neighbor-api
```


7) Validate that the new index returns the correct search results by opening the same search 5-10 pages as in step 1. Confirm that they are the same and that the same number of hits in the console are returned. (Due to the fuzz function in the backend, on searches with many results the lat. and long. values can vary enough to slightly change the hit numbers. Listings on the edge of the search diameter can be fuzzed outside/inside the diameter with the new index. To account for this locally, comment out the fuzz function temporarily.)

8)  IN STAGING: Test rollback. Remove the ELASTIC_SEARCH_INDEX_VERSION ENV VAR and confirm that the search uses the previous index.

9) In case of rollback, use the start-time from step 1 and the query from step 4 to add to the old index all listings created/updated since the ENV VAR change.


## STEPS FOR DEVELOPER TEAM (to set up everyone's local search index)


1) Run rake task to create and populate the new index:

```text
rake api:create_index_and_populate CUSTOM_INDEX_NAME='development-listings-{hostname}-v2'
```

2) Pull config-management.