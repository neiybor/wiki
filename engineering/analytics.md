<!-- TITLE: Analytics -->
<!-- SUBTITLE: A quick summary of Analytics -->

# Analytics
## Automating Kissmetrics report queries for Grow
1. Create report in KM
2. Run / schedule job
	1. For a cohort report schedule the report with a date like
		1. `rake api:pull_km REPORT_ID={report ID} REPORT_BUCKET=neiybor-kissmetrics-production REPORT_KEY={report name}.csv DATE_RANGE='{"type":"after", "date": "{date}"}'`
		2. E.g. `rake api:pull_km REPORT_ID=395982 REPORT_BUCKET=neiybor-kissmetrics-production REPORT_KEY=visit_to_registration.csv DATE_RANGE='{"type":"after", "date": "2018-01-06"}'`
		3. Replace the report ID, report name, and date
	2. For a people report schedule the report like this
		1. `rake api:pull_km REPORT_ID={report ID} REPORT_BUCKET=neiybor-kissmetrics-production REPORT_KEY={report name}.csv`
	3. For a custom report (e.g. cohort with a population) pass a `QUERY_URL` parameter
		1. Run the report you want in Kissmetrics UI with Chrome dev tools open.
		1. See the JSON it posts to create the query.
		1. Upload it to a public location (like the neiybor-public S3 bucket)
		1. Pass that URL to the job in the `QUERY_URL` parameter
		1. Like QUERY_URL=https://neiybor-public.s3-us-west-1.amazonaws.com/analytics/KMCohortWithPopulationFormatted.json
3. Create a presigned URL for the csv file in S3 `aws s3 presign --expires-in 63072000 neiybor-kissmetrics-production/{report name}.csv`
4. Import data into Google sheets using the IMPORTDATA() function, passing in the URL generated in the previous step

Operations and Marketing is using this sheet to organize Kissmetric export requests: https://docs.google.com/spreadsheets/d/1sCKheSExk0B9hn5xn-0Y9Mh09CentXsps5Tmb6bKzKY/edit?usp=sharing