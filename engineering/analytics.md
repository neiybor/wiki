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
		1. `rake api:pull_km REPORT_ID=394625 REPORT_BUCKET=neiybor-kissmetrics-production REPORT_KEY=total_registrations.csv`
3. Create a presigned URL for the csv file in S3 `aws s3 presign --expires-in 63072000 neiybor-kissmetrics-production/{report name}.csv`
4. Import data into Google sheets using the IMPORTDATA() function, passing in the URL generated in the previous step