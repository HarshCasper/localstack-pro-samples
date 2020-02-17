# LocalStack Demo: Athena Queries over S3 Files

Simple demo application illustrating how to run Athena queries over S3 files locally, using LocalStack.

## Prerequisites

* LocalStack
* Docker
* Node.js / `npm`
* `make`

## Installing

To install the dependencies:
```
make install
```

## Starting LocalStack

Make sure that LocalStack is started with the following `SERVICES` configuration:
```
LOCALSTACK_API_KEY=... DEBUG=1 SERVICES=serverless,athena localstack start
```

## Running

Start the app locally and run the Athena test queries:
```
make run
```

The demo script performs the following actions:

1. Create an S3 bucket and upload test data (CSV files with person details) to the bucket
2. Run queries to create the table metadata in Athena
3. Running a simple query over the test file - querying the number of users by gender (male/female)
4. Downloading the query results from the S3 results bucket

You should see something similar to the following log output in the terminal:
```
$ ./run.sh
Uploading test data to S3...
make_bucket: athena-test
upload: data/data.csv to s3://athena-test/data/data.csv         
Running queries to create database and table definitions...
Starting SELECT query over data in S3. Query ID: c842d095
S3 query output location: s3://athena-test/results/Unsaved/2020/02/16/c842d095
download: s3://athena-test/results/Unsaved/2020/02/16/c842d095/results.csv to ../../../../../tmp/c842d095.results.csv
Query result downloaded from S3:
gender,1
Male,49
Female,51
```

## License

This code is available under the Apache 2.0 license.
